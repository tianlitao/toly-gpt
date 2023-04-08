[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/verification/src/genesis_verifier.rs)

The code defines a set of verifiers for the genesis block of the CKB blockchain. The genesis block is the first block in the blockchain and has special rules that are different from other blocks. The verifiers ensure that the genesis block follows these rules.

The `GenesisVerifier` struct is the main entry point for the verifiers. It implements the `Verifier` trait and takes a `Consensus` object as input. The `verify` method of the `GenesisVerifier` struct calls a set of verifiers to ensure that the genesis block is valid. These verifiers include the `NumberVerifier`, `EpochVerifier`, `ParentHashVerifier`, `CellbaseVerifier`, `UnclesVerifier`, and `DAOVerifier`.

The `NumberVerifier` checks that the block number of the genesis block is 0. The `EpochVerifier` checks that the epoch number of the genesis block is 0. The `ParentHashVerifier` checks that the parent hash of the genesis block is the zero hash. The `CellbaseVerifier` checks that the genesis block contains exactly one cellbase transaction, and that the input of the cellbase transaction is valid. The `UnclesVerifier` checks that the genesis block has no uncles. The `DAOVerifier` checks that the DAO field of the genesis block is valid.

The verifiers are implemented as separate structs that implement the `Verifier` trait. Each verifier takes a `BlockView` object as input and returns a `Result<(), Error>` object. If the block fails the verification, an error is returned.

The code is used in the larger CKB project to ensure that the genesis block of the blockchain is valid. The verifiers are called when the genesis block is created to ensure that it follows the special rules for the first block in the blockchain. The verifiers are also used when validating new blocks to ensure that they follow the same rules as the genesis block.
## Questions:
 1. What is the purpose of the `GenesisVerifier` struct and how does it differ from the `BlockVerifier` struct?

   The `GenesisVerifier` struct is used to verify the genesis block of the blockchain, which has different rules than regular blocks. It verifies specific properties of the genesis block, such as its number, epoch, parent hash, and cellbase. In contrast, the `BlockVerifier` struct is used to verify regular blocks and has additional checks for things like block size and transaction validation.

2. What is the `DAOVerifier` struct and what does it verify?

   The `DAOVerifier` struct is used to verify the DAO (decentralized autonomous organization) field of a block's header. It calculates the expected DAO value based on the block's transactions and consensus rules, and checks that it matches the actual DAO value in the header. This helps ensure that the block's rewards and fees are distributed correctly.

3. What is the purpose of the `CellbaseVerifier` struct and what checks does it perform?

   The `CellbaseVerifier` struct is used to verify the cellbase transaction of a block, which is the first transaction and generates new coins for the miner. It checks that the block contains exactly one cellbase transaction, that the cellbase transaction is in the correct position, that its inputs and outputs are valid, and that its input is a valid cellbase input for the block's number.
