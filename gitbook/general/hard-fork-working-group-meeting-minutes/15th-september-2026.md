# 15th September 2026

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/general/hard-fork-working-group-meeting-minutes/8th-september-2026#action-items-and-next-steps) - Bosko
2. [Dijkstra era hard fork](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era/dijkstra-overview) - Bosko, all
   1. Releases, readiness and community engagement - Sam, Jeff, Bosko
      1. 11.1.1
      2. 11.2
   2. Leios - Jeff, Kevin
      1. New committee approach and preserving security requirements? LL security guarantee
      2. Security audit and formal conformance against the specification (not the CIP)
      3. Hardware wallet upgrades
         1. Responsibility for any upgrade costs
   3. Scope and timing - Jeff, Bosko
      1. [IOLabs - Dijkstra Era Hard Fork](https://docs.google.com/document/d/1nVCzB8-l0fKpZLrQVrq9uLIkT69twuEaYHdf2fSEgOE/edit?tab=t.0#heading=h.blm90nnxn47g)
      2. Technical risk log - Kevin, IO
      3. [Dijkstra Dependencies](https://drive.google.com/file/d/1VF9YavmkDiDkUCwzVzgv8_PwiZnt3-6F/view?usp=sharing) and gating
      4. Each remaining scope item (besides CIP-23 and CIP-50 which are already documented) have its impact documented ([PR](https://github.com/IntersectMBO/hf-wg-documentation/pull/43) opened) in the [Cardano Upgrades space](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) (Core semantics changes, Breaking API changes, New features)
   4. Protocol parameters and constitutional amendments
      1. [Updated list of Dijkstra parameters](https://hackmd.io/@eJKr9l7wQ6aU2PgNdrfgZg/Dijktstra-parameters) was shared with the Parameter Committee on Thursday, 10th September
   5. Comms
      1.
   6. Node diversity
      1. Node diversity celebration day in Singapore & Online - organized by Amaru team
         * [Announcement](https://x.com/Amaru_Cardano/status/2095090242357240201)
         * [Content and agenda](https://hackmd.io/@Amaru/DiversityCelebrationDraft) (can be modified)
      2. Dingo node team is [making significant progress](https://x.com/InASingleWord/status/2097012520787771427?s=20) and continues to build momentum
         * Last week, Dingo by Blink labs is the [#1 most active Cardano repo with the highest number of commits](https://cardanoupdates.koios.rest/)
      3. Haskell Cardano node in a web browser ([X post from Seungheon Oh](https://x.com/SeungheonO/status/2099326668284285421))
         * You can run full Haskell Cardano node in a web browser (running the ouroboros protocol and following the tip)
         * Balance and submit transaction fully on a browser
      4. Haskell, Amaru (Rust), Dingo (Go), Dugite (Rust), TSUNAGI (Zig), Gerolamo (TypeScript), Dolos (Rust), Turbocardano (C++), Razor (.NET), Scalus (Scala), Yano (Java)
3. AOB

#### Key materials

* Summary
  * **Dijkstra Era hard fork**
    * Releases, readiness and community engagement
      * [11.1.1](https://github.com/IntersectMBO/cardano-node/releases/tag/11.1.1)
        * [11.1.1](https://github.com/IntersectMBO/cardano-node/releases/tag/11.1.1) ~~is expected to be released soon~~
          * released between the end of the meeting and finalizing notes
        * It will be mainnet ready
        * brings small improvements
        * removes legacy tracing system
      * 11.2
        * Integration is already underway and is expected to be completed in the 2 weeks, at which point will be pre-released
        * Roughly one week after pre-release it is expected to be released
        * It essentially brings everything (which includes new block format) but Leios from [the Dijkstra scope perspective](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview#phase-1-dijkstra-hard-fork-protocol-version-12-q4-2026)
        * This version **shouldnt** be considered of being capable to survive the hard fork event
        * It will enable early DIjkstra testing and will unlock beginning of downstream tooling integration against the specified feature set
        * DijkstraNet testnet will start with pv11 and will be forked to pv12 (again, without Leios)
    * Leios
      * Kevin raised few questions to IO on behalf of the Technical Steering Committee
        1. Do we have confirmation from the security researchers that the new committee approach preserves security requirements?  If not, do any adjustments need to be made to the LL security guarantee (eg thresholds)
        2. What, if any, security audit is being done (protocol level or code level - general audits are expensive and not useful). What, if any., formal conformance is being done against the specification. (not the CIP).
        3. Do we need hardware wallet upgrades (I assume yes). If so, have the relevant vendors been contacted yet, and who is responsible for any upgrade costs (IO has paid these in the past but I know at least one vendor applied for treasury funding this year)
      * Daniel and Amani from IO will provide feedback on security audits
      * Hardware Wallets need upgrade due to a number of reasons
        * There are supposedly SPOs that have their cold keys stored on hardware wallets.
          * With Leios, there is a need for SPOs to sign pool registration certificates with their HW wallet
          * The pool registration certificate has changed for Leios to register BLS keys (in a backward compatible way)
          * As many as possible HW wallets need to support this workflow for highest participation in Leios voting
        * HFWG needs wallet teams liaison to address risk of delayed upgrade
        * Some of those projects already have Treasury Funding, if required\* additional spend is needed, Tooling Sustainability program is still available until the end of 2026. (Need to apply before Thanksgiving)
          * [Tooling Sustainability Project Intake Form](https://forms.clickup.com/9015279944/f/8cnmga8-37315/O6P6T73ETVLHJY9C6D)
      * [Recent showcase of the Leios prototype](https://x.com/carloslodelar/status/2099763976561181130) by Sebastian and Carlos
        * Leios node peaking at 250 TxkB/s (\~1,000 simple 250-byte transactions per second) on a local cluster with emulated round trip times for higher fidelity.
        * Mainnet today tops out at 4.5 TxkB/s.
        * The work ahead sits in the network stack, where tuning and optimisation carry these numb
    * Scope and timing
      * The goal stays the same, Dijkstra era hard fork enactment in 2026
      * Dijkstra scope can always be referenced from [Dijkstra overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) page
      * Technical risk log from IO will be shared with the HFWG
      * Kevin explained the importance of [Dijkstra Dependencies](https://drive.google.com/file/d/1VF9YavmkDiDkUCwzVzgv8_PwiZnt3-6F/view?usp=sharing) list that include more dependencies than the ones that exists in IO Dijkstra delivery plan
        * That list should contain critical path tooling and items as well
        * In order to avoid any misalignment in ambiguity, IO, TSC, HFWG and the whole community can use [Dijkstra Dependencies](https://drive.google.com/file/d/1VF9YavmkDiDkUCwzVzgv8_PwiZnt3-6F/view?usp=sharing) list as a reference and provide any comment there in a genuine collaborative effort (anybody with the link has commenting access)
      * Each remaining scope item (besides CIP-23 and CIP-50 which are already documented) have its impact documented ([PR](https://github.com/IntersectMBO/hf-wg-documentation/pull/43) opened) in the [Cardano Upgrades space](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) (Core semantics changes, Breaking API changes, New features) and all experts from the HFWG can be invited to review and comment on this [PR](https://github.com/IntersectMBO/hf-wg-documentation/pull/43)
    * Protocol parameters and Constitutional amendments
      * [Updated list of Dijkstra parameters](https://hackmd.io/@eJKr9l7wQ6aU2PgNdrfgZg/Dijktstra-parameters) was shared with the Parameter Committee on Thursday, 10th September
      * After they are confirmed and finalized, the parameters will be part of 11.2 release with some initial values
      * With the release of version 11.3 which is the first one to contain all Dijkstra features, including linear Leios, sensible guardrails can be assessed and defined
    * Comms
      * Comms team's focus continues to be to move away from simply relaying the HFWG outputs in the Intersect Upgrade Bulletin and Weekly Update, to a more action-oriented "here is the news and what each ecosystem category can start to do to be prepared" approach
    * Node diversity
      * Node diversity celebration day in Singapore & Online - organized by Amaru team
        * [Announcement](https://x.com/Amaru_Cardano/status/2095090242357240201)
        * [Content and agenda](https://hackmd.io/@Amaru/DiversityCelebrationDraft) (can be modified)
      * Node diversity workshop, organized by Amaru team, will happen in London on 12th & 13th November with the venue that is yet to be confirmed
      * Dingo node team achieved great milestone with having blocks produced on all Cardano networks&#x20;
        * Preview
        * Preprod
        * Musashi
        * Prime Testnet
        * Cardano Mainnet
      * Amaru [v10.11.20260912](https://github.com/pragma-org/amaru/releases/tag/v10.11.20260912) is out
        * Full duplex connections
        * Better peer management
        * Improved block fetching
        * Important fixes w.r.t governance
      * Haskell Cardano node in a web browser ([X post from Seungheon Oh](https://x.com/SeungheonO/status/2099326668284285421))
        * Full Haskell Cardano node can be run in a web browser (running the ouroboros protocol and following the tip)
        * Balance and submit transaction fully in a browser
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
* [Recording](https://drive.google.com/file/d/1QiMipI-wjVBoJguHVycH2THPuSlXzkHd/view?usp=drive_link)
* [Transcript](https://docs.google.com/document/d/1SPzG7naLnA_z_j-WoGMlkZo2kLfQB-gmqCsvrAad8EY/edit?usp=drive_link)
* [Chat](https://drive.google.com/file/d/11cxslM3LZvVmT1uRCUaGHLrkWbebUA05/view?usp=drive_link)

#### **Action items and next steps**

* **All:** Review and comment on this [PR](https://github.com/IntersectMBO/hf-wg-documentation/pull/43) that is raised to document impact on all changes being introduced in the Dijkstra era hard fork
* **Bosko:** Create overall Dijkstra delivery timeline in Miro with the focus on dependencies so each HFWG participant/attendee and more broadly ecosystem, have clear view of the activities and milestones towards the DIjkstra era hard fork enactment
* **Daniel/Amani:** Provide feedback on security audits for Leios based on three questions asked by Kevin on behalf of Technical Steering Committee
*   **Carlos/Sebastian/Ryan Cerkoryn/HFWG:** Reach out to Keystone, Ledger, Trezor, Bitbox (..?)

    and point them to the CDDL change of adding [`bls_key`](https://github.com/IntersectMBO/cardano-ledger/blob/2c33b4f858c0e62b300d121996a479f505d8c0e5/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L469)
* **Daniel/Jeff:** Share the technical risk log from IO with the HFWG
* **TSC/IO/All:** Collaborate on [Dijkstra dependencies](https://docs.google.com/spreadsheets/d/1meEMAMLaAiSaR4DkhmXz5LpGgFlnX_vTBPMV-vGmEzk/edit?usp=sharing) to identify gaps and achieve common understanding and wider alignment (it should include critical path tooling)
* **Carlos/Bosko:** Confirm whether Peras parameters are part of the [updated list of Dijkstra parameters](https://hackmd.io/@eJKr9l7wQ6aU2PgNdrfgZg/Dijktstra-parameters)&#x20;
* **Parameter Committee:** Provide feedback on the [updated list of Dijkstra parameters](https://hackmd.io/@eJKr9l7wQ6aU2PgNdrfgZg/Dijktstra-parameters) to IO
* **Damien/Bosko:** Confirm the venue for the Node diversity workshop in London on 12th & 13th November
* **Bosko/all:** Start the neutral naming process for the hard fork async
* **Jeff:** Provide major release notes on node starting with version 11.2 which would help with early readiness assessment and integration planning by downstream tooling
* **Elena/Bosko:** Check and cross-reference readiness approach being taken in previous hard forks with Chang, Plomin and beyond
* **Kevin/Sam L/Ryan C W/Damien:** Draft the decision making and prioritization process for future hard forks
