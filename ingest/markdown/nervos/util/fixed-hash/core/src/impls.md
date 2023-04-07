[View code on GitHub](https://github.com/nervosnetwork/ckb/util/fixed-hash/core/src/impls.rs)

This code defines a set of macros and implements methods for four different types: H160, H256, H512, and H520. These types represent fixed-size byte arrays of 20, 32, 64, and 65 bytes respectively. 

The `impl_methods!` macro is used to generate the same set of methods for each of these types. The macro takes two arguments: the name of the type and the number of bytes in the array. The macro then generates two methods for each type: `as_bytes` and `from_slice`.

The `as_bytes` method returns a reference to the byte slice that represents the array. This method can be useful when working with other libraries or functions that require a byte slice as input.

The `from_slice` method takes a byte slice as input and returns a new instance of the corresponding type. If the length of the input slice does not match the expected length of the array, the method returns an error. Otherwise, it creates a new instance of the type and copies the bytes from the input slice into the array.

These methods can be used throughout the larger project to convert between byte slices and the fixed-size byte arrays represented by these types. For example, if the project needs to serialize or deserialize data that includes one of these types, it can use the `as_bytes` method to get a byte slice representation of the array, and then use a serialization library to encode or decode the data. Similarly, if the project receives a byte slice that includes one of these types, it can use the `from_slice` method to create a new instance of the corresponding type. 

Overall, this code provides a convenient way to work with fixed-size byte arrays in Rust, and can be used throughout the larger project to handle serialization, deserialization, and other operations that involve these types.
## Questions: 
 1. What is the purpose of the `impl_methods` macro and how is it used in this code?
   - The `impl_methods` macro is used to generate implementation code for the `as_bytes` and `from_slice` methods for the `H160`, `H256`, `H512`, and `H520` structs. It takes in the name of the struct and the size of the byte array and generates the implementation code for the two methods.
   
2. What do the `as_bytes` and `from_slice` methods do?
   - The `as_bytes` method returns a reference to the byte slice of the struct. The `from_slice` method takes in a byte slice and returns a new instance of the struct if the byte slice is of the correct length, otherwise it returns a `FromSliceError`.

3. What are the `H160`, `H256`, `H512`, and `H520` structs used for?
   - These structs are used to represent different sizes of hash values (160, 256, 512, and 520 bits respectively) and provide methods for converting to and from byte slices. They are likely used in cryptographic operations within the `ckb` project.