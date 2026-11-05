# Fee Function Update (Reference Inputs)

This item has no CIP. It changes the transaction minimum-fee function so reference inputs are priced. It is not CIP-23 Fair Min Fees. That is a pool margin floor. It is not the Conway reference-script surcharge. That is the next page.

Reference inputs (CIP-31) let a transaction mention a UTxO without spending it. Nodes still fetch, deserialise, and hold that UTxO for script context. Conway's min-fee formula charges `a · size(tx) + b` plus script-execution and reference-script terms. The referenced input bodies themselves were not a first-class extra term. Dijkstra adds that accounting.

Per the overview, parameters start hardcoded, with a later path to make them updatable protocol parameters. That is the same playbook Conway used for reference-script stride and multiplier.

**CIP:** none
**Overview:** [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), Fee Function Update (Reference Inputs)
**Do not confuse with:** [Fair Min Fees (CIP-23)](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/fair-min-fees-conditional), [Reference Script Pricing and Limits](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/reference-script-pricing-and-limits)
**Node scope:** [cardano-node#6634](https://github.com/IntersectMBO/cardano-node/issues/6634)

***

## Core semantics changes

Implications, why it concerns you, and what needs to be updated in response.

### What the ledger actually does

Minimum fee for a Dijkstra transaction is still deterministic and still checked in phase-1. The function gains a term that depends on the reference inputs the transaction lists, by count or by serialised size of the referenced outputs. Follow the ledger implementation when coding. Do not treat this sentence as the formula.

Until those coefficients are promoted to protocol parameters, changing them requires another hard fork or intra-era version bump. Expect genesis and era values to match whatever the ledger team froze for protocol version 12.

Spending inputs, minting, withdrawals, CIP-159 deposits, and CIP-118 children all still go through the existing size, execution, and reference-script terms. This page only adds the reference-input piece.

### Why this concerns wallets, explorers, indexers, and pool tools

**Every fee estimator.** Wallets, cardano-cli `transaction build`, Mesh, Lucid, CSL fee helpers, batchers, and "is this transaction balanced?" off-chain code that reimplements `minfee` will underpay if they keep the Conway function on Dijkstra transactions that use reference inputs. Underpaying is a phase-1 reject, not a silent overpay.

**dApps that reference large UTxOs.** Protocols that pass big inline-datum outputs in as reference inputs become more expensive. That is intended. Nodes pay I/O and RAM for those bytes.

**Explorers.** "Minimum fee" and "fee breakdown" panels need a new line item. Do not dump it into "reference script fee".

**This is live on hard-fork day** if the hardcoded term is non-zero. Unlike CIP-23 and CIP-50, the overview does not describe a `Nothing` or dormant switch.

### What to update

1. Reimplementations of `minfee` in every SDK: add the reference-input term. Keep Conway behaviour for pre-Dijkstra eras.
2. cardano-cli and cardano-api build pipeline.
3. Documentation that prints `fee = a·size + b + exec + refScript`.
4. Tests: a transaction with many reference inputs and no reference scripts must cost more than the same transaction with those inputs omitted.
5. Do not touch pool-margin or pledge-leverage calculators.

***

## Breaking API changes

Why it was unavoidable, and what needs to be updated in response.

Fee is a ledger function of era, protocol parameters, and transaction. A new era is allowed to change the function. Making the coefficients hardcoded is why this item can ship without a CIP and without a constitution row on day one.

### Wire and query contract

| Channel | Shape |
| --- | --- |
| `query protocol-parameters` | May not expose the new coefficients while they are hardcoded. Do not assume a JSON key exists on hard-fork day. |
| Transaction JSON | No new user-set field. Reference inputs already exist. |
| Phase-1 failure | Same `FeeTooSmallUTxO` family. The computed minimum is just higher. |
| Later promotion to protocol parameters | New keys plus constitution and guardrails rows. Treat as a follow-up bulletin. |

If the node later surfaces the coefficients, record the exact JSON names from the implementation. Do not invent them here.

### What to update

- Closed-form fee code.
- Any "fee = this Python one-liner" in runbooks.
- Parameter-committee docs: this is not yet a governable knob.

***

## New features

What new capabilities it unlocks that you might want to start thinking about.

- **Pricing of CIP-31.** Referencing a 10 kB inline-datum UTxO stops being a free DoS assist.
- **A path to governance later.** Once the coefficients are protocol parameters, the same path reference-script stride took from Conway to Dijkstra, the Parameter Change process can tune them without an era.
- **Design pressure toward small referenced outputs.** Protocols that stuff large blobs into referenced UTxOs will feel it. Storing the blob as a reference script is a different price curve. See the next page.

If a ticket mentions "min fee" and "pools", it is CIP-23, not this page.
