# Remove isValid from Transactions

CIP-167 deletes the flag from the standalone (mempool) encoding. Block encoding is a separate story. Conway keeps validity outside the transaction object, as an `invalid_transactions` index list. The Dijkstra ledger CDDL instead moves the flag to the end of each transaction inside a block. See [Wire format](#wire-format).

```
mempool_transaction = [transaction_body, transaction_witness_set, auxiliary_data/ nil] / [transaction_body, transaction_witness_set, true, auxiliary_data/ nil]
```

* **CIP:** [CIP-167 Remove isValid from transactions](https://cips.cardano.org/cip/CIP-0167) (also [CIP-0167 on GitHub](https://github.com/cardano-foundation/CIPs/tree/master/CIP-0167), PR [cardano-foundation/CIPs#1089](https://github.com/cardano-foundation/CIPs/pull/1089))
* **Overview:** [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), Remove isValid from Transactions (CIP-167)&#x20;
* **Ledger PR (merged):** [cardano-ledger#5480](https://github.com/IntersectMBO/cardano-ledger/pull/5480) (2025-12-22)&#x20;
* **Follow-up:** [cardano-ledger#5605](https://github.com/IntersectMBO/cardano-ledger/issues/5605) drops the transitional decoder that still accepts `isValid = true`.

***

## Core semantics changes

Implications, why it concerns you, and what needs to be updated in response.

### What the ledger actually does

Starting in Dijkstra:

* Serialize standalone transactions without the boolean.
* Deserialize standalone transactions without the boolean and treat them as `isValid = true` at the type level.
* Transitional deserialize: a Conway-shaped four-tuple is still accepted at the hard fork if and only if the boolean is `true`. That is so in-flight mempool entries survive the fork. A four-tuple with `false` is not accepted as a Dijkstra standalone transaction.
* Later eras will drop the transitional decoder (#5605).

On-chain behaviour of collateral and failed scripts does not change. The block producer still decides which transactions in a block are applied and which are collateral-only, and the ledger checks that decision. In Dijkstra each `block_transaction` records it as a trailing `bool`. The `invalid_transactions` index list proposed in CIP-176 was dropped from the ledger CDDL.

### Why this concerns wallets, explorers, indexers, and pool tools

**Submit and mempool codecs.** Wallets, bot backends, Ogmios submit, cardano-cli, and hardware-bridge middleware that always write the four-tuple will produce CBOR the Dijkstra mempool must either transitional-decode or reject.

**Indexers that parse standalone transactions.** Mempool monitors and "seen in mempool" explorers will read the third array element as auxiliary data if they still expect a bool.

**Libraries that let the user set `isValid = false` on a constructed transaction** must distinguish validity intent for trusted local submission from node-computed validity. Remove the flag from Dijkstra standalone serialization, and preserve local-submission safeguards through the submission interface as supported by the node.

**Block parsers** follow CIP-176, not this CIP. Do not mix the two tickets.

### What to update

1. Every CBOR encoder for "transaction as submitted": drop the boolean.
2. Every CBOR decoder: accept 3-element arrays. Optionally accept 4-element with `true` during the Dijkstra era only.
3. Cardano API, CSL, pallas, and Trezor or Ledger transaction serialize paths.
4. Tests and golden CBOR.
5. Docs and SDK examples that show `isValid` on the submit object.

***

## Breaking API changes

Why it was unavoidable, and what needs to be updated in response.

The standalone tuple is a public encoding. Changing its arity is visible to every submitter. Doing it in a new era is the honest option. The unsigned flag is ignored for remote submissions, while trusted local submissions use it as a safeguard; that intent needs to be handled by the submission interface when the flag is removed.

### Wire format

The validity flag moves rather than disappears. A submitted transaction loses it. A transaction inside a block regains it as a fourth, trailing element, after the auxiliary data rather than before it. So the same three-element prefix appears in both places, and a decoder has to know which context it is reading. A Conway decoder applied to either form will misread the third element.

| CDDL rule | Change from Conway | What your tooling must do |
| --- | --- | --- |
| [`mempool_transaction`](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L21-L24) | Replaces Conway's [`transaction`](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/conway/impl/cddl/data/conway.cddl#L16-L17), `[body, wits, bool, aux / nil]`. Now `[body, wits, aux / nil]`. The Conway four-element form is still accepted, but only with `true`. | Encode three elements. Decode both forms during Dijkstra, and reject `false`. |
| [`block_transaction`](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L8-L9) | New. `[body, wits, aux / nil, bool]`: the flag is last, and is set by the block producer. | Block decoders read four elements in this order. Do not reuse the Conway `transaction` decoder. |
| [`sub_transaction`](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L829-L830) | New, and never carries a flag. | See [Nested Transactions](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/nested-transactions). |

**Not in the CDDL.** These points are about how the encoding is used, not its shape:

* The transaction ID is the hash of the body alone, so it does not depend on the flag.
* The transitional four-element decoder is planned to go in the next era ([cardano-ledger#5605](https://github.com/IntersectMBO/cardano-ledger/issues/5605)). The CDDL comment says encoders should drop the flag now.
* The ledger CDDL has dropped the `invalid_transactions` list proposed in CIP-176. Follow the ledger CDDL, not the CIP text.

Links go to the Dijkstra CDDL at cardano-ledger commit [`8631831`](https://github.com/IntersectMBO/cardano-ledger/tree/863183157cc39c48615078eab85389766bdc695b) (23 November 2026). The CDDL is not frozen yet, so check the line before relying on it.

### Wire and query contract

| Channel                      | Conway                                | Dijkstra                                              |
| ---------------------------- | ------------------------------------- | ----------------------------------------------------- |
| Standalone `transaction`     | `[body, wits, bool, aux / nil]`       | `[body, wits, aux / nil]`                             |
| Transitional Dijkstra decode | not applicable                        | `[body, wits, true, aux / nil]` also accepted         |
| `[body, wits, false, aux]`   | Conway valid encoding                 | Not a valid Dijkstra standalone transaction           |
| TxId                         | Unchanged. The flag was never hashed. | Unchanged                                             |
| Block body                   | `invalid_transactions` index list     | Each `block_transaction` ends with its own `bool`     |

JSON query APIs that expose `isValid` on a submitted transaction should either drop the field or document it as node-computed, not user-supplied.

### What to update

* Golden files and compact-cddl packages.
* Submit endpoints that echo the raw CBOR they accepted.
* Any "phase-2 expected to fail" helper that uses the flag for trusted local submission: adapt it to the supported submission interface while preserving protection against unintended collateral collection.

***

## New features

What new capabilities it unlocks that you might want to start thinking about.

None for end users. This is a simplification:

* one less ambiguous bit on the wire,
* slightly smaller submit CBOR,
* a single story: the node decides validity, the block records which transactions were invalid.

Pair this page with CIP-176 when updating block and mempool codecs. Pair it with CIP-118 when encoding children. Sub-transactions already omit the flag.
