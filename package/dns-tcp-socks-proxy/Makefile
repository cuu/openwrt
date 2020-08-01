#
# dns-tcp-socks-proxy Makefile for OpenWRT
#
#

include $(TOPDIR)/rules.mk

#
PKG_NAME:=dns-tcp-socks-proxy
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/cuu/dns-tcp-socks-proxy.git
PKG_SOURCE_VERSION:=8d414e2e73d996d62aed49cf99b5bb374d1e67d7
PKG_SOURCE_VERSION_SHORT:=8d414e2e
PKG_MIRROR_HASH:=skip

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_SOURCE_VERSION_SHORT)

include $(INCLUDE_DIR)/package.mk

define Package/dns-tcp-socks-proxy
  SECTION:=base
  CATEGORY:=Base system
  TITLE:=A simple dns proxy to tunnel DNS requests over a socks proxy
  URL:=https://github.com/jtripper/dns-tcp-socks-proxy
  MENU:=1
endef

define Package/dns-tcp-socks-proxy/description
  A simple dns proxy to tunnel DNS requests over a socks proxy (for example, over ssh or Tor). This can come in handy when setting up transparent proxies.
  It chooses a random DNS server for each request from the file "resolv.conf" which is a newline delimited list of DNS servers.
  The daemon must be run as root in order for it to bind to port 53.
endef

#define Package/dns-tcp-socks-proxy/config
#	source "$(SOURCE)/Config.in"
#endef

define Build/Configure
endef

ifdef CONFIG_GCC_VERSION_LLVM
  TARGET_CFLAGS += -fnested-functions
endif

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC="$(TARGET_CC)" \
		CROSS_COMPILE="$(TARGET_CROSS)" \
		EXTRA_CFLAGS="$(TARGET_CFLAGS)" \
		ARCH="$(ARCH)" 
	
endef

define Package/dns-tcp-socks-proxy/install
  $(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/dns_proxy $(1)/usr/bin
endef

$(eval $(call BuildPackage,dns-tcp-socks-proxy))
