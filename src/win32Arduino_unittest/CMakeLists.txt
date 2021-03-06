include_directories(${CMAKE_SOURCE_DIR}/src/win32Arduino)
link_directories(${LIBRARY_OUTPUT_PATH})

include_directories($ENV{GOOGLETEST_HOME}/include)
link_directories($ENV{GOOGLETEST_HOME}/build)

add_executable(win32Arduino_unittest
  demo.cpp
  demo.h
  gtesthelper.cpp
  gtesthelper.h
  main.cpp
  TestGetLastCommand.h
  TestGetLastCommand.cpp
  TestWin32Arduino.h
  TestWin32Arduino.cpp
  TestDemo.h
  TestDemo.cpp )

if (WIN32)
  add_definitions(-D_CRT_SECURE_NO_WARNINGS)

  target_link_libraries(win32Arduino_unittest debug     win32Arduino.lib gtest.lib)
  target_link_libraries(win32Arduino_unittest optimized win32Arduino.lib gtest.lib)
endif()

if (UNIX)
  target_link_libraries(win32Arduino_unittest debug     libwin32Arduino.a libgtest.so)
  target_link_libraries(win32Arduino_unittest optimized libwin32Arduino.a libgtest.so)
endif (UNIX)
