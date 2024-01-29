# Binary Rewriting Test Suite

This repository comprises a set of PE executable files encompassing a diverse array of code. Its primary goal is to facilitate testing the accuracy of bin2bin transformations. We are focused on assessing the effectiveness of our binary rewriting capabilities, particularly when applied to substantial binaries exceeding 200MB which may engaging in various "odd" behaviors.

### Why?

Most research papers on the topic of binary rewriting usually targets ELF files. Majority of these papers use the binutils that gnu ships. We are building software to protect windows executable files and I couldnt find a large repo with pre-compiled test bins ready to use. That is why this exists.

### Terminology

- **bin2bin**: The process of reading in a binary file, applying transformations, and producing an output binary file.
- **Transformations**: Encompassing actions such as obfuscation, simplification, etc.
- **Well-Behaved Code** (Defined below)

### Well-Behaved Code

*Formal*

Consider the set of all possible code as M, the set of code produced by the compiler from a source language as J, and well-behaved code as the set P. P is a subset of J, and J is a subset of M.

*Informal*

Well-behaved functions encompass most functions emitted by a compiler, with a few specific exceptions. These exceptions include:

- Functions with relocations to memory outside of the binary itself.
- Functions with computed references into the middle of another compiled function.

### Test List

The test bins consist of tests from the following projects:

- testfloat - https://github.com/backengineering/testfloat-pe
- openssl - https://github.com/openssl/openssl/tree/master/test
- llvm - [JIT Fibonacci](https://github.com/llvm/llvm-project/tree/main/llvm/examples/Fibonacci), [IRTransforms](https://github.com/llvm/llvm-project/tree/main/llvm/examples/IRTransforms), [OrcV2Examples](https://github.com/llvm/llvm-project/tree/main/llvm/examples/OrcV2Examples), [clang](https://clang.llvm.org/docs/UsersManual.html)
- coremark - https://github.com/backengineering/coremark-pe

This also contains all sorts of misc tests aimed at breaking disassembly (recursive functions, functions that call each other, noreturn functions, all sorts of jump tables).

### How To Use The Tests

Any files inside of the `32bit/` and `64bit/` folders can be executed on the commandline. You should run the original exe, save the stdout, transform the PE, then run it again and compare the new stdout. The original and the transformed should be the same. If not something is broken!


Original:

```
E:\bin2bin-tests\64bit>i32_to_f32.exe
Testing i32_to_f32, rounding near_even, tininess before rounding.
372 tests total.
372 tests performed.
In 372 tests, no errors found in i32_to_f32, rounding near_even, tininess before rounding.
```

Transformed:

```
E:\bin2bin-tests\64bit>output.exe
Testing i32_to_f32, rounding near_even, tininess before rounding.
372 tests total.
372 tests performed.
In 372 tests, no errors found in i32_to_f32, rounding near_even, tininess before rounding.
```
