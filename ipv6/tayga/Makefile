# $Id: Makefile 5624 2006-11-23 00:29:07Z nbd $

include $(TOPDIR)/rules.mk

PKG_NAME:=tayga
PKG_VERSION:=0.9.2
PKG_RELEASE:=1

PKG_SOURCE:=tayga-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://www.litech.org/tayga/
PKG_MD5SUM:=7a7b24165ce008df772f398d86fa280e
PKG_CAT:=bzcat

PKG_BUILD_DIR:=$(BUILD_DIR)/tayga-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/tayga
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+ip +kmod-ipv6 +kmod-tun
  TITLE:=Out-of-kernel stateless NAT64 implementation for Linux
  URL:=http://www.litech.org/tayga/
endef

define Package/tayga/description
  TAYGA is an out-of-kernel stateless NAT64 implementation for
  Linux.  It uses the TUN driver to exchange packets with the
  kernel, which is the same driver used by OpenVPN and QEMU/KVM.
endef

# TODO: port scripts to netifd
ifdef CONFIG_PACAKGE_netifd
  define Package/tayga/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tayga $(1)/usr/sbin/
  endef
else
  define Package/tayga/install
	$(INSTALL_DIR) $(1)/usr/sbin $(1)/lib/network $(1)/etc/hotplug.d/iface
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tayga $(1)/usr/sbin/
	$(INSTALL_DATA) ./files/tayga.sh $(1)/lib/network/tayga.sh
	$(INSTALL_DATA) ./files/tayga.hotplug $(1)/etc/hotplug.d/iface/95-tayga
  endef
endif

$(eval $(call BuildPackage,tayga))
