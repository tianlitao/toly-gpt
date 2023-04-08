[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/util/fixed-hash/macros/src/lib.rs)

This code provides several procedural macros to construct const fixed-sized hashes. The purpose of this code is to make it easier to construct human-readable const fixed-sized hashes that can be checked at compile time, thus avoiding any runtime errors.

The code uses macros to define four functions: `h160`, `h256`, `h512`, and `h520`. These functions take a hexadecimal string or a trimmed hexadecimal string as input and return a const fixed-sized hash. The input string is checked to ensure that it is a hexadecimal string with a 0x-prefix. If the input is malformed, a runtime error is thrown.

The `impl_hash!` macro is used to define these functions. It takes two arguments: the name of the function and the type of the hash. If the type of the hash is not specified, it defaults to the name of the function. The macro generates a docstring for each function that explains how to use it and provides a link to the corresponding documentation.

This code is part of the `ckb_fixed_hash` crate and is not intended to be used directly. All proc-macros in this crate are re-exported in the `ckb_fixed_hash` crate, where examples can be found.

Example usage of the `h256` function:

```rust
use ckb_fixed_hash_macros::h256;

const MY_HASH: [u8; 32] = h256!("0x1234567890123456789012345678901234567890123456789012345678901234");
```
## Questions:
 1. What is the purpose of this code?

    This code provides proc-macros to construct const fixed-sized hashes in a human-readable way, which will be checked in compile time and never cause any runtime error. It is an internal crate used by crate `ckb_fixed_hash`, and all proc-macros in this crate are re-exported in crate `ckb_fixed_hash`.

2. Why is it difficult to construct const fixed-sized hashes using an array or `FromStr::from_str`?

    If we use an array to construct const fixed-sized hashes, it's difficult to read. If we use `FromStr::from_str` to construct fixed-sized hashes, the result is not a constant, which will reduce runtime performance and could cause a runtime error if the input is malformed.

3. What is the format of the input that the proc-macros expect?

    The input has to be a hexadecimal string with 0x-prefix. The proc-macros can create a const fixed-sized hash from a hexadecimal string or a trimmed hexadecimal string.
