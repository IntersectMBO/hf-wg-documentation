# 13th October 2026

### <mark style="color:$danger;">**WORK IN PROGRESS**</mark>

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
    * Constitutional amendments
    * Timeline
    * Scope
    * Risks
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

* **Bosko:** Share [the review of the Leios Risk register](https://docs.google.com/document/d/1kvf8twFWhwsYtnLfjjgu7D3isJBTKdm3zXgre1PRfFo/edit?usp=sharing) with the HFWG, prepared by Technical Steering Committee member Leandros
* **HFWG members:** Assess [Dijkstra risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?gid=66373110#gid=66373110), identify potential gaps and provide updates where necessary and/or applicable
* **Michiel/Elena/Bosko:** Determine HFWG wallet teams liaison(s) and finalize wallet teams outreach list
  *   **HFWG wallet teams liaison:** Reach out to Keystone, Ledger, Trezor, Bitbox (..?)

      and point them to the CDDL change of adding [`bls_key`](https://github.com/IntersectMBO/cardano-ledger/blob/2c33b4f858c0e62b300d121996a479f505d8c0e5/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L469)
* **Elena/Bosko:** Check and cross-reference readiness approach being taken in previous hard forks with Chang, Plomin and beyond
