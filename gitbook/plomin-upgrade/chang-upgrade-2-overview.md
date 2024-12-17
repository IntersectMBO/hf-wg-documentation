# Plomin upgrade overview

{% hint style="info" %}
**We're open! Join the next working group meeting**

Commencing from October 28th onwards we'll be meeting twice a week and you can find the details below:

* Twice weekly: Tuesdays and Thursdays: https://lu.ma/calendar/cal-mUnW4X66H0JRPQh (please RSVP from here)
* Time: 4:00 PM UTC
* Location: Virtual meeting (invitations will be sent via email)
* Recordings of most sessions will be available on Intersect YouTube the day after each meeting
* [https://www.youtube.com/@Intersectmbo](https://www.youtube.com/@Intersectmbo)

\
**Other ways to learn more and participate**\
Throughout November and December we'll be hosting X Spaces and other Q\&A sessions via Discord. \
For further details or inquiries, please do not hesitate to reach out to us at hard-fork@intersectmbo.org.&#x20;
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

Indicatively this is illustrated below;

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>Illustrative governance action timeline</p></figcaption></figure>

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
