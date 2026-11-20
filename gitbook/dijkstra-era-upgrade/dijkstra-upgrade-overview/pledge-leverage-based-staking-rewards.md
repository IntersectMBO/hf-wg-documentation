# Pledge Leverage-Based Staking Rewards

At the Dijkstra Phase 1 hard fork the ledger grows a new protocol parameter, `maxPledgeLeverage` (CIP-50's *L*). It ships as `Nothing` in Dijkstra genesis, so CIP-50 preserves the current Shelley reward formula for identical inputs. No redelegation event or zero-pledge penalty is introduced by CIP-50 at the hard fork. Once the Constitution and guardrails permit it, a later Parameter Change governance action can set *L* to a concrete value; only then is the cap enabled and rewards attributable to subsequent block production become zero for zero-pledge pools.

This is not CIP-23 (`minPoolMargin`) and not `minPoolCost`. Those are separate parameters. See the [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), [CIP-50](https://cips.cardano.org/cip/CIP-50), and ledger implementation [IntersectMBO/cardano-ledger#5943](https://github.com/IntersectMBO/cardano-ledger/pull/5943) (merged 2026-08-03; parameter name in code is `maxPledgeLeverage`, not the `maxLeverageFactor` leftover in the PR description).

---

## Core semantics changes

Implications, why it concerns you, and what needs to be updated in response.

### What the ledger actually does

The existing maximum pool reward calculation in `maxPool'` is unchanged when `maxPledgeLeverage` is unset (`SNothing` / JSON `null`):

```
σ' = min(σ, z0)
```

When it is set to a value *L*:

```
σ' = min(σ, z0, L · pR)
```

where `σ` is total pool stake (including owners' stake) divided by the ledger's circulation, `z0 = 1/k` (`k` = `stakePoolTargetNum` / `nOpt`), and `pR` is **relative pledge** (`declared pledge / circulation`). Here circulation is `maxSupply − reserves` at reward calculation, not total active stake. Eligible pledge `p'` is **not** re-capped by *L*. `a0` (`poolPledgeInfluence`) still applies on top of the capped `σ'`.

Consequences once *L* is set, and not before:

- The maximum pool reward uses effective stake capped at `min(pool_stake, k-saturation, L · pledge)`. Extra delegation above the binding cap does not increase this maximum; realised rewards still depend on apparent performance.
- A pool with **zero pledge earns a zero reward pot**. Delegators on that pool receive nothing from RSS. This is the behaviour the overview blurb warns about.
- A well-pledged pool that stays under both `k`-saturation and the leverage cap is rewarded exactly as today (modulo the usual `a0` term).
- Splitting a fixed pledge cannot increase the aggregate pledge-based ceiling `L · Σ pledge`, but can still increase effective stake and rewards when the per-pool `k` cap binds.
- Apparent performance, block production, and pool registration are untouched. Under-pledged pools still make blocks; they just stop being paid for the excess stake. The existing requirement that self-delegated owners' stake cover the declared pledge also remains.
- Reduced payouts are not immediately redistributed to other pools: the undistributed reward remainder returns to reserves.

HF-day default is `Nothing`. Tooling that always applies `min(σ, z0, L·p)` without checking for `null` will be **wrong** on Dijkstra day one.

### Why this concerns wallets, explorers, indexers, pool tools

- **Reward / APY estimators** that reimplement RSS (wallets, explorers, Koios, DBSync-derived dashboards, CNTools, pool splitters) must grow the `Nothing` vs `Just L` branch. Applying a numeric cap before activation can under-report rewards; retaining the old formula after activation can over-report rewards, including for zero-pledge pools.
- **Saturation UI**, once *L* is set, is no longer a single number `z0`. Each pool gains a second, pledge-dependent cap `L · pledge` (in ADA: `L * pledged_ada`). Display both; the binding one is `min(k-sat, leverage-sat)`.
- **Delegator UX.** After activation, extra delegation to an over-leveraged pool shares the capped reward pot and dilutes rewards per ADA; new delegators do not necessarily earn zero. Fixed costs and margin can leave nothing for delegators even when pledge is nonzero. Wallets should warn before delegation, not after the epoch snapshot. Explorers should flag “leverage saturated” the same way they flag `k`-saturated.
- **Zero-pledge pools.** They keep working through the hard fork. Once a concrete *L* applies, they earn no rewards for the affected production epochs, but previously earned rewards can still be credited later. Pool lists, “expected rewards”, and “my rewards this epoch” all have to handle a step-change that is **not** on HF day.
- **Do not wait for Peras / Phase 2.** The parameter is defined in the Dijkstra era package (Phase 1, protocol v12). Setting *L* is intra-era governance, not a new ledger era.

### What to update

1. Any local copy of `maxPool` / `maxPool'` / the Shelley RSS. Thread an optional `maxPledgeLeverage`. Pre-Dijkstra eras, and Dijkstra with `null`, must take the identity branch.
2. Pool pages: show pledge, current leverage `total_pool_stake / declared_pledge`, cap *L* (or “unset”), and which cap binds.
3. Epoch reward pipelines (DBSync, Koios, custom indexers): preserve the pairing of the **Go** snapshot, block-production epoch, and **previous epoch's PParams** used by the [reward calculation](https://github.com/IntersectMBO/cardano-ledger/blob/da825e45b9e9d5e9e54614f48723364155ced56f/eras/shelley/impl/src/Cardano/Ledger/Shelley/LedgerState/PulsingReward.hs). If *L* becomes current at the start of epoch E, rewards for production in E are calculated in E+1 and credited at the start of E+2. An enacted *L* does not rewrite already-computed pots or credited balances.
4. Governance UIs (GovTool, Parameter Committee tools, proposal builders): treat `maxPledgeLeverage` as optional. Submitting a Parameter Change that *sets* it will also need an updated constitution and guardrails script (see Breaking API / activation). Thresholds are the **technical** group (DReps + CC). An update to this parameter alone requires no SPO vote (`NoStakePoolGroup`; not classified in the security group).
5. Genesis / testnet configs: `UpgradeDijkstraPParams.maxPledgeLeverage` is optional and defaults to unset. Do not invent an HF value of *L*.

---

## Breaking API changes

Why it was unavoidable, and what needs to be updated in response.

Dijkstra is a new ledger era, so PParams CBOR/JSON **must** grow a slot for every new parameter even if the feature is dormant. There is no way to add `maxPledgeLeverage` later in an intra-era hard fork. The era therefore serialises it from day one, with `null` meaning “feature off”.

### Wire / query contract

| Channel | Shape |
| --- | --- |
| JSON PParams (`queryCurrentPParams`, `queryFuturePParams`, `govState`, `ratifyState`) | `"maxPledgeLeverage": null` or a non-negative interval (JSON number or `{numerator, denominator}`) |
| Parameter update CDDL | `protocol_param_update` index **38**: `max_pledge_leverage = nonnegative_interval / nil` |
| Haskell | `MaxPledgeLeverage (StrictMaybe NonNegativeInterval)`; getter `ppMaxPledgeLeverageG` (Conway and earlier always `SNothing`); Dijkstra lenses `ppMaxPledgeLeverageL` / `ppuMaxPledgeLeverageL` |
| Guardrails / Plutus Data | `SNothing` → `Constr 1 []`; `SJust L` → `Constr 0 [List [I num, I denom]]` |
| Dijkstra genesis | optional key `"maxPledgeLeverage"`; omitted or `null` → unset |

Parameter updates have three distinct states: omitted tag/key means **unchanged**; explicit tag 38 `nil` / JSON `null` means **unset the cap**; a numeric value means **set or change the cap**. The outer `StrictMaybe` in `ppuMaxPledgeLeverageL` records update presence, while `MaxPledgeLeverage` contains the optional value. Unsetting is a ledger capability subject to the Constitution and guardrails.

Parsers that assume a fixed Conway PParams map, or that reject unknown JSON keys, will fail on Dijkstra queries. Parsers that drop unknown keys will silently report “no L” even after governance sets one.

Index **38** is this parameter. Index **39** on current ledger `master` is CIP-23 `minPoolMargin`. Do not reuse either tag, and do not name CLI flags after the stale PR string `maxLeverageFactor`.

### Why `null` rather than a huge L

Any finite numeric sentinel (e.g. L = 10 000, CIP's weak-cap end) would zero the maximum rewards of zero-pledge pools. `Nothing` is a real semantic no-op: the [property tests](https://github.com/IntersectMBO/cardano-ledger/blob/da825e45b9e9d5e9e54614f48723364155ced56f/libs/cardano-ledger-core/test/Test/Cardano/Ledger/State/SnapShotsSpec.hs) compare the same inputs against the pre-Dijkstra formula. The [Imp test](https://github.com/IntersectMBO/cardano-ledger/blob/da825e45b9e9d5e9e54614f48723364155ced56f/eras/dijkstra/impl/testlib/Test/Cardano/Ledger/Dijkstra/Imp/PoolSpec.hs) comparing pools with different pledges explicitly sets `a0 = 0` to isolate leverage; existing pledge influence remains when `a0` is nonzero.

### Constitution and guardrails: blocking for activation, not for the HF

The ledger does **not** hard-code CIP-50's range `1 ≤ L ≤ 10 000`. `ppuWellFormed` does not mention this parameter. Activation therefore needs an appropriate permitted range in the Constitution and guardrails script. Zero is not a safe substitute for unset: with positive pledge and `a0`, the [unchanged pledge term](https://github.com/IntersectMBO/cardano-ledger/blob/da825e45b9e9d5e9e54614f48723364155ced56f/libs/cardano-ledger-core/src/Cardano/Ledger/State/SnapShots.hs#L128-L144) can make `maxPool'` negative at `L = 0`. This is a formula edge case requiring boundary testing, not a demonstrated end-to-end mainnet failure.

Under the Hard Fork Working Group's current consensus, the hard fork can proceed without a Constitution update, but newly introduced parameters cannot be changed until the Constitution and guardrails script are updated. Changing `maxPledgeLeverage` therefore requires:

1. A **New Constitution or Guardrails Script** action (DReps + CC) updates the Constitution and guardrails script to permit and constrain changes to tag 38, and
2. A **Parameter Change** (technical group: DReps + CC, no SPO vote) sets the value.

HF-day `null` preserves reward behaviour; it is not a claim that a numeric value is within an approved range.

### What to update

- cardano-cli / cardano-api / GovTool / proposal CBOR builders: encode/decode tag 38, including `nil`.
- Explorer and indexer PParams tables: new nullable column. Preserve `null` distinctly from `0` and, in update records, from an omitted field.
- Any hardcoded Conway CDDL or “list of PParams keys” allow-list.
- Guardrails-script tooling and Parameter Committee UIs: add a row for `maxPledgeLeverage` when the constitution text exists. Until then, show the parameter as **defined but not activatable**.

---

## New features

What new capabilities it unlocks that you might want to start thinking about.

Nothing new happens at the Phase 1 hard fork except that the knob exists. The capabilities below are for the day a Parameter Change enacts a concrete *L*, and for the governance process that gets there.

- **Leverage as a first-class pool metric.** `total_pool_stake / declared_pledge` (infinite for positive stake with zero pledge; undefined if both are zero) becomes as operationally important as saturation. Rank, filter, and alert on it. A pool can be far below `k`-saturation and still be leverage-saturated.
- **“Pledge required to support this stake” calculator.** For positive *L*, rearranged cap: `pledge_needed = pool_stake / L` (and `pledge_needed = z0_in_ada / L` to run a fully saturated pool). Useful for SPO onboarding, wallet “can I delegate here?”, and pool-splitter UX.
- **Zero-pledge watchlists.** Once *L* applies, those pools' delegators earn nothing for the affected production epochs; pending payouts and credited balances remain. Tools that already list zero-pledge pools (Koios, explorers, Balance Analytics-style dashboards) should add a post-activation migration warning, not a new consensus rule.
- **Governance preview.** Parameter UIs can simulate RSS under candidate *L* values (CIP-50 research looked at 10, 100, 1 000, 10 000; the ledger does not prefer one). Preview must keep `a0` and `k` as independent inputs. This parameter does not replace them.
- **MPO consolidation pressure.** The group's pledge-based ceiling is `L · Σ pledge`, not necessarily its realised effective stake or rewards. Splitting can still overcome the per-pool `k` cap. Consolidation and decentralization benefits depend on operator and delegator responses; the ledger does not enforce independent ownership.
- **Testnet rehearsal.** Preview / pre-prod can rehearse activation once upgraded to Dijkstra and their own governance and guardrails permit the change; they need not wait for mainnet constitution text. Verify enactment-to-payment timing, numeric bounds, and explicit unset updates before mainnet activation.

CIP-50's “Path to Active” still talks about agreeing *L* before the hard fork and putting it on the Hard-Fork action. That section needs reconciliation with the implementation and planned rollout: hard fork with `Nothing`, activate later with a Parameter Change once the Constitution and guardrails permit it.
