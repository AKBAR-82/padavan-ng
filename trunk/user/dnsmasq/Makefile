SRC_NAME=dnsmasq-2.8x

COPTS := -DHAVE_BROKEN_RTC -DNO_INOTIFY -DNO_AUTH -DNO_LOOP -DNO_DUMPFILE
ifndef CONFIG_IPV6
COPTS += -DNO_IPV6
endif
ifndef CONFIG_USB_SUPPORT
COPTS += -DNO_TFTP
endif
ifeq ($(CONFIG_FIRMWARE_ENABLE_DNSMASQ_REGEX),y)
COPTS += -DHAVE_REGEX
ifeq ($(CONFIG_FIRMWARE_INCLUDE_IPSET),y)
COPTS += -DHAVE_REGEX_IPSET
endif
endif
ifneq ($(CONFIG_FIRMWARE_INCLUDE_IPSET),y)
COPTS += -DNO_IPSET
endif

CFLAGS += -ffunction-sections -fdata-sections -fvisibility=hidden
LDFLAGS += -Wl,--gc-sections

all:
	$(MAKE) -j$(HOST_NCPU) -C $(SRC_NAME) CFLAGS="$(CFLAGS)" LDFLAGS="$(LDFLAGS)" COPTS="$(COPTS)"

clean:
	$(MAKE) -C $(SRC_NAME) clean

romfs:
	$(ROMFSINST) $(SRC_NAME)/src/dnsmasq /usr/sbin/dnsmasq
