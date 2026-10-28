# 27th October 2026

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/general/hard-fork-working-group-meeting-minutes/20th-october-2026#action-items-and-next-steps) - Bosko
2. [Dijkstra era hard fork](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era/dijkstra-overview) - Bosko, all
   1. Releases
      1. [11.2](https://github.com/IntersectMBO/cardano-node/issues/6672) - Jeff, Amani, Sam
      2. 11.3 - Sebastian
         1. Includes [CIP-23](https://cips.cardano.org/cip/CIP-23)
      3. [Project view of versions](https://github.com/orgs/input-output-hk/projects/167/views/15)
   2. [Dijkstra risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?gid=66373110#gid=66373110) review
   3. Scope
      1. Each remaining scope item (besides CIP-23 and CIP-50 which are already documented) have its impact documented ([PR](https://github.com/IntersectMBO/hf-wg-documentation/pull/43) opened) in the [Cardano Upgrades space](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) (Core semantics changes, Breaking API changes, New features)
         * [Updated Leios impact assessment available for feedback](https://drive.google.com/file/d/1GJNMixEGb6-jEOh8Yy_p2N--cPPz1Jh6/view?usp=sharing) (passed from TSC to original authors)
   4. Constitutional amendments - [Dijkstra era parameters in CAP](https://cap.intersectmbo.org/#/detail/12)
   5. Comms - Ian, Matthew
   6. Node diversity
      1. Node diversity workshop in London, **12th&13th November** organized by Amaru team
         * London Marriott Hotel Canary Wharf\
           Address: 22 Hertsmere Rd, London E14 4ED, United Kingdom
         * [Working agenda](https://hackmd.io/0b_HvF4AS-q4wayJP6M25A)
      2. Haskell, Amaru (Rust), Dingo (Go), Dugite (Rust), TSUNAGI (Zig), Gerolamo (TypeScript), Dolos (Rust), Turbocardano (C++), Razor (.NET), Scalus (Scala), Yano (Java)
3. Hard Fork Working Group funding (Technical Steering Committee budget)
   1. Application form - [https://forms.clickup.com/9015279944/f/8cnmga8-55475/D8A3VU9CZOQQU56CYX](https://forms.clickup.com/9015279944/f/8cnmga8-55475/D8A3VU9CZOQQU56CYX)
4. AOB

#### Key materials

* Summary
  * **Dijkstra Era hard fork**
    * Releases
      * 11.2
        * Release is imminent and is expected to become available today or tomorrow
        * Once available it will be used to fork DijkstraNet into the Dijkstra era
        * This version includes the full feature set of Dijkstra era hard fork scope except Leios
        * SPOs need to update the node version prior to the hard fork
        * It is expected that some version of 11.2, be it 11.2 or 11.2.1, 11.2.2, etc, become mainnet ready
      * 11.3
        * At least 2 week away
        * Realistically 3-4 weeks for 11.3 version tagged and pre-released
    * Cardano Testnets
      * DijkstraNet
        * Call to action on downstream tooling integration against 11.2 on DijkstraNet (as soon as it becomes available)
        * Plutus v4 cost models and primitives were taken into consideration
          * There are 2 ways to bring them into the Dijkstra era
            * Hardcoding them into the genesis file
            * Protocol Parameter Update governance action that precedes hard fork (preferred way)
              * Should this be the case, governance action that bring new plutus cost models at least would need to be submitted as soon as possible
      * Musashi Dojo
        * Call to action on downstream tooling integration against 11.3 prototype on Musashi Dojo
      * SanchoNet
        * The expectation would be to follow other Cardano testnets and fork in the Dijkstra  as a community owned one
    * Scope
      * Documenting the scope needs the following:
        * Merge [the updated Leios impact assessment](https://drive.google.com/file/d/1GJNMixEGb6-jEOh8Yy_p2N--cPPz1Jh6/view?usp=sharing) to the Cardano Upgrades GitBook [page](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/ouroboros-linear-leios)
        * Merge the remaining impact assessments to the Dijkstra era GitBook space after addressing Kevins review of them
        * Add CIP-23 full implementation to the [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) GitBook page
        * Adjust CIP-23 impact assessment page based on the plan for the full CIP-23 implementation in Dijkstra era
    * Risk
      * [Dijkstra risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?gid=66373110#gid=66373110) now has risk owner assigned to each risk item
      * There should be another column in the risk log representing formal risk assessment for each record in the log ([action item from the last call](https://cardanoupgrades.docs.intersectmbo.org/general/hard-fork-working-group-meeting-minutes/20th-october-2026#action-items-and-next-steps))
      * All risks with the scoring 50 and above were assessed and discussed on the call and where applicable, scoring was adjusted to lower number by successfully applying mitigation strategies
    * Constitutional amendments
      * Following up on the successful [Dijkstra Rollout - Constitutional update and guardrails](https://drive.google.com/file/d/1qcQ_DGtIp0_TTxwDdDCHokAbDMt1Rmqb/view?usp=sharing) call last Friday, Carlos announced the shorter version of the [Dijkstra Era Constitution Changes](https://docs.google.com/presentation/d/1t8ysTu6ruYcFBBGHm50-wwuQ6uxZn8dn/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true) presentation
    * Node diversity
      * Node diversity workshop in London, **12th&13th November** organized by Amaru team
        * London Marriott Hotel Canary Wharf Address: 22 Hertsmere Rd, London E14 4ED, United Kingdom
        * [Working agenda](https://hackmd.io/0b_HvF4AS-q4wayJP6M25A)
    * Hard Fork Working Group funding (Technical Steering Committee budget)
      * [Application form](https://forms.clickup.com/9015279944/f/8cnmga8-55475/D8A3VU9CZOQQU56CYX)
  * Hard Fork Working Group will continue to meet once a week until the Dijkstra era hard fork work solidifies enough to mandate more alignments and sync

#### **Reference links and engagement points**

* Hard Fork Working Group communication channels
  * [Discord](https://discord.com/channels/1136727663583698984/1242097284619960411) — `#wg-hard-fork`
  * [Weekly bulletins](https://x.com/IntersectMBO) (url edited)
  * [Luma calendar](https://luma.com/calendar/cal-TMjYNpSY4huYYif)
  * [Email](mailto:hard-fork@intersectmbo.org)
* [BLS Key rotation](https://github.com/input-output-hk/ouroboros-leios/issues/1024)
* [Dijkstra readiness tracker](https://docs.google.com/spreadsheets/d/1C1Ai_YTqwKLHtICunzbh_o0FD9XB54Kh/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true)
* [Dijkstra Risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?usp=sharing)
* [CAP (Constitutional Ammendment Portal)](https://cap.intersectmbo.org/)
  * [Guides](https://cap.intersectmbo.org/#/guides)
  * [Introduction to CAPs and CISs](https://cap.intersectmbo.org/#/guides/intro-to-caps-and-cis)
* [Antithesis](https://cardanofoundation.org/blog/improving-cardano-antithesis)
* [Recording](https://drive.google.com/file/d/1zsRFIC4DzGOgSA-rywYiQW-yR_DfQO8w/view?usp=drive_link)
* [Transcript](https://docs.google.com/document/d/1lMVy2rAcD5sIo3askQpTQOcitiFDXjOtJHuVQSWn7qw/edit?usp=drive_link)
* [Chat](https://drive.google.com/file/d/1SNkHCVMt5Mis444WsB0aCCkM-FEq_6ym/view?usp=drive_link)

#### **Action items and next steps**

* **Ian/Larisa:** Prepare coordinated comms plan, for downstream tooling integration and ecossytem readiness progress, that will be executed as soon as 11.2 version is released (with the limited integration possible against 11.3 prototype)
* **Carlos:** Provide the shorter version of the [Dijkstra Era Constitution Changes](https://docs.google.com/presentation/d/1t8ysTu6ruYcFBBGHm50-wwuQ6uxZn8dn/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true) presentation
* **Bosko:** Merge [the updated Leios impact assessment](https://drive.google.com/file/d/1GJNMixEGb6-jEOh8Yy_p2N--cPPz1Jh6/view?usp=sharing) to the Cardano Upgrades GitBook [page](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/ouroboros-linear-leios)
* **Bosko:** Merge the remaining impact assessments to the Dijkstra era GitBook space after addressing Kevins review of them
* **Bosko:** Add CIP-23 full implementation to the [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) GitBook page
* **Bosko:** Adjust CIP-23 impact assessment page based on the plan for the full CIP-23 implementation in Dijkstra era
* **Bosko:** Add another column in the [Dijkstra risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?gid=66373110#gid=66373110) representing formal risk assessment for each record in the log
* **Bosko:** Consider adjusting DIjkstra risk log for better visibility and risk management
