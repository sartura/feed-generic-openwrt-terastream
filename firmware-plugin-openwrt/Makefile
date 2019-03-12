include $(TOPDIR)/rules.mk

PKG_NAME:=firmware-plugin-openwrt
PKG_RELEASE:=2018-10-25
PKG_VERSION:=0.1.1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/sartura/firmware-plugin-openwrt.git
PKG_SOURCE_VERSION:=56b55e7046c28d6f11f35d1b505905ca5641d7af
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.xz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION)

PKG_BUILD_ROOT:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)
PKG_BUILD_DIR:=$(PKG_BUILD_ROOT)

PKG_MAINTAINER:=Matija Amidzic <matija.amidzic@sartura.hr>

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/firmware-plugin-openwrt
  SECTION:=Sysrepo Plugins
  CATEGORY:=Sysrepo Plugins
  TITLE:=firmware plugin
  DEPENDS:= +sysrepo +sysrepoctl +libopenssl +libcurl +libubox +libubus +libblobmsg-json +libjson-c
endef

define Package/firmware-plugin-openwrt/description
	Sysrepo firmware plugin for generic openwrt
endef

CMAKE_OPTIONS:= \
	-DCMAKE_INSTALL_PREFIX=/usr \
	-DCMAKE_BUILD_TYPE=Debug \
	-DPLUGIN:BOLL=TRUE

define Package/firmware-plugin-openwrt/install
	$(INSTALL_DIR) $(1)/usr/lib/sysrepo/plugins/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/sysrepo-plugin-router-firmware.so $(1)/usr/lib/sysrepo/plugins/

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/yang/router-software@2018-10-22.yang $(1)/etc/sysrepo/yang/

	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/firmware.default $(1)/etc/uci-defaults/99_firmware
endef

$(eval $(call BuildPackage,firmware-plugin-openwrt))
