# @@@LICENSE
#
# Copyright (c) 2014-2018 LG Electronics, Inc.
#
# Unless otherwise specified or set forth in the NOTICE file, all content,
# including all source code files and documentation files in this repository are:
# Confidential computer software. Valid license from LG required for
# possession, use or copying.
#
# LICENSE@@@

# Default settings used for device. Target-specific overrides are done below.
# If you change a value here, check to see if the overrides below are still necessary.

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
else() #desktop implementation
webos_build_configured_file(default/umediaserver_resource_config.txt SYSCONFDIR umediaserver)
endif()
