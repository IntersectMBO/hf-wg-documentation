---
hidden: true
---

# Road to van Rossem hard fork

This page presents the readiness path toward the **van Rossem Hard Fork** through three complementary views:

* **Timeline** - delivery progress
  * It answers - **Did milestones happen?**
* **Readiness Streams (Fishbone)** - capability convergence
  * It answers - **Are required capabilities present?**
* **Control Room** - operational risk monitoring
  * It answers - **Is hard fork likely to succeed?**

These views intentionally represent different dimensions of readiness and may diverge during the hard fork lifecycle.

***

### Hard Fork Readiness Snapshot

Last updated: 2026-02-20\
Maintained by: Hard Fork Working Group

| View                  | Status | Meaning                              |
| --------------------- | ------ | ------------------------------------ |
| Timeline Progress     | 🟡     | Milestones progressing as planned    |
| Readiness Convergence | 🟡     | Streams advancing toward alignment   |
| Operational Risk      | ⚪      | Ecosystem adoption still progressing |

***

### Timeline View 🟡

Tracks execution of planned milestones.\
Status reflects **completion against plan**, not operational risk.

| Date                          | Milestone                                                  | RAG Status | Link | Short Description                                                    |
| ----------------------------- | ---------------------------------------------------------- | ---------- | ---- | -------------------------------------------------------------------- |
| 16 Feb 2026                   | Pre-release node v10.6.2 released on Sancho                | 🟢         |      | Pre-release node published for early ecosystem testing on SanchoNet. |
| 27 Feb 2026                   | Hard fork ready node v10.7.0 released for Cardano testnets | 🟡         |      | Hard fork candidate node released for broader testnet validation.    |
| 6 Mar 2026                    | Testing of pre-release node v10.6.2 completed on Sancho    | ⚪          |      | Completion of SanchoNet validation testing.                          |
| 6 Mar 2026                    | Final benchmarking completed for v10.7.0                   | ⚪          |      | Performance benchmarking finalized prior to governance submission.   |
| 6 Mar 2026                    | Hard fork governance action submitted on Cardano Preview   | ⚪          |      | Governance proposal submitted initiating Preview upgrade process.    |
| 9 Mar 2026                    | Hard fork governance action enacted on Cardano Preview     | ⚪          |      | Governance approval activates upgrade on Preview network.            |
| 9 Mar 2026                    | Hard fork ready node v10.7.0 testing on Cardano Preview    | ⚪          |      | Hard fork-ready node enters Preview validation phase.                |
| 20 Mar 2026                   | Testing of v10.7.0 completed on Cardano Preview            | ⚪          |      | Preview testing finalized confirming readiness progression.          |
| 23 Mar 2026                   | Hard fork governance action submitted on Cardano PreProd   | ⚪          |      | Governance proposal submitted to PreProd network.                    |
| 24 Mar 2026                   | Hard fork governance action enacted on Cardano PreProd     | ⚪          |      | Governance approval activates upgrade on PreProd.                    |
| 7 Apr 2026                    | Testing of v10.7.0 completed on Cardano PreProd            | ⚪          |      | Production-like validation completed.                                |
| 8 Apr 2026 (Epoch 624 begins) | Hard fork governance action submitted on Cardano Mainnet   | ⚪          |      | Mainnet governance proposal submitted initiating production upgrade. |
| 8 May 2026 (Epoch 629 ends)   | Hard fork governance action enacted on Cardano Mainnet     | ⚪          |      | Governance enactment triggers Mainnet hard fork event.               |

**Timeline Status Legend**

⚪ Planned - future milestone\
🟡 In progress / governance decision window active\
🟢 Completed\
🔴 Delayed or blocked

***

### Readiness Streams (Fishbone View) 🟡

The hard fork occurs when independent readiness streams converge.\
Each stream represents a required capability validated through evidence milestones.

**Promotion Path (Spine)**

Sancho → Preview → PreProd → Mainnet

***

#### Node Development & Release Readiness 🟡

Failure here -> No HF possible

| Evidence Milestone                    | Date   | Status |
| ------------------------------------- | ------ | ------ |
| Pre-release node v10.6.2 released     | 16 Feb | 🟢     |
| Hard fork ready node v10.7.0 released | 27 Feb | ⚪      |
| Final benchmarking completed          | 6 Mar  | ⚪      |

***

#### Technical Validation & Testing ⚪

Failure here -> Unsafe HF

| Evidence Milestone                   | Date     | Status |
| ------------------------------------ | -------- | ------ |
| Sancho testing completed             | 6 Mar    | ⚪      |
| v10.7.0 testing on Preview           | 9–20 Mar | ⚪      |
| v10.7.0 testing completed on Preview | 20 Mar   | ⚪      |
| v10.7.0 testing completed on PreProd | 7 Apr    | ⚪      |

***

#### Governance Authorization ⚪

Failure here -> HF cannot legally occur

| Evidence Milestone                     | Date   | Status |
| -------------------------------------- | ------ | ------ |
| Governance Action submitted on Preview | 6 Mar  | ⚪      |
| Governance Action enacted on Preview   | 9 Mar  | ⚪      |
| Governance Action submitted on PreProd | 23 Mar | ⚪      |
| Governance Action enacted on PreProd   | 24 Mar | ⚪      |
| Governance Action submitted on Mainnet | 8 Apr  | ⚪      |
| Governance Action enacted on Mainnet   | 8 May  | ⚪      |

***

#### Ecosystem Readiness ⚪

Failure here -> Chain split risk

| Evidence Milestone                   | Period      | Status |
| ------------------------------------ | ----------- | ------ |
| HF-ready node available to ecosystem | From 27 Feb | ⚪      |
| Preview ecosystem participation      | March       | ⚪      |
| PreProd ecosystem participation      | April       | ⚪      |
| Mainnet upgrade saturation           | Apr–May     | ⚪      |

***

#### Operational Coordination & Release Management ⚪

Failure here -> Operational instability

| Evidence Milestone               | Period  | Status |
| -------------------------------- | ------- | ------ |
| Promotion path executed          | Mar–Apr | ⚪      |
| Epoch-aligned Mainnet submission | 8 Apr   | ⚪      |
| Activation coordination          | May     | ⚪      |

* ⚪ **Not Yet Evidenced**
  * Readiness evidence is not yet available or not expected at the current phase
  * The stream has not reached evaluation stage
  * Normal during early hard fork lifecycle phases
* 🟡 **Converging**
  * Partial readiness demonstrated
  * Some evidence milestones completed
  * Additional validation or ecosystem alignment still required
  * Stream progressing toward readiness
* 🟢 **Ready**
  * Required evidence milestones completed and validated
  * Capability confirmed to support safe hard fork progression
  * No known blockers within this readiness stream
* 🔴 **At Risk**
  * Required readiness missing, blocked, or regressing
  * Evidence contradicts expected readiness
  * Stream threatens convergence toward activation

***

### Control Room View ⚪

Monitors live readiness health across streams.\
**Overall readiness equals the weakest panel.**\
Control Room status is based on observable ecosystem signals and trend assessment,\
providing forward looking operational confidence rather than historical confirmation.

| Panel        | RAG | Monitoring Focus                       |
| ------------ | --- | -------------------------------------- |
| Node Release | ⚪   | Stability and recommended node version |
| Testing      | ⚪   | Unknown risk reduction                 |
| Governance   | ⚪   | Participation and proposal clarity     |
| Ecosystem    | ⚪   | Upgrade adoption trend                 |
| Operations   | ⚪   | Coordination readiness                 |

* ⚪ **Not Yet Assessed**
  * Operational health not yet evaluated or too early in lifecycle
  * Insufficient live signals available
  * Normal during early preparation phases
* 🟡 **Watch / Emerging Risk**
  * Readiness progressing but uncertainty remains
  * Signals require monitoring
  * Convergence depends on continued ecosystem alignment
  * No immediate blocker, but attention required
* 🟢 **Stable**
  * Stream operating as expected
  * No significant operational concerns observed
  * Current signals support safe progression toward activation
* 🔴 **Intervention Required**
  * Active risk or instability detected
  * Convergence toward hard fork may be threatened
  * Coordination, communication, or mitigation action needed
