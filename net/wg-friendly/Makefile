include $(TOPDIR)/rules.mk

PKG_NAME:=wg-friendly
PKG_VERSION:=0.1.0
PKG_RELEASE:=16

PKG_SOURCE_PROTO:=git
# Hier ist deine exakte Wunsch-URL ohne .git Endung hinterlegt:
PKG_SOURCE_URL:=https://github.com/g6094199/OpenWRT-Wireguard-friendly-cli-peernames
PKG_SOURCE_VERSION:=main
#PKG_MIRROR_HASH:=ca53419d0e19d1bb0b06dc60edd0d8e7aacf8b74a3f83d3534c7087d96197e2b

PKG_MAINTAINER:=g6094199
PKG_LICENSE:=GPL-3.0

include $(INCLUDE_DIR)/package.mk

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

define Package/wg-friendly
  SECTION:=net
  CATEGORY:=Network
  TITLE:=WireGuard friendly CLI peer names
  DEPENDS:=+wireguard-tools +ucode +ucode-mod-uci
  PKGARCH:=all
  PKG_FLAGS:=nonshared

endef

define Package/wg-friendly/description
  Small helper script written in ucode to show WireGuard peers with friendly names from UCI.
endef

define Build/Compile
	# Reines ucode-Skript, keine Kompilierung notwendig
endef

define Package/wg-friendly/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/wg-friendly $(1)/usr/bin/wg-friendly

	$(INSTALL_DIR) $(1)/usr/share/doc/wg-friendly
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/README.md $(1)/usr/share/doc/wg-friendly/README.md
endef

$(eval $(call BuildPackage,wg-friendly))
