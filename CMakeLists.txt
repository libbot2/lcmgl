project(bot2-lcmgl)
cmake_minimum_required(VERSION 3.1)

set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)

add_subdirectory(cmake)

# Find required dependencies
find_package(lcm REQUIRED)
include(${LCM_USE_FILE})

find_package(ZLIB REQUIRED)

# Set up optional language components
macro(lcmgl_option NAME PACKAGE)
  string(TOUPPER LCMGL_ENABLE_${NAME} _option)
  string(TOUPPER ${PACKAGE}_FOUND _with)

  find_package(${PACKAGE})

  option(${_option} "Enable ${NAME} components" ${${_with}})

  if(${_option} AND NOT ${_with})
    find_package(${PACKAGE} REQUIRED)
  endif()

  unset(_option)
  unset(_with)
endmacro()

lcmgl_option(Python PythonInterp)
lcmgl_option(Java Java)

if(LCMGL_ENABLE_JAVA)
  include(UseJava)

  if(NOT TARGET lcm-java)
    message(FATAL_ERROR "lcm-java not found; was LCM built with Java support?")
  endif()
endif()

# Build components
add_subdirectory(lcmtypes)

add_subdirectory(client)
# add_subdirectory(render) TODO
# add_subdirectory(viewer) TODO

if(LCMGL_ENABLE_PYTHON)
  add_subdirectory(python)
endif()

if(LCMGL_ENABLE_JAVA)
  add_subdirectory(java)
endif()
