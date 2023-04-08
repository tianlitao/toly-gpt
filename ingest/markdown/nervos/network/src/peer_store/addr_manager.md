[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/network/src/peer_store/addr_manager.rs)

The `AddrManager` struct is responsible for managing a list of addresses that can be used to connect to peers in the network. It keeps track of each address's unique ID, the `AddrInfo` struct that contains information about the address, and a list of random IDs that are used to randomly select addresses to connect to.

The `add` method adds a new address to the manager. It first checks if the address can be converted to a `SocketAddr`, and if so, it checks if the address already exists in the manager. If it does, it compares the last connection time of the existing address with the new address and returns if the new address is older. If the address is new, it generates a new ID, adds the address to the `addr_to_id` map, adds the `AddrInfo` to the `id_to_info` map, and adds the ID to the `random_ids` list.

The `fetch_random` method returns a list of random addresses that are worth trying to connect to. It first creates a set of duplicate IPs to ensure that only one address per IP is returned. It then loops through the `random_ids` list, shuffling it as it goes, and checks if each address is connectable and passes a given filter function. If it does, it adds the address to the `addr_infos` list until it reaches the desired count.

The `count` method returns the number of addresses in the manager.

The `addrs_iter` method returns an iterator over the `AddrInfo` structs in the manager.

The `remove` method removes an address from the manager by its IP and port. It first converts the address to a `SocketAddr`, removes the ID from the `addr_to_id` map, removes the `AddrInfo` from the `id_to_info` map, and removes the ID from the `random_ids` list.

The `get` method returns the `AddrInfo` for a given address by its IP and port.

The `get_mut` method returns a mutable reference to the `AddrInfo` for a given address by its IP and port.

The `swap_random_id` method swaps two random IDs in the `random_ids` list and updates the `random_id_pos` field in the corresponding `AddrInfo` structs to keep them consistent.

Overall, the `AddrManager` struct provides a way to manage a list of addresses that can be used to connect to peers in the network. It allows for adding, removing, and retrieving addresses, as well as selecting random addresses to connect to. It is an important component of the larger project as it helps to maintain a healthy network of peers.
## Questions:
 1. What is the purpose of the `AddrManager` struct and what data does it store?
- The `AddrManager` struct is used to manage address information and store it in various data structures such as `HashMap` and `Vec`. It stores information such as the next ID, a mapping of socket addresses to IDs, a mapping of IDs to address information, and a vector of random IDs.

2. What is the purpose of the `fetch_random` method and what does it return?
- The `fetch_random` method returns a vector of `AddrInfo` structs that are randomly selected from the `AddrManager`. These addresses are chosen based on whether they are worth trying or connecting to, as determined by a provided filter function.

3. What is the purpose of the `remove` method and how does it work?
- The `remove` method removes an address from the `AddrManager` by its IP address and port number. It first converts the provided `Multiaddr` to a `SocketAddr`, then uses this to look up the corresponding ID in the `addr_to_id` mapping. If an ID is found, the corresponding `AddrInfo` is removed from the `id_to_info` mapping and the ID is removed from the `random_ids` vector by swapping it with the last index and popping it off.
