include $(TOPDIR)/rules.mk

PKG_NAME:=esurfingclient
PKG_VERSION:=1.1.1
PKG_RELEASE:=2

# 如果你的源码就在 dl 目录下
PKG_SOURCE:=esurfingclient.tar.gz
PKG_SOURCE_URL:=file://$(TOPDIR)/dl
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_HASH:=skip
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/esurfingclient
	SECTION:=net
	CATEGORY:=Network
	TITLE:=ESurfingClient
	# 重点：在这里列出运行时依赖
	DEPENDS:=+libcurl +libopenssl +ca-bundle
endef

define Package/esurfingclient/description
	A lightweight esurfing authentication client
endef

# CMake 配置参数
CMAKE_OPTIONS += \
	-DCMAKE_BUILD_TYPE=Release \
	-DBUILD_SHARED_LIBS=OFF

define Package/esurfingclient/install
	$(INSTALL_DIR) $(1)/usr/bin
	# 注意：这里的二进制文件名必须和 CMakeLists.txt 中 TARGET 生成的名字完全一致（注意大小写）
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/ESurfingClient $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/etc/init.d/esurfingclient.init $(1)/etc/init.d/esurfingclient

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/etc/config/esurfingclient.config $(1)/etc/config/esurfingclient
endef

$(eval $(call BuildPackage,esurfingclient))
