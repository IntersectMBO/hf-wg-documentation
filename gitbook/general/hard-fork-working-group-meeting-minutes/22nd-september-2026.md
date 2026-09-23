# 22nd September 2026

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/general/hard-fork-working-group-meeting-minutes/15th-september-2026#action-items-and-next-steps) - Bosko
2. [Dijkstra era hard fork](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era/dijkstra-overview) - Bosko, all
   1. Releases, readiness and community engagement - Sam, Jeff, Bosko
      1. [11.1.2](https://github.com/IntersectMBO/cardano-node/releases/tag/11.1.2)
      2. 11.1.3
      3. [11.2](https://github.com/IntersectMBO/cardano-node/issues/6672)
   2. Leios - Jeff, Kevin
      1. Security audit, hardware wallet upgrades and responsibility for any upgrade costs - Daniel
         * HFWG needs wallet teams liaison to address risk of delayed upgrade
   3. Scope and timing - Jeff, Bosko
      1. [IOLabs - Dijkstra Era Hard Fork](https://docs.google.com/document/d/1nVCzB8-l0fKpZLrQVrq9uLIkT69twuEaYHdf2fSEgOE/edit?tab=t.0#heading=h.blm90nnxn47g)
      2. [Technical risk log](https://drive.google.com/file/d/1MyBwgE-fI8lKMUYP_ctkHkchCPtXhB2X/view?usp=sharing) - IO shared with TSC
         * Anybody with the link has commenting access
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
      2. Dingo node team [achieved](https://x.com/InASingleWord/status/2097012520787771427?s=20) great milestone with having blocks produced on all Cardano networks
         * Preview
         * Preprod
         * Musashi
         * Prime Testnet
         * Cardano Mainnet
      3. Amaru [v10.11.20260918](https://github.com/pragma-org/amaru/releases/tag/v10.11.20260918) is out
         * [Milestones](https://github.com/pragma-org/amaru/milestones)
           * Minimum viable Block producer (pre-release) - 1st October
           * Block producer (beta-release) - 29th October
           * Block producer (Dijkstra Release) - 26th November
           * Block producer (Leios Release) - 26th November
      4. [Gerolamo produces blocks](https://x.com/MicheleHarmonic/status/2098671266290909505) on Cardano Preview testnet - 12th September
      5. [Scalus 1.2.0](https://github.com/scalus3/scalus/releases/tag/v1.2.0) - 17th September
         * generated validators smaller, ordered collections faster, and contract APIs safer
         * brings a self-contained Emulator and streaming blockchain APIs to JVM and JavaScript
      6. Haskell Cardano node in a web browser ([X post from Seungheon Oh](https://x.com/SeungheonO/status/2099326668284285421) - 14th September)
         * You can run full Haskell Cardano node in a web browser (running the ouroboros protocol and following the tip)
         * Balance and submit transaction fully on a browser
      7. Haskell, Amaru (Rust), Dingo (Go), Dugite (Rust), TSUNAGI (Zig), Gerolamo (TypeScript), Dolos (Rust), Turbocardano (C++), Razor (.NET), Scalus (Scala), Yano (Java)
3. Neutral naming process - Bosko
   1. [Draft open for feedback](https://docs.google.com/document/d/1RK2PEKAbvLtM4p7KWHNsdCEqN4OhZQEy/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true)
4. AOB

#### Key materials

* Summary
  * **Dijkstra Era hard fork**
    * Releases, readiness and community engagement
      * [11.1.2](https://github.com/IntersectMBO/cardano-node/releases/tag/11.1.2)
        * Released last week on 17th September
        * Optimizes memory usage in time lock scripts
        * Memory increase is under investigation
      * 11.1.3
        * Will act as a patch to address a storage issue related to IP addresses in the ledger state
        * It is expected later this week
      * [11.2](https://github.com/IntersectMBO/cardano-node/issues/6672)
        * It essentially brings everything (which includes new block format) but Leios from [the Dijkstra scope perspective](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview#phase-1-dijkstra-hard-fork-protocol-version-12-q4-2026)
          * Includes Plutus v4 context
        * Last week security fixes on 11.1 delayed work on version 11.2 for 1-2 weeks
        * This version **shouldnt** be considered of being capable to survive the hard fork event
    * Leios
      * Kevin H., chair of Technical Steering Committee, is still to respond to Daniel from IO in regars to questions over security audits
        * So far, there are no major concerns as long as the feedback from BeCryptic (which is doing the security audits) is shared with the Hard Fork Working Group
      * HFWG needs wallet teams liaison to address risk of delayed upgrade
    * Scope and timing
      * [Technical risk log](https://drive.google.com/file/d/1MyBwgE-fI8lKMUYP_ctkHkchCPtXhB2X/view?usp=sharing) that IO shared with TSC will be converted to spreadsheet file for easier maintenance and collaboration
        * technical risk log items are expected to contain github references
      * [Dijkstra Dependencies](https://drive.google.com/file/d/1VF9YavmkDiDkUCwzVzgv8_PwiZnt3-6F/view?usp=sharing) log should be used for collaboration
      * Each remaining scope item (besides CIP-23 and CIP-50 which are already documented) have its impact documented ([PR](https://github.com/IntersectMBO/hf-wg-documentation/pull/43) opened) in the [Cardano Upgrades space](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) (Core semantics changes, Breaking API changes, New features)
    * Protocol parameters and Constitutional amendments
      * Parameter Committee did an initial review of the updated Dijkstra parameters document shared by Carlos
        * Committee is writing notes that will be later discussed with IO teams
        * It appears that there will be \~100 new guardrails paramaters for Dijkstra and additional \~50 for Peras - changes are considered substantial
          * 1st level audit - security research input is needed
          * 2nd level audit - check the text of guardrails and open it for review
            * constitutional amendment process can be leveraged for it
        * Amaru team offered collaboration on guardrails testing
    * Node diversity
      * Several node teams are either:
        * producing blocks on mainnet (Haskell, Dingo) or
        * on the path to be producing blocks on mainnet (Amaru, Gerolamo)
      * One of the key topics for node diversity workshop in London on 12th & 13th November (venue is yet to be confirmed) will be conformance of any node
      * Node diversity will additionaly be discussed in the upcoming Security Council meeting
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
* [Recording](https://drive.google.com/file/d/1mt7zmajl49QCU7eA8f8dEp0DFzaCn7PD/view?usp=drive_link)
* [Transcript](https://docs.google.com/document/d/1QmheXQiXszXbjC_HwKNVyZI0ROSBohvcqtX_dALUjOU/edit?usp=drive_link)
* [Chat](https://drive.google.com/file/d/1Dw-7aS8WOQzoiF3yAdzkbiWjmXqjSf8X/view?usp=drive_link)

#### **Action items and next steps**

* **Bosko:** Create overall Dijkstra delivery timeline in Miro with the focus on dependencies so each HFWG participant/attendee and more broadly ecosystem, have clear view of the activities and milestones towards the DIjkstra era hard fork enactment
* **Michiel/Elena/Bosko:** Determine HFWG wallet teams liaison
  *   **HFWG wallet teams liaison:** Reach out to Keystone, Ledger, Trezor, Bitbox (..?)

      and point them to the CDDL change of adding [`bls_key`](https://github.com/IntersectMBO/cardano-ledger/blob/2c33b4f858c0e62b300d121996a479f505d8c0e5/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L469)
* **Daniel/Amani/Bosko:** Convert Leios technical risk log to more easily maintainable spreadsheet file where anyone with the link has commenting permissions
* **Parameter Committee:** Provide feedback on the [updated list of Dijkstra parameters](https://hackmd.io/@eJKr9l7wQ6aU2PgNdrfgZg/Dijktstra-parameters) to IO
  * Consider including Amaru team in the guardrails testing
* **All:** Review and comment on this [PR](https://github.com/IntersectMBO/hf-wg-documentation/pull/43) that is raised to document impact on all changes being introduced in the Dijkstra era hard fork
* **Damien/Bosko:** Confirm the venue for the Node diversity workshop in London on 12th & 13th November
* **Jeff:** Provide major release notes on node starting with version 11.2 which would help with early readiness assessment and integration planning by downstream tooling
* **Elena/Bosko:** Check and cross-reference readiness approach being taken in previous hard forks with Chang, Plomin and beyond

