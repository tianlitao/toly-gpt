[View code on GitHub](https://github.com/nervosnetwork/ckb/util/metrics/src/lib.rs)

# ckb-metrics

The `ckb-metrics` crate is a lightweight metrics facade used in CKB. It provides a set of tools for metrics. The crate `ckb-metrics-service` is the runtime which handles the metrics data in CKB.

The `Metrics` struct contains various metrics that can be used to track different aspects of the CKB system. These metrics include:

- `ckb_chain_tip`: A gauge metric for CKB chain tip header number.
- `ckb_freezer_size`: A gauge for tracking the size of all frozen data.
- `ckb_freezer_read`: A counter for measuring the effective amount of data read.
- `ckb_relay_transaction_short_id_collide`: A counter for relay transaction short id collide.
- `ckb_relay_cb_transaction_count`: A counter for relay compact block transaction count.
- `ckb_relay_cb_reconstruct_ok`: A counter for relay compact block reconstruct ok.
- `ckb_relay_cb_fresh_tx_cnt`: A counter for relay compact block fresh transaction count.
- `ckb_relay_cb_reconstruct_fail`: A counter for relay compact block reconstruct fail.
- `ckb_shared_best_number`: A gauge for CKB shared best number.
- `ckb_sys_mem_process`: A gauge vector for CKB system memory process statistics.
- `ckb_sys_mem_jemalloc`: A gauge vector for CKB system memory jemalloc statistics.
- `ckb_message_bytes`: A histogram for CKB network connections.
- `ckb_sys_mem_rocksdb`: A gauge vector for CKB rocksdb statistics.
- `ckb_network_ban_peer`: A counter for CKB network ban peers.

The `gather()` function is used to collect all the metrics data. It returns a vector of `prometheus::proto::MetricFamily`.

The `handle()` function is used to check whether the metrics service is enabled. If it is enabled, it returns `Some(&'static METRICS)`, otherwise it returns `None`.

The `tests` module contains tests to ensure that all metrics have valid names and labels.
## Questions: 
 1. What is the purpose of the `ckb-metrics` crate and how does it relate to the `ckb-metrics-service` runtime?
   
   Answer: The `ckb-metrics` crate is a set of tools for metrics, while the `ckb-metrics-service` runtime handles the metrics data in CKB. The crate is a lightweight metrics facade used in CKB.

2. What metrics are being tracked in this code and how are they being collected?
   
   Answer: The code is tracking various metrics such as CKB chain tip header number, size of all frozen data, effective amount of data read, and more. These metrics are being collected using various Prometheus macros such as `register_int_gauge`, `register_int_counter`, `register_histogram_vec`, and `register_int_gauge_vec`.

3. How does the `handle()` function determine whether the metrics service is enabled or not?
   
   Answer: The `handle()` function determines whether the metrics service is enabled or not by checking the value of the `METRICS_SERVICE_ENABLED` static variable. If the value is set, it returns `Some(&METRICS)`, otherwise it returns `None`. The `ENABLE_COLLECT_METRICS` thread-local variable is used to cache the value of `METRICS_SERVICE_ENABLED` to avoid repeated lookups.