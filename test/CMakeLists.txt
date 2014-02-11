FILE (GLOB_RECURSE test_SRCS *.cpp *.cxx *.cc *.C *.c *.h *.hpp)
SET (test_LIBS ${Boost_LIBRARIES})
SET (test_BIN ${PROJECT_NAME}-unittests)

INCLUDE_DIRECTORIES("${gmock_SOURCE_DIR}/include"
                    "${gmock_SOURCE_DIR}"
                    "${gtest_SOURCE_DIR}/include"
                    # This directory is needed to build directly from Google
                    # Test sources.
                    "${gtest_SOURCE_DIR}")

INCLUDE_DIRECTORIES("../src")

SET (test_SRCS
  ${test_SRCS}
  # Any extra source files
  )

ADD_EXECUTABLE(${test_BIN} ${test_SRCS})
TARGET_LINK_LIBRARIES(${test_BIN} ${test_LIBS} gtest gtest_main gmock gmock_main)

ADD_CUSTOM_TARGET(check ALL "${MAINFOLDER}/bin/${test_BIN}" DEPENDS ${test_BIN} COMMENT "Executing unit tests..." VERBATIM SOURCES ${test_SRCS})
ADD_CUSTOM_TARGET(test "${MAINFOLDER}/bin/${test_BIN}" DEPENDS ${test_BIN} COMMENT "Executing unit tests..." VERBATIM SOURCES ${test_SRCS})
