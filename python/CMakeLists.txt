set(python_dir python${PYTHON_VERSION_MAJOR}.${PYTHON_VERSION_MINOR})

install(DIRECTORY bot_lcmgl
  DESTINATION lib${LIB_SUFFIX}/${python_dir}/site-packages
  PATTERN "*.py")
