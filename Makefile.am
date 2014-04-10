
ACLOCAL_AMFLAGS = -I m4

JANSSON_CPPFLAGS= -I$(top_builddir)/compat/jansson-2.5/src -I$(top_srcdir)/compat/jansson-2.5/src

EXTRA_DIST	= example.conf m4/gnulib-cache.m4 \
		  ADL_SDK/readme.txt api-example.php miner.php	\
		  API.class API.java api-example.c hexdump.c \
		  doc/API doc/FAQ doc/GPU doc/SCRYPT doc/windows-build.txt

SUBDIRS		= lib compat ccan

bin_PROGRAMS     = ogminer

ogminer_CPPFLAGS = $(PTHREAD_FLAGS) -fno-strict-aliasing $(JANSSON_CPPFLAGS)
ogminer_LDFLAGS  = $(PTHREAD_FLAGS)
ogminer_LDADD    = $(DLOPEN_FLAGS) @LIBCURL_LIBS@ @JANSSON_LIBS@ @PTHREAD_LIBS@ \
		  @OPENCL_LIBS@ @NCURSES_LIBS@ @PDCURSES_LIBS@ @WS2_LIBS@ \
		  @MM_LIBS@ @RT_LIBS@ @MATH_LIBS@ lib/libgnu.a ccan/libccan.a

ogminer_CPPFLAGS += -I$(top_builddir)/lib -I$(top_srcdir)/lib @OPENCL_FLAGS@

if !HAVE_WINDOWS
ogminer_CPPFLAGS += @LIBCURL_CFLAGS@
endif

ogminer_CPPFLAGS += $(ADL_CPPFLAGS)

if USE_GIT_VERSION
GIT_VERSION      := $(shell sh -c 'git describe --abbrev=4 --dirty')
ogminer_CPPFLAGS += -DGIT_VERSION=\"$(GIT_VERSION)\"
endif

ogminer_SOURCES := ogminer.c
ogminer_SOURCES	+= api.c
ogminer_SOURCES	+= elist.h miner.h compat.h bench_block.h
ogminer_SOURCES	+= util.c util.h uthash.h
ogminer_SOURCES	+= sha2.c sha2.h
ogminer_SOURCES	+= logging.c logging.h
ogminer_SOURCES += driver-opencl.c driver-opencl.h
ogminer_SOURCES += ocl.c ocl.h
ogminer_SOURCES += findnonce.c findnonce.h
ogminer_SOURCES += adl.c adl.h adl_functions.h
ogminer_SOURCES += pool.c pool.h
ogminer_SOURCES += algorithm.c algorithm.h
ogminer_SOURCES += scrypt.c scrypt.h
ogminer_SOURCES += kernel/*.cl

bin_SCRIPTS	= $(top_srcdir)/kernel/*.cl

