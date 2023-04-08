[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/util/types/src/extension/capacity.rs)

The code provided contains implementations of methods for calculating the occupied capacity of different types of cells in the CKB blockchain. The occupied capacity is the amount of space a cell takes up in a block. This is important because the amount of space a cell occupies determines the fee that must be paid to include it in a block.

The `Script` struct has a method `occupied_capacity` that calculates the occupied capacity of a script cell. The occupied capacity of a script cell includes the size of the `code_hash` (32 bytes), the `hash_type` (1 byte), and the size of the `args` field (variable size). The `args` field is calculated by calling the `args` method on the `Script` struct and getting the length of the raw data. The method returns a `CapacityResult` which is a type alias for a `Result` with a `Capacity` type.

The `CellOutput` struct has two methods for calculating the occupied capacity of a cell output. The first method, `occupied_capacity`, calculates the occupied capacity of a cell output. The occupied capacity of a cell output includes the size of the `output_data` field (provided), the `capacity` field (8 bytes), the size of the `lock` field (variable size), and the size of the `type` field (variable size). The `lock` and `type` fields are calculated by calling the `occupied_capacity` method on the `lock` and `type_` fields respectively. The `type_` field is optional and must be checked for `None` before calling `occupied_capacity`. The method returns a `CapacityResult` which is a type alias for a `Result` with a `Capacity` type.

The second method in `CellOutput` is `is_lack_of_capacity` which returns a boolean indicating if the `capacity` field of a cell output is smaller than the occupied capacity of the cell output. The method takes a `data_capacity` parameter which is the capacity of the data in the cell output. The method returns a `CapacityResult` which is a type alias for a `Result` with a `bool` type.

The `CellOutputBuilder` struct has a method `build_exact_capacity` which builds a `CellOutput` and sets its `capacity` field equal to its occupied capacity exactly. The method takes a `data_capacity` parameter which is the capacity of the data in the cell output. The method returns a `CapacityResult` which is a type alias for a `Result` with a `packed::CellOutput` type.

The `CellOutputVec` struct has a method `total_capacity` which sums the capacities of all `CellOutput`s in the vector. The method returns a `CapacityResult` which is a type alias for a `Result` with a `Capacity` type.
## Questions:
 1. What is the purpose of the `ckb_occupied_capacity` crate and how is it used in this code?
   - The `ckb_occupied_capacity` crate is used to define a `Result` type for capacity calculations. It is used in this code to return the result of capacity calculations as a `CapacityResult` type.

2. What is the difference between `occupied_capacity` functions in `packed::Script` and `packed::CellOutput`?
   - The `occupied_capacity` function in `packed::Script` calculates the occupied capacity of a script, including the `code_hash`, `hash_type`, and `args`. The `occupied_capacity` function in `packed::CellOutput` calculates the occupied capacity of a cell output, including the `output_data`, `capacity`, `lock`, and `type`.

3. What is the purpose of the `build_exact_capacity` function in `packed::CellOutputBuilder`?
   - The `build_exact_capacity` function in `packed::CellOutputBuilder` builds a `CellOutput` and sets its `capacity` equal to its `occupied capacity` exactly. This is useful for ensuring that the capacity of a cell output is exactly what is needed, without any excess capacity.
