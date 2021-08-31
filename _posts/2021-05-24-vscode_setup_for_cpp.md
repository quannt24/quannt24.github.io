---
layout: default
title:  "My VSCode Setup for C/C++"
date:   Tue May 11 07:50:37 AM +07 2021
categories: C C++ VSCode
---

# Development Environment Outside of VSCode

- Linux
- gcc, g++
- cmake
- git

# Extensions

Following extensions are installed:

- C/C++ [ms-vscode.cpptools]: For C/C++ language support.
- C++ Helper [amiralizadeh9480.cpp-helper]: Optional, for generating header guards and function implementations.
- CMake [twxs.cmake]: For language support for CMake files.
- CMake Tools [ms-vscode.cmake-tools]: Support development of projects using CMake, such as build system (of course, instead of using the compilers/toolchains directly by VSCode) build/include/link paths, build kits...
- Git Graph [mhutchie.git-graph]: Full graph of Git history.

If developing remotely, i.e. the real development environment is a Linux host, while VSCode runs from another machine (possibly Windows), the above extensions shall be installed in the remote host. And the following extensions shall be installed in local:

- Remote - SSH [ms-vscode-remote.remote-ssh]

# CMake Kits

When building by `cmake` from CLI and a toolchain file is required, it is usually passed as a CLI argument, i.e.:
```
cmake \
    -DCMAKE_TOOLCHAIN_FILE=$TOOLCHAIN_FILE \
    $TOP_DIR
```

It could be more integrated if VSCode can pick up the toolchain file and pass the argument to `cmake`, or even as a kit. This is achieved by using CMake Tools' `cmake-kits.json`. It makes sense to have this file per project (e.g. `.vscode/cmake-kits.json`). The content is similar to:
```
[
  {
    "name": "ppc-toolchain",
    "toolchainFile": "/opt/ppc-toolchain/ppc-toolchain.cmake"
  },
  {
    "name": "gcc-4.7-toolchain",
    "toolchainFile": "gcc-4.7-toolchain.cmake"
  }
]
```

There are several ways to specify CMake kits, which suite different requirements. Toolchain file is a neat way doing this comparing to specifying compilers directly because the same mechanism is used by CLI.

# Random Things

## Position of new tab (editor)

In Settings:

Controls where editors open. Select left or right to open editors to the left or right of the currently active one. Select first or last to open editors independently from the currently active one.
```
"workbench.editor.openPositioning": "last",
```

# References

- https://vector-of-bool.github.io/docs/vscode-cmake-tools/kits.html
