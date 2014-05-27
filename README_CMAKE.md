# Build class with CMake

This readme file explains how to build class using [CMake][http://www.cmake.org/ "CMake"] build 
tool. I assume that you have CMake as well as gnu autotools installed in your sysem. I have tested
the following under Ubuntu 14.04, with gcc,clang and icc compilers.

## Compilation

Move to the `class_public` directory and make a build directory inside it. Let's call it `build`.

	$ cd class_public
	$ mkdir build
	
From the build directory, execute the `cmake` command.

	$ cd build
	$ cmake ../
	
If everything goes well the output will be like

	-- The C compiler identification is GNU 4.8.2
	-- Check for working C compiler: /usr/bin/cc
	-- Check for working C compiler: /usr/bin/cc -- works
	-- Detecting C compiler ABI info
	-- Detecting C compiler ABI info - done
	-- Try OpenMP C flag = [-fopenmp]
	-- Performing Test OpenMP_FLAG_DETECTED
	-- Performing Test OpenMP_FLAG_DETECTED - Success
	-- Found OpenMP: -fopenmp  
	-- Configuring done
	-- Generating done
	-- Build files have been written to: /arxiv/source_tree/class_public/build
	
Now use the `make` command to build the library and executable.

	$ make
	
If everything goes well your output will be like

	[  2%] Building C object CMakeFiles/class.dir/tools/growTable.c.o
	[  4%] Building C object CMakeFiles/class.dir/tools/dei_rkck.c.o
	[  6%] Building C object CMakeFiles/class.dir/tools/sparse.c.o
	[  8%] Building C object CMakeFiles/class.dir/tools/evolver_rkck.c.o
	[ 10%] Building C object CMakeFiles/class.dir/tools/evolver_ndf15.c.o
	[ 12%] Building C object CMakeFiles/class.dir/tools/arrays.c.o
	[ 14%] Building C object CMakeFiles/class.dir/tools/parser.c.o
	[ 16%] Building C object CMakeFiles/class.dir/tools/quadrature.c.o
	[ 18%] Building C object CMakeFiles/class.dir/tools/hyperspherical.c.o
	[ 20%] Building C object CMakeFiles/class.dir/tools/common.c.o
	[ 22%] Building C object CMakeFiles/class.dir/source/input.c.o
	[ 25%] Building C object CMakeFiles/class.dir/source/background.c.o
	[ 27%] Building C object CMakeFiles/class.dir/source/thermodynamics.c.o
	[ 29%] Building C object CMakeFiles/class.dir/source/perturbations.c.o
	[ 31%] Building C object CMakeFiles/class.dir/source/primordial.c.o
	[ 33%] Building C object CMakeFiles/class.dir/source/nonlinear.c.o
	[ 35%] Building C object CMakeFiles/class.dir/source/transfer.c.o
	[ 37%] Building C object CMakeFiles/class.dir/source/spectra.c.o
	[ 39%] Building C object CMakeFiles/class.dir/source/lensing.c.o
	[ 41%] Building C object CMakeFiles/class.dir/hyrec/hyrectools.c.o
	[ 43%] Building C object CMakeFiles/class.dir/hyrec/helium.c.o
	[ 45%] Building C object CMakeFiles/class.dir/hyrec/hydrogen.c.o
	[ 47%] Building C object CMakeFiles/class.dir/hyrec/history.c.o
	Linking C static library libclass.a
	[ 47%] Built target class
	[ 50%] Building C object CMakeFiles/class.exe.dir/tools/growTable.c.o
	[ 52%] Building C object CMakeFiles/class.exe.dir/tools/dei_rkck.c.o
	[ 54%] Building C object CMakeFiles/class.exe.dir/tools/sparse.c.o
	[ 56%] Building C object CMakeFiles/class.exe.dir/tools/evolver_rkck.c.o
	[ 58%] Building C object CMakeFiles/class.exe.dir/tools/evolver_ndf15.c.o
	[ 60%] Building C object CMakeFiles/class.exe.dir/tools/arrays.c.o
	[ 62%] Building C object CMakeFiles/class.exe.dir/tools/parser.c.o
	[ 64%] Building C object CMakeFiles/class.exe.dir/tools/quadrature.c.o
	[ 66%] Building C object CMakeFiles/class.exe.dir/tools/hyperspherical.c.o
	[ 68%] Building C object CMakeFiles/class.exe.dir/tools/common.c.o
	[ 70%] Building C object CMakeFiles/class.exe.dir/source/input.c.o
	[ 72%] Building C object CMakeFiles/class.exe.dir/source/background.c.o
	[ 75%] Building C object CMakeFiles/class.exe.dir/source/thermodynamics.c.o
	[ 77%] Building C object CMakeFiles/class.exe.dir/source/perturbations.c.o
	[ 79%] Building C object CMakeFiles/class.exe.dir/source/primordial.c.o
	[ 81%] Building C object CMakeFiles/class.exe.dir/source/nonlinear.c.o
	[ 83%] Building C object CMakeFiles/class.exe.dir/source/transfer.c.o
	[ 85%] Building C object CMakeFiles/class.exe.dir/source/spectra.c.o
	[ 87%] Building C object CMakeFiles/class.exe.dir/source/lensing.c.o
	[ 89%] Building C object CMakeFiles/class.exe.dir/hyrec/hyrectools.c.o
	[ 91%] Building C object CMakeFiles/class.exe.dir/hyrec/helium.c.o
	[ 93%] Building C object CMakeFiles/class.exe.dir/hyrec/hydrogen.c.o
	[ 95%] Building C object CMakeFiles/class.exe.dir/hyrec/history.c.o
	[ 97%] Building C object CMakeFiles/class.exe.dir/source/output.c.o
	[100%] Building C object CMakeFiles/class.exe.dir/main/class.c.o
	Linking C executable class
	[100%] Built target class.exe

You may see some warnings from the compiler in between. These can be safely ignored. Now you will
see that we have built `class` executable and the `libclass.a` in the `build` directory.

	$ ls -la
	drwxrwxr-x  3 sree sree    4096 May 27 11:48 .
	drwxrwxr-x 16 sree sree    4096 May 27 11:47 ..
	-rwxrwxr-x  1 sree sree 1559666 May 27 11:46 class
	-rw-rw-r--  1 sree sree   11294 May 27 11:39 CMakeCache.txt
	drwxrwxr-x  6 sree sree    4096 May 27 11:46 CMakeFiles
	-rw-rw-r--  1 sree sree    1615 May 27 11:39 cmake_install.cmake
	-rw-rw-r--  1 sree sree 1655244 May 27 11:46 libclass.a
	-rw-rw-r--  1 sree sree   31220 May 27 11:39 Makefile

### Build options

You can pass the build type (`RELEASE` or `DEBUG`) as option to the `cmake` command. Let's pass the 
`DEBUG` option as an example. We execute the following commands from the `build` directory.

	$ cmake ../ -DCMAKE_BUILD_TYPE=DEBUG
	$ make
	
Note that by default the `CMAKE_BUILD_TYPE` is set to `RELEASE`.
	
### Changing compilers

If you are using `bash` shell, then we can change the compilers by simply passing the `CC` 
environment variable to the `cmake` as below. Let's say that your compiler is `clang`,

	$ CC=clang cmake ../
	
or you would like to use Intel compilers,

	$ CC=icc cmake ../
	
In other shells such as `csh` or `tcsh` you may need to set the environment variable `CC` by
using `setenv` command.
	
	$ setenv CC icc
	$ cmake ../
	
### Changing the make verbose

You may want to see the what happens when the `make` command is issued. This can be achieved by
turning on the `VERBOSE` option.

	$ make VERBOSE=1
	
### Clean

You can clean targets by 

	$ make clean
	
This will clean all the targets compiled.
	

	
	
	
