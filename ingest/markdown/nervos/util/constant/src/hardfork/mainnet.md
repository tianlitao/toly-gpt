[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/util/constant/src/hardfork/mainnet.rs)

This code defines several constants related to the CKB (Nervos Network) blockchain.

The first constant, `CHAIN_SPEC_NAME`, is a string that represents the name of the chain specification. This constant is likely used throughout the project to identify the specific chain being used.

The next two constants, `RFC0028_START_EPOCH` and `CKB2021_START_EPOCH`, are both unsigned 64-bit integers that represent the starting epoch numbers for different versions of the CKB blockchain. The `RFC0028_START_EPOCH` constant is hard-coded to a specific epoch number defined in the RFC0028 specification, while the `CKB2021_START_EPOCH` constant is currently set to 0, but will likely be updated to a specific epoch number in the future.

These constants are likely used throughout the CKB project to define and reference specific epochs within the blockchain. For example, they may be used in consensus rules, block validation, or other areas where specific epoch numbers are required.

Here is an example of how these constants might be used in code:

```rust
if current_epoch >= RFC0028_START_EPOCH {
    // perform RFC0028-specific logic
} else if current_epoch >= CKB2021_START_EPOCH {
    // perform CKB2021-specific logic
} else {
    // perform default logic
}
```

In this example, the code checks the current epoch number against the `RFC0028_START_EPOCH` and `CKB2021_START_EPOCH` constants to determine which version of the blockchain is being used, and performs different logic accordingly.
## Questions:
 1. What is the purpose of the `CHAIN_SPEC_NAME` constant?
   - The `CHAIN_SPEC_NAME` constant is used to specify the name of the chain specification.

2. Why is the `CKB2021_START_EPOCH` constant commented out and replaced with a value of 0?
   - The `CKB2021_START_EPOCH` constant was likely commented out because it was not yet finalized or implemented, and a value of 0 was used as a placeholder.

3. What is the significance of the `RFC0028_START_EPOCH` constant?
   - The `RFC0028_START_EPOCH` constant hardcodes the epoch number for the RFC0028 epoch, which is a specific epoch used in the CKB blockchain protocol.
