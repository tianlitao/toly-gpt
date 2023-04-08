[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/network/src/behaviour.rs)

The code defines an enum called `Behaviour` that represents the different behaviors of peers in a network. Each behavior is associated with a score that is used to evaluate the behavior of the peer. The `Behaviour` enum has two variants, `TestGood` and `TestBad`, which are only used for testing purposes.

The `Behaviour` enum has an implementation block that defines a method called `score`. This method returns the score associated with the behavior. If the code is being run in a test environment, the method returns a score of 10 for `TestGood` and -10 for `TestBad`. If the code is not being run in a test environment, the method returns a score of 0.

This code is part of the larger `ckb` project, which is not described in this file. It is likely that this code is used to evaluate the behavior of peers in a network and adjust their scores accordingly. The scores may be used to determine which peers are more trustworthy or reliable, or to identify peers that are behaving maliciously.

Here is an example of how this code might be used:

```rust
use crate::Behaviour;

let peer_behavior = Behaviour::TestGood;
let peer_score = peer_behavior.score();
println!("Peer score: {}", peer_score); // Output: Peer score: 10
```

In this example, we create a `Behaviour` enum variant called `TestGood` and call the `score` method on it to get the associated score. The score is then printed to the console.
## Questions:
 1. What is the purpose of the `Behaviour` enum?
   - The `Behaviour` enum is used to represent different types of peer behaviours and maintain a score for each peer based on their behaviour.

2. Why is the feature related to reporting peer behaviour currently disabled?
   - The reason for disabling the feature related to reporting peer behaviour is not mentioned in the code. It is possible that it was not fully implemented or tested, or it may have been deemed unnecessary for the current version of the project.

3. How is the score calculated for each type of behaviour?
   - The score for each type of behaviour is calculated using the `score()` method of the `Behaviour` enum. For test behaviours, the score is either 10 or -10 depending on whether the behaviour is good or bad. For non-test behaviours, the score is always 0.
