[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/util/types/src/core/hardfork.rs)

The code defines a `HardForkSwitch` struct and a `HardForkSwitchBuilder` struct, which are used to manage hard forks in the CKB (Nervos Network) blockchain. The `HardForkSwitch` struct contains fields for each hard fork feature, represented as an `EpochNumber`. The `HardForkSwitchBuilder` struct is used to build a `HardForkSwitch` instance with the desired hard fork features enabled.

The `define_methods!` macro is used to define methods for each hard fork feature. These methods are used to get the epoch number when a feature is enabled, check if a feature is enabled at a given epoch number, disable a feature, and get a description of the feature. The macro generates code for each feature, which includes an implementation of these methods for the `HardForkSwitch` and `HardForkSwitchBuilder` structs.

The `HardForkSwitch` struct has methods to create a new builder, create a new instance with all features disabled, and get a vector of epoch numbers when features that require refreshing tx-pool caches will be enabled. The `HardForkSwitchBuilder` struct has a `build` method that returns a `HardForkSwitch` instance with the configured features enabled.

Overall, this code provides a way to manage hard forks in the CKB blockchain by enabling and disabling features at specific epoch numbers. The `define_methods!` macro makes it easy to add new hard fork features and generate the necessary code for managing them.
## Questions:
 1. What is the purpose of the `define_methods!` macro and how is it used in this code?
- The `define_methods!` macro defines methods for each feature of the hard fork switch, including getter methods, methods to check if a feature is enabled, and methods to disable a feature. It is used to generate these methods for each feature in the `HardForkSwitch` and `HardForkSwitchBuilder` structs.

2. What is the purpose of the `HardForkSwitch` and `HardForkSwitchBuilder` structs?
- The `HardForkSwitch` struct is used to select hard fork features based on the epoch number, and the `HardForkSwitchBuilder` struct is used to build an instance of `HardForkSwitch` with specific features enabled or disabled.

3. What is the purpose of the `script_result_changed_at` method in the `HardForkSwitch` struct?
- The `script_result_changed_at` method returns a vector of epoch numbers at which new features that require refreshing tx-pool caches will be enabled.
