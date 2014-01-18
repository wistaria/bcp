cmake_minimum_required(VERSION 2.8 FATAL_ERROR)
project(bcp NONE)

# find ALPS Library
find_package(ALPS REQUIRED PATHS ${ALPS_ROOT_DIR} $ENV{ALPS_HOME} NO_SYSTEM_ENVIRONMENT_PATH)
message(STATUS "Found ALPS: ${ALPS_ROOT_DIR} (revision: ${ALPS_VERSION})")
include(${ALPS_USE_FILE})

# enable C++ compiler
enable_language(CXX)

# rule for generating 'bcp'
file(GLOB BCP_SOURCES ${ALPS_Boost_ROOT_DIR}/tools/bcp/*.cpp)
foreach(name cpp_main.cpp execution_monitor.cpp debug.cpp)
  list(APPEND BCP_SOURCES ${ALPS_Boost_ROOT_DIR}/libs/test/src/${name})
endforeach(name)
add_executable(bcp ${BCP_SOURCES})
target_link_libraries(bcp ${ALPS_LIBRARIES})
