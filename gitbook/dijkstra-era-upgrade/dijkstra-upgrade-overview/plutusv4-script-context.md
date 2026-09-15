# PlutusV4 Script Context

Dijkstra introduces PlutusV4 so scripts can see the new transaction and ledger structures: guards, nested transactions, account deposits and intervals, and the Dijkstra-era certificate and purpose set.

This page is the context schema, not the whole PlutusV4 language. New builtins, for example CIP-168 `Value` helpers, `dropList`, and `case` on `Data`, are gated on the same protocol version but tracked by the Plutus team separately. CIP-156 `multiIndexArray` is not in Dijkstra.

There is no standalone CIP titled "PlutusV4 Script Context". The schema is specified in pieces in CIP-112, CIP-118, CIP-159, and the ledger `EraPlutusTxInfo 'PlutusV4 DijkstraEra` instance.

**CIP:** none. See [CIP-112](https://cips.cardano.org/cip/CIP-0112), [CIP-118](https://cips.cardano.org/cip/CIP-118), [CIP-159](https://cips.cardano.org/cip/CIP-0159).
**Overview:** [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), PlutusV4 Script Context
**Ledger:** `Cardano.Ledger.Dijkstra.TxInfo`, `EraPlutusTxInfo 'PlutusV4 DijkstraEra`
**Plutus team notes:** [2026-09-09 update](https://updates.cardano.intersectmbo.org/2026-09-09-plutus-core/). V4 context encoding work uses `List` for product types rather than `Constr`.

***

## Core semantics changes

Implications, why it concerns you, and what needs to be updated in response.

### What the ledger actually does

A script declared as PlutusV4 is given a V4 `ScriptContext` / `TxInfo`. Relative to V3, scripts can observe at least:

- Guarding purpose and the set of guards that ran (CIP-112).
- `txInfoSubTxs` on a top-level Guard in a nested batch (CIP-118). Spend, mint, and withdraw scripts inside a child do not see siblings.
- `txInfoDirectDeposits` and `txInfoAccountBalanceIntervals` (CIP-159 Phase 1, ADA-only).
- Dijkstra-era certificates and purposes as translated by `toPlutusTxCert` / `toPlutusScriptPurpose` for V4.

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

### Wire and query contract

| Channel | Shape |
| --- | --- |
| Script envelope | New language constructor PlutusV4 |
| Redeemer purpose | Adds `Guarding`. Nested batches index purposes per level. |
| V4 `TxInfo` | V3 fields plus guards, optional `txInfoSubTxs`, and CIP-159 account fields |
| Encoding note | Plutus team is moving V4 product types to `List` encoding to cheapen decode. Consume the frozen V4 spec, not a V3-shaped `Constr` mental model. |
| PParams | `costModels.PlutusV4`, or the name the node JSON actually exposes |
| Ledger errors | `DijkstraContextError` wrapping Conway errors plus sub-transaction context failures |

Do not assume field order from a blog post. The ledger `toPlutusTxInfo` instance is the source of truth until a CIP freezes the V4 ABI.

### What to update

- Closed-world purpose enums in every SDK.
- Any hand-rolled `ScriptContext` decoder in production scripts. Those should use compiler-generated types anyway.
- Node query JSON that lists cost models.

***

## New features

What new capabilities it unlocks that you might want to start thinking about.

- **Scripts that understand Dijkstra.** Without V4, guards, children, and account deposits are invisible, which is why CIP-118 forbids old languages on those transactions.
- **Cheaper shared policy.** One V4 guard sees the batch. Child spend scripts stay small.
- **Account-aware validators.** A V4 script can require "this transaction deposited at least N to account A" or "account A's balance is in [L, U)" without a UTxO state machine.
- **Language-side V4 builtins, separate track.** `case` on `Data`, `dropList`, selected `Value` builtins. Useful, but they are not the script-context item. Do not document CIP-168 as this page.

Upgrade scripts only when they need the new fields. Leaving V3 on a simple spend remains valid.
