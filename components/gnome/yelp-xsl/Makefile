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
# Copyright (c) 2015, 2020, Oracle and/or its affiliates. All rights reserved.
#

BUILD_BITS=             NO_ARCH
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		yelp-xsl
COMPONENT_VERSION=	3.34.0
COMPONENT_PROJECT_URL=  https://wiki.gnome.org/Apps/Yelp
COMPONENT_ARCHIVE_HASH= \
	sha256:e8063aee67d1df634f3d062f1c28130b2dabb3c0c66396b1af90388f34e14ee2
COMPONENT_BUGDB=	gnome/docviewer
COMPONENT_ANITYA_ID=	13164

TPNO=			54137

TEST_TARGET= $(NO_TESTS)

include $(WS_MAKE_RULES)/gnome-component.mk

# Assumes GNU xgettext in PATH.
CONFIGURE_ENV += PATH=$(GNUBIN):$(PATH)

CONFIGURE_OPTIONS += --enable-doc

REQUIRED_PACKAGES += developer/documentation-tool/itstool
REQUIRED_PACKAGES += developer/documentation-tool/mallard/ducktype
REQUIRED_PACKAGES += library/libxslt
