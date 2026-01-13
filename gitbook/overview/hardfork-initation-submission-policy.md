---
description: >-
  This page shows the Hard Fork Working Group's hard fork governance action
  submission policy
---

# Hard Fork Initiation Submission Policy

The hardfork working group maintains a policy reflecting the ecosystem criteria that is required before they recommend submitting a hard fork initiation governance action.

The first iteration of this policy (`v0.1`) was developed and then followed by the working group for submission of the Plomin hardfork action. The policy is maintained via the [hf-wg-documentation/hardfork-initation-submission-policy.md](hardfork-initation-submission-policy.md).

{% hint style="warning" %}
To provide feedback on the policy you can

* Email **hard-fork@intersectmbo.org**
* Raise an issue via [Github/HF-WG-Documentation](https://github.com/IntersectMBO/hf-wg-documentation/issues/new) (or pull request - [see how-to](https://github.com/IntersectMBO/hf-wg-documentation?tab=readme-ov-file#contributing))
* Request to join the working group by emailing your interest **hard-fork@intersectmbo.org**.
{% endhint %}

## Mainnet Hard Fork Initiation Governance Action Submission Criteria

Version: `0.2`

This policy describes specific metrics which the hard fork working group (HFWG) considers before recommending submission of a Hard Fork Initiation governance action to Cardano mainnet.

This policy aims to apply to the most normal circumstances, special cases such as security upgrades may not necessarily apply.

### Context

* The hard fork working group **can not** decide if Cardano is ready to hard fork, this is up to the CC, SPOs and DReps.
* The HFWG **can** decide when to recommend the submission of a hard fork initiation action - _When do we think we are ready for SPOs and the CC to consider a hard fork?_
* The HFWG **can** recommend key indicators we would like to see met before a hard fork is ratified, these indicators can be forwarded to the voters for consideration.
* The decision to recommend the submission of a hard fork action must be ratified by the Technical Steering Committee.
* Submitting a hard fork initiation governance action does not guarantee the ratification and enactment of a hard fork.

#### Definitions

* **Full Release**: A new release intended for use on Mainnet. Not a pre-release.
* **Hard Fork Ready**: A state of tooling/infrastructure as indicated by the builder/maintainer.

### Submission

#### Must see for submission

* Full release of _hard fork ready_ Cardano haskell node - released and available for at least **one week**.
  * The one week counter can be reset by breaking change releases.
* Preview Testnet hard forked - 2 epochs (1 day epochs)
* PreProd Testnet hard forked - no strict time limit.
* Tooling readiness (full releases) - [DB-Sync](https://github.com/IntersectMBO/cardano-db-sync), [cardano-wallet](https://github.com/cardano-foundation/cardano-wallet), [Ogmios](https://github.com/cardanosolutions/ogmios).
* Engagement with all key stakeholders kicked-off - tooling, exchanges, wallets, dApps/DeFi, CC, DReps, SPOs.

#### Would like to see for submission

* Preview Testnet hard forked - 3 epochs (1 day epochs)
* PreProd Testnet hard forked - 2 epochs
* Regular engagement with all key stakeholders - tooling, exchanges, wallets, dApps/DeFi, CC, DReps, SPOs.
* Tooling Upgrades in-progress - all been reached out to and engaged:
  * Libraries - CSL, CML, JS-SDK, CTL, Mesh, lucid, Pallas, Aiken
  * Tools - Rosetta, GraphQL, CNTools, SPO scripts
  * High level tooling - Blockfrost, Maestro, Koios, Demeter
  * Indexers - Kupo, Oura, Scrolls, Carp
  * Governance - GovTool, DRep Campaign, tempo.vote
* Block explorers - in-progress - Cexplorer, AdaStat, Cardanoscan
* Exchange readiness - progress is shown, confirmation of tooling upgrades for the first few.
* Wallet readiness - progress is shown.
* DApp/DeFi readiness - progress is shown.
* SPO readiness - progress is shown.

### Would like to see for ratification

The idea for this section, is it matches the metrics tracked for Chang #1. These are in addition to the on-chain voting ratification requirements.

* No major holidays or events - tech teams ready to respond and support to issues
* Preview Testnet hard forked - 42 epochs (1 day epochs)
* PreProd Testnet hard forked - 3 epochs
* SPO readiness - 80% stake measure by pool tool.
* Exchange readiness - 80% by liquidity.
* DApp/Defi readiness - 80% of top 20 projects.
* Tooling readiness - 80% of named tools.
* Wallet readiness - 80% of top 15

***

* Note: DApp and Defi readiness is subjective. Different upgrades will affect the ecosystem in entirely different ways. The HFWG looks for evidence that trusted and mature ecosystem builders, where a level of expertise and experience are evidenced, have upgraded. This demonstrates 'the art of the possible’, which contributes to understanding ecosystem impact and timeline required, and also builds confidence a good level of testing has been undertaken.

