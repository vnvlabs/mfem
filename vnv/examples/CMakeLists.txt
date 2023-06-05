
project(MFEMExamples)
cmake_minimum_required(VERSION 3.21)
set(CMAKE_EXPORT_COMPILE_COMMANDS YES)

find_package(MFEM REQUIRED)
find_package(Injection REQUIRED)
add_executable(ex1 ex0.cpp)
target_link_libraries(ex0 PUBLIC MFEM::MFEM)
link_vnv_file(ex0 MFEM_EX0 cpp)

