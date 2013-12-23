cmake_minimum_required(VERSION 2.8.9)

project(MVCDemo)

# Find includes in corresponding build directories.
set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Instruct CMake to run moc automatically when needed.
set(CMAKE_AUTOMOC ON)

# Find the Qt libraries
find_package(Qt5Core REQUIRED)
find_package(Qt5Gui REQUIRED)
find_package(Qt5OpenGL REQUIRED)

# Dependencies
find_package(GLEW REQUIRED)
find_package(OpenGL REQUIRED)
find_package(CGAL REQUIRED)
# find_package(GLU REQUIRED)
# find_package(GMP REQUIRED)

# CGAL: Wrong rounding: -frounding-math option with GCC
if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
  add_definitions(-frounding-math)
endif()

set(SRC_DIR ${CMAKE_CURRENT_SOURCE_DIR}/src)

set(SOURCES ${SRC_DIR}/glshaders.cpp
            ${SRC_DIR}/glwidget.cpp
            ${SRC_DIR}/main.cpp
            ${SRC_DIR}/mainwindow.cpp
            ${SRC_DIR}/mvcshaders.cpp
            ${SRC_DIR}/MVCCloner.cpp
            ${SRC_DIR}/sourcewidget.cpp
            ${SRC_DIR}/utils.cpp
)

set(HEADERS ${SRC_DIR}/CloningParameters.h
            ${SRC_DIR}/CoordinatesMesh.h
            ${SRC_DIR}/glshaders.h
            ${SRC_DIR}/glwidget.h
            ${SRC_DIR}/mainwindow.h
            ${SRC_DIR}/mvcshaders.h
            ${SRC_DIR}/MVCCloner.h
            ${SRC_DIR}/sourcewidget.h
            ${SRC_DIR}/utils.h
)

# Includes
include_directories(${GLEW_INCLUDE_DIRS} ${GLU_INCLUDE_PATH} ${CGAL_INCLUDE_DIRS})

# Create an executable.
add_executable(${PROJECT_NAME} ${SOURCES} ${HEADERS})

# Use Qt modules.
qt5_use_modules(${PROJECT_NAME} Core Gui OpenGL)

# Link libraries
target_link_libraries(${PROJECT_NAME} ${GLEW_LIBRARIES} ${OPENGL_LIBRARIES} ${CGAL_LIBRARY} gmp)