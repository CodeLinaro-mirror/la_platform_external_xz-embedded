ACLOCAL_AMFLAGS := -I m4

AM_CFLAGS := -Wundef \
        -Wstrict-prototypes \
        -Wno-trigraphs \
        -g -O0 \
        $(LOCBASEUTIL_CFLAGS) \
        -fno-inline \
        -fno-short-enums \
        -fpic \
        -D_GNU_SOURCE \
        -DHAVE_CONFIG_H=1 \
        -DBUILD_DIVSUFSORT64 \
        -I../android_include \
        -I../include

AM_CPPFLAGS := \
              -I. \
              -I$(WORKSPACE)/OTA/external/libdivsufsort/android_include \
              -I$(WORKSPACE)/OTA/streaming/external/libchrome \
              -I$(WORKSPACE)/OTA/streaming/external/libbrillo \
              -I$(WORKSPACE)/OTA/streaming/external/modp_b64 \
              -D_FILE_OFFSET_BITS=64 \
              -D_USE_RTTI_FOR_TYPE_TAGS \
              -std=c++11

AUTOMAKE_OPTIONS = subdir-objects

AM_LDFLAGS := -shared -version-info 1:0:0


libxz_src_la_SOURCES :=  linux/lib/xz/xz_crc32.c \
        linux/lib/xz/xz_dec_bcj.c \
        linux/lib/xz/xz_dec_lzma2.c \
        linux/lib/xz/xz_dec_stream.c


libxz_header_la_SOURCES := userspace/xz_config.h \
        linux/include/linux/xz.h
library_includedir := $(pkgincludedir)

library_include_HEADERS := $(libxz_header_la_SOURCES)

lib_LTLIBRARIES := libxz.la
libxz_la_SOURCES := $(libxz_src_la_SOURCES)
libxz_la_SOURCES += $(libxz_header_la_SOURCES)


if USE_GLIB
libxz_la_CFLAGS := $(AM_CFLAGS) -DUSE_GLIB @GLIB_CFLAGS@
libxz_la_CPPFLAGS := $(AM_CPPFLAGS) -fpermissive -DUSE_GLIB @GLIB_CFLAGS@ 
libxz_la_LIBADD := -lm -lcurl -lssl -lmodpb64 -lcrypto -lpthread @GLIB_LIBS@
else
libxz_la_CFLAGS := $(AM_CFLAGS)
libxz_la_CPPFLAGS := $(AM_CPPFLAGS) -fpermissive
libxz_la_LIBADD := -lm -lcurl -lssl -lmodpb64 -lcrypto -lpthread
endif


