[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/util/types/src/core/reward.rs)

The code defines several structs related to the rewards and issuance of the native token in the CKB project. These structs are used to represent the details of miner rewards issued by the block cellbase transaction, native token issuance, miner reward, and the rewards details for a block when it is finalized.

The `BlockReward` struct contains information about the total block reward, primary block reward, secondary block reward, transaction fees rewarded to miners because the transaction is committed in the block, and transaction fees rewarded to miners because the transaction is proposed in the block or its uncles. The `BlockIssuance` struct contains information about the primary and secondary issuance of the native token. The `MinerReward` struct contains information about the miner's reward, including the primary and secondary issuance, transaction fees for committed and proposed transactions. Finally, the `BlockEconomicState` struct includes the rewards details for a block and when the block is finalized.

The purpose of these structs is to provide a way to represent the rewards and issuance of the native token in the CKB project. They can be used in various parts of the project where such information is required. For example, the `BlockEconomicState` struct can be used to represent the economic state of a block, which can be useful for various purposes such as analyzing the network's economic activity.

The code also includes an implementation of the `From` trait for the `MinerReward` struct, which allows the conversion of a `BlockReward` struct to a `MinerReward` struct. This can be useful when working with both types of structs and needing to convert between them.

Overall, this code provides a way to represent and work with the rewards and issuance of the native token in the CKB project, which is an essential aspect of the project's economic model.
## Questions:
 1. What is the purpose of this code and how does it relate to the ckb project?
- This code defines structs that represent the rewards and issuance details for a block in the ckb blockchain.

2. What is the difference between primary and secondary block rewards?
- Primary block rewards are issued to miners for creating a new block, while secondary block rewards are issued based on the amount of CKB used to store state and deposited and locked in the NervosDAO.

3. How are transaction fees rewarded to miners in a block?
- Miners receive 60% of the transaction fee for each transaction committed in the block and 40% of the transaction fee for each transaction proposed in the block and committed later in its active commit window.
