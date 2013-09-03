#
# Copyright (C) 2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=emlog
PKG_RELEASE:=1
PKG_REV:=dac60f9e3cebabe715cc3d3e8af082ac1f3caf44
PKG_VERSION:=$(PKG_REV)

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://gitorious.org/~astifter/misc-kernel/astifters-emlog.git
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define KernelPackage/emlog
  SUBMENU:=Other modules
  TITLE:=Embedded log support
  FILES:=$(PKG_BUILD_DIR)/emlog.ko
endef

define KernelPackage/emlog/description
 Kernel module that implements an embedded-system log-device
endef

define Build/Compile
	$(MAKE) -C $(LINUX_DIR) \
		ARCH="$(LINUX_KARCH)" \
		CROSS_COMPILE="$(TARGET_CROSS)" \
		SUBDIRS="$(PKG_BUILD_DIR)" \
		modules
endef

$(eval $(call KernelPackage,emlog))

