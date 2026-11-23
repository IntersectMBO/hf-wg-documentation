# PlutusV4 Script Context

Dijkstra introduces PlutusV4 so scripts can see the new transaction and ledger structures: guards, nested transactions, account deposits and intervals, and the Dijkstra-era certificate and purpose set.

This page is the context schema, not the whole PlutusV4 language. New builtins, for example CIP-168 `Value` helpers, are gated on the same protocol version but tracked by the Plutus team separately. CIP-156 `multiIndexArray` is not in Dijkstra.

There is no standalone CIP titled "PlutusV4 Script Context". The schema is specified in pieces in CIP-112, CIP-118, CIP-159, and the ledger `EraPlutusTxInfo 'PlutusV4 DijkstraEra` instance.

* **CIP:** none. See [CIP-112](https://cips.cardano.org/cip/CIP-0112), [CIP-118](https://cips.cardano.org/cip/CIP-118), [CIP-159](https://cips.cardano.org/cip/CIP-0159)
* **Overview:** [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), PlutusV4 Script Context
* **Ledger:** `Cardano.Ledger.Dijkstra.TxInfo`, `EraPlutusTxInfo 'PlutusV4 DijkstraEra`
* **Plutus team notes:** [2026-09-09 update](https://updates.cardano.intersectmbo.org/2026-09-09-plutus-core/). V4 context encoding work uses `List` for product types rather than `Constr`

***

## Core semantics changes

Implications, why it concerns you, and what needs to be updated in response.

### What the ledger actually does

A script declared as PlutusV4 is given a V4 `ScriptContext` / `TxInfo`. Relative to V3, scripts can observe at least:

* Guarding purpose and the set of guards that ran (CIP-112).
* `txInfoSubTxs` on a top-level Guard in a nested batch (CIP-118). Spend, mint, and withdraw scripts inside a child do not see siblings.
* `txInfoDirectDeposits` and `txInfoAccountBalanceIntervals` (CIP-159 Phase 1, ADA-only).
* Dijkstra-era certificates and purposes as translated by `toPlutusTxCert` / `toPlutusScriptPurpose` for V4.

PlutusV1 to V3 still exist. They cannot be mixed onto a transaction that uses sub-transactions or top-level guards except via CIP-118 isolation mode, where the top-level must stand alone.

Cost models: V4 has its own cost model in protocol parameters, same pattern as V2 and V3. Scripts using V4 builtins that the Plutus team gated on this protocol version will fail evaluation on Conway nodes.

### Why this concerns wallets, explorers, indexers, and pool tools

**Compiler authors and dApp teams.** This is a new language version. Compilers must emit V4 envelopes, new context decoders, and new purpose constructors. Existing V3 scripts keep working on transactions that do not use Dijkstra-only structure.

**Indexers.** Redeemer tags and script-hash maps include V4 and Guarding. "Which Plutus version ran?" dashboards need a fourth bucket.

**Wallets.** They do not decode `TxInfo`, but they must attach the right language tag and redeemers when a dApp asks to run a V4 script.

**Auditors.** Any script that pattern-matches a closed V3 context will mis-parse a V4 context if someone feeds it the new bytes. That is a compiler and wrapper problem, not a ledger surprise.

### What to update

1. Aiken, Plutus Tx, OpShin, Scalus, Helios: V4 `ScriptContext` types, purpose enum, cost model.
2. Off-chain context mocks used in unit tests.
3. Blueprint / CIP-57 metadata: language version V4.
4. Indexers: `plutus_v4` script type, new purpose tag, new `TxInfo` JSON if you project context.
5. Guardrails and cost-model governance: a V4 cost model must be named in the constitution and guardrails before it can be updated the Conway way.

***

## Breaking API changes

Why it was unavoidable, and what needs to be updated in response.

Script context is an on-chain ABI. Adding fields or purposes without a new language version would silently change what V3 scripts see. V4 is the compatibility boundary.

### Wire format

The script context itself is not in the CDDL. It is built by the ledger and passed to the script as Plutus data, so its shape is defined by `plutus-ledger-api` and the ledger's translation code. What the CDDL does carry is everywhere a script or language can appear. PlutusV4 adds one value to each of those. It also changes one thing every Plutus transaction uses: the old array form of redeemers is gone. A Conway encoder that still writes redeemers as an array produces transactions that Dijkstra rejects, even when no V4 script is involved.

| CDDL rule | Change from Conway | What your tooling must do |
| --- | --- | --- |
| [`script`](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L393-L399) | Adds `[4, plutus_v4_script]`. | Handle the new tag in reference scripts and script-hash calculation. |
| [`language`](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L32) | Range grows from `0 .. 2` to `0 .. 3`; `3` is PlutusV4. | Used in the script data hash. Extend any closed enumeration. |
| [`cost_models`](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L756-L762) | Key `3` is now the PlutusV4 cost model. | Map key 3 to V4 in protocol-parameter codecs. |
| [`transaction_witness_set` key 8](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L874) | New. `nonempty_set<plutus_v4_script>`. | Decode and encode witness key 8. |
| [`auxiliary_data_map` key 5](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L933) | New. `[* plutus_v4_script]`. | Accept V4 scripts in auxiliary data. |
| [`redeemers`](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L888-L892) | Map form only. Conway also allowed [an array of redeemers](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/conway/impl/cddl/data/conway.cddl#L785-L791). | Always encode redeemers as a map keyed by `[tag, index]`. This applies to every Plutus transaction, not only V4. |
| [`redeemer_tag`](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L894-L901) | Adds `6 ; guarding`. | See [Guard Scripts](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/observe-script-type-guard-scripts). |

**Not in the CDDL.** The `ScriptContext` / `TxInfo` layout (field order, the `List` versus `Constr` encoding, `txInfoGuards`, `txInfoSubTxs` and the CIP-159 fields) comes from `plutus-ledger-api` and the ledger's `toPlutusTxInfo`. The ledger's upgrade parameters also require a `plutusV4CostModel` value at the hard fork.

Links go to the Dijkstra CDDL at cardano-ledger commit [`8631831`](https://github.com/IntersectMBO/cardano-ledger/tree/863183157cc39c48615078eab85389766bdc695b) (23 November 2026). The CDDL is not frozen yet, so check the line before relying on it.

### Wire and query contract

| Channel          | Shape                                                                                                                                           |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| Script envelope  | New language constructor PlutusV4                                                                                                               |
| Redeemer purpose | Adds `Guarding`. Nested batches index purposes per level.                                                                                       |
| V4 `TxInfo`      | V3 fields plus guards, optional `txInfoSubTxs`, and CIP-159 account fields                                                                      |
| Encoding note    | Plutus team is moving V4 product types to `List` encoding to cheapen decode. Consume the frozen V4 spec, not a V3-shaped `Constr` mental model. |
| PParams          | `costModels.PlutusV4`, or the name the node JSON actually exposes                                                                               |
| Ledger errors    | `DijkstraContextError` wrapping Conway errors plus sub-transaction context failures                                                             |

Do not assume field order from a blog post. The ledger `toPlutusTxInfo` instance is the source of truth until a CIP freezes the V4 ABI.

### What to update

* Closed-world purpose enums in every SDK.
* Any hand-rolled `ScriptContext` decoder in production scripts. Those should use compiler-generated types anyway.
* Node query JSON that lists cost models.

***

## New features

What new capabilities it unlocks that you might want to start thinking about.

* **Scripts that understand Dijkstra.** Without V4, guards, children, and account deposits are invisible, which is why CIP-118 forbids old languages on those transactions.
* **Cheaper shared policy.** One V4 guard sees the batch. Child spend scripts stay small.
* **Account-aware validators.** A V4 script can require "this transaction deposited at least N to account A" or "account A's balance is in \[L, U)" without a UTxO state machine.
* **Language-side V4 builtins, separate track.** Selected `Value` builtins. Useful, but they are not the script-context item. Do not document CIP-168 as this page.

Upgrade scripts only when they need the new fields. Leaving V3 on a simple spend remains valid.
