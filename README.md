# Binary Rewriting Test Suite

This repository comprises a set of PE executable files encompassing a diverse array of code. Its primary goal is to facilitate testing the accuracy of bin2bin transformations. We are focused on assessing the effectiveness of our binary rewriting capabilities, particularly when applied to substantially large binaries exceeding 200MB which may have various "odd" behaviors. ***For now this repo will only contain x86 executables.***

### Usage 

Any PE files under `32bit/` and `64bit/` can be executed on the commandline. They will output text, you can compare this text with the transformed version of the binary to see if they match.

### SEH Tests

All tests under the `seh/` folder are 64bit PE executable files. These tests do not print anything out if successful, instead the exit code should be checked to make sure it is zero. If it is non-zero then the SEH test has failed.

### Why?

Most research papers on the topic of binary rewriting usually targets ELF files. Majority of these papers use the binutils that gnu ships. We are building software to protect windows executable files and I couldnt find a large repo with pre-compiled test bins ready to use. That is why this exists. This is also used by our CI workflows to test our code as we write it. Very useful!

### Test List

The test bins consist of tests from the following projects:

- zasm - https://github.com/zyantific/zasm/tree/master/examples
- chrome - https://developer.chrome.com/blog/chrome-for-testing/
- testfloat - https://github.com/backengineering/testfloat-pe
- openssl - https://github.com/openssl/openssl/tree/master/test
- llvm - [JIT Fibonacci](https://github.com/llvm/llvm-project/tree/main/llvm/examples/Fibonacci), [IRTransforms](https://github.com/llvm/llvm-project/tree/main/llvm/examples/IRTransforms), [OrcV2Examples](https://github.com/llvm/llvm-project/tree/main/llvm/examples/OrcV2Examples), [clang](https://clang.llvm.org/docs/UsersManual.html)
- coremark - https://github.com/backengineering/coremark-pe
- windows_seh_tests - https://github.com/Microsoft/windows_seh_tests
- windows compiler tests (more seh) - https://github.com/Microsoft/compiler-tests
- corkami weird pe files - https://github.com/corkami/pocs/tree/master/PE/bin
- vulnerable windows drivers - https://github.com/namazso/physmem_drivers
- VisualUEFI - https://github.com/ionescu007/VisualUefi
- MultiWorldDemo - https://github.com/UNAmedia/ue5-multiworld-demo
- FPChess - https://wiki.freepascal.org/fpChess
- loki testbins - https://github.com/RUB-SysSec/loki/tree/main/loki/testcases/real_world_crypto

This also contains all sorts of misc tests aimed at breaking disassembly (recursive functions, functions that call each other, noreturn functions, all sorts of jump tables).

### Compile Options & Binary Information

Most bins will be compiled with /O2, /GL, and /LTCG. However not all bins will be compiled with these options. Real world bins will have a wide range of optimization/compiler options so we try to replicate this by not having every single binary use /O2, /GL, etc. Its important to note this because code compiled with /GL you cannot assume volitile registers are really volitile. The compiler can do some non-abi stuff with functions inside of the binary.
