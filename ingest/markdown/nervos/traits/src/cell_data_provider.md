[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/traits/src/cell_data_provider.rs)

The code defines a trait called `CellDataProvider` that provides methods for loading and fetching cell data and cell data hashes. This trait is used for cell data storage in the larger ckb project.

The `load_cell_data` method loads cell data from memory if it exists, otherwise it falls back to storage access. It takes a `CellMeta` object as an argument and returns an `Option<Bytes>` object. If the `mem_cell_data` field of the `CellMeta` object is not `None`, it returns a copy of the data. Otherwise, it calls the `get_cell_data` method of the trait implementation with the `out_point` field of the `CellMeta` object as an argument.

The `load_cell_data_hash` method is similar to `load_cell_data`, but it loads the cell data hash instead of the data itself. It takes a `CellMeta` object as an argument and returns an `Option<Byte32>` object. If the `mem_cell_data_hash` field of the `CellMeta` object is not `None`, it returns a copy of the hash. Otherwise, it calls the `get_cell_data_hash` method of the trait implementation with the `out_point` field of the `CellMeta` object as an argument.

The `get_cell_data` method fetches cell data from storage. It takes an `OutPoint` object as an argument and returns an `Option<Bytes>` object.

The `get_cell_data_hash` method fetches the cell data hash from storage. It takes an `OutPoint` object as an argument and returns an `Option<Byte32>` object. This method is designed to facilitate caching, as loading a large amount of cell data and calculating the hash may be a performance bottleneck. In unit tests or other scenarios that are not performance bottlenecks, the results of `get_cell_data` can be used to calculate the hash as a default implementation.

Overall, this code provides a flexible and efficient way to store and fetch cell data and cell data hashes in the ckb project. It allows for memory caching and facilitates performance optimization.
## Questions:
 1. What is the purpose of the `CellDataProvider` trait?
   - The `CellDataProvider` trait is used for cell_data storage.
2. What does the `load_cell_data` function do?
   - The `load_cell_data` function loads cell_data from memory and falls back to storage access if necessary.
3. Why is there a separate function `get_cell_data_hash` for fetching cell_data_hash from storage?
   - There is a separate function `get_cell_data_hash` for fetching cell_data_hash from storage because loading a large amount of cell data and calculating hash may be a performance bottleneck, so this function is designed to facilitate caching.
