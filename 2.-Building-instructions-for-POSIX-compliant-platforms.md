## Pre-requisites

- Recommended compiler: [g++](https://gcc.gnu.org/) version 5.0 or later
(for good C++11 support)
- [Eigen 3](http://eigen.tuxfamily.org) linear algebra library. I assume here that 
the library is installed in `$HOME/eigen`, although the location may vary, e.g. if 
the libary was installed using a package manager.
- Quantum++ library located in `$HOME/qpp`

## Optional

- [CMake](http://www.cmake.org/) version 3.0 or later, highly recommended
- [MATLAB](http://www.mathworks.com/products/matlab/) compiler include header 
files:
`/Applications/MATLAB_R2016a.app/extern/include`
- [MATLAB](http://www.mathworks.com/products/matlab/) compiler shared library 
files:
`/Applications/MATLAB_R2016a.app/bin/maci64`

## Building using [CMake](http://www.cmake.org/) (version 3.0 or later)

The current version of the repository has a `./CMakeLists.txt` configuration 
file for building examples using [CMake](http://www.cmake.org/). 
To build an example using [CMake](http://www.cmake.org/), 
I recommend an out-of-source build, i.e., from the root of the project 
(where `./include` is located), type

    mkdir ./build
    cd ./build
    cmake ..
    make

The commands above build the release version (default) executable `qpp`, 
from the source file `./examples/minimal.cpp`,
without [MATLAB](http://www.mathworks.com/products/matlab/) support (default), 
inside the directory `./build`. 

If the location of [Eigen 3](http://eigen.tuxfamily.org) is not detected
automatically by the [CMake](http://www.cmake.org/) build script, 
then the build script will fail (with an error message). In this case 
the location of [Eigen 3](http://eigen.tuxfamily.org) needs to be specified
manually in the [CMake](http://www.cmake.org/) build command line by passing
the `-DEIGEN3_INCLUDE_DIR=path_to_eigen3` flag, e.g.

    cmake .. -DEIGEN3_INCLUDE_DIR=/usr/local/eigen3

To build a different configuration, 
e.g. the debug version with [MATLAB](http://www.mathworks.com/products/matlab/)
support, type from the root of the project

    cd ./build
    rm -rf *
    cmake -DCMAKE_BUILD_TYPE=Debug -DWITH_MATLAB=ON ..
    make
    
Or, to disable [OpenMP](http://openmp.org/) support (enabled by default), type
   
    cd ./build
    rm -rf *
    cmake -DWITH_OPENMP=OFF ..
    make

To change the name of the example file or the location of 
[MATLAB](http://www.mathworks.com/products/matlab/) installation, 
edit the `./CMakeLists.txt` file. Inspect also `./CMakeLists.txt` 
for additional fine-tuning options. Do not forget to clean the `./build` 
directory before a fresh build!

## Building without an automatic build system

- Example file: `$HOME/qpp/examples/minimal.cpp`
- Output executable: `$HOME/qpp/examples/minimal`
- You must run the commands below from inside the directory 
`$HOME/qpp/examples` 

### Release version (without [MATLAB](http://www.mathworks.com/products/matlab/) support) 

	g++ -pedantic -std=c++11 -Wall -Wextra -Weffc++ -fopenmp \
         -O3 -DNDEBUG -DEIGEN_NO_DEBUG \
         -isystem $HOME/eigen -I $HOME/qpp/include \
         minimal.cpp -o minimal

### Debug version (without [MATLAB](http://www.mathworks.com/products/matlab/) support)

	g++ -pedantic -std=c++11 -Wall -Wextra -Weffc++ -fopenmp \
         -g3 -DDEBUG \
         -isystem $HOME/eigen -I $HOME/qpp/include \
          minimal.cpp -o minimal

### Release version (with [MATLAB](http://www.mathworks.com/products/matlab/) support)

	g++ -pedantic -std=c++11 -Wall -Wextra -Weffc++ -fopenmp \
         -O3 -DNDEBUG -DEIGEN_NO_DEBUG \
         -isystem $HOME/eigen -I $HOME/qpp/include \
         -I/Applications/MATLAB_R2016a.app/extern/include \
         -L/Applications/MATLAB_R2016a.app/bin/maci64 \
         -lmx -lmat minimal.cpp -o minimal

### Debug version (with [MATLAB](http://www.mathworks.com/products/matlab/) support)

	g++ -pedantic -std=c++11 -Wall -Wextra -Weffc++ -fopenmp \
         -g3 -DDEBUG \
         -isystem $HOME/eigen -I $HOME/qpp/include \
         -I /Applications/MATLAB_R2016a.app/extern/include \
         -L /Applications/MATLAB_R2016a.app/bin/maci64 \
         -lmx -lmat minimal.cpp -o minimal

## Additional remarks

### Building with [Clang++](http://clang.llvm.org/)
- If you use [clang++](http://clang.llvm.org/) version 3.7 or later (previous versions do not have [OpenMP](http://openmp.org/) support) and want 
to use [OpenMP](http://openmp.org/) (enabled by default in the library), make sure to modify 
`CLANG_LIBOMP` and `CLANG_LIBOMP_INCLUDE` in `CMakeLists.txt` so they point to 
the correct location of the [OpenMP](http://openmp.org/) library, as otherwise 
[clang++](http://clang.llvm.org/) will not find `<omp.h>` and the `libomp` 
shared library. Under Linux, you may need to modify also `-fopenmp=...` flag
as well. As such, I do not recommend using [clang++](http://clang.llvm.org/)
with [OpenMP](http://openmp.org/) due to various platform-dependent issues.

### Building with [clang++](http://clang.llvm.org/) on [OS X/macOS](http://www.apple.com/osx)

- I highly recommend to install [clang++](http://clang.llvm.org/) version 3.7 or later via [macports](https://www.macports.org/). 
- If you enable
[MATLAB](http://www.mathworks.com/products/matlab/) support, make sure that 
the environment variable `DYLD_LIBRARY_PATH` is set to point to the 
[MATLAB](http://www.mathworks.com/products/matlab/) 
compiler library location, see the `run_mac_MATLAB.sh` script. 
Otherwise, you get a runtime error similar to  

    > dyld: Library not loaded: @rpath/libmat.dylib.
    
   * I recommend running via a script, as otherwise setting the 
    `DYLD_LIBRARY_PATH` globally may interfere with 
    [macports](https://www.macports.org/)' [CMake](http://www.cmake.org/) 
    installation (in case you use [CMake](http://www.cmake.org/) from 
    [macports](https://www.macports.org/)). If you use a script, 
    then the environment variable is local to the script and 
    does not interfere with the rest of the system.

   * Example of running script, assumed to be located in the root directory 
    of Quantum++
        
            #!/bin/sh
            
            MATLAB=/Applications/MATLAB_R2016a.app
            export DYLD_LIBRARY_PATH=$DYLD_LIBRARY_PATH:$MATLAB/bin/maci64
            
            ./build/qpp

### Building debug versions with [g++](https://gcc.gnu.org/) on [OS X/macOS](http://www.apple.com/osx)

- If you build a debug version with [g++](https://gcc.gnu.org/) and use 
[gdb](http://www.gnu.org/software/gdb/) to step inside template functions 
you may want to add `-fno-weak` compiler flag. See 
<http://stackoverflow.com/questions/23330641/gnu-gdb-can-not-step-into-template-functions-os-x-mavericks>
for more details about this problem.