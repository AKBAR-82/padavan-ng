# https://github.com/ngtcp2/nghttp3

SRC_VER = 1.10.1
SRC_NAME = nghttp3-$(SRC_VER)
SRC_URL = https://github.com/ngtcp2/nghttp3/releases/download/v$(SRC_VER)/$(SRC_NAME).tar.xz

CFLAGS += -fPIC
CXXFLAGS += -fPIC

all: download_test extract_test config_test
	$(MAKE) -j$(HOST_NCPU) -C $(SRC_NAME)/build

download_test:
	( if [ ! -f $(SRC_NAME).tar.xz ]; then \
		wget -t5 -T20 --no-check-certificate -O $(SRC_NAME).tar.xz $(SRC_URL) \
		    || rm -f $(SRC_NAME).tar.xz; \
	fi )

extract_test:
	( if [ ! -d $(SRC_NAME) ]; then \
		tar xJf $(SRC_NAME).tar.xz; \
	fi )
	
config_test:
	( if [ -f ./config_done ]; then \
		echo "the same configuration"; \
	else \
		make configure && touch config_done; \
	fi )

configure:
	( mkdir -p $(SRC_NAME)/build && cd $(SRC_NAME)/build ; \
	cmake	-DCMAKE_INSTALL_PREFIX:PATH=/ \
		-DENABLE_EXAMPLES=OFF \
		-DENABLE_STATIC_LIB=ON \
		-DENABLE_SHARED_LIB=OFF \
		-DENABLE_STATIC_CRT=OFF \
		-DCMAKE_BUILD_TYPE=Release \
		-DCMAKE_TOOLCHAIN_FILE=$(ROOTDIR)/include/cross-mipsel-linux.cmake .. \
	)

clean:
	if [ -d $(SRC_NAME)/build ] ; then \
		rm -rf $(SRC_NAME)/build ; \
	fi ; \
	rm -f config_done

install:
	$(MAKE) -C $(SRC_NAME)/build install DESTDIR=$(STAGEDIR)

romfs:
