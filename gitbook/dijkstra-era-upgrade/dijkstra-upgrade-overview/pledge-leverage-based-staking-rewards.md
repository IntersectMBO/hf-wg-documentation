# Pledge Leverage-Based Staking Rewards

At the Dijkstra Phase 1 hard fork the ledger grows a new protocol parameter, `maxPledgeLeverage` (CIP-50's *L*). It ships as `Nothing` in Dijkstra genesis, so pool rewards on HF day are bit-for-bit the current Shelley formula. No redelegation event, no zero-pledge penalty, no change to APY calculators' outputs. A later Parameter Change governance action can set *L* to a concrete non-negative interval; only then does the cap bind, and only then do pools with zero pledge earn zero rewards.

This is not CIP-23 (`minPoolMargin`) and not `minPoolCost`. Those are separate parameters. See the [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), [CIP-50](https://cips.cardano.org/cip/CIP-50), and ledger implementation [IntersectMBO/cardano-ledger#5943](https://github.com/IntersectMBO/cardano-ledger/pull/5943) (merged 2026-08-03; parameter name in code is `maxPledgeLeverage`, not the `maxLeverageFactor` leftover in the PR description).

---

## Core semantics changes

Implications, why it concerns you, and what needs to be updated in response.

### What the ledger actually does

The existing reward-pot function `maxPool'` is unchanged when `maxPledgeLeverage` is unset (`SNothing` / JSON `null`):

```
σ' = min(σ, z0)
```

When it is set to a value *L*:

```
σ' = min(σ, z0, L · pR)
```

where `σ` is the pool's relative stake, `z0 = 1/k` (`k` = `stakePoolTargetNum` / `nOpt`), and `pR` is **relative pledge** (`declared pledge / total circulating stake used in the snapshot`). Eligible pledge `p'` is **not** re-capped by *L*. `a0` (`poolPledgeInfluence`) still applies on top of the capped `σ'`.

Consequences once *L* is set, and not before:

- A pool whose stake exceeds *L* times its pledge is treated as if it only had `L · pledge` of stake for rewards. Extra delegation does not increase the pot.
- A pool with **zero pledge earns a zero reward pot**. Delegators on that pool receive nothing from RSS. This is the behaviour the overview blurb warns about.
- A well-pledged pool that stays under both `k`-saturation and the leverage cap is rewarded exactly as today (modulo the usual `a0` term).
- Splitting a fixed pledge across more pools does not increase total effective stake: each pool's cap is `L · (its pledge)`.
- Apparent performance, block production, and pool registration are untouched. Under-pledged pools still make blocks; they just stop being paid for the excess stake.

HF-day default is `Nothing`. Tooling that always applies `min(σ, z0, L·p)` without checking for `null` will be **wrong** on Dijkstra day one.

### Why this concerns wallets, explorers, indexers, pool tools

- **Reward / APY estimators** that reimplement RSS (wallets, explorers, Koios, DBSync-derived dashboards, CNTools, pool splitters) must grow the `Nothing` vs `Just L` branch. Shipping the capped formula unconditionally will under-report rewards until governance sets *L*, and will be wrong for zero-pledge pools after it does.
- **Saturation UI** is no longer a single number `z0`. Each pool gains a second, pledge-dependent cap `L · pledge` (in ADA: `L * pledged_ada`). Display both; the binding one is `min(k-sat, leverage-sat)`.
- **Delegator UX.** After activation, sending more stake to an over-leveraged pool is wasted. Wallets should warn before delegation, not after the epoch snapshot. Explorers should flag “leverage saturated” the same way they flag `k`-saturated.
- **Zero-pledge pools.** There are hundreds of them on mainnet today. They keep working through the hard fork. They become economically dead the epoch the Parameter Change enacts a concrete *L*. Pool lists, “expected rewards”, and “my rewards this epoch” all have to handle a step-change that is **not** on HF day.
- **Do not wait for Peras / Phase 2.** The parameter is defined in the Dijkstra era package (Phase 1, protocol v12). Setting *L* is intra-era governance, not a new ledger era.

### What to update

1. Any local copy of `maxPool` / `maxPool'` / the Shelley RSS. Thread an optional `maxPledgeLeverage`. Pre-Dijkstra eras, and Dijkstra with `null`, must take the identity branch.
2. Pool pages: show pledge, current leverage `σ / p`, cap *L* (or “unset”), and which cap binds.
3. Epoch reward pipelines (DBSync, Koios, custom indexers): keep computing today’s formula until the enacted PParams say otherwise; then switch. Rewards are paid from the **Go** snapshot with a two-epoch lag, same as now. An enacted *L* does not rewrite already-computed pots.
4. Governance UIs (GovTool, Parameter Committee tools, proposal builders): treat `maxPledgeLeverage` as optional. Submitting a Parameter Change that *sets* it will also need an updated constitution and guardrails script (see Breaking API / activation). Thresholds are the **technical** group (DReps + CC). SPOs do **not** vote on this parameter (`NoStakePoolGroup`; not security-relevant).
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

Parsers that assume a fixed Conway PParams map, or that reject unknown JSON keys, will fail on Dijkstra queries. Parsers that drop unknown keys will silently report “no L” even after governance sets one.

Index **38** is this parameter. Index **39** on current ledger `master` is CIP-23 `minPoolMargin`. Do not reuse either tag, and do not name CLI flags after the stale PR string `maxLeverageFactor`.

### Why `null` rather than a huge L

A numeric sentinel (e.g. L = 10 000, CIP's weak-cap end) would have changed rewards on HF day, even if only in the noise. `Nothing` is a real semantic no-op and is what the Imp tests assert: two pools that differ only in pledge earn **identical** rewards while the parameter is unset.

### Constitution and guardrails: blocking for activation, not for the HF

The ledger does **not** hard-code CIP-50's range `1 ≤ L ≤ 10 000`. `ppuWellFormed` does not mention this parameter. Bounds live in the constitution and the on-chain guardrails script, same pattern as `poolPledgeInfluence` / `stakePoolTargetNum`, and the same requirement GitBook already records for Dijkstra's new reference-script parameters.

As of this draft, neither the constitution nor the guardrails script lists `maxPledgeLeverage`. A Parameter Change that sets *L* is therefore not actionable until:

1. A **New Constitution or Guardrails Script** action (DReps + CC) adds bounds for tag 38, and
2. A **Parameter Change** (technical group: DReps + CC, no SPO vote) sets the value.

The hard fork itself does not need those updates. HF-day `null` is in-range because nothing is being changed.

### What to update

- cardano-cli / cardano-api / GovTool / proposal CBOR builders: encode/decode tag 38, including `nil`.
- Explorer and indexer PParams tables: new nullable column. Do not coerce `null` to `0` (that would zero every pool's rewards).
- Any hardcoded Conway CDDL or “list of PParams keys” allow-list.
- Guardrails-script tooling and Parameter Committee UIs: add a row for `maxPledgeLeverage` when the constitution text exists. Until then, show the parameter as **defined but not activatable**.

---

## New features

What new capabilities it unlocks that you might want to start thinking about.

Nothing new happens at the Phase 1 hard fork except that the knob exists. The capabilities below are for the day a Parameter Change enacts a concrete *L*, and for the governance process that gets there.

- **Leverage as a first-class pool metric.** `delegated_stake / pledge` (infinite if pledge is 0) becomes as operationally important as saturation. Rank, filter, and alert on it. A pool can be far below `k`-saturation and still be leverage-saturated.
- **“Pledge required to support this stake” calculator.** Rearranged cap: `pledge_needed = pool_stake / L` (and `pledge_needed = z0_in_ada / L` to run a fully saturated pool). Useful for SPO onboarding, wallet “can I delegate here?”, and pool-splitter UX.
- **Zero-pledge watchlists.** Once *L* is set, those pools' delegators earn nothing. Tools that already list zero-pledge pools (Koios, explorers, Balance Analytics-style dashboards) should add a post-activation migration warning, not a new consensus rule.
- **Governance preview.** Parameter UIs can simulate RSS under candidate *L* values (CIP-50 research looked at 10, 100, 1 000, 10 000; the ledger does not prefer one). Preview must keep `a0` and `k` as independent inputs. This parameter does not replace them.
- **MPO consolidation pressure.** After activation, extra pools with the same pledge budget do not earn extra pot. Pool-group views can show “effective cap across the group's pledge” as a single number `L · Σ pledge`.
- **Testnet rehearsal.** Preview / pre-prod can set *L* via Parameter Change without waiting for mainnet constitution text. That is the right place to verify reward pipelines, not mainnet HF day.

CIP-50's “Path to Active” still talks about agreeing *L* before the hard fork and putting it on the Hard-Fork action. **Do not follow that.** The implementation, the GitBook overview, and the genesis default all say: hard fork with `Nothing`, activate later with a Parameter Change.
