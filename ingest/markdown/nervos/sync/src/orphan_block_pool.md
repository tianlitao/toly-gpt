[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/sync/src/orphan_block_pool.rs)

The code defines a data structure called `OrphanBlockPool` that is used to store orphaned blocks in a blockchain network. Orphaned blocks are blocks that have a parent block that is not yet available in the network. The purpose of the `OrphanBlockPool` is to keep track of these orphaned blocks until their parent blocks become available.

The `OrphanBlockPool` is implemented using a hash map that groups blocks by their parent hash. The hash map is called `InnerPool` and is defined as a private struct within the `OrphanBlockPool`. The `InnerPool` struct also contains two other hash maps: `parents` and `leaders`. The `parents` hash map maps a block hash to its parent hash, while the `leaders` hash set contains the parent hashes of all blocks that are not orphaned but have at least one child block in the pool.

The `OrphanBlockPool` provides several methods to insert, remove, and retrieve blocks from the pool. When a block is inserted into the pool using the `insert` method, it is added to the `blocks` hash map under its parent hash. If the parent block is not already in the pool, its hash is added to the `leaders` hash set. If the parent block is already in the pool, the `leaders` hash set is updated to remove the child block's hash.

The `remove_blocks_by_parent` method removes all blocks in the pool that have a given parent hash. It does this by first checking if the parent hash is in the `leaders` hash set. If it is not, it returns an empty vector. If it is, it removes all blocks in the `blocks` hash map that have the given parent hash and returns them in a vector. It also removes the block hashes from the `parents` hash map and updates the `leaders` hash set to remove the parent hash.

The `get_block` method retrieves a block from the pool given its hash. It does this by first looking up the block's parent hash in the `parents` hash map. If the parent hash is found, it looks up the block's hash in the `blocks` hash map under the parent hash. If the block is found, it is returned. Otherwise, `None` is returned.

The `clean_expired_blocks` method removes all blocks from the pool that have an epoch number that is more than `EXPIRED_EPOCH` epochs behind the current epoch number. It does this by iterating over all parent hashes in the `leaders` hash set and checking if the first block in the `blocks` hash map under each parent hash has an epoch number that is more than `EXPIRED_EPOCH` epochs behind the current epoch number. If it does, all blocks in the chain starting from the first block are removed from the pool and their hashes are returned in a vector.

The `OrphanBlockPool` is thread-safe and uses a `RwLock` to ensure that multiple threads can access it concurrently. The `OrphanBlockPool` is used in the larger project to keep track of orphaned blocks in the network and to ensure that they are not lost when their parent blocks become available.
## Questions:
 1. What is the purpose of the `OrphanBlockPool` struct and how is it used?
- The `OrphanBlockPool` struct is used to store orphaned blocks, which are blocks that have a missing parent block. It has methods to insert, remove, and retrieve blocks, as well as to clean up expired blocks.

2. What is the significance of the `leaders` field in the `InnerPool` struct?
- The `leaders` field in the `InnerPool` struct is a set of parent block hashes that are not in the orphan pool but have at least one child block in the pool. These blocks are considered "leaders" and are used to determine which blocks can be removed when cleaning up expired blocks.

3. What is the purpose of the `need_clean` method in the `InnerPool` struct?
- The `need_clean` method in the `InnerPool` struct is used to determine if a parent block needs to be cleaned up because it and its descendants have expired. It checks the epoch number of the first block belonging to the parent and returns true if it is older than the current epoch number plus a constant value.
