#
# Copyright (C) 2007-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=tcpdump
PKG_VERSION:=4.9.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.tcpdump.org/release/ \
	http://ftp.gwdg.de/pub/misc/tcpdump/ \
	http://www.at.tcpdump.org/ \
	http://www.br.tcpdump.org/
PKG_MD5SUM:=1e0293210b0dea5ef18e88e4150394b7

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(BUILD_VARIANT)/$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_PARALLEL:=1

PKG_MAINTAINER:=Felix Fietkau <nbd@openwrt.org>
PKG_LICENSE:=BSD-3-Clause

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/tcpdump
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libpcap +libopenssl
  TITLE:=Network monitoring and data acquisition tool
  URL:=http://www.tcpdump.org/
endef

CONFIGURE_ARGS += \
	--with-system-libpcap

ifeq ($(CONFIG_IPV6),y)
CONFIGURE_ARGS += \
	--enable-ipv6
endif

TARGET_CFLAGS += -ffunction-sections -fdata-sections
TARGET_LDFLAGS += -Wl,--gc-sections

CONFIGURE_VARS += \
	BUILD_CC="$(TARGET_CC)" \
	HOSTCC="$(HOSTCC)" \
	td_cv_buggygetaddrinfo="no" \
	ac_cv_linux_vers=$(LINUX_VERSION) \
	ac_cv_header_rpc_rpcent_h=no \
	ac_cv_lib_rpc_main=no \
	ac_cv_path_PCAP_CONFIG=""

MAKE_FLAGS :=

MAKE_FLAGS += \
	CCOPT="$(TARGET_CFLAGS)" INCLS="-I. $(TARGET_CPPFLAGS)"


define Package/tcpdump/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/tcpdump $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,tcpdump))
