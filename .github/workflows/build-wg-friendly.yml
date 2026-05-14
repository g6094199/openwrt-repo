# package/wg-friendly/Makefile
include $(TOPDIR)/rules.mk

PKG_NAME:=wg-friendly
PKG_VERSION:=0.1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/g6094199/OpenWRT-Wireguard-friendly-cli-peernames.git
PKG_SOURCE_VERSION:=REPLACE_WITH_TAG_OR_COMMIT

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

# Prepare: klone das upstream-Repo und kopiere das Script in ./files/
define Build/Prepare
    $(call Build/Prepare/Default)
    # Saubere Build-Quelle sicherstellen
    rm -rf $(PKG_BUILD_DIR)
    mkdir -p $(PKG_BUILD_DIR)
    # Klonen (tiefe Kopie); wenn PKG_SOURCE_VERSION ein Branch/Tag ist, wird --branch genutzt
    @if [ -n "$(PKG_SOURCE_VERSION)" ]; then \
      git clone --depth 1 --branch $(PKG_SOURCE_VERSION) $(PKG_SOURCE_URL) $(PKG_BUILD_DIR) || { \
        # Falls branch checkout fehlschlägt (z.B. bei Commit-Hash), klone default und checkout Commit
        rm -rf $(PKG_BUILD_DIR); git clone --depth 1 $(PKG_SOURCE_URL) $(PKG_BUILD_DIR); \
        git -C $(PKG_BUILD_DIR) fetch --depth 1 origin $(PKG_SOURCE_VERSION) || true; \
        git -C $(PKG_BUILD_DIR) checkout $(PKG_SOURCE_VERSION) || true; \
      }; \
    else \
      git clone --depth 1 $(PKG_SOURCE_URL) $(PKG_BUILD_DIR); \
    fi
    # Erstelle files/ und kopiere das Script (Pfad im upstream-Repo: wg-friendly im Repo-Root)
    mkdir -p ./files
    install -m 0755 $(PKG_BUILD_DIR)/wg-friendly ./files/wg-friendly || true
endef

define Build/Compile
    # kein Kompilieren nötig (Shell-Script)
endef

define Package/wg-friendly/install
    $(INSTALL_DIR) $(1)/usr/bin
    $(INSTALL_BIN) ./files/wg-friendly $(1)/usr/bin/wg-friendly
    # optional: docs oder default config
    $(INSTALL_DIR) $(1)/usr/share/doc/wg-friendly
    $(INSTALL_DATA) ./files/README $(1)/usr/share/doc/wg-friendly/README || true
endef

$(eval $(call BuildPackage,wg-friendly))
