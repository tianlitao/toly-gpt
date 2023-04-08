[View code on GitHub](https://github.com/nervosnetwork/ckb/blob/develop/script/src/cost_model.rs)

# CKB VM Cost Model

This code is part of the CKB (Nervos Common Knowledge Base) project and is responsible for assigning cycles to instructions in the CKB VM (Virtual Machine) cost model. The CKB VM is a RISC-V based VM that executes scripts in the Nervos CKB blockchain.

The code defines two functions and a constant:

## BYTES_PER_CYCLE

This constant defines how many bytes can be transferred when the VM costs one cycle. It is set to 4.

## transferred_byte_cycles

This function calculates how many cycles are spent to load the specified number of bytes. It takes the number of bytes as an argument and returns the number of cycles. The calculation is done by dividing the number of bytes by BYTES_PER_CYCLE and rounding up to the nearest integer.

Example:

```rust
use ckb_vm::instructions::Instruction;
use ckb_vm::instructions::insts;
use ckb_vm::cost_model::{transferred_byte_cycles, BYTES_PER_CYCLE};

let instruction = Instruction::new(insts::OP_LD, 0, 0, 0, 0);
let cycles = transferred_byte_cycles(8);
assert_eq!(cycles, 2);
```

## instruction_cycles

This function returns the number of cycles spent to execute a specific instruction. It takes an instruction as an argument and returns the number of cycles. The function uses a match statement to determine the number of cycles based on the instruction's opcode.

Example:

```rust
use ckb_vm::instructions::Instruction;
use ckb_vm::instructions::insts;
use ckb_vm::cost_model::instruction_cycles;

let instruction = Instruction::new(insts::OP_LD, 0, 0, 0, 0);
let cycles = instruction_cycles(instruction);
assert_eq!(cycles, 2);
```

The code is used in the larger CKB project to calculate the cost of executing scripts in the CKB blockchain. The cost is used to prevent spam and ensure that scripts are executed efficiently.
## Questions:
 1. What is the purpose of this code file?
- This code file contains a cost model that assigns cycles to instructions in the CKB VM.

2. How is the number of cycles spent to load a specified number of bytes calculated?
- The function `transferred_byte_cycles` calculates the number of cycles spent to load a specified number of bytes by dividing the number of bytes by `BYTES_PER_CYCLE` and rounding up to the nearest integer.

3. What instructions have a cycle cost other than 1?
- Instructions such as `OP_LD`, `OP_LW`, `OP_LH`, `OP_LB`, `OP_LWU`, `OP_LHU`, `OP_LBU`, `OP_SB`, `OP_SH`, `OP_SW`, `OP_SD`, `OP_BEQ`, `OP_BGE`, `OP_BGEU`, `OP_BLT`, `OP_BLTU`, `OP_BNE`, `OP_EBREAK`, `OP_ECALL`, `OP_JAL`, `OP_MUL`, `OP_MULW`, `OP_MULH`, `OP_MULHU`, `OP_MULHSU`, `OP_DIV`, `OP_DIVW`, `OP_DIVU`, `OP_DIVUW`, `OP_REM`, `OP_REMW`, `OP_REMU`, `OP_REMUW`, `OP_WIDE_MUL`, `OP_WIDE_MULU`, `OP_WIDE_MULSU`, `OP_WIDE_DIV`, `OP_WIDE_DIVU`, `OP_FAR_JUMP_REL`, and `OP_FAR_JUMP_ABS` have a cycle cost other than 1.
