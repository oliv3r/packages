#
# Copyright (C) 2006-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=snapcast
PKG_VERSION:=0.28.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://github.com/badaix/snapcast/releases/download/$(PKG_VERSION)/
PKG_HASH:=7911037dd4b06fe98166db1d49a7cd83ccf131210d5aaad47507bfa0cfc31407

PKG_FIXUP:=autoreconf
PKG_BUILD_FLAGS:=no-mips16
PKG_INSTALL:=1

PKG_MAINTAINER:=Olliver Schinagl <oliver@schinagl.nl>
PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/snapserver
SECTION:=sound
CATEGORY:=Sound
TITLE:=Synchronous multiroom audio player (server)
URL:=https://github.com/baidax/snapcast
DEPENDS:=+alsa-lib +libavahi-client
endef

define Package/snapserver/description
  Snapcast is a multiroom client-server audio player, where all clients are
  time synchronized with the server to play perfectly synced audio. It's not a
  standalone player, but an extension that turns your existing audio player
  into a Sonos-like multiroom solution.
endef

define Package/snapserver/conffiles
/etc/snapserver.conf
endef

CMAKE_BINARY_SUBDIR=build

CMAKE_OPTIONS += \
	-DBUILD_WITH_AVAHI=ON \
	-DBUILD_WITH_EXPAT=ON \
	-DBUILD_WITH_FLAC=ON \
	-DBUILD_WITH_OPUS=ON \
	-DBUILD_WITH_PULSE=ON \
	-DBUILD_WITH_TREMOR=ON \
	-DBUILD_WITH_VORBIS=ON \
	-DBUILD_TESTS=OFF

define Package/snapserver/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/snapserver $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) ./files/snapserver.conf $(1)/etc/snapserver.conf
	$(INSTALL_DIR) $(1)/var/lib/snapserver
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/share/snapserver/* $(1)/usr/share/snapserver/
endef

define Package/snapclient/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/snapclient $(1)/usr/bin/
endef

$(eval $(call BuildPackage,snapserver))
$(eval $(call BuildPackage,snapclient))
