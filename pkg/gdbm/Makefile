# $FENRIR$
#
# Copyright © 2019, Colvin Wellborn All rights reserved.

PACKAGE		= gdbm
ARCHIVE		= gdbm-1.17.tar.gz
URL		= http://ftp.gnu.org/gnu/gdbm
CHECKSUM	= f20ce117abc6f302ecf62c34d41c1ecf
SOURCE_DIR	= gdbm-1.17

default: build install clean

include $(CURDIR)/../../mk/pkg.mk

build: chroot-check fetch extract
	cd $(BUILD_DIR) \
	&& ./configure \
		--prefix=/usr \
		--disable-static \
		--enable-libgdbm-compat \
	&& make -j$(PKG_JOBS)

test:
	cd $(BUILD_DIR) && make check

install:
	cd $(BUILD_DIR) && make install

.PHONY: default build test install
