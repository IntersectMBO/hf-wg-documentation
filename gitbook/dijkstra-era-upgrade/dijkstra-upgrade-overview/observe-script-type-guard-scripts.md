# Observe Script Type / Guard Scripts

CIP-112 adds a script purpose that is not tied to spending, minting, withdrawing, certifying, voting, or proposing. The script runs because the transaction lists it. The transaction is invalid if that script does not run successfully.

The published CIP title is Observe Script Type. The ledger team renamed the concept to Guard during review. "Observer" sounds passive, and these scripts can fail the transaction. In Dijkstra code and CDDL the names are `guards`, `GuardingPurpose`, `RequireGuard`, and `Credential 'Guard`. Use Guard for the implemented feature. Mention Observe as the CIP title.

Guards are required by CIP-118 nested transactions, where children demand top-level guards, and by the PlutusV4 context, which adds the new purpose and `TxInfo` fields.

**CIP:** [CIP-112 Observe Script Type](https://cips.cardano.org/cip/CIP-0112) (also [CIP-0112 on GitHub](https://github.com/cardano-foundation/CIPs/blob/master/CIP-0112/README.md), original PR [#749](https://github.com/cardano-foundation/CIPs/pull/749))
**Overview:** [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), Observe Script Type / Guard Scripts (CIP-112)
**Ledger umbrella:** [cardano-ledger#5603](https://github.com/IntersectMBO/cardano-ledger/issues/5603)
**Used by:** [Nested Transactions (CIP-118)](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/nested-transactions)

***

## Core semantics changes

Implications, why it concerns you, and what needs to be updated in response.

### What the ledger actually does

A Dijkstra `TxBody` carries a `guards` set of credentials. For each guard:

- a key credential must be witnessed by a signature. This is the old `required_signers` job, moved here.
- a script credential requires the corresponding script to be present and evaluate successfully. Plutus guards need a redeemer under the Guarding purpose; native-script guards do not.

Listing a guard does not imply a UTxO spend, a mint, or a withdrawal. Shared policy no longer needs a dummy script input or a withdraw-zero staking trick. A zero mint does not trigger a minting script because zero mint entries are filtered out.

Native scripts gain a `RequireGuard` constructor. CIP JSON still says `"type": "observer"`. A native script can demand that a given guard credential is in the body's `guards` set.

`required_signers` / `reqSignerHashes` is no longer a witness-only side channel. Ledger work on #5603 includes "Switch role of reqSignerHashes from Witness to Guard". Treat Conway `requiredSigners` and Dijkstra `guards` as the same slot evolved, not as two independent lists, unless the final CDDL freezes them as distinct. Check the Dijkstra CDDL before writing a codec.

PlutusV4 is required to see the new purpose in script context. A transaction that lists script guards cannot carry PlutusV3-or-earlier scripts on the default path. That is the same rule as nested transactions.

### Why this concerns wallets, explorers, indexers, and pool tools

**dApp authors.** The recommended way to share one policy across many spends is now "put it in `guards` once", not "attach the same spend script to n extra inputs". Batching protocols that paid O(n·m) script executions can drop to O(1) for the shared check.

**Native and Plutus hybrids.** A native multisig can `RequireGuard` a Plutus policy without wrapping itself in a Plutus script.

**Wallets.** Transaction builders must collect guard redeemers and show them in signing summaries: this transaction runs policy X even though it does not spend X. Hardware wallet UIs that only list inputs, mints, and withdrawals will hide the actual authority.

**Indexers.** Redeemer tags grow a Guarding case. Script-purpose enumerations that are a closed Conway set will drop or reject Dijkstra redeemers.

### What to update

1. Transaction builders: API to add a guard credential plus optional redeemer or datum. Map Conway `requiredSigners` to Dijkstra `guards`.
2. Plutus toolchain (Aiken, Plutus Tx, OpShin, Scalus): `ScriptPurpose` = `Guarding`, or the final Plutus-side name, plus a context field listing executed guards.
3. Native-script JSON and CBOR: new constructor. Update CIP-1854 and other multisig parsers.
4. Indexers and explorers: show Guards next to signers, mints, and withdrawals. Attribute execution units to the Guarding purpose.
5. CIP-118 integrators: a child's `requiredTopLevelGuards` is a request that the parent put those hashes in `guards` and run them. Enforce that in the aggregator, not only in the ledger.

***

## Breaking API changes

Why it was unavoidable, and what needs to be updated in response.

New script purposes and native-script constructors cannot be added to PlutusV3. The era change is the compatibility break.

### Wire and query contract

| Channel | Shape |
| --- | --- |
| TxBody | `guards`: set of `Credential 'Guard` (key hash or script hash) |
| Redeemers | New tag / purpose `Guarding`, indexed into the guards set |
| Native script | New constructor `RequireGuard`. CIP JSON uses `"type": "observer"`. |
| PlutusV4 purpose | `GuardingPurpose` carrying index and script hash |
| PlutusV4 `TxInfo` | List of executed guard credentials. For top-level guards in a nested batch, `txInfoSubTxs` is also populated. See CIP-118. |
| Ledger Haskell | `guardsTxBodyL`, `mkGuardingPurpose`, `mkRequireGuard` on `Cardano.Ledger.Dijkstra` |

Closed enums for redeemer tags (spend, mint, cert, reward, vote, propose) fail closed-world decoders. Add the new tag. Do not reuse vote or propose.

### What to update

- Every language binding that pattern-matches script purposes.
- Hardware wallet attestation formats.
- Guardrails-script and constitution tooling are not directly affected unless a new protocol parameter is introduced for guard limits. CIP-112 itself is a structure change, not a protocol parameter.

***

## New features

What new capabilities it unlocks that you might want to start thinking about.

- **Replace withdraw-zero.** Any protocol whose only reason to touch a stake address was "run this script" should migrate to a guard. Cheaper, clearer, no accidental reward-account coupling.
- **Replace dummy mint and dummy spend.** Same migration for minting-policy-as-global-validator and extra script inputs used only to force a script to run.
- **Native scripts that can demand Plutus.** Treasury-style native scripts can require a Plutus guard without becoming Plutus themselves.
- **Batch policy for CIP-118.** The parent guard is the only script that sees every child. Product designs for atomic swaps and sponsored transactions should put cross-leg invariants there.
- **Required-signer continuity.** Ordinary "Alice must sign" still works. It is a key-credential guard. Update docs so users do not think required signers vanished.

Guards do not create a new address type and do not move value. For micropayments and account balances see CIP-159. For the context schema see PlutusV4.
