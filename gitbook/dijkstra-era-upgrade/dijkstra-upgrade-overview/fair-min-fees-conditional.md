# Fair Min Fees (CIP-23)

CIP-23 introduces a new **stake-pool** protocol parameter, `minPoolMargin`: a proportional floor on a pool's **variable fee (margin)**. It complements the fixed-fee floor `minPoolCost`. The Dijkstra implementation also moves enforcement of the fixed-cost minimum from certificate validation to reward calculation.

CIP-23 concerns staking rewards. The separate [Fee Function Update (Reference Inputs)](fee-function-update-reference-inputs.md) concerns **transaction fees**.

**CIP:** [CIP-23 Fair Min Fees](https://cips.cardano.org/cip/CIP-0023) (also [CIP-0023 on GitHub](https://github.com/cardano-foundation/CIPs/blob/master/CIP-0023/README.md))

**Overview:** [Dijkstra upgrade overview](README.md)

**Ledger implementation (merged):** [cardano-ledger#5949](https://github.com/IntersectMBO/cardano-ledger/pull/5949), parameter definition; [cardano-ledger#6197](https://github.com/IntersectMBO/cardano-ledger/pull/6197), reward logic and pool-validation changes, closing [#5954](https://github.com/IntersectMBO/cardano-ledger/issues/5954)

### Full implementation at PV12 (read this first)

**The parameter and its reward rules are included in Dijkstra Phase 1, protocol version 12. No PV13 activation is required for CIP-23.** The [20 October 2026 HFWG decision](../../general/hard-fork-working-group-meeting-minutes/20th-october-2026.md) and current [node scope #6634](https://github.com/IntersectMBO/cardano-node/issues/6634) supersede the earlier parameter-at-PV12 / logic-at-PV13 plan. Ledger PR #6197 merged on 23 October 2026. The implementation details below were checked against ledger revision [`b1e34c68`](https://github.com/IntersectMBO/cardano-ledger/tree/b1e34c68aa58ea176d3f5e8f87866dcaa3bb0627) on 11 November 2026. Network activation and downstream readiness require their own release and test evidence.

| Included at Dijkstra PV12 | Behaviour |
|---|---|
| Protocol parameter `minPoolMargin` | Dijkstra PParams, JSON field `"minPoolMargin"`, protocol-parameter update key **39**, and required Conway→Dijkstra upgrade value |
| Reward-time margin floor | `effectiveMargin = max(declared margin, minPoolMargin)` |
| Reward-time fixed-cost floor | `effectiveCost = max(declared cost, minPoolCost)` |
| Pool registration and updates | Below-floor margin and cost are accepted, subject to the other certificate rules; the floors apply during rewards |
| Initial margin floor | **0**, as recommended by the CIP and described in the current [CAP-12 draft](https://cap.intersectmbo.org/#/detail/12); a subsequent Parameter Update can set a nonzero value |

**A zero margin floor leaves declared margins unchanged; it does not defer the reward rule to PV13.** The cost clamp and removal of the certificate-time cost rejection also apply at PV12, even while `minPoolMargin` is 0. Governance permission to change either floor remains a separate requirement.

Parameter name in code: **`minPoolMargin`**. Haskell: `dppMinPoolMargin`, lenses `ppMinPoolMarginL` / `ppuMinPoolMarginL`. Pre-Dijkstra eras expose getter `ppMinPoolMarginG` defaulting to 0.

---

### Impact Analysis

## Core semantics changes

Implications, why it concerns you and what needs to be updated in response

**What the floors do.** A fixed-cost cut consumes a larger percentage of smaller reward pots when pools declare the same cost. A margin floor applies the same minimum percentage to rewards remaining **after fixed costs**. For pool reward pot R above effective cost C and effective margin m, the fee component is `C + m · (R − C)`, excluding owners' ordinary stake rewards and rounding; if R ≤ C, delegators receive zero. Raising the margin floor alone reduces payouts at affected pools for otherwise identical inputs. It does not remove the fixed-cost size bias. Moving toward predominantly proportional fees also requires separate governance decisions on `minPoolCost`; CIP-23 does not automatically reduce or remove that parameter.

**Reward logic is active from PV12.** Both operator and delegator calculations use the greater of the snapshot's declared fee and the protocol minimum. The [reward code](https://github.com/IntersectMBO/cardano-ledger/blob/b1e34c68aa58ea176d3f5e8f87866dcaa3bb0627/eras/shelley/impl/src/Cardano/Ledger/Shelley/Rewards.hs#L294-L309) explicitly gates the clamps on protocol major version **≥12**, and [operator rewards use the same gate](https://github.com/IntersectMBO/cardano-ledger/blob/b1e34c68aa58ea176d3f5e8f87866dcaa3bb0627/eras/shelley/impl/src/Cardano/Ledger/Shelley/Rewards.hs#L353-L363). Earlier protocol versions retain declared-fee reward calculations.

**Pool certificates at PV12.** Dijkstra accepts registration and re-registration with `margin < minPoolMargin` **and** with `cost < minPoolCost`; other certificate checks still apply. The [Dijkstra POOL rule](https://github.com/IntersectMBO/cardano-ledger/blob/b1e34c68aa58ea176d3f5e8f87866dcaa3bb0627/eras/dijkstra/impl/src/Cardano/Ledger/Dijkstra/Rules/Pool.hs) removes `StakePoolCostTooLowPOOL`. Existing pools need not re-register solely to satisfy either floor, and the ledger does not rewrite their declared fees. This extends the CIP's legacy-certificate clamping to new registrations and updates, differing from its certificate-time margin requirement. The cost-clamp change is additional implementation scope recorded in #5954 and delivered by #6197.

**Zero does not guarantee every payout is unchanged.** With `minPoolMargin = 0`, the margin clamp alone is a no-op. However, the cost clamp can affect an existing pool whose snapshot cost is below the applicable `minPoolCost`, for example after a previous increase to that minimum, and pools can newly register below-floor costs at PV12. A declared cost of 0 does not give delegators a zero fixed-cost cut while the protocol's minimum remains positive.

**Snapshots and payment timing.** Use the declared cost and margin in the relevant pool snapshot and the protocol parameters for the reward calculation, rather than the latest displayed values. The [reward pipeline](https://github.com/IntersectMBO/cardano-ledger/blob/b1e34c68aa58ea176d3f5e8f87866dcaa3bb0627/eras/shelley/impl/src/Cardano/Ledger/Shelley/LedgerState/PulsingReward.hs#L99-L120) takes the Go snapshot and previous epoch's PParams; it [passes that parameter set's version and both minima into the pulser](https://github.com/IntersectMBO/cardano-ledger/blob/b1e34c68aa58ea176d3f5e8f87866dcaa3bb0627/eras/shelley/impl/src/Cardano/Ledger/Shelley/LedgerState/PulsingReward.hs#L199-L206). PV12 activation does not retroactively recalculate earlier rewards. Verify the fork transition, parameter enactment and delayed payouts on testnets instead of assuming the first payment after the fork uses the new floors.

**Genesis / initial value.** The CIP recommends introduction at **0**, and the current CAP-12 draft describes this followed by a Parameter Update to choose the floor. Ledger empty PParams also default to 0. Test fixtures and testnet genesis files may use nonzero values such as `0.015` (1.5%); these are not mainnet parameter decisions. Check the final genesis for each network. Once PV12 is active, an enacted nonzero floor affects the applicable reward calculations without another hard fork.

**Constitution and guardrails.** The [enacted Constitution](https://cardano.org/constitution/) reviewed on 11 November 2026 does not yet name `minPoolMargin`. PARAM-01 restricts updates to named parameters; HARDFORK-05 and NEW-CONSTITUTION-01a require new-parameter guardrails. The current node scope plans the Constitution and guardrails-script update **ahead of the Dijkstra hard fork**, so the new parameters can be governed from the start. This replaces the old parameter-only rollout assumption.

The current **CAP-12 v5 draft**, still under consultation, proposes `minPoolMargin` guardrails and coordinating it with `minPoolCost`, including an amendment to MPC-03. Its MPM-03 upper bound is still **[PENDING]**. These proposals are not enacted guardrails or an agreed nonzero fee. Verify the final ratified text and script before offering live governance updates. The [ledger groups](https://github.com/IntersectMBO/cardano-ledger/blob/b1e34c68aa58ea176d3f5e8f87866dcaa3bb0627/eras/dijkstra/impl/src/Cardano/Ledger/Dijkstra/PParams.hs#L236-L237) are `EconomicGroup` / `NoStakePoolGroup`: a standalone update uses the economic DRep threshold and CC approval, without the additional SPO security-parameter vote. A bundled action can have additional voting requirements.

**What to update in response**

- Prepare reward calculators, pool-registration tooling and user guidance for **PV12**, together with protocol-parameter decoding.
- Keep declared and effective fees distinct. Permit below-floor pool fees in Dijkstra forms and warn which effective fees will be used; retain earlier-era validation where applicable.
- Track the Constitution/guardrails bundle and final genesis values as PV12 readiness dependencies. A zero initial margin floor is a parameter setting, not a missing implementation.
- Keep reference-input transaction-fee work separate; it has different activation rules and consumers.

## Breaking API changes

Why it was unavoidable and what needs to be updated in response

Dijkstra adds the new PParams field and the code that consumes it at PV12. Reward and submission integrations must be ready for the same fork.

**Protocol-parameter serialization**

- The [Dijkstra CDDL](https://github.com/IntersectMBO/cardano-ledger/blob/b1e34c68aa58ea176d3f5e8f87866dcaa3bb0627/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L719-L721) adds optional update key **`39 : unit_interval ; min pool margin`**. Omission means unchanged; `0` sets a zero floor; `0.015` means 1.5%; `1` means 100%. Explicit `null` / `nil` is invalid. `[0, 1]` is the ledger type bound, not an approved governance range; a 100% effective margin leaves non-owner delegators no rewards.
- Dijkstra `PParams` JSON includes `"minPoolMargin"`. JSON supports a number or numerator/denominator object; CBOR uses a tag-30 rational. Guardrails Plutus Data uses `List [I numerator, I denominator]`, without CIP-50's optional-value constructor.
- Audit fixed PParams schemas and strict decoders in current/future parameter and governance-state query consumers, DBSync, explorers and GovTool. Persist the floor for historical Dijkstra epochs. Verify JSON pass-through paths such as Koios `/cli_protocol_params` preserve it; `/tip` does not return protocol parameters.
- Conway→Dijkstra [upgrade PParams JSON requires `"minPoolMargin"`](https://github.com/IntersectMBO/cardano-ledger/blob/b1e34c68aa58ea176d3f5e8f87866dcaa3bb0627/eras/dijkstra/impl/src/Cardano/Ledger/Dijkstra/PParams.hs#L443-L450). Genesis / HF-prep tooling must supply the agreed network value.
- Strict CBOR/PParams bindings must use key **39** for `minPoolMargin`; key **38** is CIP-50 `maxPledgeLeverage`.

**Reward and submission behaviour at PV12**

- Projection and ranking APIs must use **both** effective fees. Assuming registered `margin` or `cost` is always the reward-calculation input can overstate delegator returns. The ledger's [non-myopic reward function](https://github.com/IntersectMBO/cardano-ledger/blob/b1e34c68aa58ea176d3f5e8f87866dcaa3bb0627/eras/shelley/impl/src/Cardano/Ledger/Shelley/PoolRank.hs#L437-L444) also applies PV12-gated clamps. However, at the reviewed revision, [`getTopRankedPools` still passes declared cost and margin to desirability](https://github.com/IntersectMBO/cardano-ledger/blob/b1e34c68aa58ea176d3f5e8f87866dcaa3bb0627/eras/shelley/impl/src/Cardano/Ledger/Shelley/PoolRank.hs#L325-L350). Treat ranking consistency as an outstanding readiness check, including a case where the floors reverse pool ordering.
- Submission paths must accept Dijkstra certificates with below-floor cost. Error handlers must account for removal of `StakePoolCostTooLowPOOL` in Dijkstra while preserving handling for earlier eras.
- Preserve the declared `pool.margin` **and** `pool.cost` in indexers. Derive effective values with epoch-appropriate PParams; overwriting the declarations loses information needed for history and later floor changes.

**Ledger library and persisted reward state**

PR #6197 adds minimum-cost and minimum-margin arguments to `rewardOnePoolMember`, adds `fvMinPoolCost` and `fvMinPoolMargin` to [`RewardUpdate.FreeVars` and its CBOR encoding](https://github.com/IntersectMBO/cardano-ledger/blob/b1e34c68aa58ea176d3f5e8f87866dcaa3bb0627/eras/shelley/impl/src/Cardano/Ledger/Shelley/RewardUpdate.hs#L211-L254), and removes deprecated `leaderRew`, `memberRew` and `nonMyopicMemberRew`. Update direct Haskell callers and readers of persisted reward-pulser state when upgrading these dependencies. These library/serialization changes must be distinguished from protocol-version-gated reward behaviour.

**CLI / governance builders**

- [cardano-api#1388](https://github.com/IntersectMBO/cardano-api/pull/1388) adds the parameter to `IntroducedInDijkstraPParams` and its ledger conversions. [cardano-cli#1497](https://github.com/IntersectMBO/cardano-cli/pull/1497) adds **`--min-pool-margin RATIONAL`** to Dijkstra `governance action create-protocol-parameters-update`. Both are merged; verify the dependency versions in the build being deployed.
- The existing **`--pool-margin`** and **`--pool-cost`** flags still describe an individual pool's declared fees. They do not set protocol minima. CIP-23 requires no additional pool-certificate field; separate Dijkstra changes such as the [BLS-key field](https://github.com/IntersectMBO/cardano-ledger/blob/b1e34c68aa58ea176d3f5e8f87866dcaa3bb0627/eras/dijkstra/impl/cddl/data/dijkstra.cddl#L467-L477) still require codec support.
- GovTool and other parameter-change builders must encode key 39, follow the final enacted guardrails, and distinguish a proposed value from an enacted value. Until the Constitution and script permit changes, the field's presence alone does not authorize an update.
- Transaction fee / `minFeeA` / `minFeeB` / reference-input fee calculations are untouched by CIP-23.

## New features

What new capabilities it unlocks that you might want to start thinking about

**Available from PV12:** the ledger can apply both pool-fee floors during rewards while keeping pool certificates valid below the floors. With the planned initial `minPoolMargin = 0`, no new proportional charge arises from the margin floor alone. After governance enacts a nonzero value, the same PV12 rules apply it; a PV13 cutover is unnecessary.

- **Explorers, wallets and SPO dashboards:** show declared and effective cost and margin. For example, a declared 0% margin with `minPoolMargin = 0.015` remains 0% on-chain while the effective margin is 1.5%, applied after effective fixed costs. Treat 1.5% as an illustration, not an agreed mainnet value.
- **Pool registration UIs / CNTools / guild scripts:** allow below-floor declarations in Dijkstra and explain the effective fees. A lower declaration may become effective after a later governance reduction of the floor, without requiring another pool update.
- **Delegation wallets:** use `max(pool.margin, protocol.minPoolMargin)` and `max(pool.cost, protocol.minPoolCost)` from PV12 for projections, with the appropriate snapshot and reward-epoch parameters. Verify pool ordering as well as the final APY calculation.
- **GovTool / PCP process:** once the Constitution and guardrails permit it, governance can coordinate margin-floor and fixed-cost changes through a Parameter Update. The implementation enables that choice; it does not select the economic policy or automatically eliminate fixed costs.

**Readiness checks for PV12**

The merged ledger tests cover [margin floors of 0 and 1](https://github.com/IntersectMBO/cardano-ledger/blob/b1e34c68aa58ea176d3f5e8f87866dcaa3bb0627/eras/dijkstra/impl/testlib/Test/Cardano/Ledger/Dijkstra/Imp/PoolSpec.hs#L627-L667); #6197 also adds below-cost registration/update and reward tests. Downstream integration testing should cover:

- Existing pools and new registrations/updates with each fee below, equal to and above its floor; declared values must remain intact.
- A zero floor and a permitted nonzero floor, cost-clamp effects while the margin floor is zero, rounding, and reward pots at or below effective cost. Exercise the ledger's margin endpoints separately from any narrower governance bounds.
- PV11→PV12 and parameter-enactment boundaries, snapshots and delayed payouts, including a pool already below `minPoolCost` and a later reduction of either floor.
- Agreement among operator/delegator rewards, projections, rankings and displayed effective fees, plus genesis, query decoding, governance encoding and guardrails acceptance/rejection in the actual node/API/CLI builds being deployed.
