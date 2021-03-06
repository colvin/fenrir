# $FENRIR$
#
# Copyright © 2019, Colvin Wellborn All rights reserved.

PACKAGE		= binutils
ARCHIVE		= binutils-2.31.1.tar.xz
URL		= http://ftp.gnu.org/gnu/binutils
CHECKSUM	= 5b7c9d4ce96f507d95c1b9a255e52418
SOURCE_DIR	= binutils-2.31.1

default: build install clean

include $(CURDIR)/../../mk/pkg.mk

bootstrap-one: fetch extract bootstrap-one-build install

bootstrap-one-build:
	mkdir $(BUILD_DIR)/build
	cd $(BUILD_DIR)/build \
	&& ../configure \
		--prefix=/tools \
		--with-sysroot=$(BUILD_ROOT) \
		--with-lib-path=/tools/lib \
		--target=$(BOOTSTRAP_TGT) \
		--disable-nls \
		--disable-werror \
	&& make -j$(PKG_JOBS) \
	&& mkdir -v /tools/lib \
	&& ln -sv lib /tools/lib64

bootstrap-two: fetch extract bootstrap-two-build bootstrap-two-install bootstrap-two-postinstall

bootstrap-two-build:
	mkdir $(BUILD_DIR)/build
	cd $(BUILD_DIR)/build \
	&& CC=$(BOOTSTRAP_TGT)-gcc \
	AR=$(BOOTSTRAP_TGT)-ar \
	RANLIB=$(BOOTSTRAP_TGT)-ranlib \
	../configure \
		--prefix=/tools \
		--disable-nls \
		--disable-werror \
		--with-lib-path=/tools/lib \
		--with-sysroot \
	&& make -j$(PKG_JOBS)

bootstrap-two-install:
	cd $(BUILD_DIR)/build && make install

bootstrap-two-postinstall:
	cd $(BUILD_DIR)/build \
	&& make -C ld clean \
	&& make -j$(PKG_JOBS) -C ld LIB_PATH=/usr/lib:/lib \
	&& cp ld/ld-new /tools/bin

build: chroot-check fetch extract
	expect -c 'spawn ls'
	mkdir $(BUILD_DIR)/build
	cd $(BUILD_DIR)/build \
	&& ../configure \
		--prefix=/usr \
		--enable-gold \
		--enable-ld=default \
		--enable-plugins \
		--enable-shared \
		--disable-werror \
		--enable-64-bit-bfd \
		--with-system-zlib \
	&& make -j$(PKG_JOBS) tooldir=/usr

test:
	cd $(BUILD_DIR)/build && make -k check

install:
	cd $(BUILD_DIR)/build && make tooldir=/usr install

.PHONY: default build test install
