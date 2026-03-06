#
# SPDX-FileCopyrightText: (c) 2026 Ring Zero Desenvolvimento de Software LTDA
# SPDX-License-Identifier: GPL-2.0-only
#
# Lua 5.4 binding to libcurl (Lua-cURLv3)
# Based on openwrt/packages lang/lua-curl-v3, adapted for Lua 5.4
#

include $(TOPDIR)/rules.mk

PKG_NAME:=lua-curl-5.4
PKG_VERSION:=0.3.13
PKG_RELEASE:=1
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

PKG_SOURCE_URL:=https://github.com/Lua-cURL/Lua-cURLv3.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=9f8b6dba8b5ef1b26309a571ae75cda4034279e5
PKG_MIRROR_HASH:=41f9e418b203fe3bdf256e4a5517ac8dbaf5ab5026b972f603052a0c56dfcfc7

include $(INCLUDE_DIR)/package.mk

define Package/lua-curl-5.4
	SUBMENU:=Lua
	SECTION:=lang
	CATEGORY:=Languages
	TITLE:=Lua 5.4 bindings to libcurl
	DEPENDS:=+libcurl +lua5.4
	URL:=https://github.com/Lua-cURL/Lua-cURLv3
	MAINTAINER:=Ring Zero <dev@ringzero.com.br>
endef

define Package/lua-curl-5.4/description
	Lua 5.4 bindings to libcurl (Lua-cURLv3).
	Provides the lcurl C module and the cURL Lua wrapper library.
endef

LUA_MODULE_PATH:=/usr/local/lib/lua/5.4
LUA_SHARE_PATH:=/usr/local/share/lua/5.4

MAKE_FLAGS += \
	UNAME="Linux" \
	LUA_INC="$(STAGING_DIR)/usr/include/lua5.4" \
	LUA_CMOD="$(LUA_MODULE_PATH)" \
	LUA_LMOD="$(LUA_SHARE_PATH)"

define Package/lua-curl-5.4/install
	$(INSTALL_DIR) $(1)$(LUA_MODULE_PATH)
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lcurl.so $(1)$(LUA_MODULE_PATH)/
	$(INSTALL_DIR) $(1)$(LUA_SHARE_PATH)
	$(CP) $(PKG_BUILD_DIR)/src/lua/* $(1)$(LUA_SHARE_PATH)/
endef

$(eval $(call BuildPackage,lua-curl-5.4))

