# Clang IR (CIR)

CIR is a new IR for Clang. The [LLVM's discourse RFC](WIP) goes in depth about
this project motivation's, status and design choices.

This repo contains a stack of commits rebased on top of LLVM upstream - see
[latest-upstream-llvm branch](WIP) for the exact starting point. The 'main'
branch is occasionally updated on top of LLVM upstream.

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

CIR is as part of LLVM and can be enabled in a build by solely adding `mlir`
and `clang` to the CMake list of *enabled projects*:

```
... -DLLVM_ENABLE_PROJECTS="clang;mlir;..." ...
```

See the [steps
here](https://llvm.org/docs/GettingStarted.html#local-llvm-configuration) for
instruction on how to build LLVM.

One quick example on building CIR in a mac laptop follows:

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
