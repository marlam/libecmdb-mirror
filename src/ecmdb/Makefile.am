# Copyright (C) 2010, 2011, 2012
# Martin Lambers <martin.lambers@uni-siegen.de>
#
# Copying and distribution of this file, with or without modification, are
# permitted in any medium without royalty provided the copyright notice and this
# notice are preserved. This file is offered as-is, without any warranty.

lib_LTLIBRARIES = libecmdb.la
nobase_include_HEADERS = ecmdb/version.h ecmdb/ecm.h ecmdb/ecmdb.h
libecmdb_la_SOURCES = ecm.cpp ecmdb.cpp jpegblob.h jpegblob.cpp
libecmdb_la_LDFLAGS = -version-info $(LT_CURRENT):$(LT_REVISION):$(LT_AGE) -no-undefined
libecmdb_la_LIBADD = $(libgta_LIBS) $(LTLIBJPEG)
AM_CPPFLAGS = -I$(top_srcdir)/src/base -I$(top_srcdir)/src/glvm -I$(top_builddir)/src/ecmdb $(libgta_CFLAGS)
pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = ecmdb.pc
DISTCLEANFILES = $(pkgconfig_DATA)

# When a shared libecmdb library is built, the libecmdb.la file causes unnecessary
# direct linking of the application with libraries that libecmdb uses. This is bad
# because the application then unnecessarily depends on the .so versions of
# these libraries, even though it does not use their interfaces directly. Direct
# linking with these libraries is only necessary for the static libecmdb library.
#
# Pkg-config solves this by providing both a Libs and Libs.private field, where
# Libs.private is only used for static linking.
#
# As of 2010-04-29, libtool has no fix for this problem. Therefore we just
# remove the libecmdb.la file by default if a shared library is built. This can
# be overriden by a configure option (--enable-la-file).
if INSTALL_LA_FILE
else
install-exec-hook:
	rm $(DESTDIR)$(libdir)/libecmdb.la
endif
