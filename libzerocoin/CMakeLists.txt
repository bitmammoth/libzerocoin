# Copyright 2013 Corgan Labs
# Copyright 2017 PIVX Developers
# This file is part of the Zerocoin project
# See LICENSE file or http://opensource.org/licenses/MIT for terms

cmake_minimum_required(VERSION 2.8)
project(zerocoin)

# Just add Debug info for Debug builds
if (CMAKE_BUILD_TYPE MATCHES "DEBUG")
  add_definitions(-DZEROCOIN_DEBUG)
endif()

include_directories(
  ${Boost_INCLUDE_DIRS}
  ${OPENSSL_INCLUDE_DIR}
)

# List of libraries to link in
#
list(APPEND zerocoin_libs
  ${Boost_LIBRARIES}
  ${OPENSSL_LIBRARIES}
)

set(ZEROCOIN_HEADERS
  Accumulator.h
  AccumulatorProofOfKnowledge.h
  Coin.h
  CoinSpend.h
  Commitment.h
  Denominations.h
  ParamGeneration.h
  Params.h
  SerialNumberSignatureOfKnowledge.h
  ZerocoinDefines.h
)

#
# List of source files to compile
#
list(APPEND zerocoin_sources
  Accumulator.cpp
  AccumulatorProofOfKnowledge.cpp
  Coin.cpp
  Denominations.cpp
  CoinSpend.cpp
  Commitment.cpp
  ParamGeneration.cpp
  Params.cpp
  SerialNumberSignatureOfKnowledge.cpp
)

add_library(zerocoin ${ZEROCOIN_HEADERS} ${zerocoin_sources})
target_link_libraries(zerocoin ${zerocoin_libs})
set_property(TARGET zerocoin PROPERTY CXX_STANDARD 11)

