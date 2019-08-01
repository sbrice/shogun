# Building Shogun

Depending on what platform or features you need, the build process may
differ. After you've built the library, running the
test suite to confirm that everything works as intended is a good next step.

If you can reproduce a test failure, search for it in the
[issue tracker](https://github.com/shogun-toolbox/shogun/issues) or
file a new issue.

## Table of Contents

* [Prerequisites](#prerequisites)
* [Unix and macOS](#unix-and-macos)
  * [Unix prerequisites](#unix-prerequisites)
  * [macOS prerequisites](#macos-prerequisites)
  * [Building Shogun](#building-shogun)
  * [Running Tests](#running-tests)
  * [Running Coverage](#running-coverage)
  * [Building the Language Interfaces](#building-the-language-interfaces)
  * [Building the Documentation](#building-the-documentation)
  * [Building the Meta Examples](#building-meta-examples)
  * [Building a Debug Build](#building-a-debug-build)
* [Windows](#windows)
  * [Prerequisites](#prerequisites)
  * [Building Shogun](#building-shogun-1)
* [Building with CMake](#building-with-cmake)
  * [Specifying a different SWIG executable](#specifying-a-different-swig-executable)
  * [Specifying a different C/C++ compiler](#specifying-a-different-cc-compiler)
  * [Specifying header/library locations](#specifying-headerlibrary-locations)

## Prerequisites

Compiling Shogun requires the standard GNU/Linux toolchain and **at least 1GB of free disk space**.

For compiling language interfaces, roughly 4GB of RAM is needed (we are working on reducing this). [CCache](https://ccache.dev/) will massively speed up the compilation process and is enabled by default if installed. Each interface has language specific requirements, see [Building Interfaces](#building-interfaces) below for details.

To build the meta examples [`python-ply`](https://pypi.org/project/ply/) and [`ctags`](http://ctags.sourceforge.net/) are required by default unless disabled using the `cmake` variable `-DBUILD_META_EXAMPLES=Off`. For details see [Building the Meta Examples](#building-the-meta-examples).

There is a larger list of optional requirements. The output of `cmake` at build time will list optional dependencies that were found or not found on your system. If a particular Shogun class is unavailable, it is likely due to an unmet dependency. See our CI test build [Dockerfile](https://github.com/shogun-toolbox/shogun/blob/develop/configs/shogun/Dockerfile) for an example configuration.

## Unix and macOS

### Unix prerequisites

* `gcc` and `g++` >= 6.3 or newer, or
* GNU Make 3.81 or newer
* [Python](https://www.python.org/downloads/)
* [CMake](https://cmake.org/download/)
* [SWIG](http://www.swig.org) ([install](https://www.dev2qa.com/how-to-install-swig-on-macos-linux-and-windows/))
* [`ctags`](http://ctags.sourceforge.net/) ([install](https://gist.github.com/sbrice/4ebc470eca1f53e7f32ed62a3dd0b276))
* [CCache](https://ccache.dev/)
* [Doxygen](http://www.doxygen.nl/)
* [clang-format](https://clang.llvm.org/docs/ClangFormat.html)

Installation via Linux package manager can be achieved with:

* Ubuntu, Debian: `sudo apt-get install python g++ make cmake ctags swig ccache doxygen`
* Fedora: `sudo dnf install python gcc-c++ make cmake ctags swig ccache doxygen`

### macOS prerequisites

* Xcode Command Line Tools >= 8 for macOS
* [Python](https://www.python.org/downloads/)
* [CMake](https://cmake.org/download/)
* [SWIG](http://www.swig.org) ([install](https://www.dev2qa.com/how-to-install-swig-on-macos-linux-and-windows/))
* [`ctags`](http://ctags.sourceforge.net/) ([install](https://gist.github.com/sbrice/4ebc470eca1f53e7f32ed62a3dd0b276))
* [CCache](https://ccache.dev/) ([install](http://macappstore.org/ccache/))
* [Doxygen](http://www.doxygen.nl/) ([install](http://macappstore.org/doxygen/))
* [clang-format](https://clang.llvm.org/docs/ClangFormat.html)

macOS users can install the `Xcode Command Line Tools` by running
`xcode-select --install`. Alternatively, if you already have the full Xcode
installed, you can find them under the menu `Xcode -> Open Developer Tool ->
More Developer Tools...`. This step will install `clang`, `clang++`, and
`make`.

---

### Jump To:

* [Building Shogun](#building-shogun)
* [Running Tests](#running-tests)
* [Building the Language Interfaces](#building-the-language-interfaces)
* [Building the Documentation](#building-the-documentation)
* [Building the Meta Examples](#building-meta-examples)
* [Building a Debug Build](#building-a-debug-build)

---

### Building Shogun

To build Shogun, first clone the source code (including GNU submodules) then run `cmake` (with desired variable) and `make` from within a staging directory (e.g. `build`):

```
git clone https://github.com/shogun-toolbox/shogun.git
cd shogun
git submodule update --init
mkdir build && cd build
cmake .. -DBUILD_META_EXAMPLES=Off -DENABLE_TESTING=On -DCMAKE_BUILD_TYPE=Debug
make
```

### Running Coverage

**Warning:** Coverage is only available with the `GNU gcc` compiler. It won't work with e.g. the default macOS `Apple LLVM clang` compiler.

**Note:** `cmake` must have been run with the variable `-DENABLE_COVERAGE=On` to enable the `coverage` target for `make`.

It's good practice to ensure any code you add or change is covered by tests. You can do so by running the test suite with coverage enabled:

```
make coverage
```

### Running Tests

**Note:** `cmake` must have been run with the variable `-DENABLE_TESTING=On` to enable the `test` target for `make`.

To verify the build:

```
make test
```

For more on testing see the [Developer Guide](./doc/guides/developing.md#testing).

### Building the Language Interfaces

To build the Shogun documentation:

```
make doc
```

For more on building the Language Interfaces see the [Language Interfaces Guide](./doc/guides/building-the-language-interfaces.md).

### Building the Documentation

To build the Shogun documentation:

```
make doc 
```

This will generate the C++ Doxygen HTML/XML Documentation (i.e. [shogun.ml/api](http://shogun.ml/api)) into your local build direcotry e.g. `build/doc/doxygen/{html,xml}`. You can view the docs from you browser by running e.g.:

```
open build/doc/doxygen/html/index.html
```

### Building the Meta Examples

To build the Shogun API Meta Examples (aka Shogun API Cookbook):

```
echo 'hmmm...`
```

For more on building the Meta Examples see the [Meta Examples Guide](./doc/guides/building-the-meta-examples.md).

### Building a Debug Build

To build a Debug build documentation:

## Windows

### Prerequisites

* [Python](https://www.python.org/downloads/)
* The "Desktop development with C++" workload from
  [Visual Studio 2017](https://www.visualstudio.com/downloads/) or the
  "Visual C++ build tools" workload from the
  [Build Tools](https://www.visualstudio.com/downloads/#build-tools-for-visual-studio-2017),
  with the default optional components.
* Basic Unix tools required for some tests,
  [Git for Windows](http://git-scm.com/download/win) includes Git Bash and tools which can be included in the global `PATH`.

### Building Shogun

If the path to your build directory contains a space or a non-ASCII character,
the build will likely fail.

```console
> .\vcbuild
```

To run the tests:

```console
> .\vcbuild test
```

To test if Node.js was built correctly:

```console
> Release\node -e "console.log('Hello from Node.js', process.version)"
```

## Building with CMake

CMake is a beast.

We encourage you to read the [Documentation](https://cmake.org/documentation/) and learn about the [*Useful Variables*](http://cmake.org/Wiki/CMake_Useful_Variables). 

In using CMake it's important to understand the concept of [**out of source builds**](https://cmake.org/Wiki/CMake_FAQ#Out-of-source_build_trees).

### Specifying a different SWIG executable

To specify a different SWIG executable when building with CMake use the `SWIG_EXECUTABLE` variable:

```
cmake .. -DSWIG_EXECUTABLE=/usr/bin/swig_custom
```
### Specifying a different C/C++ Compiler

To specify a different compiler set the environment `CC` and `CXX` variables.

```
CC=/path/to/gcc CXX=/path/to/g++ cmake ..
```

You may need to delete the build directory or clear the `cmake` cache.

See CMake FAQ [*How do I use a different compiler?*](http://www.cmake.org/Wiki/CMake_FAQ#How_do_I_use_a_different_compiler.3F) for details.

### Specifying header/library locations

To specify header files or libraries in custom locations, manually adjust the library and include paths with the `CMAKE_INCLUDE_PATH` and `CMAKE_LIBRARY_PATH` variables:

```
cmake .. -DCMAKE_INCLUDE_PATH=/my/include/path -DCMAKE_LIBRARY_PATH=/my/library/path
```