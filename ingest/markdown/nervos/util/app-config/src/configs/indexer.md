[View code on GitHub](https://github.com/nervosnetwork/ckb/util/app-config/src/configs/indexer.rs)

The code defines a struct `IndexerConfig` that holds configuration options for an indexer. The struct has several fields, including `store`, `secondary_path`, `poll_interval`, `index_tx_pool`, `block_filter`, `cell_filter`, `db_background_jobs`, and `db_keep_log_file_num`. These fields are used to configure the indexer's behavior, such as where to store the index, how often to poll for new blocks, and whether to index transactions in the CKB transaction pool.

The `IndexerConfig` struct implements the `Default` trait, which provides a default configuration for the indexer. The `adjust` method is used to canonicalize paths in the configuration options. If the `store` or `secondary_path` fields are not set, they are set to default values based on the `indexer_dir` parameter. If the paths are relative, they are converted to absolute paths using the `root_dir` parameter as the current working directory.

The code also defines a constant function `default_poll_interval` that returns the default poll interval of 2 seconds.

This code is likely used in a larger project that involves indexing data on the CKB blockchain. The `IndexerConfig` struct provides a way to configure the indexer's behavior, and the `adjust` method ensures that the configuration options are valid and canonicalized. Other parts of the project likely use the `IndexerConfig` struct to create an indexer with the desired configuration options. For example:

```rust
let mut config = IndexerConfig::default();
config.store = PathBuf::from("/path/to/index/store");
config.index_tx_pool = true;
config.adjust(Path::new("/root/dir"), "indexer");
let indexer = Indexer::new(config);
```
## Questions: 
 1. What is the purpose of the `IndexerConfig` struct?
- The `IndexerConfig` struct is used to store configuration options for the indexer.

2. What is the purpose of the `adjust` method?
- The `adjust` method is used to canonicalize paths in the config options, and set default values for the `store` and `secondary_path` fields if they are not set.

3. What is the purpose of the `default_poll_interval` function?
- The `default_poll_interval` function returns the default value for the `poll_interval` field if it is not set in the configuration options.