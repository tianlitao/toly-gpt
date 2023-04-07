[View code on GitHub](https://github.com/nervosnetwork/ckb/sync/src/synchronizer/block_fetcher.rs)

The `BlockFetcher` struct is responsible for fetching blocks from a peer during the block synchronization process. It is part of the larger `ckb` project, which is a cryptocurrency implementation based on the Nervos CKB blockchain.

The `BlockFetcher` struct has several methods that are used to fetch blocks from a peer. The `new` method creates a new instance of the `BlockFetcher` struct. It takes a `Synchronizer` instance, a `PeerIndex`, and an `IBDState` as input parameters. The `Synchronizer` instance is used to synchronize the blocks between peers. The `PeerIndex` is used to identify the peer from which the blocks are to be fetched. The `IBDState` is used to determine whether the node is in IBD (Initial Block Download) mode.

The `reached_inflight_limit` method checks whether the number of blocks in-flight from the peer has reached the limit. If the limit has been reached, the method returns `true`, indicating that no more blocks can be downloaded from the peer.

The `is_better_chain` method checks whether the header of the block being fetched is on a better chain than the current active chain. If the header is on a better chain, the method returns `true`.

The `peer_best_known_header` method returns the best known header of the peer.

The `update_last_common_header` method updates the last common header between the node and the peer. It takes the best known header of the peer as input and returns the last common header between the node and the peer.

The `fetch` method fetches blocks from the peer. It first checks whether the number of blocks in-flight from the peer has reached the limit. If the limit has been reached, the method returns `None`. If the limit has not been reached, the method updates the best known header of the peer and checks whether the header of the block being fetched is on a better chain than the current active chain. If the header is not on a better chain, the method returns `None`. If the header is on a better chain, the method updates the last common header between the node and the peer and fetches blocks from the peer. The method returns a vector of vectors of block hashes.

Overall, the `BlockFetcher` struct is an important component of the block synchronization process in the `ckb` project. It is used to fetch blocks from a peer and ensure that the node is synchronized with the rest of the network.
## Questions: 
 1. What is the purpose of the `BlockFetcher` struct and its associated methods?
- The `BlockFetcher` struct is used to fetch blocks from peers during block synchronization. Its methods are used to determine which blocks to fetch and from which peers.

2. What is the significance of the `IBDState` enum and how is it used in this code?
- The `IBDState` enum represents the state of the Initial Block Download process. It is used to determine whether to update the `best_known_header` based on an ordered list of unknown headers, and whether to compare block timestamps with the current system time.

3. What is the purpose of the `BLOCK_DOWNLOAD_WINDOW` and `INIT_BLOCKS_IN_TRANSIT_PER_PEER` constants, and how are they used in this code?
- `BLOCK_DOWNLOAD_WINDOW` is the maximum number of blocks to download at once during block synchronization. It is used to limit the number of blocks that can be downloaded from a single peer at a time. `INIT_BLOCKS_IN_TRANSIT_PER_PEER` is the initial number of blocks to request from a peer during block synchronization. It is used to determine the number of blocks to fetch at once and how to split them into chunks.