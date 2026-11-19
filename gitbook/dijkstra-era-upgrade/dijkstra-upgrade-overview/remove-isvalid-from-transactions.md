# Remove isValid from Transactions

Standalone mempool, submit, and N2C transaction CBOR in Conway is a four-tuple:

`[transaction_body, transaction_witness_set, isValid, auxiliary_data / nil]`

`isValid` is not signed, not part of the transaction ID, and not what consensus uses when the transaction sits in a block. Anyone can flip it on the wire. For remote submissions from untrusted nodes, the node ignores the submitted value. It evaluates the transaction as valid, and if phase-2 fails for that reason alone it admits the transaction to the mempool with `isValid = false` so collateral can be collected. For trusted local submissions, the node reads the flag to help prevent unintended collateral collection.

CIP-167 deletes the flag from the standalone encoding. Block encoding is a separate story. Conway already stores validity outside the transaction object, and CIP-176 rewrites the block body anyway.

**CIP:** [CIP-167 Remove isValid from transactions](https://cips.cardano.org/cip/CIP-0167) (also [CIP-0167 on GitHub](https://github.com/cardano-foundation/CIPs/tree/master/CIP-0167), PR [cardano-foundation/CIPs#1089](https://github.com/cardano-foundation/CIPs/pull/1089))
**Overview:** [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), Remove isValid from Transactions (CIP-167)
**Ledger PR (merged):** [cardano-ledger#5480](https://github.com/IntersectMBO/cardano-ledger/pull/5480) (2025-12-22)
**Follow-up:** [cardano-ledger#5605](https://github.com/IntersectMBO/cardano-ledger/issues/5605) drops the transitional decoder that still accepts `isValid = true`.

GitBook `SUMMARY.md` currently lists this stub as `remove-isvalid-from-transactionsto-be-added.md`. Rename that file when you land this page. See the install notes.

***

## Core semantics changes

Implications, why it concerns you, and what needs to be updated in response.

### What the ledger actually does

Starting in Dijkstra:

- Serialize standalone transactions without the boolean.
- Deserialize standalone transactions without the boolean and treat them as `isValid = true` at the type level.
- Transitional deserialize: a Conway-shaped four-tuple is still accepted at the hard fork if and only if the boolean is `true`. That is so in-flight mempool entries survive the fork. A four-tuple with `false` is not accepted as a Dijkstra standalone transaction.
- Later eras will drop the transitional decoder (#5605).

On-chain behaviour of collateral and failed scripts does not change. Consensus still decides which transactions in a block are applied vs collateral-only. CIP-176's block body carries an `invalid_transactions` index list for that.

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

### Wire and query contract

| Channel | Conway | Dijkstra |
| --- | --- | --- |
| Standalone `transaction` | `[body, wits, bool, aux / nil]` | `[body, wits, aux / nil]` |
| Transitional Dijkstra decode | not applicable | `[body, wits, true, aux / nil]` also accepted |
| `[body, wits, false, aux]` | Conway valid encoding | Not a valid Dijkstra standalone transaction |
| TxId | Unchanged. The flag was never hashed. | Unchanged |
| Block body | Separate CIP-176 layout | `invalid_transactions` indices plus full transactions |

JSON query APIs that expose `isValid` on a submitted transaction should either drop the field or document it as node-computed, not user-supplied.

### What to update

- Golden files and compact-cddl packages.
- Submit endpoints that echo the raw CBOR they accepted.
- Any "phase-2 expected to fail" helper that uses the flag for trusted local submission: adapt it to the supported submission interface while preserving protection against unintended collateral collection.

***

## New features

What new capabilities it unlocks that you might want to start thinking about.

None for end users. This is a simplification:

- one less ambiguous bit on the wire,
- slightly smaller submit CBOR,
- a single story: the node decides validity, the block records which transactions were invalid.

Pair this page with CIP-176 when updating block and mempool codecs. Pair it with CIP-118 when encoding children. Sub-transactions already omit the flag.
