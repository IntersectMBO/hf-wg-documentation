# 2nd June 2026

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/van-rossem-upgrade/hard-fork-working-group-meeting-minutes/28th-may-2026#action-items-and-next-steps) - Bosko
2. [Node 11.0.1](https://github.com/IntersectMBO/cardano-node/releases/tag/11.0.1) & [DBSync 13.7.1.0](https://github.com/IntersectMBO/cardano-db-sync/releases/tag/13.7.1.0) - Sam/Ramsay/Jeff
3. [Van Rossem Upgrade Update](https://docs.google.com/presentation/d/1pEFh_GC3Nx2nTVPXj9bke9R7C9Bkr8Hk/edit?slide=id.p1\&pli=1#slide=id.p1) - Bosko, all
   1. Ogmios [v6.14.0.1](https://github.com/IntersectMBO/ogmios/releases/tag/v6.14.0.1) has been released
   2. Kupo [v2.11.0.1](https://github.com/IntersectMBO/kupo/releases/tag/v2.11.0.1) is released
   3. [PoolTool](https://pooltool.io/networkhealth)
      1. Nodes reporting 11.0.1 - 45%
      2. Blocks Protocol Version current epoch - 66%
   4. [Cardanoscan HF readiness](https://cardanoscan.io/hfReadiness)
      1. Stake Pools ready - 21.34%
      2. Stake ready - 39.10%
      3. Exchange readiness - Ready (0%); In Progress (9%); Not started (91%)
   5. [Readiness tracker](https://docs.google.com/spreadsheets/d/1ECoYFCtrRtFX3BvqfhaZi6FxlXQMoTGP/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true)
4. van Rossem hard fork progress - Bosko
   1. PreProd
      1. [Cardanoscan](https://preprod.cardanoscan.io/govAction/gov_action108a5htqnmlp89ffn2ucf7u9u33s0r9gpx7eytpdc2q28y50ly42qqf9jcen)
      2. [Cexplorer](https://preprod.cexplorer.io/gov/action/79fb4bac13dfc272a53357309f70bc8c60f1950137b24585b850147251ff2554%230)
      3. Wasnt ratified on **31st May**, next opportunity is **5th June** and if successful, it would be enacted on **10th June**. We need to aim for 65% to be in a "safer" zone
   2. Mainnet
      1. Mainnet hard fork initiation governance action submission date - 8th June, 13th June
5. Plutus Cost Model - Kevin, Ryan, Bosko
   1. Mainnet - submitted on 26th May, **more than 20%** of yes stake
6. van Rossem comms - Ian / Larisa
   1. Comms plan - CF, Midnight, Shielded, Emurgo, Intersect, IO
      1. Weekly comms meeting
   2. Comms in the last week - anything we missed
   3. Comms in the week ahead
7. [Risk log](https://docs.google.com/spreadsheets/d/1DSAiayrPOhhzSKKKljbd2WxHQPFmzKsvoyyA-BJUDg8/edit?gid=1105903724#gid=1105903724)
8. AOB

#### Key materials

* Summary
  * Latest version of DBSync is [13.7.1.0](https://github.com/IntersectMBO/cardano-db-sync/releases/tag/13.7.1.0) and its recommended to upgrade to that version
    * If you are running DBSync version 13.7.0.5, it is also van Rossem compatible, and it just needs migration script executed as described in the release notes
  * Ogmios [v6.14.0.1](https://github.com/IntersectMBO/ogmios/releases/tag/v6.14.0.1) and Kupo [v2.11.0.1](https://github.com/IntersectMBO/kupo/releases/tag/v2.11.0.1) have been released in Intersect forked repos
    * It is yet to be confirmed when the Ogmios and Kupo author can review changes introduced in the forked repos and merge them in the original codebase. Ideally it would happen in time before mainnet hf governance action submission
  * PreProd hard fork initiation governance action wasnt ratified on **31st May**, next opportunity is **5th June** and if successful, it would be enacted on **10th June**
    * The cause of hard fork action not being ratified is yet to be proven
    * Current numbers shown by PreProd Adastat and PreProd Cardanoscan are \~60% and \~58% respectively
    * After achieving enough certainty that the hard fork action is expected to be enacted on PreProd there should be comms piece going out emphasizing that yet another milestone has been achieved towards the van Rossem hf on mainnet goal and calling out dapps and other stakeholders to continue adoption and testing against preprod signalling at go/no-go call schedule
  * Go/no-go decision call for mainnet hard fork initiation governance action submission which was originally planned for **8th June**, has been postponed to **15th June**
    * It needs to have a checklist, criteria that would help make confident decision
    * Dapps should be invited to report based on the readiness checklist
    * If there is a positive, go decision, it is expected the the action would be submitted on mainnet on **15th or 16th June**
      * Since mainnet epoch boundary is on 18th June, it would take up to 6 epochs for voting and 1 more epoch for enactment (5 weeks)
  * Plutus cost model parameter update governance action on mainnet is continuing to have traction
  * Sam Leathers presented ChaP release tracker that should become documented in Intersect docs as soon as its ready
* Hard Fork Working Group communication channels
  * [Discord](https://discord.com/channels/1136727663583698984/1242097284619960411) — `#wg-hard-fork`
  * [Weekly bulletins](https://x.com/IntersectMBO)
  * [Luma calendar](https://luma.com/calendar/cal-TMjYNpSY4huYYif)
* [van Rossem Upgrade Update](https://docs.google.com/presentation/d/1pEFh_GC3Nx2nTVPXj9bke9R7C9Bkr8Hk/edit?slide=id.p1\&pli=1#slide=id.p1)
* [van Rossem readiness tracker](https://docs.google.com/spreadsheets/d/1ECoYFCtrRtFX3BvqfhaZi6FxlXQMoTGP/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true)

#### **Action items and next steps**

* **Bosko:** Work with IO engineers and IO exec support to confirm the cause of PreProd not forking
* **Jeff:** Reach out to Ogmios and Kupo author and assess whether he can review the changes introduced in forked Ogmios and Kupo repos and merge them back in the original code base before hf governance action is potentially submitted on mainnet on 15th June
* **Leonard:** Invite dapps to test against PreProd once it forks
* **Ian:** After achieving enough certainty that the hard fork action is expected to be enacted on PreProd there should be comms piece going out emphasizing that yet another milestone has been achieved towards the van Rossem hf on mainnet goal and calling out dapps and other stakeholders to continue adoption and testing against preprod signalling at go/no-go call schedule
* **Bosko:** Re-schedule the Go/No go call for the decision on submission of van Rossem hard fork initiation governance action on mainnet for 15th June
* **Bosko:** [The readiness tracker](https://docs.google.com/spreadsheets/d/1ECoYFCtrRtFX3BvqfhaZi6FxlXQMoTGP/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true) should be updated with the certain thresholds for nodes running latest stable version 11.0.1 (50%), top 20 dapps, top 20 exchanges by liquidity, etc. That would also bring additional confidence layer for a decision to submit hard fork initiation governance action on mainnet

