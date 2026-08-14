# 15th June 2026 - Mainnet hf ga submission - go/no-go decision call

#### Agenda

1. [Hard Fork Submission Readiness](https://docs.google.com/spreadsheets/d/1ECoYFCtrRtFX3BvqfhaZi6FxlXQMoTGP/edit?gid=1419501400#gid=1419501400) - Bosko
2. [Hard Fork Ratification Readiness](https://docs.google.com/spreadsheets/d/1ECoYFCtrRtFX3BvqfhaZi6FxlXQMoTGP/edit?gid=17673737#gid=17673737) - Bosko
3. Hard fork [governance action metadata](https://docs.google.com/document/d/1Yfyq9RvsCPblNborLC1wo03-rbU3zF1O1mIddETpSDs/edit?tab=t.0) - Ryan, Elena
   1. [transaction raw file](https://github.com/IntersectMBO/governance-actions/blob/mainnet-hf-van-rossem/mainnet/2026-06-12-hf-van-rossem/hf.tx-unsigned)
   2. [transaction JSON representation](https://github.com/IntersectMBO/governance-actions/blob/mainnet-hf-van-rossem/mainnet/2026-06-12-hf-van-rossem/hf.tx-unsigned.json)
   3. [transaction via CQuisitor](https://cardananium.github.io/cquisitor/#transaction-validator?cbor=84a400d9010282825820c75bb221606687aa858ec89c7a15c88e9c17054f2e045ae31ecc8a9687cd206e00825820c8a7dc38c2a5590b328ac53971d8e0281c021ba7fb17a36618f3fb5e2b626aa300018182583901076ad93c90e7dafc2ad468212fb2e2701559d1d32f25ebdc1facdada611943783e94de22f533778841521e97f77588fe05447f464be192c91a002afc0f021a0002cf0514d9010281841b000000174876e800581de1192688a334130db2b51aedea594301010b0d1d2e9a86a460932520ba83018258200b19476e40bbbb5e1e8ce153523762e2b6859e7ecacbaf06eae0ee6a447e79b900820b00827842697066733a2f2f6261666b726569616f6e71326f337279713477746b3479346b74326c3735756135786a7275626465676d65766166327168786466677a61696470715820fd12b5dffc3a4ce8d62df824f706ad11076fc3553ef20b410100c80543fed42ea0f5f6\&net=mainnet\&type=Transaction)
   4. [transaction via TxStudio](https://www.transaction.studio/?cbor=84a400d9010282825820c75bb221606687aa858ec89c7a15c88e9c17054f2e045ae31ecc8a9687cd206e00825820c8a7dc38c2a5590b328ac53971d8e0281c021ba7fb17a36618f3fb5e2b626aa300018182583901076ad93c90e7dafc2ad468212fb2e2701559d1d32f25ebdc1facdada611943783e94de22f533778841521e97f77588fe05447f464be192c91a002afc0f021a0002cf0514d9010281841b000000174876e800581de1192688a334130db2b51aedea594301010b0d1d2e9a86a460932520ba83018258200b19476e40bbbb5e1e8ce153523762e2b6859e7ecacbaf06eae0ee6a447e79b900820b00827842697066733a2f2f6261666b726569616f6e71326f337279713477746b3479346b74326c3735756135786a7275626465676d65766166327168786466677a61696470715820fd12b5dffc3a4ce8d62df824f706ad11076fc3553ef20b410100c80543fed42ea0f5f6)
   5. [metadata file JSONLD](https://github.com/IntersectMBO/governance-actions/blob/mainnet-hf-van-rossem/mainnet/2026-06-12-hf-van-rossem/metadata-raw-inline.jsonld)
   6. [metadata markdown representation](https://github.com/IntersectMBO/governance-actions/blob/mainnet-hf-van-rossem/mainnet/2026-06-12-hf-van-rossem/metadata-raw-export.md)
   7. [this was the metadata tweak](https://github.com/IntersectMBO/governance-actions/pull/167/changes/7bd63f3f5c7e29f95baa3bb3390e1e455713e5ac#diff-186701ff7abd4\[%E2%80%A6]ece01275d8ab62fL72) - it was related to improving accuracy of the audits that were conducted
4. Comms - Larisa
   1. Announcement ready should decided to submit hard fork governance action to mainnet
   2. Alternative messaging considered ready should decided not to submit hard fork governance action to mainnet
5. Technical support - Bosko
6. AOB

#### Key materials

* Summary
  * Hard fork working group acknowledges the fact that against the Hard Fork Initiation Submission Policy (v0.2, van Rossem):
    * All [_must see_](https://docs.google.com/spreadsheets/d/1ECoYFCtrRtFX3BvqfhaZi6FxlXQMoTGP/edit?gid=1419501400#gid=1419501400) _for submission_ criteria are fulfilled
    * All [_would like to see_](https://docs.google.com/spreadsheets/d/1ECoYFCtrRtFX3BvqfhaZi6FxlXQMoTGP/edit?gid=1419501400#gid=1419501400) _for submission_ criteria are fulfilled except one - PreProd has been hard forked for 1 epoch against a preferred 2
    * Most of the items from [_would like to see_](https://docs.google.com/spreadsheets/d/1ECoYFCtrRtFX3BvqfhaZi6FxlXQMoTGP/edit?gid=17673737#gid=17673737) for **ratification** is either already completed or on a steady, provable path to success
  * On that basis, the Hard Fork Working Group's position is to recommend submission of the Hard Fork Initiation governance action to mainnet in the current epoch 637, pending Technical Steering Committee ratification
    * The outcome of the vote was (based on the [poll](https://docs.google.com/spreadsheets/d/1on8e9d8c7lksYXAJsVhM7xrOJQA7rhxntp81nSv1hGc/edit?usp=sharing) and explicit messages in the call [chat](https://docs.google.com/document/d/16hKDXdtnsthOoQppeKUUnMl3kHCGP9G6qFQdgy_sSZU/edit?usp=sharing)):
      * 25 in favour
      * 1 against
      * 8 abstain/non-votes
  * If the hard fork governance action is submitted on mainnet before the current epoch 637 ends on 18th June, earliest possible ratification date for it would be 23rd June and earliest possible enactment date would be 28th June
    * It looks like its more likely that it will be in the second half of the governance action duration
    * Possible Ratification Dates
      * June 23rd, June 28th, July 3rd, July 8th, July 13th, July 18th
    * Possible Enactment Dates
      * June 28th, July 3rd, July 8th, July 13th, July 18th, July 23rd
  * Plutus Cost Models protocol parameter update governance action has been ratified and will be enacted on 18th June
  * The expectation is that hard fork governance action and treasury withdrawal actions should be socially separated from the launch perspective
  * [Recording](https://drive.google.com/file/d/1sYjtifaKEpVKm8JlxsAg8HR4Df_8Oq-q/view?usp=drive_link)

#### **Decision(s)**

* The Hard Fork Working Group's position is to recommend submission of the Hard Fork Initiation governance action to mainnet in the current epoch 637, pending Technical Steering Committee ratification

#### **Action items and next steps**

* **Bosko:** [van Rossem upgrade FAQ](https://cardanoupgrades.docs.intersectmbo.org/van-rossem-upgrade/van-rossem-upgrade-faq) should be expanded to include precise information breakdown based on the prepared van Rossem hard fork metadata

