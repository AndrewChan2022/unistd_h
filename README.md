[![Build status](https://ci.appveyor.com/api/projects/status/xvvs61dleihfd0w4?svg=true)](https://ci.appveyor.com/project/SSE4/unistd-h)

header-only Windows implementation of the `<unistd.h>` header.

tested on the following compilers:
- Visual Studio
- Clang for Windows (clang-cl)
- GCC (MinGW)

implements the following functions:
- access
- chdir
- close
- dup
- dup2
- execl
- execle
- execlp
- execp
- execpe
- execpp
- rmdir
- unlink


# build

```bash
cmake -S . -B build -DCMAKE_INSTALL_PREFIX=windowsbuild/unistd
cmake --build build --target install --config Release -- /m
```

# usage

```bash

cmake_minimum_required(VERSION 3.12)
project(testunistd C)

# add to windows env path or manually add to CMAKE_PREFIX_PATH
list(APPEND CMAKE_PREFIX_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../windowsbuild/unistd)
find_package(unistd REQUIRED)

add_executable(${PROJECT_NAME} main.c)
target_link_libraries(${PROJECT_NAME} PRIVATE unistd::unistd)

```

# test

```bash
cd test
cmake -S . -B build
cmake --build build

build\Debug\testunistd.exe
```