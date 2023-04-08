[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/tx-pool/src/component/recent_reject.rs)

The `RecentReject` struct in this code represents a recent reject pool for transactions. It is used to store rejected transactions for a limited amount of time and then remove them. The purpose of this struct is to keep track of rejected transactions and prevent them from being re-submitted too quickly.

The struct has several methods for creating and manipulating the pool. The `new` method creates a new `RecentReject` instance with default shard number of 5. The `build` method allows for customization of the shard number. The `put` method adds a rejected transaction to the pool, while the `get` method retrieves a rejected transaction from the pool. The `shrink` method removes the oldest transactions from the pool when the pool size exceeds a certain limit. The `get_shard` method is a helper function that determines which shard a transaction should be stored in based on its hash.

The `RecentReject` struct uses a `DBWithTTL` instance to store the rejected transactions. The `DBWithTTL` is a wrapper around a RocksDB instance that allows for setting a time-to-live (TTL) value for each key-value pair. When the TTL expires, the key-value pair is automatically removed from the database.

Overall, the `RecentReject` struct is an important component of the larger project as it helps to prevent spam transactions from being re-submitted too quickly. By keeping track of rejected transactions and removing them after a certain amount of time, the struct helps to ensure that the network is not overwhelmed with spam transactions.

Example usage:

```rust
use ckb_types::packed::Byte32;
use ckb_pool::txs_pool::RecentReject;
use ckb_error::AnyError;

fn main() -> Result<(), AnyError> {
    let mut recent_reject = RecentReject::new("/path/to/db", 100, 60)?;
    let tx_hash = Byte32::zero();
    let reject_reason = "invalid transaction".to_string();
    recent_reject.put(&tx_hash, reject_reason)?;
    let retrieved_reject = recent_reject.get(&tx_hash)?;
    assert_eq!(retrieved_reject, Some("invalid transaction".to_string()));
    Ok(())
}
```
## Questions:
 1. What is the purpose of the `RecentReject` struct and its methods?
- The `RecentReject` struct is used to store and manage recent transaction rejects. Its methods allow for adding and retrieving rejects, as well as managing the storage of the rejects.

2. What is the significance of the `shard_num` field and how is it used?
- The `shard_num` field determines the number of shards used to store the rejects. It is used to calculate the shard number for a given transaction hash and to create and drop shards as needed to manage the storage of the rejects.

3. How does the `shrink` method work and when is it called?
- The `shrink` method is called when the total number of stored rejects exceeds the `count_limit` field. It randomly selects a shard to drop and creates a new one with the same name and TTL. It then updates the `total_keys_num` field to reflect the new total number of stored rejects.
