include $(TOPDIR)/rules.mk

PKG_NAME:=wg-friendly
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

# Nutze das Flag für Architektur-unabhängige Pakete
PKG_FLAGS:=nonshared

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com
PKG_SOURCE_VERSION:=main
PKG_MIRROR_HASH:=skip

PKG_MAINTAINER:=g6094199
PKG_LICENSE:=GPL-3.0

include $(INCLUDE_DIR)/package.mk

define Package/wg-friendly
  SECTION:=net
  CATEGORY:=Network
  TITLE:=WireGuard friendly peernames (ucode)
  # Hier wird die Architektur auf "all" gesetzt
  PKGARCH:=all
  DEPENDS:=+ucode +ucode-mod-uci +ucode-mod-fs +wireguard-tools
  URL:=https://github.com
endef

define Package/wg-friendly/description
  This script adds wireguard friendly user names from the network config
  to a wg output imitation.
endef

define Build/Compile
	true
endef

define Package/wg-friendly/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/wg-friendly $(1)/usr/bin/wg-friendly
endef

$(eval $(call BuildPackage,wg-friendly))
