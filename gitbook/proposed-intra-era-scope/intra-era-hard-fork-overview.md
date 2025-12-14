# Intra-era hard fork overview

Intersect plays the role of coordinator, as a functional servant-leader on behalf of the community and delivery teams working on hard fork activity. The functional teams within Intersect will work with the various committees, working groups, and delivery teams, relaying information here on the knowledge base. Ultimately the date for the hard fork is directly influenced by the community, the relevant constitutional approval and required on-chain voting.

***

## Upgrade Release

#### **Plutus upgrades**

1. All built-in functions are available across Plutus V1, V2, and V3:\
   Expanding the capabilities of Plutus V1 and V2 scripts and unifying the feature availability across versions.
2. case Expressions for built-in types:\
   Enables case expressions on Bool, Integer, and Data within UPLC. Provides significant performance improvements and cleaner script logic. Addresses one of the major performance bottlenecks in data matching.
3. New built-ins and native types:

* [CIP-138 | Array type](https://cips.cardano.org/cip/CIP-138) – adding efficient, native on-chain array handling
* [CIP-153 | MaryEraValue type](https://cips.cardano.org/cip/CIP-153) – optimised multi-asset value operations
* [CIP-109 | Modular exponentiation builtin](https://cips.cardano.org/cip/CIP-109) – critical for advanced crypto
* [CIP-132 | dropList builtin](https://cips.cardano.org/cip/CIP-132) – efficient list manipulation
* [CIP-133 | Multi-scalar multiplication over BLS12-381](https://cips.cardano.org/cip/CIP-133) – useful for advanced cryptographic operations, specifically with zero-knowledge proof systems

All of these new builtins will be introduced across all Plutus versions. Collectively, these changes increase script performance, reduce execution cost, and meaningfully extend what builders can accomplish in Plutus.

#### **Ledger and Cardano Node enhancements**

VRF Key uniqueness enforcement:

* Ensures no two stake pools reuse the same VRF key
* Strengthens pool security and mitigates possible attack vectors
* This means that from the point of hardfork, VRK key hash uniqueness is enforced at the ledger level

Revised reference input rules for Plutus V1/V2:

* Adjusts predicate checks that previously caused issues for scripts using reference inputs
* This fixes a scenario where&#x20;

Constitutional Committee voting restriction moved to a ledger rule:

* Shifts a mempool-only check into a proper ledger predicate failure
* Improves transparency and governance correctness

Non-matching withdrawals predicate:

* Clearer error messaging and safer validation of withdrawal structures

Improved protocol parameter hash mismatch reporting:

* Better diagnostics when PPView hashes differ
* Helps operators identify and resolve configuration issues quickly

***

## Governance Actions

To be determined

***

## Delegating

A key part of the governance model is delegating. Delegating is the act of 'loaning' your Voting Power - which equals ADA the balance in your wallet - to someone else. The person or organisation that you delegate to are called DReps, which is short for "Delegate Representatives". DReps represent you in a similar way as a parliamentary or congressional representative does in an analog government. Simply put, they vote on your behalf.

It is recommended you participate and delegate to a DRep ahead of the intra-era upgrade mainnet hard fork.
