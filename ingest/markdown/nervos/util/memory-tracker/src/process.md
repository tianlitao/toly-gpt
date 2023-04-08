[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/util/memory-tracker/src/process.rs)

The code is a Rust module that tracks the memory usage of the CKB (Nervos Network) process, Jemalloc, and RocksDB through ckb-metrics. The module exports a single function `track_current_process` that takes two arguments: an interval and an optional tracker. The interval is the number of seconds between each memory usage check, and the tracker is an optional object that implements the `TrackRocksDBMemory` trait.

The function starts by checking if the interval is zero, in which case it logs a message that memory tracking is disabled. Otherwise, it logs a message that memory tracking is enabled and initializes some variables to track Jemalloc memory usage. It then spawns a new thread that loops indefinitely, sleeping for the specified interval between each iteration.

In each iteration, the thread first advances the Jemalloc epoch and fetches the current process memory information. It then updates the ckb-metrics with the current process memory usage and Jemalloc memory usage. If a tracker object is provided, it also calls the `gather_memory_stats` method on the tracker object to gather RocksDB memory usage statistics.

The module also defines a `Memory` struct that represents the memory usage of a process. It implements the `FromStr` trait to parse the memory information from a string. The `get_current_process_memory` function reads the memory information from the `/proc/{pid}/statm` file and returns a `Memory` object.

Overall, this module provides a way to track the memory usage of the CKB process, Jemalloc, and RocksDB and expose the information through ckb-metrics. It can be used to monitor the memory usage of the CKB node and detect memory leaks or other memory-related issues.

Example usage:

```rust
use ckb_memory_tracker::{track_current_process, Memory};

fn main() {
    let interval = 10;
    let tracker = Some(MyTracker::new());
    track_current_process(interval, tracker);
}

struct MyTracker {}

impl MyTracker {
    fn new() -> Self {
        MyTracker {}
    }

    fn gather_memory_stats(&self) {
        // gather RocksDB memory stats
    }
}
```
## Questions:
 1. What is the purpose of the `track_current_process` function?

   The `track_current_process` function is used to track the memory usage of the CKB process, Jemalloc, and RocksDB through `ckb-metrics`.

2. What is the purpose of the `Memory` struct and the `FromStr` trait implementation for it?

   The `Memory` struct represents the memory usage of a process, and the `FromStr` trait implementation is used to parse the memory information from a string.

3. What is the purpose of the `je_mib!` and `mib_read!` macros?

   The `je_mib!` macro is used to lookup the jemalloc MIB for a given key, and the `mib_read!` macro is used to read the jemalloc stats for a given MIB.
