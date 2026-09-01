# 1st September 2026

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/general/hard-fork-working-group-meeting-minutes/25th-august-2026#action-items-and-next-steps) - Bosko
2. [Dijkstra era hard fork](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era/dijkstra-overview) - Bosko, all
   1. Releases, readiness and community engagement - Sam, Bosko
      1. 11.2
         * CIPs, protocol parameters, BLS keys
         * CDDL?
         * DBSync?
         * Downstream tooling?
      2. 11.3
   2. Scope and timing - Jeff, Bosko
      1. [IOLabs - Dijkstra Era Hard Fork](https://docs.google.com/document/d/1nVCzB8-l0fKpZLrQVrq9uLIkT69twuEaYHdf2fSEgOE/edit?tab=t.0#heading=h.blm90nnxn47g)
      2. The aim is to have each scope item having its impact documented in the [Cardano Upgrades space](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) (Core semantics changes, Breaking API changes, New features)
   3. Protocol parameters and constitutional amendments
      1. [Dijkstra protocol parameters for the constitution update](https://docs.google.com/document/d/1M649pDQtquYr4n5QBx_Q7vfzyFINQssN8Cpp553BGvA/edit?usp=sharing) - shared with Parameter Committee on 27th August
      2. [Dijkstra Constitution Parameters - Summary & Tracking Issues](https://docs.google.com/document/d/1M649pDQtquYr4n5QBx_Q7vfzyFINQssN8Cpp553BGvA/edit?usp=sharing) - shared with Parameter Committee on 27th August
   4. Comms
      1.
   5. Naming
      1. [Metadata](https://docs.google.com/document/d/1tIkFkxycv4ndmOar99-iiUdr8prZYdYx__Eu3UzRE2I/edit?usp=sharing) is being prepared for the submission of naming info action
         * Aiming to be submitted in epoch 654 (starts 6th September) or 655 (starts 11th September), pending Alexander Esgen family approval
         * Based on [the hfwg call motion on 23rd July](https://cardanoupgrades.docs.intersectmbo.org/general/hard-fork-working-group-meeting-minutes/23rd-july-2026#key-materials), hfwg is proposing to name the hard fork after **Alexander Esgen**, with adding In Memoriam section to eternalize others who sadly passed away in recent months/years
           * HFWG acknowledges that there is the expired [info action](https://cardanoscan.io/govAction/gov_action1fzatpjn3e3r09mjzzfptznef9wxg8q4a5uraq04xvfjyhmfzhzfsqqgfc9h) to name it after **Fabian von Bergen**, although deemed unconstitutional from the perspective of not having the document at the designated URL immutable, gained sizable DReps and SPOs support
           * **Steven Lupien**
           * **Gregg Morgan** aka [@bone\_pool](https://x.com/bone_pool)
           * **Sean Davies**
   6. Node diversity
      1. Amaru
         * Block production node release (Target): September 29th start with a pre-release, have a beta \~4 weeks after
         * 2 upcoming node diversity events organized by Amaru team - Damien
           * One around Token2049 on the 6th October (online event with a small cohort offline in Singapore)
           * 12th + 13th November node diversity workshop in London
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
      * 11.2
        * Integration has started
        * It essentially brings everything (which includes new block format) but Leios from [the Dijkstra scope perspective](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview#phase-1-dijkstra-hard-fork-protocol-version-12-q4-2026)
        * This version **shouldnt** be considered of being capable to survive the hard fork event
        * It will enable early DIjkstra testing and will unlock beginning of downstream tooling integration against the specified feature set
        * DijkstraNet testnet will start with pv11 and will be forked to pv12 (again, without Leios)
      * 11.3
        * This is intended to be the full Dijkstra scope version and the first one to be marked as hf ready, however, as follows below:
      * 12.0
        * This is the version that is meant to bring Dijkstra era to life with protocol version 12
    * Scope and timing
      * Dijkstra scope is well [documented](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview#phase-1-dijkstra-hard-fork-protocol-version-12-q4-2026)
      * [Technical delivery plan](https://docs.google.com/document/d/1nVCzB8-l0fKpZLrQVrq9uLIkT69twuEaYHdf2fSEgOE/edit?usp=sharing) from IO, its [current version](https://docs.google.com/document/d/1nVCzB8-l0fKpZLrQVrq9uLIkT69twuEaYHdf2fSEgOE/edit?usp=sharing) (after recalibration), communicates:
        * moderate confidence timeline (HF GA enactment window from 5th December at the earliest to 4th January at the latest)
        * high confidence timeline (HF GA enactment window from 24th Feburary at the earliest to 26th March at the latest)
      * Although the impact that Dijkstra era hard fork brings is well documented from the perspective of CIPs included, there are certain aspects like fee function update for example, whose impact is not documented
        * All changes should be documented in a way that helps downstream tooling teams to adjust and prepare to be ready for the hard fork
        * Major release notes would significantly contribute to the right level of information
      * Document impact on all changes being introduced in the Dijkstra era hard fork and reference it in the Cardano Upgrades GitBook space
    * Protocol parameters and Constitutional amendments
      * On the behalf of IO team, Carlos provided a list of Dijkstra protocol parameters to the Parameter Committee ahead of the committee meeting this Thursday
        * IO representatives confirmed they will be attending the meeting for an open discussion and a walkthrough of the parameters
        * It is also expected to have the first draft of the new constitution, which takes Dijkstra introduced parameters into account, to be prepared by Carlos from IO this week
        * Peras related parameters are yet to be provided, but will have the fixed value set and shouldnt be considered concerning from the guardrails perspective
    * Comms
      * Comms will continue this week with the upgrade bulletin on X published and shared this week
    * Naming
      * Hard Fork Working Group members are invited to provide feedback on the drafted naming info action [metadata](https://docs.google.com/document/d/1tIkFkxycv4ndmOar99-iiUdr8prZYdYx__Eu3UzRE2I/edit?usp=sharing) at the earliest possible convenience
      * On the next HFWG meeting next week, metadata could potentially be considered finalized&#x20;
      * Technical Steering Committee would ackonwledge it and endorse it based on HFWG recommendation
      * Naming info action will not be submitted to chain prior to the approval of the Alexander Esgen family
        * Furthermore, families of all other community members considered for In Memoriam section, will be contacted to get the approval too (Gregg Morgan, Fabian Von Bergen, Steven Lupien and Sean Davies)
      * In the potential absence of the community members families approval, Hard Fork Working Group will consider different naming approach
    * Node diversity
      * Amaru
        * For the node diversity celebration event in Singapore, on 7th and 8th October in Singapore
          * Attendees: Every node implementation leader
            * &#x20;Jeff and Carlos will likely represent Haskell node team
          * Purpose: Get a look at all the implementation timelines
        * Node diversity workshop in London, on 12th and 13th November
          * Attendees: Node implementation teams; SPOs; Hard fork decision makers
          * Purpose: Decide on the cost-efficient approach for Cardano network upgrades
        * Amaru team representative Damien, brought up following topics as potential candidates for a discussion on the workshop
          * minimal standards to consider something a good Cardano product with subtopics
            * Conformance
            * Data sets
            * Adversarial scenarios
          * in the node diverse Cardano ecosystem, source of truth moves from Haskell node to the protocol level
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
* [Recording](https://drive.google.com/file/d/1guRQG2HLpNMx5-NXxr3oA_1wrg69XufO/view?usp=drive_link)
* [Transcript](https://docs.google.com/document/d/1LLQnubfefXKZsu8ThK5rnCFxMFrrpIUJ_NwzkX-EGl8/edit?usp=drive_link)
* [Chat](https://drive.google.com/file/d/1HeWI4l0XgLOwr_K0jlYF1xrDsIytqZND/view?usp=drive_link)

#### **Action items and next steps**

* Carlos: Attend the Parameter Committee meeting on Thursday, 3rd September and give a walkthrough of Dijkstra related protocol parameters and the constitution draft that would reflect those changes&#x20;
* **Jeff:** Provide major release notes on node starting with version 11.2 which would help with early readiness assessment and integration planning by downstream tooling
* **Bosko/Sebastian/Carlos:** Document impact on all changes being introduced in the Dijkstra era hard fork and reference it in the Cardano Upgrades GitBook space
* **Bosko:** Finalize v1 of Dijkstra readiness tracker (includes readiness reported against different networks) to apply correct and precise readiness calculations in it
* **Elena/Bosko:** Check and cross-reference readiness approach being taken in previous hard forks with Chang, Plomin and beyond
* **Nick:** Reach out to and try to get Alexander Esgen family approval to name the Dijkstra era hard fork after him
* **Bosko:** Reach out to families of all other community members considered for In Memoriam section to get the approval for them being mentioned (Gregg Morgan, Fabian Von Bergen, Steven Lupien and Sean Davies)
* **Bosko:** Create overall Dijkstra delivery timeline in Miro so each HFWG participant/attendee and more broadly ecosystem, have clear view of the activities and milestones towards the DIjkstra era hard fork enactment
* **Kevin/Sam L/Ryan C W/Damien:** Draft the decision making and prioritization process for future hard forks
