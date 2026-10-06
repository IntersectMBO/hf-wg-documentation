# 6th October 2026

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/general/hard-fork-working-group-meeting-minutes/29th-september-2026#action-items-and-next-steps) - Bosko
2. [Dijkstra era hard fork](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era/dijkstra-overview) - Bosko, all
   1. Releases, readiness and community engagement - Sam, Amani, Bosko
      1. [11.2](https://github.com/IntersectMBO/cardano-node/issues/6672)
      2. [11.3](https://github.com/input-output-hk/ouroboros-leios/issues/840)
         * New version of Plutus 1.72+, no integration neeeded
         * Enables new primitives
         * Optional fiels in guardrails script
      3. [Project view of versions](https://github.com/orgs/input-output-hk/projects/167/views/15)
   2. Leios - Jeff, Amani, Sam, Kevin
   3. Scope and timing - Bosko, Jeff
      1. [IOLabs - Dijkstra Era Hard Fork](https://docs.google.com/document/d/1nVCzB8-l0fKpZLrQVrq9uLIkT69twuEaYHdf2fSEgOE/edit?tab=t.0#heading=h.blm90nnxn47g)
      2. [Dijkstra risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?gid=66373110#gid=66373110)
         * Now contains all identified items from IO [Technical risk log](https://drive.google.com/file/d/1MyBwgE-fI8lKMUYP_ctkHkchCPtXhB2X/view?usp=sharing)
      3. [Dijkstra Dependencies](https://drive.google.com/file/d/1VF9YavmkDiDkUCwzVzgv8_PwiZnt3-6F/view?usp=sharing) and gating
      4. Each remaining scope item (besides CIP-23 and CIP-50 which are already documented) have its impact documented ([PR](https://github.com/IntersectMBO/hf-wg-documentation/pull/43) opened) in the [Cardano Upgrades space](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) (Core semantics changes, Breaking API changes, New features)
   4. Protocol parameters and constitutional amendments
      1. [Dijkstra era parameters in CAP](https://cap.intersectmbo.org/#/detail/12)
   5. Node diversity
      1. Node diversity celebration day today in Singapore & Online - organized by Amaru team
         * [Announcement](https://x.com/Amaru_Cardano/status/2095090242357240201)
         * [Content and agenda](https://hackmd.io/@Amaru/DiversityCelebrationDraft) (can be modified)
      2. Dingo
      3. Amaru
      4. Gerolamo
      5. Scalus
      6. Haskell, Amaru (Rust), Dingo (Go), Dugite (Rust), TSUNAGI (Zig), Gerolamo (TypeScript), Dolos (Rust), Turbocardano (C++), Razor (.NET), Scalus (Scala), Yano (Java)
   6. Comms
   7. Neutral naming process - Bosko
      1. [Draft open for feedback](https://docs.google.com/document/d/1RK2PEKAbvLtM4p7KWHNsdCEqN4OhZQEy/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true)
3. Hard Fork Working Group funding (Technical Steering Committee budget)
4. AOB

#### Key materials

* Summary
  * **Dijkstra Era hard fork**
    * Releases, readiness and community engagement
      * 11.2
        * This version is well in progress
        * It brings everything (which includes new block format) but Leios from [the Dijkstra scope perspective](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview#phase-1-dijkstra-hard-fork-protocol-version-12-q4-2026)
        * It will also include parameters in draft
        * Full release is likely 1-2 weeks away
        * This version **shouldnt** be considered of being capable to survive the hard fork event
        * It would be able to be run on DijkstraNet, rather than Musashi as it would be incompatible with the node running on Musashi
        * Expectation is to have it tagged with 11.2 this week and next week mainnet ready (if no other issues have been found)
      * 11.3
        * Precise Leios feature list is expected to become known from IO team by the end of this week
          * These decisions would serve the goal of having a version supporting leios by the end of the month
    * Timing
      * 15th December is the last reasonable date for the hard fork to be enacted
        * That requires hard fork initiation governance action to be submitted on \~10th November having 35 days for the full voting window and enactment epoch
        * That further requires that the 11.3 release candidate is ready no later than\~23rd October
        * It also assumes the 11.3 version to be perfect with no issues found, which would then be promoted to 12.0
          * Should there be a need for 11.4 version, 2026 timeline for Dijkstra hard fork enactment becomes impossible to achieve
        * According to Leios team, DBSync, Ogmios, Pallas have all been having an updated versions running on Musashi
          * Leios team emphasizes that the time for Leios testing is now, on Musashi network
    * Risks
      * [Dijkstra risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?gid=66373110#gid=66373110) (now including risks shared by IO) needs to be carefully managed, especially as there are few high scoring risks
        * Technical Steering Committee reviewed the risks and the findings will be shared with IO team and the Hard Fork Working Group
    * Protocol parameters and Constitutional amendments
      * Updating the constitution is still planned to happen before the hard fork
        * It needs to be submitted in the next 2 weeks in order to happen before the hard forkt enactment planned for December 2026
        * Scenario where consitution change is considered to happend after the hard fork enactment, parameters not being amendable is not the only way to disable Leios if needed
          * Disabling Leios could be achieved with removing sufficient level of SPOs BLS keys
        * Leios being active at the beginning of the Dijkstra era is aimed to be conservatively configured, perhaps only 2x for throughput
          * It would consider an iterative cycles of parameters graduation where once sure everything is working correctly, it would be followed by a parameter update to increase throughput a little bit more.&#x20;
          * Community voice would be respected in each of those iterative cycles, especially on the aspect of economic viability
      * For each of the milestone in the sequence until the end of 2026 there should be a targeted comms plan
    * Node diversity is already here
      * There was [**Cardano - Node diversity celebration day in Singapore (and online) - 6th October 26**](https://hackmd.io/@Amaru/DiversityCelebrationDraft) organized by Amaru team where each node team presented the state, value it brings to the community, plans for Q4 2026 and into 2027
        * Artifacts of the call will be shared later
        * Serves as a great starting point for another Node diversity workshop in London on 12th & 13th November organized by Amaru team
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
* [Recording](https://drive.google.com/file/d/1E8ASkxOrkusDVyugemff3qZopAjmuiG_/view?usp=drive_link)
* [Transcript](https://docs.google.com/document/d/1qb3bbBMKzGzsK37FC5egZ2SGpkgJ_ARlOZ2PeVI_2LY/edit?usp=drive_link)
* [Chat](https://drive.google.com/file/d/1dwFpkJhXpde0rtdz1hctQL0xf6bczWvA/view?usp=drive_link)

#### **Action items and next steps**

* **IO team:** Tag 11.2 version before the next HFWG call, 13th October
* **Amani/Leonard:** Specify decisions and Leios feature list within 11.3 by the end of this week and share it with the Hard Fork Working Group in the respective slack channel
* **Comms team:** Emphasize that the time for Leios testing is now, on Musashi Dojo
* **HFWG members:** Assess [Dijkstra risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?gid=66373110#gid=66373110), identify potential gaps and provide updates where necessary and/or applicable
* **Bosko:** Share [the review of the Leios Risk register](https://docs.google.com/document/d/1kvf8twFWhwsYtnLfjjgu7D3isJBTKdm3zXgre1PRfFo/edit?usp=sharing) with the HFWG, prepared by Technical Steering Committee member Leandros
* **Carlos/Kevin/TSC/PC:** Prepare new constitution governance action for submission in the next 2 weeks (\~21st October)
* **Matthew Capps/Larisa/Ian:** Prepare targeted comms plan for each milstone of the sequence until the end of 2026 (first of them being the new constitution)
* **Michiel/Elena/Bosko:** Determine HFWG wallet teams liaison(s) and finalize wallet teams outreach list
  *   **HFWG wallet teams liaison:** Reach out to Keystone, Ledger, Trezor, Bitbox (..?)

      and point them to the CDDL change of adding [`bls_key`](https://github.com/IntersectMBO/cardano-ledger/blob/2c33b4f858c0e62b300d121996a479f505d8c0e5/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L469)
* **Bosko:** Add Daniel Calatayud as editor to the [Dijkstra Hard Fork Risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?gid=66373110#gid=66373110)
* **Kevin/CIP expert(s):** Review and comment on this [PR](https://github.com/IntersectMBO/hf-wg-documentation/pull/43) that is raised to document impact of all changes being introduced in the Dijkstra era hard fork
* **Damien/Bosko:** Confirm the venue for the Node diversity workshop in London on 12th & 13th November
* **Bosko:** Create overall Dijkstra delivery timeline in Miro with the focus on dependencies so each HFWG participant/attendee and more broadly ecosystem, have clear view of the activities and milestones towards the DIjkstra era hard fork enactment
* **Elena/Bosko:** Check and cross-reference readiness approach being taken in previous hard forks with Chang, Plomin and beyond
