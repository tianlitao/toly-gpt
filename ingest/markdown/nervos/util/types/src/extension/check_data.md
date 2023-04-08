[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/util/types/src/extension/check_data.rs)

This code provides a set of functions for verifying the correctness of binary data structures used in the ckb project. The functions are implemented as extensions to various reader types defined in the `packed` module.

The `Blockchain` section of the code provides functions for checking the correctness of data structures related to the blockchain, such as scripts, cell outputs, cell dependencies, and transactions. For example, the `check_data` function for `CellOutputReader` checks that both the lock and type scripts of a cell output are valid by calling their respective `check_data` functions. Similarly, the `check_data` function for `RawTransactionReader` checks that the number of outputs matches the number of output data items, and that the cell dependencies and outputs are valid.

The `Network` section of the code provides functions for checking the correctness of data structures related to network communication, such as block transactions and relay transactions. For example, the `check_data` function for `BlockTransactionsReader` recursively checks that all transactions in a block are valid by calling their respective `check_data` functions. Similarly, the `check_data` function for `RelayTransactionsReader` recursively checks that all relay transactions are valid.

These functions are used throughout the ckb project to ensure that binary data structures are correctly formed and can be safely processed by other parts of the system. For example, when receiving a block over the network, the `check_data` function for `SendBlockReader` can be used to verify that the block is valid before processing it further.

Example usage:

```
use crate::packed::BlockReader;

fn process_block_data(data: &[u8]) {
    let block_reader = BlockReader::from_compatible_slice(data).unwrap();
    if block_reader.check_data() {
        // process block
    } else {
        // handle invalid block
    }
}
```
## Questions:
 1. What is the purpose of the `check_data` function in each of the implemented readers?
- The `check_data` function is used to recursively verify the correctness of the binary data structure for each reader.

2. What is the difference between the `packed` and `core` modules used in this code?
- The `packed` module contains packed structs that represent binary data structures, while the `core` module contains high-level data structures and logic for the blockchain.

3. Why are some of the `check_data` functions marked as `pub` while others are not?
- The `pub` functions are intended to be used by external modules, while the non-`pub` functions are only used internally within the `ckb` module.
