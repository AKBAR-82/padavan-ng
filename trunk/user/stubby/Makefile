SRC_NAME=stubby-0.4.3
SRC_URL=https://github.com/getdnsapi/stubby/archive/refs/tags/v0.4.3.tar.gz

all: download_test extract_test config_test
#all: config_test
	$(MAKE) -j$(HOST_NCPU) -C $(SRC_NAME)/build

download_test:
	( if [ ! -f $(SRC_NAME).tar.gz ]; then \
		wget -t5 -T20 --no-check-certificate -O $(SRC_NAME).tar.gz $(SRC_URL) || rm -f $(SRC_NAME).tar.gz; \
	fi )

extract_test:
	( if [ ! -d $(SRC_NAME) ]; then \
		tar xf $(SRC_NAME).tar.gz ; \
	fi )

config_test:
	( if [ -f ./config_done ]; then \
		echo "the same configuration"; \
	else \
		make configure && touch config_done; \
	fi )

configure:
	( mkdir -p $(SRC_NAME)/build && cd $(SRC_NAME)/build ; \
	cmake   -DCMAKE_INSTALL_PREFIX=/usr \
		-DCMAKE_INSTALL_FULL_RUNSTATEDIR=/var/run \
		-DCMAKE_INSTALL_FULL_SYSCONFDIR=/etc/storage \
		-DCMAKE_INSTALL_SYSCONFDIR=/etc/storage \
		-DCMAKE_BUILD_TYPE=Release \
		-DCMAKE_TOOLCHAIN_FILE=$(ROOTDIR)/include/cross-mipsel-linux.cmake .. \
	)

clean:
	rm -rf $(SRC_NAME)/build
	rm config_done

romfs:
	$(ROMFSINST) $(SRC_NAME)/build/stubby /usr/sbin/stubby
	$(ROMFSINST) -p +x /usr/bin/stubby.sh
