# Dijkstra upgrade overview

## Scope

#### [CIP-164 Leios](https://cips.cardano.org/cip/CIP-0164)

Ouroboros Leios, an optimistic consensus protocol designed for high-throughput operation while preserving Ouroboros Praos security properties. Block producers simultaneously create both a standard Praos block and a larger secondary block referencing additional transactions. Secondary blocks undergo committee validation before ledger inclusion, enabling significantly higher throughput.

#### [CIP-140 Peras](https://cips.cardano.org/cip/CIP-0140)

Ouroboros Peras, an enhancement to the Ouroboros Praos protocol that introduces a voting layer for fast settlement. It is adaptively secure, supports dynamic participation, and integrates self healing. Voting provides a “boost” to blocks that receive a quorum of votes, and this dramatically reduces the roll-back probability of the boosted block and its predecessors.

#### [CIP-118: Nested transactions](https://cips.cardano.org/cip/CIP-0118)

A set of changes that revolve around nested transactions, a construct for composing certain kinds of _partially valid transactions_, such as unbalanced transactions, or transactions with missing fees. The missing value or data must be provided by a subsequent transaction. Such partially valid transactions, which are called sub-transactions, must be placed into batches by aggregators. The batch must also include a _top-level_ transaction. The completed batch must be fully balanced. Applying a complete batch results in a valid ledger update, however, applying each of the individual transactions would not be possible.

#### [CIP-159 phase 1: Accounts Enhancements](https://cips.cardano.org/cip/CIP-0159)

Currently, Cardano's account addresses (a.k.a. reward addresses) can only be used for receiving ADA from the Cardano protocol (e.g., staking rewards). Users are not allowed to deposit assets into these addresses. By removing this restriction, and enabling very specific plutus script support, Cardano can unlock new use cases **without sacrificing local determinism**. And by still requiring UTxO inputs in transactions, these accounts avoid many of the pitfalls from Ethereum-style accounts.

<mark style="color:$info;">Phase 1 scope to be explained</mark>

#### [CIP-112 Guard scripts](https://cips.cardano.org/cip/CIP-0112)

Introduce a new Plutus scripts type `Observe` in addition to those currently available (spending, certifying, rewarding, minting, drep). The purpose of this script type is to allow arbitrary validation logic to be decoupled from any ledger action. Since observe validators are decoupled from actions, you can run them in a transaction without needing to perform any associated action (ie you don't need to consume a script input, or mint a token, or withdraw from a staking script just to execute this validator).

#### [CIP-181 Remove DRep delegation Requirement for Reward Withdrawals](https://cips.cardano.org/cip/CIP-0181)

Removes the requirement that a reward withdrawal be conditioned on governance voting delegation. Under the current Conway governance regime introduced by [CIP-1694](https://cips.cardano.org/cip/CIP-1694), rewards continue to accrue normally, but after the bootstrap phase a reward account may be prevented from withdrawing unless its stake credential is delegated for voting to a registered DRep or one of the predefined voting options.

#### Fee function update (No CIP) -> Reference inputs

To be added

#### PlutusV4 context

To be added

#### Reference script pricing and limits

To be added

#### [CIP-167 Remove isValid from transactions](https://cips.cardano.org/cip/CIP-0167)

Removing the `isValid` boolean from the CBOR encoding of standalone transactions (e.g. for mempool). This would not affect the serialization of the transactions within blocks, since isValid flag is already stored separately from the transaction.

#### [CIP-176 Non-segregated Block Body Serialization](https://cips.cardano.org/cip/CIP-0176)

Changing the CBOR encoding of a block body from a segregated layout to a plain sequence of transactions. Current layout: all transaction bodies are concatenated and encoded first, followed by their witness sets, then followed by auxiliary-data hashes, and finally followed by validity flags. Proposed layout: each transaction is serialized in full before the next transaction is written to the stream.

#### [CIP-23 (Part-1) Fair Min Fees (minPoolMargin)](https://cips.cardano.org/cip/CIP-0023)

Introduces a new protocol parameter, `minPoolMargin`, which specifies a lower bound on the variable fee (margin) a stake pool may set. The parameter is introduced initially set to `0` to avoid disrupting existing pool certificates. This proposal does not change or reduce the existing minimum fixed pool fee (`minPoolCost`).

<mark style="color:$info;">Part 1 scope to be explained</mark>

#### [CIP-050 Pledge Leverage-Based Staking Rewards (maxPledgeLeverage, L)](https://cips.cardano.org/cip/CIP-0050)

Introduces a new pledge leverage parameter, _L_, into the RSS to more directly and fairly constrain such under-pledged pools. By capping rewards for pools with excessive stake relative to pledge, _L_ penalizes severely under-pledged pools while having minimal effect on well-pledged or small pools. The adjusted scheme aligns economic incentives with decentralization: it redistributes stake toward well-pledged pools (increasing their rewards) and makes it more difficult for single entities to dominate via multiple pools.

## Timeline

***

#### Product Committee Reference plan

{% embed url="https://product.cardano.intersectmbo.org/hardfork-planning/dijkstra/" %}
