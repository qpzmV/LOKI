#------------------------------------------------------------------------------
# Top-level CMake file for ut of bcos-framework
# ------------------------------------------------------------------------------
# Copyright (C) 2021 FISCO BCOS.
# SPDX-License-Identifier: Apache-2.0
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
# ------------------------------------------------------------------------------
file(GLOB_RECURSE SOURCES "*.cpp" "*.h" "*.sol")

# cmake settings
set(TEST_BINARY_NAME test-bcos-framework)

add_executable(${TEST_BINARY_NAME} ${SOURCES})
target_include_directories(${TEST_BINARY_NAME} PRIVATE . ${CMAKE_SOURCE_DIR})

find_package(wedpr-crypto CONFIG QUIET REQUIRED)
find_package(Boost CONFIG QUIET REQUIRED serialization unit_test_framework)

target_link_libraries(${TEST_BINARY_NAME} ${UTILITIES_TARGET} Boost::serialization Boost::unit_test_framework)
add_test(NAME test-framework WORKING_DIRECTORY ${CMAKE_RUNTIME_OUTPUT_DIRECTORY} COMMAND ${TEST_BINARY_NAME})