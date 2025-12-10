
# Mainnet Hard Fork Initiation Governance Action Submission Criteria

Version: `0.2`

This policy describes specific metrics which the hard fork working group (HFWG) considers before recommending submission of a hard fork initiation governance action to Cardano mainnet.

This policy aims to apply to the most normal circumstances, special cases such as security upgrades may not necessarily apply.

### Context

- The hard fork working group **can not** decide if Cardano is ready to hard fork, this is up to the ICC, SPOs and DReps.
  - Historically, the working group could decide this, but we are now in the *brave new world*.
- The HFWG **can** decide when to recommend the submission of a hard fork initiation action - *When do we think we are ready for SPOs and the ICC to consider a hard fork?*
- The HFWG **can** recommend key indicators we would like to see met before a hard fork is ratified, these indicators can be forwarded to the voters for consideration.
- The decision to recommend the submission of a hard fork action must be ratified by the Technical Steering Committee.
- Submitting a hard fork does not guarantee the ratification and enactment of a hard fork.

### Definitions

- **Full Release**: A new release intended for use on Mainnet. Not a pre-release.
- **hard fork Ready**: A state of tooling as indicated by the builder.

## Submission

### Must see for submission

- Full release of *hard fork ready* Cardano haskell node - available for at least one week.
  - The one week counter can be reset by breaking change releases.
- Preview Testnet hard forked - 2 epochs (1 day epochs)
- PreProd Testnet hard forked - no strict time limit.
- Tooling readiness (full releases) - [DB-Sync](https://github.com/IntersectMBO/cardano-db-sync), [cardano-wallet](https://github.com/cardano-foundation/cardano-wallet), [Ogmios](https://github.com/cardanosolutions/ogmios).
- Engagement with all key stakeholders kicked-off - tooling, exchanges, wallets, dApps/Defi, ICC, DReps, SPOs.

### Would like to see for submission

- Preview Testnet hard forked - 3 epochs (1 day epochs)
- PreProd Testnet hard forked - 2 epochs
- Regular engagement with all key stakeholders - tooling, exchanges, wallets, dApps/Defi, ICC, DReps, SPOs.
- Tooling Upgrades in-progress - all been reached out to and engaged:
  - Libraries - CSL, CML, JS-SDK, CTL, Mesh, lucid, Pallas, Aiken
  - Tools - Rosetta, GraphQL, CNTools, SPO scripts
  - High level tooling - Blockfrost, Maestro, Koios, Demeter
  - Indexers - Kupo, Oura, Scrolls, Carp
  - Governance - GovTool, CC-Portal, DRep Campaign, tempo.vote
- Block explorers - in-progress - Cexplorer, AdaStat, Cardanoscan, CF explorer 
- Exchange readiness - progress is shown, confirmation of tooling upgrades for the first few.
- Wallet readiness - progress is shown.
- DApp/Defi readiness - progress is shown.
- SPO readiness - progress is shown.

## Would like to see for ratification

The idea for this section, is it matches the metrics tracked for Chang #1.
These are in addition to the on-chain voting ratification requirements.

- No major holidays or events - tech teams ready to respond and support to issues
- Preview Testnet hard forked - 42 epochs (1 day epochs)
- PreProd Testnet hard forked - 3 epochs
- SPO readiness - 80% stake measure by pool tool.
- Exchange readiness - 80% by liquidity.
- DApp/Defi readiness - 80% of top 20 projects.
- Tooling readiness - 80% of named tools.
- Wallet readiness - 80% of top 15
