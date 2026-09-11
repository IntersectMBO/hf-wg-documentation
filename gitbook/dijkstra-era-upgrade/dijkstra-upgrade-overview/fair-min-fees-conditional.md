# Fair Min Fees (conditional)

CIP-23 introduces a new **stake-pool** protocol parameter, `minPoolMargin`: a size-neutral proportional floor on a pool's **variable fee (margin)**. It complements, and does not replace, the existing fixed-fee floor `minPoolCost`.

This is **not** the Dijkstra item [Fee Function Update (Reference Inputs)](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview/fee-function-update-reference-inputs). That item has no CIP and changes **transaction fees** for reference inputs. CIP-23 does not touch transaction fees.

**CIP:** [CIP-23 Fair Min Fees](https://cips.cardano.org/cip/CIP-23) (also [CIP-0023 on GitHub](https://github.com/cardano-foundation/CIPs/blob/master/CIP-0023/README.md))  
**Overview:** [Dijkstra upgrade overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview), Conditional: Fair Min Fees (CIP-23)  
**Ledger PR (merged):** [cardano-ledger#5949](https://github.com/IntersectMBO/cardano-ledger/pull/5949), parameter definition only  
**PV13 logic (tracked separately):** [cardano-ledger#5954](https://github.com/IntersectMBO/cardano-ledger/issues/5954), intra-era hard fork

### PV12 parameter vs PV13 activation (read this first)

**The current rollout plan (September 2026) introduces the parameter at PV12, with the logic and activation at the PV13 intra-era hard fork.** The earlier conditional Phase 1 wording in the [Dijkstra overview](https://cardanoupgrades.docs.intersectmbo.org/dijkstra-era-upgrade/dijkstra-upgrade-overview) needs reconciliation with this split. PV12 guardrail rationale should describe a parameter introduced at 0 that preserves existing reward behaviour, without implying the PV13 clamp is already enforced.

| Ships at Phase 1 (Dijkstra PV12) | Logic and activation at PV13 (#5954) |
|---|---|
| Protocol parameter `minPoolMargin` on Dijkstra `PParams` | Reward-time floor: `effectiveMargin = max(declared margin, minPoolMargin)` |
| CDDL `protocol_param_update` key **39**, type `unit_interval` | Below-floor margin certificates remain accepted; the floor applies during rewards |
| JSON field `"minPoolMargin"` on current/future PParams and gov-state queries | A nonzero floor can affect rewards once the rule is active |
| Conway→Dijkstra upgrade genesis field `minPoolMargin` (required) | The related plan to clamp `cost` against `minPoolCost` instead of rejecting certs |
| Initial value **0** (also `UnitInterval` minBound) | A zero margin floor leaves declared margins unchanged |

Phase 1 does **not** start charging a protocol minimum margin, and it does **not** reject 0% margin pool certificates. A `minPoolMargin` of 0 is a no-op for the margin clamp even at PV13; any accompanying cost-rule changes must be assessed separately. Constitution and guardrails updates govern whether the parameter can be changed, independently of the PV13 rule activation.

Parameter name in code (not a CIP-only alias): **`minPoolMargin`**. Haskell: `dppMinPoolMargin`, lenses `ppMinPoolMarginL` / `ppuMinPoolMarginL`. Pre-Dijkstra eras expose getter `ppMinPoolMarginG` defaulting to 0.

---

### Impact Analysis

## Core semantics changes

Implications, why it concerns you and what needs to be updated in response

**What CIP-23 is for.** `minPoolCost` is the minimum permitted fixed pool cost. For pools declaring the same cost, that cut consumes a larger percentage of smaller reward pots and can push stake toward larger pools. `minPoolMargin` is a **percentage floor** on the pool's variable fee. Once the PV13 fee rule is on and the applicable parameter is above 0, every pool's *effective* margin used in the reward formula is at least that floor, independent of pool size. `minPoolCost` is unchanged by this CIP; both floors are independent. Margin applies **after fixed costs**: for reward pot R above cost C and effective margin m, the fee component is `C + m · (R − C)`, excluding owners' ordinary stake rewards and rounding; if R ≤ C, delegators receive zero. A uniform margin floor does not remove the fixed-cost size bias. Raising the floor alone reduces payouts at affected pools for otherwise identical inputs; the CIP's fairness example changes both fixed costs and margin.

**Phase 1 hard-fork day: no reward-formula change from CIP-23.** Merged PR [#5949](https://github.com/IntersectMBO/cardano-ledger/pull/5949) (koslambrou, 2026-08-04) added the parameter and stated explicitly there is **no change to the logic**. Open issue [#5954](https://github.com/IntersectMBO/cardano-ledger/issues/5954) (lehins; labels `DijkstraEra`, `intra-era-hardfork`) is the fee rule. The reviewed ledger revision (`ae2c8912`, 9 September 2026) does not yet implement that rule. Node scope [#6634](https://github.com/IntersectMBO/cardano-node/issues/6634) records the same split: serialization at v12, activation at intra-era v13.

**Pool certificates at Phase 1.** The Dijkstra `pool_params` CDDL is still `cost : coin` and `margin : unit_interval`. The POOL rule still rejects `cost < minPoolCost` (`StakePoolCostTooLowPOOL`) and still accepts any margin in `[0, 1]`. **Dijkstra Phase 1 will not fail a pool registration or re-registration because margin is below `minPoolMargin`.** Do not add a hard submit-time block in CNTools, guild scripts, or pool-registration UIs on HF day.

**When the fee rule activates at PV13.** CIP-23 already proposes reward-time clamping for legacy certificates. #5954 extends this approach to new registrations and updates, deviating from the CIP's "certificates MUST have `margin >= minPoolMargin`":

- Registration / update with `margin < minPoolMargin` will still succeed.
- At **reward calculation**, the ledger will use `max(declared margin, minPoolMargin)`.
- The same clamp is planned for `cost` vs `minPoolCost` (that *would* retire today's cert-time `StakePoolCostTooLowPOOL` rejection). That cost change is **not** in CIP-23; it is extra ledger intent on the same ticket.

Until PV13, rewards use the declared margin from the applicable pool snapshot, which may differ from the latest displayed value. After activation, calculations must pair that snapshot margin with the protocol floor applicable to the reward epoch. The existing [reward pipeline](https://github.com/IntersectMBO/cardano-ledger/blob/ae2c8912b204d11e102faeb617b6faa6a8c9f934/eras/shelley/impl/src/Cardano/Ledger/Shelley/LedgerState/PulsingReward.hs#L99-L120) uses the Go snapshot and previous epoch's PParams; verify the PV13 transition and delayed payouts when #5954 is implemented.

**Genesis / initial value.** CIP-23 recommends introducing the parameter at **0**. Ledger empty PParams and Conway-like golden files use 0. Test `exampleDijkstraGenesis` uses `0.015` (1.5%) as fixture data. That is **not** a mainnet decision. A nonzero value, if permitted and set before PV13, would not affect margins until rule activation; no second parameter update would then be needed for that value to take effect.

**Constitution.** Under the HFWG's current consensus, PV12 can introduce `minPoolMargin` without a Constitution update, but **governance cannot change it until the Constitution and guardrails script are updated**. This dependency is separate from PV13 activation. Guardrail rationale drafted for PV12 must describe the parameter-only state and distinguish it from the planned PV13 reward rule. Analog: today's `minPoolCost` is Economic-group, listed as governance-critical, with MPC-01/02/03 bounds. Code places `minPoolMargin` in `EconomicGroup` / `NoStakePoolGroup` (DRep+CC, not SPO security vote, unless bundled). That grouping is **not yet constitutional text**.

**What to update in response**

- Treat Phase 1 as "new pparam appears; CIP-23 itself does not change staking rewards or pool-certificate validation."
- Plan the PV13 intra-era cutover for effective-vs-declared margin (and possibly effective-vs-declared cost).
- Do not fold this into reference-input / min-fee work. Different page, different code path, different consumers.
- Track the Constitution/guardrails bundle separately from the ledger PR. Without it, GovTool cannot legally change the value.

## Breaking API changes

Why it was unavoidable and what needs to be updated in response

New updatable protocol parameters can only be introduced in a **new era**, which is why the field ships at Phase 1 even though the rule is dormant. Intra-era hard forks cannot add PParams.

**Serialization (unavoidable at PV12)**

- `protocol_param_update` CDDL adds optional key **`39 : unit_interval ; min pool margin`**. Omission means unchanged; `0` sets a zero floor; `0.015` means 1.5%; `1` means 100%. Explicit `null` / `nil` is invalid. `[0, 1]` is the ledger type bound, not an approved governance range; a 100% effective margin leaves non-owner delegators no rewards.
- Dijkstra `PParams` JSON includes `"minPoolMargin"` (golden files show `0` next to `"minPoolCost"`). JSON supports a number or numerator/denominator object; CBOR uses a tag-30 rational. Guardrails Plutus Data uses `List [I numerator, I denominator]`, without CIP-50's optional-value constructor.
- `queryCurrentPParams` / `queryFuturePParams` / `queryGovState` / `queryRatifyState` golden CBOR **and** JSON changed. Audit fixed protocol-parameter schemas and strict decoders in node-query consumers, DBSync, explorers, and GovTool. Verify JSON pass-through paths such as Koios `/cli_protocol_params` preserve the field; `/tip` does not return protocol parameters.
- Conway→Dijkstra **upgrade PParams** JSON requires `"minPoolMargin"` (`o .: "minPoolMargin"`, not optional). Genesis / HF-prep tooling that builds `UpgradeDijkstraPParams` must supply it.

**Unchanged by CIP-23 itself at PV12**

- CIP-23 adds no field to individual pool registration certificates. Other Dijkstra changes still require codec updates: the [Dijkstra CDDL](https://github.com/IntersectMBO/cardano-ledger/blob/ae2c8912b204d11e102faeb617b6faa6a8c9f934/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L463-L477) includes an optional BLS-key field.
- Pool-cert CLI flags (`--pool-margin`, `--pool-cost`): CIP-23 requires no additional pool-margin field or flag.
- Paid rewards: dormant CIP-23 introduces no change to their calculation; assess other PV12 changes separately.
- Transaction fee / `minFeeA`/`minFeeB` / reference-input fee function: untouched by CIP-23.

**Behaviour changes at PV13, when #5954 activates**

- Reward projection APIs that take registered `margin` as the rate used by the ledger become wrong for any pool below the floor.
- If the bundled `minPoolCost` clamp lands, submit paths that rely on `StakePoolCostTooLowPOOL` as a mempool error will see those transactions **accepted**, with the floor applied only at rewards. Pool UIs that "helpfully" refuse `cost < minPoolCost` would then be stricter than the ledger.

**What to update in response**

- DBSync / Koios / explorers: persist `minPoolMargin` for Dijkstra epochs, extending fixed schemas where necessary and preserving it in JSON storage. Keep pool.margin as declared.
- GovTool and other param-change builders: know tag 39 and the JSON name `minPoolMargin`. Until the Constitution and guardrails permit it, parameter updates cannot proceed. Surface that, don't offer a live slider that cannot submit.
- cardano-cli / API consumers: accept the new field on `query protocol-parameters`. Do not require a new pool-cert field for CIP-23.
- Strict CBOR/`PParams` struct bindings (Rust/Go/TS era codecs, Scalus, Lucid-class libs): extend the Dijkstra PParams type. Tag 38 is `maxPledgeLeverage` (CIP-50); tag 39 is `minPoolMargin` (CIP-23). Do not swap them.

## New features

What new capabilities it unlocks that you might want to start thinking about

**Phase 1 capability:** the ledger can *carry* a governable proportional fee floor. Tooling can display it, persist it, and test Parameter Update encoding against Preview/Preprod once constitution+script allow it. CIP-23 itself leaves staking rewards unchanged at PV12.

**After PV13 activation, with a nonzero parameter:**

- **Declared vs effective margin.** Explorers, wallets, and SPO dashboards should show both. A pool registered at 0% with `minPoolMargin = 0.015` still has on-chain margin 0%; the effective margin is 1.5%, applied after fixed costs. Ranking by "lowest margin" without the clamp will be wrong.
- **Pool registration UIs / CNTools / guild scripts.** Keep allowing 0% (ledger will). Add a warning when `margin < minPoolMargin`: "the effective margin will be at least `minPoolMargin`, applied after fixed costs." Same pattern later for `cost` if #5954's cost clamp lands.
- **Delegation wallets.** Projected APY must use `max(pool.margin, protocol.minPoolMargin)` (and `max(pool.cost, protocol.minPoolCost)` if that clamp ships). Use snapshot and protocol parameters for the relevant reward epoch, not simply the latest displayed values. Otherwise affected pools will look better than they pay.
- **GovTool / PCP process.** Once the Constitution and guardrails permit changes, `minPoolMargin` is the knob CIP-23 always intended: raise the proportional floor through a Parameter Update rather than another hard fork. CIP-23 does not prescribe the target; the CIP rationale table uses 1.5% only as an example. Initial HF value is expected to be 0 so the raise is a later governance action.
- **Stopgap vs structural.** Near-term `minPoolCost` cuts (e.g. PCP-006) are a different lever. CIP-23 enables a proportional floor, but moving toward predominantly proportional fees also requires separate decisions on fixed costs; do not document a `minPoolCost` change as "Fair Min Fees."

After PV13 activation, tooling can show the **declared and effective proportional margins**, and governance can adjust the floor once the Constitution and guardrails permit it. Total fee burdens still depend on fixed costs. Test below-floor registrations and updates, existing pools, snapshot/payment boundaries, margin values of 0 and 1, and any bundled cost clamp before activation readiness is declared.
