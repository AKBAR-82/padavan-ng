ifndef ROOTDIR
ROOTDIR=../..
endif

ROMFS_DIR = $(ROOTDIR)/romfs

include $(ROOTDIR)/user/shared/boards.mk

PROJECT_HOME_URL="https:\/\/gitlab.com\/dm38\/padavan-ng"
LABEL_COPYRIGHT_TEXT="© 2011-2020 Padavan \& N56U project community \& Linaro \& Alxdm"

BOARD_PATTERN=s/ZVMODELVZ/$(CONFIG_FIRMWARE_PRODUCT_ID)/g
COPYR_PATTERN=s/ZVCOPYRVZ/$(LABEL_COPYRIGHT_TEXT)/g
DWURL_PATTERN=s/ZVDWURLVZ/$(PROJECT_HOME_URL)/g

WEBUI_NAME=n56u_ribbon_fixed

all:

romfs:
	echo "Make www romfs"
	rm -Rf $(ROMFS_DIR)/www
	cp -R $(WEBUI_NAME) $(ROMFS_DIR)/www
	rm -f $(ROMFS_DIR)/www/httpd_check.htm
	echo "ASUSTeK" > $(ROMFS_DIR)/www/httpd_check.htm
	cd $(ROMFS_DIR)/www && ln -sf /opt/share/www/custom custom
	cp dict/EN.header $(ROMFS_DIR)/www
	cp -f logo/$(CONFIG_VENDOR).png $(ROMFS_DIR)/www/bootstrap/img/logo.png \
		|| cp -f logo/padavan.png $(ROMFS_DIR)/www/bootstrap/img/logo.png
ifeq ($(CONFIG_FIRMWARE_INCLUDE_DNSCRYPT),y)
	cd $(ROMFS_DIR)/www && ln -sf /usr/share/dnscrypt-proxy/dnscrypt-resolvers.csv dnscrypt-resolvers.csv
endif
ifeq ($(CONFIG_FIRMWARE_INCLUDE_WPAD),y)
	ln -s /etc/storage/wpad.dat $(ROMFS_DIR)/www/wpad.dat
	ln -s /etc/storage/wpad.dat $(ROMFS_DIR)/www/wpad.da
	ln -s /etc/storage/wpad.dat $(ROMFS_DIR)/www/proxy.pac
endif
ifeq ($(CONFIG_FIRMWARE_INCLUDE_LANG_BR),y)
	echo "LANG_BR=Brazil" >> $(ROMFS_DIR)/www/EN.header
	cp dict/BR.dict $(ROMFS_DIR)/www
endif
ifeq ($(CONFIG_FIRMWARE_INCLUDE_LANG_CZ),y)
	echo "LANG_CZ=Česky" >> $(ROMFS_DIR)/www/EN.header
	cp dict/CZ.dict $(ROMFS_DIR)/www
endif
ifeq ($(CONFIG_FIRMWARE_INCLUDE_LANG_DA),y)
	echo "LANG_DA=Dansk" >> $(ROMFS_DIR)/www/EN.header
	cp dict/DA.dict $(ROMFS_DIR)/www
endif
ifeq ($(CONFIG_FIRMWARE_INCLUDE_LANG_DE),y)
	echo "LANG_DE=Deutsch" >> $(ROMFS_DIR)/www/EN.header
	cp dict/DE.dict $(ROMFS_DIR)/www
endif
ifeq ($(CONFIG_FIRMWARE_INCLUDE_LANG_ES),y)
	echo "LANG_ES=Español" >> $(ROMFS_DIR)/www/EN.header
	cp dict/ES.dict $(ROMFS_DIR)/www
endif
ifeq ($(CONFIG_FIRMWARE_INCLUDE_LANG_FI),y)
	echo "LANG_FI=Finsk" >> $(ROMFS_DIR)/www/EN.header
	cp dict/FI.dict $(ROMFS_DIR)/www
endif
ifeq ($(CONFIG_FIRMWARE_INCLUDE_LANG_FR),y)
	echo "LANG_FR=Français" >> $(ROMFS_DIR)/www/EN.header
	cp dict/FR.dict $(ROMFS_DIR)/www
endif
ifeq ($(CONFIG_FIRMWARE_INCLUDE_LANG_NO),y)
	echo "LANG_NO=Norsk" >> $(ROMFS_DIR)/www/EN.header
	cp dict/NO.dict $(ROMFS_DIR)/www
endif
ifeq ($(CONFIG_FIRMWARE_INCLUDE_LANG_PL),y)
	echo "LANG_PL=Polski" >> $(ROMFS_DIR)/www/EN.header
	cp dict/PL.dict $(ROMFS_DIR)/www
endif
ifeq ($(CONFIG_FIRMWARE_INCLUDE_LANG_RU),y)
	echo "LANG_RU=Pусский" >> $(ROMFS_DIR)/www/EN.header
	cp dict/RU.dict $(ROMFS_DIR)/www
endif
ifeq ($(CONFIG_FIRMWARE_INCLUDE_LANG_SV),y)
	echo "LANG_SV=Svensk" >> $(ROMFS_DIR)/www/EN.header
	cp dict/SV.dict $(ROMFS_DIR)/www
endif
ifeq ($(CONFIG_FIRMWARE_INCLUDE_LANG_UK),y)
	echo "LANG_UK=Українська" >> $(ROMFS_DIR)/www/EN.header
	cp dict/UK.dict $(ROMFS_DIR)/www
endif
	cat $(ROMFS_DIR)/www/EN.header dict/EN.footer > $(ROMFS_DIR)/www/EN.dict
	sed -i 's/^Web_Title=.*/Web_Title=ZVMODELVZ Wireless Router/' $(ROMFS_DIR)/www/*.dict
	sed $(BOARD_PATTERN) -i $(ROMFS_DIR)/www/*.dict
	sed $(COPYR_PATTERN) -i $(ROMFS_DIR)/www/*.dict
	sed $(DWURL_PATTERN) -i $(ROMFS_DIR)/www/*.dict
	rm -f $(ROMFS_DIR)/www/EN.header
	rm -f $(ROMFS_DIR)/www/bootstrap/js/bootstrap.js
	rm -f $(ROMFS_DIR)/www/bootstrap/js/engage.itoggle.js
	rm -f $(ROMFS_DIR)/www/bootstrap/js/jquery.backgroundpos.min.js
	rm -f $(ROMFS_DIR)/www/bootstrap/js/jquery.easing.1.3.js
	rm -f $(ROMFS_DIR)/www/bootstrap/css/bootstrap.css
ifeq ($(BOARD_HAS_5G_RADIO),0)
	rm -f $(INSTALLDIR)/www/Advanced_ACL_Content.asp
	rm -f $(INSTALLDIR)/www/Advanced_WAdvanced_Content.asp
	rm -f $(INSTALLDIR)/www/Advanced_WGuest_Content.asp
	rm -f $(INSTALLDIR)/www/Advanced_Wireless_Content.asp
	rm -f $(INSTALLDIR)/www/Advanced_WMode_Content.asp
	rm -f $(INSTALLDIR)/www/Advanced_WSecurity_Content.asp
	rm -f $(INSTALLDIR)/www/Main_WStatus_Content.asp
	rm -f $(INSTALLDIR)/www/wireless.js
	rm -f $(INSTALLDIR)/www/wds_aplist.asp
	rm -f $(INSTALLDIR)/www/device-map/router.asp
endif
ifndef CONFIG_IPV6
	rm -f $(INSTALLDIR)/www/Advanced_IPv6_Content.asp
endif
ifndef CONFIG_ATA
	rm -f $(INSTALLDIR)/www/device-map/sata.asp
endif
ifndef CONFIG_USB_SUPPORT
	rm -f $(INSTALLDIR)/www/Advanced_Modem_others.asp
	rm -f $(INSTALLDIR)/www/Advanced_Printer_others.asp
	rm -f $(INSTALLDIR)/www/modem_isp.js
	rm -f $(INSTALLDIR)/www/device-map/modem.asp
	rm -f $(INSTALLDIR)/www/device-map/printer.asp
	rm -f $(INSTALLDIR)/www/device-map/hub.asp
endif
ifneq ($(STORAGE_ENABLED),y)
	rm -f $(INSTALLDIR)/www/Advanced_AiDisk_ftp.asp
	rm -f $(INSTALLDIR)/www/Advanced_AiDisk_others.asp
	rm -f $(INSTALLDIR)/www/Advanced_AiDisk_samba.asp
	rm -f $(INSTALLDIR)/www/aidisk.asp
	rm -f $(INSTALLDIR)/www/disk_folder_tree.js
	rm -f $(INSTALLDIR)/www/device-map/disk.asp
	rm -f $(INSTALLDIR)/www/device-map/safely_remove_disk.asp
	rm -rf $(INSTALLDIR)/www/aidisk
	rm -rf $(INSTALLDIR)/www/images/AiDisk
	rm -rf $(INSTALLDIR)/www/images/Tree
endif

clean:
	@echo "Clean www romfs"
