# Non-segregated Block Body Serialization

Since Shelley, a block body is segregated: all transaction bodies, then all witness sets, then auxiliary data, then validity flags. CIP-176 changes that to a sequence of whole transactions. In the ledger CDDL, each transaction in a block carries its own trailing validity flag.

The change is required so CIP-118 nested transactions and the extra block-body fields Leios and Peras need do not have to stitch child bodies, child witnesses, and parent witnesses across four parallel arrays.

* **CIP:** [CIP-176 Non-segregated Block Body Serialization](https://cips.cardano.org/cip/CIP-0176) (also [CIP-0176 on GitHub](https://github.com/cardano-foundation/CIPs/tree/master/CIP-0176))&#x20;
* **Overview:** [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), Non-segregated Block Body Serialization (CIP-176)&#x20;
* **Related:** [Remove isValid (CIP-167)](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/remove-isvalid-from-transactions), [Nested Transactions (CIP-118)](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/nested-transactions), [Peras codec extensions (CIP-140)](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/peras-codec-extensions)

***

## Core semantics changes

Implications, why it concerns you, and what needs to be updated in response.

### What the ledger actually does

Ledger validity of a transaction does not change. Only the bytes of the block change.

CIP-176 shape:

```
block =
  [ header
  , block_body
  ]
 
block_body =
  [ transactions      : [* block_transaction]
  , leios_certificate : leios_certificate/ nil
  , peras_certificate : peras_certificate/ nil
  ]
 
block_transaction =
  [transaction_body, transaction_witness_set, auxiliary_data/ nil, bool]
```

Each transaction is serialized in full before the next one. Validity is a per-transaction boolean, the last element of each `block_transaction`. It carries the same information as Conway's `invalid_transactions` index list. CIP-176 proposed keeping an index list; the ledger CDDL dropped it.

Consensus still uses the header's body hash over the new encoding. Block body size limits apply to the new layout.

### Why this concerns wallets, explorers, indexers, and pool tools

**Almost no wallet or dApp work.** Transaction construction and submit are unaffected. CIP text is explicit: only tools that encode or decode blocks move.

**Indexers, alternative nodes, Mithril, archive nodes, N2N chain-sync consumers, and block explorers that hash raw block CBOR** take a hard break. A Conway decoder on a Dijkstra block will read the first array as transaction bodies, when each element is actually a complete four-element transaction.&#x20;

The block body hash becomes a single hash over the serialized block\_body as a whole:

```
blockBodyHash = hash(block_body)
```

That breaks Mithril and any indexer that verifies blocks itself.

**Size estimators in block production.** Segregated layout made "how many more transactions fit?" a sum of four columns. Non-segregated size is the size of each complete transaction plus the index list. That is simpler, and it is why CIP-176 sits next to CIP-118.

### What to update

1. Block decoders in every language. Haskell ledger is the reference. Also pallas, gouroboros, cardano-multiplatform-lib, and similar.
2. Chain-sync and block-fetch test vectors and golden CBOR.
3. Explorer raw-block views and "copy CBOR" tools.
4. Tools that splice a transaction out of a block by walking the old body-array.
5. Any checksum or audit script that assumed Conway field order.

***

## Breaking API changes

Why it was unavoidable, and what needs to be updated in response.

Nested transactions make segregated serialization error-prone because offsets cross levels. Leios and Peras add optional certificate blobs to the body. Both want "append this object", not "append four slices in four arrays". Dijkstra is a new era, so the body CDDL can change once.

### Wire format

The block keeps its outer `[header, body]` split, but everything inside the body changes. Conway's five-element block, with bodies, witnesses, auxiliary data and invalid indices in parallel arrays, becomes `[header, block_body]`. The body is a list of complete transactions plus two optional certificates. There is no compatibility path. A Conway block decoder cannot read a Dijkstra block, and a Dijkstra one cannot read a Conway block, so block decoders must dispatch on era.

| CDDL rule | Change from Conway | What your tooling must do |
| --- | --- | --- |
| [`block`](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L3) | Was the [five-element Conway block](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/conway/impl/cddl/data/conway.cddl#L8-L14): `[header, transaction_bodies, transaction_witness_sets, auxiliary_data_set, invalid_transactions]`. Now `[header, block_body]`. | Dispatch on era before decoding. |
| [`block_body`](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L113-L117) | New. `[transactions, leios_certificate / nil, peras_certificate / nil]`. | Decode all three slots, even if you ignore the certificates. A three-element body is the normal case, not an error. |
| [`block_transaction`](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L8-L9) | New. A complete transaction, `[body, wits, aux / nil, bool]`, with the validity flag last. | Read validity from each transaction. The `invalid_transactions` list proposed in CIP-176 is not in the ledger CDDL. |
| [`header_body`](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L61-L74) | Adds `block_body_contains_leios_cert` and `eb_references_announcement`, and replaces `protocol_version` with `header_version_info`. | Header decoders change too. See [Ouroboros Linear Leios](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/ouroboros-linear-leios). |

**Not in the CDDL.**

* How the body hash is computed. In the ledger code (`hashBlockBody` in `Cardano.Ledger.Dijkstra.BlockBody`), `block_body_hash` is a hash of the serialized `block_body` as a whole. The CDDL comment beside that header field still says "merkle triple root", which is left over from Conway.
* Which slot holds what for a given block. For example, by protocol rule a block that carries a Leios certificate carries no transactions.

Links go to the Dijkstra CDDL at cardano-ledger commit [`8631831`](https://github.com/IntersectMBO/cardano-ledger/tree/863183157cc39c48615078eab85389766bdc695b) (23 November 2026). The CDDL is not frozen yet, so check the line before relying on it.

### Wire and query contract

| Channel                       | Conway, segregated                        | Dijkstra, CIP-176                                                                      |
| ----------------------------- | ----------------------------------------- | -------------------------------------------------------------------------------------- |
| Block shape                   | `[header, bodies, witness sets, auxiliary data map, invalid indices]` | `[header, block_body]`                                                     |
| Body slot 0                   | not applicable                            | `[* block_transaction]` complete transactions                                          |
| Body slots 1 and 2            | not applicable                            | `leios_certificate / nil`, `peras_certificate / nil`                                   |
| Transaction object in a block | split across arrays                       | one CBOR item, `[body, wits, aux / nil, bool]`. The flag is last.                     |

JSON APIs that already return `{header, transactions[]}` are fine if they rebuild from the new CBOR. APIs that return the four Conway arrays must version their schema.

### What to update

* Ogmios and N2C block schemas.
* DBSync block ingest.
* Checkpoints and snapshot formats that embed raw bodies.

***

## New features

What new capabilities it unlocks that you might want to start thinking about.

No user-facing feature. It is the encoding that lets the era do three other jobs:

* nested transactions without a combinatorial serialization spec,
* Leios certificates and Peras certificates as ordinary body fields,
* simpler "does this transaction still fit in the block?" arithmetic.

If you only build and submit transactions, you can ignore this page. If you parse blocks, this is the first Dijkstra ticket to land in your codec.
