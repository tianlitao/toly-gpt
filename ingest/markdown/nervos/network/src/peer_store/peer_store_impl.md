[View code on GitHub](https://github.com/nervosnetwork/ckb/network/src/peer_store/peer_store_impl.rs)

# PeerStore

The `PeerStore` is a module that manages the state of peers in the CKB network. It keeps track of connected peers, discovered peers, and banned peers. It also provides methods to add, remove, and update peer information.

## Usage

The `PeerStore` is used throughout the CKB network to manage peer information. It is used to add and remove peers from the network, to keep track of peer status, and to manage banned peers.

## Methods

### `new`

```rust
pub fn new(addr_manager: AddrManager, ban_list: BanList) -> Self
```

Creates a new `PeerStore` instance with an `AddrManager` and a `BanList`.

### `add_connected_peer`

```rust
pub fn add_connected_peer(&mut self, addr: Multiaddr, session_type: SessionType)
```

Adds a connected peer to the `PeerStore`. This method assumes that the peer is connected, which implies that the address is "verified".

### `add_addr`

```rust
pub fn add_addr(&mut self, addr: Multiaddr, flags: Flags) -> Result<()>
```

Adds a discovered peer address to the `PeerStore`. This method assumes that the peer and address are untrusted since we have not connected to it.

### `add_outbound_addr`

```rust
pub fn add_outbound_addr(&mut self, addr: Multiaddr, flags: Flags)
```

Adds an outbound peer address to the `PeerStore`.

### `update_outbound_addr_last_connected_ms`

```rust
pub fn update_outbound_addr_last_connected_ms(&mut self, addr: Multiaddr)
```

Updates the last connected timestamp for an outbound peer address.

### `report`

```rust
pub fn report(&mut self, addr: &Multiaddr, behaviour: Behaviour) -> ReportResult
```

Reports peer behaviours to the `PeerStore`.

### `remove_disconnected_peer`

```rust
pub fn remove_disconnected_peer(&mut self, addr: &Multiaddr) -> Option<PeerInfo>
```

Removes a disconnected peer from the `PeerStore`.

### `peer_status`

```rust
pub fn peer_status(&self, peer_id: &PeerId) -> Status
```

Gets the status of a peer in the `PeerStore`.

### `fetch_addrs_to_attempt`

```rust
pub fn fetch_addrs_to_attempt(&mut self, count: usize, required_flags: Flags) -> Vec<AddrInfo>
```

Fetches a list of peers for outbound connection. This method randomly returns recently connected peer addresses.

### `fetch_addrs_to_feeler`

```rust
pub fn fetch_addrs_to_feeler(&mut self, count: usize) -> Vec<AddrInfo>
```

Fetches a list of peers for feeler connection. This method randomly returns peer addresses that we have never connected to.

### `fetch_random_addrs`

```rust
pub fn fetch_random_addrs(&mut self, count: usize, required_flags: Flags) -> Vec<AddrInfo>
```

Fetches a list of valid addresses that have successfully connected. This method is used for discovery.

### `ban_addr`

```rust
pub(crate) fn ban_addr(&mut self, addr: &Multiaddr, timeout_ms: u64, ban_reason: String)
```

Bans an address from the `PeerStore`.

### `is_addr_banned`

```rust
pub fn is_addr_banned(&self, addr: &Multiaddr) -> bool
```

Checks if an address is banned from the `PeerStore`.

### `ban_list`

```rust
pub fn ban_list(&self) -> &BanList
```

Gets the `BanList` from the `PeerStore`.

### `mut_ban_list`

```rust
pub fn mut_ban_list(&mut self) -> &mut BanList
```

Gets a mutable reference to the `BanList` from the `PeerStore`.

### `clear_ban_list`

```rust
pub fn clear_ban_list(&mut self)
```

Clears the `BanList` from the `PeerStore`.

### `check_purge`

```rust
fn check_purge(&mut self) -> Result<()>
```

Checks and tries to delete addresses if the `PeerStore` has reached its limit. This method returns an error if the `PeerStore` is full and cannot be purged.

## Structs

### `PeerStore`

```rust
pub struct PeerStore {
    addr_manager: AddrManager,
    ban_list: BanList,
    connected_peers: HashMap<PeerId, PeerInfo>,
    score_config: PeerScoreConfig,
}
```

The `PeerStore` struct is the main struct for the `PeerStore` module. It contains an `AddrManager`, a `BanList`, a `HashMap` of connected peers, and a `PeerScoreConfig`.
## Questions: 
 1. What is the purpose of the `PeerStore` struct and what data does it store?
- The `PeerStore` struct is used to store information about peers, including their addresses, connection status, and behavior scores. It also contains an `AddrManager` and `BanList` for managing peer addresses and bans.

2. How does the `PeerStore` handle adding and removing peers and their addresses?
- The `PeerStore` has methods for adding connected peers, discovered peer addresses, and outbound peer addresses. It also has methods for removing disconnected peers and banned addresses. When adding addresses, the `PeerStore` checks if they are already banned and purges the address list if it reaches a certain limit.

3. What is the purpose of the `fetch_addrs_to_attempt` method and how does it work?
- The `fetch_addrs_to_attempt` method is used to randomly select a specified number of peer addresses for outbound connection attempts. It filters out addresses that are already connected or have been connected within the last 3 days, and also filters by required flags.