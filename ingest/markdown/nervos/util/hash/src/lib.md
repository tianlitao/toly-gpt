[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/util/hash/src/lib.rs)

The code defines the default hash function used in the ckb project, which is based on the blake2b algorithm. The hash function is configured to produce a 32-byte digest and uses a personalization string of "ckb-default-hash". The code provides functions for creating a new hasher, hashing a slice of binary data, and returning the resulting digest.

The `new_blake2b` function creates a new instance of the blake2b hasher with the default configuration. This hasher can be used to hash inputs incrementally by calling the `update` method with successive chunks of data, and then calling the `finalize` method to obtain the resulting digest.

The `blake2b_256` function provides a convenient way to hash a slice of binary data and obtain the resulting digest. If the input slice is empty, the function returns a precomputed blank hash value. Otherwise, it calls the `inner_blake2b_256` function to perform the actual hashing.

The `inner_blake2b_256` function creates a new blake2b hasher, updates it with the input slice, and finalizes it to obtain the resulting digest. This function is used by the `blake2b_256` function to perform the actual hashing.

The code also defines several constants, including the blank hash value, the output digest size, and the personalization string used by the blake2b hasher.

Overall, this code provides a simple and efficient way to hash binary data using the blake2b algorithm with the default configuration used in the ckb project. It can be used by other parts of the project that require hashing functionality, such as the transaction validation and block verification modules.
## Questions:
 1. What hash function does CKB use by default and what are its configurations?

   CKB uses blake2b hash function with a digest size of 32 and personalization of "ckb-default-hash".

2. What is the purpose of the BLANK_HASH constant and how is it used?

   BLANK_HASH is the hash output on empty input and is used as a default value when hashing empty inputs.

3. How can a developer use the new_blake2b function to hash inputs incrementally?

   A developer can use the new_blake2b function to create a new hasher and then update it with input slices incrementally. The hash result can be saved by calling the finalize method on the hasher.
