project(RigidAlignment)
cmake_minimum_required(VERSION 2.8)

find_package(SlicerExecutionModel REQUIRED)

include(${SlicerExecutionModel_USE_FILE})
include(${GenerateCLP_USE_FILE})
include_directories(Mesh)
include_directories( ${CMAKE_SOURCE_DIR} ${CMAKE_BINARY_DIR} )

generateCLP(RIGID_WRAPPER_SRC wrapper/RigidWrapper.xml)

# MESH library
find_package(MeshLib REQUIRED)
include_directories(${Mesh_INCLUDE_DIRS} ${Mesh_INCLUDE_DIRS}/Util)
link_directories(${Mesh_LIBRARY_DIRS})

set (Registration_SOURCES src/RigidAlignment.cpp)
include_directories(src)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ~/bin)
add_executable(RigidAlignment ${Registration_SOURCES} wrapper/RigidWrapper.cpp ${RIGID_WRAPPER_SRC})
target_link_libraries(RigidAlignment Mesh)
