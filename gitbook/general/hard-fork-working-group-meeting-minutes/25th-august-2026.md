# 25th August 2026

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/general/hard-fork-working-group-meeting-minutes/18th-august-2026#action-items-and-next-steps) - Bosko
2. [Dijkstra era hard fork](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era/dijkstra-overview) - Bosko, all
   1. Scope and timing
      1. [Google doc from IO is now properly versioned](https://docs.google.com/document/d/1nVCzB8-l0fKpZLrQVrq9uLIkT69twuEaYHdf2fSEgOE/edit?tab=t.0#heading=h.blm90nnxn47g)
      2. Scope stays the same as communicated before
      3. Next milestone is **Feature complete at component level**, by the end of August
      4. The aim is to have each scope item having its impact documented in the [Cardano Upgrades space](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) (Core semantics changes, Breaking API changes, New features)
   2. Protocol parameters and constitutional amendments
      1. Parameter names are yet to be defined (\~2 weeks away)
      2. Dijkstra era hard fork bring new parameters not only for Leios, but for other scope items too and all need to be addressed as all should be included in the constitutional amendments
      3. There is an upcoming discussion this Friday on constitutional amendments related to Dijkstra governance and tech domain experts
   3. Readiness and Community engagement
      1. CDDL is expected to be completed in the next 3 weeks
      2. DBSync changes are following Dijkstra scope already, work is happening in parallel and soon after the node is marked as hard fork ready, DBSync will be too
      3. The above will unlock progress on engagement
   4. Comms
      1. The main focus of the comms teams remain Update Constitutional Committee governance action and low SPO engagement
         * If the action doesnt pass, governance on Cardano stalls
   5. Naming
      1. Metadata is being prepared for the submission of naming info action
         * Aiming to be submitted in epoch 654 (starts 6th September)
         * Based on [the hfwg call motion on 23rd July](https://cardanoupgrades.docs.intersectmbo.org/general/hard-fork-working-group-meeting-minutes/23rd-july-2026#key-materials), hfwg is proposing to name the hard fork after **Alexander Esgen**, with adding In Memoriam section to eternalize others who sadly passed away in recent months/years
           * **Fabian von Bergen** - there is the [info action](https://cardanoscan.io/govAction/gov_action1fzatpjn3e3r09mjzzfptznef9wxg8q4a5uraq04xvfjyhmfzhzfsqqgfc9h) that expired
             * 61.28% DReps, 4.31% SPOs, 3 No and 1 Abstain CC)
           * **Steven Lupien**
           * **Gregg Morgan** aka [@bone\_pool](https://x.com/bone_pool)
           * **Sean Davies**
         * Any hfwg or other community member is invited to provide more details on the members who passed away in order to have the memory of their lives and impact eternal
   6. Node diversity
      1. Amaru
         * Team is expecting to have Praos block producing ready node on mainnet by the end of 2026 and is unwrapping other items in the scope
         * 2 upcoming node diversity events
           * One around Token2049 on the 6th October (online event with a small cohort offline in Singapore)
           * 12th + 13th November node diversity workshop in London
      2. Haskell, Amaru (Rust), Dingo (Go), Dugite (Rust), TSUNAGI (Zig), Gerolamo (TypeScript), Dolos (Rust), Turbocardano (C++), Razor (.NET), Scalus (Scala), Yano (Java)
3. AOB

#### Key materials

* Summary
  * First part of the meeting wasnt properly recorded, but the structured meeting notes below cover the meeting in its entirety
    * Partial recording, transcript and chat are available [below](https://cardanoupgrades.docs.intersectmbo.org/general/hard-fork-working-group-meeting-minutes/25th-august-2026#reference-links-and-engagement-points)
  * **Dijkstra Era hard fork**
    * Scope and timing
      * Adding ledger interface for plutus v4 will be part of version 11.2
        * It is expected to happen in the next 2 weeks
      * 11.2 should not be considered as the hard fork ready version, rather one that gives insight into Dijkstra and some early testing of its capabilities
      * 11.3 version which is considered to be feature complete was expected to be completed by the end of August
      * Based on the above, the delivery timeline should be adjusted and is yet to be determined to which extent
    * Protocol parameters and Constitutional amendments
      * TSC perspective
        * Protocol parameters need to be confirmed (expected in node 11.2)
        * Discussion of guardrails can commence with the parameter committee once parameters are sufficiently fixed
      * Dijkstra era hard fork bring new parameters not only for Leios, but for other scope items too and all need to be addressed as all should be included in the constitutional amendments
      * There is an upcoming discussion this Friday on constitutional amendments related to Dijkstra governance and tech domain experts
      * Parameters Committee needs one week for proper review of confirmed DIjkstra era hard fork parameters
    * Readiness and Community engagement
      * CDDL is expected to be completed in the next 3 weeks
      * DBSync changes are following Dijkstra scope already, work is happening in parallel and soon after the node is marked as hard fork ready, DBSync will be too
      * The above will unlock progress on engagement
    * Comms
      * The main focus of the comms teams remain Update Constitutional Committee governance action and low SPO engagement
        * If the action doesnt pass, governance on Cardano stalls
    * Naming
      * Metadata is being prepared for the submission of naming info action
        * It doesnt need to be overly descriptive, but it needs to cover the social aspect of it sufficiently
        * More detailed bios of the people considered so far, for the name and in memoriam section, will be added to the hard fork initiation governance action in due time
      * Aiming to be submitted in epoch 654 (starts 6th September)
      * Based on [the hfwg call motion on 23rd July](https://cardanoupgrades.docs.intersectmbo.org/general/hard-fork-working-group-meeting-minutes/23rd-july-2026#key-materials), hfwg is proposing to name the hard fork after **Alexander Esgen**, with adding In Memoriam section to eternalize others who sadly passed away in recent months/years
      * Hard Fork Working Group should take naming process into consideration for future hard forks with the aim to have it defined, transparent and widely communicated
        * It could mean adjusting the hard fork submission policy as the current one has nothing specified on how hard forks should be named
    * Node diversity
      * Amaru team expectation for Q4 2026 is to be able to produce a first block on mainnet, work on conformance (collaborating with Alex Sierkov from Turbocardano), performances and robustness
        * Block production node release (Target): September 29th start with a pre-release, have a beta \~4 weeks after
        * Q3 2026 goal is achieved - Release a robust relay node binary ([version 10.11.20260820^beta](https://github.com/pragma-org/amaru/releases/tag/v10.11.20260820))
        * Diversity “celebration day” in Singapore: 6th October
          * Attendees: Every node implementation leader
          * Purpose: Get a look at all the implementation timelines
        * Node diversity workshop in London: 12th & 13th November
          * Attendees: Node implementation teams; SPOs; Hard fork decision makers
          * Purpose: Decide on the cost-efficient approach for Cardano network upgrades
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
* [CAP (Constitutional Ammendment Portal)](https://cap.intersectmbo.org/)
  * [Guides](https://cap.intersectmbo.org/#/guides)
  * [Introduction to CAPs and CISs](https://cap.intersectmbo.org/#/guides/intro-to-caps-and-cis)
* [Antithesis](https://cardanofoundation.org/blog/improving-cardano-antithesis)
* [Recording](https://drive.google.com/file/d/1Z0IwnHBS-7o-n2o6ShcVb58rzF-nOmIo/view?usp=drive_link)
* [Transcript](https://docs.google.com/document/d/172-g-7sG3vC98jr82uMDnmHI9sjWA5qpC_-jBc1Q2wo/edit?usp=drive_link)
* [Chat](https://drive.google.com/file/d/1MmxMx0V4D-Zb-B75x6_oDaJFRtwYAlLN/view?usp=drive_link)

{% file src="../../.gitbook/assets/2026_08_25_Amaru_Events.pdf" %}

#### **Action items and next steps**

* **Bosko:** Confirm the timeline(s), different confidence levels plans with Jeff from IO
* **Bosko:** Create overall Dijkstra delivery timeline in Miro so each HFWG participant/attendee and more broadly ecosystem, have clear view of the activities and milestones towards the DIjkstra era hard fork enactment
* **Carlos/Sebastian/Jeff:** Confirm the list of Dijkstra era hard fork protocol parameters to the Parameter Committee as discussion of guardrails can commence with the parameter committee once parameters are sufficiently fixed
* **Bosko:** Finalize v1 of Dijkstra readiness tracker (includes readiness reported against different networks) to apply correct and precise readiness calculations in it
* **Bosko/Sebastian/Carlos:** Document impact on all changes being introduced in the Dijkstra era hard fork and reference it in the Cradano Upgrades GitBook space
* **Elena/Bosko:** Check and cross-reference readiness approach being taken in previous hard forks with Chang, Plomin and beyond
* **Elena:** Prepare hard fork naming info action metadata in order to be reviewed by the hard fork working group, technical steering committee and civics committee
* **Elena/Bosko:** Collect the relevant bios of the people considered so far, for the name and in memoriam section, so those can be added to the hard fork initiation governance action in due time
* **Kevin/Sam L/Ryan C W/Damien:** Draft the decision making and prioritization process for future hard forks
