#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License (the "License").
# You may not use this file except in compliance with the License.
#
# You can obtain a copy of the license at usr/src/OPENSOLARIS.LICENSE
# or http://www.opensolaris.org/os/licensing.
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at usr/src/OPENSOLARIS.LICENSE.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#
# Copyright (c) 2017, 2020, Oracle and/or its affiliates.
#

# parfait is a bit unhappy (24796622)
export PARFAIT_BUILD=no

BUILD_BITS =            32_and_64
COMPILER =              gcc
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		mozjs
COMPONENT_VERSION=	38.2.1
COMPONENT_PROJECT_URL=	https://developer.mozilla.org/en-US/docs/Mozilla/Projects/SpiderMonkey
COMPONENT_SRC=          mozjs-38.0.0
COMPONENT_ARCHIVE=	mozjs38_38.2.1~rc0.orig.tar.bz2
COMPONENT_ARCHIVE_HASH= \
	sha256:01994c758174bc173bcf4960f05ecb4da21014f09641a63b2952bbf9eeaa8b5c
COMPONENT_ARCHIVE_URL=	https://launchpad.net/ubuntu/+archive/primary/+files/$(COMPONENT_ARCHIVE)
COMPONENT_BUGDB=	library/libmozjs
COMPONENT_ANITYA_ID=	11754

TPNO=			36160

CXXFLAGS += -std=c++11

# Only used during build process.
PYTHON_VERSIONS= 2.7
PYTHON= $(PYTHON.2.7.$(BITS))

# Tests hook up need work
TEST_TARGET = $(SKIP_TEST)

include $(WS_MAKE_RULES)/common.mk

# configure script is not at root of source tree.
CONFIGURE_SCRIPT= $(SOURCE_DIR)/js/src/configure

CONFIGURE_ENV += PYTHON="$(PYTHON)"
CONFIGURE_ENV += LDSHARED="$(CC) -shared"
CONFIGURE_ENV += NSPR_CONFIG="/usr/bin/pkg-config nspr"

CONFIGURE_OPTIONS += --enable-ctypes
CONFIGURE_OPTIONS += --disable-tests
# Uses ancient embedded version of ICU.
CONFIGURE_OPTIONS += --without-intl-api
# Resulting packages are a few hundred megabytes larger without this!
CONFIGURE_OPTIONS += --enable-install-strip
CONFIGURE_OPTIONS += --enable-readline
CONFIGURE_OPTIONS += --enable-shared-js
CONFIGURE_OPTIONS += --disable-static-js
CONFIGURE_OPTIONS += --enable-system-ffi
CONFIGURE_OPTIONS += --enable-threadsafe
CONFIGURE_OPTIONS += --with-system-zlib
CONFIGURE_OPTIONS += --with-x
CONFIGURE_OPTIONS += --enable-strip
CONFIGURE_OPTIONS += --with-system-nspr

# js coredumps on sparc - see bug 24935318
ifeq ($(MACH), sparc)
LD_EXEC_OPTIONS.64 += -M $(WS_COMPONENTS)/desktop/polkit/mapfile
COMPONENT_BUILD_ENV.64 += LD_EXEC_OPTIONS="$(LD_EXEC_OPTIONS.64)"
COMPONENT_INSTALL_ENV.64 += LD_EXEC_OPTIONS="$(LD_EXEC_OPTIONS.64)"
endif

unexport SHELLOPTS
COMPONENT_TEST_ARGS =   -k -i
COMPONENT_TEST_TRANSFORMS += \
        '-n ' \
        '-e "/TOTAL:/p" ' \
        '-e "/SKIP:/p" ' \
        '-e "/PASS:/p" ' \
        '-e "/FAIL:/p" ' \
        '-e "/ERROR:/p" '

REQUIRED_PACKAGES += library/libffi
REQUIRED_PACKAGES += library/nspr
REQUIRED_PACKAGES += library/readline
REQUIRED_PACKAGES += library/security/nss
REQUIRED_PACKAGES += library/zlib
REQUIRED_PACKAGES += system/library/gcc/gcc-c++-runtime
REQUIRED_PACKAGES += system/library/gcc/gcc-c-runtime
REQUIRED_PACKAGES += system/library/math
