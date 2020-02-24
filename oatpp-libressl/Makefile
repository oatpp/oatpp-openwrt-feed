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
PKG_NAME:=oatpp-libressl
PKG_VERSION:=1.0.0
PKG_RELEASE=1
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/oatpp/oatpp-libressl.git
PKG_SOURCE_VERSION:=2cf02b6fd08bb9be29bdbe5188f35f2155c0c843
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_LICENSE:=APACHE-2.0
CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/oatpp-libressl/Default
	SECTION:=oatpp
	CATEGORY:=Libraries
	SUBMENU:=Oat++
	URL:=https://oatpp.io
	ABI_VERSION:=$(PKG_VERSION)
	MENU:=1
endef

define Package/oatpp-libressl
	$(call Package/oatpp-libressl/Default)
	TITLE:=Oat++-libressl
	DEFAULT:=m
	DEPENDS:=+oatpp +libressl
endef

define Package/oatpp-libressl/description
LibreSSL-module for oat++
endef

define Package/oatpp-libressl/config
	source "$(SOURCE)/Config.in"
endef

CMAKE_OPTIONS= \
	-DBUILD_SHARED_LIBS=$(if $(CONFIG_OATPP_BUILD_TYPE_SHARED),ON,OFF) \
	-DOATPP_BUILD_TESTS=$(if $(CONFIG_OATPP_LIBRESSL_INSTALL_TEST_BIN),ON,OFF) \
	-DLIBRESSL_ROOT_DIR=$(STAGING_DIR)/usr/

OATPP_BUILD_TYPE=$(if $(CONFIG_OATPP_BUILD_TYPE_SHARED),so,a)

define Package/oatpp-libressl/install
	$(INSTALL_DIR) $(1)/usr/lib/oatpp-$(PKG_VERSION)/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/oatpp-$(PKG_VERSION)/liboatpp-libressl.$(OATPP_BUILD_TYPE) $(1)/usr/lib/oatpp-$(PKG_VERSION)/
	$(if $(CONFIG_OATPP_SYMLINK_LIB),$(LN) oatpp-$(PKG_VERSION)/liboatpp-libressl.$(OATPP_BUILD_TYPE) $(1)/usr/lib/liboatpp-libressl.$(OATPP_BUILD_TYPE).$(PKG_VERSION))
	$(if $(CONFIG_OATPP_SYMLINK_LIB),$(LN) oatpp-$(PKG_VERSION)/liboatpp-libressl.$(OATPP_BUILD_TYPE) $(1)/usr/lib/liboatpp-libressl.$(OATPP_BUILD_TYPE))


	$(if $(CONFIG_OATPP_LIBRESSL_INSTALL_TEST_BIN),$(INSTALL_DIR) $(1)/usr/bin)
	$(if $(CONFIG_OATPP_LIBRESSL_INSTALL_TEST_BIN),$(INSTALL_BIN) $(PKG_BUILD_DIR)/test/module-tests $(1)/usr/bin/oatppLibreSSLTest)
endef

$(eval $(call BuildPackage,oatpp-libressl))
