# 3rd November 2026

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/general/hard-fork-working-group-meeting-minutes/27th-october-2026#action-items-and-next-steps) - Bosko
2. [Dijkstra era hard fork](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era/dijkstra-overview) - Bosko, all
   1. Releases
      1. [11.2](https://github.com/IntersectMBO/cardano-node/issues/6672) - Jeff, Amani, Sam
      2. 11.3 - Sebastian
         * Includes [CIP-23](https://cips.cardano.org/cip/CIP-23)
      3. [Project view of versions](https://github.com/orgs/input-output-hk/projects/167/views/15)
   2. [Dijkstra risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?gid=66373110#gid=66373110) review
   3. Scope
      1. Each remaining scope item (besides CIP-23 and CIP-50 which are already documented) have its impact documented ([PR](https://github.com/IntersectMBO/hf-wg-documentation/pull/43) opened) in the [Cardano Upgrades space](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) (Core semantics changes, Breaking API changes, New features)
         * [Updated Leios impact assessment available for feedback](https://drive.google.com/file/d/1GJNMixEGb6-jEOh8Yy_p2N--cPPz1Jh6/view?usp=sharing) (passed from TSC to original authors)
   4. Constitutional amendments - [Dijkstra era parameters in CAP](https://cap.intersectmbo.org/#/detail/12)
   5. Comms - Larisa, Ian, Matthew
   6. Node diversity
      1. Node diversity workshop in London next week, **12th&13th November** organized by Amaru team
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
      * [11.2](https://github.com/IntersectMBO/cardano-node/releases/tag/11.2.0)
        * Pre-released on 28th October 2026
        * Used to fork DijkstraNet into the Dijkstra era with enactment on 2nd Noevmber 2026
        * This version includes the full feature set of Dijkstra era hard fork scope except Leios and Fair min fees (CIP-23) implementation
        * There is a memory usage regression observed
          * Problems are identified including problem observed on 11.1.x versions
          * Tests conducted so far, prove that fixes are bringing memory usage to 11.0 levels
          * Full mainnet release is expected later this week and is expected to be tagged as 11.2.1
      * [11.3](https://github.com/orgs/input-output-hk/projects/167/views/15)
        * Currently at least 2-3 weeks away from being released
        * There is currently significant portion of work being done on the consensus side
    * Plutus primitives
      * A number of new plutus primitives is being worked on
      * Respective governance actions are expected to be enacted on all Cardano testnets prior to the hard fork happening on each of those
    * Cardano Testnets
      * DijkstraNet
        * Forked to the Dijkstra era on 2nd November with 11.2
        * Includes the full feature set of Dijkstra era hard fork scope except Leios and Fair min fees (CIP-23) implementation
        * Downstream tooling teams are encouraged to start the integration against the available Dijkstra era feature set
        * Advanced configuration of DijkstraNet Testnet available [here](https://book.play.dev.cardano.org/adv-dijkstra.html)
        * Discord channel: [dijkstra-net](https://discord.com/channels/826816523368005654/1565517149047361586)
      * Musashi Testnet
        * Downstream tooling teams are encouraged to do the early integration against 11.3 prototype on Musashi Testnet
        * Week 44 node release available [here](https://github.com/input-output-hk/ouroboros-leios/releases/tag/rc-2026w44)
        * Discord channel: [musashi-testnet](https://discord.com/channels/826816523368005654/1517210858365911242)
      * SanchoNet
        * Expected to soon fork into the Dijkstra era
        * Discord channel: [sanchonet](https://discord.com/channels/826816523368005654/1141734250438197370)
    * Scope
      * Documenting the scope needs the following:
        * Merge the remaining impact assessments to the Dijkstra era GitBook space after addressing Kevins review of them
        * Add CIP-23 full implementation to the [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) GitBook page
        * Adjust CIP-23 impact assessment page based on the plan for the full CIP-23 implementation in Dijkstra era
    * Risk management
      * All risks with the scoring 50 and above were assessed and discussed on the call and where applicable, scoring was adjusted to lower number by successfully applying mitigation strategies
      * There is now another column in the risk log representing formal risk assessment for each record in the log
    * Constitutional amendments
      * [Fifth version of the new constitution](https://cap.intersectmbo.org/#/detail/12) has been uploaded to CAP last week by Carlos
        * Includes feedback collected so far
      * It is expected to soon have another iteration, sixth version
        * Should include actual values instead of placeholders
      * Parameter Committee will have a meeting on Thursday, 5th November
        * Carlos (Dijkstra) and Seabastian (Leios) are going to attend
      * New guardrails are going to be enacted and available on all Cardano testnets with custom configurations on preview and preprod)
      * Kevin (Parameter Committee) expressed the need for reference scripts from benchmarking team
      * Thomas from the Civics Committee will organize a series of additional meetings to further propagate the understanding of the upcoming changes of Cardano constitution and guardrails
      * Carlos has expressed the aim to submit the new constitution and guardrails no later than 25th November (or between epochs 667 and 669)
    * Ecosystem readiness
      * SPOs
        * Martin (ATADA) expressed concerns over confusion on whats being available and where, which features, which testnet, which version
          * as an example BLS registration is available with 11.2 on DijkstraNet although Linear Leios will only come with 11.3
      * Wallets
        * Vaccuumlabs representative shared the updates on making sure Ledger HW wallet is going to be DIjkstra compatible
          * Support for stake pool registration certificates in the Cardano Ledger app
          * Support for BLS is developed and waiting for the inclusion in the next release
          * Looking into other potential Dijkstra features they need to support.
        * VLs next priority is Trezor HW wallet
        * VL team currently dont have capacity to own Keystone HW wallet efforts
    * Node diversity
      * Amaru team has set the 5th November as the key milestone achievement date where Amaru node is expected to begin producing blcoks on mainnet
    * Hard Fork Working Group funding (Technical Steering Committee budget)
      * [Application form](https://forms.clickup.com/9015279944/f/8cnmga8-55475/D8A3VU9CZOQQU56CYX)
  * Hard Fork Working Group will continue to meet once a week until the Dijkstra era hard fork work solidifies enough to mandate more alignments and sync

#### **Reference links and engagement points**

* Hard Fork Working Group communication channels
  * [Discord](https://discord.com/channels/1136727663583698984/1242097284619960411) — `#wg-hard-fork`
  * [Weekly bulletins](https://x.com/IntersectMBO)
  * [Luma calendar](https://luma.com/calendar/cal-TMjYNpSY4huYYif)
  * [Email](mailto:hard-fork@intersectmbo.org)
* [BLS Key rotation](https://github.com/input-output-hk/ouroboros-leios/issues/1024)
* [Dijkstra readiness tracker](https://docs.google.com/spreadsheets/d/1C1Ai_YTqwKLHtICunzbh_o0FD9XB54Kh/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true)
* [Dijkstra Risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?usp=sharing)
* [Dijkstra era parameters in CAP](https://cap.intersectmbo.org/#/detail/12)
* [Antithesis](https://cardanofoundation.org/blog/improving-cardano-antithesis)
* [Recording](https://drive.google.com/file/d/1g_FEw-Z9Xv8aMKp5oN0E3i1DzizEagpa/view?usp=drive_link)
* [Transcript](https://docs.google.com/document/d/16h0N3XZPpmwJZIAD5UEXTSVQ5ZBTao30VgMJPFeZ4E8/edit?usp=drive_link)
* [Chat](https://drive.google.com/file/d/1KzurOaiIQvEcubamGlryDdgqf2GCtg2T/view?usp=drive_link)

#### **Action items and next steps**

* **Carlos:** Provide the shorter version of the [Dijkstra Era Constitution Changes](https://docs.google.com/presentation/d/1t8ysTu6ruYcFBBGHm50-wwuQ6uxZn8dn/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true) presentation
* **Leonard / Olga:** Provide the compatibility matrix on whats being available and where, which features, which testnet, which version
* **Thomas L:** organize a series of additional meetings to further propagate the understanding of the upcoming changes of Cardano constitution and guardrails
* **Carlos:** Draft the sixth version fo the Cardano constitution in relation to Dijkstra era parameters
* **Bosko:** Merge the remaining impact assessments to the Dijkstra era GitBook space after addressing Kevins review of them
* **Bosko:** Add CIP-23 full implementation to the [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) GitBook page
* **Bosko:** Adjust CIP-23 impact assessment page based on the plan for the full CIP-23 implementation in Dijkstra era
* **Bosko:** Consider adjusting Dijkstra risk log for better visibility and risk management
