[View code on GitHub](https://github.com/nervosnetwork/ckb/util/app-config/src/args.rs)

This file contains various structs that represent parsed command line arguments for different subcommands of the `ckb` command-line tool. Each struct contains fields that represent the parsed arguments for a specific subcommand. 

For example, the `ExportArgs` struct contains the parsed `ckb.toml` configuration, the loaded consensus, and the target directory to save the exported file. Similarly, the `InitArgs` struct contains various fields that represent the parsed arguments for the `ckb init` subcommand, such as the CKB root directory, the chain name, the RPC port, and the P2P port. 

These structs are used throughout the `ckb` project to represent the parsed command line arguments for different subcommands. For example, the `ExportArgs` struct is used in the `export` module to export the current chain data to a file. The `InitArgs` struct is used in the `init` module to initialize a new CKB node with the specified configuration. 

The `CustomizeSpec` struct is used to customize the parameters for the chain spec. It contains a field for specifying a string as the genesis message. The `key_value_pairs` method generates a vector of key-value pairs that can be used to customize the chain spec. 

Overall, this file provides a way to represent the parsed command line arguments for different subcommands of the `ckb` command-line tool. These structs are used throughout the `ckb` project to configure and execute various operations.
## Questions: 
 1. What is the purpose of the `ExportArgs` struct?
- The `ExportArgs` struct represents the parsed command line arguments for the `ckb export` command, including the parsed `ckb.toml`, loaded consensus, and target directory to save the exported file.

2. What is the difference between `RunArgs` and `MinerArgs`?
- `RunArgs` represents the parsed command line arguments for the `ckb run` command, including the parsed `ckb.toml`, loaded consensus, and various options related to running the node. `MinerArgs`, on the other hand, represents the parsed command line arguments for the `ckb miner` command, including the parsed `ckb-miner.toml`, selected PoW algorithm, memory tracker options, and limit on the number of nonces found before the miner process exits.

3. What is the purpose of the `CustomizeSpec` struct?
- The `CustomizeSpec` struct represents the customized parameters for chain spec, including the genesis message. It provides methods to check whether any parameters are unset and to generate a vector of key-value pairs for the parameters. It is used in the `InitArgs` struct for the `ckb init` command.