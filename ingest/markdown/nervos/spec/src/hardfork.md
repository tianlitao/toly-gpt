[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/spec/src/hardfork.rs)

The `HardForkConfig` module is responsible for defining the hard fork parameters for the CKB (Nervos Common Knowledge Base) blockchain. Hard forks are a mechanism used to introduce new features or changes to the blockchain protocol. The `HardForkConfig` module defines the parameters for each hard fork, which are then used to create a `HardForkSwitch` object that can be used to enable or disable specific features at specific epochs.

The `HardForkConfig` struct is defined with several fields, each corresponding to a specific hard fork parameter. Each field is optional and can be set to `None` if the parameter is not applicable for a particular hard fork. The struct also implements several methods that can be used to create a `HardForkSwitch` object based on the defined parameters.

The `complete_mainnet` and `complete_testnet` methods create a `HardForkSwitch` object with default values for all parameters that have not been set. These methods are used to create a `HardForkSwitch` object for the mainnet and testnet respectively.

The `complete_with_default` method creates a `HardForkSwitch` object with default values for all parameters that have not been set, but allows the user to specify a default epoch number for any unset parameters.

The `update_builder_via_edition` method is used internally to update a `HardForkSwitchBuilder` object with the defined hard fork parameters. This method is called by the `complete_mainnet` and `complete_testnet` methods.

Overall, the `HardForkConfig` module is an important part of the CKB blockchain, as it defines the hard fork parameters that are used to enable or disable specific features at specific epochs. By defining these parameters, the module allows for the introduction of new features and changes to the blockchain protocol in a controlled and predictable manner.
## Questions:
 1. What is the purpose of this code?
   - This code defines a struct `HardForkConfig` that contains parameters for various hard forks in the CKB blockchain, and provides methods to complete the hard fork switch for mainnet, testnet, or a user-provided epoch.

2. What are some of the hard fork parameters included in this code?
   - Some of the hard fork parameters included in this code are `rfc_0028`, `rfc_0029`, `rfc_0030`, `rfc_0031`, `rfc_0032`, `rfc_0036`, and `rfc_0038`. Each parameter corresponds to a specific hard fork and is an optional `EpochNumber`.

3. What is the purpose of the `check_default!` macro?
   - The `check_default!` macro is used to check if a hard fork parameter has been set for `mainnet` or `testnet`, and if so, return an error message. If the parameter has not been set, the macro returns a default value. This is used in the `update_builder_via_edition` method to update the `HardForkSwitchBuilder` with the appropriate hard fork parameters.
