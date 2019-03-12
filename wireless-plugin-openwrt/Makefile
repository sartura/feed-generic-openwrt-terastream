include $(TOPDIR)/rules.mk

PKG_NAME:=wireless-plugin-openwrt
PKG_RELEASE:=2018-11-30
PKG_VERSION:=0.1.1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/sartura/wireless-plugin-openwrt.git
PKG_SOURCE_VERSION:=d92173d7ac2d2d6b4748fea07aec2c1f14a0b6e7
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.xz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION)

PKG_BUILD_ROOT:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)
PKG_BUILD_DIR:=$(PKG_BUILD_ROOT)

PKG_MAINTAINER:=Matija Amidzic <matija.amidzic@sartura.hr>

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/wireless-plugin-openwrt
  SECTION:=Sysrepo Plugins
  CATEGORY:=Sysrepo Plugins
  TITLE:=wireless plugin
  DEPENDS:= +sysrepo +libuci +sysrepoctl +libubus +libubox +libblobmsg-json
endef

define Package/wireless-plugin-openwrt/description
	Sysrepo wireless plugin for generic OpenWrt
endef

CMAKE_OPTIONS:= \
	-DCMAKE_INSTALL_PREFIX=/usr \
	-DCMAKE_BUILD_TYPE=Debug \
	-DPLUGIN:BOLL=TRUE

define Package/wireless-plugin-openwrt/install
	$(INSTALL_DIR) $(1)/usr/lib/sysrepo/plugins/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/sysrepo-plugin-router-wireless.so $(1)/usr/lib/sysrepo/plugins/

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/yang/router-wireless@2018-11-27.yang $(1)/etc/sysrepo/yang/

	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/wireless.default $(1)/etc/uci-defaults/99_wireless
endef

$(eval $(call BuildPackage,wireless-plugin-openwrt))
