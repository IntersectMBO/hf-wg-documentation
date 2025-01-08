# Hotfix 10.1.4 - notice for SPOs

## Notice for Stake Pool Operators: Hotfix 10.1.4&#x20;

Over the holiday period, a Cardano community member testing on the pre-production network identified a potential issue that could affect node stability under certain conditions once the Plomin hard fork (HF) has been enacted. After investigating this report the developer team confirmed the root cause of the issue and determined how to address it.  A hotfix has been developed that will be included in Cardano Node version 10.1.4.

This hotfix adds safeguards at the mempool level to block specific transaction types. By introducing these enhancements, version 10.1.4 aims to maintain stable block production and reduce the likelihood of disruptions following the Plomin HF.

It is recommended that all node users, especially SPOs and relays upgrade to node version 10.1.4 as soon as practical.

***

### Actions for SPOs

1. **Upgrade to Node 10.1.4**\
   We strongly recommend that all node users, especially SPOs and relays plan to update their environments to Node 10.1.4 , available now via the usual [Cardano releases repository. ](https://github.com/IntersectMBO/cardano-node/releases/tag/10.1.4)
2. **Verify system resources**\
   Please ensure your node infrastructure, particularly CPU and memory resources, can handle both typical and peak activity levels. Adequate provisioning will help maintain uninterrupted block production if transaction volumes spike.
3. **No change to the HF timeline**\
   This hotfix does not affect the governance schedule for the Plomin HF itself. Its goal is simply to reinforce stability following the planned hard fork.

### **Next steps and getting help**

Intersect’s Hard Fork Working Group continues to work closely with stakeholders to ensure a seamless transition. By upgrading to Node 10.1.4, SPOs play a crucial role in safeguarding the network and enabling a successful Plomin hard fork..

For more information and to follow progress, visit the[ Cardano Node repository](https://github.com/input-output-hk/cardano-node) and connect with the Hard Fork Working Group on our official[ Discord](https://discord.gg/). Please reach out through the community forums or support channels with any questions. We appreciate your cooperation in maintaining a secure and reliable Cardano ecosystem.
