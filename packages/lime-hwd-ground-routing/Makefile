#
# Copyright (C) 2006-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v3.
#

include $(TOPDIR)/rules.mk

LIME_BUILDDATE:=$(shell date +%Y%m%d_%H%M)
LIME_CODENAME:=bigbang

GIT_COMMIT_DATE:=$(shell git log -n 1 --pretty=%ad --date=short . )
GIT_COMMIT_TSTAMP:=$(shell git log -n 1 --pretty=%at . )

PKG_NAME:=lime-hwd-ground-routing
PKG_VERSION=$(GIT_COMMIT_DATE)-$(GIT_COMMIT_TSTAMP)

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  TITLE:=Manage 802.1q VLANs for ground routing
  CATEGORY:=LiMe
  URL:=http://libre-mesh.org
  DEPENDS:=+lime-system +lua +libuci-lua
endef

define Build/Compile
	@rm -rf ./build || true
	@cp -r ./src ./build
	@sed -i '/^\s*--!.*/d' build/*.lua || true
	@sed -i '/^\s*#\[Doc\]/d' build/*.sh || true
endef

define Package/$(PKG_NAME)/install
	@mkdir -p $(1)/usr/lib/lua/lime/hwd || true
	$(CP) ./build/ground_routing.lua $(1)/usr/lib/lua/lime/hwd/ground_routing.lua
	@chmod +x $(1)/usr/lib/lua/lime/hwd/ground_routing.lua
endef

$(eval $(call BuildPackage,$(PKG_NAME)))