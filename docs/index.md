# Clang IR (CIR)

CIR is a new IR for Clang. The [LLVM's discourse RFC](WIP) goes in depth about
this project motivation's, status and design choices.

The source of truth for CIR is found at
[https://github.com/facebookincubator/clangir](https://github.com/facebookincubator/clangir).

This repo contains a stack of commits rebased on top of LLVM upstream - see
[latest-upstream-llvm
branch](https://github.com/facebookincubator/clangir/tree/latest-upstream-llvm)
for the exact starting point. The 'main' branch is occasionally updated on top
of LLVM upstream.

## How to get ClangIR

### Clone

```
$ git clone https://github.com/facebookincubator/clangir.git llvm-project
```

### Adding as remote

Alternatively, one can just add remotes:

```
$ cd llvm-project
$ git remote add fbi git@github.com:facebookincubator/clangir.git
$ git checkout -b clangir fbi/main
```

## How to build

In order to enable CIR related functionality, just add `mlir`
and `clang` to the CMake list of *enabled projects* and do a regular
LLVM build.

```
... -DLLVM_ENABLE_PROJECTS="clang;mlir;..." ...
```

See the [steps
here](https://llvm.org/docs/GettingStarted.html#local-llvm-configuration) for
general instruction on how to build LLVM.

For example, building CIR on macOS could look like:

```
TBD
```

## How to run tests

Test are an important part on preventing regressions and covering functionality
on new features. There are multiple ways to run CIR tests.

The more aggresive (slower) one:
```
$ ninja check-all
```

CIR specific test targets using ninja:
```
$ ninja check-clang-cir
$ ninja check-clang-cir-codegen
```

Using `lit` from build directory:

```
$ cd build
$ ./bin/llvm-lit -a ../clang/test/CIR
```

## How to contribute

Any change to the project should be done over github pull requests, anyone is welcome to contribute!
