# 11th August 2026

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/overview/hard-fork-working-group-meeting-minutes/4th-august-2026#action-items-and-next-steps) - Bosko
2. [Dijkstra era hard fork](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era/dijkstra-overview) - Bosko, all
   1. Scope
      1. IO Team presented their plan - [Dijkstra Era Hard Fork: Delivery Plan](https://docs.google.com/document/d/1nVCzB8-l0fKpZLrQVrq9uLIkT69twuEaYHdf2fSEgOE/edit?usp=sharing)
      2. [Product committee - Dijkstra Era: Phased Rollout Plan](https://product.cardano.intersectmbo.org/hardfork-planning/dijkstra/)
   2. Constitutional amendments and the CAP process
      1. [CAP (Constitutional Ammendment Portal)](https://cap.intersectmbo.org/)
         * [Guides](https://cap.intersectmbo.org/#/guides)
         * [Introduction to CAPs and CISs](https://cap.intersectmbo.org/#/guides/intro-to-caps-and-cis)
           * Constitutional Amendment Proposals (**CAPs**)
           * Constitutional Issue Statements (**CISs**)
   3. Node diversity
      1. Amaru
         * Relay capable of doing validation and syncing to the tip
         * Block production is expected come in 6 to 7 weeks
      2. Haskell, Amaru (Rust), Dingo (Go), Dugite (Rust), TSUNAGI (Zig), Gerolamo (TypeScript), Dolos (Rust), Turbocardano (C++), Razor (.NET), Scalus (Scala)
3. AOB

#### Key materials

* Summary
  * **Dijkstra Era hard fork**
    * Scope & Timing
      * IO Labs Jeff shared the official update async
        * Scope has not changed
        * Dates have not changed
        * Comms are being aligned between Intersect and IO - Jenna and Ian
      * Bootstrapping phase needs to be accounted for in the timelines as Leios becomes activated only after the hard fork is enacted and sufficient number of BLS keys have been registered
      * Overall timeline should be created in Miro so each HFWG participant/attendee and more broadly ecosystem, have clear view of the activities and milestones towards the DIjkstra era hard fork enactment
    * Node Diversity
      * Amaru
        * Team representative, Damien Czapla, shared updates and clarified Amaru node status as currently being relay capable of doing validation and syncing to the tip
          * When it comes to block producing on mainnet, they expect to be ready in November 2026
        * The team will analyze the scope of Dijkstra era hard fork and share their roadmap and plans afterwards
        * It was pointed out that the changes, especially breaking ones, need to be documented reasonably well which would make ecosystem & community adoption a smoother experience with lessons learned from van Rossem hard fork effort
      * There was a specific discussion point on scope items impact potentially being discussed through GitHub as a communication tool, at least initially
        * Sebastian from Leios team shared the initial reading material from a leios perspective: [https://github.com/input-output-hk/ouroboros-leios/blob/main/docs/ImpactAnalysis.md](https://github.com/input-output-hk/ouroboros-leios/blob/main/docs/ImpactAnalysis.md)
          * It will be added/referenced as a resource to the Cardano Upgrades GitBook space
      * Other alternative nodes
        * Although all other mapped alternative node teams representatives have been invited to the hfwg meetings, Damien from Amaru team offered to reiterate values and the discussion points with other teams and invite them to the hfwg calls
        * Hard Fork Working Group welcomes any alternative node team as equal to these discussions that benefit the whole Cardano ecosystem
    * Readiness
      * [Dijkstra readiness skeleton tracker](https://docs.google.com/spreadsheets/d/1C1Ai_YTqwKLHtICunzbh_o0FD9XB54Kh/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true) has been created by Intersect which will be expanded to include more precise details and calculations on readiness, especially on the testnets readiness is being reported against by the community teams listed
      * Adam pointed out that there is valuable experience from past hard forks which can be leveraged for community teams taking responsibility to report readiness themselves by raising respective PRs in GitHub repo
      * Damien Czapla from Amaru team shared updates on [Antithesis](https://cardanofoundation.org/blog/improving-cardano-antithesis) and improving Cardano testing with it
        * Antithesis is a testing platform combining:
          1. a _deterministic hypervisor_ that can run nearly arbitrary pieces of software, emulating the full complexity of the underlying operating system and [network](https://cardanofoundation.org/glossary?search=Network), including the ability to simulate the passing of time;
          2. _property-based testing_ and _fuzzing_ to deterministically generate complex test scenarios and check observable properties of the system-under-test, with the ability to _reproduce_ failures;
          3. analysis and reporting tools to help troubleshoot issues signaled by test runs.
  * Constitutional amendments and the CAP process
    * Constitutional amendments related to DIjkstra era hard fork now have a natural place for discussion, followed with submission and enactment
    * The newly established process with [the designated CAP portal](https://cap.intersectmbo.org/) is created and supported by the Civics Committee, [giving Cardano's Constitution a way to grow](https://intersectmbo.org/news/the-constitutional-amendment-portal-giving-cardanos-constitution-a-way-to-grow)
  * Decision making and prioritization process for future hard forks
    * Amaru team would like to participate in the process shaping along with another alternative node teams
  * Hard Fork Working Group will continue to meet once a week until the Dijkstra era hard fork work solidifies enough to mandate more alignments and sync

#### **Reference links and engagement points**

* Hard Fork Working Group communication channels
  * [Discord](https://discord.com/channels/1136727663583698984/1242097284619960411) — `#wg-hard-fork`
  * [Weekly bulletins](https://x.com/IntersectMBO) (url edited)
  * [Luma calendar](https://luma.com/calendar/cal-TMjYNpSY4huYYif)
  * [Email](mailto:hard-fork@intersectmbo.org)
* [Product committee - Dijkstra Era: Phased Rollout Plan](https://product.cardano.intersectmbo.org/hardfork-planning/dijkstra/)
* [Leios impact analysis](https://github.com/input-output-hk/ouroboros-leios/blob/main/docs/ImpactAnalysis.md)
* [CAP (Constitutional Ammendment Portal)](https://cap.intersectmbo.org/)
  * [Guides](https://cap.intersectmbo.org/#/guides)
  * [Introduction to CAPs and CISs](https://cap.intersectmbo.org/#/guides/intro-to-caps-and-cis)
* [Antithesis](https://cardanofoundation.org/blog/improving-cardano-antithesis)
* [Recording](https://drive.google.com/file/d/1nDGQkHvwNMBkO5yBjzzSObI5IidNW1_Q/view?usp=drive_link)
* [Transcript](https://docs.google.com/document/d/13B9pNTwdJNJrkMWod-kQBfPAcd_IZZBmRjEGpnHdBms/edit?usp=drive_link)
* [Chat](https://drive.google.com/file/d/1fA5YKt0i8SoONFt7Gfahzui3nbHtfaaL/view?usp=drive_link)

#### **Action items and next steps**

* **Bosko:** Create overall Dijkstra delivery timeline in Miro so each HFWG participant/attendee and more broadly ecosystem, have clear view of the activities and milestones towards the DIjkstra era hard fork enactment
* **Bosko/Sebastian/Carlos:** Document impact on all changes being introduced in the Dijkstra era hard fork and reference it in the Cradano Upgrades GitBook space
* **Bosko:** [**Dijkstra Era: Phased Rollout plan**](https://product.cardano.intersectmbo.org/hardfork-planning/dijkstra/) should be moved to [Cardano Upgrades space](https://cardanoupgrades.docs.intersectmbo.org/) along with introducing more feedback based updates (readiness reporting and impact analysis)
* **Carlos:** Attend the next parameter committee call to further discuss the impact on constitution and parameters for the Dijkstra era hard fork
* **Damien:** Reiterate values and the discussion points with other alternative node teams and invite them to the hard fork working group calls
* **Bosko:** Readiness tracker should be expanded to include more precise details and calculations on readiness
* **Elena/Bosko:** Check and cross-reference readiness approach being taken in previous hard forks with Chang, Plomin and beyond
* **Kevin/Sam L/Ryan C W/Damien:** Draft the decision making and prioritization process for future hard forks
