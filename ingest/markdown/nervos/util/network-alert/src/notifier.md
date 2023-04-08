[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/util/network-alert/src/notifier.rs)

The `Notifier` module is responsible for receiving and processing alerts from the network and notifying other modules in the system. The module maintains a list of received alerts, cancelled alerts, and alerts that should be noticed by the self node.

The `Notifier` struct contains several fields, including a `cancel_filter` which is an LRU cache of cancelled alerts, a `received_alerts` hashmap of received alerts, a `noticed_alerts` vector of alerts that should be noticed by the self node, a `client_version` which is an optional `semver::Version` representing the version of the client, and a `notify_controller` which is a `ckb_notify::NotifyController` used to notify other modules in the system.

The `Notifier` struct has several methods, including `new` which initializes a new `Notifier` instance, `add` which adds a new alert to the `received_alerts` hashmap and notifies other modules if necessary, `cancel` which cancels an alert and removes it from the `received_alerts` hashmap and `noticed_alerts` vector, `clear_expired_alerts` which removes all expired alerts from the `received_alerts` hashmap and `noticed_alerts` vector, `has_received` which checks if an alert has already been received or cancelled, `received_alerts` which returns a vector of all unexpired alerts, and `noticed_alerts` which returns a vector of alerts that should be noticed by the self node.

The `add` method is the most complex method in the `Notifier` module. It first checks if the alert has already been received, and if so, returns early. It then checks if the alert has a cancel_id, and if so, cancels the alert with that id. It then adds the alert to the `received_alerts` hashmap. It checks if the alert is version-effective by comparing the alert's min_version and max_version fields with the client_version field. If the alert is not version-effective, it returns early. If the alert has already been noticed, it returns early. Otherwise, it notifies other modules using the `notify_controller` and adds the alert to the `noticed_alerts` vector, sorting the vector by priority.

Overall, the `Notifier` module is an important component of the `ckb` project, responsible for receiving and processing alerts from the network and notifying other modules in the system. It provides a simple API for adding and cancelling alerts, and for retrieving unexpired and noticed alerts.
## Questions:
 1. What is the purpose of the `Notifier` struct and how is it used?
- The `Notifier` struct is used to notify other modules of alerts. It contains methods to add, cancel, and clear alerts, as well as retrieve received and noticed alerts.

2. What is the significance of the `client_version` field and how is it used?
- The `client_version` field is an optional `semver::Version` that represents the version of the client using the `Notifier`. It is used to determine if an alert is effective for the client based on its minimum and maximum versions.

3. What is the purpose of the `CANCEL_FILTER_SIZE` constant and how is it used?
- The `CANCEL_FILTER_SIZE` constant is the maximum number of cancelled alerts that can be stored in the `cancel_filter` LRU cache. It is used to limit the memory usage of the `Notifier`.
