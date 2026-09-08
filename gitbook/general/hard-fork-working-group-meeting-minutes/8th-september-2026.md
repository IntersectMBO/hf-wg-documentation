# 8th September 2026

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/general/hard-fork-working-group-meeting-minutes/1st-september-2026#action-items-and-next-steps) - Bosko
2. [Dijkstra era hard fork](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era/dijkstra-overview) - Bosko, all
   1. Releases, readiness and community engagement - Sam, Bosko
      1. 11.1.1
      2. 11.2
      3. 11.3
      4. Critical path tooling - Jordan, IO
         1. Ogmios and Kupo alternatives - `cardano-rpc` and `cardano-sieve` ready for testing
   2. Scope and timing - Jeff, Bosko
      1. [IOLabs - Dijkstra Era Hard Fork](https://docs.google.com/document/d/1nVCzB8-l0fKpZLrQVrq9uLIkT69twuEaYHdf2fSEgOE/edit?tab=t.0#heading=h.blm90nnxn47g)
      2. Technical risk log - Kevin, IO
      3. [Dijkstra Dependencies](https://drive.google.com/file/d/1VF9YavmkDiDkUCwzVzgv8_PwiZnt3-6F/view?usp=sharing)
      4. The aim is to have each scope item having its impact documented in the [Cardano Upgrades space](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) (Core semantics changes, Breaking API changes, New features)
   3. Protocol parameters and constitutional amendments
      1. [Dijkstra protocol parameters for the constitution update](https://docs.google.com/document/d/1M649pDQtquYr4n5QBx_Q7vfzyFINQssN8Cpp553BGvA/edit?usp=sharing) - shared with Parameter Committee on 27th August
      2. [Dijkstra Constitution Parameters - Summary & Tracking Issues](https://docs.google.com/document/d/1M649pDQtquYr4n5QBx_Q7vfzyFINQssN8Cpp553BGvA/edit?usp=sharing) - shared with Parameter Committee on 27th August
   4. Comms
      1. Critical path tooling, Ogmios and Kupo alternatives?
   5. Naming
      1. Naming info action - [metadata draft](https://docs.google.com/document/d/1tIkFkxycv4ndmOar99-iiUdr8prZYdYx__Eu3UzRE2I/edit?tab=t.0)
      2. HF naming process
   6. Node diversity
      1. Node diversity celebration day in Singapore & Online - organized by Amaru team
         1. [Announcement](https://x.com/Amaru_Cardano/status/2095090242357240201)
         2. [Content and agenda](https://hackmd.io/@Amaru/DiversityCelebrationDraft) (can be modified)
      2. Haskell, Amaru (Rust), Dingo (Go), Dugite (Rust), TSUNAGI (Zig), Gerolamo (TypeScript), Dolos (Rust), Turbocardano (C++), Razor (.NET), Scalus (Scala), Yano (Java)
3. AOB

#### Key materials

* Summary
  * **Dijkstra Era hard fork**
    * Releases, readiness and community engagement
      * 11.1
        * mainnet ready
        * brings small improvements
        * removes legacy tracing system
        * expected to be pre-released later today
      * 11.2
        * Integration is already underway and is expected to be completed in the next few weeks
        * It essentially brings everything (which includes new block format) but Leios from [the Dijkstra scope perspective](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview#phase-1-dijkstra-hard-fork-protocol-version-12-q4-2026)
          * The state of release will be outlined and kept up-to-date in the following GH issue: [https://github.com/IntersectMBO/cardano-node/issues/6672](https://github.com/IntersectMBO/cardano-node/issues/6672)&#x20;
        * This version **shouldnt** be considered of being capable to survive the hard fork event
        * It will enable early DIjkstra testing and will unlock beginning of downstream tooling integration against the specified feature set
        * DijkstraNet testnet will start with pv11 and will be forked to pv12 (again, without Leios)
      * Critical path tooling
        * Ogmios and Kupo alternatives - Even though `cardano-rpc` and `cardano-sieve` are considered ready for trial, Jeff from IO voiced the concern over the adoption curve so it was said that the effort on building the alternatives is prolonged for 2027
        * Dolos and Pallas are also considered to be on the critical path when it comes to readiness for Dijkstra
    * Scope and timing
      * [Dijkstra Overview page](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), after being cleaned up of the specific dates will become the single source of truth for Dijkstra hard fork scope
      * Document impact on all changes being introduced in the Dijkstra era hard fork and reference it in the Cardano Upgrades GitBook space
      * There was a walkthrough of the identified Dijkstra gating and dependencies by Kevin
        * [Dependencies diagram](https://drive.google.com/file/d/1VF9YavmkDiDkUCwzVzgv8_PwiZnt3-6F/view?usp=sharing)
          * It will move to Miro for better collaboration
        * [Dependencies spreadsheet](https://docs.google.com/spreadsheets/d/1meEMAMLaAiSaR4DkhmXz5LpGgFlnX_vTBPMV-vGmEzk/edit?usp=sharing)
          * Will become Dijkstra dependencies tracker with few more potential fields added
    * Protocol parameters and Constitutional amendments
      * There is going to be a new protocol parameters document prepared by Carlos from IO within the next day or two which will be considered the source of truth for Parameter Committee assessment and will be used for vertical CIP conformance
        * Alternative node teams need CIP level source of truth, rather than Haskell implementation level
    * Comms
      * The main focus is to move away from simply relaying the HFWG outputs in the Intersect Upgrade Bulletin and Weekly Update, to a more action-oriented "here is the news and what each ecosystem category can start to do to be prepared" approach
        * [Slide deck](https://docs.google.com/presentation/d/1V0CrMz1w7KeNUAc2VluTF51DFdTfZro2V6o8K4mMK4M/edit?usp=sharing)
    * Naming
      * Hard Fork Working Group had a motion on [23rd July](https://cardanoupgrades.docs.intersectmbo.org/general/hard-fork-working-group-meeting-minutes/23rd-july-2026#key-materials) where it recommended to name the next hard fork after Alexander Esgen
      * Naming info action [metadata](https://docs.google.com/document/d/1tIkFkxycv4ndmOar99-iiUdr8prZYdYx__Eu3UzRE2I/edit?usp=sharing) is drafted, but it can only be submitted pending Alexander **Esgen** family approval
      * In the absence of it, few potential alternatives have been considered
        * Adopting the neutral, technical naming process that relies on technical details, rather than community members (they would still be considered for In Memoriam section)
        * Naming it after Fabian **von Bergen**, referencing [the naming info action](https://adastat.net/governances/48bab0ca71cc46f2ee421242b14f292b8c8382bda707d03ea662644bed22b89300) that was submitted by community members independently of the Hard Fork Working Group and which passed the 50% threshold of DReps social aspect support
        * Naming it in a neutral way, but dedicating it to a good, socially responsible cause, that goes beyond Cardano ecosystem
    * Node diversity
      * Node diversity celebration day in Singapore & Online - organized by Amaru team
        * [Announcement](https://x.com/Amaru_Cardano/status/2095090242357240201)
        * [Content and agenda](https://hackmd.io/@Amaru/DiversityCelebrationDraft) (can be modified)
      * Dingo node team is [making significant progress](https://x.com/InASingleWord/status/2097012520787771427?s=20) and continues to build momentum
        * This week, Dingo by Blink labs is the [#1 most active Cardano repo with the highest number of commits](https://cardanoupdates.koios.rest/)
  * Hard Fork Working Group will continue to meet once a week until the Dijkstra era hard fork work solidifies enough to mandate more alignments and sync

#### **Reference links and engagement points**

* Hard Fork Working Group communication channels
  * [Discord](https://discord.com/channels/1136727663583698984/1242097284619960411) — `#wg-hard-fork`
  * [Weekly bulletins](https://x.com/IntersectMBO) (url edited)
  * [Luma calendar](https://luma.com/calendar/cal-TMjYNpSY4huYYif)
  * [Email](mailto:hard-fork@intersectmbo.org)
* [Product committee - Dijkstra Era: Phased Rollout Plan](https://product.cardano.intersectmbo.org/hardfork-planning/dijkstra/)
* [Leios impact analysis](https://github.com/input-output-hk/ouroboros-leios/blob/main/docs/ImpactAnalysis.md)
* [BLS Key rotation](https://github.com/input-output-hk/ouroboros-leios/issues/1024)
* [Dijkstra readiness tracker](https://docs.google.com/spreadsheets/d/1C1Ai_YTqwKLHtICunzbh_o0FD9XB54Kh/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true)
* [Dijkstra Risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?usp=sharing)
* [CAP (Constitutional Ammendment Portal)](https://cap.intersectmbo.org/)
  * [Guides](https://cap.intersectmbo.org/#/guides)
  * [Introduction to CAPs and CISs](https://cap.intersectmbo.org/#/guides/intro-to-caps-and-cis)
* [Antithesis](https://cardanofoundation.org/blog/improving-cardano-antithesis)
* [Recording](https://drive.google.com/file/d/1nQwAU2BgSKpLyUKOFjLzxmH4jiyy0Hfg/view?usp=sharing)
* [Transcript](https://docs.google.com/document/d/1P2ZmTFBwVaUky3pjmNuS6KaBpxzUOPUZnDYeu2bS3ko/edit?usp=sharing)
* [Chat](https://drive.google.com/file/d/1CCWcYneoY4qur3CIfp1-tUb1H71YLrWc/view?usp=sharing)

#### **Action items and next steps**

* **Bosko:** [Dijkstra Overview page](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), should be cleaned up of the specific dates to become the single source of truth for Dijkstra hard fork scope
* **Bosko/Ryan C W:** Document impact on all changes being introduced in the Dijkstra era hard fork and reference it in the Cardano Upgrades GitBook space
* **Bosko:** Create overall Dijkstra delivery timeline in Miro with the focus on dependencies so each HFWG participant/attendee and more broadly ecosystem, have clear view of the activities and milestones towards the DIjkstra era hard fork enactment
* **Kevin/Bosko:** Promote [Dijkstra dependencies spreadsheet](https://docs.google.com/spreadsheets/d/1meEMAMLaAiSaR4DkhmXz5LpGgFlnX_vTBPMV-vGmEzk/edit?usp=sharing) to the official dependencies tracker for Dijkstra are hard fork
* **Carlos:** Prepare the new protocol parameters document which will be considered the source of truth for Parameter Committee assessment and will be used for vertical CIP conformance
* **Ian:** Move away from simply relaying the HFWG outputs in the Intersect Upgrade Bulletin and Weekly Update, to a more action-oriented "here is the news and what each ecosystem category can start to do to be prepared" approach
* **Nick/IO:** Reach out to and try to get Alexander Esgen family approval to name the Dijkstra era hard fork after him
* **Bosko/all:** Start the neutral naming process for the hard fork async
* **Jeff:** Provide major release notes on node starting with version 11.2 which would help with early readiness assessment and integration planning by downstream tooling
* **Elena/Bosko:** Check and cross-reference readiness approach being taken in previous hard forks with Chang, Plomin and beyond
* **Kevin/Sam L/Ryan C W/Damien:** Draft the decision making and prioritization process for future hard forks
