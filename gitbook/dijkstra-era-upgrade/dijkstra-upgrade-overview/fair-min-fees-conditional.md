# Fair Min Fees (conditional)

CIP-23 introduces a new **stake-pool** protocol parameter, `minPoolMargin`: a size-neutral proportional floor on a pool's **variable fee (margin)**. It complements, and does not replace, the existing fixed-fee floor `minPoolCost`.

This is **not** the Dijkstra item [Fee Function Update (Reference Inputs)](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/fee-function-update-reference-inputs). That item has no CIP and changes **transaction fees** for reference inputs. CIP-23 does not touch transaction fees.

**CIP:** [CIP-23 Fair Min Fees](https://cips.cardano.org/cip/CIP-23) (also [CIP-0023 on GitHub](https://github.com/cardano-foundation/CIPs/blob/master/CIP-0023/README.md))  
**Overview:** [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), Conditional: Fair Min Fees (CIP-23)  
**Ledger PR (merged):** [cardano-ledger#5949](https://github.com/IntersectMBO/cardano-ledger/pull/5949), parameter definition only  
**Remaining logic (open, no PR):** [cardano-ledger#5954](https://github.com/IntersectMBO/cardano-ledger/issues/5954), intra-era hard fork

### Phase 1 vs dormant (read this first)

The [Dijkstra overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) frames CIP-23 as **conditional**: the parameter is defined at Phase 1; the fee rule may activate at Phase 1 or, if implementation and governance are not ready, ship dormant and activate in a later intra-era hard fork. Phase 2's activate list includes CIP-23 if it did not activate in Phase 1.

**As implemented today (September 2026), Phase 1 takes the dormant path.**

| Ships at Phase 1 (Dijkstra PV12) | Stays dormant until a later intra-era HF (planned PV13 / #5954) |
|---|---|
| Protocol parameter `minPoolMargin` on Dijkstra `PParams` | Reward-time floor: `effectiveMargin = max(declared margin, minPoolMargin)` |
| CDDL `protocol_param_update` key **39**, type `unit_interval` | Any change to pool **registration / re-registration** validation for margin |
| JSON field `"minPoolMargin"` on current/future PParams and gov-state queries | Raising the parameter above 0 in a way that actually changes SPO payouts |
| Conway→Dijkstra upgrade genesis field `minPoolMargin` (required) | The related plan to clamp `cost` against `minPoolCost` instead of rejecting certs |
| Empty/default value **0** (`UnitInterval` minBound) | Constitution / guardrails script listing (still pending; see below) |

Phase 1 does **not** start charging a protocol minimum margin, and it does **not** reject 0% margin pool certificates. A `minPoolMargin` of 0 is a no-op even after the fee rule exists.

Parameter name in code (not a CIP-only alias): **`minPoolMargin`**. Haskell: `dppMinPoolMargin`, lenses `ppMinPoolMarginL` / `ppuMinPoolMarginL`. Pre-Dijkstra eras expose getter `ppMinPoolMarginG` defaulting to 0.

---

### Impact Analysis

## Core semantics changes

Implications, why it concerns you and what needs to be updated in response

**What CIP-23 is for.** `minPoolCost` is a fixed ada cut taken before delegator rewards. It is the same number for a 2M-ada pool and a saturated pool, so it is a much larger *percentage* tax on small pools and pushes stake toward large ones. `minPoolMargin` is a **percentage floor** on the pool's variable fee. Once the fee rule is on and governance sets the parameter above 0, every pool's *effective* margin used in the reward formula is at least that floor, independent of pool size. `minPoolCost` is unchanged by this CIP; both floors are independent.

**Phase 1 hard-fork day: no reward-formula change.** Merged PR [#5949](https://github.com/IntersectMBO/cardano-ledger/pull/5949) (koslambrou, 2026-08-04) added the parameter and stated explicitly there is **no change to the logic**. Open issue [#5954](https://github.com/IntersectMBO/cardano-ledger/issues/5954) (lehins; labels `DijkstraEra`, `intra-era-hardfork`) is the fee rule. There is **no implementing PR** for #5954. Node scope [#6634](https://github.com/IntersectMBO/cardano-node/issues/6634) records the same split: serialization at v12, activation at intra-era v13.

**Pool certificates at Phase 1.** The Dijkstra `pool_params` CDDL is still `cost : coin` and `margin : unit_interval`. The POOL rule still rejects `cost < minPoolCost` (`StakePoolCostTooLowPOOL`) and still accepts any margin in `[0, 1]`. **Dijkstra Phase 1 will not fail a pool registration or re-registration because margin is below `minPoolMargin`.** Do not add a hard submit-time block in CNTools, guild scripts, or pool-registration UIs on HF day.

**When the fee rule later activates (planned, not Phase 1).** #5954 documents a deliberate deviation from the CIP's "certificates MUST have `margin >= minPoolMargin`":

- Registration / update with `margin < minPoolMargin` will still succeed.
- At **reward calculation**, the ledger will use `max(declared margin, minPoolMargin)`.
- The same clamp is planned for `cost` vs `minPoolCost` (that *would* retire today's cert-time `StakePoolCostTooLowPOOL` rejection). That cost change is **not** in CIP-23; it is extra ledger intent on the same ticket.

Until that intra-era fork, advertised margin, on-chain margin, and the margin used in rewards remain the same number.

**Genesis / initial value.** CIP-23 recommends introducing the parameter at **0**. Ledger empty PParams and Conway-like golden files use 0. Test `exampleDijkstraGenesis` uses `0.015` (1.5%) as fixture data. That is **not** a mainnet decision. A non-zero mainnet value would still do nothing until the fee rule is on.

**Constitution.** `minPoolMargin` is **not** in the enacted Constitution. PARAM-01 / HARDFORK-05 / NEW-CONSTITUTION-01a: a Parameter Update cannot change an unnamed parameter, and new HF parameters need Appendix guardrails plus a guardrails-script update. Node #6634 says CIP-23 guardrail-script impact is "likely not at PV12; pending decisions." Assume Phase 1 may define the field on-chain while **governance still cannot raise it** until a New Constitution action names it. Analog: today's `minPoolCost` is Economic-group, listed as governance-critical, with MPC-01/02/03 bounds. Code places `minPoolMargin` in `EconomicGroup` / `NoStakePoolGroup` (DRep+CC, not SPO security vote, unless bundled). That grouping is **not yet constitutional text**.

**What to update in response**

- Treat Phase 1 as "new pparam appears, behaviour of staking rewards and pool certs is unchanged."
- Plan a second, intra-era cutover for effective-vs-declared margin (and possibly effective-vs-declared cost).
- Do not fold this into reference-input / min-fee work. Different page, different code path, different consumers.
- Track the Constitution/guardrails bundle separately from the ledger PR. Without it, GovTool cannot legally change the value.

## Breaking API changes

Why it was unavoidable and what needs to be updated in response

New updatable protocol parameters can only be introduced in a **new era**, which is why the field ships at Phase 1 even though the rule is dormant. Intra-era hard forks cannot add PParams.

**Serialization (unavoidable at PV12)**

- `protocol_param_update` CDDL adds optional key **`39 : unit_interval ; min pool margin`**.
- Dijkstra `PParams` JSON includes `"minPoolMargin"` (golden files show `0` next to `"minPoolCost"`).
- `queryCurrentPParams` / `queryFuturePParams` / `queryGovState` / `queryRatifyState` golden CBOR **and** JSON changed. Any node-query decoder, DBSync epoch-param table, Koios `/tip`/`/cli_protocol_params`, explorer "current parameters" page, or GovTool parameter form that assumes a closed Conway key set will mis-parse or drop the field.
- Conway→Dijkstra **upgrade PParams** JSON requires `"minPoolMargin"` (`o .: "minPoolMargin"`, not optional). Genesis / HF-prep tooling that builds `UpgradeDijkstraPParams` must supply it.

**Not breaking at PV12**

- Pool registration certificate format: unchanged.
- Pool-cert CLI flags (`--pool-margin`, `--pool-cost`): no cardano-cli/node PR found; no new flag.
- Reward REST/SQL schemas that store *paid* rewards: numbers do not change at PV12.
- Transaction fee / `minFeeA`/`minFeeB` / reference-input fee function: untouched by CIP-23.

**Breaking later, when #5954 activates (flag as a second wave)**

- Reward projection APIs that take registered `margin` as the rate used by the ledger become wrong for any pool below the floor.
- If the bundled `minPoolCost` clamp lands, submit paths that rely on `StakePoolCostTooLowPOOL` as a mempool error will see those transactions **accepted**, with the floor applied only at rewards. Pool UIs that "helpfully" refuse `cost < minPoolCost` would then be stricter than the ledger.

**What to update in response**

- DBSync / Koios / explorers: add `min_pool_margin` (or equivalent) on protocol-parameter tables for Dijkstra epochs. Keep pool.margin as declared.
- GovTool and other param-change builders: know tag 39 and the JSON name `minPoolMargin`. Until the Constitution lists it, the guardrails script must reject updates. Surface that, don't offer a live slider that cannot submit.
- cardano-cli / API consumers: accept the new field on `query protocol-parameters`. Do not require a new pool-cert field.
- Strict CBOR/`PParams` struct bindings (Rust/Go/TS era codecs, Scalus, Lucid-class libs): extend the Dijkstra PParams type. Tag 38 is `maxPledgeLeverage` (CIP-50); tag 39 is `minPoolMargin` (CIP-23). Do not swap them.

## New features

What new capabilities it unlocks that you might want to start thinking about

**Phase 1 capability:** the ledger can *carry* a governable proportional fee floor. Tooling can display it, persist it, and test Parameter Update encoding against Preview/Preprod once constitution+script allow it. Nothing in the staking product changes for users on HF day.

**After intra-era activation + a non-zero parameter:**

- **Declared vs effective margin.** Explorers, wallets, and SPO dashboards should show both. A pool registered at 0% with `minPoolMargin = 0.015` still has on-chain margin 0%; delegators pay 1.5%. Ranking by "lowest margin" without the clamp will be wrong.
- **Pool registration UIs / CNTools / guild scripts.** Keep allowing 0% (ledger will). Add a warning when `margin < minPoolMargin`: "the protocol will charge `minPoolMargin` anyway." Same pattern later for `cost` if #5954's cost clamp lands.
- **Delegation wallets.** Projected APY must use `max(pool.margin, protocol.minPoolMargin)` (and `max(pool.cost, protocol.minPoolCost)` if that clamp ships). Otherwise small 0% pools will look better than they pay.
- **GovTool / PCP process.** Once named in the Constitution, `minPoolMargin` is the knob CIP-23 always intended: raise the proportional floor through a Parameter Update rather than another hard fork. CIP-23 does not prescribe the target; the CIP rationale table uses 1.5% only as an example. Initial HF value is expected to be 0 so the raise is a later governance action.
- **Stopgap vs structural.** Near-term `minPoolCost` cuts (e.g. PCP-006) are a different lever. CIP-23 is the proportional replacement path; do not document a `minPoolCost` change as "Fair Min Fees."

No new wallet feature, NFT, or Plutus primitive is involved. The only new user-visible capability after activation is **honest, size-neutral minimum pool take-rate**, plus the ability for governance to set that take-rate without another era.
