# Reference Script Pricing and Limits

Conway already charges for reference scripts and already caps their total size. The price per byte is a protocol parameter, `minFeeRefScriptCostPerByte`, 15 lovelace per byte on mainnet. The tier width, tier multiplier, and per-transaction / per-block caps were hardcoded in the ledger: 25,600-byte stride, multiplier 1.2, 200 KiB per transaction and 1 MiB per block.

Dijkstra lifts those hardcoded pieces into protocol parameters so governance can change them. The formula does not change on hard-fork day if genesis copies the Conway constants. What changes is that the constants become visible, serialised, and, after constitution and guardrails updates, updatable.

**CIP:** none. Conway behaviour lives in [ledger ADR 009](https://github.com/IntersectMBO/cardano-ledger/blob/master/docs/adr/2024-08-14_009-refscripts-fee-change.md).
**Overview:** [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), Reference Script Pricing and Limits
**Do not confuse with:** [Fee Function Update (Reference Inputs)](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/fee-function-update-reference-inputs), [Fair Min Fees (CIP-23)](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/fair-min-fees-conditional)
**Ecosystem signal:** Ogmios Dijkstra encoders already expose `refScriptCostStride`, `refScriptCostMultiplier`, `maxRefScriptSizePerTx`, `maxRefScriptSizePerBlock`.

***

## Core semantics changes

Implications, why it concerns you, and what needs to be updated in response.

### What the ledger actually does

Collect every reference script on the transaction's spent and referenced inputs, used or not. Sum the raw script bytes, not the CBOR tag or language wrapper. Apply the tiered function:

- first `refScriptCostStride` bytes at `minFeeRefScriptCostPerByte`,
- each further stride multiplies the per-byte price by `refScriptCostMultiplier`.

Reject the transaction if total reference-script bytes exceed `maxRefScriptSizePerTx`. Reject the block if the block-wide sum exceeds `maxRefScriptSizePerBlock`.

Conway shipped stride = 25,600, multiplier = 1.2, and hard caps in code. Dijkstra stores those four values on `PParams` next to the already-governable `minFeeRefScriptCostPerByte`.

Hard-fork-day behaviour matches Conway if and only if genesis uses the Conway numbers. Do not assume a price change at the fork.

### Why this concerns wallets, explorers, indexers, and pool tools

**Fee estimators** that baked 25600 and 1.2 into source must read the parameters for Dijkstra epochs. A later Parameter Change can move them.

**Governance UIs.** New keys need forms, but only after the Constitution appendix and the guardrails script name them. Until then the fields exist on-chain and cannot legally be changed. Same PARAM-01 / HARDFORK-05 story as CIP-23 and CIP-50.

**Indexers.** Epoch-param tables need four new columns. Do not overwrite Conway epochs with the new names.

**Block producers.** `maxRefScriptSizePerBlock` is now a visible consensus limit. Monitoring should treat it like `maxBlockBodySize`.

### What to update

1. `minfee` implementations: read stride, multiplier, and both caps from protocol parameters in Dijkstra. Keep constants for Conway.
2. DBSync, Koios, and Ogmios protocol-parameter JSON.
3. GovTool and Parameter Committee templates, after the constitution text exists.
4. Explorer fee breakdowns: show which tier a transaction landed in.
5. Guardrails script and constitution pull request. Without it the knobs are display-only.

***

## Breaking API changes

Why it was unavoidable, and what needs to be updated in response.

New updatable parameters can only be added in a new era. That is why they ship at Phase 1 even if the first values equal Conway's constants.

### Wire and query contract

| Channel | Shape |
| --- | --- |
| JSON PParams | `minFeeRefScriptCostPerByte` already present, plus `refScriptCostStride`, `refScriptCostMultiplier`, `maxRefScriptSizePerTx`, `maxRefScriptSizePerBlock`. Names as in ledger / Ogmios Dijkstra encoder. Confirm against node golden JSON. |
| Haskell | `dppMinFeeRefScriptCostPerByte`, `dppRefScriptCostStride`, `dppRefScriptCostMultiplier`, plus the two max-size fields on Dijkstra PParams |
| Guardrails / Plutus Data | New parameter indices once the script is updated |
| Genesis | Conway to Dijkstra upgrade PParams must supply the new fields |

Parsers that allow-list Conway keys will drop the new ones and then compute the wrong fee after the first Parameter Change.

### What to update

- Closed Conway PParams structs in Rust, Go, and TypeScript.
- Docs that say "stride and multiplier are hardcoded".
- Constitution appendix drafts. Economic vs technical grouping is a Parameter Committee decision. Do not invent the group here.

***

## New features

What new capabilities it unlocks that you might want to start thinking about.

- **Governable anti-DoS knobs.** If reference-script traffic becomes cheap or expensive relative to hardware, DReps can move stride, multiplier, or caps without an era.
- **Live dashboards.** Explorers can show the live curve instead of a wiki constant.
- **Capacity planning for SPOs.** The block-level cap is a first-class number next to block size and block execution units.

Still no change to how you attach a reference script. CIP-33 mechanics are untouched.
