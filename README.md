# Binary Rewriting Test Suite

This repository comprises a set of PE executable files encompassing a diverse array of code. Its primary goal is to facilitate testing the accuracy of bin2bin transformations. We are focused on assessing the effectiveness of our binary rewriting capabilities, particularly when applied to substantially large binaries exceeding 200MB which may have various "odd" behaviors.

### Usage 

Any PE files under `32bit/` and `64bit/` can be executed on the commandline. They will output text, you can compare this text with the transformed version of the binary to see if they match.

### Why?

Most research papers on the topic of binary rewriting usually targets ELF files. Majority of these papers use the binutils that gnu ships. We are building software to protect windows executable files and I couldnt find a large repo with pre-compiled test bins ready to use. That is why this exists. This is also used by our CI workflows to test our code as we write it. Very useful!

### Test List

The test bins consist of tests from the following projects:

- testfloat - https://github.com/backengineering/testfloat-pe
- openssl - https://github.com/openssl/openssl/tree/master/test
- llvm - [JIT Fibonacci](https://github.com/llvm/llvm-project/tree/main/llvm/examples/Fibonacci), [IRTransforms](https://github.com/llvm/llvm-project/tree/main/llvm/examples/IRTransforms), [OrcV2Examples](https://github.com/llvm/llvm-project/tree/main/llvm/examples/OrcV2Examples), [clang](https://clang.llvm.org/docs/UsersManual.html)
- coremark - https://github.com/backengineering/coremark-pe
- windows_seh_tests - https://github.com/Microsoft/windows_seh_tests

This also contains all sorts of misc tests aimed at breaking disassembly (recursive functions, functions that call each other, noreturn functions, all sorts of jump tables).
