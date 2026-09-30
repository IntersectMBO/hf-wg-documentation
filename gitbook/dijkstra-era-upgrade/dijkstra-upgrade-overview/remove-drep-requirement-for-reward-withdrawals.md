# Remove DRep Requirement for Reward Withdrawals

Conway, after the bootstrap / Plomin era, rejects a reward withdrawal if the stake credential is not delegated to a registered DRep, to Abstain, or to No Confidence. Tooling surfaces this as `ConwayWdrlNotDelegatedToDRep` or Ogmios `ForbiddenWithdrawal`.

CIP-181 deletes that check. A withdrawal that is otherwise valid is accepted whether or not the account has a voting delegation.

This is a relaxation. Every withdrawal that worked in Conway still works. Withdrawals that Conway rejected solely for missing DRep delegation start working at the Dijkstra hard fork. There is no new parameter and no dormant flag.

**CIP:** [CIP-181 Remove DRep Requirement for Reward Withdrawals](https://cips.cardano.org/cip/CIP-0181) (also [CIP-0181 on GitHub](https://github.com/cardano-foundation/CIPs/tree/master/CIP-0181))
**Overview:** [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), Remove DRep Requirement for Reward Withdrawals (CIP-181)
**Related but different:** [Account Address Enhancement, Phase 1 (CIP-159)](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/account-address-enhancement-phase-1) changes how accounts receive and assert balances. CIP-181 only changes a Conway governance gate on withdrawals.

***

## Core semantics changes

Implications, why it concerns you, and what needs to be updated in response.

### What the ledger actually does

Remove the withdrawal-time test that required a DRep, Abstain, or No-Confidence delegation. Other withdrawal rules stay. The account must be registered, the amount must be available, witnesses must satisfy the stake credential, and balancing must hold.

Governance itself is unchanged. DRep registration, vote delegation certificates, and voting power are untouched. An ada holder can still postpone choosing a DRep and still withdraw.

### Why this concerns wallets, explorers, indexers, and pool tools

**Wallets and custodians.** Many UIs currently block "Claim rewards" and push a DRep picker first. That gate becomes a product choice, not a ledger requirement. Leaving it in place after protocol version 12 will confuse users whose CLI withdrawal just works.

**Exchanges.** Cold-wallet reward sweeps that failed for "not delegated to a DRep" start succeeding. Ops runbooks should drop that error as a hard stop.

**Governance analytics.** Participation metrics that treated "has withdrawn" as "has delegated" were always a bit wrong. After CIP-181 they are useless for that inference.

**This is live on hard-fork day.** No Parameter Change is required.

### What to update

1. Wallet copy and flow: claiming rewards must not require a DRep step. Offering delegation as an optional next action is fine.
2. Error handling: stop mapping `ConwayWdrlNotDelegatedToDRep` / `ForbiddenWithdrawal` as an expected Dijkstra failure.
3. Docs, FAQs, and support macros written during the Conway bootstrap.
4. Hardware and custodial policies that encoded the Conway rule as an internal invariant.
5. Do not change DRep delegation certificate builders. They remain how voting power is assigned.

***

## Breaking API changes

Why it was unavoidable, and what needs to be updated in response.

The change is a deleted predicate, so encodings do not grow. The break is behavioural. Submit paths and tests that expected a failure now get a success.

### Wire and query contract

| Channel | Shape |
| --- | --- |
| Withdrawal field | Unchanged `{reward_account → coin}` in Phase 1 |
| Certificates | Unchanged |
| PParams | No new key |
| Errors | `ConwayWdrlNotDelegatedToDRep` must not fire in Dijkstra |
| Queries | `query stake-address-info` still reports delegation. It no longer predicts withdrawability. |

### What to update

- Integration tests that submit a withdrawal without a DRep and expect rejection.
- Ogmios and submit-api error catalogues.
- Analytics jobs that classify "undelegated-and-unwithdrawable" accounts.

***

## New features

What new capabilities it unlocks that you might want to start thinking about.

- **Decoupled staking and voting.** Delegate to an SPO, leave voting undecided, still take rewards home.
- **Less coerced convenience delegation.** Wallets no longer have a protocol-level reason to pre-select a DRep so the user can click Claim.
- **Cleaner CIP-159 story.** Micropayment accounts can withdraw without first becoming governance actors.

CIP-181 does not pay anyone extra and does not change RSS. It only unlocks funds the protocol had already credited.
