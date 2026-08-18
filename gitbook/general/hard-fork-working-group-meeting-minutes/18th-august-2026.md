# 18th August 2026

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/overview/hard-fork-working-group-meeting-minutes/11th-august-2026#action-items-and-next-steps) - Bosko
2. [Dijkstra era hard fork](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era/dijkstra-overview) - Bosko, all
   1. Scope
   2. Protocol parameters introduction and changes
   3. Constitutional amendments
   4. Readiness and Community engagement
   5. Comms
   6. Timing
   7. Node diversity
      1. Haskell, Amaru (Rust), Dingo (Go), Dugite (Rust), TSUNAGI (Zig), Gerolamo (TypeScript), Dolos (Rust), Turbocardano (C++), Razor (.NET), Scalus (Scala)
3. AOB

#### Key materials

* Summary
  * **Dijkstra Era hard fork**
    * Scope
      * Each CIP included in the next hard fork should have its impact assessment documented and available within this Cardano Upgrades space
      * There are no items, other than listed CIPs and/or already documented scope, that are merged to the codebase
        * Should there be a need, especially if its a P0 or P1 issue, IO team will notify the Hard Fork Working Group so those potential additional changes could be documented, their impact assessed and properly accounted for
    * Protocol parameters changes and Constitutional amendments
      * Carlos from IO team expressed next things that need to be resolved
        * Naming protocol parameters
        * Guardrails changes and definition
      * It was also mentioned once again, that the constitutional changes should happen before the hard fork
    * Readiness and Community engagement
      * Readiness tracker skeleton for Dijkstra was created a while ago and it still needs to be expanded to include more precise details and calculations on readiness
      * Constitutional updates needed for Dijkstra is Cardano community driven effort and its not meant to strip community away of any power
        * Hard fork can still happen even if the constitutional amendments arent ratified by the community prior to the hard fork
        * These constitutional changes are meant to be strictly and narrowly limited to certain technical changes when it comes to above mentioned protocol parameters
    * Comms
      * For the early community engagement it was deemed that the upgrade bulletin with all the latest items
    * Timing
      * IO team states that they are on track with the original plan and still running at risk
      * Jeff pointed out that the Haskell node teams are having an incredible pace, very committed to respect projected timeline of having a hard fork enacted in 2026
        * The biggest risk at the moment is having the node release candidate ready within the expected timeframe
      * Stability and quality of the release remains the top priority for IO teams without cutting corners
    * Current Cardano Governance
      * Ryan Cerkoryn called out low SPO engagement for the current Update COnstitutional Committee governance action
        * If not voted for, ratified and enacted, it can cause a stall in Cardano governance which would affect and likely affect hard fork timeline
    * Node diversity
      * Amaru team representative Damien stated that the team looked into the frozen scope of Dijkstra era hard fork and is expecting to have block producing ready node on mainnet before the hard fork is enacted with respecting the timeline communicated on hard fork working group meetings so far
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
* [Recording](https://drive.google.com/file/d/19Eq0gQJLpwxFht2vvqnf5MftayUQEX-r/view?usp=drive_link)
* [Transcript](https://docs.google.com/document/d/17DzfzecGMmeBk_l2QplmPaNwJDcvgT4X0FE06n_T_Ck/edit?usp=drive_link)
* [Chat](https://drive.google.com/file/d/1QSKVy5dKA0YrDnreVyGTzfqpCelbogHq/view?usp=drive_link)

#### **Action items and next steps**

* **Carlos:** Discuss upcoming constitutional and guardrails changes with parameter committee async or on the next call
* Larisa/Bosko: It should be underscored in comms pieces going out that the constitutional updates needed for Dijkstra is Cardano community driven effort and its not meant to strip community away of any power, but rather meant to be strictly and narrowly limited to certain technical changes
* **TSC/Kevin:** Add to TSC agenda and discuss outreach plan to help with the SPO engagament in Update Constitutional Committee governance action
* **Bosko:** Create overall Dijkstra delivery timeline in Miro so each HFWG participant/attendee and more broadly ecosystem, have clear view of the activities and milestones towards the DIjkstra era hard fork enactment
* **Bosko/Sebastian/Carlos:** Document impact on all changes being introduced in the Dijkstra era hard fork and reference it in the Cradano Upgrades GitBook space
* **Bosko:** Readiness tracker should be expanded to include more precise details and calculations on readiness
* **Elena/Bosko:** Check and cross-reference readiness approach being taken in previous hard forks with Chang, Plomin and beyond
* **Kevin/Sam L/Ryan C W/Damien:** Draft the decision making and prioritization process for future hard forks
