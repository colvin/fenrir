# $FENRIR$
#
# Copyright © 2019, Colvin Wellborn All rights reserved.

PACKAGE		= grep
ARCHIVE		= grep-3.1.tar.xz
URL		= http://ftp.gnu.org/gnu/grep
CHECKSUM	= feca7b3e7c7f4aab2b42ecbfc513b070
SOURCE_DIR	= grep-3.1

default: build install clean

include $(CURDIR)/../../mk/pkg.mk

bootstrap-two: fetch extract bootstrap-two-build install

bootstrap-two-build:
	cd $(BUILD_DIR) \
	&& ./configure --prefix=/tools \
	&& make -j$(PKG_JOBS)

build: chroot-check fetch extract
	cd $(BUILD_DIR) \
	&& ./configure \
		--prefix=/usr \
		--bindir=/bin \
	&& make -j$(PKG_JOBS)

test:
	cd $(BUILD_DIR) && make -k check

install:
	cd $(BUILD_DIR) && make install

.PHONY: default build test install
