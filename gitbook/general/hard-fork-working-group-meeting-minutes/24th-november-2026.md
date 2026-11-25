# 24th November 2026

#### <mark style="color:$danger;">**WORK IN PROGRESS**</mark>

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
      * 11.2.1, 11.2.2, 11.2.3
        *
      * [11.3](https://github.com/orgs/input-output-hk/projects/167/views/15)
        *
    * Constitutional amendments
      *
    * Cardano Testnets
      * DijkstraNet
        *
        * Downstream tooling teams are encouraged to start the integration against the available Dijkstra era feature set
        * Advanced configuration of DijkstraNet Testnet available [here](https://book.play.dev.cardano.org/adv-dijkstra.html)
        * Discord channel: [dijkstra-net](https://discord.com/channels/826816523368005654/1565517149047361586)
      * Musashi Testnet
        *
        * Discord channel: [musashi-testnet](https://discord.com/channels/826816523368005654/1517210858365911242)
      * SanchoNet
        *
        * Discord channel: [sanchonet](https://discord.com/channels/826816523368005654/1141734250438197370)
      * Preview
        *
    * Node diversity
      * [Block produced on mainnet](https://kleioscan.com/#/mainnet/nodes)
        * cardano-node, Amaru, Dingo, cardano-bean, tsunagi
    * Euler Scoping Working Group
      *
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

* **Leonard H/Bosko/Jeff:** Confirm the chosen path for Ogmios/Kupo from the readiness aspect
* **Kevin/TSC:** Provide baseline to the Leios team for the hardware requirements
* **Bosko:** Adjust Dijkstra risk log for better visibility and risk management
* **Bosko/Carlos:** Provide unified delivery timelines (high level one and more detailed one)
* **Kevin:** Provide the link for the public call of the Euler Scoping Working Group
  * **Bosko:** Add the above link to the Hard Fork Working Group Luma calendar
