#############################################################################
#
# Project         _____    __   ____   _      _
#                (  _  )  /__\ (_  _)_| |_  _| |_
#                 )(_)(  /(__)\  )( (_   _)(_   _)
#                (_____)(__)(__)(__)  |_|    |_|
#
#
# Copyright 2018-present, Benedikt-Alexander Mokroß <bam@icognize.de>
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
#############################################################################

include $(TOPDIR)/rules.mk
PKG_NAME:=oatpp-websocket
PKG_VERSION:=1.1.0
PKG_RELEASE:=7
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/oatpp/oatpp-websocket.git
PKG_SOURCE_VERSION:=41a0480fdd4cf8a076c9fbd79959be1156ecb204
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_LICENSE:=APACHE-2.0
CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/oatpp-websocket/Default
	SECTION:=oatpp
	CATEGORY:=Libraries
	SUBMENU:=Oat++
	URL:=https://oatpp.io
	ABI_VERSION:=$(PKG_VERSION)
	MENU:=1
endef

define Package/oatpp-websocket
	$(call Package/oatpp-websocket/Default)
	TITLE:=Oat++-websocket
	DEFAULT:=m
	DEPENDS:=+oatpp
endef

define Package/oatpp-websocket/description
Websocket-module for oat++
endef

define Package/oatpp-websocket/config
	source "$(SOURCE)/Config.in"
endef

CMAKE_OPTIONS= \
	-DBUILD_SHARED_LIBS=$(if $(CONFIG_OATPP_BUILD_TYPE_SHARED),ON,OFF) \
	-DOATPP_BUILD_TESTS=$(if $(CONFIG_OATPP_WEBSOCKET_INSTALL_TEST_BIN),ON,OFF)

OATPP_BUILD_TYPE=$(if $(CONFIG_OATPP_BUILD_TYPE_SHARED),so,a)


define Package/oatpp-websocket/install
	$(INSTALL_DIR) $(1)/usr/lib/oatpp-$(PKG_VERSION)/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/oatpp-$(PKG_VERSION)/liboatpp-websocket.$(OATPP_BUILD_TYPE) $(1)/usr/lib/oatpp-$(PKG_VERSION)/
	$(if $(CONFIG_OATPP_SYMLINK_LIB),$(LN) oatpp-$(PKG_VERSION)/liboatpp-websocket.$(OATPP_BUILD_TYPE) $(1)/usr/lib/liboatpp-websocket.$(OATPP_BUILD_TYPE).$(PKG_VERSION))
	$(if $(CONFIG_OATPP_SYMLINK_LIB),$(LN) oatpp-$(PKG_VERSION)/liboatpp-websocket.$(OATPP_BUILD_TYPE) $(1)/usr/lib/liboatpp-websocket.$(OATPP_BUILD_TYPE))

	$(if $(CONFIG_OATPP_WEBSOCKET_INSTALL_TEST_BIN),$(INSTALL_DIR) $(1)/usr/bin)
	$(if $(CONFIG_OATPP_WEBSOCKET_INSTALL_TEST_BIN),$(INSTALL_BIN) $(PKG_BUILD_DIR)/test/module-tests $(1)/usr/bin/oatppWebsocketTest)
endef

$(eval $(call BuildPackage,oatpp-websocket))
