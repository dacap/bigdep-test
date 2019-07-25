cmake_minimum_required(VERSION 3.12)

set(CMAKE_BUILD_TYPE "Release" CACHE STRING "" FORCE)

# Makes usesmall_with_bigsmall just like usebig
#set(CMAKE_CXX_FLAGS "" CACHE STRING "" FORCE)
#set(CMAKE_EXE_LINKER_FLAGS "" CACHE STRING "" FORCE)

# Makes usesmall_with_bigsmall smaller
set(CMAKE_CXX_FLAGS "" CACHE STRING "" FORCE)
set(CMAKE_EXE_LINKER_FLAGS "-dead_strip" CACHE STRING "" FORCE)

add_library(big big.cpp)
add_library(bigsmall bigsmall.cpp)
add_library(small small.cpp)
add_executable(usebig usebig.cpp)
add_executable(usesmall usesmall.cpp)
add_executable(usesmall_with_bigsmall usesmall.cpp)

target_link_libraries(usebig big)
target_link_libraries(usesmall small)
target_link_libraries(usesmall_with_bigsmall bigsmall)
