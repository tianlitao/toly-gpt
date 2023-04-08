[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/network/src/peer_registry.rs)

The `PeerRegistry` module is responsible for managing the network connections of the CKB node. It keeps track of all the connected peers and their session information. The module also enforces connection limits and whitelisting rules.

The `PeerRegistry` struct contains a hashmap of `Peer` structs, which represent the connected peers. It also contains the maximum number of inbound and outbound connections allowed, a flag indicating whether only whitelisted peers are allowed, and sets of whitelisted and feeler peers.

The `new` function initializes a new `PeerRegistry` instance with the given configuration parameters. It creates an empty hashmap of peers, extracts the peer IDs from the given whitelist addresses, and initializes the feeler and whitelist peer sets.

The `accept_peer` function is called when a new peer connects to the node. It takes the remote address, session ID, session type, and a `PeerStore` instance as input. It first checks if the session ID already exists in the hashmap, and if so, returns an error. It then extracts the peer ID from the remote address and checks if it already exists in the hashmap. If it does, it returns an error.

If the peer is not whitelisted, it checks if the whitelist-only flag is set and returns an error if it is. It also checks if the remote address is banned and returns an error if it is. It then checks if the maximum number of inbound or outbound connections has been reached and evicts a peer if necessary. If the peer is outbound and the maximum outbound limit has been reached, it returns an error.

If all checks pass, it adds the peer to the `PeerStore`, creates a new `Peer` instance, inserts it into the hashmap, and returns an optional evicted peer.

The `try_evict_inbound_peer` function is called when a new inbound connection is accepted and the maximum number of inbound connections has been reached. It selects a candidate list of peers to evict based on various criteria such as ping time, last message received time, and connection time. It then groups the peers by network group and randomly selects one to evict.

The `add_feeler`, `remove_feeler`, and `is_feeler` functions are used to manage the feeler peer set.

The `get_peer`, `get_peer_mut`, and `remove_peer` functions are used to retrieve and modify peer information.

The `get_key_by_peer_id` function is used to retrieve the session ID of a peer given its ID.

The `peers` and `connected_peers` functions are used to retrieve information about all connected peers.

The `connection_status` function returns a `ConnectionStatus` struct containing information about the total number of sessions, the number of non-whitelisted inbound and outbound sessions, and the maximum inbound and outbound limits.
## Questions:
 1. What is the purpose of the `PeerRegistry` struct and how is it used in the project?
- The `PeerRegistry` struct is used to keep track of opened session information and connection status for the ckb project's peer-to-peer network. It is used to accept new peers, remove disconnected peers, and get information about connected peers.

2. What is the significance of the `whitelist_only` field in the `PeerRegistry` struct?
- The `whitelist_only` field determines whether only whitelisted peers are allowed to connect to the network or if all peers are allowed. If set to true, only whitelisted peers are allowed to connect.

3. What is the purpose of the `try_evict_inbound_peer` function in the `PeerRegistry` struct?
- The `try_evict_inbound_peer` function is used to evict an inbound peer from the network if the maximum number of inbound connections has been reached. It selects a candidate list of peers to evict based on various criteria such as ping time and connection time, and then randomly selects one to evict.
