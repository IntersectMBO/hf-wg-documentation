---
description: This page shows the Hardfork working group's Hardfork Submission policy
---

# Hardfork Initation Submission Policy

The hardfork working group maintains an offical policy reflecting the ecosystem criteria that is required before they recommend submitting a hardfork initiation governance action.

The first iteration of this policy was developed and then followed by the working group for submission of the Plomin hardfork action.&#x20;

The policy is maintained via the [hf-wg-documentation/policies](../../policies/hardfork-submission-criteria.md#mainnet-hardfork-initiation-governance-action-submission-criteria) repository. We copy-paste the policy here for convenience.

{% hint style="warning" %}
To provide feedback on the policy you can

* Email **hard-fork@intersectmbo.org**
* Raise an issue via [Github/HF-WG-Documentation](https://github.com/IntersectMBO/hf-wg-documentation/issues/new) (or pull request - [see how-to](https://github.com/IntersectMBO/hf-wg-documentation?tab=readme-ov-file#chang-2-updating-tooling-readiness))
* Request to join the working group by emailing your interest **hard-fork@intersectmbo.org**.
{% endhint %}

## Mainnet Hardfork Initiation Governance Action Submission Criteria

Version: `0.1`

This policy describes specific metrics which the hardfork working group (HFWG) considers before recommending submission of a hardfork initiation governance action to Cardano mainnet.

This policy aims to apply to the most normal circumstances, special cases such as security upgrades may not necessarily apply.

#### Context

* The hardfork working group **can not** decide if Cardano is ready to hardfork, this is up to the ICC, SPOs and DReps.
  * Historically, the working group could decide this, but we are now in the _brave new world_.
* The HFWG **can** decide when to recommend the submission of a hardfork initiation action - _When do we think we are ready for SPOs and the ICC to consider a hardfork?_
* The HFWG **can** recommend key indicators we would like to see met before a hardfork is ratified, these indicators can be forwarded to the voters for consideration.
* The decision to recommend the submission of a hardfork action must be ratified by the Technical Steering Committee.
* Submitting a hardfork does not guarantee the ratification and enactment of a hardfork.

#### Definitions

* **Full Release**: A new release intended for use on Mainnet. Not a pre-release.
* **Hardfork Ready**: A state of tooling as indicated by the builder.

### Submission

#### Must see for submission

* Full release of _hardfork ready_ Cardano haskell node - available for at least one week.
  * The one week counter can be reset by breaking change releases.
* Preview Testnet hardforked - 2 epochs (1 day epochs)
* PreProd Testnet hardforked - no strict time limit.
* Tooling readiness (full releases) - [DB-Sync](https://github.com/IntersectMBO/cardano-db-sync), [cardano-wallet](https://github.com/cardano-foundation/cardano-wallet), [Ogmios](https://github.com/cardanosolutions/ogmios).
* Engagement with all key stakeholders kicked-off - tooling, exchanges, wallets, dApps/Defi, ICC, DReps, SPOs.

#### Would like to see for submission

* Preview Testnet hardforked - 3 epochs (1 day epochs)
* PreProd Testnet hardforked - 2 epochs
* Regular engagement with all key stakeholders - tooling, exchanges, wallets, dApps/Defi, ICC, DReps, SPOs.
* Tooling Upgrades in-progress - all been reached out to and engaged:
  * Libraries - CSL, CML, JS-SDK, CTL, Mesh, lucid, Pallas, Aiken
  * Tools - Rosetta, GraphQL, CNTools, SPO scripts
  * High level tooling - Blockfrost, Maestro, Kiois, Demeter
  * Indexers - Kupo, Oura, Scrolls, Carp
  * Governance - GovTool, CC-Portal, DRep Campaign, tempo.vote
* Block explorers - in-progress - Cexplorer, AdaStat, Cardanoscan, CF explorer
* Exchange readiness - progress is shown, confirmation of tooling upgrades for the first few.
* Wallet readiness - progress is shown.
* DApp/Defi readiness - progress is shown.
* SPO readiness - progress is shown.

### Would like to see for ratification (WIP)

The idea for this section, is it matches the metrics tracked for Chang #1. These are in addition to the on-chain voting ratification requirements.

* No major holidays or events - tech teams ready to respond and support to issues
* Preview Testnet hardforked - 42 epochs (1 day epochs)
* PreProd Testnet hardforked - 3 epochs
* SPO readiness - 80% stake measure by pool tool.
* Exchange readiness - 80% by liquidity.
* DApp/Defi readiness - 80% of top 20 projects.
* Tooling readiness - 80% of named tools.
* Wallet readiness - 80% of top 15
