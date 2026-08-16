# Dijkstra upgrade overview

### Overview <a href="#overview" id="overview"></a>

The Dijkstra era delivers Cardano's next major protocol upgrade in two phases. Phase 1 introduces the Dijkstra ledger era and ships Ouroboros Linear Leios as a complete, activated feature, targeting Q4 2026. Phase 2 activates Ouroboros Peras via an intra-era hard fork, a protocol version bump within the Dijkstra era that does not require a new era package in the ledger code.

The distinction matters for what each phase can change. A new era ships a complete new ledger code package and can introduce new block structures, new serialization formats, new cryptography, new protocol parameters, and new Plutus versions. An intra-era hard fork bumps the protocol version within the existing era and can change anything gate-able on a protocol version check: activating consensus rules, enabling new Plutus primitives within an existing Plutus version, turning on features whose block-body structures and protocol parameters were already defined by the era. Because Phase 1 ships the codec extensions and the protocol parameters Peras requires, Phase 2 can activate that protocol without a new era.

| Phase                                                                                                                                  | Mechanism           | Era      | Code Complete Target | Primary Activation                                                                        |
| -------------------------------------------------------------------------------------------------------------------------------------- | ------------------- | -------- | -------------------- | ----------------------------------------------------------------------------------------- |
| [Phase 1](https://product.cardano.intersectmbo.org/hardfork-planning/dijkstra/#phase-1-dijkstra-hard-fork-protocol-version-12-q4-2026) | New era (v12)       | Dijkstra | Q4 2026              | Ouroboros Linear Leios, Nested Transactions, Peras codec extensions & protocol parameters |
| [Phase 2](https://product.cardano.intersectmbo.org/hardfork-planning/dijkstra/#phase-2-peras-activation-intra-era-hard-fork-q2-2027)   | Intra-era hard fork | Dijkstra | Q2 2027              | Ouroboros Peras                                                                           |

Each phase rolls out in sequence: Preview testnet, then Pre-production testnet, then Mainnet. A governance action is submitted and ratified on each network before the hard fork is enacted. DReps, SPOs, and the Constitutional Committee vote on the mainnet governance action, as established by CIP-1694.

caution

All dates and quarters are estimated targets for code completion and mainnet-ready benchmarked releases. They do not include governance processes or community testing. The time required for Preview and Pre-production rollout, SPO testing windows, and on-chain governance ratification will extend beyond these targets before any mainnet hard fork is enacted. All targets are estimates only and not guarantees.

***

### Phase 1: Dijkstra Hard Fork (Protocol Version 12, Q4 2026) <a href="#phase-1-dijkstra-hard-fork-protocol-version-12-q4-2026" id="phase-1-dijkstra-hard-fork-protocol-version-12-q4-2026"></a>

#### Design Rationale <a href="#design-rationale" id="design-rationale"></a>

This phase activates Ouroboros Linear Leios via a hard fork, a protocol version bump to Protocol Version 12. the Dijkstra era.

Linear Leios is a partial realisation of the Leios throughput vision. It delivers meaningful gains but does not achieve everything a fuller Leios deployment could. Substantial research was done on the broader Leios design, but the additional complexities it would require were not sufficiently pinned down for a first mainnet deployment, and the closest approaches raised concerns around changes to the user experience the dapp ecosystem was not prepared to accept. A future path toward a more complete Leios would require changes to block and transaction structure and a new ledger era, Euler or later.

Linear Leios increases Cardano's throughput without changing the security guarantees of the base protocol. The original Leios research design used three block types including Input Blocks; Linear Leios eliminates those and works with two:

* **Ranking Blocks (RBs)** are the existing Praos blocks, extended with optional fields to announce and certify Endorser Blocks.
* **Endorser Blocks (EBs)** are larger supplementary blocks that contain references to additional transactions, not the transactions themselves.

Transactions continue to propagate through the standard mempool. When a block producer wins slot leadership, it produces an RB that optionally announces an Endorser Block. The announcement is part of the RB header itself and contains the hash of the EB, which in turn holds the hashes of the transactions being endorsed. Nodes that do not already have those transactions request them from peers via new node-to-node protocols. A stake-based committee then certifies the EB; the certificate contains the hash of the EB and the aggregated signatures proving a 75% quorum of active stake. A subsequent RB includes that certificate, applying the endorsed transactions to the ledger. If no certified EB is available, a Ranking Block includes transactions directly as in standard Praos. The result is that the network can absorb significantly more transactions per unit of time without requiring larger blocks or faster slots.

In addition it ships the block body extensions and protocol parameters required by Ouroboros Peras (to be activated in phase 2). Block structure changes require a new era, so they must land here.

#### Rollout Milestones <a href="#rollout-milestones" id="rollout-milestones"></a>

| Milestone                            | Notes                                                                                                     |
| ------------------------------------ | --------------------------------------------------------------------------------------------------------- |
| Node release                         | Dijkstra-compatible node released for testnet operators                                                   |
| **Preview hard fork**                | Governance action submitted and enacted on Preview; SPO testing window opens                              |
| Preview SPO testing window           | \~2 weeks; integration testing, tooling validation, EB propagation testing, throughput benchmarking       |
| **Pre-production hard fork**         | Governance action submitted and enacted on Pre-production; SPO testing window opens                       |
| Pre-production SPO testing window    | \~1-2 weeks; final readiness checks                                                                       |
| Mainnet governance action submission | Hard Fork Initiation action submitted on Mainnet; DReps, SPOs, and Constitutional Committee voting period |
| **Mainnet hard fork**                | Following governance ratification; date TBD                                                               |

#### In Scope <a href="#in-scope" id="in-scope"></a>

[GitHub reference](https://github.com/IntersectMBO/cardano-node/issues/6634)

**Ouroboros Linear Leios (**[**CIP-164**](https://cips.cardano.org/cip/CIP-0164)**)**

The headline feature of the Dijkstra hard fork, Linear Leios lets a block producer publish a larger Endorser Block alongside its Praos block, referencing the transactions the base block has no room for; a committee of stake pools certifies that block before its transactions enter the ledger, so throughput rises sharply while Praos security guarantees hold. It puts the bandwidth and compute already sitting idle on today's nodes to work, and the higher volume matters economically as well, since transaction fees must take over from the diminishing Reserve to sustain rewards and pool profitability. Leios ships complete in Phase 1, with throughput raised gradually via protocol parameter updates after activation.

**Nested Transactions (**[**CIP-118**](https://cips.cardano.org/cip/CIP-0118)**)**

A major feature of the Dijkstra hard fork. Nested transactions allow a transaction to contain child transactions with independent witnesses and execution contexts, for more expressive on-chain logic. Implementation is well advanced.

**Observe Script Type / Guard Scripts (**[**CIP-112**](https://cips.cardano.org/cip/CIP-0112)**)**

Introduces a new script type that can observe transaction validity without being executed as part of spending or minting. Required for expressive transaction guards and a dependency for the PlutusV4 script context.

**Account Address Enhancement, Phase 1 (**[**CIP-159**](https://cips.cardano.org/cip/CIP-0159)**)**

Phase 1 of account address improvements. Delivers the ledger-level definitions for account-style addresses on Cardano.

**Remove isValid from Transactions (**[**CIP-167**](https://cips.cardano.org/cip/CIP-0167)**)**

Removes the `isValid` field from transactions, simplifying the transaction structure and script execution.

**Non-segregated Block Body Serialization (**[**CIP-176**](https://cips.cardano.org/cip/CIP-0176)**)**

Changes block body serialization to a non-segregated format, required for the block body extensions Leios and other future features need.

**PlutusV4 Script Context**

Introduces the updated script context for PlutusV4, enabling scripts to observe the new transaction and ledger structures introduced in Dijkstra.

**Fee Function Update (Reference Inputs)**

Updates the fee function to account for reference inputs. No CIP; parameters will be hardcoded initially with a path to make them updatable later.

**Reference Script Pricing and Limits**

The pricing and size limits for reference scripts have been in effect since Conway as hardcoded values. Dijkstra introduces them as proper protocol parameters. For the community to update them via governance actions, both the Constitution and the guardrails script must be updated to include bounds and rules for these new parameters.

**Remove DRep Requirement for Reward Withdrawals (**[**CIP-181**](https://cips.cardano.org/cip/CIP-0181)**)**

Removes the requirement for a DRep delegation to be present when withdrawing staking rewards, reducing friction for ada holders who want to withdraw without participating in governance.

**Pledge Leverage-Based Staking Rewards (**[**CIP-50**](https://cips.cardano.org/cip/CIP-0050)**)**

Introduces a leverage parameter L that ties pool rewards to the ratio of delegated stake to pledge. The parameter is introduced with a default value of `Nothing`, which preserves current reward behaviour exactly — no change takes effect at the hard fork. DReps can subsequently vote to set L to a concrete value, at which point pools with zero pledge would earn zero rewards.

#### Structural Groundwork for Phase 2 <a href="#structural-groundwork-for-phase-2" id="structural-groundwork-for-phase-2"></a>

These are not feature activations. They are the block structure changes, header extensions, and protocol parameter introductions that Phase 2 depends on. Because all of these require a new era, they must ship in Phase 1. Any protocol parameters needed to govern Peras behaviour must also be defined here, even if their values are not yet active, since protocol parameters cannot be introduced in an intra-era hard fork.

| Change                                                                  | Purpose                                                                                                                           |
| ----------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| [CIP-140](https://cips.cardano.org/cip/CIP-0140) Peras codec extensions | Introduces the codec changes needed for block bodies to optionally carry a Peras certificate, without activating the voting layer |

#### Conditional: Fair Min Fees ([CIP-23](https://cips.cardano.org/cip/CIP-0023)) <a href="#conditional-fair-min-fees-cip-23" id="conditional-fair-min-fees-cip-23"></a>

The protocol parameter introduced by CIP-23 is defined at Phase 1, but the fee rule itself may or may not activate at the Phase 1 hard fork. If implementation and governance readiness align, CIP-23 activates with Phase 1. If not, the parameter definition ships dormantly and the fee rule activates in a subsequent intra-era hard fork within the Dijkstra era.

***

### Phase 2: Peras Activation (Intra-era Hard Fork, Q2 2027) <a href="#phase-2-peras-activation-intra-era-hard-fork-q2-2027" id="phase-2-peras-activation-intra-era-hard-fork-q2-2027"></a>

#### What Changes <a href="#what-changes" id="what-changes"></a>

This phase activates Ouroboros Peras via an intra-era hard fork, a protocol version bump within the Dijkstra era. The CIP-140 codec extensions shipped with Phase 1, so no new ledger era is needed. The structural groundwork is already in place; this hard fork activates the consensus rules that switch it on.

Peras is a settlement-speed upgrade that adds a voting overlay to the existing Ouroboros Praos chain selection rule. Committees of stake pool operators vote on recent chain tips; once a tip accumulates sufficient votes it is treated as settled well before the standard Praos depth would allow. Peras does not change how blocks are produced. It changes how quickly the network can consider a block irreversible.

#### Rollout Milestones <a href="#rollout-milestones-1" id="rollout-milestones-1"></a>

| Milestone                            | Notes                                                                                           |
| ------------------------------------ | ----------------------------------------------------------------------------------------------- |
| Node release                         | Peras-compatible node released for testnet operators                                            |
| **Preview hard fork**                | Governance action submitted and enacted on Preview; SPO testing window opens                    |
| Preview SPO testing window           | \~2 weeks; voting overlay testing, settlement latency validation                                |
| **Pre-production hard fork**         | Governance action submitted and enacted on Pre-production; SPO testing window opens             |
| Pre-production SPO testing window    | \~1-2 weeks; final readiness checks                                                             |
| Mainnet governance action submission | Governance action submitted on Mainnet; DReps, SPOs, and Constitutional Committee voting period |
| **Mainnet activation**               | Following governance ratification; date TBD                                                     |

#### Activates <a href="#activates" id="activates"></a>

* [CIP-140](https://cips.cardano.org/cip/CIP-0140): Ouroboros Peras, full activation of the Peras voting layer and accelerated settlement guarantees
* [CIP-23](https://cips.cardano.org/cip/CIP-0023): Fair Min Fees fee rule, if not activated in Phase 1

#### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

* Phase 1 mainnet live (CIP-140 codec extensions and protocol parameters in place)
* Peras node implementation merged to mainline
* Governance action ratified on-chain by DReps, SPOs, and Constitutional Committee

***

### Considered but Not Included in This Era <a href="#considered-but-not-included-in-this-era" id="considered-but-not-included-in-this-era"></a>

These CIPs were evaluated for Dijkstra but will not be included in this era:

| CIP                                                              | Title                                          | Rationale                                                                                                                                                                                                                                                                            |
| ---------------------------------------------------------------- | ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [CIP-180](https://github.com/cardano-foundation/CIPs/pull/1157)  | Producer Identification                        | Ledger team does not have the capacity to implement within this era, and alternative node implementations have not reached agreement on the approach.                                                                                                                                |
| [CPS-0023](https://github.com/cardano-foundation/CIPs/pull/1103) | Cardano Multi Asset Treasury                   | Requires the CIP-159 account address infrastructure included in Phase 1 to lay the groundwork. Better targeted at Euler once that foundation is in place.                                                                                                                            |
| [CIP-156](https://cips.cardano.org/cip/CIP-0156)                 | Plutus Core Builtin Function - multiIndexArray | Not included in the PlutusV4 scope for Dijkstra due to limited Plutus team resources. As it requires no ledger changes, it could potentially be picked up in any upcoming intra-era hard fork if capacity allows.                                                                    |
| [CIP-160](https://cips.cardano.org/cip/CIP-0160)                 | Receiving Script Purpose and Addresses         | Insufficient ledger resources to implement within this era given its complexity.                                                                                                                                                                                                     |
| [CIP-163](https://cips.cardano.org/cip/CIP-0163)                 | Time-Bound Delegation with Dynamic Rewards     | Explicitly contentious: the same community poll saw 54.1% vote NO, making it the most rejected item on the shortlist. Including it would hand opponents a clear mandate to vote against the hard fork.                                                                               |
| [CIP-173](https://github.com/cardano-foundation/CIPs/pull/1129)  | Net Change Limit Parameter                     | A major overhaul that is not implementable in the current ledger state: the ledger does not retain history of past epoch inflows and outflows, which the NCL calculation requires. Needs a detailed implementation plan before it can be scoped. Better targeted at Euler or beyond. |
| [CIP-0175](https://github.com/cardano-foundation/CIPs/pull/1140) | Stake Pool Hot Credentials                     | Too complex to implement given existing ledger team commitments for this era. Better targeted at Euler.                                                                                                                                                                              |

### Wishlist / Future Consideration <a href="#wishlist--future-consideration" id="wishlist--future-consideration"></a>

Community proposals not yet targeted at any scheduled hard fork:

| CIP                                                              | Title                            |
| ---------------------------------------------------------------- | -------------------------------- |
| [CIP-0182](https://github.com/cardano-foundation/CIPs/pull/1164) | Optimistic Constitutionality     |
| [CIP-0168](https://github.com/cardano-foundation/CIPs/pull/1090) | More BuiltinValue Functions      |
| [CIP-????](https://github.com/cardano-foundation/CIPs/pull/1072) | More Descriptive Script Purposes |
| (no CIP yet)                                                     | Quantum-secure signature schemes |

***

#### Product Committee Reference plan

{% embed url="https://product.cardano.intersectmbo.org/hardfork-planning/dijkstra/" %}
