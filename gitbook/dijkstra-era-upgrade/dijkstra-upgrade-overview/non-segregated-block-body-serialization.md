# Non-segregated Block Body Serialization

Since Shelley, a block body is segregated: all transaction bodies, then all witness sets, then auxiliary data, then validity flags. CIP-176 changes that to a sequence of whole transactions, plus a list of indices of invalid, collateral-only transactions.

The change is required so CIP-118 nested transactions and the extra block-body fields Leios and Peras need do not have to stitch child bodies, child witnesses, and parent witnesses across four parallel arrays.

**CIP:** [CIP-176 Non-segregated Block Body Serialization](https://cips.cardano.org/cip/CIP-0176) (also [CIP-0176 on GitHub](https://github.com/cardano-foundation/CIPs/tree/master/CIP-0176))
**Overview:** [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), Non-segregated Block Body Serialization (CIP-176)
**Related:** [Remove isValid (CIP-167)](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/remove-isvalid-from-transactions), [Nested Transactions (CIP-118)](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/nested-transactions), [Peras codec extensions (CIP-140)](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/peras-codec-extensions)

***

## Core semantics changes

Implications, why it concerns you, and what needs to be updated in response.

### What the ledger actually does

Ledger validity of a transaction does not change. Only the bytes of the block change.

CIP-176 shape:

```
block = [ header, block_body ]

block_body =
  [ invalid_transactions : [* transaction_index]
  , transactions         : [* transaction]
  ]
```

Each `transaction` is serialized in full before the next one. Validity is not a per-transaction boolean inside those objects. It is the `invalid_transactions` index list, the same information Conway stored as a parallel `isValid` array.

Consensus still uses the header's body hash over the new encoding. Block body size limits apply to the new layout.

### Why this concerns wallets, explorers, indexers, and pool tools

**Almost no wallet or dApp work.** Transaction construction and submit are unaffected. CIP text is explicit: only tools that encode or decode blocks move.

**Indexers, alternative nodes, Mithril, archive nodes, N2N chain-sync consumers, and block explorers that hash raw block CBOR** take a hard break. A Conway body decoder on a Dijkstra block will read the first array as "transaction bodies" when it is actually the invalid-index list.

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

### Wire and query contract

| Channel | Conway, segregated | Dijkstra, CIP-176 |
| --- | --- | --- |
| Body slot 0 | `[* transaction_body]` | `[* transaction_index]` invalid set |
| Body slot 1 | `[* witness_set]` | `[* transaction]` complete transactions |
| Later slots | auxiliary data, isValid flags, era extras | not used for those. Extras such as a Peras cert or Leios cert attach per the era CDDL. |
| Transaction object in a block | split across arrays | one CBOR item. Under CIP-167 it has no standalone `isValid`. |

JSON APIs that already return `{header, transactions[]}` are fine if they rebuild from the new CBOR. APIs that return the four Conway arrays must version their schema.

### What to update

- Ogmios and N2C block schemas.
- DBSync block ingest.
- Checkpoints and snapshot formats that embed raw bodies.

***

## New features

What new capabilities it unlocks that you might want to start thinking about.

No user-facing feature. It is the encoding that lets the era do three other jobs:

- nested transactions without a combinatorial serialization spec,
- Leios certificates and Peras certificates as ordinary body fields,
- simpler "does this transaction still fit in the block?" arithmetic.

If you only build and submit transactions, you can ignore this page. If you parse blocks, this is the first Dijkstra ticket to land in your codec.
