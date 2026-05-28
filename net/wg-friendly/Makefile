# package/wg-friendly/Makefile
include $(TOPDIR)/rules.mk

PKG_NAME:=wg-friendly
PKG_VERSION:=0.1.0
PKG_RELEASE:=2

# OpenWrt lädt den Quellcode automatisch via Git herunter und entpackt ihn nach $(PKG_BUILD_DIR)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com
# Nutze den aktuellsten Commit-Hash oder ein Tag aus dem Upstream-Repo
PKG_SOURCE_VERSION:=main
PKG_MIRROR_HASH:=skip

PKG_MAINTAINER:=g6094199
PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

define Package/wg-friendly
  SECTION:=net
  CATEGORY:=Network
  TITLE:=WireGuard friendly CLI peer names
  DEPENDS:=+wireguard-tools
endef

define Package/wg-friendly/description
  Small helper to show WireGuard peers with friendly names from UCI.
endef

# Standard-Verhalten reicht völlig aus, OpenWrt erledigt das Klonen im Hintergrund
define Build/Prepare
	$(call Build/Prepare/Default)
endef

# Da es ein reines Shell-Skript ist, wird die Kompilierung übersprungen
define Build/Compile
endef

# Installation direkt aus dem automatisch geklonten Quellordner ($(PKG_BUILD_DIR))
define Package/wg-friendly/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/wg-friendly $(1)/usr/bin/wg-friendly

	$(INSTALL_DIR) $(1)/usr/share/doc/wg-friendly
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/README.md $(1)/usr/share/doc/wg-friendly/README.md
endef

$(eval $(call BuildPackage,wg-friendly))
