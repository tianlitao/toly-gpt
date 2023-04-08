[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/util/jsonrpc-types/src/indexer.rs)

This code defines several structs and enums used in the ckb project's indexer module. The purpose of the indexer is to provide a way to search for cells (the basic unit of storage in the ckb blockchain) based on various criteria.

The `IndexerTip` struct represents the current tip of the indexer, which is the highest block number that has been fully indexed.

The `IndexerCell` struct represents a live cell, which is a cell that has not yet been spent. It contains information about the cell's output, output data, and location in the blockchain.

The `IndexerPagination` struct is a generic wrapper around a collection of objects and a cursor used for paging through the collection.

The `IndexerSearchKey` struct represents the search parameters used to query the indexer. It includes a `Script` object, which is used to filter cells based on their script (a program that defines the cell's behavior), as well as several optional filters for other cell properties.

The `IndexerScriptSearchMode` enum represents the search mode used for script filtering, which can be either prefix or exact.

The `IndexerRange` struct represents a range of values, used for filtering cells based on various properties such as script length or output capacity.

The `IndexerSearchKeyFilter` struct represents the optional filters that can be applied to a search query.

The `IndexerScriptType` enum represents the type of script being searched for, which can be either lock or type.

The `IndexerOrder` enum represents the order in which search results should be returned, either ascending or descending.

The `IndexerCellsCapacity` struct represents the total capacity of a collection of cells.

The `IndexerTx` enum represents a transaction returned by the indexer, which can be either ungrouped (with a single cell) or grouped (with multiple cells).

The `IndexerTxWithCell` struct represents an ungrouped transaction, with information about the transaction and the cell it contains.

The `IndexerTxWithCells` struct represents a grouped transaction, with information about the transaction and a collection of cells it contains.

The `IndexerCellType` enum represents the type of cell being returned, either input or output.

Overall, this code provides a set of data structures used to represent the various components of a search query and its results in the ckb indexer module. These structures can be used by other parts of the project to interact with the indexer and retrieve information about cells in the blockchain.
## Questions:
 1. What is the purpose of the `IndexerSearchKey` struct and its fields?
- `IndexerSearchKey` represents the parameters for searching cells in the indexer, including the script to search for, script type, search mode, filters, and other options.

2. What is the difference between `IndexerTx::Ungrouped` and `IndexerTx::Grouped`?
- `IndexerTx::Ungrouped` represents a transaction with a single cell, while `IndexerTx::Grouped` represents a transaction with multiple cells. `IndexerTxWithCell` is used for `Ungrouped` transactions, while `IndexerTxWithCells` is used for `Grouped` transactions.

3. What is the purpose of the `IndexerPagination` struct and its fields?
- `IndexerPagination` is used to provide paging for a collection of objects, with the `objects` field representing the current page of objects and the `last_cursor` field representing the cursor for the next page. It is generic over the type of objects being paginated.
