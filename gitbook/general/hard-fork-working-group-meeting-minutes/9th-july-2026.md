# 9th July 2026

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/van-rossem-upgrade/hard-fork-working-group-meeting-minutes/7th-july-2026#action-items-and-next-steps) - Bosko
2. Van Rossem Upgrade Update - Bosko, all
   1. [PoolTool](https://pooltool.io/networkhealth) - Blocks Protocol Version 11 current epoch - 92%
   2. [Cexplorer HF readiness](https://cexplorer.io/hardfork?block=5_days) - Block production v11 last 5 days 94.80%
   3. [Cardanoscan Exchanges](https://cardanoscan.io/hfReadiness) - Liquidity Ready 83.27%
   4. [Hard Fork ratification readiness - tracker](https://docs.google.com/spreadsheets/d/1ECoYFCtrRtFX3BvqfhaZi6FxlXQMoTGP/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true)
   5. Ratification&#x20;
      1. 13th July, 18th July
   6. Enactment
      1. 18th July, 23rd July
   7. [Risk log](https://docs.google.com/spreadsheets/d/1DSAiayrPOhhzSKKKljbd2WxHQPFmzKsvoyyA-BJUDg8/edit?gid=1105903724#gid=1105903724)
   8. Hard Fork ratification and enactment effects on other live governance actions
   9. van Rossem comms - Ian / Larisa
   10. Technical support before and after hard fork enactment - Bosko, Can
3. [Dijkstra era hard fork](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era/dijkstra-overview)
4. AOB

#### Key materials

* Summary
  * **van Rossem hard fork**
    * All readiness ratification metrics are met
    * Support is steadily increasing
    * Voting thresholds for DReps and SPOs have been surpassed
    * There are 4 out 5 positive CC votes
    * Possible ratification dates are 13th and 18th July
    * Possible enactment dates are 18th and 23rd July
    * If the hard fork governance action is ratified on the next epoch boundary on 13th, Reimburse Ikigai treasury withdrawal action will be delayed for an epoch, thus effectively expiring
      * The ledger prioritizes hard fork ratification above all other actions and will delay anything that ratifies at the same time
    * On the last epoch boundary:
      * Reduce mincommitteesize governance action was ratified
      * Hydra Treasury Withdrawal governance action was ratified
      * Reimbursing Ikigai Treasury Withdrawal governance action unfortunately didnt reach the ratification threshold
  * **Dijkstra Era hard fork**
    * Hard Fork Working Group discussed several aspects of the next era hard fork having the foundation in scope, timing, prioritization and process
    * Scope
      * There are multiple sources of information circulating that show the list of potential scope candidates
        * CIP shortlist - [https://docs.google.com/document/d/1YN\_Rn3RaY26JHlnhsNU-rQR3tnrihGAp7QHQcBrtEWQ/edit?usp=sharing](https://docs.google.com/document/d/1YN_Rn3RaY26JHlnhsNU-rQR3tnrihGAp7QHQcBrtEWQ/edit?usp=sharing)
        * Kanban board - [https://github.com/orgs/IntersectMBO/projects/57/views/1](https://github.com/orgs/IntersectMBO/projects/57/views/1)
        * [https://github.com/IntersectMBO/cardano-ledger/issues/5604](https://github.com/IntersectMBO/cardano-ledger/issues/5604)
        * CIP 0151 [https://docs.google.com/document/d/19NCm3wC2LQI6g3DcpbBm9g597uZcjZiMvwWziqSy\_04/edit?usp=sharing](https://docs.google.com/document/d/19NCm3wC2LQI6g3DcpbBm9g597uZcjZiMvwWziqSy_04/edit?usp=sharing)
        * CIP 1112 out of treasury proposal
        * CIP-0180? | Block Producer Identification - [https://github.com/cardano-foundation/CIPs/pull/1157](https://github.com/cardano-foundation/CIPs/pull/1157)
        * CPS to describe some of the issues with wallets that are inactive/in cold storage for a long period of time. [https://cips.cardano.org/cps/CPS-0022](https://cips.cardano.org/cps/CPS-0022)
      * Currently, the main feature drivers discussed are Leios, Peras and nested transactions
      * Some scope candidates might be added to intra era hf in Dijkstra
      * Scope freeze needed as soon as possible, within a month
    * Timing
      * Its been emphasized that in order to have next hard fork ready and enacted by the end of 2026, it needs to happen by December 15th, which in turn means hard fork initiation governance action needs to be submitted by November 15th the latest
      * Due to the complexity of the discussed potential scope, it was raised that exchanges would need a good set of instructions and a heads up on the changes before upgrading their infrastructure
      * There is going to be socialization period of 90 days accounted for in the overall timeline due to the guardrails changes
    * Prioritization
      * There were different ideas discussed on the prioritization approach with some of them being:
        * CIP-0179 polling for decision making
        * Ekklessia Hydra based voting
    * Process
      * Landscape will likely be the one to include diverse nodes (Haskell, Amaru - Rust, Dingo - Go)
      * Scope, timing, prioritization are rooted in the process that is yet to be defined but shouldnt be a blocking challenge for the things that are known
    * Hard Fork Working Group meetings will continue to happen twice a week, until at least the Dijkstra hard fork scope is set, after which the future meeting cadence will be decided
* Hard Fork Working Group communication channels
  * [Discord](https://discord.com/channels/1136727663583698984/1242097284619960411) — `#wg-hard-fork`
  * [Weekly bulletins](https://x.com/IntersectMBO)
  * [Luma calendar](https://luma.com/calendar/cal-TMjYNpSY4huYYif)
  * [Email](mailto:hard-fork@intersectmbo.org)
* [van Rossem Upgrade Update](https://docs.google.com/presentation/d/1pEFh_GC3Nx2nTVPXj9bke9R7C9Bkr8Hk/edit?slide=id.p1\&pli=1#slide=id.p1)
* [van Rossem readiness tracker](https://docs.google.com/spreadsheets/d/1ECoYFCtrRtFX3BvqfhaZi6FxlXQMoTGP/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true)

#### **Action items and next steps**

* **van Rossem hard fork**
  * **Can/Bosko:** Make sure on-call duty is properly defined and set for and around the anticipated hard fork ratification and enactment dates
* **Dijkstra Era hard fork**
  * **Sam:** Using [CIP shortlist](https://docs.google.com/document/d/1YN_Rn3RaY26JHlnhsNU-rQR3tnrihGAp7QHQcBrtEWQ/edit?usp=sharing) as the starting reference and a discussion point, create the markdown page under Cardano Product Committee that reflects discussed scope items
  * **Bosko:** Continue creating supporting structure and relevant documentation within the hard fork working group GitBook space under Technical Steering Committee
  * **Bosko:** Refine and update hard fork working group calls invitees list for DIjkstra hf related discussion
  * **Tex:** Create ecosystem dependency mapping document(s)
