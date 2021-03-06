cmake_minimum_required (VERSION 2.8.12)
project(optflow C Fortran)

set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)

add_compile_options(-O3 -march=native -g -fexceptions -Werror=array-bounds)

include_directories(SOFTWARE)

find_package(BLAS REQUIRED)

add_library(linpack SOFTWARE/dsvdc.f)
target_link_libraries(linpack blas)
target_compile_options(linpack PRIVATE -Wall)

add_executable(flow2ps SOFTWARE/psflow.c)
target_link_libraries(flow2ps m)

add_executable(anandan ANANDAN/anandan.c)
target_link_libraries(anandan m)

add_executable(fleet FLEET/fleet.c)
target_link_libraries(fleet linpack m)

add_executable(horn HORN/horn.c)
target_link_libraries(horn m)

add_executable(lucas LUCAS/lucas.c)
target_link_libraries(lucas m)

add_executable(nagel NAGEL/nagel.c)
target_link_libraries(nagel m)

add_executable(singh SINGH/singh.c)
target_link_libraries(singh linpack)

add_executable(uras URAS/uras.c)
target_link_libraries(uras m)
