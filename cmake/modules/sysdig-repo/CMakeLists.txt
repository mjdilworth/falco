#
# Copyright (C) 2019 The Falco Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with
# the License. You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the
# specific language governing permissions and limitations under the License.
#
cmake_minimum_required(VERSION 3.5.1)

project(sysdig-repo NONE)

include(ExternalProject)

# The sysdig git reference (branch name, commit hash, or tag)

# To update sysdig version for the next release, change the default below
# In case you want to test against another sysdig version just pass the variable - ie., `cmake -DSYSDIG_VERSION=dev ..`
if(NOT SYSDIG_VERSION)
  set(SYSDIG_VERSION "146a431edf95829ac11bfd9c85ba3ef08789bffe")
  set(SYSDIG_CHECKSUM "SHA256=6e477ac5fe9d3110b870bd4495f01541373a008c375a1934a2d1c46798b6bad6")
endif()

ExternalProject_Add(
  sysdig
  URL "https://github.com/draios/sysdig/archive/${SYSDIG_VERSION}.tar.gz"
  URL_HASH "${SYSDIG_CHECKSUM}"
  CONFIGURE_COMMAND ""
  BUILD_COMMAND ""
  INSTALL_COMMAND ""
  TEST_COMMAND ""
  PATCH_COMMAND patch -p1 -i ${CMAKE_CURRENT_SOURCE_DIR}/patch/libscap.patch)
