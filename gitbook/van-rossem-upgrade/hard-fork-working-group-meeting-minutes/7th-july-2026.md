# 7th July 2026

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/van-rossem-upgrade/hard-fork-working-group-meeting-minutes/2nd-july-2026#action-items-and-next-steps) - Bosko
2. [Node 11.0.1](https://github.com/IntersectMBO/cardano-node/releases/tag/11.0.1) & [DBSync 13.7.1.0](https://github.com/IntersectMBO/cardano-db-sync/releases/tag/13.7.1.0) - Sam
   1. [Cardano Solutions/Ogmios](https://github.com/CardanoSolutions/ogmios/releases/tag/v7.0.0) - <mark style="color:green;">**Ready**</mark>
   2. [Kupo](https://github.com/IntersectMBO/kupo/) (Intersect forked version)&#x20;
3. Van Rossem Upgrade Update - Bosko, all
   1. [PoolTool](https://pooltool.io/networkhealth) - Blocks Protocol Version current epoch - 91%
   2. [Cexplorer HF readiness](https://cexplorer.io/hardfork?block=5_days) - Block production v11 last 5 days \~95%
   3. [Cardanoscan Exchanges](https://cardanoscan.io/hfReadiness) - Liquidity Ready 80.19%
   4. [Hard Fork ratification readiness - tracker](https://docs.google.com/spreadsheets/d/1ECoYFCtrRtFX3BvqfhaZi6FxlXQMoTGP/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true)
   5. Possible Ratification Dates
      1. ~~June 28th~~, ~~July 3rd~~, July 8th, July 13th, July 18th
   6. Possible Enactment Dates
      1. ~~July 3rd~~, ~~July 8th~~, July 13th, July 18th, July 23rd
4. Hard Fork ratification and enactment effects on other live governance actions
5. van Rossem comms - Ian / Larisa
   1. Comms in the last week - anything we missed
   2. Comms in the week ahead
6. [Risk log](https://docs.google.com/spreadsheets/d/1DSAiayrPOhhzSKKKljbd2WxHQPFmzKsvoyyA-BJUDg8/edit?gid=1105903724#gid=1105903724) - Bosko
7. Technical support before and after hard fork enactment - Bosko, Can
8. Dijkstra era hard fork
9. AOB

#### Key materials

* Summary
  * There is a steady progress of votes towards the thresholds needed for the hard fork initiation governance action to be ratified
    * DReps support currently sits at \~75% (threshold at 60%)
    * SPOs at almost 51% (which is the threshold)
    * CC votes at 3 out of 5 needed for a threshold
  * It was pointed out that, due to the governance-action priority rules, hard fork governance action can delay treasury withdrawals, protocol parameter changes and info actions
    * Delaying info actions has no real significant impact
    * Delaying treasury actions or protocol parameter changes can be affected significantly
      * If the delayed action is about to reach expiration and get ratified/delayed this way on its last epoch before expiration, it will expire and be removed from the ledger governance state as if it was expired when reaching 'govActionLifetime'
  * The issue described above require community coordination and will be included in the adjusted comms
* Hard Fork Working Group communication channels
  * [Discord](https://discord.com/channels/1136727663583698984/1242097284619960411) — `#wg-hard-fork`
  * [Weekly bulletins](https://x.com/IntersectMBO)
  * [Luma calendar](https://luma.com/calendar/cal-TMjYNpSY4huYYif)
  * [Email](mailto:hard-fork@intersectmbo.org)
* [van Rossem Upgrade Update](https://docs.google.com/presentation/d/1pEFh_GC3Nx2nTVPXj9bke9R7C9Bkr8Hk/edit?slide=id.p1\&pli=1#slide=id.p1)
* [van Rossem readiness tracker](https://docs.google.com/spreadsheets/d/1ECoYFCtrRtFX3BvqfhaZi6FxlXQMoTGP/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true)

#### **Action items and next steps**

* **Mike:** Confirm governance action ratification logic and precedence hard fork has over other types of governance actions and the impact it is going to make
* **Ian/Larisa:** Adjust the comms so it reflects challenges and impact on other governance actions around hard fork ratification

