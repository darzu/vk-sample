# Building

The repository contains everything required to compile and build the examples on Windows using a C++ compiler that supports at least C++14. All required dependencies are included. The project uses [CMake](https://cmake.org/) as the build system.

## General CMake options

### Asset path setup

Asset (and shader) paths used by the samples can be adjusted using CMake options. By default, paths are absolute and are based on the top level of the current CMake source tree. The following arguments can be used to adjust this:

- ```RESOURCE_INSTALL_DIR```: Set an absolute path for assets and shaders to which they are installed and from which they are loaded
- ```USE_RELATIVE_ASSET_PATH```: Use a fixed relative (to the binary) path for loading assets and shaders

## Platform specific build instructions

### Windows
Use the provided CMakeLists.txt with [CMake](https://cmake.org) to generate a build configuration for your favorite IDE or compiler, e.g.:

```
cmake -G "Visual Studio 16 2019" -A x64
```

or to build from commmand line:
```
cmake .
cmake --build .
```

full clean rebuild everything and run (from Git Bash):
```
git clean -dfX
cmake .
cmake --build .
./bin/Debug/deferredshadows.exe
```

or one-line clean-run-clean
```
git clean -dfX && cmake . && cmake --build . && ./bin/Debug/deferredshadows.exe && git clean -dfX
```