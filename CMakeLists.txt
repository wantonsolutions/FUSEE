cmake_minimum_required(VERSION 3.16 FATAL_ERROR)

project(DDCKV LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 20)

find_package(Boost REQUIRED)
add_definitions(-DBOOST_ERROR_CODE_HEADER_ONLY)
add_definitions(-DBOOST_SYSTEM_NO_DEPRECATED)
# add_definitions(-libverbs)

SET(GCC_COVERAGE_LINK_FLAGS "-libverbs -lrdmacm -lpthread -lgcov")
SET( CMAKE_EXE_LINKER_FLAGS  "${CMAKE_EXE_LINKER_FLAGS} ${GCC_COVERAGE_LINK_FLAGS}" )

include_directories(src)
include_directories(/usr/include/infiniband)
set(CMAKE_BUILD_TYPE Release)

add_subdirectory(src)

add_subdirectory(ycsb-test)
add_subdirectory(crash-recover-test)
add_subdirectory(micro-test)

enable_testing()
add_subdirectory(tests)