
LIB_VERSION = 0.0.1
LD_VERSION = 0:1:0

AM_CFLAGS = -Wall -Wsign-compare -I$(top_builddir)/include \
	-I$(top_srcdir)/include -DBUILDING_IPMI_SELECTOR_DLL

lib_LTLIBRARIES = libOpenIPMIposix.la libOpenIPMIpthread.la

libOpenIPMIpthread_la_SOURCES = posix_thread_os_hnd.c selector.c
libOpenIPMIpthread_la_LIBADD = -lpthread $(GDBM_LIB) \
	$(top_builddir)/utils/libOpenIPMIutils.la $(RT_LIB)
libOpenIPMIpthread_la_LDFLAGS = -rdynamic -version-info $(LD_VERSION) \
	-no-undefined

libOpenIPMIposix_la_SOURCES = posix_os_hnd.c selector.c
libOpenIPMIposix_la_LIBADD = $(top_builddir)/utils/libOpenIPMIutils.la \
	$(GDBM_LIB) $(RT_LIB)
libOpenIPMIposix_la_LDFLAGS = -rdynamic -version-info $(LD_VERSION) \
	-no-undefined

noinst_HEADERS = heap.h

noinst_PROGRAMS = test_heap test_handlers

test_heap_SOURCES = test_heap.c
test_heap_LDADD = 
test_heap_CFLAGS = -Wall -Wsign-compare -I$(top_builddir)/include \
	-I$(top_srcdir)/include

test_handlers_SOURCES = test_handlers.c
test_handlers_LDADD = libOpenIPMIposix.la libOpenIPMIpthread.la \
	$(top_builddir)/utils/libOpenIPMIutils.la $(GDBM_LIB)
test_handlers_CFLAGS = -Wall -Wsign-compare -I$(top_builddir)/include \
	-I$(top_srcdir)/include

TESTS = test_heap test_handlers
