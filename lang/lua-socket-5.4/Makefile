#
# SPDX-FileCopyrightText: (c) 2026 Ring Zero Desenvolvimento de Software LTDA
# SPDX-License-Identifier: GPL-2.0-only
#
# Lua 5.4 binding to LuaSocket
# Based on openwrt/packages lang/luasocket, adapted for Lua 5.4
#

include $(TOPDIR)/rules.mk

PKG_NAME:=lua-socket-5.4
PKG_VERSION:=3.1.0
PKG_RELEASE:=1
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

PKG_SOURCE_URL:=https://github.com/lunarmodules/luasocket.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_MIRROR_HASH:=1ee81f1f5a63d0d14c8c8571e8940604cbf1443c3b18ee7d3d1bac6791f853fc

include $(INCLUDE_DIR)/package.mk

define Package/lua-socket-5.4
	SUBMENU:=Lua
	SECTION:=lang
	CATEGORY:=Languages
	TITLE:=Lua 5.4 socket library
	DEPENDS:=+lua5.4
	URL:=https://github.com/lunarmodules/luasocket
	MAINTAINER:=Ring Zero <dev@ringzero.com.br>
endef

define Package/lua-socket-5.4/description
	LuaSocket is the most comprehensive networking support
	library for the Lua language. It provides easy access to
	TCP, UDP, DNS, SMTP, FTP, HTTP, MIME and much more.
	This package is built for Lua 5.4.
endef

LUA_MODULE_PATH:=/usr/local/lib/lua/5.4
LUA_SHARE_PATH:=/usr/local/share/lua/5.4

define Build/Configure
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/ \
		LIBDIR="$(TARGET_LDFLAGS)" \
		CC="$(TARGET_CC) $(TARGET_CFLAGS) $(TARGET_CPPFLAGS) $(FPIC)" \
		LD="$(TARGET_CROSS)ld -shared" \
		LUAV=5.4 LUAINC_linux_base=$(STAGING_DIR)/usr/include \
		all
endef

define Package/lua-socket-5.4/install
	$(INSTALL_DIR) $(1)$(LUA_SHARE_PATH)
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/src/{ltn12,mime,socket}.lua \
		$(1)$(LUA_SHARE_PATH)/

	$(INSTALL_DIR) $(1)$(LUA_MODULE_PATH)
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/mime-1.0.3.so \
		$(1)$(LUA_MODULE_PATH)/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/socket-3.0.0.so \
		$(1)$(LUA_MODULE_PATH)/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/unix.so \
		$(1)$(LUA_MODULE_PATH)/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/serial.so \
		$(1)$(LUA_MODULE_PATH)/

	$(INSTALL_DIR) $(1)$(LUA_MODULE_PATH)/mime
	ln -sf ../mime-1.0.3.so $(1)$(LUA_MODULE_PATH)/mime/core.so

	$(INSTALL_DIR) $(1)$(LUA_MODULE_PATH)/socket
	ln -sf ../socket-3.0.0.so $(1)$(LUA_MODULE_PATH)/socket/core.so
	ln -sf ../unix.so $(1)$(LUA_MODULE_PATH)/socket/unix.so

	$(INSTALL_DIR) $(1)$(LUA_SHARE_PATH)/socket
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/src/{ftp,http,smtp,tp,url,headers}.lua \
		$(1)$(LUA_SHARE_PATH)/socket/
endef

$(eval $(call BuildPackage,lua-socket-5.4))

