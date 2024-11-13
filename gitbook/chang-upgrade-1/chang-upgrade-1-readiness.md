---
description: >-
  This page outlines the engineering and ecosystem readiness for the Chang
  hardfork.
---

# Chang Upgrade #1 readiness

{% hint style="info" %}
Chang #1 hard fork successfully occurred 1st September 2024 on Cardano Mainnet.

This page is an attestation of readiness reported at that time, which was used by the hard fork working group to make the recommendation to hard fork.

Please note that the evidence and attestations below are no longer up to date, further releases or versions could now be available - please check with the provider of any tool, product or service prior to use.&#x20;
{% endhint %}

## Hard fork recommendation

The following information was reviewed by the hard fork working group and seen as sufficient evidence to recommend enacting the Chang #1 hard fork on Mainnet

* The hardfork working group met on 2024-08-28 to discuss the Go / No Decision, the group unanimously agreed to proceed with the hardfork mainnet on 1st September.
  * The hardfork action was subsequently signed by the genesis keys and submitted to chain: [see transaction via cardanoscan](https://cardanoscan.io/transaction/9ba6a580bceb8f94e65a683e8291c89382835f46e3cf928eb521f5581ade4820?tab=protocolupdates).
* By **Stake**, over <mark style="color:green;">**92%**</mark> of **SPOs** on 9.1.0 - the desired hard fork threshold for SPOs has been reached :tada:
* By **Liquidity,** over <mark style="color:green;">**92%**</mark> of Exchanges on 9.1.0 - the desired hard fork threshold for exchanges has been reached :tada:
* TVL by top 20 DApp projects are over <mark style="color:green;">**83%**</mark> ready, with steady progress and testing on PreProd from August 24.

***

## Core Infrastructure Components

Core infrastructure encompasses all technologies included within the Cardano Node, as well as key tools.

{% hint style="success" %}
High-level status: <mark style="color:green;">**Ready**</mark>
{% endhint %}

<table><thead><tr><th width="273">Name</th><th width="476">Status </th></tr></thead><tbody><tr><td>Ledger</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Consensus</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Network</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Plutus Core</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Cardano CLI</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>DB-Sync</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>End to End Testing</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Performance and Tracing </td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr></tbody></table>

***

### Environments

Cardano has a range of network environments, and each will require a Hard Fork, below we compare the prevalence of Cardano blocks created by Node versions within the last 8 hours. 75%+ will indicate readiness for the Hard Fork to Conway ( Protocol 9.0)

{% hint style="info" %}
High-level status: <mark style="color:green;">**Ready**</mark>
{% endhint %}

<table><thead><tr><th width="138">Network</th><th width="170">9.1.0 Blocks (%)</th><th width="136">Ledger Era</th><th>Governance</th></tr></thead><tbody><tr><td>MainNet</td><td><mark style="color:green;">92<strong>%</strong></mark></td><td>Babbage</td><td>N/A</td></tr><tr><td>PreProd</td><td><mark style="color:green;"><strong>95%</strong></mark></td><td>Conway</td><td>Bootstrapping Phase</td></tr><tr><td>Preview</td><td><mark style="color:green;"><strong>84%</strong></mark></td><td>Conway</td><td>Bootstrapping Phase</td></tr><tr><td>SanchoNet</td><td><mark style="color:green;"><strong>100%</strong></mark></td><td>Conway</td><td>Full (post-bootstrapping)</td></tr></tbody></table>

For _live_ numbers please visit [Cexplorer/versions](https://cexplorer.io/versions)

| Total Stake Pools | Stake Pools Ready | Stake Ready % |
| ----------------- | ----------------- | ------------- |
| 3097              | 1163              | 92.46 %       |

For the latest numbers please visit: [cardanoscan](https://cardanoscan.io/changreadiness)

{% hint style="info" %}
Section maintained by IOG Core Tech Team

Last Updated; 2024-08-27
{% endhint %}

***

### Exchange Readiness

Exchange readiness is tracked against the top exchanges by ADA liquidity (as reported by [Cexplorer/hfs](https://cexplorer.io/hfs)).

For the latest info on _Exchanges by Liquidity_ please visit: [Cardanoscan](https://cardanoscan.io/changreadiness) (source) and [Cexplorer](https://cexplorer.io/hfs).

<table><thead><tr><th width="377">Exchange</th><th width="358">Status</th></tr></thead><tbody><tr><td>AscendEX (BitMax)</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Azbit</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Binance</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Binance US</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>BingX</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>BitBNS</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Bitfinex</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Bithumb</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Bitkub</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>BitMart</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Bitrue</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Bitvavo</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Blockchain.com</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>BTSE</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Bybit</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>CEX.IO</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Changelly PRO</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Coinbase Exchange</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>CoinEx</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Crypto.com Exchange</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>EXMO</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>FMFW.io</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Gate.io</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>HitBTC</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>HTX</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Indodax</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Kraken</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>KuCoin</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>LATOKEN</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>LBank</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>LCX Exchange</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Mercado Bitcoin</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>MEXC</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>OKCoin Japan</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>OKX</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>P2B</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Poloniex</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>TokoCrypto</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Upbit</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>WhiteBIT</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>WOO X</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Bitbank</td><td><mark style="color:orange;"><strong>In Progress</strong></mark></td></tr><tr><td>Bitstamp</td><td><mark style="color:orange;"><strong>In Progress</strong></mark></td></tr><tr><td>Coinstore</td><td><mark style="color:orange;"><strong>In Progress</strong></mark></td></tr><tr><td>DigiFinex</td><td><mark style="color:orange;"><strong>In Progress</strong></mark></td></tr><tr><td>Paribu</td><td><mark style="color:orange;"><strong>In Progress</strong></mark></td></tr><tr><td>XT.COM</td><td><mark style="color:orange;"><strong>In Progress</strong></mark></td></tr></tbody></table>

{% hint style="info" %}
Section maintained by Cardano Foundation

Last Updated; 2024-08-29
{% endhint %}

***

### Tooling Readiness

Tooling readiness is supported from version [Node 9.1.0 ](https://github.com/IntersectMBO/cardano-node/releases/tag/9.1.0)compatible releases and reported by each team.

{% hint style="info" %}
High-level status: <mark style="color:orange;">**In Progress**</mark>
{% endhint %}

#### Low-Level Tooling

We define Low-Level Tooling, as tools which are required by higher-level tools, dApps, and wallets.

Libraries

<table><thead><tr><th width="189">Library</th><th>Status</th></tr></thead><tbody><tr><td>Cardano Serialization Library</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Cardano Multiplatform Library</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Cardano JavaScript SDK</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Pallas</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Cardano Transaction Library</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>MeshSDK</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Aiken</td><td><mark style="color:orange;"><strong>In Progress</strong></mark></td></tr></tbody></table>

Tools

<table><thead><tr><th width="371">Tools</th><th width="373">Status </th></tr></thead><tbody><tr><td>cardano-wallet</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Rosetta</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>GraphQL</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>cntools (guild-operators)</td><td><mark style="color:orange;"><strong>In Progress</strong></mark></td></tr><tr><td>SPO Scripts (@gitmachtl)</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Ogmios</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr></tbody></table>

Indexers

| Indexers | Status                                             |
| -------- | -------------------------------------------------- |
| Kupo     | <mark style="color:orange;">**In Progress**</mark> |
| Oura     | <mark style="color:green;">**Ready**</mark>        |
| Scrolls  | <mark style="color:orange;">**In Progress**</mark> |
| DB-Sync  | <mark style="color:green;">**Ready**</mark>        |
| Carp     | <mark style="color:green;">**Ready**</mark>        |

#### Higher Level Tooling

<table><thead><tr><th width="167">Tools</th><th>Status</th></tr></thead><tbody><tr><td>Blockfrost</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Koios</td><td><mark style="color:green;"><strong>Ready</strong></mark> (<a href="https://t.me/CardanoKoios/9764/13866">telegram announcement here</a>)</td></tr><tr><td>Maestro</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr></tbody></table>

{% hint style="info" %}
Section maintained by Cardano Foundation

Last updated; 2024-08-28
{% endhint %}

***

### Wallets Readiness

Wallet readiness is tracked against their integration against Cardano Node versions, as well as self-reported readiness.

{% hint style="info" %}
High-level status: <mark style="color:orange;">**In Progress**</mark>
{% endhint %}

#### Light Wallets

<table><thead><tr><th width="175">Wallet</th><th width="286">Highlevel Status</th><th>Preview Network</th></tr></thead><tbody><tr><td>Begin</td><td><mark style="color:green;"><strong>Ready</strong></mark><strong> (no governance features)</strong></td><td><mark style="color:green;"><strong>Ready</strong></mark><strong> (no governance features)</strong></td></tr><tr><td>Eternl</td><td><mark style="color:green;"><strong>Ready</strong></mark></td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Eternl (mobile)</td><td><mark style="color:green;"><strong>Ready</strong></mark></td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Lace</td><td><mark style="color:green;"><strong>Ready</strong></mark></td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Nami</td><td><mark style="color:green;"><strong>Ready</strong></mark><strong> (no governance features)</strong></td><td><mark style="color:green;"><strong>Ready</strong></mark><strong> (no governance features)</strong></td></tr><tr><td>Nufi</td><td><mark style="color:green;"><strong>Ready</strong></mark></td><td><mark style="color:green;"><strong>Ready</strong></mark><strong> (no governance features)</strong></td></tr><tr><td>Vespr</td><td><mark style="color:green;"><strong>Ready</strong></mark></td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Vespr (Mobile)</td><td><mark style="color:green;"><strong>Ready</strong></mark></td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Tokeo</td><td><mark style="color:green;"><strong>Ready</strong></mark><strong> (no governance features)</strong></td><td><mark style="color:green;"><strong>Ready</strong></mark><strong> (no governance features)</strong></td></tr><tr><td>Yoroi</td><td><mark style="color:green;"><strong>Ready</strong></mark></td><td><mark style="color:green;"><strong>Ready</strong></mark><strong> (via nightly)</strong></td></tr><tr><td>Yoroi (Mobile)</td><td><mark style="color:green;"><strong>Ready</strong></mark></td><td><mark style="color:green;"><strong>Ready</strong></mark><strong> (no governance features)</strong></td></tr><tr><td>Gero</td><td><mark style="color:orange;"><strong>In Progress</strong></mark></td><td><mark style="color:orange;"><strong>In Progress</strong></mark></td></tr><tr><td>Gero Mobile</td><td><mark style="color:orange;"><strong>In Progress</strong></mark></td><td><mark style="color:orange;"><strong>In progress</strong></mark></td></tr><tr><td>Typhon</td><td><mark style="color:orange;"><strong>In Progress</strong></mark></td><td><mark style="color:orange;"><strong>In progress</strong></mark></td></tr><tr><td>Flint</td><td><mark style="color:red;"><strong>Won't progress</strong></mark> <strong>(</strong><a href="https://x.com/FlintWallet/status/1828184961960308832?t=0eIBBMnAY5feMTOlojFlSg&#x26;s=19"><strong>X post</strong></a><strong>)</strong></td><td><mark style="color:red;"><strong>Won't progress</strong></mark> <strong>(</strong><a href="https://x.com/FlintWallet/status/1828184961960308832?t=0eIBBMnAY5feMTOlojFlSg&#x26;s=19"><strong>X post</strong></a><strong>)</strong></td></tr></tbody></table>

#### **Key**

* **no governance features:** Indicates that a wallet has updated their infrastructure to be able to survive the hardfork. But they have not added any new features to be able to interact with on-chain governance.

#### Hardware Wallets

<table><thead><tr><th width="177">Wallet</th><th>Readiness</th></tr></thead><tbody><tr><td>Trezor</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Ledger (Nano S+, Nano X, Stax)</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Ledger (Nano S)</td><td><mark style="color:green;"><strong>Ready</strong></mark><strong> (see</strong> <a href="https://x.com/ATADA_Stakepool/status/1828788278373548248"><strong>announcement</strong></a><strong>)</strong></td></tr><tr><td>Keystone</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr></tbody></table>

#### Full Node / CLI Wallets

<table><thead><tr><th width="182">Wallet</th><th>Readiness</th></tr></thead><tbody><tr><td>Daedalus</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>AdaLite</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>CNTools</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr></tbody></table>

{% hint style="info" %}
Section maintained by the Wallets Working Group

Last updated; 2024-08-30
{% endhint %}

***

### DApp Project Readiness

DApp and project readiness is tracked against self reported readiness, dApp developers do need to prepare as Conway will change costing around the use of reference scripts.

_Please see_ [_Ref Script Cost Calculator_](https://docs.google.com/spreadsheets/d/1KFJCCbkDE5GaghlD4rDXB12pqLKnDFUNOKi0WErp\_-Q/edit?gid=0#gid=0) _from IOG Core Team._

{% hint style="info" %}
High-level status: <mark style="color:orange;">**In Progress**</mark>
{% endhint %}

<table><thead><tr><th width="398">Project</th><th width="355">Status</th></tr></thead><tbody><tr><td>Minswap</td><td><mark style="color:green;"><strong>Ready</strong></mark> (<a href="https://x.com/longminswap/status/1825919688423133549">X post</a>)</td></tr><tr><td>Indigo</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Liqwid (finance)</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Sundae Labs</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Djed</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Lenfi</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Wingriders</td><td><mark style="color:green;"><strong>Ready</strong></mark> (<a href="https://x.com/wingriderscom/status/1824124808386265386">X post</a>)</td></tr><tr><td>MuseliSwap</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>VyFinance</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Levvy Finance</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Danogo</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Astarter</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Saturn Swap</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>CherryLend</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Charli3</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>NEWM</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Orcfax</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Genius Yield</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Iagon</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>NMKR</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Summon</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>Optim</td><td><mark style="color:orange;"><strong>In Progress</strong></mark></td></tr><tr><td>Fluid Tokens</td><td><mark style="color:orange;"><strong>In Progress</strong></mark></td></tr><tr><td>Axo</td><td><mark style="color:orange;"><strong>In Progress</strong></mark></td></tr><tr><td>Spectrum</td><td><mark style="color:orange;"><strong>In Progress</strong></mark></td></tr><tr><td>Splash</td><td>TBC</td></tr><tr><td>TeddySwap</td><td><strong>TBC</strong></td></tr><tr><td>Cerra</td><td><strong>TBC</strong></td></tr><tr><td>21.co</td><td><strong>TBC</strong></td></tr><tr><td>Aada Finance</td><td><strong>TBC</strong></td></tr><tr><td>Book.io</td><td><strong>TBC</strong></td></tr><tr><td>Clarity</td><td><strong>TBC</strong></td></tr><tr><td>DexHunter</td><td><strong>TBC</strong></td></tr><tr><td>Encoins</td><td><strong>TBC</strong></td></tr><tr><td>JPG.Store</td><td><strong>TBC</strong></td></tr><tr><td>Lending Pond</td><td><strong>TBC</strong></td></tr><tr><td>Moneta</td><td><strong>TBC</strong></td></tr><tr><td>MyUSD</td><td><strong>TBC</strong></td></tr><tr><td>Revuto</td><td><strong>TBC</strong></td></tr><tr><td>Rosenbridge</td><td><strong>TBC</strong></td></tr><tr><td>USDM</td><td><strong>TBC</strong></td></tr></tbody></table>

TVL Numbers supplied via [Defi Lama](https://defillama.com/chain/Cardano).

{% hint style="info" %}
Section maintained by Anatasia Labs

Last updated; 2024-08-30
{% endhint %}

### Supporting Governance Initiatives - Readiness

The Chang #1 hardfork will introduce governance to Cardano, specific tooling is being developed to support the governance model.

Whilst having governance tools prepared for mainnet hardfork is ideal, these tools should not block mainnet hardfork.

#### Governance Tooling

{% hint style="info" %}
High-level status: <mark style="color:orange;">**In Progress**</mark>
{% endhint %}

<table><thead><tr><th width="170">Tool</th><th width="216">Status</th></tr></thead><tbody><tr><td>GovTool</td><td><mark style="color:orange;"><strong>In Progress</strong></mark></td></tr><tr><td>Constitutional Committee Portal</td><td><mark style="color:orange;"><strong>In Progress</strong></mark></td></tr><tr><td>DRep Campaign Platform</td><td><mark style="color:orange;"><strong>In Progress</strong></mark></td></tr></tbody></table>

{% hint style="info" %}
Section maintained by the Governance Tools Working Group

Last Updated; 2024-08-30
{% endhint %}

#### Interim Constitutional Committee Readiness

Interim Constitutional Committee readiness is tracked against training module completion as well as on-chain mainnet cold credential creation.

{% hint style="success" %}
High-level status: <mark style="color:green;">**Ready**</mark>
{% endhint %}

<table><thead><tr><th width="290" align="center">Member</th><th>Readiness</th></tr></thead><tbody><tr><td align="center">Cardano Atlantic Council</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td align="center">Cardano Japan</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td align="center">Cardano Foundation</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td align="center">Eastern Cardano Council</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td align="center">Emurgo</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td align="center">Intersect</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td align="center">Input Output</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr></tbody></table>

{% hint style="info" %}
Section maintained by IOG Voltaire Team
{% endhint %}

#### DRep Pioneer Program                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         &#x20;

DRep Pioneer Program readiness is tracked against total number of participants who have gone through a DRep pioneer program workshop.\
Learn more and get involved: [DRep Pioneer Program Overview](https://app.gitbook.com/o/Prbm1mtkwSsGWSvG1Bfd/s/VNa3QAZtN9ihYGiFy8AM/).

{% hint style="info" %}
High-level status: <mark style="color:green;">**Ready**</mark>
{% endhint %}

<table><thead><tr><th width="284">Total DRep Training Completed</th><th>Status</th></tr></thead><tbody><tr><td>50</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>75</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>100</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>150</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr><tr><td>300</td><td><mark style="color:green;"><strong>Ready</strong></mark></td></tr></tbody></table>

{% hint style="info" %}
Section maintained by Intersect DRep Pioneer Program lead
{% endhint %}

***

More information on the [Major Release Process](https://docs.intersectmbo.org/cardano/cardano-upgrades/major-release-process) is also available, as well as a [frequently asked questions](https://docs.intersectmbo.org/cardano/cardano-upgrades/hard-forks/hard-fork-frequently-asked-questions) page.
