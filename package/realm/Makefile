# SPDX-License-Identifier: MIT
#
# Copyright (C) 2026 wukitest

include $(TOPDIR)/rules.mk

PKG_NAME:=realm
PKG_VERSION:=2.9.6
PKG_RELEASE:=1

# The 360 T7 is aarch64 and ImmortalWrt uses musl libc.
PKG_SOURCE:=realm-aarch64-unknown-linux-musl.tar.gz
PKG_SOURCE_URL:=https://github.com/zhboner/realm/releases/download/v$(PKG_VERSION)/
PKG_HASH:=f4c0318dd86854da483dcb7645b4f39cae2cc3f91c688fef969d53220b949488
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKGARCH:=aarch64_cortex-a53

PKG_LICENSE:=MIT
PKG_MAINTAINER:=wukitest

include $(INCLUDE_DIR)/package.mk

define Package/realm
  SECTION:=net
  CATEGORY:=Network
  TITLE:=A high performance network relay tool
  URL:=https://github.com/zhboner/realm
  DEPENDS:=+ca-bundle
endef

define Package/realm/description
  Realm is a high performance network relay tool written in Rust.
endef

define Package/realm/conffiles
/etc/config/realm
/etc/realm/
endef

define Build/Prepare
	$(INSTALL_DIR) $(PKG_BUILD_DIR)
	$(TAR) -xzf $(DL_DIR)/$(PKG_SOURCE) -C $(PKG_BUILD_DIR)
endef

define Build/Compile
endef

define Package/realm/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/realm $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) $(CURDIR)/files/realm.config $(1)/etc/config/realm
	$(INSTALL_DIR) $(1)/etc/realm
	$(INSTALL_CONF) $(CURDIR)/files/realm/config.toml $(1)/etc/realm/config.toml
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) $(CURDIR)/files/realm.init $(1)/etc/init.d/realm
endef

$(eval $(call BuildPackage,realm))
