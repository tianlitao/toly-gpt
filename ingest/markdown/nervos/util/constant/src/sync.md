[View code on GitHub](https://github.com/nervosnetwork/ckb/util/constant/src/sync.rs)

This code defines various constants related to the download and synchronization of blocks in the ckb project. These constants include timeouts, limits on the number of blocks that can be downloaded at once, and ban times for certain types of messages.

One important constant is MAX_TIP_AGE, which sets the maximum age of the local highest block that is allowed before exiting the Initial Block Download (IBD) state. This ensures that the node is up-to-date with the latest blocks before proceeding with normal operation.

Another set of constants relate to the download scheduler, which determines how many blocks can be requested at one time and how often the scheduler adjusts the number of tasks. These constants help to balance the need for efficient block downloads with the risk of disordering blocks or overwhelming peers with too many requests.

Other constants include timeouts for block downloads and ban times for certain types of messages. These help to prevent malicious behavior and ensure that the network operates smoothly.

Overall, these constants play an important role in ensuring that the ckb network is able to efficiently and securely synchronize blocks between nodes. They can be used throughout the project to set timeouts, limits, and other parameters related to block synchronization. For example, the MAX_TIP_AGE constant could be used in a function that checks whether the local node is up-to-date with the latest blocks, while the MAX_BLOCKS_IN_TRANSIT_PER_PEER constant could be used in a function that determines how many blocks to request from a peer.
## Questions: 
 1. What is the purpose of the constants related to download scheduling?
- The constants define limits and parameters for the download scheduler, including the number of blocks that can be requested at one time, the frequency of inspections, and the maximum number of tasks that can be adjusted.

2. What is the purpose of the constants related to ban times?
- The constants define the default ban times for messages and syncs that are deemed useless or have no common ancestor block.

3. What is the purpose of the constants related to transaction hashes?
- The constants define limits on the number of transaction hashes that can be relayed in a batch and the number of unknown transaction hashes that can be stored per peer and in total.