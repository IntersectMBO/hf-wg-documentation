---
hidden: true
---

# Chang Upgrade #1 FAQ

{% hint style="info" %}
This FAQ is in support of the Chang #1 hard fork only. Answers may not be applicable for Chang #2 or other upgrades.
{% endhint %}

The hard fork working group has collated key questions and formed the following frequently asked questions (FAQ) for the benefit of the community.

Currently, we're hosting weekly Q\&A sessions. If you're interested in joining, please join us on [Discord](https://discord.gg/wQU2dPjK3Z).

***

## **Questions for ada holders**

<details>

<summary><strong>Will there be token migration required due to the hard fork?</strong></summary>

No, there will be no token migration required as part of the Chang hard fork. The fork is a protocol update that will be implemented automatically across the network. All ADA tokens will remain fully accessible and functional before, during, and after the hard fork without any need for token migration. However, you should ensure that your wallet and any tools you are using are up-to-date with the latest version to support any new features or improvements introduced by the fork.

</details>

<details>

<summary><strong>What should token holders on-chain and those with staked tokens do?</strong></summary>

For token holders, whether on-chain or staked, there is no specific action required on your part. Your tokens will remain safe and fully functional. However, you should ensure that your wallet and any tools you are using are up-to-date with the latest version to support any new features or improvements introduced by the fork.

</details>

***

## **Questions on the general Chang hard fork**

<details>

<summary><strong>What improvements can users expect from this upgrade?</strong></summary>

The Chang hard fork will introduce significant enhancements to the Cardano ecosystem, introducing a new era of decentralized governance. Chang brings the first step in Cardano’s era of [Voltaire](https://roadmap.cardano.org/en/voltaire/), with the deployment of the [CIP-1694](https://www.1694.io/) governance model. Further included is[ Plutus V3](https://iohk.io/en/blog/posts/2024/02/12/unlocking-more-opportunities-with-plutus-v3/), which brings a host of enhancements and new built-ins for smart contract developers.

</details>

<details>

<summary><strong>What happens if I do not update my node software for the Chang hard fork?</strong></summary>

If you do not update your [node ](https://github.com/IntersectMBO/cardano-node/releases)software to align with the Chang hard fork, your node will become incompatible with the updated blockchain. This may result in your node being unable to process transactions or interact correctly with the updated network.

</details>

<details>

<summary><strong>What is the potential impact if a particular wallet, dApp, etc., isn’t explicitly updated?</strong></summary>

The ecosystem must upgrade to at least [Node 9.1.0](https://github.com/IntersectMBO/cardano-node/releases/tag/9.1.0) to ensure continued compatibility and normal operation.

The fee calculation for Plutus V2 reference scripts has been adjusted, which may cause disruption.

</details>

<details>

<summary><strong>Where can users find the latest information about the Chang upgrade?</strong></summary>

The community can find the latest information on the Chang upgrade on [Intersect's knowledge base](https://docs.intersectmbo.org/cardano/cardano-hardforks-and-upgrades/chang-upgrade), [weekly newsletters](https://intersectmbo.org/news) and through updates posted on official [Twitter](https://twitter.com/intersectmbo).

</details>

<details>

<summary><strong>Are there any expected downtimes or maintenance periods associated with the Chang hard fork?</strong></summary>

No, the network is expected to remain completely operational through the hard fork, although users are warned that tooling they use may require maintenance.

</details>

<details>

<summary><strong>How does the upcoming Chang hard fork differ from Vasil - the last hard fork?</strong></summary>

The Chang Hard Fork on the Cardano network marks a significant advancement from the previous [Vasil ](https://iohk.io/en/blog/posts/2022/09/16/vasil-what-to-expect/)upgrade, focusing on more comprehensive range of improvement:&#x20;

* **Community Driven Governance -** Introduces a governance model that allows ADA holders to participate directly in decision making processes through on chain consensus.&#x20;
* **Delegate Representatives (DReps) -** Plays a crucial role in representing community interests and influencing the network’s future direction.&#x20;
* **Constitution Convention -** An event where stakeholders draft a guiding framework for network governance and community interaction.&#x20;
* **Community Vote on Constitution -** Engages the broader community in voting on the drafted constitution, emphasizing Cardano’s commitment to decentralized governance.&#x20;

This update signifies Cardano’s transition into the [Voltaire era](https://roadmap.cardano.org/en/voltaire/), focusing on scalability, security, and community governance, setting the stage for further innovations and broader adoption.&#x20;

</details>

<details>

<summary><strong>What preparations are involved in the Chang hard fork?</strong></summary>

Preparations for the Chang hard fork include the creation of a detailed Genesis file which will include the [Constitution](https://www.intersectmbo.org/news/cardanos-governance-key-terms-and-milestones), governance policy scripts, the interim constitutional [committee](https://docs.intersectmbo.org/cardano/cardano-governance/overview), and all initial settings for [governance parameters](https://docs.cardano.org/explore-cardano/parameter-guide/). This Genesis file is crucial and will be reviewed thoroughly before it is finalized and implemented.

</details>

***

## Questions on the Hard Fork working group

<details>

<summary><strong>What is the purpose of the hard fork working group?</strong></summary>

The main purpose is to facilitate the sharing of information and support consensus planning among the community and delivery teams contributing to Chang. It aims to ensure all parties are aligned and informed about updates and decisions.

</details>

<details>

<summary><strong>How often does the hard fork working group meet?</strong></summary>

The group meets weekly in the lead-up to a hard fork.

</details>

<details>

<summary><strong>How can the community get involved in the hard fork working group?</strong></summary>

Community members can request to be part of the group. Details on how to join can be found on the [working group page](https://intersect.gitbook.io/intersect-committees-groups/groups-overview/working-groups/hard-fork-working-group). Additionally, staying informed through updates and sharing information helps everyone stay aware of the roadmap and progress.

</details>

***

## **Questions on the Conway Era**

<details>

<summary><strong>Have the changes to the ledger and protocol for the Conway era been finalized, can people add support for them at this point without something possibly changing later on?</strong></summary>

Yes, the changes have been finalized with the exception of any impacts from testing results. Adjustments may be necessary if testing identifies the need for changes.

</details>

***

## **Questions on Testing and Development**

<details>

<summary><strong>How will the Chang hard fork be previewed and tested before full deployment?</strong></summary>

Node 9.1.0 will be previewed and tested concurrently with the [pre-production network](https://docs.cardano.org/cardano-testnets/environments/). This process is controlled by the community, ensuring thorough testing and validation before the full deployment. The preview and pre-production are expected to follow the same governance rules as the [mainnet](https://book.play.dev.cardano.org/env-mainnet.html), ensuring consistency across [environments](https://book.play.dev.cardano.org/environments.html).

</details>

<details>

<summary><strong>How does the community involvement in testing work?</strong></summary>

Community testing is conducted on [SanchoNet ](https://sancho.network/get-started/)as well as other test networks, where various elements including governance policies and committee scripts can be tested. This stage allows for community feedback and is essential for ensuring the robustness of the hard fork. Community members can participate in this testing by engaging with the latest node versions available on [SanchoNet](https://sancho.network/get-started/).

</details>

<details>

<summary><strong>What is the role of stake pool operators upgrading to the latest node for the Chang hard fork?</strong></summary>

Stake Pool Operators play an important (the most important!) part in any hard fork. The community requires them to upgrade prior to a hard fork combinator event. The latest status of SPOs' readiness can be found on our [Ecosystem Readiness page](https://docs.intersectmbo.org/cardano/cardano-hardforks-and-upgrades/chang-upgrade/chang-upgrade-1-readiness).

</details>

<details>

<summary><strong>What happens to Preview, Pre-Production, and Sanchonet following the hard fork?</strong></summary>

* **Sanchonet:** Will continue running for governance testing to ensure thorough testing and transition to new governance mechanisms.
* **Preview:** Will fork shortly after the 9.1.0 release and remain in Chang in governance bootstrapping for the coming months.
* **Pre-Production:** Will be closely aligned with mainnet to ensure consistent testing and readiness.

</details>

<details>

<summary><strong>What are the new parameters/changes for the hard fork?</strong></summary>

New parameters include governance-related changes such as thresholds and committee sizes, and technical changes like the min ref script cost per byte and the Pluto V3 cost model. For detailed information, please refer to the [CIP-1694 documentation](https://www.1694.io/en).

</details>

***

## **Questions relating to Governance, Voltaire, and the Roadmap**

<details>

<summary><strong>How does the Voltaire Era influence the Chang Hard Fork in terms of governance?</strong></summary>

The [Voltaire Era](https://roadmap.cardano.org/en/voltaire/) is a critical and final phase in Cardano’s evolution, introducing robust community-driven [governance mechanisms](https://cardanofoundation.org/governance). This era enables ADA holders to vote on network upgrades and funding proposals through a decentralized governance system. The Chang Hard Fork can be seen as a technical step that supports the principles of the Voltaire Era by enhancing the blockchain’s capabilities, thus preparing it for more sophisticated governance functions that the Voltaire Era aims to implement.

</details>

<details>

<summary><strong>What governance features introduced in the Voltaire Era will be utilized or expanded in the Chang Hard Fork?</strong></summary>

The Chang Hard Fork will introduce [on-chain governance](https://www.1694.io/) to Cardano.

</details>

<details>

<summary><strong>What are some key milestones to watch out for in Cardano’s roadmap for 2024?</strong></summary>

In addition to the Chang Hard Fork, Cardano’s roadmap for 2024 includes significant milestones such as the Cardano Constitution Workshops, Intersect Growth initiative, and advancements in real-world [asset tokenization](https://www.essentialcardano.io/glossary/asset-tokenization). These developments are poised to reshape the landscape of decentralized finance and blockchain technology.&#x20;

</details>

<details>

<summary><strong>How can I stay updated on the hard fork roadmap?</strong></summary>

For the latest updates and detailed information, visit the [Timeline and Dependencies page](https://docs.intersectmbo.org/cardano/cardano-upgrades/hard-forks/chang-timeline-and-dependencies).

</details>

***

## Questions on how to get involved and how to prepare

<details>

<summary><strong>How will changes and updates be communicated to the community?</strong></summary>

Updates and significant changes will be communicated through various channels including [Twitter](https://twitter.com/intersectmbo), [Discord](https://discord.com/invite/wQU2dPjK3Z), and the project’s [knowledge base](https://docs.intersectmbo.org/). Important updates will also be discussed in follow-up meetings, ensuring all stakeholders have the latest information and can provide feedback.

</details>

<details>

<summary><strong>What role does community governance play in the Cardano upgrade roadmap?</strong></summary>

Community governance is a central aspect of Cardano’s upgrade [roadmap](https://roadmap.cardano.org/en/). Through initiatives like the Cardano Constitution Workshops and Delegate Representatives ([DReps](https://docs.intersectmbo.org/cardano/cardano-governance/governance-roles/delegated-representatives-dreps)), the community actively participates in decision-making processes, shaping the future direction of the network.

</details>

<details>

<summary><strong>What steps should users take to prepare for the hard fork?</strong> </summary>

**Here’s what users can do to prepare:**&#x20;

* **Stay informed** - Follow official [Cardano ](https://cardano.org/)and [intersect ](https://www.intersectmbo.org/)channels for announcements and updates regarding the hard fork.
* **Update wallets and applications** - Ensure you’re using the latest versions of [Cardano wallets](https://docs.cardano.org/new-to-cardano/types-of-wallets/) and applications to guarantee compatibility with the new protocol.&#x20;
* **Take part in SanchoNet testing -**  It is a specialized [test ](https://sancho.network/get-started/)network to comprehensively implement and test the tools for the self-governance of the Cardano blockchain.

</details>

***

## Questions on learning and resources

<details>

<summary><strong>Where can I find more information on related topics?</strong></summary>

**Useful resources:**

* [SanchoNet](https://sancho.network/get-started)
* [Cardano Docs](https://docs.cardano.org)
* [CIP-1694](https://www.1694.io/en)

</details>

