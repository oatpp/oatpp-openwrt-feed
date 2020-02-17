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
PKG_NAME:=oatpp-swagger
PKG_VERSION:=1.0.0
PKG_RELEASE=7
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/oatpp/oatpp-swagger.git
PKG_SOURCE_VERSION:=136f09aae1182b0c9172b6d621bca726d6d4e7e2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_LICENSE:=APACHE-2.0
CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/oatpp-swagger/Default
	SECTION:=oatpp
	CATEGORY:=Libraries
	SUBMENU:=Oat++
	URL:=https://oatpp.io
	ABI_VERSION:=$(PKG_VERSION)
	MENU:=1
endef

define Package/oatpp-swagger
	$(call Package/oatpp-swagger/Default)
	TITLE:=Oat++-swagger
	DEFAULT:=m
	DEPENDS:=+oatpp
endef

define Package/oatpp-swagger/description
Swagger-module for oat++
endef

define Package/oatpp-swagger/config
	source "$(SOURCE)/Config.in"
endef

CMAKE_OPTIONS= \
	-DBUILD_SHARED_LIBS=$(if $(CONFIG_OATPP_BUILD_TYPE_SHARED),ON,OFF) \
	-DOATPP_BUILD_TESTS=$(if $(CONFIG_OATPP_SWAGGER_INSTALL_TEST_BIN),ON,OFF)

OATPP_BUILD_TYPE=$(if $(CONFIG_OATPP_BUILD_TYPE_SHARED),so,a)


define Package/oatpp-swagger/install
	$(INSTALL_DIR) $(1)/usr/lib/oatpp-$(PKG_VERSION)/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/oatpp-$(PKG_VERSION)/liboatpp-swagger.$(OATPP_BUILD_TYPE) $(1)/usr/lib/oatpp-$(PKG_VERSION)/
	$(if $(CONFIG_OATPP_SYMLINK_LIB),$(LN) oatpp-$(PKG_VERSION)/liboatpp-swagger.$(OATPP_BUILD_TYPE) $(1)/usr/lib/liboatpp-swagger.$(OATPP_BUILD_TYPE).$(PKG_VERSION))

    $(if $(CONFIG_OATPP_SWAGGER_INSTALL_TEST_BIN),$(INSTALL_DIR) $(1)/usr/bin,)
	$(if $(CONFIG_OATPP_SWAGGER_INSTALL_TEST_BIN),$(INSTALL_BIN) $(PKG_BUILD_DIR)/test/module-tests $(1)/usr/bin/oatppSwaggerTest,)

	$(if $(CONFIG_OATPP_SWAGGER_INSTALL_UI),$(INSTALL_DIR) $(1)/usr/share/oatpp-$(PKG_VERSION)/bin/oatpp-swagger/res,)

	$(if $(CONFIG_OATPP_SWAGGER_INSTALL_UI),$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/include/oatpp-$(PKG_VERSION)/bin/oatpp-swagger/res/*.png $(1)/usr/share/oatpp-$(PKG_VERSION)/bin/oatpp-swagger/res)
	$(if $(CONFIG_OATPP_SWAGGER_INSTALL_UI),$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/include/oatpp-$(PKG_VERSION)/bin/oatpp-swagger/res/*.html $(1)/usr/share/oatpp-$(PKG_VERSION)/bin/oatpp-swagger/res)
	$(if $(CONFIG_OATPP_SWAGGER_INSTALL_UI),$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/include/oatpp-$(PKG_VERSION)/bin/oatpp-swagger/res/*.js $(1)/usr/share/oatpp-$(PKG_VERSION)/bin/oatpp-swagger/res)
	$(if $(CONFIG_OATPP_SWAGGER_INSTALL_UI),$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/include/oatpp-$(PKG_VERSION)/bin/oatpp-swagger/res/*.css $(1)/usr/share/oatpp-$(PKG_VERSION)/bin/oatpp-swagger/res)
endef

$(eval $(call BuildPackage,oatpp-swagger))
