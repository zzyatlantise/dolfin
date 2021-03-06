cmake_minimum_required(VERSION 3.5.0)

PROJECT(dolfin_pybind11)

find_package(pybind11 REQUIRED CONFIG HINTS ${PYBIND11_DIR} ${PYBIND11_ROOT}
  $ENV{PYBIND11_DIR} $ENV{PYBIND11_ROOT})

find_package(DOLFIN REQUIRED)
include(${DOLFIN_USE_FILE})

# Check for mpi4py
#set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH}
#  ${CMAKE_CURRENT_SOURCE_DIR}/cmake)
#find_package(MPI4PY)

# Create the binding library
pybind11_add_module(cpp SHARED
  src/dolfin.cpp
  src/parameter.cpp
  src/adaptivity.cpp
  src/ale.cpp
  src/common.cpp
  src/fem.cpp
  src/function.cpp
  src/generation.cpp
  src/geometry.cpp
  src/graph.cpp
  src/log.cpp
  src/math.cpp
  src/mesh.cpp
  src/multistage.cpp
  src/io.cpp
  src/la.cpp
  src/nls.cpp
  src/refinement.cpp)

#if (MPI4PY_FOUND)
#  target_include_directories(cpp PRIVATE ${MPI4PY_INCLUDE_DIR})
#  add_definitions(-DHAS_MPI4PY)
#endif()

# Add DOLFIN libraries and other config
target_link_libraries(cpp PRIVATE pybind11::module dolfin)
