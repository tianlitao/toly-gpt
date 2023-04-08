[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/sync/src/relayer/compact_block_process.rs)

The `CompactBlockProcess` struct and its associated methods define the logic for processing a compact block message received from a peer in the CKB project.

When a compact block message is received, the `execute` method is called to process the message. The method first performs a non-contextual check on the compact block to ensure that it meets certain criteria, such as having a height greater than the current epoch length. If the block passes this check, a contextual check is performed to ensure that the block is not already stored in the database, that its parent block is not stored in the database, and that the compact header is valid. If the block passes both checks, it is reconstructed and accepted.

If the block fails either check, a status code is returned indicating the reason for the failure. If the block is missing transactions or uncles, a request is sent to the peer for the missing data. If the reconstructed block has a different transactions root than the original compact block, the node may ban the peer but does not mark the block as invalid, as the block hash may be wrong due to short ID collisions.

The `CompactBlockProcess` struct also defines a `CompactBlockMedianTimeView` struct that implements the `HeaderProvider` trait. This is used to provide the median time context for compact block header verification.

Overall, the `CompactBlockProcess` struct and its associated methods play an important role in ensuring the validity of compact block messages received from peers in the CKB project.
## Questions:
 1. What is the purpose of the `CompactBlockProcess` struct and its `execute` method?
- The `CompactBlockProcess` struct is responsible for processing a received compact block message.
- The `execute` method performs various checks on the compact block and its header, requests missing transactions and uncles from the peer if necessary, reconstructs the block, and accepts it if it is valid.

2. What are the potential reasons for a `StatusCode::CompactBlockIsStaled` error to be returned from the `non_contextual_check` function?
- The `non_contextual_check` function checks if the compact block's height is greater than the current tip minus the epoch length.
- If the compact block's height is lower than this threshold, it is considered stale and the `CompactBlockIsStaled` error is returned.

3. What is the purpose of the `CompactBlockMedianTimeView` struct and how is it used in the `contextual_check` function?
- The `CompactBlockMedianTimeView` struct implements the `HeaderProvider` trait and is used to provide a median time context for header verification.
- In the `contextual_check` function, an instance of `CompactBlockMedianTimeView` is created with a closure that retrieves pending headers from the `pending_compact_blocks` map.
- This median time context is then used to create a `HeaderVerifier` instance, which is used to verify the compact block's header.
