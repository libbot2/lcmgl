set(sources
  lcmgl.c
)

set(install_headers
  lcmgl.h
)

add_library(bot2-lcmgl-client ${sources})

target_include_directories(bot2-lcmgl-client
  INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
  PRIVATE
  ${ZLIB_INCLUDE_DIRS}
)

target_link_libraries(bot2-lcmgl-client
  PUBLIC
  bot2-lcmgl-lcmtypes
  lcm
  PRIVATE
  ${ZLIB_LIBRARIES}
)

install(TARGETS bot2-lcmgl-client
  EXPORT ${PROJECT_NAME}Targets
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib${LIB_SUFFIX}
  ARCHIVE DESTINATION lib${LIB_SUFFIX}
  INCLUDES DESTINATION include/libbot2
)

install(FILES ${install_headers}
  DESTINATION include/libbot2
)
