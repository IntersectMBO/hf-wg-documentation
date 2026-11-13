# Nested Transactions

A Dijkstra transaction may carry sub-transactions: children that need not pay their own fee, need not be balanced, and must not carry collateral. The top-level transaction supplies fee and collateral for the whole batch. The ledger applies the batch as one unit. Individual children would be rejected if submitted alone.

This is how Dijkstra supports atomic swaps, fee sponsorship, and Babel-fee style matching without a second round-trip on chain. Off-chain matching is still required. An unbalanced child cannot enter the mempool by itself.

Nested transactions depend on CIP-112 Guard scripts and on the PlutusV4 script context. A transaction that contains sub-transactions or top-level guards cannot run PlutusV1 to V3 scripts except through the isolation mode described below.

**CIP:** [CIP-118 Nested Transactions](https://cips.cardano.org/cip/CIP-118) (also [CIP-0118 on GitHub](https://github.com/cardano-foundation/CIPs/tree/master/CIP-0118))
**Overview:** [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), Nested Transactions (CIP-118)
**Ledger umbrella:** [cardano-ledger#5123](https://github.com/IntersectMBO/cardano-ledger/issues/5123)
**Depends on:** [Observe Script Type / Guard Scripts (CIP-112)](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/observe-script-type-guard-scripts), [PlutusV4 Script Context](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/plutusv4-script-context)

***

## Core semantics changes

Implications, why it concerns you, and what needs to be updated in response.

### What the ledger actually does

`TxBody` grows a list of sub-transactions. A sub-transaction has its own body, witness set, and optional auxiliary data. It cannot contain another level of sub-transactions, a fee field, collateral inputs, or a collateral return. The CDDL rejects those cases.

Value preservation is checked on the batch: inputs and outputs of the top-level plus every child, plus CIP-159 direct deposits where present. Fees are paid only by the top-level. Collateral is provided only by the top-level and covers every script in the batch. If any phase-2 script in the batch fails, the whole batch is invalid and collateral is collected. The ledger does not apply the children that passed.

Inputs of every level must already exist in the UTxO set before the batch is applied. Children cannot spend each other's outputs inside the same batch. That closes flash-loan patterns that create and spend inside one batch.

Script context is isolated for ordinary purposes. A spending or minting script inside a child sees that child's `TxInfo`, not the siblings and not the parent. Top-level Guard scripts from CIP-112 are the exception. They see the full batch, including `txInfoSubTxs`. A child can list `requiredTopLevelGuards`. The parent must run those guards.

Total serialized size of the batch is bounded by `maxTxSize`.

**Legacy isolation mode.** If the top-level still uses PlutusV1 to V3, the ledger validates that top-level as if it were alone. It must balance by itself. It must not rely on children for scripts or datums. Its guards may contain key credentials, preserving required-signer behaviour, but must not contain script credentials. Children in that mode must balance among themselves. This is a compatibility hatch, not the default path.

### Why this concerns wallets, explorers, indexers, and pool tools

**Wallets and dApp SDKs.** Building a payment is no longer one `TxBody` and one witness set. A wallet may sign a child that is unbalanced on purpose and hand it to an aggregator. The aggregator builds the parent, adds fee and collateral, attaches required guards, and submits once. CIP-30, CIP-185, and serialization libraries that can only sign a full Conway transaction will not speak this protocol.

**Explorers and indexers.** One ledger object now contains several transaction IDs. Reward, UTxO, and script-execution views have to attribute each input, output, mint, and withdrawal to the level that declared it, while treating the batch as the atomic unit for "did this land?"

**Mempool and SPOs.** Only the completed batch is a mempool citizen. Relays do not gossip naked children. Phase-2 runs once for the batch, which is the DoS control.

**Plutus developers.** Scripts that inspect "the whole transaction" from a spend purpose will not see sibling legs. If a protocol needs a batch-wide invariant, that invariant belongs in a top-level guard, not in a spend validator on one child.

### What to update

1. Transaction construction libraries (cardano-cli, cardano-api, Lucid, Mesh, CSL, pallas, and similar SDKs): encode `subTxs`, `requiredTopLevelGuards`, per-level witness sets, and batch balancing.
2. Wallet signing flows: sign a child without claiming it is a submittable transaction. Refuse to submit a child to `submitTx`.
3. Indexers: new tables for parent to child, per-level redeemers, per-level auxiliary data. Do not flatten children into extra inputs of the parent without recording the boundary.
4. Explorer UX: show a batch as a tree. Link each child ID. Explain that fee and collateral sit on the parent.
5. Aggregator, Babel-fee, and DEX off-chain matchers: this is the on-chain construct those products have been waiting for. CIP-118 does not define a standard off-chain matching protocol. That remains product work.
6. Phase-2 budgeting tools: collateral and execution units are scoped to the parent.

***

## Breaking API changes

Why it was unavoidable, and what needs to be updated in response.

A Conway `transaction_body` has no slot for children. Adding one is an era change. Combined with CIP-176, the block no longer stores bodies and witnesses in segregated arrays, which is what makes nested encoding tractable.

### Wire and query contract

| Channel | Shape |
| --- | --- |
| Top-level `transaction_body` | New field for one or more `sub_transaction` values. CIP drafts have used body index 23. CIP-159 also discussed 23 for `direct_deposits`. Bind the frozen Dijkstra CDDL, not a single CIP README number. |
| `sub_transaction` | `[sub_transaction_body, transaction_witness_set, auxiliary_data / nil]`. No `isValid`, no fee, no collateral. |
| `required_top_level_guard` | `[credential, plutus_data / nil]` on the child |
| `guards` | CIP-112 field on parent and child |
| Redeemers | Indexed per level. A child's spend redeemer 0 is not the parent's spend redeemer 0. |
| PlutusV4 `TxInfo` | `txInfoSubTxs` populated only for top-level Guard purposes |
| ApplyTx errors | Nested failure type wrapping the child transaction ID. See ledger `SubTxContextError` and nested predicate failures. |

Any decoder that walks "the" witness set of "the" transaction will miss child witnesses. Any fee estimator that looks only at the parent body will under-price the batch.

### What to update

- CBOR and CDDL bindings in every language.
- Submit paths: reject children submitted as top-level. Accept parents that contain them.
- Ogmios, Koios, and GraphQL transaction JSON: add `subTransactions`, `requiredTopLevelGuards`, and per-level redeemers.
- Formal spec and conformance tests follow ledger issue #5123 milestones.

***

## New features

What new capabilities it unlocks that you might want to start thinking about.

- **Atomic unbalanced swaps.** Alice signs a child that is short asset A and long ADA. Bob's parent supplies A and takes the ADA. One ledger step. No escrow script is required for the matching itself. Guards can still enforce policy.
- **Fee and minUTxO sponsorship.** A dApp parent pays fee, collateral, and the min-ADA a user's child cannot cover. This replaces "please send me 2 ADA first".
- **Babel fees at the ledger edge.** A matcher accepts a child that does not pay ADA fees and attaches an ADA-paying parent. CIP-118 does not itself price the native-asset leg. That stays off-chain.
- **Batch-wide policy via guards.** A protocol can require "this parent ran guard G with redeemer R" before any child is meaningful. Children request that with `requiredTopLevelGuards`.
- **Script sharing across the batch.** Witnessed and reference scripts are shared. Datums are not. Place datums per level.

Do not wait for Peras. Nested transactions activate with Dijkstra Phase 1. Do not implement this without CIP-112 and PlutusV4. The three are one product.
