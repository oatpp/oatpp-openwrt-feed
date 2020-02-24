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
PKG_NAME:=oatpp-mbedtls
PKG_VERSION:=1.0.0
PKG_RELEASE:=1
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/oatpp/oatpp-mbedtls.git
PKG_SOURCE_VERSION:=d10cb66b3f4f78b2856fc4701f30f425217e01fb
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_LICENSE:=APACHE-2.0
CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/oatpp-mbedtls/Default
	SECTION:=oatpp
	CATEGORY:=Libraries
	SUBMENU:=Oat++
	URL:=https://oatpp.io
	ABI_VERSION:=$(PKG_VERSION)
	MENU:=1
endef

define Package/oatpp-mbedtls
	$(call Package/oatpp-mbedtls/Default)
	TITLE:=Oat++-mbedtls
	DEFAULT:=m
	DEPENDS:=+oatpp +libmbedtls
endef

define Package/oatpp-mbedtls/description
mbedtls-module for oat++
endef

define Package/oatpp-mbedtls/config
	source "$(SOURCE)/Config.in"
endef

CMAKE_OPTIONS= \
	-DBUILD_SHARED_LIBS=$(if $(CONFIG_OATPP_BUILD_TYPE_SHARED),ON,OFF) \
	-DOATPP_BUILD_TESTS=$(if $(CONFIG_OATPP_MBEDTLS_INSTALL_TEST_BIN),ON,OFF) \
	-DMBEDTLS_ROOT_DIR=$(STAGING_DIR)/usr/

OATPP_BUILD_TYPE=$(if $(CONFIG_OATPP_BUILD_TYPE_SHARED),so,a)

define Package/oatpp-mbedtls/install
	$(INSTALL_DIR) $(1)/usr/lib/oatpp-$(PKG_VERSION)/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/oatpp-$(PKG_VERSION)/liboatpp-mbedtls.$(OATPP_BUILD_TYPE) $(1)/usr/lib/oatpp-$(PKG_VERSION)/
	$(if $(CONFIG_OATPP_SYMLINK_LIB),$(LN) oatpp-$(PKG_VERSION)/liboatpp-mbedtls.$(OATPP_BUILD_TYPE) $(1)/usr/lib/liboatpp-mbedtls.$(OATPP_BUILD_TYPE).$(PKG_VERSION))
	$(if $(CONFIG_OATPP_SYMLINK_LIB),$(LN) oatpp-$(PKG_VERSION)/liboatpp-mbedtls.$(OATPP_BUILD_TYPE) $(1)/usr/lib/liboatpp-mbedtls.$(OATPP_BUILD_TYPE))

	$(if $(CONFIG_OATPP_MBEDTLS_INSTALL_TEST_BIN),$(INSTALL_DIR) $(1)/usr/bin)
	$(if $(CONFIG_OATPP_MBEDTLS_INSTALL_TEST_BIN),$(INSTALL_BIN) $(PKG_BUILD_DIR)/test/module-tests $(1)/usr/bin/oatppLibreSSLTest)
endef

$(eval $(call BuildPackage,oatpp-mbedtls))
