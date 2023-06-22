 This project will create a target called IDLtoCpp that will generate the C++ file Functions.cpp from the IDL file Functions.idl. The generated C++ file will then be linked to the target main, which will be the executable that is built. The project also includes a custom target called run that will run the executable main.

```
cmake_minimum_required(VERSION 3.1)
project(IDLtoCpp)
set(CMAKE_CXX_STANDARD 17)
add_executable(IDLtoCpp IDLtoCpp.cpp)

# The IDL file to process
set(IDL_FILE Functions.idl)

# The output C++ file
set(CPP_FILE Functions.cpp)

# The command to run to generate the C++ file
set(IDL_TO_CPP_COMMAND "IDLtoCpp")

# Add a custom command to generate the C++ file
add_custom_command(
  TARGET IDLtoCpp
  COMMAND ${IDL_TO_CPP_COMMAND} ${IDL_FILE} ${CPP_FILE}
  DEPENDS ${IDL_FILE}
  COMMENT "Generating C++ file from IDL file"
)

# Add the generated C++ file to the target
target_sources(IDLtoCpp PRIVATE ${CPP_FILE})

# Build the project
add_executable(main main.cpp)
target_link_libraries(main IDLtoCpp)

# Run the project
add_custom_target(run COMMAND ./main)

# To build the project, run:
bash
mkdir build
cd build
cmake ..
make
```