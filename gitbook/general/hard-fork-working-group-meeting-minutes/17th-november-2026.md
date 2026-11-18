# 17th November 2026

### <mark style="color:$danger;">**WORK IN PROGRESS (Recording, Transcript and Chat are available)**</mark>

#### Agenda

1. [Action items from the last call](https://cardanoupgrades.docs.intersectmbo.org/general/hard-fork-working-group-meeting-minutes/10th-november-2026#action-items-and-next-steps) - Bosko
2. [Dijkstra era hard fork](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era/dijkstra-overview) - Bosko, all
   1. Releases
      1. 11.2.1, 11.2.2, 11.2.3 - Jeff, Amani, Sam
      2. 11.3 - Sebastian
      3. [Project view of versions](https://github.com/orgs/input-output-hk/projects/167/views/15)
   2. [Dijkstra risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?gid=66373110#gid=66373110) review
   3. Scope
      1. Each remaining scope item (besides CIP-23 and CIP-50 which are already documented) have its impact documented ([PR](https://github.com/IntersectMBO/hf-wg-documentation/pull/43) opened) in the [Cardano Upgrades space](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) (Core semantics changes, Breaking API changes, New features)
         * [Updated Leios impact assessment available for feedback](https://drive.google.com/file/d/1GJNMixEGb6-jEOh8Yy_p2N--cPPz1Jh6/view?usp=sharing) (passed from TSC to original authors)
   4. Constitutional amendments - [Dijkstra era parameters in CAP](https://cap.intersectmbo.org/#/detail/12)
   5. Comms - Larisa, Ian, Matthew
   6. Node diversity
      1. [Blocks produced on mainnet](https://kleioscan.com/#/mainnet/nodes)
         * cardano-node, Amaru, Dingo, cardano-bean, tsunagi
      2. Node diversity workshop in London last week, **12th&13th November** organized by Amaru team
         * [Node diversity - Building cost efficient software the "Cardano Way"](https://x.com/Amaru_Cardano/status/2122473330758586462?a=aftT0hlT6IQUlSGlVYQ\&s=20)
         * [X post](https://x.com/Amaru_Cardano/status/2122473569191948308?a=hz1EpdGAiEVnZXmJvWQ\&s=20)
      3. Haskell, Amaru (Rust), Dingo (Go), Dugite (Rust), TSUNAGI (Zig), Gerolamo (TypeScript), Dolos (Rust), Turbocardano (C++), Razor (.NET), Scalus (Scala), Yano (Java)
3. Hard Fork Working Group funding (Technical Steering Committee budget)
   1. Application form - [https://forms.clickup.com/9015279944/f/8cnmga8-55475/D8A3VU9CZOQQU56CYX](https://forms.clickup.com/9015279944/f/8cnmga8-55475/D8A3VU9CZOQQU56CYX)
4. AOB

#### Key materials

* Summary
  * **Dijkstra Era hard fork**
    * Releases
      * 11.2.1, 11.2.2, 11.2.3
        * 11.2.1 is the last pre-released version and is used to run DijkstraNet at the moment
        * 11.2.2 was delayed a bit due to the conformance issue discovered at the Node diversity workshop, fix is expected soon (tag is available [here](https://github.com/IntersectMBO/cardano-node/releases/tag/11.2.2))
          * Regression testing was done and proved version reached good quality
        * 11.2.3, that will address conformance issue fix, is expected to be pre-released soon and made mainnet ready by the end of this week
        * These versions are not capable of surviving the hard fork
      * [11.3](https://github.com/orgs/input-output-hk/projects/167/views/15)
        * All work necessary for minimum viable Linear Leios is already in PR
        * Main stream work at the moment relates to review of \~10000 lines of code
        * Smaller "plumbing" things expected to be finalized
        * It is expected to be pre-released in 2-3 weeks after which DijkstraNet will be re-forked
        * This is the first candidate that has a chance to be promoted to 12.0 provided successful testing without any showstopper issues
    * Cardano Testnets
      * DijkstraNet
        * Currently running with the pre-released 11.2.1 version of the node
          * It includes all of the Dijkstra scope but Linear Leios (CIP-164) and Fair Min Fees (CIP-23)
          * It also allows registration of BLS keys
        * Downstream tooling teams are encouraged to start the integration against the available Dijkstra era feature set
        * Advanced configuration of DijkstraNet Testnet available [here](https://book.play.dev.cardano.org/adv-dijkstra.html)
        * Discord channel: [dijkstra-net](https://discord.com/channels/826816523368005654/1565517149047361586)
      * Musashi Testnet
        * Downstream tooling teams are encouraged to do the early integration against 11.3 prototype on Musashi Testnet
        * Week 46 node release available [here](https://github.com/input-output-hk/ouroboros-leios/releases/tag/rc-2026w46)
        * Discord channel: [musashi-testnet](https://discord.com/channels/826816523368005654/1517210858365911242)
      * SanchoNet
        * Expected to soon fork into the Dijkstra era
        * Discord channel: [sanchonet](https://discord.com/channels/826816523368005654/1141734250438197370)
    * Scope
      * Adjusted CIP-23 impact assessment page the [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) GitBook space based on the plan for the full CIP-23 implementation in Dijkstra era
      * Merge the remaining impact assessments to the Dijkstra era GitBook space after addressing their pending reviews
    * Risk management
      *
    * Constitutional amendments
      *
    * Ecosystem readiness
      * Tooling - High level
        *
      * SPOs
        * Compatibility matrix was shared in the last weeks upgrade bulletin and will be added to the [Dijkstra upgrade readiness](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-readiness) page
    * Node diversity
      * Amaru
        *
      * [Block produced on mainnet](https://kleioscan.com/#/mainnet/nodes)
        * cardano-node, Amaru, Dingo, cardano-bean, tsunagi
      * Node diversity workshop in London last week, **12th&13th November** organized by Amaru team
    * Hard Fork Working Group funding (Technical Steering Committee budget)
      * [Application form](https://forms.clickup.com/9015279944/f/8cnmga8-55475/D8A3VU9CZOQQU56CYX)
  * Hard Fork Working Group will continue to meet once a week until the Dijkstra era hard fork work solidifies enough to mandate more alignments and sync

#### **Reference links and engagement points**

* Hard Fork Working Group communication channels
  * [Discord](https://discord.com/channels/1136727663583698984/1242097284619960411) — `#wg-hard-fork`
  * [Weekly bulletins](https://x.com/IntersectMBO)
  * [Luma calendar](https://luma.com/calendar/cal-TMjYNpSY4huYYif)
  * [Email](mailto:hard-fork@intersectmbo.org)
* [Dijkstra era | Cardano's next protocol upgrade](https://www.youtube.com/watch?v=k4x0eP_h1Qo)
* [BLS Key rotation](https://github.com/input-output-hk/ouroboros-leios/issues/1024)
* [Dijkstra readiness tracker](https://docs.google.com/spreadsheets/d/1C1Ai_YTqwKLHtICunzbh_o0FD9XB54Kh/edit?usp=sharing\&ouid=106134819668558877362\&rtpof=true\&sd=true)
* [Dijkstra Risk log](https://docs.google.com/spreadsheets/d/1NXMFkCpqNlq8SPSgzPNi_ZYLUg25tVWU-i4yz7fQhcI/edit?usp=sharing)
* [Dijkstra era parameters in CAP](https://cap.intersectmbo.org/#/detail/12)
* [Antithesis](https://cardanofoundation.org/blog/improving-cardano-antithesis)
* [Recording](https://drive.google.com/file/d/1N6rQ3Aw0r2AdeH2_VwNi0K2_TnsMJncO/view?usp=drive_link)
* [Transcript](https://docs.google.com/document/d/17rrXkxL2tWY1p2e8CPy7xpN9EgCXe6XILT-aPaxHfAE/edit?usp=drive_link)
* [Chat](https://drive.google.com/file/d/17-z5h7R0MJphPP34a6bkk8lhiKn8kzMy/view?usp=drive_link)

#### **Action items and next steps**

*
