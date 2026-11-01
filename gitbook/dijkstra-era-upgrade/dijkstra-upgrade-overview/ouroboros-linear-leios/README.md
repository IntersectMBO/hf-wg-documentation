# Ouroboros Linear Leios

### Impact Analysis

Linear Leios is the headline Dijkstra Phase 1 feature. A block producer issues an Endorser Block (EB) alongside its ordinary Praos block, now called a Ranking Block (RB). The EB is a list of transaction hashes that the RB has no room for. A committee of stake pools votes on the EB with BLS signatures. Once a quorum is reached, a later RB carries a certificate instead of transactions, and the certified EB's transactions enter the ledger.

Transaction format and transaction semantics do not change. What changes is how the chain reaches consensus on a transaction sequence, what a block body contains, what SPOs run, and how much data flows. Linear Leios activates at the Dijkstra hard fork, and becomes available when sufficient pools have registered their BLS keys and any other necessary conditions are met. Throughput is then raised gradually through protocol-parameter updates, not on hard-fork day.

* **CIP:** [CIP-164 Ouroboros Linear Leios](https://cips.cardano.org/cip/CIP-0164) (original PR [cardano-foundation/CIPs#1078](https://github.com/cardano-foundation/CIPs/pull/1078))
* **Overview:** [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), Ouroboros Linear Leios (CIP-164)
* **Engineering impact analysis:** [Leios impact analysis](https://github.com/input-output-hk/ouroboros-leios/blob/main/docs/ImpactAnalysis.md). It derives node requirements (`REQ`) and component changes (`NEW` / `UPD`) for consensus, network, ledger, cryptography, P\&T and end-to-end testing. This page is the ecosystem-facing summary. Where they disagree on detail, the engineering document and the frozen ledger CDDL win.&#x20;
* **Protocol parameters:** Dijkstra CDDL keys 40 to 48. Discussion in [cardano-ledger#5965](https://github.com/IntersectMBO/cardano-ledger/issues/5965).&#x20;
* **BLS key rotation:** [ouroboros-leios#1024](https://github.com/input-output-hk/ouroboros-leios/issues/1024)
* **Depends on:** [Non-segregated Block Body Serialization (CIP-176)](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/non-segregated-block-body-serialization)
* **Do not confuse with:** [Peras codec extensions (CIP-140)](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/peras-codec-extensions). Peras certificates are dormant in Phase 1. Linear Leios certificates are live.

The engineering analysis was written assuming a later era ("Euler"). The Dijkstra overview places Linear Leios in Phase 1, protocol version 12. Read its "Euler" as "Dijkstra".

***

### Core semantics changes <a href="#core-semantics-changes" id="core-semantics-changes"></a>

Implications, why it concerns you, and what needs to be updated in response.

#### What the protocol actually does <a href="#what-the-protocol-actually-does" id="what-the-protocol-actually-does"></a>

Terms used below:

* **RB, Ranking Block.** A Praos block with extra header fields. It carries transactions (a TxRB) or a Linear Leios certificate (a CertRB).
* **EB, Endorser Block.** A list of hashes of serialised transactions. Announced by hash in the header of the RB issued with it. Empty EBs are not issued.
* **EB closure.** The transactions an EB references. Rebuilding the EB from its closure is just hashing.
* **Vote.** A BLS signature by a committee member supporting an RB header, and so the EB it announced.
* **Certificate.** An aggregate of enough votes. A CertRB's certificate makes the EB announced by the preceding RB part of the chain.

Chain selection is still Praos. Linear Leios only decides whether an announced EB's transactions get onto the chain. Praos traffic and computation take strict priority over Linear Leios traffic, and fresher EBs take priority over stale ones. If voting fails, the chain degrades to ordinary Praos blocks. It does not stall.

Ledger rules for a single transaction are unchanged. Applying a CertRB means applying the certified EB's transactions, validated against the ledger state before the CertRB itself is ticked in. Votes already attest the EB's validity, so the node adopts a certified EB with a new, cheaper "apply without re-validation" path. The ledger work is to make that path significantly cheaper than today's `reapplyTx`.

The ledger state gains a voting committee. SPOs register BLS public keys. Persistent voters are chosen at each epoch boundary by Fait Accompli sortition, alongside non-persistent voters. The committee is queryable.

Under low load, transactions still land in TxRBs exactly as today. Under high load, a 12 MB backlog that Praos would take around 44 minutes to clear lands in one certified EB within a few minutes. Average throughput and latency improve, but what happens to a single transaction under load changes. See latency-sensitive systems below. Note that if Linear Leios is unavailable for some reason, however, throughput will drop to Praos levels, potentially creating long-lived backlogs.

#### Why this concerns wallets, explorers, indexers, and pool tools <a href="#why-this-concerns-wallets-explorers-indexers-and-pool-tools" id="why-this-concerns-wallets-explorers-indexers-and-pool-tools"></a>

**SPOs.** One new duty: manage a BLS key pair. Generate it, register it, rotate it on a schedule like KES, and configure the block-producing node with it. The node then votes automatically.

Hardware needs rise in stages as governance raises throughput. Plan for the stage you are in and the next one, not straight for the simulated ceiling. One exception: fast SSDs are needed from day one (see below).

| Stage                                               | Throughput          | Chain growth, if sustained | Relay egress, rough peak |
| --------------------------------------------------- | ------------------- | -------------------------- | ------------------------ |
| Praos today                                         | 4.5 TxkB/s capacity | about 0.15 TB a year       | a few Mb/s               |
| Linear Leios as demonstrated (MusashiNet, about 6x) | about 27 TxkB/s     | about 0.85 TB a year       | about 20 Mb/s            |
| CIP-164 demand projection for 2030                  | about 60 TxkB/s     | about 1.9 TB a year        | about 50 Mb/s            |
| CIP-164 simulated ceiling                           | 200 to 250 TxkB/s   | about 6 to 8 TB a year     | about 200 Mb/s           |

Chain growth assumes capacity is used continuously, so real growth tracks demand and is lower. Egress assumes about 100 downstream peers fetching everything. It is an upper bound, not a measurement. CIP-164's simulations, which these rows partly rely on, did not model memory or disk.

* **CPU.** A four-core machine becomes the baseline. Average load stays low, but load is bursty around EB validation.
* **Bandwidth.** CIP-164's "under 10 Mb/s" is a per-link cap in a simulated topology, not a relay's total. Relay egress scales with throughput times downstream peers, and CIP-164 itself warns that operators with significant stake will need more relay resources. Today's transaction submission protocol also fetches the same transaction from every peer that offers it. The more efficient version 2 is still being rolled out. A worst-case withheld-EB burst is over a gigabyte of download at any stage. Size relays for peak egress, not average ingress.
*   **Egress cost.** The change most likely to hurt SPO economics, and it grows with each stage. On metered cloud hosting (AWS internet egress, October 2026: $0.09/GB for the first 10 TB a month, falling in tiers), sustained relay egress costs roughly:

    | Sustained egress | Per month | Approx. cost |
    | ---------------- | --------- | ------------ |
    | 2 Mb/s           | 0.6 TB    | $50          |
    | 20 Mb/s          | 6.5 TB    | $570         |
    | 50 Mb/s          | 16 TB     | $1,400       |
    | 200 Mb/s         | 65 TB     | $5,300       |

    These figures are per relay, and most pools run two or more relays. CIP-164's operating-cost table puts total per-node operation at about $130 a month at 250 kB/s. Egress at the higher stages would swamp that. Mitigations are hosting with unmetered or flat-rate bandwidth, transaction submission version 2, and capping downstream peer counts, although capping trades against network health. Each step up in throughput should take SPO egress cost into account alongside fee revenue.
* **Memory and ledger backend.** The UTxO set will eventually grow beyond what the in-memory ledger backend can hold on ordinary machines. Higher throughput brings that point closer, but does not by itself cause it. The LSM-tree backend for UTxO-HD is therefore likely to become mandatory in order to deal with UTxO growth, with 8 to 16 GB of RAM as the working range on current benchmarks, rather than ever-larger RAM to keep the ledger in memory.
* **Disk capacity.** Certified EB closures are kept forever, so storage grows with throughput, as the table shows. At the demonstrated stage it is under a terabyte a year. Near the ceiling it is several terabytes a year. Storage, backups, Mithril snapshots, and node re-sync time all scale with it. Buy capacity in stages.
*   **Disk speed: fast SSDs are needed regardless of stage.** Spinning hard disks are likely to become unusable for block producers and relays, for two independent reasons:

    * **LSM-tree ledger.** Once the LSM-tree backend is mandated to deal with UTxO growth, the UTxO set lives on disk. Every transaction's inputs then become random reads and writes, and LSM-trees rely on fast random reads. A hard disk manages roughly 100 to 200 random I/O operations a second, and even demonstrated Linear Leios rates need far more. This applies from the moment LSM is required, whatever the throughput, so SPOs need fast SSDs on this route even without Linear Leios.
    * **Linear Leios itself.** EB closures are written as they arrive, and a withheld-EB burst writes over a gigabyte at network speed. The engineering analysis flags disk contention between Praos and Linear Leios as a risk. Votes have a deadline, so a block producer that cannot validate an EB in time misses its vote. A slow disk also delays Praos block adoption, which is the thing Linear Leios must not disturb.

    Treat a fast SSD, preferably NVMe, as a requirement for block producers and relays from the Dijkstra hard fork, with capacity added as throughput rises. Archive and indexer nodes have the same problem at larger volumes.

Mempool capacity also grows, to at least two EBs.

**Wallets, dApps, and SDKs.** Little in the code. Transaction building, signing, fee calculation, and the submission protocol are unchanged. What a successful submission means under load does change. See the next paragraph. Any SDK or dApp that references protocol parameters will need to be updated. CIP-164 does not change the transaction format. Use the other Dijkstra pages for the Phase 1 items that do change transactions.

**Indexers, data nodes, explorers, Mithril, and anything that decodes blocks.** A block is no longer self-contained. A CertRB body holds a certificate, and its transactions live in an EB fetched separately. Tools that consume blocks through a node client interface should see a backward-compatible view (see below). Tools that speak node-to-node or parse raw block CBOR must resolve EB closures themselves.

**Latency-sensitive systems.** Behaviour under congestion changes, not just its scale. Under Praos the mempool holds about two blocks' worth of transactions. Once it is full, submission stalls: local submission waits for room and peers stop pulling. A dApp therefore learns straight away that its transaction has not been admitted, and can wait, re-price, re-route, or drop it. Under Linear Leios the mempool holds at least two EBs' worth. Far more transactions are accepted, and then wait for an EB to be announced, voted on, and certified. That can be 50 s or more at peak, and longer if an EB fails to certify and its transactions have to wait for a later block. Being accepted into the mempool stops being a good signal that inclusion is imminent, and the early push-back that dApps rely on today arrives later or not at all. Bridges, DEXes, batchers, algorithmic stablecoins, and L2s should track on-chain inclusion rather than mempool admission. They should also revisit timeouts, retry logic, and anything that assumes accepted means next block.

**dApps generally.** Two further assumptions stop holding.

* **Throughput varies.** Chain capacity is no longer a fixed number of bytes per block. It depends on whether EBs certify: on committee participation, on enough pools having registered BLS keys, and on network conditions. It also steps up as governance raises the Linear Leios parameters. When Linear Leios is degraded or unavailable, capacity falls back to Praos levels within the same epoch. dApps that schedule batches, auctions, liquidations, or oracle updates against an assumed capacity should handle a range rather than a constant.
* **Settlement takes longer from submission.** A transaction carried in an EB reaches the chain only when a later CertRB certifies that EB. Confirmation depth, and so settlement, is counted from the CertRB, not from when the EB was announced. Time from submission to an agreed confirmation depth is therefore longer and more variable than inclusion time alone suggests. Exchanges, bridges, and anything that releases value after N confirmations should measure that end to end, from submission. Do not treat EB announcement as inclusion. Peras, in Phase 2, is the feature aimed at faster settlement. Linear Leios does not provide it.

**Exchanges and custodians.** Affected on several fronts at once:

* **Infrastructure.** They run their own nodes, usually with DBSync, Ogmios, or cardano-wallet behind them. The disk, fast-SSD, and egress points above apply in full, and indexer ingest has to keep up at Linear Leios rates.
* **Deposit detection.** Pipelines that read blocks through a node client interface should keep working, provided the backward-compatible block view ships as proposed. Pipelines that parse raw block CBOR, or follow the chain node-to-node, must resolve EB closures, or they will miss deposits carried in certified EBs.
* **Crediting policy.** Confirmation counts used to credit deposits should be counted from the CertRB, and end-to-end settlement time re-measured. See dApps generally above.
* **Withdrawals and sweeps.** Under congestion, mempool admission no longer signals imminent inclusion. Batching, fee-bumping, and retry logic for withdrawals and hot-to-cold sweeps should track on-chain inclusion, and allow for capacity varying between epochs.
* **Upgrade timing.** Nodes and indexers must be on a Dijkstra-capable release before the hard fork, and tested on Preview and Preprod at Linear Leios load.

Other Dijkstra Phase 1 items matter to exchanges too: deposits to stake addresses (CIP-159), the new submit encoding (CIP-167), and withdrawals without DRep delegation (CIP-181). See those pages.

**Everyone who stores chain data.** That means indexers, explorers, archive nodes, and full-node wallets such as Daedalus. How much more data, and when, is uncertain. Today's Praos capacity is about 4.5 TxkB/s: 90 kB every 20 s on average. CIP-164 simulations ran without congestion at 200 TxkB/s, about 45x that, with a theoretical ceiling near 300 TxkB/s. Those are simulator results under favourable conditions:

* honest nodes and a 750-node mainnet-like topology,
* average mainnet Plutus load,
* committees smaller than the 900 seats recommended,
* no modelling of memory, disk, or garbage-collection pressure.

The real node has not yet shown these rates. The first public testnet phase, MusashiNet "Earth" (June to August 2026), peaked at 26.8 TxkB/s, about 5 to 6x Praos capacity. That was under synthetic load, with cautious initial parameters, on a network of up to 63 pools, not mainnet. Sustained full load also stretched block propagation: over 40% of blocks took more than a second to reach the network, against near-universal sub-second delivery on mainnet today. That is the Praos-protection property Linear Leios has to preserve. Treat 5 to 6x as today's demonstrated figure, and the simulated rates as targets yet to be shown. Mainnet starts lower and is raised step by step as testnets and benchmarks justify. Demand is also well below capacity: CIP-164's own projection is about 15 TxkB/s in 2026 and about 60 TxkB/s by 2030. Plan capacity in stages against the parameters governance actually sets, with the simulated ceiling as the outer bound.

Full-node wallets are hit hardest, because they run on end users' own machines. A desktop wallet that keeps the whole chain needs disk growing by terabytes a year at high throughput, a fast SSD rather than a laptop hard disk, and a much longer initial sync. Keeping up after time offline also takes longer, because a week away now means catching up on a week of Linear Leios-rate data. Full-node wallet teams should plan Mithril-based bootstrap as the default, revisit minimum system requirements, and tell users clearly when a light wallet is the better choice.

#### What to update <a href="#what-to-update" id="what-to-update"></a>

1. SPO tooling and runbooks: BLS key generation, registration, rotation, expiry monitoring, and node configuration. Treat it like KES.
2. Network and consensus libraries outside Haskell (Pallas, Gouroboros, Amaru, Dingo, Acropolis): new block structure, EB fetch, vote and certificate handling, BLS verification. They also need the new Linear Leios protocol parameters (keys 40 to 48). The timing periods, committee size, quorum threshold, and EB size and execution limits drive voting, certification, and EB validation directly, so they must be read from the current ledger state and followed when governance changes them, not hardcoded.
3. Block decoders: RB header fields, certificate body variant, and EB structure. Combine with the CIP-176 body layout.
4. Indexers and explorers: index transactions under the CertRB that certified them. Optionally record EB, vote, and committee data for Linear Leios dashboards.
5. Storage and ingest pipelines, including full-node wallets: move block producers and relays to fast SSDs before the hard fork, and prepare for the LSM-tree ledger backend. Add disk capacity in stages as governance raises throughput, using the staging table above. Revisit full-node wallet system requirements and bootstrap. Load-test at Linear Leios rates on the testnets before mainnet parameters are raised.
6. Latency-sensitive dApps: stop using mempool admission as a congestion signal. Track on-chain inclusion, and re-test timeout, retry, and resubmission logic against high-load Linear Leios inclusion times.
7. All dApps: tolerate variable chain capacity, and measure settlement from submission to confirmation depth, counted from the CertRB. Revisit confirmation counts used to release value.

***

### Breaking API changes <a href="#breaking-api-changes" id="breaking-api-changes"></a>

Why it was unavoidable, and what needs to be updated in response.

The block format, the ledger state (voting committee and BLS keys), and the protocol parameters all change. Those changes need a new era. The transaction format does not change, so the break is confined to block-level and node-level interfaces.

#### Wire and query contract <a href="#wire-and-query-contract" id="wire-and-query-contract"></a>

| Channel                                   | Shape in Dijkstra                                                                                                                                                                                            |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| RB header                                 | Two new fields: `block_body_contains_leios_cert` (bool) and `eb_references_announcement` (`[eb_hash, eb_size]` or nil). Header size budget is the existing `maxBlockHeaderSize`.                             |
| RB body                                   | `[transactions, leios_certificate / nil, peras_certificate / nil]`, per CIP-176. A CertRB carries the certificate and, by protocol rule, no transactions.                                                    |
| EB                                        | List of transaction hashes, plus sizes. Fetched separately from the RB.                                                                                                                                      |
| Certificate                               | `[signers, signature]`: a bitfield of up to 65,536 committee members and one 48-byte aggregate BLS signature.                                                                                                |
| Vote                                      | BLS12-381 signature. Diffused node-to-node, never on chain.                                                                                                                                                  |
| Pool registration certificate             | Optional `bls_key` = `[96-byte public key, 48-byte proof of possession]` after the VRF key hash. Omitting it keeps the old shape valid. A dedicated BLS-only rotation certificate is still under discussion. |
| N2N mini-protocols                        | New Linear Leios protocols for EB announcements, EBs, EB transactions, and votes. Multiplexer biased to Praos.                                                                                               |
| N2C `LocalChainSync`, UTxO-RPC Sync       | Requirement: backward-compatible block view. The proposed approach inlines the certified EB's transactions into the served block body. Not yet frozen.                                                       |
| N2C `LocalTxSubmission`, `LocalTxMonitor` | Unchanged                                                                                                                                                                                                    |
| N2C `LocalStateQuery`                     | Extended. Voting committee and new protocol parameters.                                                                                                                                                      |
| PParams                                   | New governable Linear Leios keys, see below                                                                                                                                                                  |

If the client interface inlines EB transactions, two things follow. Served block bodies can be about 140x bigger than a 90 kB Praos block. The header body-hash no longer equals a plain hash of the served body bytes. Block integrity checks must verify the certificate and recompute the EB.

#### New protocol parameters <a href="#new-protocol-parameters" id="new-protocol-parameters"></a>

From the Dijkstra CDDL and `PParams` on cardano-ledger `master` (October 2026). Values for mainnet are not set yet. The design discussion is in [cardano-ledger#5965](https://github.com/IntersectMBO/cardano-ledger/issues/5965).

| Key | JSON name                          | Type          | Meaning                                                            |
| --- | ---------------------------------- | ------------- | ------------------------------------------------------------------ |
| 40  | `leiosAnnouncementPeriodLength`    | milliseconds  | Time for RB headers, and so EB announcements, to reach the network |
| 41  | `leiosVotePeriodLength`            | milliseconds  | Window in which committee members may vote on an EB                |
| 42  | `leiosDiffusionPeriodLength`       | milliseconds  | Extra time after voting to make the EB available network-wide      |
| 43  | `leiosCommitteeSize`               | uint16        | Target committee size. Replaces the earlier stake-coverage idea.   |
| 44  | `leiosQuorumStakeThreshold`        | unit interval | Fraction of committee stake a certificate's votes must represent   |
| 45  | `maxEndorserBlockReferencesSize`   | uint32        | Maximum size of the EB itself, the list of transaction references  |
| 46  | `maxEndorserBlockTxsSize`          | uint32        | Maximum total size of the transactions an EB references            |
| 47  | `maxEndorserBlockExecutionUnits`   | ex units      | Plutus memory and steps across an EB's transactions                |
| 48  | `maxRefScriptSizePerEndorserBlock` | uint32        | Reference-script bytes across an EB's transactions                 |
| 2   | `maxBlockBodySize`                 | existing      | RB size limit, unchanged                                           |

The periods are in milliseconds, not slots. All nine are in the ledger's Network and Security groups, so changing them needs SPO votes as well as DReps and the Constitutional Committee. None can be changed until the constitution and guardrails script name them. BLS key expiry is proposed as a Dijkstra genesis value, not a governable parameter.

#### What to update <a href="#what-to-update" id="what-to-update"></a>

* cardano-cli and cardano-api: BLS key generation, pool registration with `bls_key`, and any rotation command.
* Node configuration templates: BLS signing key, plus the proposed two-key handover.
* Ogmios, Koios, DBSync, and GraphQL: certificate-bearing blocks, committee queries, new protocol parameters.
* Hardware wallets: display the BLS field on pool registration. Whether HW support is required for the hard fork is still debated.
* Guardrails script and constitution appendix for the Linear Leios parameters.
* Tracing and monitoring dashboards: Linear Leios introduces a new set of observables.

***

### New features <a href="#new-features" id="new-features"></a>

What new capabilities it unlocks that you might want to start thinking about.

* **Throughput.** Headroom beyond Praos. The prototype has shown 5 to 6x Praos capacity on MusashiNet. Simulations suggest up to about 45x, 200 TxkB/s. Real mainnet gains will start from the demonstrated figure, set by the parameters governance enacts and by what the implementation demonstrates on testnets. Raised step by step after activation, which gives operators and indexers time to scale.
* **Burst absorption.** A backlog clears in minutes rather than tens of minutes, without a change to user transactions.
* **Fee revenue headroom.** More transactions per epoch, at the point where fees must take over from the shrinking Reserve to fund rewards.
* **Stronger evidence for certified transactions.** A certificate is a stake supermajority endorsement. The engineering analysis flags this as a possible stronger early-finality signal than first inclusion in a Praos block. Not specified yet. Do not market it as finality.
* **BLS on the node.** BLS12-381 signing, aggregation, and proof of possession land in `cardano-base`. Peras is expected to reuse them in Phase 2.
* **Linear Leios-aware analytics.** EB, vote, and certificate data open new monitoring and explorer views, if your users want them.

Test on [MusashiNet](https://www.musashi.network/) now. Its first phase reported its results in [Leios hit 6x Cardano's throughput on its first testnet](https://www.iog.io/news/leios-hit-6x-cardano-s-throughput-on-its-first-testnet) (IOG, August 2026). The engineering analysis asks for a high-load testnet early so infrastructure teams find their scaling limits before mainnet throughput is raised.

***

#### Leios Portal <a href="#leios-portal" id="leios-portal"></a>

{% embed url="https://leios.cardano-scaling.org/" %}

#### Leios Dev Tracker <a href="#leios-dev-tracker" id="leios-dev-tracker"></a>

Track the development journey of Leios behind the scenes, with activity updates and evolving roadmaps.

{% embed url="https://engineering.iog.io/leios" %}

#### Musashi Network <a href="#musashi-network" id="musashi-network"></a>

{% embed url="https://www.musashi.network/" %}
