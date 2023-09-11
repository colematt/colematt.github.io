---
layout: post
title:  Building LLVM for RISC-V Cross Compilation
date: 2018-11-26 15:26:00 -0500
tags: [llvm, riscv]
---

So you want to build software for the RISC-V architecture (I'm playing with the [Open ISA Vega RV32M1 development board](https://open-isa.org/))? Great, you'll need a compiler. Although [GCC officially supports you](https://riscv.org/software-tools/risc-v-gnu-compiler-toolchain/), with [full upstream support as of GCC 7.1 and binutils 2.28](https://riscv.org/2018/08/update-on-the-development-of-the-risc-v-software-toolchain/), if you're interested in _hacking_ the compiler before building software, you've probably chosen LLVM. In that case, you'll need a bit more effort to get LLVM to build as a cross-compiler.

<!--more-->

## Prerequisites

This process assumes that you begin in the directory where your RISC-V GNU build tools and LLVM project directories will reside. You will need to determine the following locations, and expand them into a fully qualified path (i.e. `/home/user/...` not `~/...`) wherever they appear in a command.

| **Location**                        | **Description**                                       | **Example Value**                   |
| ----------------------------------- | ----------------------------------------------------- | ----------------------------------- |
| `$TOP`                              | The location where you want your cross-compiler       | `export TOP=$(pwd)`                 |
| `$RISCV_GNU_TOOLCHAIN_INSTALL_ROOT` | The location where the GNU toolchain installs itself. | `/$TOP/riscv-gnu-toolchain/install` |
| `$LLVM_INSTALL_ROOT`                | The location where LLVM installs itself.              | `/$TOP/llvm-project/install`        |

You'll also need some packages. This tutorial presumes Ubuntu 18.04.2 LTS, and thus gets the packages from Aptitude. These instructions will probably also work for other operating systems as well, you're just on your own for package management.

```shell
sudo apt-get update
sudo apt-get install autoconf automake autotools-dev bison build-essential \
  cmake curl flex gawk gcc gcc-multilib gperf libmpc-dev libmpfr-dev \
  libgmp-dev libncurses5-dev make ninja-build openjdk-8-jre python python3 \
  texinfo u-boot-tools zlib1g-dev 
```

## Installation

Change to the directory at which you want your cross-compiler source tree and set `$TOP` to this directory.

```shell
export TOP=$(pwd)
```

### Get the RISC-V GNU Toolchain

Briefly, the RISC-V foundation maintains a RISC-V GNU toolchain for x86 cross-compilation, which you will need to cross-compile. The build tooling handles this for you, [more information here.](https://github.com/riscv/riscv-gnu-toolchain#installation-linux)

```shell
cd $TOP
git clone --recursive https://github.com/riscv/riscv-gnu-toolchain
cd riscv-gnu-toolchain
mkdir install && export RISCV_GNU_TOOLCHAIN_INSTALL_ROOT=$(pwd)/install
./configure --prefix=$RISCV_GNU_TOOLCHAIN_INSTALL_ROOT --with-arch=rv32imc --with-abi=ilp32
make -j
```

### Get the LLVM Project Monorepo

The LLVM project monorepo is the easiest way to get all of the sources and put them in the correct location. Previously, one had to acquire all of the individual LLVM projects and extract them to the correct subdirectories in order for CMake to detect that you wanted to build these subprojects. Now, we simply specify these in the CMake invocation (see **Build LLVM**).

```shell
cd $TOP
git clone https://github.com/llvm/llvm-project.git
```

If you’d like to set your repository to a particular project release, reset the repository to the release's commit SHA (e.g. `d0d8eb2`) or its tag (e.g `llvmorg-7.0.1`), for example: 

```shell
cd $TOP/llvm-project
git reset --hard llvmorg-7.0.1`.
```

## Build LLVM

```shell
cd $TOP/llvm-project
mkdir build install && export LLVM_INSTALL_ROOT=$(pwd)/install
cd build
cmake -G Ninja \
  -DCMAKE_BUILD_TYPE="Debug" \
  -DCMAKE_INSTALL_PREFIX="$LLVM_INSTALL_ROOT" \
  -DBUILD_SHARED_LIBS=True \
  -DLLVM_USE_SPLIT_DWARF=True \
  -DLLVM_OPTIMIZED_TABLEGEN=True \
  -DLLVM_BUILD_TESTS=True \
  -DLLVM_EXPERIMENTAL_TARGETS_TO_BUILD="RISCV" \
  -DLLVM_ENABLE_PROJECTS="clang;lld;debuginfo-tests" \
  -DDEFAULT_SYSROOT="$RISCV_GNU_TOOLCHAIN_INSTALL_ROOT/riscv32-unknown-elf" \
  -DGCC_INSTALL_PREFIX="$RISCV_GNU_TOOLCHAIN_INSTALL_ROOT" \
  -DLLVM_DEFAULT_TARGET_TRIPLE="riscv32-unknown-elf" \
  ../
cmake --build . --target install
cmake --build . --target check-all
```

If you'd prefer a simple go/no-go test on the build, instead of running the time-expensive `check-all` target in the last step, inspect the return value (`echo $?`) of the first `cmake --build` command for a value of `0`.

## Invoking the Compiler

If you set the default sysroot (`-DDEFAULT_SYSROOT`), GCC install prefix (`-DGCC_INSTALL_PREFIX`) and default target triple (`-DLLVM_DEFAULT_TARGET_TRIPLE`) when building using CMake, you don't need to pass these arguments explicitly when invoking Clang:

```shell
$LLVM_INSTALL_ROOT/bin/clang [options...] infile
```

Otherwise, you do have to pass these arguments when invoking Clang:

```shell
$LLVM_INSTALL_ROOT/bin/clang \
  --sysroot=$RISCV_GNU_TOOLCHAIN_INSTALL_ROOT/riscv32-unknown-elf \
  --gcc-toolchain=$RISCV_GNU_TOOLCHAIN_INSTALL_ROOT \
  --target=riscv32-unknown-elf \
  [options...] infile 
```

Since passing these arguments can be tedious, you can alias these commands:

```shell
alias riscv-clang=$LLVM_INSTALL_ROOT/bin/clang --sysroot=$RISCV_GNU_TOOLCHAIN_INSTALL_ROOT/riscv32-unknown-elf --gcc-toolchain=$RISCV_GNU_TOOLCHAIN_INSTALL_ROOT --target=riscv32-unknown-elf
alias riscv-clang++=$LLVM_INSTALL_ROOT/bin/clang++ --sysroot=$RISCV_GNU_TOOLCHAIN_INSTALL_ROOT/riscv32-unknown-elf --gcc-toolchain=$RISCV_GNU_TOOLCHAIN_INSTALL_ROOT --target=riscv32-unknown-elf
alias | grep riscv-clang
```

----------

## Links
- [Building RISC Code with LLVM](https://groups.google.com/a/groups.riscv.org/forum/#!topic/sw-dev/eoV9FCLnaF0) discusses the _unrecognized command line option '-fforce-enable-int128'_ error.
- [lowRISC/risc-llvm at Github](https://github.com/lowRISC/riscv-llvm)
- [A Step-by-Step Guide to the LLVM RISC-V Backend](https://github.com/lowRISC/riscv-llvm/tree/master/docs)
- [Building LLVM with CMake](http://llvm.org/docs/CMake.html)
