[View code on GitHub](https://github.com/nervosnetwork/ckb/network/src/peer_store/types.rs)

This code defines several structs and functions related to peer management in the ckb project. 

The `PeerInfo` struct represents information about a peer, including its connected address, session type, and the time it was last connected. The `AddrInfo` struct represents information about an address that a peer can be reached at, including the address itself, a score indicating the quality of the address, and various timestamps and counters related to connection attempts. The `BannedAddr` struct represents information about an IP address that has been banned, including the address itself, the time until which the ban is in effect, and the reason for the ban.

The `multiaddr_to_ip_network` function takes a `Multiaddr` and attempts to convert it to an `IpNetwork`, which represents an IP address and its associated subnet mask. This is used to extract the IP address from a `Multiaddr` so that it can be checked against a list of banned addresses.

The `ip_to_network` function takes an `IpAddr` and converts it to an `IpNetwork`. This is used to convert an `IpAddr` to the appropriate type of `IpNetwork` so that it can be stored in a `BannedAddr` struct.

The `AddrInfo` struct has several methods for managing connection attempts. The `connected` method takes a closure that returns a boolean and checks whether the address has been connected to within the time frame specified by the closure. The `tried_in_last_minute` method checks whether the address has been tried within the last minute. The `is_connectable` method checks whether the address is currently connectable based on various criteria, including whether it has been tried too many times or failed too many times. The `mark_tried` method updates the `AddrInfo` struct to reflect that a connection attempt has been made. The `mark_connected` method updates the `AddrInfo` struct to reflect that a successful connection has been made. The `flags` method updates the flags associated with the address.

Overall, this code provides a framework for managing peer connections and addresses in the ckb project. It allows for tracking of connection attempts and quality of addresses, as well as banning of problematic IP addresses.
## Questions: 
 1. What is the purpose of the `PeerInfo` and `AddrInfo` structs?
- `PeerInfo` represents information about a peer, including its connected address, session type, and last connected time.
- `AddrInfo` represents information about an address, including its multiaddr, score, last connected time, last try time, attempts count, random ID position, and flags.

2. What is the purpose of the `BannedAddr` struct?
- `BannedAddr` represents information about a banned IP address, including the IP address itself, the ban until time, the ban reason, and the creation time.

3. What are the `multiaddr_to_ip_network` and `ip_to_network` functions used for?
- `multiaddr_to_ip_network` converts a `Multiaddr` to an `IpNetwork` by extracting the IP address component of the `Multiaddr`.
- `ip_to_network` converts an `IpAddr` to an `IpNetwork` by creating an `IpNetwork` with the same IP address and default prefix length.