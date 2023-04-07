[View code on GitHub](https://github.com/nervosnetwork/ckb/util/app-config/src/configs/rpc.rs)

The code defines two structs, `Module` and `Config`, that are used to configure and enable various modules for the ckb project's RPC server. The `Module` struct is an enum that lists all the available modules that can be enabled, such as `Net`, `Chain`, `Miner`, etc. The `Config` struct contains various configuration options for the RPC server, such as the listen addresses for the TCP and WS servers, the maximum request body size, the number of worker threads, and the list of enabled modules.

The `Config` struct also has several methods that check whether a particular module is enabled or not. These methods take no arguments and return a boolean value indicating whether the corresponding module is enabled or not. For example, the `net_enable` method checks whether the `Net` module is enabled or not, and returns `true` if it is, and `false` otherwise.

This code is used in the larger ckb project to configure and enable various modules for the RPC server. Developers can use the `Config` struct to customize the RPC server to their needs, and enable only the modules that they require. The `Module` enum provides a list of all the available modules that can be enabled, making it easy for developers to choose which modules they want to use.

Here is an example of how this code might be used in the ckb project:

```rust
use ckb_jsonrpc_types::Script;
use ckb_rpc_config::{Config, Module};

fn main() {
    // Create a new RPC server configuration
    let mut config = Config {
        listen_address: "127.0.0.1:8114".to_string(),
        tcp_listen_address: Some("127.0.0.1:8115".to_string()),
        ws_listen_address: Some("127.0.0.1:8116".to_string()),
        max_request_body_size: 10_000_000,
        threads: Some(4),
        modules: vec![
            Module::Net,
            Module::Chain,
            Module::Miner,
            Module::Pool,
            Module::Stats,
        ],
        reject_ill_transactions: true,
        enable_deprecated_rpc: false,
        extra_well_known_lock_scripts: vec![],
        extra_well_known_type_scripts: vec![],
    };

    // Enable the Subscription module
    config.modules.push(Module::Subscription);

    // Check if the Net module is enabled
    if config.net_enable() {
        println!("Net module is enabled");
    } else {
        println!("Net module is not enabled");
    }
}
```
## Questions: 
 1. What is the purpose of the `ckb_jsonrpc_types::Script` import and how is it used in this code?
   
   The `ckb_jsonrpc_types::Script` import is used to define the `extra_well_known_lock_scripts` and `extra_well_known_type_scripts` fields in the `Config` struct, which allow for customized lock and type scripts to be used in the RPC server.

2. What is the significance of the `#[serde(default)]` attribute used in some of the fields of the `Config` struct?
   
   The `#[serde(default)]` attribute specifies that if a field is missing from the input when deserializing the `Config` struct, it should be set to its default value instead of causing a deserialization error.

3. How are the `Config` struct's `*_enable` methods used in the context of the `Module` enum?
   
   The `*_enable` methods are used to check whether a particular `Module` is enabled in the `Config` struct's `modules` field. This allows for conditional behavior based on which modules are enabled in the RPC server.