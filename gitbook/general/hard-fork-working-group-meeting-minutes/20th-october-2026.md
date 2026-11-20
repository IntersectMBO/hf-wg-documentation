# 20th October 2026

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/general/hard-fork-working-group-meeting-minutes/13th-october-2026#action-items-and-next-steps) - Bosko
2. [Dijkstra era hard fork](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era/dijkstra-overview) - Bosko, all
   1. Releases
      1. [11.2](https://github.com/IntersectMBO/cardano-node/issues/6672) - Jeff, Amani, Sam
      2. 11.3 - Sebastian
         * [Rc 2026w42 pre-release](https://github.com/input-output-hk/ouroboros-leios/releases/tag/rc-2026w42)
      3. [Project view of versions](https://github.com/orgs/input-output-hk/projects/167/views/15)
   2. Scope
      1. [CIP-23](https://cips.cardano.org/cip/CIP-23) - Jeff, Leonard, Amani
      2. Each remaining scope item (besides CIP-23 and CIP-50 which are already documented) have its impact documented ([PR](https://github.com/IntersectMBO/hf-wg-documentation/pull/43) opened) in the [Cardano Upgrades space](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) (Core semantics changes, Breaking API changes, New features)
         * [Updated Leios impact assessment available for feedback](https://drive.google.com/file/d/1GJNMixEGb6-jEOh8Yy_p2N--cPPz1Jh6/view?usp=sharing) (passed from TSC to original authors)
   3. [Dijkstra risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?gid=66373110#gid=66373110) review
   4. Constitutional amendments - [Dijkstra era parameters in CAP](https://cap.intersectmbo.org/#/detail/12)
      1. Dijkstra Rollout - Constitutional update and guardrails - Friday 23rd October, 2pm UTC
         * [meeting link](https://meet.google.com/bqd-dpyz-nrt)
         * Will be recorded and shared afterwards
         * Open for CC members, SPOs and DReps too
   5. Comms - Ian, Matthew
      1. [Leios Rollout Journey](https://docs.google.com/document/d/1J-ceP1gaKBd4drRTPI6C4r_3acaevg6XcZFfOTKBkqE/edit?tab=t.0#heading=h.r2inwd4eretc) (prepared by Matthew Capps)
   6. Node diversity
      1. Node diversity workshop in London, **12th&13th November** organized by Amaru team
         * London Marriott Hotel Canary Wharf\
           Address: 22 Hertsmere Rd, London E14 4ED, United Kingdom
         * [Working agenda](https://hackmd.io/0b_HvF4AS-q4wayJP6M25A)
      2. [Dingo](https://x.com/blinklabs_io/status/2110670354100187359?s=20)
         * Capable of forging blocks across all Cardano networks (Preview, Preprod, Mainnet, Musashi)
         * Is not only a block producer and with API mode enabled it gets you Blockfrost, Kupo, Mesh/Rosetta, and UTxO RPC APIs
      3. Haskell, Amaru (Rust), Dingo (Go), Dugite (Rust), TSUNAGI (Zig), Gerolamo (TypeScript), Dolos (Rust), Turbocardano (C++), Razor (.NET), Scalus (Scala), Yano (Java)
3. Time of the HFWG call starting next week - 2:30pm UTC
4. Hard Fork Working Group funding (Technical Steering Committee budget)
5. AOB

#### Key materials

* Summary
  * **Dijkstra Era hard fork**
    * Releases
      * 11.2
        * In progress, tagged version expected this week
        * Once available it will be used to respun DijkstraNet into the Conway era which will soon after be forked into the Dijkstra era
        * This version includes the full feature set of Dijkstra era hard fork scope except Leios
        * It is also expected to bring several other capabilities to mainnet, most notably availability of LSM
          * Requirements with the use of LSM are expected to be \~12GB
          * SPO Chris STR8 confirmed he will test LSM and provide feedback
      * 11.3
        * In progress, with a lot of work that remains to be done
        * It is at least 2 weeks away of being tagged as a version
        * Current weekly version, [Rc 2026w42 pre-release](https://github.com/input-output-hk/ouroboros-leios/releases/tag/rc-2026w42), is considered to be Leios based prototype which now contains the full feature set of DIjkstra era hard fork scope including Leios
          * This version can serve as an early downstream tooling integration point that gives insight into the Dijkstra era on Musashi testnet
        * [BLS key rotation](https://github.com/input-output-hk/ouroboros-leios/issues/1024)
          * using the `pool_registration_cert` in a transaction requires not only a signature matching the pool id (cold key), **but also witnesses for all `pool_owners`**&#x20;
          * There should not be a requiremenet from pool owners to do BLS key registration and rotation
          * Two potential solutions are being discussed [here](https://github.com/input-output-hk/ouroboros-leios/issues/1024#issuecomment-6285711848):
            * Introduce a new, dedicated cert about BLS key registration and rotation
            * Allow to update BLS keys in the pool params without owner signature, which is likely the one to be implemented for Dijkstra era, with proper solution deferred to Euler era
              * Full Cardano ledger team rationale available [here](https://github.com/IntersectMBO/cardano-ledger/issues/6198#issuecomment-6300201087), in the respective repo [GitHub issue](https://github.com/IntersectMBO/cardano-ledger/issues/6198)
    * Scope
      * CIP-23 is confirmed to be fully included in the Dijkstra era hard fork scope
      * [Updated Leios impact assessment](https://drive.google.com/file/d/1GJNMixEGb6-jEOh8Yy_p2N--cPPz1Jh6/view?usp=sharing), which was passed from TSC to original authors, will be merged to the Cardano Upgrades GitBook space where Leios team can provide feedback and raise PRs if applicable
      * The rest of the impact assessments are also expected to be merged once feedback on the raised PR provided by Kevin is addressed
    * Risk
      * The initial Dijkstra risk log walthrough was done by Kevin
      * A lot of the risks can be mitigated with enough evidence provided
      * It was agreed that each risk will have the owner assigned as soon as possible, where each risk owner will also be granted editor permission set
      * There will be another column in the risk log representing formal risk assessment for each record in the log
    * Constitutional amendments
      * Parameter Committee met with Carlos last week, and the expectation is that there is going to be a new draft of the Constitution this week
      * There is also a scheduled call for the end of this week which will be recorded and shared afterwards
        * Dijkstra Rollout - Constitutional update and guardrails - Friday 23rd October, 2pm UTC - [meeting link](https://meet.google.com/bqd-dpyz-nrt)
        * It is open for CC members, SPOs and DReps too
        * Its also possible to register for it through the [Cardano Hard Forks Luma calendar](https://luma.com/calendar/cal-TMjYNpSY4huYYif)
    * Comms
      * Intersect and IO are preparing the respective blog posts that follow DIjkstra era and linear Leios rollout respectively
      * There is a fortnightly comms meeting that includes IO, Cardano Foundation and Intersect comms representatives all collaborating on the complementing Dijkstra era hard fork comms strategy
        * As the next milestones become closer, comms meeting is expected to transition to at least the weekly one
    * Node diversity
      * Node diversity workshop in London, **12th&13th November** organized by Amaru team
        * Venue: **London Marriott Hotel Canary Wharf**\
          Location: **22 Hertsmere Rd, London E14 4ED, United Kingdom**
        * [Working agenda](https://hackmd.io/0b_HvF4AS-q4wayJP6M25A)
        * One of the key topics of the workshop will be the consideration of cost and community needs perspectives for each feature in the future era hard forks
    * Hard Fork Working Group call will stay at the same timeslot next week, despite the Daylight Saving Time change that is going to happen soon
      * DST in Europe ends on **Sunday, October 25, 2026**
      * DST in United States ends on **Sunday, November 1, 2026, at 2:00 a.m. local time**
    * Several SPOs attending the meeting expressed their gratitude for being heard by the development teams for addressing their long waited needs on CIP-23 implementation
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
* [Recording](https://drive.google.com/file/d/17q5bO2YW-CzfgSlx4i1bSYqovATwgvJh/view?usp=drive_link)
* [Transcript](https://docs.google.com/document/d/1EwtYM8gBwuxw23etsbc75j4I_Fy29RuFqF3DCihr3Qs/edit?usp=drive_link)
* [Chat](https://drive.google.com/file/d/13jXLl9DqxDo9KNX6Jio7JhaumELz6f6s/view?usp=drive_link)

#### **Action items and next steps**

* **Bosko:** Merge [the updated Leios impact assessment](https://drive.google.com/file/d/1GJNMixEGb6-jEOh8Yy_p2N--cPPz1Jh6/view?usp=sharing) to the Cardano Upgrades GitBook [page](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/ouroboros-linear-leios)
* **Bosko:** Merge the remaining impact assessments to the Dijkstra era GitBook space after addressing Kevins review of them
* **Bosko:** Add CIP-23 full implementation to the [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) GitBook page
* **Bosko:** Adjust CIP-23 impact assessment page based on the plan for the full CIP-23 implementation in Dijkstra era
* **Bosko:** Assign each risk in the [Dijkstra risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?gid=66373110#gid=66373110) a risk owner and grant editor permission set to all owners
* **Bosko:** Add another column in the [Dijkstra risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?gid=66373110#gid=66373110) representing formal risk assessment for each record in the log
* **Carlos:** Prepare the series of recordings to better inform community stakeholders about the intended guardrails
