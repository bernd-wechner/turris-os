include $(TOPDIR)/rules.mk

PKG_NAME:=ustream-ssl
PKG_VERSION:=2015-07-09
PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://nbd.name/ustream-ssl.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=c2d73c22618e8ee444e8d346695eca908ecb72d3
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
CMAKE_INSTALL:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(BUILD_VARIANT)/$(PKG_SOURCE_SUBDIR)

PKG_LICENSE:=ISC
PKG_LICENSE_FILES:=

PKG_MAINTAINER:=Felix Fietkau <nbd@openwrt.org>

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/libustream/default
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=ustream SSL Library
  DEPENDS:=+libubox
  ABI_VERSION:=$(PKG_VERSION)
endef

define Package/libustream-openssl
  $(Package/libustream/default)
  TITLE += (openssl)
  DEPENDS += +PACKAGE_libustream-openssl:libopenssl
  VARIANT:=openssl
endef

define Package/libustream/default/install
	$(INSTALL_DIR) $(1)/lib/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/libustream-ssl.so $(1)/lib/
endef

Package/libustream-openssl/install = $(Package/libustream/default/install)

$(eval $(call BuildPackage,libustream-openssl))
