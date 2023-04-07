[View code on GitHub](https://github.com/nervosnetwork/ckb/network/src/services/outbound_peer.rs)

The `OutboundPeerService` struct is responsible for ensuring that the outbound connections of the current node reach the expected upper limit as much as possible. It periodically detects and verifies data in the peer store, keeps the whitelist nodes connected as much as possible, and periodically detects that the observed addresses are all valid.

The struct has a `new` function that takes in an `Arc` of `NetworkState`, a `ServiceControl`, and a `Duration` for the interval between connection attempts. It returns a new instance of `OutboundPeerService`.

The `OutboundPeerService` struct has several private functions that are used to dial feelers, try to dial peers, try to dial whitelist nodes, and try to dial observed addresses. These functions are called periodically by the `Future` implementation of the struct.

The `Future` implementation of the struct is responsible for polling the private functions periodically. It uses a `tokio::time::interval` to schedule the polling of these functions. The `poll` function of the `Future` implementation polls the interval and calls the private functions when the interval ticks.

Overall, the `OutboundPeerService` struct is an important part of the CKB project's networking layer. It ensures that the node maintains a healthy number of outbound connections and that these connections are to valid and trusted peers.
## Questions: 
 1. What is the purpose of this code?
- This code defines a `OutboundPeerService` struct that periodically attempts to connect to peers in order to ensure that the outbound connections of the current node reach the expected upper limit as much as possible, detect and verify data in the peer store, keep whitelist nodes connected as much as possible, and periodically detect that the observed addresses are all valid.

2. What is the significance of the `FEELER_CONNECTION_COUNT` constant?
- The `FEELER_CONNECTION_COUNT` constant is used to determine the number of peers to attempt to connect to when dialing feeler nodes.

3. What is the purpose of the `try_identify_count` field?
- The `try_identify_count` field is used to keep track of the number of times `try_dial_peers` has been called without successfully connecting to any peers. If this count exceeds 3, the function will attempt to connect to bootnodes in addition to peers from the peer store.