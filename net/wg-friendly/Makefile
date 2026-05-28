# package/wg-friendly/Makefile
include $(TOPDIR)/rules.mk

PKG_NAME:=wg-friendly
PKG_VERSION:=0.1.0
PKG_RELEASE:=2

# Die vollständige Quell-URL zum Repository des Skripts
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/g6094199/wg-friendly.git
# Wird von der GitHub Action dynamisch vor jedem Build überschrieben
PKG_SOURCE_VERSION:=PLACEHOLDER
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
  PKGARCH:=all
endef

define Package/wg-friendly/description
  Small helper to show WireGuard peers with friendly names from UCI.
endef

define Build/Prepare
	$(call Build/Prepare/Default)
endef

define Build/Compile
	# Reines Shell-Skript, keine Kompilierung nötig
endef

define Package/wg-friendly/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/wg-friendly $(1)/usr/bin/wg-friendly

	$(INSTALL_DIR) $(1)/usr/share/doc/wg-friendly
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/README.md $(1)/usr/share/doc/wg-friendly/README.md
endef

$(eval $(call BuildPackage,wg-friendly))
