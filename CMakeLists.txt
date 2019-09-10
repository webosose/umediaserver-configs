# Copyright (c) 2018-2019 LG Electronics, Inc.
#
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
#
# SPDX-License-Identifier: Apache-2.0

cmake_minimum_required(VERSION 2.8.7)
include(webOS/webOS)
webos_modules_init(1 1 1 QUALIFIER RC7)
webos_component(1 0 0)
webos_distro_dep()
webos_distro_variant_dep()

SET(RESOURCE_CONFIG_VERSION "1.0")
SET(CODEC_CONFIG_VERSION "1.0")
set(CONF_PIPELINE_BINARY_PATH "${WEBOS_INSTALL_SBINDIR}")
set(CONF_SCHEMA_PATH "${WEBOS_INSTALL_SYSCONFDIR}/umediaserver")

if (${WEBOS_TARGET_MACHINE} MATCHES "qemux86")
webos_build_configured_file(qemux86/umediaserver_resource_config.txt SYSCONFDIR umediaserver)
elseif ("${WEBOS_TARGET_MACHINE}" STREQUAL "raspberrypi3")
webos_build_configured_file(raspberrypi3/umediaserver_resource_config.txt SYSCONFDIR umediaserver)
webos_build_configured_file(raspberrypi3/device_codec_capability_config.json SYSCONFDIR umediaserver)
elseif ("${WEBOS_TARGET_MACHINE}" STREQUAL "raspberrypi4")
webos_build_configured_file(raspberrypi4/umediaserver_resource_config.txt SYSCONFDIR umediaserver)
webos_build_configured_file(raspberrypi4/device_codec_capability_config.json SYSCONFDIR umediaserver)
else() #desktop implementation
webos_build_configured_file(default/umediaserver_resource_config.txt SYSCONFDIR umediaserver)
endif()
