# 4th June 2026

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/van-rossem-upgrade/hard-fork-working-group-meeting-minutes/2nd-june-2026#action-items-and-next-steps) - Bosko
2. [Node 11.0.1](https://github.com/IntersectMBO/cardano-node/releases/tag/11.0.1) & [DBSync 13.7.1.0](https://github.com/IntersectMBO/cardano-db-sync/releases/tag/13.7.1.0) - Sam
3. [Van Rossem Upgrade Update](https://docs.google.com/presentation/d/1pEFh_GC3Nx2nTVPXj9bke9R7C9Bkr8Hk/edit?slide=id.p1\&pli=1#slide=id.p1) - Bosko, all
   1. Ogmios [v6.14.0.2](https://github.com/IntersectMBO/ogmios/releases/tag/v6.14.0.2) has been released
      1. Issue found by community member on [v6.14.0.1](https://github.com/IntersectMBO/ogmios/releases/tag/v6.14.0.1), fix [PR](https://github.com/IntersectMBO/ogmios/pull/5) raised by Jordan from IO in Intersect forked Ogmios repo
      2. Can it be reviewed and merged back into the original codebase by the time of the mainnet hf action submission?
   2. Kupo [v2.11.0.1](https://github.com/IntersectMBO/kupo/releases/tag/v2.11.0.1) is released
      1. Can it be reviewed and merged back into the original codebase by the time of the mainnet hf action submission?
   3. [PoolTool](https://pooltool.io/networkhealth)
      1. Nodes reporting 11.0.1 - 49% <mark style="color:green;">**↑**</mark>
      2. Blocks Protocol Version current epoch - 68% <mark style="color:green;">**↑**</mark>
   4. [Cardanoscan HF readiness](https://cardanoscan.io/hfReadiness)
      1. Stake Pools ready - 21.99% <mark style="color:green;">**↑**</mark>
      2. Stake ready - 39.39% <mark style="color:green;">**↑**</mark>
      3. Exchange readiness - Ready (2%); In Progress (28%); Not started (71%)
   5. [Cexplorer HF readiness](https://cexplorer.io/hardfork?block=5_days)
      1. Block production v11 - 81.47%
      2. Exchange readiness by liquidity - Ready (0.91%); In Progress (53.42%); Not started (45.67%)
   6. [Readiness tracker](https://docs.google.com/spreadsheets/d/1ECoYFCtrRtFX3BvqfhaZi6FxlXQMoTGP/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true)
4. van Rossem hard fork progress - Bosko
   1. PreProd
      1. [Cardanoscan](https://preprod.cardanoscan.io/govAction/gov_action108a5htqnmlp89ffn2ucf7u9u33s0r9gpx7eytpdc2q28y50ly42qqf9jcen)
      2. [AdaStat](https://preprod.adastat.net/governances/79fb4bac13dfc272a53357309f70bc8c60f1950137b24585b850147251ff255400)
      3. Wasnt ratified on **31st May**, next opportunity is **5th June** and if successful, it would be enacted on **10th June**
      4. Summary of what happened, why it wasnt ratified on the epoch boundary on **31st May** and why we are confident it is likely to be ratified on the next epoch boundary on **5th June** (tomorrow)
   2. Mainnet
      1. Go/No-go Mainnet hard fork initiation governance action submission date - **15th June**
5. Plutus Cost Model - Kevin, Ryan, Bosko
   1. Mainnet - submitted on 26th May, continuing to gain traction
6. van Rossem comms - Ian / Larisa
   1. Comms plan - CF, Midnight, Shielded, Emurgo, Intersect, IO
      1. Weekly comms meeting
   2. Comms in the last week - anything we missed
   3. Comms in the week ahead
7. [Risk log](https://docs.google.com/spreadsheets/d/1DSAiayrPOhhzSKKKljbd2WxHQPFmzKsvoyyA-BJUDg8/edit?gid=1105903724#gid=1105903724)
8. Technical support before and after hard fork enactment
9. AOB

#### Key materials

* Summary
  * Latest version of DBSync is [13.7.1.0](https://github.com/IntersectMBO/cardano-db-sync/releases/tag/13.7.1.0) and its recommended to upgrade to that version
    * If you are running DBSync version 13.7.0.5, it is also van Rossem compatible, and it just needs migration script executed as described in the release notes
  * Ogmios [v6.14.0.2](https://github.com/IntersectMBO/ogmios/releases/tag/v6.14.0.2) and Kupo [v2.11.0.1](https://github.com/IntersectMBO/kupo/releases/tag/v2.11.0.1) have been released in Intersect forked repos
    * Both will be added to the checklist that would hrd fork working group make the right decision on submission of the hard fork initiation governance action on mainnet
  * PreProd hard fork initiation governance action is expected to be ratified on **5th June** (the numbers are far above the needed threshold, highly unlikely that the support would drop), and subsequently it would be enacted on **10th June**
    * The cause of hard fork action not being ratified on the previous epoch boundary
      * 25M delegation that became active on 291->292 epoch boundary, and thats what pushed it from 52.1% to 50.68% and this is why it failed
      * that late delegation exposed the discrepancies in calculations
        * Tools are wrong on excluding auto abstain for SPOs for hard fork initiation governance actions
        * Tools are likely not wrong on excluding auto abstain for any other type of gov actions like protocol parameter update
        * What could change it would be:
          * explicit votes
            * yes and abstain -> pushing the percentage higher
            * no -> pushing percentage lower
            * late delegation -> pushing percentage lower
    * Comms team is in the loop of all the important changes and will communicate accordingly
  * Go/no-go decision call for mainnet hard fork initiation governance action submission which was originally planned still holds for **15th June**
    * It will have a checklist, criteria that would help make confident decision
    * Dapps should be invited to report based on the readiness checklist
    * If there is a positive, go decision, it is expected the the action would be submitted on mainnet on **15th or 16th June**
      * Since mainnet epoch boundary is on 18th June, it would take up to 6 epochs for voting and 1 more epoch for enactment (5 weeks)
  * Plutus cost model parameter update governance action on mainnet is continuing to have traction
  * Risk log is adjusted to reflect latest updates (few of them have their likelihood and impact reduced)
* Hard Fork Working Group communication channels
  * [Discord](https://discord.com/channels/1136727663583698984/1242097284619960411) — `#wg-hard-fork`
  * [Weekly bulletins](https://x.com/IntersectMBO)
  * [Luma calendar](https://luma.com/calendar/cal-TMjYNpSY4huYYif)
* [van Rossem Upgrade Update](https://docs.google.com/presentation/d/1pEFh_GC3Nx2nTVPXj9bke9R7C9Bkr8Hk/edit?slide=id.p1\&pli=1#slide=id.p1)
* [van Rossem readiness tracker](https://docs.google.com/spreadsheets/d/1ECoYFCtrRtFX3BvqfhaZi6FxlXQMoTGP/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true)

#### **Action items and next steps**

* **Jeff:** Reach out to Ogmios and Kupo author and assess whether he can review the changes introduced in forked Ogmios and Kupo repos and merge them back in the original code base before hf governance action is potentially submitted on mainnet on 15th June
* **Leonard:** Invite dapps to test against PreProd once it forks
* **Bosko:** Re-schedule the hard fork tech support call for the decision on submission
* **Leonard/Bosko:** Sync and asses guardrails status for hard fork initiation governance action
* **Bosko:** [The readiness tracker](https://docs.google.com/spreadsheets/d/1ECoYFCtrRtFX3BvqfhaZi6FxlXQMoTGP/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true) should be updated with the certain thresholds for nodes running latest stable version 11.0.1 (50%), top 20 dapps, top 20 exchanges by liquidity, etc. That would also bring additional confidence layer for a decision to submit hard fork initiation governance action on mainnet

