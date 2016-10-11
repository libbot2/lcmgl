if(LCMGL_ENABLE_PYTHON)
  set(python_args PYTHON_SOURCES python_install_sources)
endif()
if(LCMGL_ENABLE_JAVA)
  set(java_args JAVA_SOURCES java_sources)
endif()

lcm_wrap_types(
  C_SOURCES c_sources
  C_HEADERS c_install_headers
  CPP_HEADERS cpp_install_headers
  ${python_args}
  ${java_args}
  bot_lcmgl_data_t.lcm
)

lcm_add_library(${PROJECT_NAME}-lcmtypes C ${c_sources} ${c_install_headers})
target_include_directories(${PROJECT_NAME}-lcmtypes INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}>)

lcm_add_library(${PROJECT_NAME}-lcmtypes-cpp CPP ${cpp_install_headers})
target_include_directories(${PROJECT_NAME}-lcmtypes-cpp INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}>)

lcm_install_headers(DESTINATION include/libbot2/lcmtypes
  ${c_install_headers}
  ${cpp_install_headers}
)

install(TARGETS ${PROJECT_NAME}-lcmtypes ${PROJECT_NAME}-lcmtypes-cpp
  EXPORT ${PROJECT_NAME}Targets
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib${LIB_SUFFIX}
  ARCHIVE DESTINATION lib${LIB_SUFFIX}
  INCLUDES DESTINATION include/libbot2/lcmtypes
)

if(LCMGL_ENABLE_PYTHON)
  lcm_install_python(${python_install_sources})
endif()

if(LCMGL_ENABLE_JAVA)
  add_jar(${PROJECT_NAME}-lcmtypes-java
    OUTPUT_NAME ${PROJECT_NAME}-lcmtypes
    INCLUDE_JARS lcm-java
    SOURCES ${java_sources}
  )

  install_jar(${PROJECT_NAME}-lcmtypes-java share/java)
endif()
