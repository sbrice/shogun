# Developing Shogun

## Requirements for merging your PR
 * Read some [tips](http://blog.ploeh.dk/2015/01/15/10-tips-for-better-pull-requests/) on how to write good pull requests.
    Make sure you don't waste your (and our) time by not respecting these basic rules.
 * All tests pass (your pull request causes [automatic checks](#buildfarm)).
    We will not look at the patch otherwise.
 * The PR is small in terms of lines changes.
 * The PR is clean and addresses **one** issue.
 * The number of commits is minimal (i.e. one), the message is neat and clear.
 * If C++ code: it is covered by [tests](#testing), it doesn't leak memory, its [API](#api) is documented, [code style](https://github.com/shogun-toolbox/shogun/wiki/Code-style).
 * If API example: it has a clear scope, it is minimal, it looks polished, it has a passing [test](#testing)
 * If docs: clear, correct English language, spell-checked
 * If notebook: cell output is removed, template is respected, plots have axis labels.
 * Formatting notebooks/docs: Please every sentence in a single line.

# Testing <a name="testing"></a>
There are three types of tests that can be executed locally, C++ unit tests, running the API examples, and integration testing the results of the API examples.
To activate them locally, enable the `-DENABLE_TESTING=ON` cmake switch before running cmake. Which tests are activated depends on your configuration.
Adding a test in most cases requires to re-run `cmake`.
All activated tests can be executed with

    make && make test

The first `make` is necessary as some tests need to be generated and/or compiled first.

Sometimes, it is useful to run a single test, which can be done via [ctest](https://cmake.org/Wiki/CMake/Testing_With_CTest), for example

    ctest -R unit-LibSVR
    ctest -R generated_cpp-binary_classifier-kernel_svm
    ctest -R integration_meta_cpp-binary_classifier-kernel_svm -V

If a test name (or even the `make test` target) does not exist, this means that your configuration did not include it.

If you are interested in details how the test is executed (command, variables, directory), add the `-V` option.
Further details can be extracted from the `CMakeLists.txt` configuration files in the tests folder.

## C++ Unit tests
These are based on the [googletest](https://github.com/google/googletest) framework and are located in `tests/unit/`.
You can compile them with

    make shogun-unit-test

You can execute single tests via `ctest`, or via directly executing the unit test binary and passing it a filter, which gives a more grained control over which sub-tests are executed

    ./bin/shogun-unit-test --gtest_filter=GaussianProcessRegression.apply_*

Note that wildcards are allowed. Running single sub-tests is sometimes useful (i.e. for bug hunting)

    ./bin/shogun-unit-test --gtest_filter=GaussianProcessRegression.apply_regression

### Debugging and Memory leaks
**All your C++ code and unit tests must be checked to not leak memory!**
You want to use a memory checker such as [valgrind](http://valgrind.org/) (or a debugger such as [gdb](https://www.gnu.org/software/gdb/)).
If you do that, you might want to compile with debugging symbols and without compiler optimizations, by using `-DCMAKE_BUILD_TYPE=Debug`

Then

    valgrind ./bin/shogun-unit-test --gtest_filter=GaussianProcessRegression.apply_regression
    gdb --args ./bin/shogun-unit-test --gtest_filter=GaussianProcessRegression.apply_regression

The option `--leak-check=full` for valgrind might be useful.
In addition to manually running valgrind on your tests, you can use `ctest` to check multiple tests.
This requires to be enable in dashboard reports in via `-DBUILD_DASHBOARD_REPORTS=ON`.
For example

    ctest -D ExperimentalMemCheck -R unit-GaussianProcessRegression

#### Adding tests
We aim to write clear, minimal, yet exhaustive tests of basic building blocks in Shogun.
Whenever you send us C++ code, we will ask you for a unit test for it.
We do test numerical results as compared to reference implementations (e.g. in Python), as well as corner cases, consistency etc.
Read on [test driven development](https://en.wikipedia.org/wiki/Test-driven_development), and search the web for tips on unit tests, e.g. [googletest's tips](https://github.com/google/googletest/blob/master/googletest/docs/Primer.md).

Take inspiration from existing tests when writing new ones.
Please structure them well.

## API example tests
Make sure to read [INTERFACES.md](INTERFACES.md) and [EXAMPLES.md](EXAMPLES.md) to understand how API examples are generated, you will need the cmake switch `-DBUILD_META_EXAMPLES=ON`.
Every API example is used for two tests: simple execution and continuous integration testing of results.
These two tests are executed for every enabled interface language.

Note that code for all interface examples needs to be generated as part of `make`, or using

    make meta_examples

This needs to be done everytime you add or modify an example.
Examples for compiled interface languages (e.g. C++, Java) need to be compiled, either as part of `make`, or via more specific targets, e.g.

    make build_cpp_meta_examples
    make build_java_meta_examples

Check the `CMakeLists.txt` in `examples/meta/*` for all such make targets.

### Simple execution.
These tests are to make sure the code is executable, and to generate results for integration testing.
These can be executed with `ctest` as described above, e.g.

    ctest -R generated*
    ctest -R generated_cpp-binary_classifier-kernel_svm -V

You can also execute the examples manually as described in [INTERFACES.md](INTERFACES.md).
Note that the `data` git submodule is required to run the examples, see [INSTALL.md](INSTALL.md).

Check the `CMakeLists.txt` in `examples/meta/*` for further details.

#### Adding tests
As every example is turned into a test when running `cmake`, all you need to do is to add an example as described in [EXAMPLES.md](EXAMPLES.md).

### Integration testing of results
You will note that each example produces an output file with the `*.dat` extension.
This is a serialized version of all numerical results of the example.
The purpose is to make sure all interface versions (say C++ and Python) of an example produce the same output, and that this output does not change over time.

The reference results are stored in the `data` git submodule, more precisely in `data/testsuite/meta/*`.
There is a symbolic link for both generated and reference results in the `build/tests/meta/` folder.
Naturally, these tests depend on executing the corresponding example first. Therefore, running a test does not run the example again, but it simply compares the output to the reference file.

Again `ctest` can be used,

    ctest -R integration_meta_*
    ctest -R integration_meta_cpp-binary_classifier-kernel_svm
    ctest -R integration_meta_python-binary_classifier-kernel_svm

See the `CMakeLists.txt` in `tests/meta` for details on the mechanics.

#### Adding tests
CMake automatically creates a test for every reference result file that it finds.
Therefore, if you want to add new test, for example after having added an example as described in [EXAMPLES.md](EXAMPLES.md), then you need to copy its generated output to the reference file folder, e.g.

    cp build/tests/meta/generated_results/cpp/regression/kernel_ridge_regression.dat data/testsuite/meta/regression/

Note we usually use the output of the C++ example as reference.

Once that is done, it would be good if you sent us a patch with the new test.
This is done via first sending a PR against the [shogun-data](https://github.com/shogun-toolbox/shogun-data), just like the standard [development cycle](#devcycle), after doing (in the `data` directory)

    git commit testsuite/meta/regression/kernel_ridge_regression.dat -m "Integration testing data for kernel ridge regression"
    git push origin

After this PR is merged, you need to send a second PR against the main repository, after commiting the updated version hash of the submodule (in the main shogun directory)

    git commit data -m "Updated to including kernel ridge regression test data"
    git push origin

If everything worked, then the [travis](#buildfarm) build in the second PR will include your test in all interface languages.
Please check the logs!

# Benchmarking <a name="benchmark"></a>
In Shogun we use [google-benchmark](https://github.com/google/benchmark) library to test the performance of the modules in the library.
In order to compile and run the benchmarks set the `BUILD_BENCHMARKS` cmake flags to true, i.e. run the cmake command with `-DBUILD_BENCHMARKS=ON` flag.

To run all the benchmakrs simply run:

    ctest -L benchmark

## Adding benchmarks
We aim to provide an easy way to benchmark modules in Shogun. Hence, whenever you send us new C++ implementation, please
consider writing benchmarks for it.

In order to add benchmark to a class, simply create a file next to the implementation, which name is suffixed with `_benchmark.cc`.
For example for the `RandomFourierDotFeatures` class the benchmarks are available in the `RandomFourierDotFeatures_benchmark.cc` file.
On top of this you need to explicitly specify to cmake that you have added a new benchmarking file.
`ADD_SHOGUN_BENCHMARK` cmake helper function should be used in `src/shogun/CMakeLists.txt` within the `benchmarking` to add a
benchmark implementations to build.
a new benchmarking file, add new benchmarks with the
`ADD_SHOGUN_BENCHMARK` cmake function the following way. In the `src/shogun/CMakeLists.txt`
file within the `benchmarking` section using th

    ADD_SHOGUN_BENCHMARK(classifier/YOLOClassifier_benchmark)


## Adding benchmarks
We aim to write clear, minimal, yet exhaustive tests of basic building blocks in Shogun.
Whenever you send us C++ code, we will ask you for a unit test for it.
We do test numerical results as compared to reference implementations (e.g. in Python), as well as corner cases, consistency etc.
Read on [test driven development](https://en.wikipedia.org/wiki/Test-driven_development), and search the web for tips on unit tests, e.g. [googletest's tips](https://github.com/google/googletest/blob/master/googletest/docs/Primer.md).



# Build farm <a name="devcycle"></a>
We run two types of buildfarms that are automatically triggered

1. [Travis](https://travis-ci.org/shogun-toolbox/shogun), and [AppVeyor](https://ci.appveyor.com/project/vigsterkr/shogun) executed in a third-party cloud when **opening** a PR
2. [Buildbot](http://buildbot.shogun-toolbox.org/waterfall), executed in our own cloud **after** every merged PR or commit

In addition, we have a few hooks on PRs that are executed along with travis, such as a preview of API examples.
You will see a list of checks in your PR.

## Travis
This is to do basic sanity checks on every PR. All interfaces have a different build, see `.travis.yml` in the repository.
The Docker image that runs the travis tests is based on `configs/shogun/Dockerfile` and can be found [here](https://hub.docker.com/r/shogun/shogun-dev/).

If you obbey the [dev cycle](#devcycle), in particular if you run tests before sending a PR, travis should never fail.

**If** travis fails

1. **Read the logs**, find the error message
2. Try to identify the problem
3. Find out whether you caused it
4. If so, reproduce locally
5. Fix it and update your PR

## Buildbot
This service builds and tests Shogun in a large number of different configurations, OS, interfaces, etc.
It ensures Shogun is portable, the build is backward compatible. It analysis Shogun's memory usage and performs static code analysis.
It often catches very subtle errors

After one of your PR is merged, check the status of the buildbot for a while.
The [waterfall](http://buildbot.shogun-toolbox.org/waterfall) view is most useful.
Again, check the logs if there are problems.


# CMake options for developers <a name="cmake"></a>
See also [INSTALL.md](INSTALL.md).
Options for developers (debugging symbols on, optimization off, etc.):

    cmake -DCMAKE_BUILD_TYPE=Debug -DENABLE_TESTING=ON -DBUILD_DASHBOARD_REPORTS=ON ..

Options for building the final binaries (debugging off, optimization on):

    cmake -DCMAKE_BUILD_TYPE=Release ..

# API documentation <a name="api"></a>
Shogun uses [doxygen](http://www.stack.nl/~dimitri/doxygen/) for its [API documentation](shogun.ml/api).
Every bit of C++ code that is added to Shogun needs doxygen compatible source-code comments.

 * Every class needs a description of what it implements. If possible, use LaTeX for math.
 * Every method needs a description, plus all parameters and return values documented.

Check existing code for inspiration. Documentation is important, so polish as good as you can!

If you have doxygen installed, you can generate the documentation locally via running

    make doxygen

and then opening `build/doc/doxygen/html/index.html` with the browser.

With the `DOXYGEN_HTML_OUTPUT` cmake flag one can turn off HTML generation of the API documentation (`-DDOXYGEN_GENERATE_HTML=NO`).

