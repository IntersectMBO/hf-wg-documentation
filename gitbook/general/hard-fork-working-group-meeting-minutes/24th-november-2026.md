# 24th November 2026

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/general/hard-fork-working-group-meeting-minutes/17th-november-2026#action-items-and-next-steps) - Bosko
2. [Dijkstra era hard fork](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era/dijkstra-overview) - Bosko, all
   1. Releases
      1. 11.2.1, 11.2.2, 11.2.3 - Jeff, Amani, Sam
      2. 11.3 - Sebastian
         * [Leios Cost Estimator](https://leios.cardano-scaling.org/cost-estimator/)
      3. [Project view of versions](https://github.com/orgs/input-output-hk/projects/167/views/15)
   2. Constitutional amendments - [Dijkstra era parameters in CAP](https://cap.intersectmbo.org/#/detail/12)
   3. Forking the testnets
   4. [Dijkstra risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?gid=66373110#gid=66373110) review
   5. [Dijkstra readiness tracker](https://docs.google.com/spreadsheets/d/1C1Ai_YTqwKLHtICunzbh_o0FD9XB54Kh/edit?gid=960883614#gid=960883614) review
      1. Lace is planning to deprecate the [cardano-js-sdk](https://github.com/input-output-hk/cardano-js-sdk) repo at the Dijkstra Era Boundary
      2. [Readiness DevX initiative by IO](https://input-output-hk.github.io/devx-updates/map/dijkstra/) (interactive diagram)
   6. Node diversity
      1. [Blocks produced on mainnet](https://kleioscan.com/#/mainnet/nodes)
         * cardano-node, Amaru, Dingo, cardano-bean, tsunagi
      2. Haskell, Amaru (Rust), Dingo (Go), Dugite (Rust), TSUNAGI (Zig), Gerolamo (TypeScript), Dolos (Rust), Turbocardano (C++), Razor (.NET), Scalus (Scala), Yano (Java)
3. AOB

#### Key materials

* Summary
  * **Dijkstra Era hard fork**
    * Releases
      * 11.2.x family of releases
        * Aditional fix is coming to the 11.2.3, and version 11.2.4 is expected to be released beginning of next week
        * Includes the whole Dijkstra era scope except for the linear Leios (CIP-164) and fair min fees (CIP-23)
        * It also includes fixes for memory regression observed in the 11.1.x family of releases
      * [11.3](https://github.com/orgs/input-output-hk/projects/167/views/15)
        * Functional parts are in place
        * Expected to be released in the next few weeks
        * Prototype version is currently running on Musashi testnet
    * Constitutional amendments
      * Cardano constitution draft v6 is [available in CAP portal](https://cap.intersectmbo.org/#/detail/12) since 24th November
      * Carlos from IO shared [Leios initial settings](https://docs.google.com/document/d/1EoOEG1VlZvmM3V-DtgauBRj2Hdc4IW_XYh4Zl8o9nVE/edit?tab=t.0#heading=h.bwldhom4whll) last week
      * Constitution draft can be submitted on Preview testnet as soon as its in viable form for testnet in the next few days
      * Cardano Preview fork wont be blocked by governance
      * The Hard Fork Working Group aim to have a go/no go vote for the submission of the constitution draft on Preview on the next weeks call on 1st December
      * Consitution draft can be submitted on PreProd shortly after, but has not been decided yet
    * Cardano Testnets
      * DijkstraNet
        * Currently running with the pre-released 11.2.x version of the node
          * It includes all of the Dijkstra scope but Linear Leios (CIP-164) and Fair Min Fees (CIP-23)
          * It also allows registration of BLS keys
        * Downstream tooling teams are encouraged to start the integration against the available Dijkstra era feature set
        * Advanced configuration of DijkstraNet Testnet available [here](https://book.play.dev.cardano.org/adv-dijkstra.html)
        * Discord channel: [dijkstra-net](https://discord.com/channels/826816523368005654/1565517149047361586)
      * Musashi Testnet
        * Downstream tooling teams are encouraged to do the early integration against 11.3 prototype on Musashi Testnet
        * Week 47 node release available <a href="https://github.com/input-output-hk/ouroboros-leios/releases/tag/rc-2026w47" target="_blank">here</a>
        * Discord channel: [musashi-testnet](https://discord.com/channels/826816523368005654/1517210858365911242)
      * SanchoNet
        * Expected to soon fork into the Dijkstra era
        * Discord channel: [sanchonet](https://discord.com/channels/826816523368005654/1141734250438197370)
      * Preview
        * The target is to fork the Preview testnet in December with the right node version
        * The necessary step is to have the 12.0 version of the node capable of surviving the hard fork event
    * Node diversity
      * [Block produced on mainnet](https://kleioscan.com/#/mainnet/nodes)
        * cardano-node, Amaru, Dingo, cardano-bean, tsunagi
    * Euler Scoping Working Group
      * Euler era which is trailing Dijkstra era has the working group formed with the early discussions on the scope
      * There is a public call scheduled for 1st December (which is a slight change of plans since last week it was supposed to happen on 2nd December)
      * <a href="https://docs.google.com/document/d/14YtDSJco0hqp-vWbWiNzHYkm4bOe6d9zBEPLW1k1hH0/edit?tab=t.0" target="_blank">Charter</a>
  * Hard Fork Working Group will continue to meet once a week until the Dijkstra era hard fork work solidifies enough to mandate more alignments and sync

#### **Reference links and engagement points**

* Hard Fork Working Group communication channels
  * [Discord](https://discord.com/channels/1136727663583698984/1242097284619960411) — `#wg-hard-fork`
  * [Weekly bulletins](https://x.com/IntersectMBO)
  * [Luma calendar](https://luma.com/calendar/cal-TMjYNpSY4huYYif)
  * [Email](mailto:hard-fork@intersectmbo.org)
* [Dijkstra era | Cardano's next protocol upgrade](https://www.youtube.com/watch?v=k4x0eP_h1Qo)
* [BLS Key rotation](https://github.com/input-output-hk/ouroboros-leios/issues/1024)
* [Leios Cost Estimator](https://leios.cardano-scaling.org/cost-estimator/)
* [Dijkstra readiness tracker](https://docs.google.com/spreadsheets/d/1C1Ai_YTqwKLHtICunzbh_o0FD9XB54Kh/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true)
* [Readiness DevX initiative by IO](https://input-output-hk.github.io/devx-updates/map/dijkstra/)
* [Dijkstra Risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?usp=sharing)
* [Dijkstra era parameters in CAP](https://cap.intersectmbo.org/#/detail/12)
* [Antithesis](https://cardanofoundation.org/blog/improving-cardano-antithesis)
* [Recording](https://drive.google.com/file/d/19CHJCuzaslej6bWI2OxT3LZ6EKYrk2S4/view?usp=drive_link)
* [Transcript](https://docs.google.com/document/d/1J94jCJoyBlKfxVEb2Ev5UFDURUn1Cdqr5KjSed7I9x8/edit?usp=drive_link)
* [Chat](https://drive.google.com/file/d/1sC2j6W0Oe_KVQSkU443Yvc4-hGjQLJq6/view?usp=drive_link)

#### **Action items and next steps**

* **Jeff:** Confirm the chosen path for Ogmios/Kupo from the readiness aspect
* **Kevin/TSC:** Provide baseline to the Leios team for the hardware requirements
* **Bosko:** Adjust Dijkstra risk log for better visibility and risk management
* **Bosko/Carlos:** Provide unified delivery timelines (high level one and more detailed one)
* **Bosko:** Provide the link for the public call of the Euler Scoping Working Group
  * **Bosko:** Add the above link to the Hard Fork Working Group Luma calendar
