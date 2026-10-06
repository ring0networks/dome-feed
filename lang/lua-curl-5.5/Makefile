#
# SPDX-FileCopyrightText: (c) 2026 Ring Zero Desenvolvimento de Software LTDA
# SPDX-License-Identifier: GPL-2.0-only
#
# Lua 5.5 binding to libcurl (Lua-cURLv3)
# Based on openwrt/packages lang/lua-curl-v3, adapted for Lua 5.5
#

include $(TOPDIR)/rules.mk

PKG_NAME:=lua-curl-5.5
PKG_VERSION:=0.3.13
PKG_RELEASE:=1
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

PKG_SOURCE_URL:=https://github.com/Lua-cURL/Lua-cURLv3.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=9f8b6dba8b5ef1b26309a571ae75cda4034279e5
PKG_MIRROR_HASH:=925a328c8afad3d625c60f23633fba445ea32d82ce20694929822af0bf5520aa

include $(INCLUDE_DIR)/package.mk

define Package/lua-curl-5.5
	SUBMENU:=Lua
	SECTION:=lang
	CATEGORY:=Languages
	TITLE:=Lua 5.5 bindings to libcurl
	DEPENDS:=+libcurl +lua5.5
	URL:=https://github.com/Lua-cURL/Lua-cURLv3
	MAINTAINER:=Ring Zero <dev@ringzero.com.br>
endef

define Package/lua-curl-5.5/description
	Lua 5.5 bindings to libcurl (Lua-cURLv3).
	Provides the lcurl C module and the cURL Lua wrapper library.
endef

LUA_MODULE_PATH:=/usr/local/lib/lua/5.5
LUA_SHARE_PATH:=/usr/local/share/lua/5.5

MAKE_FLAGS += \
	UNAME="Linux" \
	LUA_INC="$(STAGING_DIR)/usr/include/lua5.5" \
	LUA_CMOD="$(LUA_MODULE_PATH)" \
	LUA_LMOD="$(LUA_SHARE_PATH)"

define Package/lua-curl-5.5/install
	$(INSTALL_DIR) $(1)$(LUA_MODULE_PATH)
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lcurl.so $(1)$(LUA_MODULE_PATH)/
	$(INSTALL_DIR) $(1)$(LUA_SHARE_PATH)
	$(CP) $(PKG_BUILD_DIR)/src/lua/* $(1)$(LUA_SHARE_PATH)/
endef

$(eval $(call BuildPackage,lua-curl-5.5))

