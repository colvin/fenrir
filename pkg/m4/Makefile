# $FENRIR$
#
# Copyright © 2019, Colvin Wellborn All rights reserved.

PACKAGE		= m4
ARCHIVE		= m4-1.4.18.tar.xz
URL		= http://ftp.gnu.org/gnu/m4
CHECKSUM	= 730bb15d96fffe47e148d1e09235af82
SOURCE_DIR	= m4-1.4.18

default: build install clean

include $(CURDIR)/../../mk/pkg.mk

bootstrap-two: fetch extract bootstrap-two-build install

bootstrap-two-build:
	cd $(BUILD_DIR) \
	&& sed -i 's/IO_ftrylockfile/IO_EOF_SEEN/' lib/*.c \
	&& echo "#define _IO_IN_BACKUP 0x100" >> lib/stdio-impl.h \
	&& ./configure --prefix=/tools \
	&& make -j$(PKG_JOBS)

build: chroot-check fetch extract
	cd $(BUILD_DIR) \
	&& sed -i 's/IO_ftrylockfile/IO_EOF_SEEN/' lib/*.c \
	&& echo "#define _IO_IN_BACKUP 0x100" >> lib/stdio-impl.h \
	&& ./configure --prefix=/usr \
	&& make -j$(PKG_JOBS)

test:
	cd $(BUILD_DIR) && make check

install:
	cd $(BUILD_DIR) && make install

.PHONY: default build test install
