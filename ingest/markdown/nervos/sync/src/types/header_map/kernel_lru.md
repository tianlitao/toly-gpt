[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/sync/src/types/header_map/kernel_lru.rs)

The code defines a struct called `HeaderMapKernel` that is used as a key-value store for `HeaderView` objects. The `HeaderView` is a type defined in another module of the project. The `HeaderMapKernel` struct has two fields: `memory` and `backend`. The `memory` field is of type `MemoryMap`, which is another struct defined in the same module. The `backend` field is of type `Backend`, which is a generic type that implements the `KeyValueBackend` trait. The `KeyValueBackend` trait is not defined in this module, but it is assumed to be defined elsewhere in the project.

The `HeaderMapKernel` struct has several methods that allow for inserting, removing, and querying `HeaderView` objects. The `contains_key` method checks if a given `Byte32` hash is present in the `memory` or `backend` fields. The `get` method retrieves a `HeaderView` object from the `memory` or `backend` fields based on a given `Byte32` hash. The `insert` method inserts a `HeaderView` object into the `memory` field. The `remove` method removes a `HeaderView` object from the `memory` and `backend` fields based on a given `Byte32` hash. The `limit_memory` method limits the size of the `memory` field by moving some of its contents to the `backend` field.

The `HeaderMapKernel` struct also has some fields and methods related to statistics. If the `stats` feature is enabled, the struct has a `stats` field of type `Mutex<HeaderMapKernelStats>`. The `HeaderMapKernelStats` struct is also defined in the same module. The `HeaderMapKernelStats` struct has several fields that keep track of the number of times certain methods are called. The `trace` method is used to print out the statistics periodically. The `stats` method is used to acquire a lock on the `stats` field.

Overall, the `HeaderMapKernel` struct provides a key-value store for `HeaderView` objects that can be used to store and retrieve headers in the CKB blockchain. The `memory` field is used for fast access to recently accessed headers, while the `backend` field is used for less frequently accessed headers. The statistics-related fields and methods are used to monitor the performance of the key-value store.
## Questions:
 1. What is the purpose of the `HeaderMapKernel` struct and what does it contain?
- The `HeaderMapKernel` struct is a key-value store for `HeaderView` objects. It contains a `MemoryMap` and a `KeyValueBackend`, as well as configuration and statistics fields.

2. What is the purpose of the `contains_key` method and how does it work?
- The `contains_key` method checks if a given `Byte32` hash is present in the `MemoryMap` or `KeyValueBackend`. If it is present in the `MemoryMap`, the method returns `true`. If it is not present in the `MemoryMap` and the `KeyValueBackend` is empty, the method returns `false`. Otherwise, the method checks if the hash is present in the `KeyValueBackend` and returns `true` or `false` accordingly.

3. What is the purpose of the `trace` method and when is it called?
- The `trace` method is called when the `HeaderMapKernel` is compiled with the `stats` feature. It outputs statistics about the key-value store to the log, including the number of items in the `MemoryMap` and `KeyValueBackend`, as well as the number of times certain methods have been called. The `trace` method is called periodically based on a frequency parameter.
