# Examples

A set of examples that use different widely used libraries (boost, protobuf, thrift etc.)


## Building

Supported OS: Windows, Linux.

### Windows

Prerequisites:

1. Download git, cmake and add them to PATH
2. Download the latest CPPAN (https://cppan.org/) client from https://cppan.org/client/
3. Add cppan to PATH too.
4. Enter any example dir you like.

```
cppan
mkdir build && cd build
cmake ..
cmake --build . --config Release
```

### Linux

Prerequisites:

1. Install git, cmake, the latest CPPAN (https://cppan.org/) client from https://cppan.org/client/ (.deb or .rpm client for your system, gcc-5 ABI is required).
2. Enter any example dir you like.
3. Run:

```
cppan
mkdir build && cd build
cmake ..
make -j4
```
