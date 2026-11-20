# 10th November 2026

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/general/hard-fork-working-group-meeting-minutes/3rd-november-2026#action-items-and-next-steps) - Bosko
2. [Dijkstra era hard fork](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era/dijkstra-overview) - Bosko, all
   1. Releases
      1. [11.2.1](https://github.com/IntersectMBO/cardano-node/releases/tag/11.2.1) - Jeff, Amani, Sam
         * Lower memory use
         * Faster snapshots while syncing
         * LSM is supported for block production
      2. 11.3 - Sebastian
      3. [Project view of versions](https://github.com/orgs/input-output-hk/projects/167/views/15)
   2. [Dijkstra risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?gid=66373110#gid=66373110) review
   3. Scope
      1. Each remaining scope item (besides CIP-23 and CIP-50 which are already documented) have its impact documented ([PR](https://github.com/IntersectMBO/hf-wg-documentation/pull/43) opened) in the [Cardano Upgrades space](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) (Core semantics changes, Breaking API changes, New features)
         * [Updated Leios impact assessment available for feedback](https://drive.google.com/file/d/1GJNMixEGb6-jEOh8Yy_p2N--cPPz1Jh6/view?usp=sharing) (passed from TSC to original authors)
   4. Constitutional amendments - [Dijkstra era parameters in CAP](https://cap.intersectmbo.org/#/detail/12)
   5. Comms - Larisa, Ian, Matthew
   6. Node diversity
      1. Amaru
         * 57 blocks created on mainnet so far
         * 20 per days projected for the coming weeks
      2. [Block produced on mainnet](https://kleioscan.com/#/mainnet/nodes)
         * cardano-node, Amaru, Dingo, cardano-bean
      3. Node diversity workshop in London this week, **12th&13th November** organized by Amaru team
         * London Marriott Hotel Canary Wharf\
           Address: 22 Hertsmere Rd, London E14 4ED, United Kingdom
         * [Working agenda](https://hackmd.io/0b_HvF4AS-q4wayJP6M25A)
      4. Haskell, Amaru (Rust), Dingo (Go), Dugite (Rust), TSUNAGI (Zig), Gerolamo (TypeScript), Dolos (Rust), Turbocardano (C++), Razor (.NET), Scalus (Scala), Yano (Java)
3. Hard Fork Working Group funding (Technical Steering Committee budget)
   1. Application form - [https://forms.clickup.com/9015279944/f/8cnmga8-55475/D8A3VU9CZOQQU56CYX](https://forms.clickup.com/9015279944/f/8cnmga8-55475/D8A3VU9CZOQQU56CYX)
4. AOB

#### Key materials

* Summary
  * **Dijkstra Era hard fork**
    * Releases
      * [11.2.1](https://github.com/IntersectMBO/cardano-node/releases/tag/11.2.1)
        * Pre-released today
        * Key highlights
          * Lower memory use
          * Faster snapshots while syncing
          * LSM is supported for block production
        * Full, mainnet ready release, expected by the end of the week
        * This is not the hard fork ready version, but rather a step towards it
        * Its available for testing on DijkstraNet and includes everything but Linear Leios ([CIP-164](https://cips.cardano.org/cip/CIP-0164)) and Fair Min Fees ([CIP-23](https://cips.cardano.org/cip/CIP-0023))
          * DijkstraNet is already in Dijkstra era
      * [11.3](https://github.com/orgs/input-output-hk/projects/167/views/15)
        * Few weeks away from being released
        * A lot of feedback is expected, will be welcomed and appreciated
        * It will include Linear Leios ([CIP-164](https://cips.cardano.org/cip/CIP-0164)) and Fair Min Fees ([CIP-23](https://cips.cardano.org/cip/CIP-0023)) compared to version [11.2.1](https://github.com/IntersectMBO/cardano-node/releases/tag/11.2.1)
        * After the round of focused and systematic testing, if there arent serious challenges, it can be potentially promoted to version 12.0 which would be considered to be the hard fork ready candidate
    * Cardano Testnets
      * DijkstraNet
        * Forked to the Dijkstra era on 2nd November with 11.2
          * Expected to run on 11.2.1 upon the release of the version
        * Includes the full feature set of Dijkstra era hard fork scope except Linear Leios (CIP-164) and Fair min fees (CIP-23) implementation
        * Downstream tooling teams are encouraged to start the integration against the available Dijkstra era feature set
        * Advanced configuration of DijkstraNet Testnet available [here](https://book.play.dev.cardano.org/adv-dijkstra.html)
        * Discord channel: [dijkstra-net](https://discord.com/channels/826816523368005654/1565517149047361586)
      * Musashi Testnet
        * Downstream tooling teams are encouraged to do the early integration against 11.3 prototype on Musashi Testnet
        * Week 45 node release available [here](https://github.com/input-output-hk/ouroboros-leios/releases/tag/rc-2026w45)
        * Discord channel: [musashi-testnet](https://discord.com/channels/826816523368005654/1517210858365911242)
      * SanchoNet
        * Expected to soon fork into the Dijkstra era
        * Discord channel: [sanchonet](https://discord.com/channels/826816523368005654/1141734250438197370)
    * Scope
      * Added CIP-23 full implementation to the [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) GitBook page
      * Adjust CIP-23 impact assessment page based on the plan for the full CIP-23 implementation in Dijkstra era
      * Merge the remaining impact assessments to the Dijkstra era GitBook space after addressing their pending reviews
    * Risk management
      * All risks with the scoring 50 and above from the [Dijkstra risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?usp=sharing) were assessed and discussed on the call and where applicable, scoring was adjusted to lower number by successfully applying mitigation strategies
      * Alternative path for Ogmios/Kupo readiness is being considered, Leonard H. to confirm the chosen path for the time being
      * Appropriate benchmarks would help define the costs-to-benefit ratio of Linear Leios for mainnet
        * Kevin will share his view on how to setup the benchmarking cluster
      * Linear Leios undermines Praos safety under adversarial conditions - The Leios team cant reproduce it anymore after adjustments being made
    * Constitutional amendments
      * Sixth version of the draft of the new Constitution is expected later this week in [CAP portal](https://cap.intersectmbo.org/#/detail/12)
      * It continues to be adjusted with more pending and outstanding items being closed
      * [CAP-12 v5 Reference-script guardrails review](https://docs.google.com/document/d/1DBL6UFbh28wjaH9yADRs4sjglIsI70rWsCbUEETosaM/edit?usp=sharing) by TSC
      * [Dijkstra era | Cardano's next protocol upgrade](https://www.youtube.com/watch?v=k4x0eP_h1Qo) (video prepared by Carlos Lopez de Lara - Product Manager, Leios)
    * Ecosystem readiness
      * Tooling - High level
        * Koios is live in DijkstraNet
      * SPOs
        * Compatibility matrix was shared in the last weeks upgrade bulletin and will be added to the [Dijkstra upgrade readiness](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-readiness) page
    * Node diversity
      * Amaru
        * 57 blocks created on mainnet so far
        * 20 per days projected for the coming weeks
      * [Block produced on mainnet](https://kleioscan.com/#/mainnet/nodes)
        * cardano-node, Amaru, Dingo, cardano-bean
      * Node diversity workshop in London this week, **12th&13th November** organized by Amaru team
        * London Marriott Hotel Canary Wharf\
          Address: 22 Hertsmere Rd, London E14 4ED, United Kingdom
    * Hard Fork Working Group funding (Technical Steering Committee budget)
      * [Application form](https://forms.clickup.com/9015279944/f/8cnmga8-55475/D8A3VU9CZOQQU56CYX)
  * Hard Fork Working Group will continue to meet once a week until the Dijkstra era hard fork work solidifies enough to mandate more alignments and sync

#### **Reference links and engagement points**

* Hard Fork Working Group communication channels
  * [Discord](https://discord.com/channels/1136727663583698984/1242097284619960411) — `#wg-hard-fork`
  * [Weekly bulletins](https://x.com/IntersectMBO)
  * [Luma calendar](https://luma.com/calendar/cal-TMjYNpSY4huYYif)
  * [Email](mailto:hard-fork@intersectmbo.org)
* [Dijkstra era | Cardano's next protocol upgrade](https://www.youtube.com/watch?v=k4x0eP_h1Qo)
* [BLS Key rotation](https://github.com/input-output-hk/ouroboros-leios/issues/1024)
* [Dijkstra readiness tracker](https://docs.google.com/spreadsheets/d/1C1Ai_YTqwKLHtICunzbh_o0FD9XB54Kh/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true)
* [Dijkstra Risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?usp=sharing)
* [Dijkstra era parameters in CAP](https://cap.intersectmbo.org/#/detail/12)
* [Antithesis](https://cardanofoundation.org/blog/improving-cardano-antithesis)
* [Recording](https://drive.google.com/file/d/1L9buCR7x-YJnzcXlsUoEAdOsCpAc4W3s/view?usp=drive_link)
* [Transcript](https://docs.google.com/document/d/1Y6TeiWhB9YVjVBeMsSshvFvXkmmqDph91DjR6i_GAO0/edit?usp=drive_link)
* [Chat](https://drive.google.com/file/d/1TiNDkZfBZAd0oBH8Q4ulnEVbVR2AV1qE/view?usp=drive_link)

#### **Action items and next steps**

* **Leonard H:** Confirm the chosen path for Ogmios/Kupo from the readiness aspect
* **Carlos:** Draft the sixth version fo the Cardano constitution in relation to Dijkstra era parameters
* **Bosko:** Merge the remaining impact assessments to the Dijkstra era GitBook space after addressing Kevins review of them
* **Bosko:** Adjust CIP-23 impact assessment page based on the plan for the full CIP-23 implementation in Dijkstra era
* **Bosko:** Consider adjusting Dijkstra risk log for better visibility and risk management
