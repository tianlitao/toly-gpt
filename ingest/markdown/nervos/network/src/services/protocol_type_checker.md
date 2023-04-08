[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/network/src/services/protocol_type_checker.rs)

The code is a service that periodically checks the sub-protocols opened by peers in the `sync` protocol of the ckb project's P2P network. The purpose of this service is to ensure that no malicious connections are made by peers who choose not to open the `sync` protocol to avoid being evicted by the network. The service checks whether all connections are normally open sync protocols, and if not, it closes the connection.

The service checks two types of sub-protocols: fully-opened and feeler. The fully-opened sub-protocol type means that all sub-protocols (except feeler) are opened, while the feeler sub-protocol type means that only the feeler protocol is open. Other protocols will be closed after a timeout.

The `ProtocolTypeCheckerService` struct is defined to implement this service. It takes in the `NetworkState`, `ServiceControl`, and `fully_open_required_protocol_ids` as parameters. The `fully_open_required_protocol_ids` is a vector of `ProtocolId` that represents the fully-opened sub-protocols.

The `check_protocol_type` method is called to check the open protocol type of each peer. If a peer has incomplete open protocols, it is disconnected from the network. The `opened_protocol_type` method is used to determine the open protocol type of a peer. If a peer has the feeler sub-protocol open, it is considered a feeler type. If a peer has all the fully-opened sub-protocols open, it is considered a fully-opened type. If a peer has incomplete open protocols, it is considered an error.

The `ProtocolTypeCheckerService` struct implements the `Future` trait to enable it to be used as a future. The `poll` method is called to poll the future. It sets up an interval to periodically check the protocol type of each peer. If the interval is not set, it sets it up and starts polling. If the interval is set, it checks whether a tick is ready and calls the `check_protocol_type` method if it is.

Overall, this service is an important part of the ckb project's P2P network as it ensures that no malicious connections are made by peers who choose not to open the `sync` protocol.
## Questions:
 1. What is the purpose of this code?

    This code defines a service that periodically checks the sub-protocols opened by peers in a P2P network to ensure that no malicious connections are present.

2. What are the valid sub-protocol types?

    There are two valid sub-protocol types: fully-opened, which means all sub-protocols except feeler are opened, and feeler, which means only the feeler protocol is open.

3. How does the service handle peers with incomplete open protocols?

    If a peer has incomplete open protocols, meaning they do not meet the requirements for either fully-opened or feeler, the service will close the connection with that peer.
