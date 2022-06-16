# Clang IR (CIR)

Clang IR (CIR) is a new IR for Clang. The [LLVM's discourse RFC](WIP) goes in depth about
the project motivation, status and design choices.

The source of truth for CIR is found at
[https://github.com/facebookincubator/clangir](https://github.com/facebookincubator/clangir).

The [main](https://github.com/facebookincubator/clangir/tree/main) branch
contains a stack of commits, occasionally rebased on top of LLVM upstream,
tracked in
[latest-upstream-llvm](https://github.com/facebookincubator/clangir/tree/latest-upstream-llvm)
branch.

* toc
{:toc}

---

# Getting started

## Git repo

```
$ git clone https://github.com/facebookincubator/clangir.git llvm-project
```

## Remote

Alternatively, one can just add remotes:

```
$ cd llvm-project
$ git remote add fbi git@github.com:facebookincubator/clangir.git
$ git checkout -b clangir fbi/main
```

# Building

In order to enable CIR related functionality, just add `mlir`
and `clang` to the CMake list of *enabled projects* and do a regular
LLVM build.

```
... -DLLVM_ENABLE_PROJECTS="clang;mlir;..." ...
```

See the [steps
here](https://llvm.org/docs/GettingStarted.html#local-llvm-configuration) for
general instruction on how to build LLVM.

For example, building and installing CIR enabled clang on macOS could look like:

```
CLANG=`xcrun -f clang`
INSTALLDIR=/tmp/install-llvm

$ cd llvm-project/llvm
$ mkdir build-release; cd build-release
$ /Applications/CMake.app/Contents/bin/cmake -GNinja \
 -DCMAKE_BUILD_TYPE=Release \
 -DCMAKE_INSTALL_PREFIX=${INSTALLDIR} \
 -DLLVM_ENABLE_ASSERTIONS=ON \
 -DLLVM_TARGETS_TO_BUILD="X86" \
 -DLLVM_ENABLE_PROJECTS="clang;mlir" \
 -DCMAKE_CXX_COMPILER=${CLANG}++ \
 -DCMAKE_C_COMPILER=${CLANG} ../
$ ninja install
```

Check for `cir-tool` to confirm all is fine:

```
$ /tmp/install-llvm/bin/cir-tool --help
```

## Running tests

Test are an important part on preventing regressions and covering new feature
functionality. There are multiple ways to run CIR tests.

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

---

# How to contribute

Any change to the project should be done over github pull requests, anyone is welcome to contribute!

---

# Documentation

