[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/rpc/src/module/subscription.rs)

The code defines an RPC module for subscriptions in the CKB (Nervos Common Knowledge Base) node. The module allows clients to subscribe to various topics related to the node's operation, such as new block headers, new transactions, and rejected transactions. The module uses the `jsonrpc_core` and `jsonrpc_pubsub` crates to implement the JSON-RPC protocol for subscriptions.

The `SubscriptionRpc` trait defines two methods: `subscribe` and `unsubscribe`. The `subscribe` method takes a `Topic` parameter and returns a subscription ID. The `unsubscribe` method takes a subscription ID and removes the corresponding subscription. The `SubscriptionRpcImpl` struct implements the `SubscriptionRpc` trait and provides the actual implementation of the subscription logic.

The `SubscriptionSession` struct represents a client's subscription session and contains a set of subscription IDs and a session object. The `PubSubMetadata` and `Metadata` traits are implemented for the `SubscriptionSession` struct to provide metadata for the JSON-RPC protocol.

The `SubscriptionRpcImpl` struct contains a map of subscribers for each topic. The `subscribe` method adds a new subscriber to the corresponding topic's map and returns a subscription ID. The `unsubscribe` method removes the subscriber with the given subscription ID from all topic maps.

The `new` function initializes the `SubscriptionRpcImpl` struct and subscribes to various topics using the `NotifyController` object. The function spawns a new task that listens for notifications on the subscribed topics and sends them to the corresponding subscribers.

Overall, the code provides a convenient way for clients to subscribe to various events in the CKB node's operation and receive notifications in real-time. The code can be used as part of a larger project that interacts with the CKB node.
## Questions:
 1. What is the purpose of the `SubscriptionRpc` trait and how is it used?

   The `SubscriptionRpc` trait defines methods for subscribing and unsubscribing to topics related to new blocks, transactions, and other events in the CKB blockchain. It is used to implement a full duplex connection between the CKB node and subscribers, which can be established via TCP or WebSocket.

2. What is the purpose of the `SubscriptionRpcImpl` struct and how is it initialized?

   The `SubscriptionRpcImpl` struct implements the `SubscriptionRpc` trait and provides methods for handling subscriptions and notifications. It is initialized with a `NotifyController` and a `Handle` using the `new` method, which subscribes to new block and transaction events and spawns a background task to notify subscribers when these events occur.

3. How are notifications sent to subscribers and what types of events can be subscribed to?

   Notifications are sent to subscribers using a `Sink<String>` and a JSON string representing the event data. Subscribers can subscribe to topics related to new block headers, new blocks, new transactions, proposed transactions, and rejected transactions. When an event occurs, the relevant subscribers are notified with a JSON string containing the event data.
