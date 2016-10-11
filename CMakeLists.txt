project(bot2-lcmgl)
cmake_minimum_required(VERSION 3.1)

include(CMakePackageConfigHelpers)

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

# Set package path for platform
if(WIN32)
  set(CONFIG_INSTALL_DIR CMake)
else()
  set(CONFIG_INSTALL_DIR lib${LIB_SUFFIX}/${PROJECT_NAME}/cmake)
endif()

# Export Java targets (note: must precede configure_package_config_file)
if(LCMGL_ENABLE_JAVA)
  set(LCMGL_INCLUDE_JAVA
    "include(\${CMAKE_CURRENT_LIST_DIR}/${PROJECT_NAME}JavaTargets.cmake)"
  )

  export_jars(
    TARGETS ${PROJECT_NAME}-client-java
    FILE ${PROJECT_BINARY_DIR}/${PROJECT_NAME}JavaTargets.cmake
   )
  install_jar_exports(
    TARGETS ${PROJECT_NAME}-client-java
    FILE ${PROJECT_NAME}JavaTargets.cmake
    DESTINATION ${CONFIG_INSTALL_DIR}
  )
endif()

# Create package configuration file
configure_package_config_file(
  ${PROJECT_SOURCE_DIR}/${PROJECT_NAME}Config.cmake.in
  ${PROJECT_BINARY_DIR}/${PROJECT_NAME}Config.cmake
  INSTALL_DESTINATION ${CONFIG_INSTALL_DIR}
)

# Export targets for build directory
export(TARGETS
  ${PROJECT_NAME}-lcmtypes
  ${PROJECT_NAME}-lcmtypes-cpp
  ${PROJECT_NAME}-client
  FILE ${PROJECT_BINARY_DIR}/${PROJECT_NAME}Targets.cmake
)

# Install package configuration files
install(EXPORT ${PROJECT_NAME}Targets
  DESTINATION ${CONFIG_INSTALL_DIR}
  FILE ${PROJECT_NAME}Targets.cmake
)

install(FILES
  ${PROJECT_BINARY_DIR}/${PROJECT_NAME}Config.cmake
  DESTINATION ${CONFIG_INSTALL_DIR}
)
