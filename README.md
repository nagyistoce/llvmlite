# llvmlite

A lightweight LLVM python binding for writing JIT compilers

Old (llvmpy)[https://github.com/llvmpy/llvmpy] binding exposes a lot of LLVM but the mapping of C++ style memory management to python is error prone. Numba and many JIT compiler does not need a full LLVM API. Only the IR builder, optimizer, and JIT compiler APIs are necessary.

llvmlite is a project originally tailored for Numba's needs, using the following approach:

- A small C wrapper around the parts of the LLVM C++ API we need that are
not already exposed by the LLVM C API.
- A ctypes Python wrapper around the C API.
- A pure Python implementation of the subset of the LLVM IR builder that we
need for Numba.

## Key Benefits

- llvmlite IR builder is pure python
- llvmlite uses LLVM assembly parser which provide better error messages (no more segfault due to bad IR construction)
- Most of llvmlite uses the LLVM C API which is small but very stable and backward compatible (low maintenance when changing LLVM version)
- The binding is not a python C-extension (no need to wrestle with Python's compiler requirement and C++11 compatibility)
- llvmlite binding memory management is explicit obj.close() or with-context
- llvmlite is quite faster in early benchmarks (the Numba test suite is twice faster)

## LLVMPY Compatibility Layer

`llvmlite.llvmpy.*` provides a minimal LLVMPY compatibility layer.

## Build

You must have a LLVM build (libraries and header files) available somewhere. If it is not installed in a standard location, you may have to tweak the build script.

Under Windows, you must have (cmake)[http://www.cmake.org/] installed, and LLVM should have been built using cmake, in Release mode.

To build the llvmlite C wrapper, run `python ffi/build.py`.

## Run tests

Run `python runtests.py`.

## Install

TODO
