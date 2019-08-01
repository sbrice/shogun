## Interfaces <a name="manual-interfaces"></a>
The native C++ interface is always included.
The cmake options for building interfaces are `-DINTERFACE_PYTHON=ON -DINTERFACE_R ..` etc.
For example, replace the cmake step above by
```
cmake -DINTERFACE_PYTHON=ON [potentially more options] ..
```

The required packages (here debian/Ubuntu package names) for each interface are

 * Python
   - `python-dev python-numpy`
   - For dealing with customized Python environments, see [here](#manual-python)
 * Octave
   - `octave liboctave-dev`
 * R
   - `r-base-core`
 * Java
   - `oracle-java8-installer`, non-standard, e.g. `https://launchpad.net/~webupd8team/+archive/ubuntu/java`
   - `jblas`, a standard third party library, `https://mikiobraun.github.io/jblas/`
 * Ruby
   - `ruby ruby-dev`, and `narray` a non-standard third party library, `http://masa16.github.io/narray/`, install with `gem install narray`
 * Lua
   - `lua5.1 liblua5.1-0-dev`
 * C-Sharp
   - `mono-devel mono-gmcs cli-common-dev`

To *use* the interfaces, in particular if not installing to the default system-wide location, see [INTERFACES.md](INTERFACES.md).
See [examples](#manual-examples) below for how to create the examples from the website locally.

## Generating examples <a name="manual-examples"></a>
All Shogun examples at our website are automatically generated code. You can
generate them (plus additional ones) locally (needs cmake switch `-DBUILD_META_EXAMPLES=ON`)

    make meta_examples

This requires [PLY for Python](https://pypi.python.org/pypi/ply), package `python-ply`, and [ctags](http://ctags.sourceforge.net/), package `ctags`.
Both source code and potential executables (C++, Java, C-Sharp) are created in `build/examples/meta/` when running `make`.

See [INTERFACES.md](INTERFACES.md) to run the generated examples and see [EXAMPLES.md](EXAMPLES.md) for more details on their mechanics.
See [DEVELOPING.md](DEVELOPING.md) for how the examples are used as tests.


## Customized Python environments <a name="manual-python"></a>
Often, there are multiple Python versions installed on the system.
There are various reasons for this, i.e. Linux without root access, MacOS + homebrew, using [Anaconda](https://www.continuum.io/downloads) or [virtualenv](https://virtualenv.pypa.io).
If Shogun is executed using a different Python version that the one it was built against, one will observe crashes when importing Shogun.
If this is your setup, you need to make sure that Shogun is both **built** and **executed** against the Python environment of **your** choice.
For that, you need to do something similar to

    cmake -DPYTHON_INCLUDE_DIR=/path/to/python/include/dir -DPYTHON_LIBRARY=path/to/python/libpythonVERSION.{so|dynlib} -DPYTHON_EXECUTABLE=/path/to/python/executable -DPYTHON_PACKAGES_PATH=/path/to/python/dist-packages ..

For example, for `brew` installed Python under MacOS, use something like:

    cmake -DPYTHON_INCLUDE_DIR=/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Headers -DPYTHON_LIBRARY=/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Versions/2.7/lib/libpython2.7.dylib  -DINTERFACE_PYTHON=ON ..

Under Linux, where you want to use Python 3, which is not the system's default:

    cmake -DPYTHON_INCLUDE_DIR=/usr/include/python3.3 -DPYTHON_EXECUTABLE:FILEPATH=/usr/bin/python3 -DPYTHON_PACKAGES_PATH=/usr/local/lib/python3.3/dist-packages -DINTERFACE_PYTHON=ON ..

On a Linux cluster without root access, using [Anaconda](https://www.continuum.io/downloads) (note you will need to activate your environment everytime you want to run Shogun):

    source path/to/anaconda/bin/activate
    cmake -DCMAKE_INSTALL_PREFIX=path/to/shogun/install/dir -DPYTHON_INCLUDE_DIR=path/to/anaconda/include/python2.7/ -DPYTHON_LIBRARY=path/to/anaconda/lib/libpython2.7.so  -DPYTHON_EXECUTABLE=path/to/anaconda/bin/python -DINTERFACE_PYTHON=ON ..

## Windows build <a name="manual-windows"></a>

Please see our [AppVeyor](https://ci.appveyor.com/project/vigsterkr/shogun) build.
It is recommended to use "Visual Studio 14 2015" or "MSBuild".
You will need to adjust all path names to the Windows style, e.g.

    git clone https://github.com/shogun-toolbox/shogun.git C:\projects\shogun
    git submodule -q update --init
    cd C:\projects\shogun
    md build && cd build

You need to specify a different generator in cmake (to match your IDE), e.g.

    cmake -G"Visual Studio 14 2015 Win64" -DCMAKE_BUILD_TYPE=Release -DBUILD_META_EXAMPLES=OFF -DENABLE_TESTING=ON ..

Compiling works as

    msbuild "C:\projects\shogun\build\shogun.sln" /verbosity:minimal /t:Clean /p:Configuration=Release /p:Platform=x64

Note: If you use /m in msbuild command without specifying the number, it may occur out of memory errors.
