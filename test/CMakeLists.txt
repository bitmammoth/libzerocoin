CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

project(tests)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}/..")

add_definitions(-DBOOST_TEST_DYN_LINK)

set(ZERO_SOURCES
  benchmark_zerocoin.cpp
  libzerocoin_tests.cpp
  tutorial_zerocoin.cpp
  )

find_package(Boost COMPONENTS system filesystem unit_test_framework REQUIRED)

include_directories(
	${include_directories} 
  ${Boost_INCLUDE_DIR}
  ${Boost_INCLUDE_DIRS}
	${CMAKE_CURRENT_SOURCE_DIR}/../libzerocoin
	${CMAKE_CURRENT_SOURCE_DIR}
	)

add_executable(zerocoin_unit_tests test_zerocoin.cpp ${ZERO_SOURCES})
IF (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
  target_link_libraries(zerocoin_unit_tests zerocoin coin gmp ${OPENSSL_LIBRARIES} ${Boost_LIBRARIES} ${ANL} miniupnpc pthread)
else()
  target_link_libraries(zerocoin_unit_tests zerocoin coin gmp ${OPENSSL_LIBRARIES} ${Boost_LIBRARIES} ${ANL} pthread)
endif()

set_property(TARGET zerocoin_unit_tests PROPERTY CXX_STANDARD 11)
  



