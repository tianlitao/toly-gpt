[View code on GitHub](https://github.com/nervosnetwork/ckb/util/light-client-protocol-server/src/constant.rs)

This code defines several constants that are used throughout the ckb project. The first constant, `BAD_MESSAGE_BAN_TIME`, is a `Duration` value that represents the amount of time a node will be banned if it sends a bad message. In this case, the value is set to 5 minutes (5 * 60 seconds).

The next three constants, `GET_BLOCKS_PROOF_LIMIT`, `GET_LAST_STATE_PROOF_LIMIT`, and `GET_TRANSACTIONS_PROOF_LIMIT`, are all `usize` values that represent limits on the number of proofs that can be requested by a node. These limits are used to prevent nodes from requesting too much data at once, which could cause performance issues or even crashes.

For example, if a node wants to request proofs for the last 1000 blocks, it would use the `GET_BLOCKS_PROOF_LIMIT` constant to ensure that it doesn't request more than the allowed limit. Similarly, if a node wants to request proofs for the last 1000 transactions, it would use the `GET_TRANSACTIONS_PROOF_LIMIT` constant.

Overall, these constants help to ensure that the ckb network operates smoothly and efficiently by setting reasonable limits on certain types of requests.
## Questions: 
 1. **What is the purpose of the `Duration` module being imported?** 
    The `Duration` module is used to define a time duration in seconds, which is used in the `BAD_MESSAGE_BAN_TIME` constant.

2. **What do the `GET_BLOCKS_PROOF_LIMIT`, `GET_LAST_STATE_PROOF_LIMIT`, and `GET_TRANSACTIONS_PROOF_LIMIT` constants represent?** 
    These constants represent limits on the number of proofs that can be retrieved for different types of data.

3. **What is the significance of the values assigned to the `BAD_MESSAGE_BAN_TIME` constant?** 
    The value assigned to `BAD_MESSAGE_BAN_TIME` is 5 minutes in seconds, which represents the amount of time a node will be banned if it sends a bad message.