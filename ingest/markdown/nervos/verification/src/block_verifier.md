[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/verification/src/block_verifier.rs)

The `BlockVerifier` struct is a block verifier that is independent of context. It contains several verifiers that are used to verify a block. The verifiers include `CellbaseVerifier`, `BlockBytesVerifier`, `BlockExtensionVerifier`, `BlockProposalsLimitVerifier`, `DuplicateVerifier`, and `MerkleRootVerifier`. The `BlockVerifier` is constructed with a `Consensus` object, which is used to get the maximum block proposals limit and the maximum block bytes.

The `CellbaseVerifier` struct is used to verify the first transaction in a block, which must be a cellbase transaction. The rest of the transactions must not be cellbase transactions. The cellbase outputs/outputs_data length must be less than or equal to 1. The cellbase output data must be empty, and the cellbase output type must be empty. The cellbase has only one dummy input, and the since must be set to the block number.

The `DuplicateVerifier` struct is used to invalidate duplicate transactions or proposals. It checks for duplicate transaction hashes and proposal IDs.

The `MerkleRootVerifier` struct is used to check the merkle root of a block. It checks the transactions root and the proposals hash.

The `BlockProposalsLimitVerifier` struct is used to check the block proposal limit. It checks the number of proposals in a block against the maximum block proposals limit.

The `BlockBytesVerifier` struct is used to check the block size limit. It checks the size of a block against the maximum block bytes.

The `NonContextualBlockTxsVerifier` struct is used to perform context-independent verification checks for block transactions. It uses the `NonContextualTransactionVerifier` to verify each transaction in a block.

Overall, these verifiers are used to ensure that a block is valid and can be added to the blockchain. They are used in the larger project to maintain the integrity of the blockchain and prevent invalid blocks from being added. Here is an example of how to use the `BlockVerifier`:

```rust
let consensus = Consensus::default();
let block = BlockView::default();
let block_verifier = BlockVerifier::new(&consensus);
let result = block_verifier.verify(&block);
assert!(result.is_ok());
```
## Questions:
 1. What is the purpose of the `BlockVerifier` struct and how is it used?

   The `BlockVerifier` struct is used to verify a block's validity by performing several checks that are independent of context. It contains several verifiers such as `CellbaseVerifier`, `BlockBytesVerifier`, `DuplicateVerifier`, and `MerkleRootVerifier`. It implements the `Verifier` trait and is used to verify a `BlockView` by calling its `verify` method.

2. What does the `CellbaseVerifier` struct check for and how is it used?

   The `CellbaseVerifier` struct checks if the first transaction in a block is a cellbase transaction and if it meets certain requirements such as having only one dummy input, having an empty output data, and having no type script. It is used by the `BlockVerifier` struct to verify a block's validity.

3. What is the purpose of the `DuplicateVerifier` struct and how is it used?

   The `DuplicateVerifier` struct is used to check for duplicate transactions or proposals in a block. It is used by the `BlockVerifier` struct to verify a block's validity. It creates two `HashSet`s to keep track of seen transactions and proposals, and returns an error if a duplicate is found.
