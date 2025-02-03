# Plomin upgrade overview

{% hint style="info" %}
On January 29, 2025, Cardano achieved the transition to full community governance with the **enactment** of the Plomin hard fork

The upgrade was enacted on-chain after the hard fork was approved by stake pool operators (SPOs) and the interim constitutional committee. This is a truly momentous achievement, not only for Cardano but for the entire blockchain industry.

This is Cardano’s first community-enacted upgrade, with all future protocol changes now fully in the hands of the community. The decision began with [CIP-1694](https://cips.cardano.org/cip/CIP-1694?utm_source=hs_email\&utm_medium=email&_hsenc=p2ANqtz-8zxUPhuLU_W5AUDlSnTVgjAw861oVYXodULuqZU7-nxWnctc_QRuDHabDYutuIgMzDzBIO), which was developed over two years and included community workshops. It is the only hard fork to make such an epochal change to blockchain governance
{% endhint %}

Intersect plays the role of coordinator, as a functional servant-leader on behalf of the community and delivery teams working on hard fork activity. The functional teams within Intersect will work with the various committees, working groups, and delivery teams, relaying information here on the knowledge base. Ultimately the date for the hard fork is directly influenced by the community, the relevant constitutional approval and required on-chain voting.

***

## Chang and Plomin Upgrade Release

The Chang and Plomin upgrades will stagger the release of governance functionality, easing adoption and onboarding for those with new or additional roles in governance.

* Chang Upgrade will deploy governance features to Cardano and enter the technical bootstrapping phase as described in CIP-1694 Bootstrapping Phase. Chang upgrade #1 was successfully completed on September 1st 2024.
* The Plomin upgrade moves CIP-1694 out of technical bootstrapping phase and unlocks the final features of on-chain governance including DRep participation and all governance actions. In November 2024, following the sudden passing of Matthew Plomin, the hard fork working group recommended to rename the second upgrade after him. This has been widely affirmed by the community in the following [governance info action](https://gov.tools/governance_actions/fff0df644d328a5367212f45bab59060bde3c4091dc96c723062896fd6197314#0).&#x20;

Further information on [CIP-1694](https://www.1694.io/en) and the interim bootstrapping period is available.

***

## Governance Phase

Following the Chang upgrade the Cardano blockchain has entered into a bootstrapping phase of governance. Special provisions will apply in this initial bootstrap phase. Firstly, during the bootstrap phase, a vote from the constitutional committee is sufficient to change the protocol parameters. Secondly, during the bootstrap phase, a vote from the constitutional committee, together with a sufficient SPO vote, is sufficient to initiate a hard fork - in this case the Plomin upgrade.

This is different to all previous hard forks or upgrades, where founding entities ultimately made the final decisions.&#x20;

***

## Governance Actions

The Plomin upgrade (formally Chang Upgrade #2) requires five (5) governance actions to be successfully enacted on chain. In this bootstrap phase of governance the ICC and SPOs will be required to vote on these accordingly.&#x20;

Intersect will raise the required governance actions, as per the recommendations provided by parameters sub-committee for Plutus parameter updates and civics committee for Plomin upgrade, ultimately moving Cardano out of bootstrap into full governance as defined by CIP-1694.

Plutus Parameter Updates:

* &#x20;The Governance Action for Mainnet parameter changes could earliest occur from epoch 517
* &#x20;The Governance Action for Pre-Production parameter changes could earliest occur from epoch 173

Plomin Upgrade:

* &#x20;The governance action for Mainnet hard fork could earliest occur from epoch 520
* &#x20;Governance action for Prep-production could earliest occur from epoch 177
* &#x20;Governance action for preview could earliest occur from epoch 736

The governance actions should follow environment order, preview before pre-production and pre-production before Mainnet. Governance actions could overlap and be raised in parallel, this is to ensure smooth transition between upgrades in environments, particularly between pre-production and Mainnet.

Indicatively the sequence of events for the hard fork is shown below

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption><p>Indicative sequence of events for Plomin Hard Fork </p></figcaption></figure>

{% hint style="info" %}
Please note, some simplifications have been made to this illustration for brevity and simplicity
{% endhint %}

Illustration steps:

1. Hard fork preview&#x20;
2. Plutus update pre-production
3. Hard fork pre-production
4. Plutus update mainnet
5. Hard fork mainnet &#x20;

{% hint style="info" %}
Governance actions can be seen via [GovTool](https://gov.tools/governance_actions) or on tools such as [CardanoScan ](https://cardanoscan.io/govActions)
{% endhint %}

Should the governance actions not occur at the earliest anticipated epoch they roll into the next. The governance actions will remain for 6 epochs before expiry, after this time they will need to be re-submitted.

## Delegating&#x20;

A key part of the governance model is delegating. Delegating is the act of 'loaning' your Voting Power - which equals ADA the balance in your wallet - to someone else. The person or organisation that you delegate to are called DReps, which is short for "Delegate Representatives". DReps represent you in a similar way as a parliamentary or congressional representative does in an analog government. Simply put, they vote on your behalf.

It is recommended you participate and delegate to a DRep ahead of the Plomin upgrade mainnet hard fork.

You can find more details on CIP-1694 governance and DReps here [https://www.1694.io/en/dreps](https://www.1694.io/en/dreps), and guides on 'how to' here [https://docs.sanchogov.tools/how-to-use-the-govtool/using-govtool](https://docs.sanchogov.tools/how-to-use-the-govtool/using-govtool).&#x20;
