set(sources
  lcmgl.c
)

set(install_headers
  lcmgl.h
)

add_library(${PROJECT_NAME}-client ${sources})

target_include_directories(${PROJECT_NAME}-client
  INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
  PRIVATE
  ${ZLIB_INCLUDE_DIRS}
)

target_link_libraries(${PROJECT_NAME}-client
  PUBLIC
  ${PROJECT_NAME}-lcmtypes
  lcm
  PRIVATE
  ${ZLIB_LIBRARIES}
)

install(TARGETS ${PROJECT_NAME}-client
  EXPORT ${PROJECT_NAME}Targets
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib${LIB_SUFFIX}
  ARCHIVE DESTINATION lib${LIB_SUFFIX}
  INCLUDES DESTINATION include/libbot2
)

install(FILES ${install_headers}
  DESTINATION include/libbot2
)
