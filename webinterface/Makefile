include $(TOPDIR)/rules.mk

PKG_NAME:=webinterface
PKG_VERSION:=0.17.16
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/webinterface
  SECTION:=administration
  CATEGORY:=Enigmabox
  TITLE:=Enigmabox web interface
  URL:=http://enigmabox.net/en/
  DEPENDS:=+cjdns
  DEPENDS+= +curl +syslog-ng +zip +unzip +shadow-usermod +kmod-ipt-nat6 +isc-dhcp-server-ipv4 +radvd +gesftpserver
  DEPENDS+= +python-django-1.4 +python-gunicorn +python-six +python-gevent +python-openssl +python-requests +django-south +python-expat +python-json +python-sqlite3 +python-unidecode +python-beanstalkc +pyyaml
  DEPENDS+= +asterisk18 +asterisk18-sounds
  DEPENDS+= +php5 +php5-fastcgi +php5-mod-mcrypt +php5-mod-pdo-sqlite +php5-mod-mysql +php5-mod-session +php5-mod-iconv +php5-mod-json +@PHP5_FILTER
  DEPENDS+= +mysql-server
  DEPENDS+= +lighttpd +lighttpd-mod-auth +lighttpd-mod-fastcgi +lighttpd-mod-proxy
  DEPENDS+= +privoxy
  DEPENDS+= +dovecot +exim4
  DEPENDS+= +cfengine +cfengine-policies
  DEPENDS+= +beanstalkd
  DEPENDS+= +wpa-supplicant +kmod-ath +kmod-ath9k-htc +kmod-brcmfmac +kmod-carl9170 +kmod-libertas-sd +kmod-libertas-usb +kmod-net-zd1201 +kmod-p54-usb +kmod-rt2500-usb +kmod-rt2800-usb +kmod-rt73-usb +kmod-rtl8187 +kmod-rtl8192cu +kmod-zd1211rw
endef

define Package/webinterface/description
 The Enigmabox administration web interface, used for configuring
 the settings of the Enigmabox. It does not depend on any OpenWRT
 interface, in fact, it replaces LuCI.

 It also serves as a metapackage. Select it, and everything else
 required for the Enigmabox will be selected.
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/webinterface/install
	$(INSTALL_DIR) $(1)/box
	cp -r ./files/root/* $(1)

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/webinterface.init $(1)/etc/init.d/webinterface

	$(INSTALL_DIR) $(1)/etc/lighttpd/sites.d
	$(INSTALL_DATA) ./files/lighttpd-site.conf $(1)/etc/lighttpd/sites.d/webinterface.conf
	$(INSTALL_DATA) ./files/mysite.conf $(1)/etc/lighttpd/sites.d/mysite.conf
	$(INSTALL_DIR) $(1)/www/htdocs

	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) ./files/backup-stuff $(1)/usr/sbin/backup-stuff
	$(INSTALL_BIN) ./files/restore-stuff $(1)/usr/sbin/restore-stuff
	$(INSTALL_BIN) ./files/set-country $(1)/usr/sbin/set-country
endef

$(eval $(call BuildPackage,webinterface))
