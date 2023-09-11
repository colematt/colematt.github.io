---
layout: post
title:  "Building SPEC CPU2017 Sandboxes"
date:   2018-08-03 19:39:00 -0500
tags: [cpu2017, benchmarks]
---

You may want to build a sandbox if one or more of these sound familiar:

- You want to build recognizable, representative binaries instead of toy programs for experimentation, but you also don't want the overhead of the actual SPEC CPU2017 benchmark suite, nor a script to manage the binaries' execution.
- You want to modify the source code of the benchmarks without corrupting the SPEC CPU2017 source tree.  Modifying the source code is allowed if you use the `strict_rundir_verify=no` option in your configuration file, or if you create a modified installation of the benchmark using the `convert_to_development` utility. But an easier option is to create sandboxes for each benchmark program you wish to investigate, and it doesn't corrupt the source tree if you're reusing it with other experiments.
- You want to modify the options or inputs provided to the benchmarks to investigate how the benchmark binaries respond.

<!--more-->

## About SPEC CPU2017

SPEC CPU2017 is a benchmark suite containing compute-intensive programs for measuring performance on a variety of computer systems. In addition to running representative programs developed from real applications with representative data sets, CPU2017 includes a driver program  -- `runcpu` -- which calls necessary utilities for benchmarking.

- `specmake` builds the benchmark binaries. If you want to try linking a library into the benchmark binaries, `specmake` will not permit this because [only a subset of typical compiler options are available](https://www.spec.org/cpu2017/Docs/config.html#sectionIII.A).
- `specinvoke` invokes the binaries and times their execution. Part of this invocation is using a specified input data set. If you want to provide your own inputs, or don't want the timing information output to the console, this is problematic.
- `specdiff`compares the output of the benchmark to supplied outputs for the data sets. If you have modified the binary in order to perform an evaluation other than performance, these comparisons will fail, generating unnecessary errors.

## Overview

See these two pieces of official documentation (but don't follow them at this time):
  
- [Avoiding runcpu](https://www.spec.org/cpu2017/Docs/runcpu-avoidance.html)
- [Sandbox Creation](https://www.spec.org/cpu2017/Docs/config.html#sectionIII.E)

Briefly, we use [runspec --action buildsetup](https://www.spec.org/cpu2017/Docs/runcpu.html#action) to create a standalone build directory and build the desired binaries. Then we invoke the binaries from the command line.

# Sandbox Creation and Employment

## Configure the Sandbox 

1. Copy **sandbox.cfg** and **sandbox.sh** from `$SPEC/config/tiny-examples/` to `$SPEC/config/` (note that by default, `runspec` will search `$SPEC/config/` for **sandbox.cfg** and halts creation if it's not found; the official instructions don't mention this).
2. Modify **sandbox.cfg** as required. Note that this is where you're going to specify any special [specmake variables](https://www.spec.org/cpu2017/Docs/makevars.html) on a benchmark-by-benchmark basis.
3. Source **sandbox.sh** to generate the sandbox.
4. Make modifications to source file as desired. Note that it may be required to copy over input files from `$SPEC/benchspec/CPU/$BENCHMARK/data/**`

## Build and Run the Sandbox Binaries

1. Be sure to source **$SPEC/shrc** if specmake is not in your `$PATH` (try `which specmake` to determine if this is required). If you don't, you will receive a *specmake: command not found* error in step 3. Your `$PWD` must be `$SPEC` when you source shrc or else you will receive a *Can't find the top of your SPEC tree* error. 
2. Change directory to the benchmark's build directory within the sandbox. The sandbox itself defaults to `/tmp/demo_buildsetup` as specified by the `output_root` variable in **sandbox.cfg**, and thus the build directories are located at `/tmp/demo_buildsetup/benchspec/CPU/**/build/`
3. Do a [specmake --dry-run](https://www.spec.org/cpu2017/Docs/utility.html#specmake) to verify that specmake will build the benchmark properly. Particularly observe that your specmake special variables' ordering is sane, such that the compilation and linking commands are each well formed.
4. Run specmake to actually build your binary.
5. Execute the binary using the command line interface specified in the [benchmark descriptions](https://www.spec.org/cpu2017/Docs/index.html#benchmarks). You can also find examples of invocation within `$SPEC/result/CPU2017.*.log` files.

### Example configuration and scripting

```ini
#!$SPEC/bin/runcpu
# $SPEC/config/sandbox.cfg

# Edit these variables to link a library to the sandbox
%define MYLIB_PATH /home/matthew/github/bingseclab/MYLIB
%define MYLIB_LIB_PATH %{MYLIB_PATH}/lib
%define MYLIB_INCL_PATH %{MYLIB_PATH}/incl

# Edit these variables to configure your sandbox
%define SANDBOX MYLIB
action = buildsetup
label = %{SANDBOX}-base
output_root = /tmp/sandbox_%{SANDBOX}
runlist = 519.lbm, 531.deepsjeng
tune = base
default=base:
  OPTIMIZE = -march=native -fno-unsafe-math-optimizations

# Configure benchmark builds (passed to specmake)
519.lbm_r,619.lbm_s: #lang='C'
 COBJOPT = -c -g -O0 -o $@
 EXTRA_CFLAGS = -I%{MYLIB_INCL_PATH} -L%{MYLIB_LIB_PATH}
 EXTRA_LDFLAGS = -I%{MYLIB_INCL_PATH} -L%{MYLIB_LIB_PATH}
 EXTRA_LIBS = -lMYLIB

531.deepsjeng_r,631.deepsjeng_s: #lang='CXX'
 CXX = /usr/bin/g++
 CXXOBJOPT = -c -g -O0 -o $@
 EXTRA_CXXFLAGS = -I%{MYLIB_INCL_PATH} -L%{MYLIB_LIB_PATH}
 EXTRA_LDFLAGS = -I%{MYLIB_INCL_PATH} -L%{MYLIB_LIB_PATH}
 EXTRA_LIBS = -lMYLIB
```

```bash
#!/bin/bash
# sandbox.sh
# see "Stupid Assumptions" in $(SPEC)/config/tiny-examples/contents

runcpu --config=sandbox | grep log
grep Makefile.spec /tmp/sandbox-MYLIB/result/CPU2017.001.log
```
