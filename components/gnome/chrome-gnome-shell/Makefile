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

#
# Copyright (c) 2018, 2020, Oracle and/or its affiliates.
#

# All components using gobject-introspection must be built with gcc as
# gobject-introspection does not produce correct results when using Studio.
COMPILER =              gcc
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		chrome-gnome-shell
COMPONENT_VERSION=	10.1
COMPONENT_PROJECT_URL=	https://wiki.gnome.org/Projects/GnomeShellIntegrationForChrome
COMPONENT_ARCHIVE=	v$(COMPONENT_VERSION).tar.gz
COMPONENT_ARCHIVE_URL=	https://github.com/GNOME/chrome-gnome-shell/archive/$(COMPONENT_ARCHIVE)
COMPONENT_ARCHIVE_HASH= \
	sha256:d93e83c7e7193e386df4acad6ea4c86ea9abc75bbe67539bbc9310607ea6aeb5
COMPONENT_BUGDB=        gnome/gnome-shell
COMPONENT_ANITYA_ID=	17138

TPNO=			41814

PYTHON_VERSION = 3.7

TEST_TARGET = $(NO_TESTS)

BUILD_STYLE = cmake

include $(WS_MAKE_RULES)/gnome-component.mk

# Need to use GNU head
COMPONENT_BUILD_ENV += PATH="$(GNUBIN):$(PATH)"

# Need to convert "#! /usr/bin/env python" to actual path for pkgdepend to work
PYTHON_SCRIPTS += $(PROTOUSRBINDIR)/chrome-gnome-shell

# Use explicit Python version rather than the default one
CMAKE_OPTIONS += -DPYTHON_EXECUTABLE=$(PYTHON)

# Deliver into vendor-packages instead of site-packages
COMPONENT_POST_INSTALL_ACTION += \
	$(MKDIR) $(PROTOUSRLIBDIR)/python3.7/vendor-packages; \
	$(MV) $(PROTOUSRLIBDIR)/python3.7/site-packages/* $(PROTOUSRLIBDIR)/python3.7/vendor-packages/

REQUIRED_PACKAGES += library/python/pygobject-3-37
REQUIRED_PACKAGES += library/python/requests-37
REQUIRED_PACKAGES += runtime/python-37
REQUIRED_PACKAGES += text/jq
