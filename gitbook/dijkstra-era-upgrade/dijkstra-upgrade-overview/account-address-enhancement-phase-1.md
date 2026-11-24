# Account Address Enhancement, Phase 1

Cardano already has account addresses, also called reward or stake addresses. Until Dijkstra they can receive ADA only from the protocol: staking rewards, refunds, treasury. CIP-159 Phase 1 lets a user transaction deposit ADA directly into a registered reward account, and lets a transaction assert bounds on that account's ADA balance.

Value can move without creating a new UTxO that has to carry `minUTxO`. Phase 1 is ADA only. Multi-asset accounts, whitelists, and `accountWhitelistCostPerByte` are Phase 2 / Euler-era work. The overview parks the multi-asset treasury CIP on that later foundation.

* **CIP:** [CIP-159 Account Address Enhancement](https://cips.cardano.org/cip/CIP-0159) (also [CIP-0159 on GitHub](https://github.com/cardano-foundation/CIPs/tree/master/CIP-0159))
* **Overview:** [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), Account Address Enhancement, Phase 1 (CIP-159)
* **Product write-up:** [Cardano Upgrades initiative](https://momentum.cardano.iog.io/proposals/cardano-upgrades)
* **Related:** [Nested Transactions (CIP-118)](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/nested-transactions) covers partial withdrawals in children. [Remove DRep requirement (CIP-181)](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/remove-drep-requirement-for-reward-withdrawals) is a separate withdrawal-permission change

***

## Core semantics changes

Implications, why it concerns you, and what needs to be updated in response.

### What the ledger actually does

Two new transaction-body maps, ADA-only in Phase 1:

* `direct_deposits`: `reward_account → coin`. Credits that many lovelace to a registered reward account. The receiving account does not witness the deposit. Same rule as sending to a UTxO script address.
* `account_balance_intervals`: `reward_account → interval`. Phase-1 validation checks the account's ADA balance, as this level of the transaction sees it, against the interval. Failure is phase-1. Intervals are evaluated before that level's certificates, withdrawals, and direct deposits, independently at the top level and in each CIP-118 child. Because children run first, the parent's interval sees balances after the children have already moved them.

Withdrawals remain `reward_account → coin` in Phase 1, but partial withdrawals are now a first-class need. If two transactions both try to drain "the whole balance" they race. Wallets should withdraw a declared amount where partial withdrawals are supported. A top-level transaction using PlutusV1 to V3 must still withdraw the full account balance; CIP-118 can isolate a partial withdrawal in a child without those legacy scripts.

Balancing includes direct deposits. ADA written into an account is ADA that left the UTxO side of the batch.

No new script purpose. Account scripts that already guard withdrawals keep using the rewarding / withdraw purpose. There is no "receiving" purpose in Phase 1. That idea lives in CIP-160, which is not in Dijkstra.

### Why this concerns wallets, explorers, indexers, and pool tools

**Wallets.** This is the change Begin Wallet and others asked for: charge 0.1 ADA for a convenience feature instead of being forced through a \~1 ADA min-UTxO output. Balance UX must show UTxO spendable and account spendable as two numbers, and must support "send to `$stake_address`" as a deposit, not as a malformed payment address.

**Custodians and exchanges.** Incoming ADA may now land on a reward account. Deposit-detection that only watches payment-address UTxOs will miss customer funds.

**Indexers.** Account balances stop being "rewards minus withdrawals". They become a live ledger balance that user transactions credit and debit. Reward-history tables are not enough.

**dApps and batchers.** Aggregators can collect micro-fees into one account instead of accumulating thousands of dust UTxOs. Combine with CIP-118 so the user's child does not have to hold min-ADA.

**Plutus.** V4 context exposes `txInfoDirectDeposits` and `txInfoAccountBalanceIntervals`. Scripts that assume "the only account movement is a withdrawal map" are incomplete.

### What to update

1. Address entry in wallets: accept stake / reward addresses as destinations for ADA deposits.
2. Balance and portfolio views: split liquid UTxO vs account. Do not hide deposits inside "unclaimed rewards".
3. Withdrawal builders: support amount-based partial withdrawals where permitted; retain full-balance withdrawals for top-level transactions using PlutusV1 to V3. Tolerate CIP-181, no DRep required, as a separate change.
4. Indexer schemas: `direct_deposits` events, running account balance, interval fields on transactions.
5. Explorers: account pages need a full credit and debit history, not only RSS payouts.
6. SDKs: encode the two new maps. Include them in fee and balance calculations.
7. Do not implement Phase-2 whitelist certificates or multi-asset `Value` in these maps for protocol version 12.

***

## Breaking API changes

Why it was unavoidable, and what needs to be updated in response.

Conway transaction bodies and Conway `TxInfo` have no slots for user-initiated account credits or balance assertions. Those slots only exist in a new era.

### Wire format

Dijkstra adds three keys to the transaction body. They are all maps keyed by a full `reward_account`, which carries its network in the header byte, not by a bare credential. A Conway decoder rejects any transaction that uses them. Two details are easy to get wrong. First, balance intervals have three CBOR shapes, not one. Second, the third map exists only on the top-level transaction, and it is checked against balances before any child runs.

| CDDL rule | Change from Conway | What your tooling must do |
| --- | --- | --- |
| [`transaction_body` key 25, `direct_deposits`](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L856) | New. `{+ reward_account => coin}`, on the top level and in children. | Encode as a non-empty map. Count deposits as value leaving the UTxO side when balancing. |
| [`transaction_body` key 26, `account_balance_intervals`](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L858) | New. `{+ reward_account => account_balance_interval}`, on the top level and in children. | Checked against the account balance as that level sees it. |
| [`account_balance_interval`](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L860-L863) | New. Either `[lower, upper / nil]`, `[lower / nil, upper]` or a bare `coin` for an exact balance. The lower bound is inclusive and the upper bound exclusive. | Support all three shapes when decoding. Never encode `[nil, nil]`, which the rule does not allow. |
| [`transaction_body` key 27, `starting_account_balance_intervals`](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L937-L938) | New, top level only. Same value type. | Use it when the parent needs to assert balances from before the children ran. A child that carries key 27 is malformed. |
| [`withdrawals`](https://github.com/IntersectMBO/cardano-ledger/blob/863183157cc39c48615078eab85389766bdc695b/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L565) | Unchanged. | No codec change. |

**Not in the CDDL.** The ledger, not the codec, enforces these:

* Every account named in a deposit or interval must be registered, and must be on the right network. For deposits the errors are `DirectDepositAccountsMissing` and `DirectDepositAddressesWithWrongNetwork`. For intervals they are `MissingAccountsIn...` and `WrongNetworkIn...`.
* A balance outside the interval is a phase-1 failure (`BalancesOutside...`).
* The rule that a PlutusV1–V3 top level must withdraw the full balance.

Links go to the Dijkstra CDDL at cardano-ledger commit [`8631831`](https://github.com/IntersectMBO/cardano-ledger/tree/863183157cc39c48615078eab85389766bdc695b) (23 November 2026). The CDDL is not frozen yet, so check the line before relying on it.

### Wire and query contract

| Channel                     | Shape in Phase 1                                                                                       |
| --------------------------- | ------------------------------------------------------------------------------------------------------ |
| `direct_deposits`           | map `reward_account → coin`.                                                                           |
| `account_balance_intervals` | map `reward_account →` ADA interval (exact, lower, upper, or both)                                     |
| `starting_account_balance_intervals` | Top level only. Same shape, checked against balances before any child runs. |
| Withdrawals                 | still `reward_account → coin`                                                                          |
| Ledger account state        | ADA balance that user transactions may credit                                                          |
| PlutusV4 `TxInfo`           | `txInfoDirectDeposits`, `txInfoAccountBalanceIntervals`, ADA-only types                                |
| Query APIs                  | Reward-account queries must return the live spendable account balance, not only "rewards due from RSS" |

CDDL field numbers collided across CIP drafts. Bindings should follow the ledger CDDL (keys 25, 26 and 27; see [Wire format](#wire-format)), not the CIP README numbers.

### What to update

* cardano-cli: deposit and interval flags, and `query stake-address-info` semantics.
* Ogmios, Koios, GraphQL: new transaction fields and account-balance queries.
* Hardware wallets: display "deposit N ADA to stake account X".
* Any tool that treated a reward address as receive-only.

***

## New features

What new capabilities it unlocks that you might want to start thinking about.

* **Micropayments and micro-fees.** Wallet-feature fees, per-request API fees, and batcher tips that were uneconomic under min-UTxO become ordinary account credits.
* **Single-sink treasuries, ADA only.** A project can publish one reward address and collect many small payments into one balance, then withdraw as needed.
* **Safer concurrent use.** Intervals let a transaction fail phase-1 if the account is not in the expected band. That substitutes for some UTxO-concurrency patterns on the account side.
* **L2 and bridge reserves, ADA only in Phase 1.** The initiative text flags L2 reserve management as a target. Phase 1 only holds ADA. Do not advertise multi-asset reserves as a Dijkstra feature.
* **Works with nested transactions.** A child can deposit or partially withdraw. The parent can assert the interval that should hold after the children.

Phase 2 (multi-asset, whitelist certificates, `AccountValue`) is not Dijkstra Phase 1. CPS-0023 multi-asset treasury was deferred for that reason.
