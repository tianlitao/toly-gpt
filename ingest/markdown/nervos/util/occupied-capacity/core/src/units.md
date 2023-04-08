[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/util/occupied-capacity/core/src/units.rs)

The code defines two structs, `Capacity` and `Ratio`, and several traits and implementations for them.

`Capacity` represents the capacity of a cell in the CKB blockchain. It is encoded as the amount of `Shannons` internally. `Shannons` is the smallest unit of CKB, and 1 CKB equals 10^8 Shannons. The `Capacity` struct has several methods to convert between different units of capacity, such as `shannons`, `bytes`, and `safe_mul_ratio`. It also has methods to perform arithmetic operations, such as `safe_add`, `safe_sub`, and `safe_mul`, which check for overflow errors.

`Ratio` represents the ratio `numerator / denominator`, where `numerator` and `denominator` are both unsigned 64-bit integers. It has methods to get the numerator and denominator of the ratio.

The code also defines a trait `IntoCapacity` and several implementations of it for different types, such as `u64`, `u32`, `u16`, and `u8`. The `IntoCapacity` trait allows these types to be converted into `Capacity`.

Overall, this code provides a way to represent and manipulate capacity in the CKB blockchain. It can be used in the larger project to calculate and manage the capacity of cells in the blockchain.

Example usage:

```rust
use ckb::Capacity;

// Create a capacity of 100 Shannons
let cap = Capacity::shannons(100);

// Convert 1 CKByte to capacity
let cap_bytes = Capacity::bytes(1).unwrap();

// Add two capacities
let cap_sum = cap.safe_add(cap_bytes).unwrap();

// Multiply a capacity with a ratio
let ratio = Ratio::new(1, 2);
let cap_ratio = cap.safe_mul_ratio(ratio).unwrap();
```
## Questions:
 1. What is the purpose of the `Ratio` struct and its methods?
- The `Ratio` struct represents a ratio of two unsigned 64-bit integers and provides methods to access its numerator and denominator.

2. What is the significance of the `BYTE_SHANNONS` constant?
- The `BYTE_SHANNONS` constant represents the number of `Shannons` in one byte.

3. What is the purpose of the `IntoCapacity` trait and its implementations?
- The `IntoCapacity` trait provides a way to convert various integer types into `Capacity` instances, allowing for more flexible usage of the `Capacity` struct. The implementations allow for conversion from `u64`, `u32`, `u16`, and `u8` types.
