set(sources
  bot_lcmgl/LCMGL.java
)

add_jar(bot2-lcmgl-client-java
  OUTPUT_NAME bot2-lcmgl
  INCLUDE_JARS bot2-lcmgl-lcmtypes-java lcm-java
  SOURCES ${sources}
)

install_jar(bot2-lcmgl-client-java share/java)
