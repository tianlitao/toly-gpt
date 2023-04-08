[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/util/logger/src/lib.rs)

The code is a logging facade for the ckb project, which is a wrapper of the log crate. The log crate provides a logging framework for Rust. The purpose of this code is to provide a more user-friendly logging interface for the ckb project.

The code defines several macros that can be used to log messages at different levels (trace, debug, info, warn, and error) with different targets. The default target is the module path of the location of the log request. The macros that support target and message are suffixed with "_target".

For example, the `trace!` macro logs a message at the trace level using the default target, while the `trace_target!` macro logs a message at the trace level using the specified target.

The code also defines a `log_enabled!` macro that determines if a message logged at the specified level and with the default target will be logged. Similarly, the `log_enabled_target!` macro determines if a message logged at the specified level and with the specified target will be logged.

The code is designed to be more user-friendly than the log crate by disallowing the use of `target:` in the basic logging macros. This is because the `target:` syntax is unfriendly to `cargo fmt`.

Overall, this code provides a more user-friendly logging interface for the ckb project, making it easier for developers to log messages at different levels with different targets.
## Questions:
 1. What is the purpose of this crate and how does it differ from the `log` crate?

   This crate is a wrapper of the `log` crate and provides a more friendly macro for logging. The major difference is that this crate disallows using `target:` in the basic logging macros and adds another group of macros to support both target and message.

2. How can a developer log a message at a specific level and target using this crate?

   A developer can use the macros `trace_target!`, `debug_target!`, `info_target!`, `warn_target!`, and `error_target!` to log a message at a specific level and target.

3. How can a developer determine if a message logged at a specific level and target will be logged?

   A developer can use the macro `log_enabled_target!` to determine if a message logged at a specific level and target will be logged. This can be used to avoid expensive computation of log message arguments if the message would be ignored anyway.
