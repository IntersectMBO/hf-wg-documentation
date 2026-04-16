# van Rossem upgrade FAQ

The hard fork working group has collated key questions and formed the following frequently asked questions (FAQ) for the benefit of the community.

## **Questions for ada holders**

<details>

<summary>Will there be token migration required due to the hard fork?</summary>

No, there will be no token migration required as part of the van Rossem hard fork. The fork is a protocol update that will be implemented automatically across the network. All ADA tokens will remain fully accessible and functional before, during, and after the hard fork without any need for token migration. However, you should ensure that your wallet and any tools you are using are up-to-date with the latest version to support any new features or improvements introduced by the fork.

</details>

<details>

<summary>What should token holders on-chain and those with staked tokens do?</summary>

For token holders, whether on-chain or staked, there is no specific action required on your part. Your tokens will remain safe and fully functional. However, you should ensure that your wallet and any tools you are using are up-to-date with the latest version to support any new features or improvements introduced by the fork.

</details>

***

## **Questions on the general van Rossem hard fork**

<details>

<summary>Cardano Testnet Definitions</summary>

Cardano Test Network Definitions

**SanchoNet Testnet**<br>

* Community run network originally for governance testing but now used for testing interesting scenarios not possible on other networks
* Potential to see untested and unreleased node versions
* Specifications
  * Very small number of community stake pools \~10
  * Varied configurations
  * Varied Protocol Parameters
* Expectations
  * No guarantees of uptime
  * No guarantees of support -- community run
  * No guarantees of upgrade readiness

**Preview Testnet**

* Aimed to be a move fast break things environment
* Tends to be long living, but significant rollbacks and truncations are to be expected
* Upgrade readiness: \~one week adoption window given ahead of hard forking
* Specifications
  * Protocol Parameters close to mainnet -- epoch lengths (1 day)
  * Small set of stake pools, primarily operated by founding entities
* Configurations close to mainnet
* Expectations
  * No guarantees of uptime -- move fast break things

**PreProd Testnet**

* Aimed to be on close parity with Cardano Mainnet, long living testnet
* Upgrade readiness: \~six week adoption window given ahead of hard forking
* Specifications
  * Protocol Parameters matching Cardano mainnet
  * Large set of stake pool operators
  * Configurations matching mainnet
* Expectations
  * Uptime aimed to be close to mainnet

</details>

<details>

<summary>What is a GA?</summary>

A governance action (GA) is a proposed on-chain change to Cardano. The various voting groups vote on it, as described within [CIP-1694 Governance Actions](https://github.com/cardano-foundation/CIPs/blob/master/CIP-1694/README.md#governance-actions).

</details>

<details>

<summary>How do I know which governance actions are real?</summary>

It is encouraged to review and read all governance actions carefully, anyone within the community can raise a governance action for consideration.&#x20;

All governance actions raised by Intersect, on behalf of the community, will be clearly sign posted and the metadata hosted on the Intersect GitHub repository.

</details>

<details>

<summary>Who can vote on these GAs?</summary>

Cardano mainnet is currency within governance bootstrapping, this means the governance model is not fully activated.&#x20;

In this bootstrapping phase only the CC and the SPOs can vote on governance actions accordingly. This is detailed in CIP-1694 bootstrap phase and interim consitution.

</details>

<details>

<summary>Why van Rossem hard fork is called an intra-era hard fork?</summary>

With an intra-era van Rossem Hard Fork, the ledger doesn't change era, keeping Cardano within the same ledger era (currently Conway). It introduces refinements, fixes, optimisations, and new features that do not require an era transition. It does require network-wide coordination, but usually with a much lower integration burden than during era transitions. Does not introduce a new transaction share or a significant breaking semantic change.

To summarize, the proposed upgrade will introduce improvements without changing transaction shape. This means the upgrade burden is much lower than for previous hardforks.

</details>

<details>

<summary>Whats in the scope for van Rossem hard fork?</summary>

**Plutus upgrades**

1. All built-in functions are available across Plutus V1, V2, and V3:\
   Expanding the capabilities of Plutus V1 and V2 scripts and unifying the feature availability across versions.
2. case Expressions for built-in types:\
   Enables case expressions on Bool, Integer, and Data within UPLC. Provides significant performance improvements and cleaner script logic. Addresses one of the major performance bottlenecks in data matching.
3. New built-ins and native types:

* [CIP-138 | Array type](https://cips.cardano.org/cip/CIP-138) – adding efficient, native on-chain array handling
* [CIP-153 | MaryEraValue type](https://cips.cardano.org/cip/CIP-153) – optimised multi-asset value operations
* [CIP-109 | Modular exponentiation builtin](https://cips.cardano.org/cip/CIP-109) – critical for advanced crypto
* [CIP-132 | dropList builtin](https://cips.cardano.org/cip/CIP-132) – efficient list manipulation
* [CIP-133 | Multi-scalar multiplication over BLS12-381](https://cips.cardano.org/cip/CIP-133) – useful for advanced cryptographic operations, specifically with zero-knowledge proof systems

All of these new builtins will be introduced across all Plutus versions. Collectively, these changes increase script performance, reduce execution cost, and meaningfully extend what builders can accomplish in Plutus.

**Ledger and Cardano Node enhancements**

VRF Key uniqueness enforcement:

* Ensures no two stake pools reuse the same VRF key
* Strengthens pool security and mitigates possible attack vectors
* This means that from the point of hardfork, VRK key hash uniqueness is enforced at the ledger level

Revised reference input rules for Plutus V1/V2:

* Adjusts predicate checks that previously caused issues for scripts using reference inputs
* This fixes a scenario where&#x20;

Constitutional Committee voting restriction moved to a ledger rule:

* Shifts a mempool-only check into a proper ledger predicate failure
* Improves transparency and governance correctness

Non-matching withdrawals predicate:

* Clearer error messaging and safer validation of withdrawal structures

Improved protocol parameter hash mismatch reporting:

* Better diagnostics when PPView hashes differ
* Helps operators identify and resolve configuration issues quickly

Proposed van Rossem scope document is available [here](https://docs.google.com/document/d/1IqRekTeC8yj0w3tZ7iDpPocUZrbpVw3Q/edit#heading=h.359txovd42cc).

</details>

***

## Questions on the Hard Fork working group

<details>

<summary>The Hard Fork Working Group's role in Cardano Upgrades</summary>

The hard fork working group is spun up to help coordinate Cardano's upgrades, with oversight from Intersect's Technical Steering Committee.

The working group aims to be a transparent place to

* discuss upgrades
* track ecosystem readiness
* make decisions on the submission on hard fork initation governance actions

Intersect staff help this effort by organising the meetings, writing up meeting minutes, publishing communications and reaching out to stakeholders.

</details>

<details>

<summary>How often does the hard fork working group meet?</summary>

The group meets weekly in the lead-up to a hard fork.

</details>

<details>

<summary>How can the community get involved in the hard fork working group?</summary>

Join the dedicated Upgrade Discord channel at [#wg-hard-fork](https://discord.com/channels/1136727663583698984/1242097284619960411) (on the Intersect Discord server). This channel is monitored by the working group, with updates being shared and questions answered. Alternatively, you can reach out to [hard-fork@intersectmbo.org](mailto:hard-fork@intersectmbo.org)&#x20;

The hard fork working group meetings are in the shared [Luma Calendar](https://luma.com/calendar/cal-TMjYNpSY4huYYif) along with the newly started X spaces for the next several weeks. The [Cardano Upgrades GitBook](https://cardanoupgrades.docs.intersectmbo.org/) contains important hard fork context, working group policies, readiness tracking, and working group meeting minutes.

To further increase reach, the group began to hold regular X spaces each Thursday.

<br>

</details>

***

## **Questions on Testing and Development**

<details>

<summary>How will the van Rossem hard fork be previewed and tested before full deployment?</summary>

Node with protocol version 11 will be previewed and tested on [preview and pre-production testnets](https://docs.cardano.org/cardano-testnets/environments/). This process is controlled by the community, ensuring thorough testing and validation before the full deployment.

</details>

<details>

<summary>How does the community involvement in testing work?</summary>

Community testing is conducted on test networks with the latest node versions, where various elements including plutus built-ins for example, can be tested. This stage allows for community feedback and is essential for ensuring the robustness of the hard fork.

</details>

<details>

<summary>What is the role of stake pool operators upgrading to the latest node for the van Rossem hard fork?</summary>

Stake Pool Operators play an important (the most important!) part in any hard fork. The community requires them to upgrade prior to a hard fork combinator event. The latest status of SPOs' readiness can be found on our [van Rossem Upgrade Readiness page](https://cardanoupgrades.docs.intersectmbo.org/van-rossem-upgrade/van-rossem-upgrade-readiness).

</details>

<details>

<summary>Is there a node version that can be used for testing?</summary>

Yes. 10.7 is intended to be the last node release that won't cross the intra-era hard fork. We encourage all SPOs, dApps, wallets and builders to **integrate and deploy** [**10.7.1**](https://github.com/IntersectMBO/cardano-node/releases/tag/10.7.1) in preparation for the **11.0** release.

</details>

***

## Questions on how to get involved and how to prepare

<details>

<summary>How will changes and updates be communicated to the community?</summary>

Updates and significant changes will be communicated through various channels including [X](https://x.com/intersectmbo), [Discord](https://discord.com/channels/1136727663583698984/1262393547915657287), and the project’s [upgrade space](https://cardanoupgrades.docs.intersectmbo.org/). Important updates will also be discussed in follow-up meetings, ensuring all stakeholders have the latest information and can provide feedback.

Meeting minutes and action items from all hard fork working group meeting can be found at this [link](https://cardanoupgrades.docs.intersectmbo.org/van-rossem-upgrade/hard-fork-working-group-meeting-minutes).

</details>

<details>

<summary>What role does community governance play in the Cardano upgrade roadmap?</summary>

Community governance is a central aspect of Cardano’s upgrade roadmap. Through different initiatives and delegated representatives (DReps) the community actively participates in decision-making processes, shaping the future direction of the network.

</details>

<details>

<summary>What steps should users take to prepare for the hard fork?</summary>

**Here’s what users can do to prepare:**&#x20;

* **Join** the dedicated Upgrade Discord channel at [#wg-hard-fork](https://discord.com/channels/1136727663583698984/1242097284619960411) (on the Intersect Discord server). This channel is monitored by the working group, with updates being shared and questions answered. Alternatively, you can reach out to [hard-fork@intersectmbo.org](mailto:hard-fork@intersectmbo.org)
  * The hard fork working group meetings are in the shared [Luma Calendar](https://luma.com/calendar/cal-TMjYNpSY4huYYif) along with the newly started X spaces for the next several weeks. The [Cardano Upgrades GitBook](https://cardanoupgrades.docs.intersectmbo.org/) contains important hard fork context, working group policies, readiness tracking, and working group meeting minutes.
  * To further increase reach, the group began to hold regular X spaces each Thursday.
* **Update wallets and applications** - Ensure you’re using the latest versions of [Cardano wallets](https://docs.cardano.org/new-to-cardano/types-of-wallets/) and applications to guarantee compatibility with the new protocol.&#x20;
* **Take part in testing -**  This is especially true for Cardano Preview testnet where you can test the tools and improvements that are brought with van Rossem hard fork.

</details>

***

If you find any information on this page incorrect or misleading please email hard-fork@intersectmbo.org and request a correction.&#x20;
