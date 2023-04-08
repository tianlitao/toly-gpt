[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/util/systemtime/src/lib.rs)

The `ckb_systemtime` module provides a way to get the current system timestamp, either the real system timestamp or a fake timestamp when the `enable_faketime` feature is enabled. The module contains several functions and a struct.

The `system_time_as_millis` function returns the real system's timestamp in milliseconds. It uses the `std::time::SystemTime` module to get the current system time and calculates the duration since the UNIX epoch. It then returns the duration in milliseconds.

The `unix_time_as_millis` function returns the system's timestamp in milliseconds. If the `enable_faketime` feature is not enabled, it returns the real system's timestamp. If the `enable_faketime` feature is enabled, it returns the fake timestamp if it is enabled, otherwise, it returns the real system's timestamp.

The `unix_time` function returns the system's timestamp as a `std::time::Duration` object. It uses the `unix_time_as_millis` function to get the timestamp in milliseconds and converts it to a duration.

The `FaketimeGuard` struct is used to set or disable the fake timestamp. It has two methods: `set_faketime` and `disable_faketime`. The `set_faketime` method sets the fake timestamp to the given value and enables the fake timestamp. The `disable_faketime` method disables the fake timestamp. The `FaketimeGuard` struct implements the `Drop` trait, which disables the fake timestamp when the `FaketimeGuard` object is dropped.

The module also contains several static variables: `FAKETIME`, `FAKETIME_ENABLED`. The `FAKETIME` variable stores the fake timestamp value. The `FAKETIME_ENABLED` variable indicates whether the fake timestamp is enabled or not.

This module can be used in the larger project to get the current system timestamp. If the `enable_faketime` feature is enabled, it can be used to set a fake timestamp for testing purposes. For example:

```
#[cfg(feature = "enable_faketime")]
fn test_faketime() {
    let faketime_guard = ckb_systemtime::faketime();
    faketime_guard.set_faketime(1000);
    assert_eq!(ckb_systemtime::unix_time_as_millis(), 1000);
}
```
## Questions:
 1. What is the purpose of the `enable_faketime` feature and how does it work?
   - The `enable_faketime` feature provides fake timestamps when enabled. It works by storing a fake timestamp in the `FAKETIME` variable and checking if `FAKETIME_ENABLED` is set to true before returning the fake timestamp.
2. What is the difference between `unix_time_as_millis` and `system_time_as_millis` functions?
   - `unix_time_as_millis` returns the system timestamp in milliseconds, either real or fake depending on whether the `enable_faketime` feature is enabled. `system_time_as_millis` always returns the real system timestamp in milliseconds.
3. What is the purpose of the `FaketimeGuard` struct and how is it used?
   - The `FaketimeGuard` struct is used to set and disable the fake timestamp provided by the `enable_faketime` feature. It is used by calling the `faketime` function to get a `FaketimeGuard` instance, then calling its `set_faketime` method to set the fake timestamp or `disable_faketime` method to disable it. The `FaketimeGuard` instance automatically disables the fake timestamp when it is dropped.
