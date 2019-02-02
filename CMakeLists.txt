cmake_minimum_required(VERSION 3.2)
project(blake2s C)

set(CMAKE_POSITION_INDEPENDENT_CODE TRUE)
set(CMAKE_C_STANDARD 11)    # force std=c11
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS OFF)

include_directories(
  ${CMAKE_SOURCE_DIR}/include
)

add_library(blake2s
  blake2s.c
  )

include(GNUInstallDirs)

install(TARGETS blake2s EXPORT blake2sConfig
  LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
  ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
  RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
  INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
  PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
  FRAMEWORK DESTINATION ${CMAKE_INSTALL_PREFIX}
  )
install(
  DIRECTORY ${CMAKE_SOURCE_DIR}/include/blake2s
  DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)
install(
  EXPORT blake2sConfig
  DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}
)
export(
  TARGETS blake2s
  FILE blake2sConfig.cmake
)

if (TESTING)
  enable_testing()
  add_executable(blake2s_test test_main.c)
  add_test(NAME blake2s_test COMMAND blake2s_test)
  target_link_libraries(blake2s_test blake2s)
endif ()
