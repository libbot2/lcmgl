set(sources
  bot_lcmgl/LCMGL.java
)

add_jar(${PROJECT_NAME}-client-java
  OUTPUT_NAME ${PROJECT_NAME}
  INCLUDE_JARS ${PROJECT_NAME}-lcmtypes-java lcm-java
  SOURCES ${sources}
)

install_jar(${PROJECT_NAME}-client-java share/java)
