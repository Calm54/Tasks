**<h4>A</h4>**
To build a C++ library with instrumentation tools like **AddressSanitizer** using CMake, you can follow these steps:

1. Make sure you have the required tools installed: CMake, a C++ compiler (such as GCC or Clang), and the AddressSanitizer (ASan) runtime library.

2. Open the CMakeLists.txt file in your codebase's root directory. This file contains instructions for building your project with CMake.

3. Inside the CMakeLists.txt file, add the following lines to enable AddressSanitizer:
```
cmake
# Enable AddressSanitizer
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fsanitize=address -fno-omit-frame-pointer")
```

These flags instruct the compiler to enable AddressSanitizer and include frame pointers in the generated code.

4. Configure the project using CMake. You can do this by running the following commands in your terminal;
```

mkdir build
cd build
cmake ..
```
The above commands create a separate directory for the build artifacts and invoke CMake to configure the project based on the CMakeLists.txt file.

5. Build the project by running the following command;
```

make
```
CMake will generate the necessary build files based on the CMakeLists.txt instructions, and the compiler will build your project with the AddressSanitizer enabled.

6. Once the build process completes successfully, you can test your library by running the executable or running your test suite.

Please note that the specific steps may vary depending on your project's structure and the CMake configuration you have. Make sure to adapt these steps accordingly.

<h4>B</h4>
To build a C++ library for profiling purposes, specifically with the goal of performing **Profile-Guided Optimization (PGO)**, you can follow these steps using CMake:

1. Ensure you have the necessary tools installed: CMake, a C++ compiler (such as GCC or Clang), and a profiler tool compatible with PGO (e.g., Google Performance Tools).

2. Open the CMakeLists.txt file in your codebase's root directory.

3. Inside the CMakeLists.txt file, add the following lines to enable profiling:
```
cmake
# Enable profiling options
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fprofile-generate")
```


These flags instruct the compiler to enable profiling and generate profiling data during the build.

4. Configure the project using CMake by running the following commands in your terminal;

```

mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Profile ..
```
The `-DCMAKE_BUILD_TYPE=Profile` option specifies the build type as "Profile," which can be used to define specific compiler flags or options for profiling.

5. Build the project by running the following command:
```

make
```
CMake will generate the necessary build files based on the CMakeLists.txt instructions, and the compiler will build your project with profiling enabled.

6. After the build completes, you can run your application or execute the corresponding test suite. The profiling data will be collected during execution.

7. Once you have gathered the profiling data, you need to perform a second build to apply Profile-Guided Optimization. Modify the CMakeLists.txt file as follows:
```
cmake
# Enable profiling options
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fprofile-use")
```
This modification enables the use of the collected profiling data during the build process.

8. Configure and build the project again using CMake:
```

cd build
cmake -DCMAKE_BUILD_TYPE=PGO ..
make
```


CMake will generate the updated build files, incorporating the collected profiling data into the optimization process.

9. The resulting build will be optimized based on the profiled execution, potentially leading to improved performance.
