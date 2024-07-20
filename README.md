# CMaker

## What it does
- Make a Cargo for C/C++ from CMake.
- Support C and C++
- Use [`GoogleTest`](https://github.com/google/googletest) for test
- Use [`Google Benchmark`](https://github.com/google/benchmark) for benchmark
- Use [`Clang-format` and `Clang-tidy`](https://github.com/llvm/llvm-project) for static program analysis (not ready yet)
- Use `Memory Sanitizer` for memory safety check (not ready yet)

## Why do that
As we all know, Cargo might be the best package manager in the computer world. It helps us to create a library or an execuable as ease. In addition, it allows us to run some examples or bins of your choice by the cargo run command. However, Cargo is designed only for Rust progarmming language. If we use C++ more often, how can we configure CMake to function similarly to Cargo? `CMaker` it is.

## License
CMaker is under [CC0 1.0 Universial](./LICENSE) license, which means it's in the world-wide public domain.