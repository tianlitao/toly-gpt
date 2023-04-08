[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/util/proposal-table/src/lib.rs)

The `ProposalTable` module is a Rust implementation of a data structure that records proposals for two-step transaction confirmation. The module contains two structs: `ProposalView` and `ProposalTable`.

`ProposalView` is a view of the point-time proposal set, which represents the on-chain proposed transaction pool stored in memory. It is created by the `ProposalTable` `finalize` method. The `w_close` and `w_far` fields define the closest and farthest on-chain distance between a transaction's proposal and commitment. The `ProposalView` struct has four methods:

- `new`: creates a new `ProposalView` instance.
- `gap`: returns proposals between `w_close` and `tip`.
- `set`: returns proposals between `w_close` and `w_far`.
- `contains_proposed`: returns true if the proposals set between `w_close` and `w_far` contains the given ID.
- `contains_gap`: returns true if the proposals set between `w_close` and `tip` contains the given ID.

`ProposalTable` is a table that records proposals set in number-ids pairs. It has two fields: `table`, which is a `BTreeMap` that contains all proposal sets, and `proposal_window`, which is a `ProposalWindow` instance. The `ProposalTable` struct has four methods:

- `new`: creates a new `ProposalTable` instance from a `ProposalWindow`.
- `insert`: inserts a number-ids pair into the table. If the table did not have this number present, true is returned. If the map did have this number present, the proposal set is updated.
- `remove`: removes a proposal set from the table, returning the set at the number if the number was previously in the table.
- `all`: returns a reference to the internal `BTreeMap` that contains all proposal sets.
- `finalize`: updates the table by proposal window move forward, dropping outdated proposal sets. It returns the removed proposal IDs set and a new `ProposalView`.

The `finalize` method updates the `ProposalTable` by moving the proposal window forward and dropping outdated proposal sets. It returns the removed proposal IDs set and a new `ProposalView`. The `new_ids` and `gap` variables are calculated based on the `candidate_number`, `proposal_start`, and `proposal_end`. If `candidate_number` is less than or equal to `w_close`, `new_ids` is an empty set, and `gap` is the set of proposals between 1 and `candidate_number`. Otherwise, `new_ids` is the set of proposals between `candidate_number - w_far` and `candidate_number - w_close`, and `gap` is the set of proposals between `candidate_number - w_close + 1` and `candidate_number`.

Overall, the `ProposalTable` module provides a way to record proposals for two-step transaction confirmation and manage them efficiently. It can be used in the larger project to ensure that transactions are confirmed in a timely and secure manner.
## Questions:
 1. What is the purpose of the `ProposalTable` struct and how is it used?

   The `ProposalTable` struct is used to record proposals set in number-ids pairs. It has methods to insert and remove proposals, and to update the table by proposal window move forward, dropping outdated proposal sets. It is used to create a view of the point-time proposal set, representing on-chain proposed transaction pool, stored in memory so that there is no need to fetch on hard disk.

2. What is the purpose of the `ProposalView` struct and how is it used?

   The `ProposalView` struct captures point-time proposal set, representing on-chain proposed transaction pool, stored in memory so that there is no need to fetch on hard disk. It has methods to return proposals between w_close and tip, proposals between w_close and w_far, and to check if a proposal is contained in the proposals set between w_close and w_far or between w_close and tip.

3. What is the purpose of the `ProposalWindow` struct and how is it used?

   The `ProposalWindow` struct defines the closest and farthest on-chain distance between a transaction’s proposal and commitment. It is used to create a new `ProposalTable` and to update the table by proposal window move forward, dropping outdated proposal sets.
