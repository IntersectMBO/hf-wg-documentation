# 29th September 2026

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/general/hard-fork-working-group-meeting-minutes/22nd-september-2026#action-items-and-next-steps) - Bosko
2. [Dijkstra era hard fork](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era/dijkstra-overview) - Bosko, all
   1. Releases, readiness and community engagement - Sam, Amani, Bosko
      1. [11.1.2](https://github.com/IntersectMBO/cardano-node/releases/tag/11.1.2)
      2. [11.1.3](https://github.com/IntersectMBO/cardano-node/releases/tag/11.1.3)
      3. [11.2](https://github.com/IntersectMBO/cardano-node/issues/6672)
   2. Leios - Jeff, Amani, Sam, Kevin
   3. Scope and timing - Bosko, Jeff
      1. [IOLabs - Dijkstra Era Hard Fork](https://docs.google.com/document/d/1nVCzB8-l0fKpZLrQVrq9uLIkT69twuEaYHdf2fSEgOE/edit?tab=t.0#heading=h.blm90nnxn47g)
      2. [Technical risk log](https://drive.google.com/file/d/1MyBwgE-fI8lKMUYP_ctkHkchCPtXhB2X/view?usp=sharing) & [Dijkstra risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?gid=66373110#gid=66373110)
      3. [Dijkstra Dependencies](https://drive.google.com/file/d/1VF9YavmkDiDkUCwzVzgv8_PwiZnt3-6F/view?usp=sharing) and gating
      4. Each remaining scope item (besides CIP-23 and CIP-50 which are already documented) have its impact documented ([PR](https://github.com/IntersectMBO/hf-wg-documentation/pull/43) opened) in the [Cardano Upgrades space](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) (Core semantics changes, Breaking API changes, New features)
   4. Protocol parameters and constitutional amendments
      1. [Updated list of Dijkstra parameters](https://hackmd.io/@eJKr9l7wQ6aU2PgNdrfgZg/Dijktstra-parameters) was shared with the Parameter Committee on Thursday, 10th September and are now under assessment
   5. Comms
      1.
   6. Node diversity
      1. Node diversity celebration day in Singapore & Online - organized by Amaru team
         * [Announcement](https://x.com/Amaru_Cardano/status/2095090242357240201)
         * [Content and agenda](https://hackmd.io/@Amaru/DiversityCelebrationDraft) (can be modified)
      2. Dingo
      3. Amaru
      4. Gerolamo
      5. Scalus
      6. Haskell, Amaru (Rust), Dingo (Go), Dugite (Rust), TSUNAGI (Zig), Gerolamo (TypeScript), Dolos (Rust), Turbocardano (C++), Razor (.NET), Scalus (Scala), Yano (Java)
3. Neutral naming process - Bosko
   1. [Draft open for feedback](https://docs.google.com/document/d/1RK2PEKAbvLtM4p7KWHNsdCEqN4OhZQEy/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true)
4. Hard Fork Working Group funding (Technical Steering Committee budget)
5. AOB

#### Key materials

* Summary
  * **Dijkstra Era hard fork**
    * Releases, readiness and community engagement
      * [11.1.3](https://github.com/IntersectMBO/cardano-node/releases/tag/11.1.3) has been released
        * Fixes Ledger's IPv4 decoding: releases before `11.1.x` decoded IPv4s using network order, which `11.1.2` inadvertently changed; this has been reverted to using network order for decoding IPv4s.
        * There is a slight increase in memory usage compared to node version `11.0.1` when **syncing**, but this is significantly less than the regression in `11.1.0`. [Full details](https://tests.cardano.intersectmbo.org/test_results/sync_reports/mainnet_11_1_1.html)
        * There is a small increase in memory usage compared to node version `11.0.1` when **on tip**, which correlates with taking ledger snapshots. (Full details published in release benchmark report
        * There is no security vulnerability that `11.1.3` is addressing, however all [11.1.2](https://github.com/IntersectMBO/cardano-node/releases/tag/11.1.2) are encouraged to upgrade to `11.1.3` as it addresses the bug described above
      * [11.2](https://github.com/IntersectMBO/cardano-node/issues/6672)
        * It essentially brings everything (which includes new block format) but Leios from [the Dijkstra scope perspective](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview#phase-1-dijkstra-hard-fork-protocol-version-12-q4-2026)
          * Includes Plutus v4 context
        * Release sequence work has started
        * The earliest possible date for having a version tagged is end of this week and, paired with the performance tests and benchmarking done over the weekend, would bring the pre-release `11.2` next week
        * Full release is likely 2-3 weeks away
        * This version **shouldnt** be considered of being capable to survive the hard fork event
      * 11.3
        * Expected to follow `11.2` few weeks after, but `11.2` is considered non-blocking for `11.3` integration progress
        * According to the latest report from the development teams, release candidate is roughly 43% done, with 20% in progress
        * This version will include Leios and if no additional fixes and adjustments needed, it will be the version promoted to the mainnet HF ready `12.0`
    * Scope
      * [Technical risk log](https://drive.google.com/file/d/1MyBwgE-fI8lKMUYP_ctkHkchCPtXhB2X/view?usp=sharing) shared by IO is to transition to [Dijkstra risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?gid=66373110#gid=66373110) with technical risks being available in separate tab
      * [Dijkstra Dependencies](https://drive.google.com/file/d/1VF9YavmkDiDkUCwzVzgv8_PwiZnt3-6F/view?usp=sharing) log should be used for collaboration
      * Each remaining scope item (besides CIP-23 and CIP-50 and CIP-164 - Leios) which are already documented) have its impact documented ([PR](https://github.com/IntersectMBO/hf-wg-documentation/pull/43) opened) in the [Cardano Upgrades space](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) (Core semantics changes, Breaking API changes, New features)
      * Leios
        * HFWG needs still needs wallet teams liaison to address risk of delayed upgrade
    * Protocol parameters and Constitutional amendments
      * Parameter Committee review doc should be publicized through CAP by the end of this week after getting the initial feedback from the committee itself
        * Kevin initial review estimates \~100 Leios related guardrails and \~50 Peras related (for the context, there are currently \~150 guardrails)
      * There is potentially going to be Plutus v4 primitives and subsequent cost models needed which would require new Prtocol Parameter Update governance action submitted on mainnet
        * status is expected to become apparent by mid-October
        * it should ideally happen before the hard fork is enacted, but can also happen after
    * Node diversity
      * There is the upcoming [**Cardano - Node diversity celebration day in Singapore (and online) - 6th October 26**](https://hackmd.io/@Amaru/DiversityCelebrationDraft) organized by Amaru team
        * _"The purpose of this event is to create a shared and visible moment around that progress. It will give Cardano’s different node implementations an opportunity to present what they are building, explain the value they intend to bring to the network and provide a clear view of their current progress and upcoming big milestones"_
    * Neutral naming process
      * There is a [draft open for feedback](https://docs.google.com/document/d/1RK2PEKAbvLtM4p7KWHNsdCEqN4OhZQEy/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true) that suggests each era could have few hf names candidates well in advance and that they could be named after significant discoveries, theorems or even problems that era named mathematicians and scientists became known for
  * Hard Fork Working Group will continue to meet once a week until the Dijkstra era hard fork work solidifies enough to mandate more alignments and sync

#### **Reference links and engagement points**

* Hard Fork Working Group communication channels
  * [Discord](https://discord.com/channels/1136727663583698984/1242097284619960411) — `#wg-hard-fork`
  * [Weekly bulletins](https://x.com/IntersectMBO) (url edited)
  * [Luma calendar](https://luma.com/calendar/cal-TMjYNpSY4huYYif)
  * [Email](mailto:hard-fork@intersectmbo.org)
* [BLS Key rotation](https://github.com/input-output-hk/ouroboros-leios/issues/1024)
* [Recent showcase of the Leios prototype](https://x.com/carloslodelar/status/2099763976561181130)
* [Dijkstra readiness tracker](https://docs.google.com/spreadsheets/d/1C1Ai_YTqwKLHtICunzbh_o0FD9XB54Kh/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true)
* [Dijkstra Risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?usp=sharing)
* [CAP (Constitutional Ammendment Portal)](https://cap.intersectmbo.org/)
  * [Guides](https://cap.intersectmbo.org/#/guides)
  * [Introduction to CAPs and CISs](https://cap.intersectmbo.org/#/guides/intro-to-caps-and-cis)
* [Antithesis](https://cardanofoundation.org/blog/improving-cardano-antithesis)
* [Recording](https://drive.google.com/file/d/1ZTJnzCXyA7gEJI5oT30fPRiUAh_zcSZZ/view?usp=drive_link)
* [Transcript](https://docs.google.com/document/d/127q9gI62KHkEVKTz-h7hu4Qgefo8CXaatFQTd5zW15Y/edit?usp=drive_link)
* [Chat](https://drive.google.com/file/d/1ySnPPFz2SRjDcgwn9szRVsWOoXyDUCHS/view?usp=drive_link)

#### **Action items and next steps**

* **Bosko:** Create overall Dijkstra delivery timeline in Miro with the focus on dependencies so each HFWG participant/attendee and more broadly ecosystem, have clear view of the activities and milestones towards the DIjkstra era hard fork enactment
* **Michiel/Elena/Bosko:** Determine HFWG wallet teams liaison
  *   **HFWG wallet teams liaison:** Reach out to Keystone, Ledger, Trezor, Bitbox (..?)

      and point them to the CDDL change of adding [`bls_key`](https://github.com/IntersectMBO/cardano-ledger/blob/2c33b4f858c0e62b300d121996a479f505d8c0e5/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L469)
* **Daniel/Amani/Bosko:** Convert Leios technical risk log to more easily maintainable spreadsheet file where anyone with the link has commenting permissions
* **Parameter Committee:** Provide feedback on the [updated list of Dijkstra parameters](https://hackmd.io/@eJKr9l7wQ6aU2PgNdrfgZg/Dijktstra-parameters) to IO
  * Consider including Amaru team in the guardrails testing
* **Ziyang/Sam:** Provide update on the need for Plutus v4 primitives and cost model by mid-October
* **Carlos/Sebastian:** Parameter Committee review doc should be publicized through CAP by the end of the week (2nd October)
* **CIP expert(s):** Review and comment on this [PR](https://github.com/IntersectMBO/hf-wg-documentation/pull/43) that is raised to document impact of all changes being introduced in the Dijkstra era hard fork
* **Damien/Bosko:** Confirm the venue for the Node diversity workshop in London on 12th & 13th November
* **Elena/Bosko:** Check and cross-reference readiness approach being taken in previous hard forks with Chang, Plomin and beyond
