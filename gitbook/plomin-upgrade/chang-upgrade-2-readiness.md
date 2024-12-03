---
description: >-
  This page outlines the engineering and ecosystem readiness for the Plomin
  hardfork upgrade
---

# Plomin upgrade readiness

{% hint style="info" %}
Intersect and the hard fork working group plays the role of coordinator, as a functional servant-leader on behalf of the community and delivery teams working on hard fork activity. The functional teams within Intersect will work with the various committees, working groups, and delivery teams, relaying information here on the knowledge base. Ultimately the date for the hard fork is directly influenced by the community, the relevant constitutional approval and required on-chain voting.
{% endhint %}

## Core Infrastructure Components <a href="#core-infrastructure-components" id="core-infrastructure-components"></a>

Core infrastructure encompasses all technologies included within the Cardano Node, as well as some key tools.

<table><thead><tr><th width="197">Release</th><th></th></tr></thead><tbody><tr><td><a href="https://github.com/IntersectMBO/cardano-node/releases">10.1.3</a></td><td><p><em><strong>It is required that users upgrade to this version of the node.</strong></em></p><p></p><p>Node <code>10.1.3</code> is a mainnet-ready release of the Cardano node that is capable of crossing the Chang#2 hard fork. This update addresses a ledger issue where DRep delegations could be removed under some conditions. This inadvertently affected the ability to withdraw rewards in Protocol Version 10, and changed the stake distribution for some DReps.</p><p></p><p><strong>For further details about <code>cardano-node 10.1.3</code> please see the</strong> <a href="https://github.com/IntersectMBO/cardano-node/releases/tag/10.1.1"><strong>release notes for <code>10.1.1</code></strong></a><strong>, since significant upgrades were performed compared to previous versions of the node.</strong></p></td></tr></tbody></table>

### 10.1.3 Ledger replay in Preview and Pre-production

Due to the nature of [Issue #4772](https://github.com/IntersectMBO/cardano-ledger/issues/4772#issuecomment-2499160212) effect on hard forked networks running Protocol version 10.0, all nodes on testnets will require a re-synchronisation from genesis. This will not be required for mainnet, as it is yet to hard fork for Protocol version 10.0 (via Plomin).

Once upgraded to 10.1.3 in any testnet, the ledger directory can be deleted to force the node to resync the network from genesis. This will ensure that the node’s ledger state will be reconstructed correctly, without the effect of Issue #4772.

{% code overflow="wrap" %}
```
To perform ledger replay:
1.	Ensure the node version is updated to 10.1.3,
2.	Stop the node service (if running),
3.	Delete ledger state (path may vary by installation type, e.g.: $ rm /var/lib/cardano-node/db-$NETWORK/ledger/*),
4.	Restart the node service and the ledger replay from genesis will occur
```
{% endcode %}

{% hint style="info" %}
To reiterate this step is not required for mainnet.
{% endhint %}

For support with this upgrade on testnets feel free to ask questions via discord at [#hfwg-plomin](https://discord.gg/Hxtz9f38Ep) on the Intersect server or #spo-testnet via the [IOHK server](https://discord.gg/inputoutput).

***

{% hint style="warning" %}
Note that, although staking rewards will continue to be earned as usual, in order to withdraw their rewards, following the Plomin hard fork, Ada holders will need to delegate to a DRep, which may be one of the pre-defined options, a single key or a Plutus v3 script. Until the hard fork, rewards may be withdrawn normally. Although following the hard fork, rewards may not be withdrawn unless a DRep is delegated to, rewards will continue to accrue to the Ada holder normally, regardless of whether or not a DRep is delegated to.
{% endhint %}

{% hint style="warning" %}
There are a number of breaking changes, including changes to era-agnostic commands. The following are designated as legacy commands:

* `address` Payment address commands
* `stake-address` Stake address commands
* `key` Key utility commands
* `transaction` Transaction commands
* `node` Node operation commands
* `stake-pool` Stake pool commands
* `query` Node query commands. Will query the local node whose Unix domain socket is obtained from the `CARDANO_NODE_SOCKET_PATH` environment variable.
* `genesis` Genesis block commands
* `governance` Governance commands
* `text-view` Commands for dealing with Shelley TextView files. Transactions, addresses etc are stored on disk as TextView files.

For example, the previous top level commands `query` and `stake-pool` are now available as `latest query` and `latest stake-pool.`

Please read full release notes [here](https://github.com/IntersectMBO/cardano-node/releases/tag/10.1.1).
{% endhint %}

All test nets now have the capability to test node 10.x releases.&#x20;

***

## Readiness and Updating this Page

Readiness is a self-attestation from the community and ecosystem, facilitated at Intersect, of being technically ready for the Plomin upgrade.&#x20;

Signalling readiness is important, this allows the on-chain governance, SPOs and the ICC in the case of Plomin upgrade, to make an informed decision voting for the governance action to enact the hard fork.

The community is encouraged to participate in updating and maintaining the status’ and details contained within this ecosystem readiness page.

You can do so by suggesting updates via this Intersect [GitHub documentation repository](https://github.com/IntersectMBO/hf-wg-documentation), a simple how to guide provided [here](../../).\
\
Alternatively, if you find any information on this page incorrect or misleading please email: hard-fork@intersectmbo.org and request an update or correction.

***

### Governance Actions

Governance actions need to be enacted/voted on-chain for the hard fork to take place, you can keep track of the applicable governance actions for Plomin upgrade below.

<table><thead><tr><th>Network</th><th>Action</th><th>Status</th><th width="195">Governance Actors</th><th>View via</th></tr></thead><tbody><tr><td><mark style="color:green;">Preview</mark></td><td><mark style="color:green;">PPU Cost Model</mark></td><td><mark style="color:green;">Enacted</mark></td><td>CC</td><td><a href="https://preview.cardanoscan.io/govAction/gov_action1rarl8newf7gsn03wl6gc9jhqsvr72autml4zz58xjq7y3mw2pw8sqsymael">CardanoScan</a></td></tr><tr><td><mark style="color:green;">Preview</mark></td><td><mark style="color:green;">Hard Fork</mark></td><td><mark style="color:green;">Enacted</mark></td><td>SPO's, CC</td><td><a href="https://preview.cardanoscan.io/govAction/gov_action1qjdwt4sjktagy4j4szgn8vpr6cx8lr9vdq7z0r8ethskytj9jtesqvrtlga">CardanoScan</a></td></tr><tr><td><mark style="color:green;">Pre-production</mark></td><td><mark style="color:green;">PPU Cost Model</mark></td><td><mark style="color:green;">Enacted</mark></td><td>CC</td><td><a href="https://preprod.cardanoscan.io/govAction/gov_action1k5hsy2yw8n5v0et524fz7nkap8qj09m5nckmxgycajlfszmyt4zsqp0n7ft?tab=action">CardanoScan</a></td></tr><tr><td><mark style="color:green;">Pre-production</mark></td><td><mark style="color:green;">Hard Fork</mark></td><td><mark style="color:green;">Enacted</mark></td><td>SPO's, CC</td><td><a href="https://preprod.cardanoscan.io/govAction/gov_action1eje876cdtrp94celmqsmvtpc0afrpkhfxzhaqayflg7l26h9v53qqnjsjww?tab=action">CardanoScan</a></td></tr><tr><td><mark style="color:orange;">Mainnet</mark></td><td><mark style="color:orange;">PPU Cost Model</mark></td><td><mark style="color:orange;">On-Chain</mark></td><td>CC</td><td><a href="https://cardanoscan.io/govAction/gov_action1k2jertppnnndejjcglszfqq4yzw8evzrd2nt66rr6rqlz54xp0zsq05ecsn">CardanoScan</a></td></tr><tr><td>Mainnet</td><td>Hard Fork</td><td>Pending</td><td>SPO's, CC</td><td></td></tr></tbody></table>

<details>

<summary><strong>Status key</strong></summary>

**Enacted**: Governance action has been applied on chain&#x20;

**Ratified**: Governance action has reached required voting thresholds, and will normally be enacted next epoch&#x20;

**Expired** - Governance action has failed to reach the required thresholds&#x20;

**On-Chain** - governance action has been submitted to the blockchain and is available for voting&#x20;

**Pending** - Governance action has not yet been submitted to the blockchain

</details>

Metadata for all Intersect governance actions can be found here on the [Intersect Gitbook repository](https://github.com/IntersectMBO/governance-actions).

***

### SPOs

Stake pool operators should upgrade to a supported mainnet node 10.x version in readiness for the hard fork. Below we compare the prevalence of Cardano blocks created by Node versions.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

As of November 28th 2024, 41% of blocks created on mainnet where created using node 10.x version. Live data can be seen via tooling such as [Pooltool.io](https://pooltool.io/networkhealth)

***

### Tooling

Tooling readiness is supported from version Node 10.1.1 compatible releases.

**Libraries**

<table><thead><tr><th width="274">Library</th><th width="210">Status</th><th>Notes</th></tr></thead><tbody><tr><td>Cardano Serialization Library</td><td></td><td></td></tr><tr><td>Cardano Multiplatform Library</td><td></td><td></td></tr><tr><td>Cardano JavaScript SDK</td><td></td><td></td></tr><tr><td>Pallas</td><td></td><td></td></tr><tr><td>Cardano Transaction Library</td><td></td><td></td></tr><tr><td>MeshSDK</td><td></td><td></td></tr><tr><td>Aiken</td><td></td><td></td></tr></tbody></table>

**Tools**

<table><thead><tr><th width="274">Tools</th><th width="206">Status</th><th>Notes</th></tr></thead><tbody><tr><td>cardano-wallet</td><td><mark style="color:green;">Ready</mark></td><td><a href="https://github.com/cardano-foundation/cardano-wallet/releases/tag/v2024-11-18">Release v2024-11-18</a></td></tr><tr><td>Rosetta</td><td></td><td></td></tr><tr><td>GraphQL</td><td></td><td></td></tr><tr><td>cntools (guild-operators)</td><td></td><td></td></tr><tr><td>SPO Scripts (@gitmachtl)</td><td></td><td></td></tr><tr><td>Ogmios</td><td><mark style="color:green;">Ready</mark></td><td><a href="https://github.com/CardanoSolutions/ogmios/releases/tag/v6.9.0">Ogmios v6.9.0</a></td></tr></tbody></table>

**Indexers**

<table><thead><tr><th width="282">Indexers</th><th width="208">Status</th><th>Notes</th></tr></thead><tbody><tr><td>Kupo</td><td></td><td></td></tr><tr><td>Oura</td><td></td><td></td></tr><tr><td>Scrolls</td><td></td><td></td></tr><tr><td>DB-Sync</td><td><mark style="color:green;">Ready</mark></td><td><a href="https://github.com/IntersectMBO/cardano-db-sync/releases/tag/13.6.0.1">DB Sync 13.6.0.1</a></td></tr><tr><td>Carp</td><td></td><td></td></tr></tbody></table>

**Higher Level Tooling**

<table><thead><tr><th width="284">Tools</th><th width="214">Status</th><th>Notes</th></tr></thead><tbody><tr><td>Blockfrost</td><td></td><td></td></tr><tr><td>Koios</td><td></td><td></td></tr><tr><td>Maestro</td><td></td><td></td></tr></tbody></table>

***

### Wallets

Wallet readiness is tracked against their integration against Cardano Node versions, as well as self-reported readiness

**Light Wallets**

<table><thead><tr><th width="232">Wallet</th><th width="286">Highlevel Status</th><th>Preview Network</th></tr></thead><tbody><tr><td>Begin</td><td></td><td></td></tr><tr><td>Eternl</td><td></td><td></td></tr><tr><td>Eternl (mobile)</td><td></td><td></td></tr><tr><td>Lace</td><td></td><td></td></tr><tr><td>Nami</td><td></td><td></td></tr><tr><td>Nufi</td><td></td><td></td></tr><tr><td>Vespr</td><td></td><td></td></tr><tr><td>Vespr (Mobile)</td><td></td><td></td></tr><tr><td>Tokeo</td><td></td><td></td></tr><tr><td>Yoroi</td><td></td><td></td></tr><tr><td>Yoroi (Mobile)</td><td></td><td></td></tr><tr><td>Gero</td><td></td><td></td></tr><tr><td>Gero Mobile</td><td></td><td></td></tr><tr><td>Typhon</td><td></td><td></td></tr><tr><td>Flint</td><td></td><td></td></tr></tbody></table>

**Hardware Wallets**

<table><thead><tr><th width="251">Wallet</th><th>Status</th><th>Notes</th></tr></thead><tbody><tr><td>Trezor</td><td></td><td></td></tr><tr><td>Ledger (Nano S+, Nano X, Stax)</td><td></td><td></td></tr><tr><td>Ledger (Nano S)</td><td></td><td></td></tr><tr><td>Keystone</td><td></td><td></td></tr></tbody></table>

#### Full Node / CLI Wallets

<table><thead><tr><th width="251">Wallet</th><th>Status</th><th>Notes</th></tr></thead><tbody><tr><td>Daedalus</td><td></td><td></td></tr><tr><td>AdaLite</td><td></td><td></td></tr><tr><td>CNTools</td><td></td><td></td></tr></tbody></table>

***

### DApps & Projects

DApp and project readiness is tracked against self reported readiness. Although this hard fork will remain in the Conway era DApp developers should refer to the [release notes](https://github.com/IntersectMBO/cardano-node/releases) and confirm readiness for the intra-era hard fork.

| Name          | Status |
| ------------- | ------ |
| Asda Finance  |        |
| Astarter      |        |
| Axo           |        |
| Book.io       |        |
| Cerra         |        |
| Charli3       |        |
| CherryLend    |        |
| Clarity       |        |
| Comment       |        |
| Danogo        |        |
| DexHunter     |        |
| Encoins       |        |
| Fluid Tokens  |        |
| Genius Yield  |        |
| Iagon         |        |
| JPG.Store     |        |
| Lending Pond  |        |
| Lenfi         |        |
| Levvy Finance |        |
| Moneta        |        |
| MuseliSwap    |        |
| MyUSD         |        |
| NEWM          |        |
| NMKR          |        |
| Optim         |        |
| Orcfax        |        |
| Revuto        |        |
| Rosenbridge   |        |
| Saturn Swap   |        |
| Spectrum      |        |
| Splash        |        |
| Summon        |        |
| TeddySwap     |        |
| USDM          |        |
| VyFinance     |        |
| Wingriders    |        |

***

{% hint style="info" %}
The community is encouraged to participate in updating and maintaining the status’ and details contained within this ecosystem readiness page.

You can do so by suggesting updates via this Intersect [GitHub documentation repository](https://github.com/IntersectMBO/hf-wg-documentation), a simple how to guide provided [here](../../).\
\
Alternatively, if you find any information on this page incorrect or misleading please email hard-fork@intersectmbo.org and request an update or correction.
{% endhint %}
