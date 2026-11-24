# Fee Function Update (Reference Inputs)

This item has no CIP. It changes the transaction minimum-fee function so reference inputs are priced. It is not CIP-23 Fair Min Fees. That is a pool margin floor. It is not the Conway reference-script surcharge. That is the next page.

Reference inputs (CIP-31) let a transaction mention a UTxO without spending it. Nodes still fetch, deserialise, and hold that UTxO for script context. Conway's min-fee formula charges `a · size(tx) + b` plus script-execution and reference-script terms. The referenced input bodies themselves were not a first-class extra term. Dijkstra adds that accounting.

Per the overview, parameters start hardcoded, with a later path to make them updatable protocol parameters. That is the same playbook Conway used for reference-script stride and multiplier.

* **CIP:** none
* **Overview:** [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), Fee Function Update (Reference Inputs)
* **Do not confuse with:** [Fair Min Fees (CIP-23)](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/fair-min-fees-conditional), [Reference Script Pricing and Limits](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/reference-script-pricing-and-limits)
* **Node scope:** [cardano-node#6634](https://github.com/IntersectMBO/cardano-node/issues/6634)

***

## Core semantics changes

Implications, why it concerns you, and what needs to be updated in response.

### What the ledger actually does

Minimum fee for a Dijkstra transaction is still deterministic and still checked in phase-1. The function gains a term that depends on the reference inputs the transaction lists. The ledger has two new coefficients for it, both in lovelace per byte. One prices the multi-asset part of each referenced output, and the other prices its datum. Follow the ledger implementation when coding. Do not treat this sentence as the formula.

The Dijkstra min-fee function doesn’t use those coefficients yet; it still calls the Conway fee function.

Spending inputs, minting, withdrawals, CIP-159 deposits, and CIP-118 children all still go through the existing size, execution, and reference-script terms. This page only adds the reference-input piece.

### Why this concerns wallets, explorers, indexers, and pool tools

**Every fee estimator.** Wallets, cardano-cli `transaction build`, Mesh, Lucid, CSL fee helpers, batchers, and "is this transaction balanced?" off-chain code that reimplements `minfee` will underpay if they keep the Conway function on Dijkstra transactions that use reference inputs. Underpaying is a phase-1 reject, not a silent overpay.

**dApps that reference large UTxOs.** Protocols that pass big inline-datum outputs in as reference inputs become more expensive. That is intended. Nodes pay I/O and RAM for those bytes.

**Explorers.** "Minimum fee" and "fee breakdown" panels need a new line item. Do not dump it into "reference script fee".

**This may be live on hard-fork day.** The coefficients are protocol parameters with no `Nothing` or dormant switch, unlike CIP-50. At commit `8631831` the min-fee function does not read them yet. Once it does, the genesis values decide whether the new term is non-zero on day one.

### What to update

1. Reimplementations of `minfee` in every SDK: add the reference-input term. Keep Conway behaviour for pre-Dijkstra eras.
2. cardano-cli and cardano-api build pipeline.
3. Documentation that prints `fee = a·size + b + exec + refScript`.
4. Tests: a transaction with many reference inputs and no reference scripts must cost more than the same transaction with those inputs omitted.
5. Do not touch pool-margin or pledge-leverage calculators.

***

## Breaking API changes

Why it was unavoidable, and what needs to be updated in response.

Fee is a ledger function of era, protocol parameters, and transaction. A new era is allowed to change the function.&#x20;

### Wire format

There is no new transaction field. The change is in how a fee is computed from fields that already exist. What does change on the wire is protocol parameters: two new keys hold the coefficients. A parameter decoder that stops at key 54, or drops unknown keys, will not see them. A fee estimator built on such a decoder will underprice transactions once the ledger uses the coefficients.

| CDDL rule | Change from Conway | What your tooling must do |
| --- | --- | --- |
| [`protocol_param_update` key 55](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L737) | New. `coin`, the min-fee per multi-asset byte in reference inputs (`refInputsCostPerMultiAssetByte`). | Add to parameter codecs and to any local fee calculation. |
| [`protocol_param_update` key 56](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L738) | New. `coin`, the min-fee per datum byte in reference inputs (`refInputsCostPerDatumByte`). | As above. |
| [`transaction_body` key 18, reference inputs](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L135) | Unchanged. | No codec change. The fee depends on what these inputs point to, so a fee estimator needs the referenced UTxOs, not just the transaction. |

**Not in the CDDL.**

* The fee formula, and when the ledger starts using these coefficients. At commit `8631831`, Dijkstra's `getMinFeeTx` still calls the Conway function.
* Both keys are in the Economic and Security groups, so changing them needs a stake pool vote as well as DReps and the Constitutional Committee.
* The ledger's upgrade parameters require both values at the hard fork.

Links go to the Dijkstra CDDL at cardano-ledger commit [`8631831`](https://github.com/IntersectMBO/cardano-ledger/tree/863183157cc39c48615078eab85389766bdc695b) (23 November 2026). The CDDL is not frozen yet, so check the line before relying on it.

### Wire and query contract

| Channel                                | Shape                                                                                                                                                                                  |
| -------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `query protocol-parameters`            | Exposes `refInputsCostPerMultiAssetByte` and `refInputsCostPerDatumByte` (keys 55 and 56). The Dijkstra min-fee function doesn’t use them yet; it still calls the Conway fee function. |
| Transaction JSON                       | No new user-set field. Reference inputs already exist.                                                                                                                                 |
| Phase-1 failure                        | Same `FeeTooSmallUTxO` family. The computed minimum is just higher.                                                                                                                    |
| Governance                             | Keys 55 and 56 are already protocol parameters. Changing them needs constitution and guardrails rows first. |

### What to update

* Closed-form fee code.
* Any "fee = this Python one-liner" in runbooks.
* Parameter-committee docs: keys 55 and 56 are protocol parameters, but they cannot be changed until the constitution and guardrails script cover them.

***

## New features

What new capabilities it unlocks that you might want to start thinking about.

* **Pricing of CIP-31.** Referencing a 10 kB inline-datum UTxO stops being a free DoS assist.
* **Design pressure toward small referenced outputs.** Protocols that stuff large blobs into referenced UTxOs will feel it. Storing the blob as a reference script is a different price curve. See the next page.

If a ticket mentions "min fee" and "pools", it is CIP-23, not this page.
