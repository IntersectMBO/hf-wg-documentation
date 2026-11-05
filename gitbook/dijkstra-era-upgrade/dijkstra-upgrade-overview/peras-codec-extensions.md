# Peras codec extensions

Ouroboros Peras (CIP-140) is the Phase 2 feature. It is a voting overlay that boosts widely supported chain tips so they can be treated as settled in minutes rather than Praos depths.

Phase 1 does not turn that overlay on. It only ships the pieces that would otherwise need a second ledger era:

- block-body room for an optional Peras certificate,
- the Peras protocol parameters on Dijkstra `PParams`,
- codecs so nodes can speak the bytes.

Phase 2 is an intra-era hard fork, planned around Q2 2027: a protocol-version bump inside Dijkstra that activates vote diffusion, certificate aggregation, and the modified chain-weight rule. Because the bytes and the parameters already exist, Phase 2 does not need an Euler-style era package.

**CIP:** [CIP-140 Ouroboros Peras](https://cips.cardano.org/cip/CIP-0140) (also [CIP-0140 on GitHub](https://github.com/cardano-foundation/CIPs/tree/master/CIP-0140))
**Overview:** [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), Structural groundwork for Phase 2, Peras codec extensions (CIP-140). Phase 2 activates the same CIP in full.
**Product plan:** [Phase 2 Peras activation](https://product.cardano.intersectmbo.org/hardfork-planning/dijkstra/#phase-2-peras-activation-intra-era-hard-fork-q2-2027)
**Related:** [Non-segregated Block Body Serialization (CIP-176)](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/non-segregated-block-body-serialization)

***

## Core semantics changes

Implications, why it concerns you, and what needs to be updated in response.

### What the ledger actually does at Phase 1

A Dijkstra block body can optionally carry a `peras_cert`. Consensus does not change chain selection, does not run Peras voting rounds, and does not boost block weight. Certificates, if present at all on test fixtures, must be ignored for settlement purposes on mainnet Phase 1.

Dijkstra `PParams` grow the CIP-140 natural-number parameters. CIP names:

- `U`, voting-round length in slots
- `L`, minimum candidate age in slots
- `A`, maximum certificate age in rounds
- `R`, rounds to ignore certificates after cool-down
- `K`, minimum rounds to wait from the start of cool-down before voting again
- `B`, extra chain weight per certificate
- `τ`, votes required for a quorum

Exact JSON and Haskell names follow the ledger package. Values in Phase 1 genesis are dormant configuration. They do not drive a live voting layer until the Phase 2 protocol version.

### Why this concerns wallets, explorers, indexers, and pool tools

**Block codecs and indexers.** A new optional field appears on the body. Decoders that reject unknown body fields will fail on any block that includes a cert, including Preview once test nodes start exercising the codec. Decoders that drop unknown fields will silently hide the cert that Phase 2 will depend on.

**PParams tables.** Seven new columns, or however the node groups them. Same "defined but not actuating" story as CIP-50's `null` leverage and CIP-23's zero margin.

**Wallets and dApps.** No Phase 1 product change. Confirmation times stay Praos. Do not advertise "2-minute finality" before Phase 2.

**SPOs.** No Phase 1 voting duty. Peras voting is a Phase 2 ops problem, with a separate node build and a separate testing window.

### What to update

1. Block body decoders: optional Peras certificate per CIP-140 CDDL.
2. PParams JSON and SQL: persist the seven parameters from protocol version 12.
3. Explorers: show the field as present or absent. Do not treat presence as "this block is Peras-settled" in Phase 1.
4. Docs and status pages: split "codec shipped" from "Peras active".
5. Plan Phase 2 work now, vote diffusion, cool-down UX, settlement APIs, but gate it on the intra-era version, not on Dijkstra day one.

***

## Breaking API changes

Why it was unavoidable, and what needs to be updated in response.

Block structure and new protocol parameters require a new era. That is the reason Peras is split across two phases.

### Wire and query contract

| Channel | Phase 1, protocol version 12 | Phase 2, intra-era bump |
| --- | --- | --- |
| Block body | Optional `peras_cert` bytes may appear. Ignored by chain selection. | Same bytes. Now input to chain weight and settlement. |
| Certificate CDDL | `voter_id`, `voting_round`, `block_hash`, VRF proof, weight, KES material as in CIP-140. Confirm frozen CDDL. | Unchanged codec. Live validation. |
| PParams | Peras keys present | Same keys, now actuating |
| Node-to-node | No Peras vote mini-protocol required | Vote diffusion required |
| Wallet confirmation API | Praos depths | May expose "Peras-boosted / settled" once specified |

### What to update

- Closed Conway block decoders.
- Any tool that hashes "the rest of the body after transactions" with a Conway layout. CIP-176 already rebuilt that layout. Peras is one more optional object on it.
- Constitution and guardrails if Peras parameters are to be changed before Phase 2. Likely unnecessary if they stay at genesis until activation.

***

## New features

What new capabilities it unlocks that you might want to start thinking about.

**At Phase 1:** only the ability to carry the bytes and the knobs. Use Preview and Preprod to round-trip certificates through indexers so Phase 2 is not the first time those parsers run.

**At Phase 2.** Plan now. Do not ship as Dijkstra-day UX.

- Settlement on the order of minutes for honest-majority-plus conditions, with a cool-down back to Praos-like behaviour if voting fails.
- Partner-chain and bridge designs that today wait for deep Praos prefixes.
- Explorer badges for boosted vs ordinary blocks.

Do not fold Linear Leios certificates and Peras certificates into one "consensus cert" type. Different crypto, different activation phase, different meaning.
