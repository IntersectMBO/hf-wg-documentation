# 13th October 2026

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/general/hard-fork-working-group-meeting-minutes/6th-october-2026#action-items-and-next-steps) - Bosko
2. [Dijkstra era hard fork](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era/dijkstra-overview) - Bosko, all
   1. Releases, readiness and community engagement - Sam, Amani, Bosko
      1. [11.2](https://github.com/IntersectMBO/cardano-node/issues/6672)
      2. [11.3](https://github.com/input-output-hk/ouroboros-leios/issues/840)
         * Benchmark and performance - Can
      3. [Project view of versions](https://github.com/orgs/input-output-hk/projects/167/views/15)
   2. Scope, timing and risk - Bosko, Jeff, Amani
      1. Timeline - Bosko, Ian
      2. CIP-23 - Martin (ATADA)
      3. [IOLabs - Dijkstra Era Hard Fork](https://docs.google.com/document/d/1nVCzB8-l0fKpZLrQVrq9uLIkT69twuEaYHdf2fSEgOE/edit?tab=t.0#heading=h.blm90nnxn47g)
      4. [Dijkstra risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?gid=66373110#gid=66373110)
         * Now contains all identified items from IO [Technical risk log](https://drive.google.com/file/d/1MyBwgE-fI8lKMUYP_ctkHkchCPtXhB2X/view?usp=sharing)
      5. [Dijkstra Dependencies](https://drive.google.com/file/d/1VF9YavmkDiDkUCwzVzgv8_PwiZnt3-6F/view?usp=sharing) and gating
      6. Each remaining scope item (besides CIP-23 and CIP-50 which are already documented) have its impact documented ([PR](https://github.com/IntersectMBO/hf-wg-documentation/pull/43) opened) in the [Cardano Upgrades space](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) (Core semantics changes, Breaking API changes, New features)
   3. Protocol parameters and constitutional amendments
      1. [Dijkstra era parameters in CAP](https://cap.intersectmbo.org/#/detail/12)
   4. Node diversity
      1. Node diversity workshop in London, **12th&13th November** organized by Amaru team
         * London Marriott Hotel Canary Wharf\
           Address: 22 Hertsmere Rd, London E14 4ED, United Kingdom
      2. Dingo
      3. Amaru
      4. Gerolamo
      5. Scalus
      6. Haskell, Amaru (Rust), Dingo (Go), Dugite (Rust), TSUNAGI (Zig), Gerolamo (TypeScript), Dolos (Rust), Turbocardano (C++), Razor (.NET), Scalus (Scala), Yano (Java)
   5. Comms
3. Hard Fork Working Group funding (Technical Steering Committee budget)
4. AOB

#### Key materials

* Summary
  * **Dijkstra Era hard fork**
    * 11.2
      * Includes everything Dijkstra related except linear Leios
      * Expected to be pre-released by the end of this week (week of 12th October)
      * After the round of testing, its is expected to be promoted to mainnet ready release next week (week of 19th October)
      * DijkstraNet will be respun with pv11 and will fork to pv12
      * Community is invited to test and validate Dijkstra feature set except linear Leios once DijkstraNet forks to pv12
    * 11.3
      * This is the version that includes linear leios and is the first candidate to be promoted to 12.0 capable of crossing hard fork should the results of testing allow so and there are no blocking issues
        * Quality of the release remains one of the key aspects of the road to Dijkstra era hard fork
      * Its few weeks away from being released, more clarity is expected to be provided by the development teams on the next Hard Fork working group meeting
      * Performance and benchmarks plan is being carefully prepared to be executed once 11.3 becomes available
      * Remaining gh issues for 11.3 are listed [here](https://github.com/orgs/input-output-hk/projects/167/views/15)
      * [Leios roadmap & activity](https://github.com/orgs/input-output-hk/projects/167/views/9)
    * Constitutional amendments
      * There are \~100 guardrails estimated for protocol version 12
      * First version of the guardrail script is expected next week
      * Results from benchmarks will shape the final parameters which would lead to the new, final version of the guardrails script
      * [Discussion on Dijkstra era parameters](https://cap.intersectmbo.org/#/detail/12) is available in the Constitutional Amendment Portal
      * Carlos from IO announced the series of recordings to better inform community stakeholders about the intended guardrails
      * Ken-Erik proposed the idea of having a call with Constitutional Committee members to run through guardrails and parameters
    * Timeline
      * Availability of the node 11.3 will inform further progress towards Dijkstra era hard fork
      * Preparing the constitutional update and plutus v4 related parameters update are the next stepping stones
    * Scope
      * Besides already agreed, frozen scope for Dijkstra, documented [here](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), a sizable group of SPOs attending the call and represented by Martin (ATADA) have expressed their support and the ask to have CIP-23 fully implemented in protocol version 12 (without waiting to be activated in protocal version 13)
      * Development teams are willing to include it if the right circumstances are met
        * Introducing full support for CIP-23 this late might delay the originally planned dates for protocol version 12
        * Should there be any additional delays unrelated to CIP-23, development team intend to include it as a complete feature in the pv12 release candidate
        * [CIP-23 Fair min fees GitHub issue](https://github.com/IntersectMBO/cardano-ledger/issues/5954)
    * Risks
      * [Dijkstra risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?gid=66373110#gid=66373110) contains few high scoring risks
        * Technical Steering Committee reviewed the risks and the findings were shared with IO team
        * Managing the risk log and addressing the risks accordingly will become one of the main drivers of the hard fork working group efforts going forward
        * All Hard Fork Working group members are encouraged to review it, assess it, provide feedback where necessary and/or applicable, act where possible and having an ownership and make familiar before the next HFWG meeting
    * Node diversity
      * Node diversity workshop in London, **12th&13th November** organized by Amaru team
        * London Marriott Hotel Canary Wharf\
          Address: 22 Hertsmere Rd, London E14 4ED, United Kingdom
        * Reach out to Damien Czapla if you would like to attend
          * [Discord](https://discord.com/users/167667690624778241)
          * [Amaru on X](https://x.com/Amaru_Cardano)
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
* [Recording](https://drive.google.com/file/d/1DPexXj7hKQE9_Aaasswi9cS88SA42xSk/view?usp=drive_link)
* [Transcript](https://docs.google.com/document/d/15QrHqLwT0ah72T6-ZC6CSFbKSGRsb9XlLHQXlDQNl8k/edit?usp=drive_link)
* [Chat](https://drive.google.com/file/d/1YntcWsF4CaGquVILNzwshdRQmf1zqlzF/view?usp=drive_link)

#### **Action items and next steps**

* **Leonard/IO dev teams:** Size the effort of CIP-23 implementation and assess its impact on the DIjkstra era hard fork timeline
* **Bosko:** Share [the review of the Leios Risk register](https://docs.google.com/document/d/1kvf8twFWhwsYtnLfjjgu7D3isJBTKdm3zXgre1PRfFo/edit?usp=sharing) with the HFWG, prepared by Technical Steering Committee member Leandros
* **HFWG members:** Assess [Dijkstra risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?gid=66373110#gid=66373110), identify potential gaps and provide updates where necessary and/or applicable
* **Carlos:** Prepare the series of recordings to better inform community stakeholders about the intended guardrails
* **HFWG/Civics Committee:** Organize the call with Constitutional Committee membersto run through guardrails and parameters
* **Michiel/Elena/Bosko:** Determine HFWG wallet teams liaison(s) and finalize wallet teams outreach list
  *   **HFWG wallet teams liaison:** Reach out to Keystone, Ledger, Trezor, Bitbox (..?)

      and point them to the CDDL change of adding [`bls_key`](https://github.com/IntersectMBO/cardano-ledger/blob/2c33b4f858c0e62b300d121996a479f505d8c0e5/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L469)
* **Elena/Bosko:** Check and cross-reference readiness approach being taken in previous hard forks with Chang, Plomin and beyond
