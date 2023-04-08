[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/util/app-config/src/configs/notify.rs)

The code defines a Rust struct called `Config` that represents a set of configuration options for notifying events in a blockchain system. The struct has several fields, each of which is an optional string or integer value. The fields are:

- `new_block_notify_script`: an executable script that is called whenever a new block is added to the blockchain. The script is passed the hash of the new block as an argument.
- `network_alert_notify_script`: an executable script that is called whenever a new network alert is received. The script is passed the alert message as an argument.
- `notify_tx_timeout`: a timeout value in milliseconds for notifying transactions.
- `notify_alert_timeout`: a timeout value in milliseconds for notifying alerts.
- `script_timeout`: a timeout value in milliseconds for executing scripts.

The `Config` struct also derives several traits, including `Clone`, `Debug`, `PartialEq`, `Serialize`, `Deserialize`, `Default`, and `Eq`. The `Serialize` and `Deserialize` traits are provided by the `serde` crate, which is used to serialize and deserialize the `Config` struct to and from TOML format.

The `at_least_100` function is a helper function that is used to deserialize the `notify_tx_timeout`, `notify_alert_timeout`, and `script_timeout` fields. It ensures that the deserialized value is at least 100, and returns an error if it is not.

The `tests` module contains a single test function that tests the deserialization of a TOML string into a `Config` struct. The test ensures that an error is returned if the `script_timeout` field is less than 100, and that no error is returned if it is greater than or equal to 100.

Overall, this code provides a way to configure notification options for a blockchain system, including scripts to be executed when certain events occur, and timeout values for notifying events. It is likely used in conjunction with other modules in the `ckb` project to provide a complete blockchain system. An example usage of the `Config` struct might look like this:

```rust
use ckb::Config;

let config = Config {
    new_block_notify_script: Some("notify_new_block.sh".to_string()),
    network_alert_notify_script: Some("notify_network_alert.sh".to_string()),
    notify_tx_timeout: Some(5000),
    notify_alert_timeout: Some(10000),
    script_timeout: Some(30000),
};

// Serialize the config to TOML format
let toml_string = toml::to_string(&config).unwrap();

// Deserialize the TOML string back into a Config struct
let deserialized_config = toml::from_str::<Config>(&toml_string).unwrap();
```
## Questions:
 1. What is the purpose of this code?
- This code defines a struct called `Config` that contains options for notifying scripts when certain events occur in a blockchain.

2. What are the possible values for `notify_tx_timeout`, `notify_alert_timeout`, and `script_timeout`?
- These fields are all optional `u64` values that default to at least 100. They are used to specify timeouts for different types of notifications.

3. What is the purpose of the `at_least_100` function?
- This function is used as a deserializer for the `notify_tx_timeout`, `notify_alert_timeout`, and `script_timeout` fields. It ensures that the deserialized value is at least 100, returning an error if it is not.
