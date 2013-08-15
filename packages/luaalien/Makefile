#
# Copyright (C) 2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=luaalien
#PKG_VERSION:=0.7.0
PKG_VERSION:=bfab480e407ca70377060575a436b086321a1346
PKG_REV:=bfab480e407ca70377060575a436b086321a1346
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_REV).tar.gz
PKG_SOURCE_URL:=git://github.com/mascarenhas/alien.git
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_REV)
PKG_SOURCE_PROTO:=git

include $(INCLUDE_DIR)/package.mk

define Package/luaalien
  SUBMENU:=Lua
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=LuaAlien
  URL:=http://luaforge.net/projects/alien/
  DEPENDS:=+lua +libffi
endef

define Package/luaalien/description
  Alien is a foreign function interface (FFI) for Lua. An FFI 
  lets Lua code call C functions directly without having to 
  write C "glue", so you can use Alien to write C extensions purely in Lua.
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR); $(AM_TOOL_PATHS) ./bootstrap)
	$(call Build/Configure/Default,)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/ \
		LIBDIR="$(TARGET_LDFLAGS)" \
		LIB_OPTION="-shared $(TARGET_LDFLAGS)" \
		CC="$(TARGET_CC) $(TARGET_CFLAGS) $(TARGET_CPPFLAGS) -std=gnu99" \
		CFLAGS="-fPIC -DLINUX -fno-stack-protector" \
		LD="$(TARGET_CROSS)ld -shared" \
        all
endef


define Package/luaalien/install
	$(INSTALL_DIR) $(1)/usr/lib/lua
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/src/alien.lua $(1)/usr/lib/lua
#	$(INSTALL_DIR) $(1)/usr/lib/lua/alien
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/src/.libs/alien_c.so $(1)/usr/lib/lua
endef

$(eval $(call BuildPackage,luaalien))
