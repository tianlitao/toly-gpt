[View code on GitHub](https://github.com/nervosnetwork/ckb/util/fixed-hash/core/src/std_str.rs)

This code defines several constants and macros for converting hexadecimal strings to fixed-size binary data types. The purpose of this code is to provide a convenient way to convert hexadecimal strings to binary data types that are commonly used in the CKB project.

The code defines two arrays, `DICT_HEX_LO` and `DICT_HEX_HI`, which are used to convert hexadecimal characters to their corresponding binary values. The `impl_std_str_fromstr` macro is used to implement the `FromStr` trait for the `H160`, `H256`, `H512`, and `H520` types, which allows these types to be constructed from hexadecimal strings. The `impl_from_trimmed_str` macro is used to implement a custom `from_trimmed_str` method for these types, which allows them to be constructed from hexadecimal strings that have been trimmed of leading zeros.

The `H160`, `H256`, `H512`, and `H520` types are fixed-size binary data types that are commonly used in the CKB project. The `H160` type represents a 160-bit hash value, the `H256` type represents a 256-bit hash value, the `H512` type represents a 512-bit hash value, and the `H520` type represents a 520-bit hash value. These types are used to represent various types of data in the CKB project, such as transaction hashes, block hashes, and cell data hashes.

The `from_trimmed_str` method provided by this code is useful because it allows hexadecimal strings to be converted to binary data types without having to worry about leading zeros. This is important because leading zeros can be omitted in some contexts, such as when representing a hash value in a JSON-RPC response. By providing a method that can handle trimmed hexadecimal strings, this code makes it easier to work with hash values in the CKB project.

Example usage:

```rust
use ckb_fixed_hash::{H160, H256};

let h160 = H160::from_trimmed_str("0x1234567890abcdef1234567890abcdef12345678").unwrap();
let h256 = H256::from_str("0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef").unwrap();
```
## Questions: 
 1. What is the purpose of the `DICT_HEX_LO` and `DICT_HEX_HI` static arrays?
   - These arrays are used to convert hexadecimal characters to their corresponding byte values. `DICT_HEX_LO` is used for even-indexed characters and `DICT_HEX_HI` is used for odd-indexed characters.
2. What is the difference between the `impl_std_str_fromstr` and `impl_from_trimmed_str` macros?
   - `impl_std_str_fromstr` is used to implement the `FromStr` trait for types that can be parsed directly from a hexadecimal string of a fixed length. `impl_from_trimmed_str` is used to implement the `FromStr` trait for types that can be parsed from a hexadecimal string of variable length, with leading zeros omitted.
3. What is the purpose of the `DICT_HEX_ERROR` constant?
   - This constant is used as a sentinel value in the `DICT_HEX_LO` and `DICT_HEX_HI` arrays to indicate that a given character is not a valid hexadecimal character.