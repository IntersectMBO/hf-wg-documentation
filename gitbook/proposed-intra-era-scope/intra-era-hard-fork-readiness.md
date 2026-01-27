# Intra-era hard fork readiness

{% hint style="warning" %}
High level status — waiting on release of hard fork capable Cardano before readiness can be properly reviewed
{% endhint %}

## Readiness and Updating this Page

Readiness is a self-attestation or via spokesperson from the community and ecosystem, facilitated at Intersect, of being technically ready for the next intra-era upgrade.

Signalling readiness is important, this allows the on-chain governance, SPOs and the Constitutional Committee in the case of next intra-era upgrade, to make an informed decision voting for the governance action to enact the hard fork.

The community is encouraged to participate in updating and maintaining the status’ and details contained within this ecosystem readiness page.

You can do so by suggesting updates via this Intersect [GitHub documentation repository](https://github.com/IntersectMBO/hf-wg-documentation) see [how-to guide](../../#updating-hard-fork-readiness-tracker).\
\
Alternatively, if you find any information on this page incorrect or misleading please email: hard-fork@intersectmbo.org and request an update or correction.

## Core Infrastructure Components <a href="#core-infrastructure-components" id="core-infrastructure-components"></a>

Core infrastructure encompasses all technologies included within the Cardano Haskell Node, as well as some key tools.

Spokesperson: Jess

<table><thead><tr><th width="273">Name</th><th width="476">Status</th></tr></thead><tbody><tr><td>Ledger</td><td><mark style="color:green;">Code complete</mark></td></tr><tr><td>Consensus</td><td><mark style="color:green;">Code complete</mark></td></tr><tr><td>Network</td><td><mark style="color:green;">Code complete</mark></td></tr><tr><td>Plutus Core</td><td><mark style="color:green;">Code complete</mark></td></tr><tr><td>Pre-Release Node (SanchoNet)</td><td><mark style="color:$warning;">In Progress — Feb 3rd target</mark></td></tr><tr><td>Full Mainnet Performance and Tracing</td><td><mark style="color:$warning;">In Progress</mark></td></tr><tr><td>Full Mainnet Ready Release</td><td><mark style="color:$warning;">In Progress — Feb 10th target (2 weeks)</mark></td></tr><tr><td>Cardano CLI</td><td><mark style="color:$warning;">In Progress</mark></td></tr><tr><td>DB-Sync</td><td><mark style="color:$warning;">In Progress</mark></td></tr></tbody></table>

***

### Testnets and Governance Actions

Spokesperson: Ryan

#### Testnets

<table><thead><tr><th width="167">Network</th><th width="215">Status</th><th>View via</th></tr></thead><tbody><tr><td>SanchoNet</td><td><mark style="color:$danger;">Blocked — need a node</mark></td><td>waiting on a Pre-Release</td></tr><tr><td>Preview</td><td><mark style="color:$danger;">Blocked — need node</mark></td><td>waiting on a full Release</td></tr><tr><td>PreProd</td><td><mark style="color:$danger;">Blocked — need node</mark></td><td>waiting on a full Release</td></tr></tbody></table>

#### Governance Actions

<table><thead><tr><th width="167">Network</th><th width="130">Action</th><th width="215">Status</th><th>View via</th></tr></thead><tbody><tr><td>SanchoNet</td><td>Cost model update</td><td><mark style="color:$danger;">Blocked — need node</mark></td><td></td></tr><tr><td>SanchoNet</td><td>Hard fork</td><td><mark style="color:$danger;">Blocked — need node</mark></td><td></td></tr><tr><td>Preview</td><td>Cost model update</td><td><mark style="color:$danger;">Blocked — need node</mark></td><td></td></tr><tr><td>Preview</td><td>Hard fork</td><td><mark style="color:$danger;">Blocked — need node</mark></td><td></td></tr><tr><td>PreProd</td><td>Cost model update</td><td><mark style="color:$danger;">Blocked — need node</mark></td><td></td></tr><tr><td>PreProd</td><td>Hard fork</td><td><mark style="color:$danger;">Blocked — need node</mark></td><td></td></tr><tr><td>Mainnet</td><td>Cost model update</td><td><mark style="color:$danger;">Blocked — need node</mark></td><td></td></tr><tr><td>Mainnet</td><td>Hard fork</td><td><mark style="color:$danger;">Blocked — need node</mark></td><td></td></tr></tbody></table>

***

### SPOs

todo

* feed in automated updates once Node available

***

### Exchanges

todo

* start tracking once Node available

***

### Tooling

Spokesperson: Todo

**Tools**

<table><thead><tr><th width="274">Tools</th><th width="206">Status</th><th>Notes</th></tr></thead><tbody><tr><td>cardano-wallet</td><td></td><td>(<a href="https://github.com/cardano-foundation/cardano-wallet/releases">release repository</a>)</td></tr><tr><td>Rosetta</td><td></td><td>(<a href="https://github.com/cardano-foundation/cardano-rosetta/releases">release repository</a>)</td></tr><tr><td>Rosetta-Java</td><td></td><td>(<a href="https://github.com/cardano-foundation/cardano-rosetta-java/releases/tag/1.1.5">release repository</a>)</td></tr><tr><td>GraphQL</td><td></td><td>(<a href="https://github.com/cardano-foundation/cardano-graphql/releases">release repository</a>)</td></tr><tr><td>cntools (guild-operators)</td><td></td><td>(<a href="https://github.com/cardano-community/guild-operators/blob/alpha/docs/Scripts/cntools-changelog.md">change log</a>)</td></tr><tr><td>SPO Scripts (@gitmachtl)</td><td></td><td>(<a href="https://github.com/gitmachtl/scripts/releases">release repository</a>)</td></tr><tr><td>Ogmios</td><td></td><td>(<a href="https://github.com/CardanoSolutions/ogmios/releases">release repository</a>)</td></tr></tbody></table>

**Libraries**

Spokesperson: Todo

<table><thead><tr><th width="287">Library</th><th width="210">Status</th><th>Notes</th></tr></thead><tbody><tr><td>Blaze Cardano</td><td></td><td>(<a href="https://github.com/butaneprotocol/blaze-cardano/releases">release repository</a>)</td></tr><tr><td>Cardano Serialization Library</td><td></td><td>(<a href="https://github.com/Emurgo/cardano-serialization-lib/releases">release repository</a>)</td></tr><tr><td>Cardano Multiplatform Library</td><td></td><td>(<a href="https://github.com/dcSpark/cardano-multiplatform-lib/releases">release repository</a>)</td></tr><tr><td>Cardano JavaScript SDK</td><td></td><td>(<a href="https://github.com/input-output-hk/cardano-js-sdk/releases">release repository</a>)</td></tr><tr><td>Pallas</td><td></td><td>(<a href="https://github.com/txpipe/pallas/releases">release repository</a>)</td></tr><tr><td>Cardano Transaction Library</td><td></td><td>(<a href="https://github.com/Plutonomicon/cardano-transaction-lib/">release repository</a>)</td></tr><tr><td>MeshSDK</td><td></td><td>(<a href="https://github.com/MeshJS/mesh/releases">release repository</a>)</td></tr><tr><td>Aiken</td><td></td><td>(<a href="https://github.com/aiken-lang/aiken/releases">release repository</a>)</td></tr><tr><td>Lucid Evolution</td><td></td><td>(<a href="https://github.com/Anastasia-Labs/lucid-evolution/releases">release repository</a>)</td></tr></tbody></table>

**Indexers**

Spokesperson: Todo

<table><thead><tr><th width="282">Indexers</th><th width="208">Status</th><th>Notes</th></tr></thead><tbody><tr><td>Kupo</td><td></td><td>(<a href="https://github.com/CardanoSolutions/kupo/releases">release repository</a>)</td></tr><tr><td>Oura</td><td></td><td>(<a href="https://github.com/txpipe/oura/releases">release repository</a>)</td></tr><tr><td>Scrolls</td><td></td><td>(<a href="https://github.com/txpipe/scrolls/releases">release repository</a>)</td></tr><tr><td>DB-Sync</td><td></td><td>(<a href="https://github.com/IntersectMBO/cardano-db-sync/releases/tag/13.6.0.4">release repository</a>)</td></tr><tr><td>Carp</td><td></td><td>(<a href="https://github.com/dcSpark/carp/releases">release repository</a>)</td></tr></tbody></table>

**Higher Level Tooling**

Spokesperson: Todo

<table><thead><tr><th width="284">Tools</th><th width="214">Status</th><th>Notes</th></tr></thead><tbody><tr><td>Blockfrost</td><td></td><td>(<a href="https://github.com/blockfrost">repository</a>)</td></tr><tr><td>Koios</td><td></td><td>(<a href="https://github.com/cardano-community/koios-artifacts/releases">release repository</a>)</td></tr><tr><td>Maestro</td><td></td><td>(<a href="https://github.com/maestro-org">repository</a>)</td></tr></tbody></table>

***

### Wallets

Wallet readiness is tracked against their integration against Cardano Node versions, as well as self-reported readiness.

Spokesperson: Ryan

**Light Wallets**

<table><thead><tr><th width="232">Wallet</th><th width="286">Highlevel Status</th><th>Notes</th></tr></thead><tbody><tr><td>Eternl</td><td></td><td></td></tr><tr><td>Eternl (mobile)</td><td></td><td></td></tr><tr><td>Lace</td><td></td><td></td></tr><tr><td>Nufi</td><td></td><td></td></tr><tr><td>MinWallet</td><td></td><td></td></tr><tr><td>Vespr</td><td></td><td></td></tr><tr><td>Tokeo</td><td></td><td></td></tr><tr><td>Yoroi</td><td></td><td></td></tr><tr><td>Typhon</td><td></td><td></td></tr><tr><td>Nami</td><td></td><td></td></tr><tr><td>Flint</td><td></td><td></td></tr></tbody></table>

**Hardware Wallets**

<table><thead><tr><th width="251">Wallet</th><th width="248">Status</th><th>Notes</th></tr></thead><tbody><tr><td>Trezor</td><td><mark style="color:$success;">N/A - no update required</mark></td><td></td></tr><tr><td>Ledger</td><td><mark style="color:$success;">N/A - no update required</mark></td><td></td></tr><tr><td>Keystone</td><td><mark style="color:$success;">N/A - no update required</mark></td><td></td></tr></tbody></table>

#### Full Node / CLI Wallets

<table><thead><tr><th width="251">Wallet</th><th>Status</th><th>Notes</th></tr></thead><tbody><tr><td>Daedalus</td><td></td><td></td></tr><tr><td>AdaLite</td><td></td><td></td></tr><tr><td>CNTools</td><td></td><td></td></tr></tbody></table>

***

### &#x20;Partner-chains + Scalability

Spokesperson: todo

<table><thead><tr><th width="251">Project</th><th>Status</th><th>Notes</th></tr></thead><tbody><tr><td>Partner-chains Toolkit</td><td></td><td></td></tr><tr><td>Midnight</td><td></td><td></td></tr><tr><td>Hydra</td><td></td><td></td></tr><tr><td>Hydroza</td><td></td><td></td></tr><tr><td>Sundail</td><td></td><td></td></tr><tr><td>Midgard</td><td></td><td></td></tr><tr><td>Gummi worm</td><td></td><td></td></tr><tr><td>Mithril</td><td></td><td></td></tr></tbody></table>

***

### Node Implementations

Spokesperson: todo

<table><thead><tr><th width="251">Implementation</th><th width="248">Status</th><th>Notes</th></tr></thead><tbody><tr><td>Acropolis</td><td></td><td></td></tr><tr><td>Amaru</td><td></td><td></td></tr><tr><td>Dingo</td><td></td><td></td></tr><tr><td>Gerlamo</td><td></td><td></td></tr></tbody></table>

***

### DApps & Projects

DApp and project readiness is tracked against self reported readiness.

Spokesperson: Todo

{% hint style="warning" %}
DApps listed on this page are self-attested by the community, to add your DApp please email **hard-fork@intersectmbo.org** or raise a pull request to this public repository via [Github/HF-WG-Documentation](https://github.com/IntersectMBO/hf-wg-documentation/issues/new) ([see how-to](https://github.com/IntersectMBO/hf-wg-documentation?tab=readme-ov-file#contributing))
{% endhint %}

| Name             | Status |
| ---------------- | ------ |
| Axo              |        |
| Book.io/Stuff.io |        |
| Danogo           |        |
| DripDropz        |        |
| Fluid Tokens     |        |
| Genius Yield     |        |
| Levvy Finance    |        |
| Minswap          |        |
| NEWM             |        |
| Snekdotfun       |        |
| Splash           |        |
| Summon           |        |
| SundeaSwap       |        |
| Tempo            |        |
| UnFrack.it       |        |
| USDM             |        |
| Wanchain         |        |

{% hint style="warning" %}
DApps listed on this page are self-attested by the community, to add your DApp please email **hard-fork@intersectmbo.org** or raise a pull request to this public repository via [Github/HF-WG-Documentation](https://github.com/IntersectMBO/hf-wg-documentation/issues/new) ([see how-to](https://github.com/IntersectMBO/hf-wg-documentation?tab=readme-ov-file#contributing))
{% endhint %}

***
