# 9th June 2026

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/van-rossem-upgrade/hard-fork-working-group-meeting-minutes/4th-june-2026#action-items-and-next-steps) - Bosko
2. [Node 11.0.1](https://github.com/IntersectMBO/cardano-node/releases/tag/11.0.1) & [DBSync 13.7.1.0](https://github.com/IntersectMBO/cardano-db-sync/releases/tag/13.7.1.0) - Sam
3. [Van Rossem Upgrade Update](https://docs.google.com/presentation/d/1pEFh_GC3Nx2nTVPXj9bke9R7C9Bkr8Hk/edit?slide=id.p1\&pli=1#slide=id.p1) - Bosko, all
   1. Ogmios [v6.14.0.2](https://github.com/IntersectMBO/ogmios/releases/tag/v6.14.0.2) - Jeff, Sam
   2. Kupo [v2.11.0.1](https://github.com/IntersectMBO/kupo/releases/tag/v2.11.0.1) - Jeff, Sam
   3. [PoolTool](https://pooltool.io/networkhealth)
      1. Nodes reporting 11.0.1 - 50% <mark style="color:green;">**↑ (+1)**</mark>
      2. Blocks Protocol Version current epoch - 76% <mark style="color:green;">**↑ (+8)**</mark>
   4. [Cexplorer HF readiness](https://cexplorer.io/hardfork?block=5_days)
      1. Block production v11 last 5 days - 84.03% <mark style="color:green;">**↑ (+2)**</mark>
   5. [Readiness tracker](https://docs.google.com/spreadsheets/d/1ECoYFCtrRtFX3BvqfhaZi6FxlXQMoTGP/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true)
4. van Rossem hard fork progress - Bosko
   1. PreProd
      1. Ratified on **5th June**, will be enacted on **10th June**
   2. Mainnet
      1. Go/No-go Mainnet hard fork initiation governance action submission date - **15th June**
      2. Guardrails status
         1. Asked Civics Committee on [Discord](https://discord.com/channels/1136727663583698984/1295329867285663826/1513851728703918113)
      3. Readiness checklist
5. Plutus Cost Model - Kevin, Ryan, Bosko
   1. Mainnet - submitted on 26th May, continuing to gain traction (currently at 47% with 19 days to go)
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
  * Ogmios and Kupo have two paths forward (both providing sufficient support to the community to progress with van Rossem hard fork readiness
    * Tools author is expected to review, adjust and make van Rossem compatible versions based on the original codebase in the week of 22nd June
    * Until that happens, forked versions of those tools (Ogmios [v6.14.0.2](https://github.com/IntersectMBO/ogmios/releases/tag/v6.14.0.2) and Kupo [v2.11.0.1](https://github.com/IntersectMBO/kupo/releases/tag/v2.11.0.1)) can be used to test for van Rossem compatibility&#x20;
  * Adoption of Node 11.0.1 and DBSync 13.7.1.0 continues to increasy steadily
    * According to [PoolTool](https://pooltool.io/networkhealth), nodes self reporting v11 are at 52% and blocks protocol version 11 in the current epoch is at 76%
    * According to [Cexplorer](https://cexplorer.io/hardfork?block=5_days), block production v11 in the last 5 days is at more than 84%
  * [Readiness tracker](https://docs.google.com/spreadsheets/d/1ECoYFCtrRtFX3BvqfhaZi6FxlXQMoTGP/edit?gid=960883614#gid=960883614) has been updated in several aspects:
    * There is now the Mainnet submission readiness checklist in the summary tab and its readiness numbers are based on items considered to be on the critical path
    * Few light wallets and few tools have become ready
    * Exchanges readiness is progressing fast
      * Point made by Kartik from CF will be actioned upon as it suggest better math being applied to calculate exchanges readiness based on each exchange liquidity percentage
    * Dapps continued and focused on adjustments and testing aginst Preview ahead of the PreProd fork where they will continue their testing efforts
      * Dapps critical path readiness assessment is based on the top entries by transaction count over the last 30 days as shown on [Transaction Leaderboard](https://cardano.org/apps/leaderboard/)
  * PreProd was ratified on **5th June**, will be enacted on **10th June**
  * van Rossem mainnet hard fork initiation governance actions metadata will be assessed by Technical Steering Committee and Civics Committee especially on affirmation that no guardrails changes have been observed nor expected
    * It is to be done ahead of the mainnet hf governance action submission go/no-go decision scheduled for Monday, 15th June
  * Plutus Cost Model parameter update governance action has been submitted on mainnet on 26th of May and its at \~48% approval with the reasonable expectation that it will end up being ratified and subsequently enacted in the next \~3 weeks
  * Comms team meetings are happening weekly and async communication continuously. The team that includes representatives from five big Cardano entities, is having a strong grip on a timely, precise, transparent and consistent messaging being made public
  * Risk log has been slightly adjusted and few risks having their likelihood reduced with further assessment and adjustments expected during the second hard fork working group meeting this week, on Thursday, 11th June
  * Tech support team updated the hard fork working group on the status and set the expectations to have process and resources tracker drafted this week so it can be aligned on ahead of the expected mainnet hf governance action submission
* Hard Fork Working Group communication channels
  * [Discord](https://discord.com/channels/1136727663583698984/1242097284619960411) — `#wg-hard-fork`
  * [Weekly bulletins](https://x.com/IntersectMBO)
  * [Luma calendar](https://luma.com/calendar/cal-TMjYNpSY4huYYif)
* [van Rossem Upgrade Update](https://docs.google.com/presentation/d/1pEFh_GC3Nx2nTVPXj9bke9R7C9Bkr8Hk/edit?slide=id.p1\&pli=1#slide=id.p1)
* [van Rossem readiness tracker](https://docs.google.com/spreadsheets/d/1ECoYFCtrRtFX3BvqfhaZi6FxlXQMoTGP/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true)

#### **Action items and next steps**

* **Jeff/Sam:** Confirm Ogmios/Kupo path ahead, whether it will be using original codebases or forked ones
* **Bosko:** Update hard fork working group on Technical Steering Committee and Civics Committee assessment of the van Rossem hard fork initiation governance action metadata, particularly on the affirmation that there are no observed nor expected guardrails changes
* **Bosko:** Update mainnet submission readiness checklist in readiness tracker so exchanges readiness level represents their liquidity percentages properly
* **Bosko:** Update hard fork working group on technical support documents status (process and resources tracker)

