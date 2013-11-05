# @@@LICENSE
#
# Copyright (c) 2007-2013 LG Electronics, Inc.
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
# LICENSE@@@

cmake_minimum_required(VERSION 2.8.7)

project(webos-initscripts NONE)

include(webOS/webOS)
webos_modules_init(1 0 0 QUALIFIER RC4)
webos_component(2 2 0)

webos_machine_impl_dep()

# Not installing control-alt-delete or rc0 here are they are
# already installed on the emulators.

set(configurelist
	files/launch/alignment.conf
	files/launch/bootmisc.conf
	files/launch/finish.conf
	files/launch/hostname.conf
	files/launch/mountall.conf
	files/launch/setup-environment.conf
	files/launch/udev.conf)

foreach (confitem ${configurelist})
	webos_build_configured_file(${confitem} UPSTARTCONFDIR "")
endforeach()

webos_build_configured_file(scripts/public/reboot_ls-hubd_if.sh SBINDIR "")

install(DIRECTORY DESTINATION ${WEBOS_INSTALL_UPSTARTCONFDIR}/finish-poststart.d)
