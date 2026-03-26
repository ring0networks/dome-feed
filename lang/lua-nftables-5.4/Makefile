#
# SPDX-FileCopyrightText: (c) 2026 Ring Zero Desenvolvimento de Software LTDA
# SPDX-License-Identifier: GPL-2.0-only
#
# Lua 5.4 binding to libnftables
#

include $(TOPDIR)/rules.mk

PKG_NAME:=lua-nftables-5.4
PKG_VERSION:=1.0.0
PKG_RELEASE:=1
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

PKG_SOURCE_URL:=https://github.com/ring0networks/luanftables.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=face82c

include $(INCLUDE_DIR)/package.mk

define Package/lua-nftables-5.4
	SUBMENU:=Lua
	SECTION:=lang
	CATEGORY:=Languages
	TITLE:=Lua 5.4 bindings to libnftables
	DEPENDS:=+nftables +lua5.4
	URL:=https://github.com/ring0networks/luanftables
	MAINTAINER:=Ring Zero <dev@ringzero.com.br>
endef

define Package/lua-nftables-5.4/description
	Lua 5.4 bindings to libnftables.
	Provides programmatic access to nftables rule management.
endef

LUA_MODULE_PATH:=/usr/local/lib/lua/5.4

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/ \
		CC="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS) $(FPIC)" \
		LDFLAGS="-shared $(TARGET_LDFLAGS)" \
		LUA_INC="-I$(STAGING_DIR)/usr/include/lua5.4" \
		NFT_INC="" \
		NFT_LIB="-lnftables" \
		LUA_CMOD="$(LUA_MODULE_PATH)" \
		nftables.so
endef

define Package/lua-nftables-5.4/install
	$(INSTALL_DIR) $(1)$(LUA_MODULE_PATH)
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/nftables.so $(1)$(LUA_MODULE_PATH)/
endef

$(eval $(call BuildPackage,lua-nftables-5.4))

