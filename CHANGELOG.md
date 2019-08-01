2018-06-01 Viktor Gal <viktor.gal@shogun-toolbox.org>

        * SHOGUN Release version 6.2.0 (libshogun 18.0, data 0.11, parameter 1)

        * First BSD 3-clause license release (see LICENSE file)
        [Heiko Strathmann, Viktor Gal, Esben Sørig]
        * Introduced new API based on generic put/get calls, factory methods,
        and fewer types. Used in examples. Requires Swig>=3.0.12
        [Heiko Strathmann, Sergey Lisitsyn, Viktor Gal, Esben Sørig]

        * Features:
                - Introduce automatic label conversion if inappropriate type is
                passed [Heiko Strathmann]
                - Replace many CMath calls with std [Akash Shivram, Yash Sharma,
                Shubham Shukla, Albert Sun, Viktor Gal, Heiko Strathmann, Esben
                Sørig]
                - Ported equals and clone methods to new tag-based parameter
                framework [Heiko Strathmann, Sergey Lisitsyn]
                - Removal of computation engine framework and parallelisation of
                log-determinant estimators [Shubham Shukla]
                - Add StanMath as a bundled third-party library and use Eigen
                shipped with StanMath [Elfarouk Yasser, Viktor Gal]
                - Efficiency improvements for MahalanobisDistance, LMNN, ridge
                regression, GMM, and the linalg framework [Wuwei Lin]
                - Add LDLT decomposition to linalg [Wuwei Lin]
                - New DotIterator API for more efficient and cleaner algorithm
                code [Michele Mazzoni]
                - Numpy>=1.7 is now required [Viktor Gal]
                - Relicensed libqp and libocas to BSD, thanks to Vojtech Franc
                [Viktor Gal]
                - Added a time-series cross-validation splitting strategy
                [Sahil Chaddha]
                - Drop obsolute VW codes [Saloni Nigam]
                - Add shogun::variant that is using mpark variant or
                std::variant depending what is available [Wuwei Lin]
                - Add benchmarking framework [Viktor Gal]
                - Many new examples [various contributors]
        * Bugfixes:
                - Enable Shogun's custom signal handler by default
                [Giovanni De Toni]
                - Various fixes for native Windows build [Viktor Gal]
                - Fix bugs in Ruby NArray typemaps [Heiko Strathmann,
                Viktor Gal]
                - Fix/refactor Platt probability scaling for SVMSs
                [durovo <aryadhruv@gmail.com>]
                - Bugfix for train-test ratio in statistical testing
                [Soumyajit De]
                - Bugfix for custom kernels in MKL [David <dhelekal>]
                - json build error fix [Andrew Wildman]
                - Fix segfault in ROC error message [Chinmay Kousik]
                - Fix potential memory leak in GMM [Marcus Edel]
        * Known issues:
                - Ruby examples do not work with new API due to potential swig
                bug, see https://github.com/shogun-toolbox/shogun/issues/4177.
                Old API functional.

2017-12-05 Viktor Gal <viktor.gal@shogun-toolbox.org>

	* SHOGUN Release version 6.1.3 (libshogun 18.0, data 0.11, parameter 1)

	* Features:
		- Drop all <math.h> function calls [Viktor Gal]
		- Use c++11 std::isnan, std:isfinite, std::isinf [Viktor Gal]
	* Bugfixes:
		- Port ipython notebooks to be python3 compatible [Viktor Gal]
		- Use the shogun-static library on Windows when linking the interface library [Viktor Gal]
		- Fix python typemap when compiling with MSVC [Viktor Gal]
		- Fix ShogunConfig.cmake paths [Viktor Gal]
		- Fix meta example parser bug in parallel builds [Esben Sørig]

2017-11-29 Viktor Gal <viktor.gal@shogun-toolbox.org>

	* SHOGUN Release version 6.1.2 (libshogun 18.0, data 0.11, parameter 1)

	* Bugfixes:
		- Fix installation of examples on WIN32 [Viktor Gal]

2017-11-28 Viktor Gal <viktor.gal@shogun-toolbox.org>

	* SHOGUN Release version 6.1.1 (libshogun 18.0, data 0.11, parameter 1)

	* Bugfixes:
                - Install headers of GPL models when LICENSE_GPL_SHOGUN is enabled [Viktor Gal]
		- Always turn on LIBSHOGUN_BUILD_STATIC when compiling with MSVC [Viktor Gal]
		- Fix ipython notebook errors [Viktor Gal]

2017-11-28 Viktor Gal <viktor.gal@shogun-toolbox.org>

	* SHOGUN Release version 6.1.0 (libshogun 18.0, data 0.11, parameter 1)

	* This release is dedicated for Heiko's successful PhD defense

	* Add conda-forge packages, to get prebuilt binaries via the cross-platform conda package manager [Dougal Sutherland]
	* Change interface cmake variables to INTERFACE_*
	* Move GPL code to gpl submodule [Heiko Strathmann]

	* Features:
		- Enable using BLAS/LAPACK from Eigen by default [Viktor Gal]
		- Add iterators to SGVector and SGMatrix [Viktor Gal]
		- Significantly lower the runtime of KernelPCA (GSoC '17) [Michele Mazzoni]
		- Refactor FisherLDA and LDA solvers (GSoC '17) [Michele Mazzoni]
		- Add automated test for trained model serialization (GSoC '17) [Michele Mazzoni]
		- Enable SWIG director classes by default [Viktor Gal]
		- Vectorize DotFeatures covariance/mean calculation [Michele Mazzoni]
		- Support for premature stopping of model training (GSoC '17) [Giovanni De Toni]
		- Add support for observable variables (GSoC '17) [Giovanni De Toni]
		- Use TFLogger to serialize observed variables for TensorBoard (GSoC '17) [Giovanni De Toni]
		- Drop CMath::dot and SGVector::dot and use linalg::dot [Viktor Gal]
		- Added class probabilities for BaggingMachine (GSoC '17) [Olivier Nguyen]
	* Bugfixes:
		- Fix transpose bug in Ruby typemap for matrices [Elias Saalmann]
		- Fix MKL detection and linking; use mkl_rt when available [Viktor Gal]
		- Fix Windows static linking [Viktor Gal]
		- Fix SWIG interface compilation on Windows [qcrist]
		- Fix CircularBuffer bug that broke parsing of big CSV and LibSVM files #1991 [Viktor Gal]
		- Fix R interface when using clang to compile the interface [Viktor Gal]

2016-11-05 Viktor Gal <viktor.gal@shogun-toolbox.org>

	* SHOGUN Release version 6.0.0 (libshogun 18.0, data 0.11, parameter 1)

	* NOTE: Contains major rewrite and clean-up of developer documentation in doc/readme [Heiko Strathmann, Lea Götz]
	* NOTE: Known issue: Octave multithreaded crashes, currently bindings are initialized single-threaded, https://github.com/shogun-toolbox/shogun/issues/3772 [Heiko Strathmann]
	
	* Add native MS Windows support [Viktor Gal]
	* Shogun requires the compiler to support C++11 features
	* Shogun cloud online: Jupyter notebook with Shogun from the browser, https://cloud.shogun.ml

	* Features:
		- LDA now supports 32, 64 and 128 bit floating point numbers [Chris Goldsworthy]
		- Add SHOGUN_NUM_THREADS enviroment variable to control the number of threads
		used by the models in runtime [Viktor Gal]
		- Added Scala Interface to the build [Abhinav Rai]
		- Major re-writing and API changes in kernel statistical hypothesis 
		testing framework, significant speed up in permutation test for
		quadratic time MMD, new kernel selection algorithms for quadratic time MMD [Soumyajit De]
	* Bugfixes:
		- Fix build error of R interface for R>=3.3.0, #3460 [Heiko Strathmann]
		- Make the code compatible with Eigen 3.3.0 [Viktor Gal]
		- Fix number of CPUs detected on Linux [Viktor Gal]
		- Fix multi-threading in KMeansBase [Viktor Gal]
		- Make ExponentialARDKernel thread-safe [Viktor Gal]
		- Make PRNG thread-safe [Viktor Gal]
		- Fix python interface when using libshogun compiled with OpenMP [Viktor Gal]
		- Fix CART to work with cross-validation [Fernando Iglesias]
	* Cleanup, efficiency updates, and API Changes:
		- Port multi-threading to use OpenMP backend in Kernel [Viktor Gal]
		- Fix false sharing in EuclideanDistance [Viktor Gal]
		- Fix out of source build of the whole project [Viktor Gal]
		- Add LIBSHOGUN cmake flag to turn off libshogun compilation [Viktor Gal]
		- Export Shogun target with cmake to enable to build modular interfaces to a
		pre-compiled libshogun on the system without requiring to compile 
		libshogun itself [Viktor Gal]

2016-11-04 Viktor Gal <viktor.gal@shogun-toolbox.org>

	* SHOGUN Release version 5.0.0 (libshogun 17.2, data 0.11, parameter 1)
	
	* NOTE: This version contains a new CMake option USE_GPL_SHOGUN, which
	        when set to OFF will exclude all GPL codes from Shogun [Heiko Strathmann].
	* GSoC 2016 project of Saurabh Mahindre: Major efficiency improvements for KMeans, LARS, Random Forests, Bagging, KNN.
	* Features:
	    - Add new Shogun cookbook for documentation and testing across all 
	      target languages [Heiko Strathmann, Sergey Lisitsyn, Esben Sorig, Viktor Gal].
	    - Added option to learn CombinedKernel weights with GP approximate inference [Wu Lin].
	    - LARS now supports 32, 64, and 128 bit floating point numbers [Chris Goldsworthy].
	* Bugfixes:
	    - Fix gTest segfaults with GCC >= 6.0.0 [Björn Esser].
	    - Make Java and CSharp install-dir configurable [Björn Esser].
	    - Autogenerate modshogun.rb with correct module-suffix [Björn Esser].
	    - Fix KMeans++ initialization [Saurabh Mahindre].
	* Cleanup, efficiency updates, and API Changes:
	    - Make Eigen3 a hard requirement. Bundle if not found on system. [Heiko Strathmann]
	    - Drop ALGLIB (GPL) dependency in CStatistics and ship CDFLIB (public domain) instead [Heiko Strathmann]
	    - Drop p-value estimation in model-selection [Heiko Strathmann]
	    - Static interfaces have been removed [Viktor Gal]
	    - New base class ShiftInvariantKernel of which GaussianKernel inherits [Rahul De].

2016-02-09 Heiko Strathmann <heiko.strathmann@shogun-toolbox.org>

	* SHOGUN Release version 4.1.0 (libshogun 17.1, data 0.10, parameter 1)
	* This is a new feature and cleanup release:
	* Features:
		- Added GEMPLP for approximate inference to the structured output framework [Jiaolong Xu].
		- Effeciency improvements of the FITC framework for GP inference (FITC_Laplce, FITC, VarDTC) [Wu Lin].
		- Added optimisation of inducing variables in sparse GP inference [Wu Lin].
		- Added optimisation methods for GP inference (Newton, Cholesky, LBFGS, ...) [Wu Lin].
		- Added Automatic Relevance Determination (ARD) kernel functionality for variational GP inference [Wu Lin].
		- Updated Notebook for variational GP inference [Wu Lin].
		- New framework for stochastic optimisation (l1/2 loss, mirror descent, proximal gradients, adagrad, SVRG, RMSProp, adadelta, ...) [Wu Lin].
		- New Shogun meta-language for automatically generating code listings in all target languages [Esben Sörig].
		- Added periodic kernel [Esben Sörig].
		- Add gradient output functionality in Neural Nets [Sanuj Sharma].
	* Bugfixes:
		- Fixes for java_modular build using OpenJDK [Björn Esser].
		- Catch uncaught exceptions in Neural Net code [Khaled Nasr].
		- Fix build of modular interfaces with SWIG 3.0.5 on MacOSX [Björn Esser].
		- Fix segfaults when calling delete[] twice on SGMatrix-instances [Björn Esser].
		- Fix for building with full-hardening-(CXX|LD)FLAGS [Björn Esser].
		- Patch SWIG to fix a problem with SWIG and Python >= 3.5 [Björn Esser].
		- Add modshogun.rb: make sure narray is loaded before modshogun.so [Björn Esser].
		- set working-dir properly when running R (#2654) [Björn Esser].
	* Cleanup, efficiency updates, and API Changes:
		- Added GPU based dot-products to linalg [Rahul De].
		- Added scale methods to linalg [Rahul De].
		- Added element wise products to linalg [Rahul De].
		- Added element-wise unary operators in linalg [Rahul De].
		- Dropped parameter migration framework [Heiko Strathmann].
		- Disabled Python integration tests by default [Sergey Lisitsyn, Heiko Strathmann].

2015-01-26 Soeren Sonnenburg <sonne@debian.org>

	* SHOGUN Release version 4.0.0 (libshogun 17.0, data 0.9, parameter 1)
	* This release features the work of our 8 GSoC 2014 students [student; mentors]:
	    - OpenCV Integration and Computer Vision Applications [Abhijeet Kislay; Kevin Hughes]
	    - Large-Scale Multi-Label Classification [Abinash Panda; Thoralf Klein]
	    - Large-scale structured prediction with approximate inference [Jiaolong Xu; Shell Hu]
	    - Essential Deep Learning Modules [Khaled Nasr; Sergey Lisitsyn, Theofanis Karaletsos]
	    - Fundamental Machine Learning: decision trees, kernel density estimation [Parijat Mazumdar ; Fernando Iglesias]
	    - Shogun Missionary & Shogun in Education [Saurabh Mahindre; Heiko Strathmann]
	    - Testing and Measuring Variable Interactions With Kernels [Soumyajit De; Dino Sejdinovic, Heiko Strathmann]
	    - Variational Learning for Gaussian Processes [Wu Lin; Heiko Strathmann, Emtiyaz Khan]
	* This release also contains several cleanups and bugfixes:
	* Features:
		- New Shogun project description [Heiko Strathmann]
		- ID3 algorithm for decision tree learning [Parijat Mazumdar]
		- New modes for PCA matrix factorizations: SVD & EVD, in-place or reallocating [Parijat Mazumdar]
		- Add Neural Networks with linear, logistic and softmax neurons [Khaled Nasr]
		- Add kernel multiclass strategy examples in multiclass notebook [Saurabh Mahindre]
		- Add decision trees notebook containing examples for ID3 algorithm [Parijat Mazumdar]
		- Add sudoku recognizer ipython notebook [Alejandro Hernandez]
		- Add in-place subsets on features, labels, and custom kernels [Heiko Strathmann]
		- Add Principal Component Analysis notebook [Abhijeet Kislay]
		- Add Multiple Kernel Learning notebook [Saurabh Mahindre]
		- Add Multi-Label classes to enable Multi-Label classification [Thoralf Klein]
		- Add rectified linear neurons, dropout and max-norm regularization to neural networks [Khaled Nasr]
		- Add C4.5 algorithm for multiclass classification using decision trees [Parijat Mazumdar]
		- Add support for arbitrary acyclic graph-structured neural networks [Khaled Nasr]
		- Add CART algorithm for classification and regression using decision trees [Parijat Mazumdar]
		- Add CHAID algorithm for multiclass classification and regression using decision trees [Parijat Mazumdar]
		- Add Convolutional Neural Networks [Khaled Nasr]
		- Add Random Forests algorithm for ensemble learning using CART [Parijat Mazumdar]
		- Add Restricted Botlzmann Machines [Khaled Nasr]
		- Add Stochastic Gradient Boosting algorithm for ensemble learning [Parijat Mazumdar]
		- Add Deep contractive and denoising autoencoders [Khaled Nasr]
		- Add Deep belief networks [Khaled Nasr]
	* Bugfixes:
		- Fix reference counting bugs in CList when reference counting is on [Heiko Strathmann, Thoralf Klein, lambday]
		- Fix memory problem in PCA::apply_to_feature_matrix [Parijat Mazumdar]
		- Fix crash in LeastAngleRegression for the case D greater than N [Parijat Mazumdar]
		- Fix memory violations in bundle method solvers [Thoralf Klein]
		- Fix fail in library_mldatahdf5.cpp example when http://mldata.org is not working properly [Parijat Mazumdar]
		- Fix memory leaks in Vowpal Wabbit, LibSVMFile and KernelPCA [Thoralf Klein]
		- Fix memory and control flow issues discovered by Coverity [Thoralf Klein]
		- Fix R modular interface SWIG typemap (Requires SWIG >= 2.0.5) [Matt Huska]
	* Cleanup and API Changes:
		- PCA now depends on Eigen3 instead of LAPACK [Parijat Mazumdar]
		- Removing redundant and fixing implicit imports [Thoralf Klein]
		- Hide many methods from SWIG, reducing compile memory by 500MiB [Heiko Strathmann, Fernando Iglesias, Thoralf Klein]
		- Drop empty generalised HMM [Fernando Iglesias]
		- Drop unused math operations in SGVector and move randperm to CMath, making SGVector more lightweight  [Fernando Iglesias]

2014-02-17 Soeren Sonnenburg <sonne@debian.org>

	* SHOGUN Release version 3.2.0 (libshogun 16.0, data 0.8, parameter 1)
	* This release also contains several cleanups and bugfixes:
	* Features:
		- Fully support python3 now
		- Add mini-batch k-means [Parijat Mazumdar]
		- Add k-means++ [Parijat Mazumdar]
		- Add sub-sequence string kernel [lambday]
	* Bugfixes:
		- Compile fixes for upcoming swig3.0
		- Speedup for gaussian process' apply()
		- Improve unit / integration test checks
		- libbmrm uninitialized memory reads [Thoralf Klein]
		- libocas uninitialized memory reads
		- Octave 3.8 compile fixes [Orion Poplawski]
		- Fix java modular compile error [Bjoern Esser]
	* Cleanup and API Changes:
		- None

2014-01-06 Soeren Sonnenburg <sonne@debian.org>

	* SHOGUN Release version 3.1.1 (libshogun 15.1, data 0.7, parameter 1)
	* This is a bugfix release:
	* Bugfixes:
		- Fix compile error occurring with CXX0X
		- Bump data version to required version

2014-01-05 Soeren Sonnenburg <sonne@debian.org>

	* SHOGUN Release version 3.1.0 (libshogun 15.0, data 0.6, parameter 1)
	* This release also contains several cleanups and bugfixes:
	* Features:
		- Add option to set k-means cluster centers [Parijat Mazumdar]
		- Add leave one out crossvalidation scheme [Saurabh Mahindre]
		- Add multiclass ipython notebook tutorials [Chiyuan Zhang]
		- Add learning of StreamingSparseFeatures in OnlineLibLinear [Thoralf Klein]
	* Bugfixes:
		- Decrease memory footprint of SGObject [Thoralf Klein]
		- Fix protobuf detection
		- Fix doxygen files and various doxygen errors
		- Fix compile error with directors
		- Fix memory leak in modular interfaces and apply*()
		- Fix leak in KNN::store_model_features
		- Notebook fixes
		- Allow custom kernel matrices of size 2^31-1 x 2^31-1 [Koen van de Sande]
		- Fix Protobuf cmake detection
		- Fix LabelsFactory methods' object ownership in SWIG interfaces with the %newobject directive.
	* Cleanup and API Changes:
		- Introduce slim SGRefObject for refcounted objects as base class of
		  SGObject [Thoralf Klein]

2013-10-28 Soeren Sonnenburg <sonne@debian.org>

	* SHOGUN Release version 3.0.0 (libshogun 14.0, data 0.6, parameter 1)
	* This release features 8 successful Google Summer of Code projects and
	  it is the result of an incredible effort by our students. All projects come with
	  very cool ipython-notebooks that contain background, code examples and
	  visualizations. These can be found on our webpage!

	  The projects are:
	  - Gaussian Processes for binary classification [Roman Votjakov]
	  - Sampling log-determinants for large sparse matrices [Soumyajit De]
	  - Metric Learning via LMNN [Fernando Iglesias]
	  - Independent Component Analysis (ICA) [Kevin Hughes]
	  - Hashing Feature Framework [Evangelos Anagnostopoulos]
	  - Structured Output Learning [Hu Shell]
	  - A web-demo framework [Liu Zhengyang]

	  Other important changes are the change of our build-system to cmake and
	  the addition of clone/equals methods to our base-class. In addition, you
	  get the usual ton of bugfixes, new unit-tests, and new mini-features.
	* Features:
		- In addition, the following features have been added:
		- Added method to importance sample the (true) marginal likelihood of a
		  Gaussian Process using a posterior approximation.
		- Added a new class for classical probability distribution that can be
		  sampled and whose log-pdf can be evaluated. Added the multivariate
		  Gaussian with various numerical flavours.
		- Cross-validation framework works now with Gaussian Processes
		- Added nu-SVR for LibSVR class
		- Modelselection is now supported for parameters of sub-kernels of
		  combined kernels in the MKL context. Thanks to Evangelos Anagnostopoulos
		- Probability output for multi-class SVMs is now supported using various
		  heuristics. Thanks to Shell Xu Hu.
		- Added an "equals" method to all Shogun objects that recursively
		  compares all registered parameters with those of another instance --
		  up to a specified accuracy.
		- Added a "clone" method to all Shogun objects that creates a deep copy
		- Multiclass LDA. Thanks to Kevin Hughes.
		- Added a new datatype, complex128_t, for complex numbers. Math functions,
		  support for SGVector/Matrix, SGSparseVector/Matrix, and serialization
		  with Ascii and Xml files added. [Soumyajit De].
		- Added mini-framework for numerical integration in one variable. Implemented
		  Gauss-Kronrod and Gauss-Hermite quadrature formulas.
		- Changed from configure script to CMake by Viktor Gal.
		- Add C++0x and C++11 cmake detection scripts
		- ND-Array typmap support for python and octave modular.
	* Bugfixes:
		- Fix json serialization.
		- Fixed bugs in FITC inference method that caused wrong posterior results.
		- Fixed bugs in GP Regression that caused negative values for the variances.
		- Fixed two memory errors in the streaming-features framework. [Thoralf Klein]
		- Fixed bug in the Kernel Mean Matching implementation (thanks to Meghana Kshirsagar).
	* Cleanup and API Changes:
		- Switch compile system to cmake
		- SGSparseVector/Matrix are now derived from SGReferenceData and thus refcounted.
		- Move README and INSTALL files to top level directory.
		- Use common RefCount class for ReferencedData and CSGObjects.
		- Rename HMSVMLabels to SequenceLabels
		- Refactored method to fit a sigmoid to SVM scores, now in CStatistics,
		  still called from CBinaryLabels.
		- Use Dynamic arrays to hold preprocessors in features instead of raw pointers.
		- Use Dynamic arrays to hold Features in CombinedFeatures.
		- Use Dynamic arrays to hold Kernels in CombinedKernels/ProductKernels.
		- Use Eigen3 for GPs, LDA

2013-03-17 Soeren Sonnenburg <sonne@debian.org>

	* SHOGUN Release version 2.1.0 (libshogun 13.0, data 0.5, parameter 1)
	* This release also contains several enhancements, cleanups and bugfixes:
	* Features:
		- Linear Time MMD two-sample test now works on streaming-features, which
		  allows to perform tests on infinite amounts of data. A block size may
		  be specified for fast processing. The below features were also added.
		  By Heiko Strathmann.
		- It is now possible to ask streaming features to produce an instance
		  of streamed features that are stored in memory and returned as a
		  CFeatures* object of corresponding type. See
		  CStreamingFeatures::get_streamed_features().
		- New concept of artificial data generator classes: Based on streaming
		  features. First implemented instances are CMeanShiftDataGenerator and
		  CGaussianBlobsDataGenerator.
		  Use above new concepts to get non-streaming data if desired.
		- Accelerated projected gradient multiclass logistic regression classifier
		  by Sergey Lisitsyn.
		- New CCSOSVM based structured output solver by Viktor Gal
		- A collection of kernel selection methods for MMD-based kernel two-
		  sample tests, including optimal kernel choice for single and combined
		  kernels for the linear time MMD. This finishes the kernel MMD framework
		  and also comes with new, more illustrative examples and tests.
		  By Heiko Strathmann.
		- Alpha version of Perl modular interface developed by Christian Montanari.
		- New framework for unit-tests based on googletest and googlemock by
		  Viktor Gal. A (growing) number of unit-tests from now on ensures basic
		  funcionality of our framework. Since the examples do not have to take
		  this role anymore, they should become more ilustrative in the future.
		- Changed the core of dimension reduction algorithms to the Tapkee library.
	* Bugfixes:
		- Fix for shallow copy of gaussian kernel by Matt Aasted.
		- Fixed a bug when using StringFeatures along with kernel machines in
		  cross-validation which cause an assertion error. Thanks to Eric (yoo)!
		- Fix for 3-class case training of MulticlassLibSVM reported by Arya Iranmehr
		  that was suggested by Oksana Bayda.
		- Fix for wrong Spectrum mismatch RBF construction in static interfaces reported
		  by Nona Kermani.
		- Fix for wrong include in SGMatrix causing build fail on Mac OS X
		  (thanks to @bianjiang).
		- Fixed a bug that caused kernel machines to return non-sense when using
          custom kernel matrices with subsets attached to them.
		- Fix for parameter dictionary creationg causing dereferencing null pointers
		  with gaussian processes parameter selection.
		- Fixed a bug in exact GP regression that caused wrong results.
		- Fixed a bug in exact GP regression that produced memory errors/crashes.
		- Fix for a bug with static interfaces causing all outputs to be
		  -1/+1 instead of real scores (reported by Kamikawa Masahisa).
	* Cleanup and API Changes:
		- SGStringList is now based on SGReferencedData.
		- "confidences" in context of CLabel and subclasses are now "values".
		- CLinearTimeMMD constructor changes, only streaming features allowed.
		- CDataGenerator will soon be removed and replaced by new streaming-
		  based classes.
		- SGVector, SGMatrix, SGSparseVector, SGSparseVector, SGSparseMatrix
		  refactoring: Now contains load/save routines, relevant functions from
		  CMath, and implementations went to .cpp file.

2012-09-01 Soeren Sonnenburg <sonne@debian.org>

	* SHOGUN Release version 2.0.0 (libshogun 12.0, data 0.4, parameter 1)
	* This release also contains several enhancements, cleanups and bugfixes:
	* Features:
		- This release contains first release of Efficient Dimensionality Reduction Toolkit (EDRT).
		- Support for new SWIG -builtin python interface feature (SWIG 2.0.4 is required now).
		- EDRT algorithms are now available using static interfaces such as matlab and octave.
		- Jensen-Shannon kernel and Homogeneous kernel map preprocessor (thanks to Viktor Gal).
		- New 'multiclass' module for multiclass classification algorithms, generic linear
		  and kernel multiclass machines, multiclass LibLinear and OCAS wrappers,
		  new rejection schemes concept by Sergey Lisitsyn.
		- Various multitask learning algorithms including L1/Lq multitask group lasso logistic regression
		  and least squares regression, L1/L2 multitask tree guided group lasso logistic regression
		  and least squares regression, trace norm regularized multitask logistic regression, clustered multitask
		  logistic regression and L1/L2 multitask group logistic regression by Sergey Lisitsyn.
		- Group and tree-guided logistic regression for binary and multiclass problems by Sergey Lisitsyn.
		- Mahalanobis distance, QDA, Stochastic Proximity Embedding,
		  generic OvO multiclass machine and CoverTree & KNN integation (thanks to Fernando J. Iglesias Garcia).
		- Structured output learning framework by Fernando J. Iglesias Garcia.
		- Hidden markov support vector machine structured output model by Fernando J. Iglesias Garcia.
		- Implementations of three Bundle method for risk minimization (BMRM) variants by Michal Uricar.
		- Latent SVM framework and latent detector example by Viktor Gal.
		- Gaussian processes framework for parameters selection and gaussian processes regression estimation
		  framework by Jacob Walker.
		- New framework for statistical hypothesis testing and algorithms for kernel-based two-sample and
		  independence tests using MMD and HSIC by Heiko Strathmann.
		- New graphical python modular examples.
		- Standard Cross-Validation splitting for regression problems by Heiko Strathmann
		- New data-locking concept by Heiko Strathmann which allows to tell machines that data
		  is not going to change during training/testing until unlocked.
		  KernelMachines now make use of that by not recomputing kernel matrix in cross-validation.
		- Cross-validation for KernelMachines is now parallelized.
		- Cross-validation is now possible with custom kernels.
		- Features may now have arbritarily many index subsets (of subsets (of subsets (...))).
		- Various clustering measures, Least Angle Regression and new multiclass strategies
		  concept (thanks to Chiyuan Zhang).
		- A bunch of multiclass learning algorithms including the ShareBoost algorithm, ECOC framework,
		  conditional probability tree, balanced conditional probability tree, random conditional probability
		  tree and relaxed tree by Chiyuan Zhang.
		- Python Sparse matrix typemap for octave modular interface (thanks to Evgeniy Andreev).
		- Newton SVM port (thanks to Harshit Syal).
		- Some progress on native windows compilation using
		  cmake and mingw-w64 (thanks to Josh aka jklontz).
		- CMake compilation improvements (thanks to Eric aka yoo).
	* Bugfixes:
		- Fix for bug in the Gaussian Naive Bayes classifier, its domain was
		  changed to log-space.
		- Fix for R_static interface installation (thanks Steve Lianoglou).
		- SVMOcas memsetting and max_train_time bugfix.
		- Various fixes for compile errors with clang.
		- Stratified-cross-validation now used different indices for each run.
	* Cleanup and API Changes:
		- Various code cleanups by Evan Shelhamer
		- Parameter migration framework by Heiko Strathmann. From now on,
		  changes in the shogun objects will not break loading old serialized
		  files anymore

2011-12-01 Soeren Sonnenburg <sonne@debian.org>

	* SHOGUN Release version 1.1.0 (libshogun 11.0, data 0.3, parameter 0)
	* This release contains several enhancements, cleanups and bugfixes:
	* Features:
	   - New dimensionality reduction algorithms:
	     Diffusion Maps, Kernel Locally Linear Embedding,
	     Kernel Local Tangent Space Alignment, Linear Local Tangent Space Alignment,
	     Neighborhood Preserving embedding, Locality Preserving Projections.
	   - Various performance improvements for dimensionality reduction methods (BLAS,
	     alignment formulation of the LLE, ..)
	   - Automatical k determination mode for Locally Linear Embedding dimension
	     reduction method based on reconstruction error.
	   - ARPACK and SUPERLU integration.
	   - Introduce the concept of Converters that can embed (arbitrary) feature
	     types into different feature types.
	   - LibSVM is now pthread-parallelized.
	   - Create modshogun.dll for csharp.
	   - Various new c# examples (thanks Daniel Korn and Ori Cohen).
	   - Dimensionality reduction examples application is introduced
	* Bugfixes:
	   - Octave_static and octave_modular examples fix.
	   - Memory leak in custom kernel is now eliminated (thanks Madeleine Seeland for reporting).
	   - Fix for linear machine set_w method (thanks Brian Cheung for reporting).
	   - DotFeatures fix for assert bug.
	   - FibonacciHeap memory leak fix.
	   - Fix for Java modular interface typemapping bug.
	   - Fix errors uncovered by LLVM / clang++.
	   - Fix for configure on Darwin-x86_64 (thanks Peter Romov for patch).
	   - Improve lua / ruby detection.
	   - Fix configure / compilation under osx and cygwin for variuos interfaces.
	* Cleanup and API Changes:
	   - Most of the inline functions have been (re)moved to the corresponding
	     .cpp file
	   - Libshogun is now being compiled with sse support for math (if available) but
	     interfaces are now being compiled with -O0 key which drastically reduces compilation time

2011-08-31 Soeren Sonnenburg <sonne@debian.org>

	* SHOGUN Release version 1.0.0 (libshogun 10.0, data 0.2, parameter 0)
	* This release contains major enhancements, cleanups and bugfixes:
	* Features:
	   - Support for new languages: java, c#, ruby, lua in modular interfaces
	     (GSoC project of Baozeng Ding)
	   - Port all examples to the new languages:
	     Ruby examples with example transition tool (thanks to Justin Patera aka serialhex)
	   - Dimensionality reduction (manifold learning) algorithms
	     are now available. In particular: Locally Linear Embedding (LLE), Hessian
	     Locally Linear Embedding (HLLE), Local Tangent Space Alignment (LTSA),
	     Kernel PCA (kPCA), Multidimensional Scaling (MDS, with possible landmark
	     approximation), Isomap (using Fibonacci Heap Dijkstra for shortest paths),
	     Laplacian Eigenmaps
	     (GSoC project of Sergey Lisitsyn)
	   - Various new kernels: TStudentKernel, CircularKernel, WaveKernel,
	     SplineKernel, LogKernel, RationalQuadraticKernel, WaveletKernel,
	     BesselKernel, PowerKernel, ExponentialKernel, CauchyKernel,
	     ANOVAKernel, MultiquadricKernel, SphericalKernel,
	     DistantSegmentsKernel (thanks GSoC students for the contributions!)
	   - Streaming / Online Feature Framework for SimpleFeatures,
	     SparseFeatures, StringFeatures (GSoC project of Shashwat Lal Das)
	   - SGD-QN, Online SGD, Online Liblinear, Online Vowpal Vabit (GSoC
	     project of Shashwat Lal Das)
	   - Model selection framework for arbitrary Machines
	     (GSoC project of Heiko Strathmann)
	   - Gaussian Mixture Models (GSoC project of Alesis Novik)
	   - FibonacciHeap for efficient shortest-path
	     problem solving (thanks to Evgeniy Andreev)
	   - Efficient HashSet (thanks to Evgeniy Andreev)
	   - ARPACK wrapper (dseupd) for symmetric eigenproblems (both
	     generalized and non-generalized),
	     some new LAPACK wrappers (Sergey Lisitsyn)
	   - New Statistics module for various statistics measures (Heiko Strathmann)
	   - Subset support to features (Heiko Strathmann)
	   - Java externalization support (Sergey Lisitsyn)
	   - Support matlab 2011a.
	* Bugfixes:
	   - Fix build failure with ld --as-needed (thanks Matthias Klose for the
			   patch).
	   - Fix initialization error in KRR static interfaces (thanks Maxwell
			   Collins for the patch).
	* Cleanup and API Changes:
	   - Introduce Machine, KernelMachine, LinearMachine, LinearOnlineMachine,
	     DistanceMachine with train() and apply() functions and drop Classifier.
	   - Restructure source code layout: Merge libshogunui and libshogun into
	     src/shogun and move all interfaces into src/shogun. Split up lib into
	     lib, io and mathematics.
	   - Create a single 'modshogun' module resembling the functionality found
	     in libshogun. Now octave_modular and other modular interfaces work reliably.
	   - Introduce SGVector, SGMatrix, SGNDArray, SGStringList for transfering
	     object-pointers and meta-data from/to shogun.
	   - Classes no longer store copies of e.g. matrices, and just pass
	     pointers on set/get operations.
	   - Stop using new[] / delete[] and switch to SG_MALLOC, SG_CALLOC,
	     SG_REALLOC, SG_FREE macros.
	   - Preproc renamed to preprocessor, PCACut renamed to PCA

2010-12-07 Soeren Sonnenburg <sonne@debian.org>

	* SHOGUN Release version 0.10.0 (libshogun 9.0, libshogunui 6.0, data 0.1)
	* This release contains several enhancements, cleanups and bugfixes:
	* Features:
		- Serialization of objects deriving from CSGObject, i.e. all shogun objects
		(SVM, Kernel, Features, Preprocessors, ...) as ASCII, JSON, XML and HDF5
		- Create SVMLightOneClass
		- Add CustomDistance in analogy to custom kernel
		- Add HistogramIntersectionKernel (thanks Koen van de Sande for the patch)
		- Matlab 2010a support
		- SpectrumMismatchRBFKernel modular support (thanks Rob Patro for the patch)
		- Add ZeroMeanCenterKernelNormalizer (thanks Gorden Jemwa for the patch)
		- Swig 2.0 support
	* Bugfixes:
		- Custom Kernels can now be > 4G  (thanks Koen van de Sande for the patch)
		- Set C locale on startup in init_shogun to prevent incompatiblies with
		ascii floats and fprintf
		- Compile fix when reference counting is disabled
		- Fix set_position_weights for wd kernel (reported by Dave duVerle)
		- Fix set_wd_weights for wd kernel.
		- Fix crasher in SVMOcas (reported by Yaroslav)
	* Cleanup and API Changes:
		- Renamed SVM_light/SVR_light to SVMLight etc.
		- Remove C prefix in front of non-serializable class names
		- Drop CSimpleKernel and introduce CDotKernel as its base class. This
		way all dot-product based kernels can be applied on top of DotFeatures
		and only a single implementation for such kernels is needed.

2010-05-31 Soeren Sonnenburg <sonne@debian.org>

	* SHOGUN Release version 0.9.3 (libshogun 8.0, libshogunui 5.0)
	* This release contains several enhancements, cleanups and bugfixes:
	* Features:
		- Experimental lp-norm MCMKL
		- New Kernels: SpectrumRBFKernelRBF, SpectrumMismatchRBFKernel, WeightedDegreeRBFKernel
		- WDK kernel supports amino acids
		- String Features now support append operations (and creation of
		- python-dbg support
		- Allow floats as input for custom kernel (and matrices > 4GB in size)
	* Bugfixes:
		- Static linking fix.
		- Fix sparse linear kernel's add_to_normal
	* Cleanup and API Changes:
		- Remove init() function in Performance Measures
		- Adjust .so suffix for python and use python distutils to figure out
		install paths

2010-03-31 Soeren Sonnenburg <sonne@debian.org>

	* SHOGUN Release version 0.9.2 (libshogun 7.0, libshogunui 4.0)
	* This release contains several enhancements, cleanups and bugfixes:
	* Features:
		- Direct reading and writing of ASCII/Binary files/HDF5 based files.
		- Implemented multi task kernel normalizer.
		- Implement SNP kernel.
		- Implement time limit for libsvm/libsvr.
		- Integrate Elastic Net MKL (thanks Ryoata Tomioka for the patch).
		- Implement Hashed WD Features.
		- Implement Hashed Sparse Poly Features.
		- Integrate liblinear 1.51
		- LibSVM can now be trained with bias disabled.
		- Add functions to set/get global and local io/parallel/... objects.
	* Bugfixes:
		- Fix set_w() for linear classifiers.
		- Static Octave, Python, Cmdline and Modular Python interfaces Compile
		cleanly under Windows/Cygwin again.
		- In static interfaces testing could fail when not directly done after
		training.
	* Cleanup and API Changes:
		- None

2009-11-16 Soeren Sonnenburg <sonne@debian.org>

	* SHOGUN Release version 0.9.1 (libshogun 6.0, libshogunui 3.1)
	* This release contains several enhancements, cleanups and bugfixes:
	* Features:
		- Integrate LaRank.
		- Memory Mapped Features (for data sets that don't fit into memory).
        - Compressor module with compression and decompression support for
        lzo, gzip, bzip2 and lzma.
		- Compressed String Features with on-the-fly decompression
		(CDecompressString preproc).
		- Parallel computation of get_kernel_matrix().
		- One may now prefix all shogun print/outputs with file name and
		line number (obj.io.enable_file_and_line())
		- Chinese Documentation thanks Elpmis Lee.
	* Bugfixes:
		- Fix One class MKL testing in static interfaces.
		- Configure fixes: Let octave not write history on configure; fail
		when cplex is forcefully enabled but not found; add cplex 12 support.
		- Fix a problem with regression and CombinedKernels employing only
		Custom kernels.
	* Cleanup and API Changes:
		- String Features now (like SimpleFeatures) upon get_feature_vector
		require an additional do_free argument and need to be freed using
		free_feature_vector.

2009-10-23 Soeren Sonnenburg <sonne@debian.org>

	* SHOGUN Release version 0.9.0 (libshogun 5.0, libshogunui 3.0)
	* This release contains several cleanups and enhancements:
	* Features:
	    - Implement set_linear_classifier for static interfaces.
		- Implement Polynomial DotFeatures.
		- Implement domain adaptation SVM.
		- Speed up ScatterSVM.
		- Initial implementation for saving and Loading of shogun objects.
		- Examples have been polished/split up into separate files.
		- Documentation and webpage improvements.
	* Bugfixes:
		- Fix one class MKL for static interfaces.
		- Fix performance measures integer overflow.
		- Configure fixes to run under OSX's snow leopard.
		- Compiles and runs under solaris both using suncc and gcc.
	* Cleanup and API Changes:
		- It is no longer necessary to call init_kernel TRAIN/TEST.
		- Removed kernel {load,save}_init.
		- Removed preproc {load,save}_init.
		- Move the mkl code from classifier/svm to classifier/mkl.
		- Removed obsolete mindy support.
		- Rename MCSVM to ScatterSVM
		- Move distributions to distributions/ directory.
		- CClassifier::classify() no longer has a label as argument.
		- Introduce CClassifier::train(CFeatures* ) and classify(CFeatures*)
          for more effective training/testing.
		- Remove unnecessary global symbols.

2009-08-16 Soeren Sonnenburg <sonne@debian.org>

	* SHOGUN Release version 0.8.0 (libshogun 4.0, libshogunui 2.0)
	* This release contains several cleanups, features and bugfixes:
	* Features:
		- Implements new multiclass svm formulation.
		- 1,2 and general q-norm MKL for classification, regression and
		one-class for wrapper and chunking algorithm for arbitrary (dual) SVM
		solvers.
		- Dynamic Programming code is now accessible from python.
		- Implements Regulatory Modules kernel.
		- Documentation updates (Tutorial, improved installation instructions,
				overview about the implemented algorithms).
	* Bugfixes:
		- Correct q-norm MKL for Newton.
		- Upon make install of elwms don't install files into R/octave/python
		if these interfaces were not configured
		- Svm-nu parameter was not set correctly.
		- Fix custom kernel initialization.
		- Correct get_subkernel_weights.
		- Proper Intel core2 compile flags detection
		- Fix number of outputs for KNN.
		- Run tests with proper LD_LIBRARY_PATH set.
		- Fix several memory leaks.
	* Cleanup and API Changes:
		- Rename svm_one_class_nu to svm_nu.
		- Clean up dynamic programming code.
		- Remove commands from_position_list and slide_window and move
		functionallity into set/add_features,
		- Remove now obsolete legacy examples.

2009-05-02 Soeren Sonnenburg <sonne@debian.org>

	* SHOGUN Release version 0.7.3 (libshogun 3.0, libshogunui 1.1)
	* This release contains several bugfixes:
	* Features:
		- Improve libshogun/developer tutorial.
		- Implement convenience function for parallel quicksort.
		- Fasta/fastq file loading for StringFeatures.
	* Bugfixes:
		- get_name function was undefined in Evaluation causing the
		PerformanceMeasures class to be defunct.
		- Workaround bugs in the std template library for math functions.
		- Compiles cleanly under OSX now, thanks to James Kyle.
	* Cleanup and API Changes:
		- Make sure that all destructors are declared virtual.

2009-03-23 Soeren Sonnenburg <sonne@debian.org>

	* SHOGUN Release version 0.7.2 (libshogun 2.0, libshogunui 1.1)
	* This release contains several cleanups and enhancements:
	* Features:
		- Support all data types from python_modular: dense, scipy-sparse
		csc_sparse matrices and strings of type bool, char, (u)int{8,16,32,64},
		float{32,64,96}. In addition, individual vectors/strings can now be
		obtained and even changed.  See examples/python_modular/features_*.py
		for examples.
		- AUC maximization now works with arbitrary kernel SVMs.
		- Documentation updates, many examples have been polished.
		- Slightly speedup Oligo kernel.
	* Bugfixes:
		- Fix reading strings from directory (f.load_from_directory()).
		- Update copyright to 2009.
	* Cleanup and API Changes:
		- Remove {Char,Short,Word,Int,Real}Features and only ever use the
		templated SimpleFeatures.
		- Split up examples in examples/python_modular to separate files.
		- Now use s.set_features(strs) instead of s.set_string_features(strs)
          to set string features.
		- The meaning of the width parameter for the Oligo Kernel changed, the
		OligoKernel has been renamed to OligoStringKernel.

2009-03-08 Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.7.1 (libshogun 1.0, libshogunui 1.0)
	* This release contains several cleanups and bugfixes:
	* Features:
		- configure now detects libshogun/ui installed in /usr/(local/)lib if
		libshogun/ui dirs are removed.
		- Improved documentation (and path and doxygen fixes).
		- Tutorial on how to develop with libshogun and to extend shogun.
		- Added the elwms (eilergendewollmilchsau) interface that is a
		chimera that in one file interfaces to python,octave,r,matlab and
		provides the run_{octave,python,r} command to run code in
		{octave,python,r} from within octave,r,matlab,python transparently
		making variables available to the target interface avoiding file i/o.
		- Implement AttributeFeatures for (attr,value) pairs, trees etc.
	* Bugfixes:
		- fix a crasher occurring with combined kernel and multiple threads.
		- configure now allows building of modular interfaces only.
		- n-dimensional arrays work now in octave.
	* Cleanup and API Changes:
		- Custom Kernel no longer requires features nor initialization, even
		not when used in CombinedKernel (the combined kernel will skip over
		custom kernels on init).

2009-02-20 Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.7.0 (libshogun 0.0, libshogunui 0.0)
	* This release contains major feature enhancements and bugfixes:
		- Implement DotFeatures and CombinedDotFeatures. DotFeatures need
		  to provide dot-product and similar operations (hence the name).
		  This enables training of linear methods with mixed datatypes
		  (sparse and dense and other even the newly implemented string
		  based SpecFeatures and WDFeatures).
		- MKL now does not require CPLEX any longer.
		- Add q-norm MKL support based on internal Newton implementation.
		- Add 1-norm MKL support based on GLPK.
		- Add multiclass MKL support based on the GLPK and the GMNP svm solver.
		- Implement Tensor Product Pair Kernel (TPPK).
		- Support compilation on the iPhone :)
		- Add an option to set wds kernel position weights.
		- Build static libshogun.a for libshogun target.
		- Testsuite can also test the modular R interface, added test for
		  OligoKernel.
		- Ocas and WDOcas can be used with a bias feature now.
		- Update to LibSVM 2.88.
		- Enable parallelized HMM code by default.
	* Cleanup and API Changes:
		- Shogun has been split up into libshogun and the static and modular
		interfaces linking to it.
		- Static interfaces now do proper reference counting.
		- Remove SparseLinearClassifier: LinearClassifier is a drop-in
		  replacement.
		- WDOcas and SVMOcas now have the bias term enabled by default.
	* Bugfixes:
		- Fix regression for COMM* kernels (normalization argument was ignored).
		- Use C99 variadic macros, instead of gcc's own variant.
		- Disable lp_solve, it is not required as we are using GLPK now.
		- Fix HMM training.

2008-11-25 Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.6.7
	* Cleanup:
		- Replace ambigous self-defined data types for char/int/float etc.
		by 'standardized' types.
		- Method classify() in WDSVMOcas now has a default value for its
		  argument.
		- Removed a few stderr debug outputs.
	* Features:
		- Testsuite now covers subSVMs in MultiClassSVMs, static interfaces
		  now support commands GET_NUM_SVMS and GET_SVM for MultiClassSVMs.
	* Bugfixes:
		- Fix for contigous arrays/vectors in interface for Python modular.
		- Fixed improper assignment of labels in constructor of WDSVMOcas
		  leading to segfaults on destruction in (python) modular interface.
		- Fixed a segfault opportunity in MultiClassSVM.

2008-10-11  Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.6.6
	* Bugfixes:
		- Include missing file regression/Regression.h.
		- Fix formula in CosineDistance.

2008-10-10  Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.6.5
	* This release contains several cleanups and bugfixes:
		- Implement KernelNormalizer class with a couple of normalization
		functions that can now be attached to almost any kernel via
		set_normalizer() in the modular and set_kernel_normalization in the
		static interfaces. This fixes a long standing bug in the
		WeightedDegreePositionStringKernel normalization WARNING will break
		compatibility to all previously trained WD-shift kernel models, use
		FIRSTELEMENT / CFirstElementKernelNormalizer for an *approximation* to
		the previous buggy behaviour. Also breaks WordMatchKernel as for this
		kernel normalization is now enabled by default.
		- The custom kernel no longer requires lhs/rhs features (it will create
				its own dummy features)
		- Linear kernels don't use kernel cache (only slows down things)
		- Integrate the Oligo string-kernel (from Meinecke et.al 2004)
		- Remove use_precompute hack from SVMLight.
		- Add precompute_kernels function to turn kernels appended to a
		combined kernel into CustomKernels (i.e. precomputed ones).
		- Add distances BrayCurtis, ChiSquare, Cosine and Tanimoto.
	* Bugfixes:
		- Support Intel MKL on 32bit archs.
		- Fix compilation when atlas/lapack is not available.

2008-08-15  Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.6.4
	* This release contains major feature enhancements and bugfixes:
		- Implement 2-norm Multiple Kernel Learning.
		- Much extended documentation.
		- Add Gaussian kernel for 32bit floating point features.
		- Testsuite is now available for static interfaces python, octave,
		  matlab and R and modular interface octave.
	* Bugfixes:
		- Tests are now run in the examples/interface directory, with paths set
		to the installation directory.
		- Filter out duplicate signals in signal handler and make sure the
		handler is removed.
		- Fix random number generator initialization.

2008-06-13  Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.6.3
	* This release contains several cleanups and bugfixes:
		- Fail nicely in out of memory situations.
		- Drop R package, now configure; make; make install will work for all
		interfaces.
		- Disable progress output by default. Ocas now uses a progress bar and
		  hence is less verbose.
		- Revised directory structure with /doc, /examples, /src, /testsuite.
		- Add common toy data repository and make all examples from all interfaces
		use it.
		- Add examples for cmdline interface.
		- Dynamically generate a reference documentation for the static interfaces.
		- Syntax highlight commands again.
		- Support for cplex 11.
		- Port MKL examples to R.
		- Merge structure learning branch.
	* Bugfixes:
		- Don't render string if it is not printed in current loglevel anyway
		and throw exceptions for messages with priority ERROR or higher.
		- Compile fix when lapack is not available.
		- Fix when only lapack and blas (but not atlas) are available.
		- Fix bug in batch/linadd occurring for WD kernel of order 1.
		- Check that strings have same length on initing WD kernels.
		- Remove signal handler on Ctrl+C to fix Ctrl+C pressed twice bug.
		- All derived classes now call their parent class on construction.
		- Fix a crasher occuring with SVRLight on multiple threads.

2008-05-15  Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.6.2
		- Experimental support for r-modular thanks to the swig team!
		- All python-modular examples describing the use of kernels,
		classifier, distributions, features, distances, regression and
		preprocessors have been ported to r-modular (requires swig from svn).
		- The 'send_command' legacy is no longer necessary, numbers can be used
		as such and don't have to be given as strings. All examples for
		r,python,octave,matlab have been converted to the new syntax.
		- Resurrected the command line interface. Basic functionionality,
		like training a classifier on strings/real valued (sparse) features
		was restored. Readline completion was added.
		- Documentation updates.
	* Bugfixes:
		- The weighted spectrum kernel is now working again.
		- Fix the testsuite to reliably check methods that use random().
		- Off-by-one bug fix in FixedDegreeStringKernel.
		- Fix reading strings from file, when strings don't have the same length.
		- Fix massive slowdown in modular interfaces for WD based kernels (it
		is 5-30 times faster now).

2008-04-19  Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.6.1
		- Now fully support octave-modular thanks to the swig team!
		- All python-modular examples describing the use of kernels,
		classifier, distributions, features, distances, regression and
		preprocessors have been ported to octave-modular.
		- Minor documentation updates.
		- Unconditionally disable swig director. This reduces wrapper code size
		and compile time and also speeds up calls to virtual functions *a lot*.
		Expect big speed improvements if you were using the python-modular
		interface.
	* Bugfixes:
		- Include missing files in documentation.
		- The 'send_command' legacy is no longer necessary.
		- Improved cmdline help, categorized in topic sg('help', 'topic')

2008-04-12  Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.6.0
	* This release contains several major enhancements:
		- The static R,octave,matlab,python interfaces have been rewritten from
		scratch simplifying future extensions. They now use the same syntax and
		support the same set of shogun commands.
		- Toy examples describing the use of kernels, classifier,
		distributions, features, distances, regression and preprocessors
		for the static python, R, octave and matlab interface have been added.
		- Improved user documentation
		- Support for ACML and Intel MKL
	* New methods:
		- POIMs for python-modular interface
	* Bugfixes:
		- Fixed memory leaks in Classifiers, Kernels, Distributions
		- Fixed severale delete[]/free mismatches
		- Fixed reading and writing of svm light format
		- Enable ctrl-c support in octave

2008-02-19  Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.5.1
	* This release contains minor bugfixes
		- Allow building w/o doxygen
		- Code cleanups
		- Support newer lapack/atlas/blas
	* New methods:
		- Added several performance measures
		- SVMSGD
		- Efficient reading/writing of svmlight format

2008-01-31  Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.5.0
	* This release contains several major enhancements:
		- Full fledged test suite for python-modular interface
		- Toy examples describing the use of kernels, classifier,
		distributions, features, distances, regression and preprocessors
		for the python-modular interface
		- Doxygen generated documentation for python-modular interface
		- Many cleanups to make python-modular interface more consistent
	* New methods:
		- WDSVMOcas
		- Update liblinear to version 1.22
	* Bugfixes:
		- StringFeatures may now directly read DNA strings from a single file
		- Option to quieten progress output
		- Several memory leaks and valgrind errors
		- Fixed rarely ocurring convergence problem in OCAS
		- Division by zero in Chi2Kernel
		- WD kernel now dynamically allocates Tries
		- Matlab clear sg ; sg crasher
		- Salzberg/HistogramWordkernel crasher
		- Fix build dependency generation using gcc -MM
	* Switched license to GPL v3

2007-11-23  Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.4.4
	* This release contains several bugfixes:
		- Memory leak fix in libsvm wrapper
		- Enable error checking in matlab interface
		- Free memory after batch computation
		- Parallel (num_threads>1) bug occurring with batch computation
		- Several python-modular interface cleanups
		- Fix for Chi2 kernel
		- Use gcc now to generate build dependencies
		- Test for existance of log2 (enables building on interix)
		- Python build fix
		- Double free fix for combined kernel (python modular interface)
	* New methods: SVMOcas, GaussianShiftKernel

2007-10-10  Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.4.3
	* This release contains minor bugfixes for the
	weighted spectrum kernel and poims

2007-09-19  Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.4.2
	* This release contains minor bugfixes and improvements
		- fix POIMs
		- compile fix when atlas/lapack is not available
		- minor code cleanup (Tries now use templates)
		- added KMeans and Hierarchical Clustering

2007-09-01  Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.4.1
	* This release contains minor bugfixes and improvements
	* Fixes for:
		- SVMLin
		- python examples
		- R examples
		- cplex 10 compatibility fixes
		- compilation fix when configured with --disable-svm-light
		- sliding window/position list fixes
	* New methods
		- Liblinear
		- Local Alignment Kernel
		- support for transfering StringFeatures of type word to matlab
		- python modular support for custom kernel

2007-07-30  Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.4.0
	* new methods:
		- SubgradientSVM
		- GMNPSVM (multiclass b-SVM)
		- SubgradientLPM
		- CplexLPM
		- LPBoost (for LPM)
		- SVMLin
		- weighted spectrum kernel
	* linadd support for GPDTSVM
	* new commands new_classifier / train_classifier / get_classifier
	* support for sparse features (from matlab)
	* cleaned and added many more examples
	* removed suffixarray code due to license conflicts
	* Matlab R2007a support
	* all string kernels now work on strings (not charfeatures)

2007-03-06  Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.3.2
	* workaround for python-numpy, when long==int==int32, add bool support
	* fix autodetection of atlas/lapack
	* fix uninitialized variables in (GUI)HMM, valgrind errors

2007-02-20  Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.3.1
	* update README
	* fix autodetection of powl() and _SC_NPROCESSORS_ONLN

2007-02-14  Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.3.0

2007-02-13  Soeren Sonnenburg <debian@nn7.de>

	* added vojtechs SVM
	* finished (regularized) LDA
	* conservational weights in WD kernel
	* added mikios kernel ridge regression (KRR)
	* many fixes in python swig interface
	* build fixes for archs that don't have powl()
	* much improved build system
	* updated coding conventions (though still in a flux)
	* enable warnings for shadowed variables
	* lots of build fixes

2006-12-05  Soeren Sonnenburg <debian@nn7.de>

	* SHOGUN Release version 0.2.1

2006-10-13  Soeren Sonnenburg <Soeren.Sonnenburg@first.fraunhofer.de>

	* swig python interface (works w/ multiple svms etc etc)

2006-10-09  Soeren Sonnenburg <Soeren.Sonnenburg@first.fraunhofer.de>

	* some autodetection magic in ./configure
	* fixed a serious bug occuring with shrinking & SVM light (target epsilon
			was not achieved as we erreanously terminated optimization)
	* fixed a serious bug when using charfeatures (or strings) w/ mxGetString
	in matlab interface (the mxGetString function has the undocumented
			`feature' of returning locale dependent results!)
	* new command use_shrinking 0/1
	* new svm classifier SVM LIBSVM_ONECLASS
	* new function get_WD_scoring
	* make much more use of templates, i.e. remove all the
	{Real,Char,Word,Byte,*}Kernel.* files

2006-09-11  Soeren Sonnenburg <Soeren.Sonnenburg@first.fraunhofer.de>

	* incorporated MINDY support
	* new alphabet class, all string features now have a defined
	alphabet plus mapping function
	* RAW (i.e. 8bit) alphabet added
	* fixes for CommStringUlongKernel (was buggy when strings have different
			lengths)
	* new get_WD_scoring function
	* compile fixes for octave and matlab on osx
	* configure now scans a number of variants to detect include and library paths
	* configure obeys INCLUDES LIBS environment variables and optional
	  paths specified by --libraries --includes
	* updated copyright infos
	* updated license infos

2006-06-30  Soeren Sonnenburg <Soeren.Sonnenburg@first.fraunhofer.de>

	* SHOGUN Release 0.1.2
	* compile fixes for R on MaxOSX
	* some compile fixes for cygwin/WIN32
	* Weighted Degree/Weighted Degree Shift kernel speedups & fixes
	* python build fixes
	* initial *workin* swig support
	* entropy example

2006-06-15  Soeren Sonnenburg <Soeren.Sonnenburg@first.fraunhofer.de>

	* SHOGUN Release version 0.1-pre1