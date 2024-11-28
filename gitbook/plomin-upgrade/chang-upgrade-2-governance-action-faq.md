# Plomin upgrade governance action FAQ

### Oops ! What's up with governance action [51f4…74#0](https://gov.tools/governance_actions/51f495aa23f4b3b3aa90afde4a0e67823bb7ac4ac65f5ffbb138373b863f2f74#0)?

This action was intended to update the Plutus V3 Cost Model by adding new costing variables for the upcoming Plutus Primitives enabled by the Plomin hard fork. However, upon review, we found that the action did not produce the intended on-chain effect because the new costing variables were unintentionally omitted. This was an error but an expected one at this stage. Once this was spotted, the decision was made to invalidate the action’s metadata to discourage voting (error message seen via [GovTool](https://gov.tools/governance_actions/51f495aa23f4b3b3aa90afde4a0e67823bb7ac4ac65f5ffbb138373b863f2f74#0)).

As the first mainnet action submitted by Intersect on behalf of a committee/working group, this experience highlights the natural growing pains of navigating a new governance landscape. These early mistakes are essential to learning, providing valuable insights that help us quickly refine and improve our approach.

Errors like this, while unexpected, are encouraging—they show us precisely where adjustments are needed and guide us in developing more robust, more effective processes. Intersect is already proactively evolving its internal procedures to address such issues. A corrected action will be submitted soon, marking another step forward as we refine and strengthen our governance processes in real-time.

### Governance Action FAQ

This FAQ goes through some common questions relating to governance actions.

The Chang upgrade #2 requires a number of governance actions to be voted for on-chain for the hard fork to be enacted. This differs from all previous hard forks, which the pioneering entities ultimately decided.&#x20;

<details>

<summary>What is a GA?</summary>

A governance action (GA) is a proposed on-chain change to Cardano. The various voting groups vote on it, as described within [CIP-1694 Governance Actions](https://github.com/cardano-foundation/CIPs/blob/master/CIP-1694/README.md#governance-actions).

</details>

<details>

<summary>What is the Plutus V3 Cost Model?</summary>

The Plutus Cost Model in Cardano calculates the computational and storage costs of executing Plutus scripts. It assigns costs to various operations within a script, allowing for accurate prediction and fair pricing of script execution. The Plutus V3 cost model applies to Plutus V3 scripts and their primitives.

</details>

<details>

<summary>Why do we need these governance actions for Chang upgrade #2?</summary>

The Chang #2 hard fork will add the ability to use new Plutus primitives within Plutus V3. By updating the Plutus V3 Cost model prior we ensure that developers are able to use the primitives as soon as the Plomin hard fork is enacted.

</details>

<details>

<summary>How do I know which governance actions are real?</summary>

It is encouraged to review and read all governance actions carefully, anyone within the community can raise a governance action for consideration.&#x20;

All governance actions raised by Intersect, on behalf of the community, will be clearly sign posted and the metadata hosted on the Intersect GitHub repository.

</details>

<details>

<summary>Who can vote on these GAs?</summary>

Cardano mainnet is currency within governance bootstrapping, this means the governance model is not fully activated.&#x20;

In this bootstrapping phase only the ICC and the SPOs can vote on governance actions accordingly. This is detailed in CIP-1694 bootstrap phase and interim consitution.

</details>

<details>

<summary>What is governance action 51f4…74#0?</summary>

An erroneous Protocol Parameter Update governance action was submitted to the Cardano mainnet. If ratified and enacted, it would have no on-chain effect.

</details>

<details>

<summary>What went wrong?</summary>

Failure in process maturity. Although the action was tested via Preview and PreProd testnets, processes were not in place to verify the actions. Processes were also not in place to ensure that the tooling being used was correctly versioned.

</details>

<details>

<summary>Why are there metadata errors?</summary>

Shortly after the error was detected, the decision was made to break the metadata anchor used for this governance action. This would then cause downstream tooling to show errors for this action, aiming to reduce the potential negative impact/confusion this action could cause.

</details>

<details>

<summary>Will 51f4…74#0 affect the chain?</summary>

Adversely, no. The impact of 51f4…74#0 is that there is a protocol parameter update on-chain that can be voted on, but it is unlikely to be voted on because it is erroneous.

</details>

<details>

<summary>Will a correct GA be submitted? </summary>

Yes, an amended action with the correct on-chain effect will be submitted shortly in coordination with the Hardfork Working Group and Parameters Committee

</details>

<details>

<summary>What have we learned?</summary>

Governance is hard. Although we developed a process, this was the first time a governance action of this magnitude was raised on mainnet. What we are trying to achieve is complex; this bootstrap phase is a one-off situation.&#x20;

</details>

***

If you find any information on this page incorrect or misleading please email hard-fork@intersectmbo.org and request a correction.&#x20;

