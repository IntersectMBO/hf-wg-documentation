---
description: >-
  This page outlines high-level the dependencies and context for the Chang #1
  hardfork.
hidden: true
---

# Chang Upgrade #1 overview

{% hint style="info" %}
Chang #1 hard fork successfully occurred 1st September 2024 on Cardano Mainnet

No further updates will be made to this page.&#x20;
{% endhint %}

Intersect plays the role of coordinator, as a functional servant-leader on behalf of the community and delivery teams working on hard fork activity. The functional teams within Intersect will work with the various committees, working groups, and delivery teams, relaying information here on the knowledge base. Ultimately the date for the hard fork is directly influenced by the community fulfilling the requirements detailed below.

***

## Chang Upgrade Release

The [Chang upgrade](https://docs.intersectmbo.org/cardano/cardano-upgrades/hard-forks/chang-upgrade) will stagger the release of governance functionality, easing adoption and onboarding for those with new or additional roles in governance.&#x20;

1. Chang Upgrade #1 will deploy governance features to Cardano and enter the technical bootstrapping phase as described in [CIP-1694 Bootstrapping Phase](https://github.com/cardano-foundation/CIPs/blob/master/CIP-1694/README.md#bootstrapping-phase)
2. Chang Upgrade #2 moves CIP-1694 out of technical bootstrapping phase and unlocks the final features of on-chain governance including DRep participation and all governance actions

Further information on [CIP-1694](https://www.1694.io/) and the interim bootstrapping period is available.

***

## Chang Upgrade #1 Events

In the lead-up to Change Upgrade #1 the following sequence of events will occur, driven by community participation and adoption.&#x20;

<table><thead><tr><th width="389">Step</th><th>Owner</th><th>Status</th></tr></thead><tbody><tr><td>Node 9.0.0 is released</td><td>IOG Core Team</td><td><mark style="color:green;"><strong>Complete</strong></mark></td></tr><tr><td>Parameters &#x26; final genesis file will be prepared (required for 9.1.0)</td><td>IOG Core Team</td><td><mark style="color:green;"><strong>Complete</strong></mark></td></tr><tr><td>Node 9.1.0 is released</td><td>IOG Core Team</td><td><mark style="color:green;"><strong>Complete</strong></mark></td></tr><tr><td><strong>Preview</strong> infrastructure upgraded to Node 9.1.0</td><td>Community</td><td><mark style="color:green;"><strong>Complete</strong></mark></td></tr><tr><td><strong>Preview h</strong>ardforked with Node 9.1.0</td><td>Community</td><td><mark style="color:green;"><strong>Complete</strong></mark></td></tr><tr><td><strong>PreProd</strong> Infrastructure (SPOs, Exchanges, wallets, dApps, etc) upgrade to 9.1.0 and test.</td><td>Community</td><td><mark style="color:green;"><strong>Complete</strong></mark></td></tr><tr><td><strong>Mainnet</strong> Infrastructure (SPOs, Exchanges, wallets, dApps, etc) upgrade to 9.1.0.</td><td>Community</td><td><mark style="color:green;"><strong>Complete</strong></mark></td></tr><tr><td><strong>PreProd</strong> critical mass indicators met to enable hardfork.</td><td>Community</td><td><mark style="color:green;"><strong>Complete</strong></mark></td></tr><tr><td><strong>Mainnet</strong> critical mass indicators met (70% SPOs and 80% Exchange liquidity upgraded and ready with 9.1.0).</td><td>Community</td><td><mark style="color:green;"><strong>Complete</strong></mark></td></tr><tr><td><strong>PreProd h</strong>ardforked with Node 9.1.0</td><td>Community</td><td><mark style="color:green;"><strong>Complete</strong></mark></td></tr><tr><td><strong>Mainnet h</strong>ardforked with Node 9.1.0</td><td>Community</td><td><mark style="color:green;"><strong>Complete</strong></mark></td></tr></tbody></table>

***

## Chang #1 Dependencies

&#x20;These are the dependencies, as agreed by the hard fork working group, which need to be completed or at a suitable point prior to initiating the hard for combinator event for the [Chang upgrades](https://docs.intersectmbo.org/cardano/cardano-upgrades/hard-forks/chang-upgrade).&#x20;

<table><thead><tr><th>Item</th><th width="154">Owner</th><th width="256">Acceptance Criteria</th><th>Status</th></tr></thead><tbody><tr><td>Node 9.1.0 genesis file preparations</td><td>Parameters Committee, ICC</td><td>ICC members have created all cold credentials, Parameters committee ratifies the parameter settings (<a href="/broken/pages/GjGchmwyEb5jsOwDj9iq#supporting-governance-initiatives-readiness">more details</a>)</td><td><mark style="color:green;"><strong>Complete</strong></mark></td></tr><tr><td>DQuadrant Chang Testing </td><td>DQuadrant</td><td>Completion of testing for all new components, no major issues outstanding </td><td><mark style="color:green;"><strong>Complete</strong></mark></td></tr><tr><td>Tweag Guardrails Script Audit</td><td>Tweag</td><td>Completion of script audit, no major issues outstanding</td><td><mark style="color:green;"><strong>Complete</strong></mark></td></tr><tr><td>Tweag Constitutional Committee Identity Script Audit</td><td>Tweag</td><td>Completion of script audit, no major issues outstanding</td><td><mark style="color:green;"><strong>Complete</strong></mark></td></tr><tr><td>Core Governance Tooling (GovTool, CC Portal, etc.)</td><td>In yon Networks, Bloxico, DQuadrant</td><td>Governance tools finished development, testing and deployed across environments (<a href="/broken/pages/GjGchmwyEb5jsOwDj9iq#supporting-governance-initiatives-readiness">more details</a>)</td><td><mark style="color:green;"><strong>Complete</strong></mark></td></tr><tr><td>Major Hardware Wallet Updates (Ledger and Trezor)</td><td>Vacuum Labs</td><td>Conway era development completed, tested, audited and included in official release (<a href="/broken/pages/GjGchmwyEb5jsOwDj9iq#wallets-readiness">more details</a>)</td><td><mark style="color:green;"><strong>Complete</strong></mark></td></tr></tbody></table>

***

## Key Context

### Node `9.0.0` vs Node `9.1.0`

* Node `9.0.0` contains all the new Conway functionality and is fully capable of full governance.
* Node `9.0.0` will not be the final node version for Preview, PreProd or Mainnet, as it will not have the correct configuration files, known as genesis files.
  * The genesis files specify things like protocol parameters and importantly the credentials for the interim constitutional committee.
* Splitting Node `9.0.0` and Node `9.1.0` allows users to test all the new Node code across networks before having the final genesis files prepared.

### Cardano Environments

**Preview**: Acts as a preview for newer Node versions, can be unstable.

**Pre-Production**: Environment that matches mainnet configuration, long-term and stable environment for final-stage integration/upgrade testing.&#x20;

**SanchoNet:** An unstable temporary network for governance testing.

**Mainnet**: Our production environment – the actual network the Cardano community uses every day.

### Bootstrapping vs Full Governance testing

* The plan is to maintain SanchoNet in full governance mode.
* While hardforking Preview Network into [bootstrapping phase](https://github.com/cardano-foundation/CIPs/blob/master/CIP-1694/README.md#bootstrapping-phase) and keeping it there for the foreseeable
* To give everyone a way to test full governance on Sancho whilst testing bootstrapping on Preview.

***

More information on the [Major Release Process](https://docs.intersectmbo.org/cardano/cardano-upgrades/major-release-process) is also available. A [frequently asked questions](https://docs.intersectmbo.org/cardano/cardano-upgrades/hard-forks/hard-fork-frequently-asked-questions) page and [Ecosystem readiness](https://docs.intersectmbo.org/cardano/cardano-upgrades/hard-forks/chang-timeline-and-dependencies/chang-upgrade-1-readiness) page related to the Chang hard fork is also being updated on the knowledge base regularly.&#x20;
