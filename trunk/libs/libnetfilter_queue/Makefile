# https://www.netfilter.org
# https://github.com/openwrt/packages/tree/master/libs/libnetfilter-queue/patches

SRC_NAME=libnetfilter_queue-1.0.5
SRC_URL=https://www.netfilter.org/pub/libnetfilter_queue/$(SRC_NAME).tar.bz2

all: download_test extract_test config_test
	$(MAKE) -j$(HOST_NCPU) -C $(SRC_NAME)

download_test:
	( if [ ! -f $(SRC_NAME).tar.bz2 ]; then \
		wget -t5 -T20 --no-check-certificate -O $(SRC_NAME).tar.bz2 $(SRC_URL) || rm -f $(SRC_NAME).tar.bz2; \
	fi )

extract_test:
	( if [ ! -d $(SRC_NAME) ]; then \
		tar jxf $(SRC_NAME).tar.bz2 ; \
		find "$(shell pwd)"/patches -type f -name "*.patch" -print0 \
		  | sort -z \
		  | xargs -r -t -0 -n 1 patch -d $(SRC_NAME) -p1 -i; \
	fi )

config_test:
	( if [ -f ./config_done ]; then \
		echo "the same configuration"; \
	else \
		make configure && touch config_done; \
	fi )

configure:
	( cd $(SRC_NAME) ; \
	autoreconf -fi ; \
	./configure \
		--prefix= \
		--enable-static \
		--disable-shared \
		--host=$(HOST_TARGET) \
		--build=$(HOST_BUILD) ; \
	)

clean:
	if [ -f $(SRC_NAME)/Makefile ] ; then \
		$(MAKE) -C $(SRC_NAME) distclean ; \
	fi ; \
	rm -f config_done

install:
	$(MAKE) -C $(SRC_NAME) install DESTDIR=$(STAGEDIR)

romfs:
