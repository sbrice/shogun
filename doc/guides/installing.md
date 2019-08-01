# Installing Shogun

The Shogun project releases pre-build packages for easy and quick install on various systems using popular package managers. 

If your system is not in the list below you will have to [Install from Source](#installing-from-source).

# Table of Contents
* [Anaconda Cloud](#anaconda-cloud)
* [macOS](#macos)
* [Windows](#windows)
* [Ubuntu](#ubuntu)
* [Debian](#debian)
* [Fedora](#fedora)
* [Docker](#docker)
* [Installing from Source](#installing-from-source)

# Anaconda Cloud

Install Shogun from [Anaconda Cloud](https://docs.anaconda.com/anaconda/install/) by running:

```
conda install shogun
```

**Available packages:**
* [`shogun`](https://anaconda.org/conda-forge/shogun) - Latest stable release of the base Shogun C++ library and Python interfaces.
* [`shogun-cpp`](https://anaconda.org/conda-forge/shogun) - Latest stable release of the base Shogun C++ library only.

# macOS

Install Shogun on macOS with [Homebrew](https://formulae.brew.sh/formula/shogun) by running:

```
brew install shogun
```

# Windows

Shogun natively compiles under Windows using Microsoft Visual C++. 

We currently only support installing binary packages via [`conda`](#anaconda-cloud) or by [installing from source](#installing-from-source).

If you are interested in packaging, documenting, or contributing to this section please [contact the TSC](../../README.md#tsc-technical-steering-committee).

# Ubuntu

Install Shogun from the official [`shogun-toolbox/stable`](https://launchpad.net/~shogun-toolbox/+archive/ubuntu/stable) Prepackaged PPA contaning the C++ library and Python bindings by running:

```
sudo add-apt-repository ppa:shogun-toolbox/stable
sudo apt-get update
sudo apt-get install libshogun18
```

For the nightly builds of our development branch use the [`shogun-toolbox/nightly`](https://launchpad.net/~shogun-toolbox/+archive/ubuntu/stable) PPA.

# Debian

Latest Debian (`stretch` or `jessie` on AMD64 architecture only) packages are available from the official Shogun repository at [`http://apt.shogun.ml`](http://apt.shogun.ml).

To install on your system, first configure your packaging tool by running (e.g. for Debian `stretch`):

```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3DD2174ACAB30365
echo "deb http://apt.shogun.ml/ stretch main" | sudo tee /etc/apt/sources.list.d/shogun-toolbox.list  > /dev/null
sudo apt-get update
```

Then install the library by running:

```
sudo apt-get install libshogun18
```

Nightly packages are available from our `nightly` component at e.g. `deb http://apt.shogun.ml/ stretch nightly`.

# Fedora

Install Shogun on [Fedora](https://apps.fedoraproject.org/packages/shogun) by running: 

```
sudo dnf install shogun
```

# Docker

The official Shogun Docker images are located in the [`shogun/shogun`](https://hub.docker.com/r/shogun/shogun/) Docker Hub repository. 

Image releases are [tagged](https://hub.docker.com/r/shogun/shogun/tags/) using the following format:

| Tag        | Descrption   |
| -----------|--------------|
| `master`   | Follows the `master` branch of the [`shogun-toolbox/shogun`](https://github.com/shogun-toolbox/shogun) repository.
| `develop`  | Follows the `develop` branch of the [`shogun-toolbox/shogun`](https://github.com/shogun-toolbox/shogun) repository.

Download the latest Shogun `master` branch image to your machine by running:

```
docker pull shogun/shogun:master
```

Then run the Shogun configured container in interactive mode with:

```
docker run -it shogun/shogun:master bash
```

You can also download the Docker SDK image used in our [Travis CI](https://travis-ci.org/shogun-toolbox/shogun/) builds from the [`shogun/shogun-dev`](https://hub.docker.com/r/shogun/shogun-dev/) Docker Hub repository.

# Installing from Source

### Step 1. Build from Source

To install Shogun from source, first ensure you can build the library on your system using the [build instructions](../../BUILDING.md).

When building remember to configure `cmake` for the desired language interfaces (e.g. `cmake .. -DINTERFACE_PYTHON=ON`). For more information see the section on [Building the Language Interfaces](../../BUILDING.md#building-the-language-interfaces)

### Step 2. Make Install

After successfully building from source run `make install` to install the built library to `/usr/local`. You can select a custom install location by running `cmake` with a custom `CMAKE_INSTALL_PREFIX` variable (e.g. `cmake .. -DCMAKE_INSTALL_PREFIX=/custom/path`). For more on `cmake` see the section on [Building with CMake](../../BUILDING.md#building-with-cmake).

If you run into any problems search for it in the [issue tracker](https://github.com/shogun-toolbox/shogun/issues/new) or file a new issue.