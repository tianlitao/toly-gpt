[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/store/src/cell.rs)

This code is part of the ckb project and defines two functions that modify the live cell set of a blockchain. The live cell set is a collection of unspent transaction outputs (UTXOs) that are available for spending. The two functions are `attach_block_cell` and `detach_block_cell`, which respectively apply and undo the effects of a block on the live cell set.

The `attach_block_cell` function takes a `StoreTransaction` and a `BlockView` as input. It first extracts all transactions from the block and then adds new live cells to the live cell set. For each transaction, it iterates over its outputs with data and creates a new `CellEntry` and `CellDataEntry` for each output. The `CellEntry` contains information about the output, such as its `cell_output`, `block_hash`, `block_number`, `block_epoch`, `index`, and `data_size`. The `CellDataEntry` contains the output's data and its hash. If the output has no data, the `CellDataEntry` is set to `None`. The `CellEntry` and `CellDataEntry` are then added to the `StoreTransaction` using `txn.insert_cells`. Finally, the function marks all inputs as dead by deleting them from the live cell set using `txn.delete_cells`.

The `detach_block_cell` function takes a `StoreTransaction` and a `BlockView` as input. It first extracts all transactions from the block and then restores all inputs that were marked as dead by the `attach_block_cell` function. For each transaction, it iterates over its input points and creates a new `CellEntry` and `CellDataEntry` for each input. The `CellEntry` contains information about the input, such as its `cell_output`, `block_hash`, `block_number`, `block_epoch`, `index`, and `data_size`. The `CellDataEntry` contains the input's data and its hash. If the input has no data, the `CellDataEntry` is set to `None`. The `CellEntry` and `CellDataEntry` are then added to the `StoreTransaction` using `txn.insert_cells`. Finally, the function undoes all live cells that were added by the `attach_block_cell` function by deleting them from the live cell set using `txn.delete_cells`.

Overall, these functions are used to maintain the integrity of the live cell set when new blocks are added or removed from the blockchain. They are called by other parts of the ckb project that deal with block validation and storage. For example, the `attach_block_cell` function is called by the `ChainController` when a new block is added to the blockchain, while the `detach_block_cell` function is called by the `ChainController` when a block is removed from the blockchain.
## Questions:
 1. What is the purpose of the `attach_block_cell` function?
- The `attach_block_cell` function applies the effects of a block on the live cell set by adding new live cells and marking inputs dead.

2. What is the purpose of the `CellEntry` and `CellDataEntry` structs?
- The `CellEntry` and `CellDataEntry` structs define the structure of a live cell entry and its data.

3. What is the purpose of the `detach_block_cell` function?
- The `detach_block_cell` function undoes the effects of a block on the live cell set by restoring inputs and undoing live cells.
