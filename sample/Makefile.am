
AM_CFLAGS = -Wall -Wsign-compare -I$(top_builddir)/include \
	-I$(top_srcdir)/include -DIPMI_CHECK_LOCKS

if HAVE_OPENIPMI_SMI
CMDHANDLER = linux_cmd_handler
EVENTD = openipmi_eventd
else
CMDHANDLER =
EVENTD =
endif

bin_PROGRAMS = openipmicmd solterm rmcp_ping $(EVENTD)

noinst_PROGRAMS = ipmisample ipmisample2 ipmisample3 ipmi_serial_bmc_emu \
		  ipmi_dump_sensors waiter_sample $(CMDHANDLER)
EXTRA_PROGRAMS = linux_cmd_handler openipmi_eventd

linux_cmd_handler_SOURCES = linux_cmd_handler.c

ipmisample_SOURCES = sample.c
ipmisample_LDADD = $(top_builddir)/utils/libOpenIPMIutils.la \
		$(top_builddir)/lib/libOpenIPMI.la \
		$(top_builddir)/unix/libOpenIPMIposix.la \
		$(OPENSSLLIBS)

ipmisample2_SOURCES = sample2.c
ipmisample2_LDADD = $(top_builddir)/utils/libOpenIPMIutils.la \
		$(top_builddir)/lib/libOpenIPMI.la \
		$(top_builddir)/unix/libOpenIPMIpthread.la \
		-lpthread $(OPENSSLLIBS)

ipmisample3_SOURCES = sample3.c
ipmisample3_LDADD = $(top_builddir)/utils/libOpenIPMIutils.la \
		$(top_builddir)/lib/libOpenIPMI.la \
		$(top_builddir)/unix/libOpenIPMIposix.la \
		$(OPENSSLLIBS)

waiter_sample_SOURCES = waiter_sample.c
waiter_sample_LDADD = $(top_builddir)/utils/libOpenIPMIutils.la \
		$(top_builddir)/lib/libOpenIPMI.la \
		$(top_builddir)/unix/libOpenIPMIposix.la \
		$(OPENSSLLIBS)

openipmi_eventd_SOURCES = eventd.c
openipmi_eventd_LDADD = $(top_builddir)/utils/libOpenIPMIutils.la \
		$(top_builddir)/lib/libOpenIPMI.la \
		$(top_builddir)/unix/libOpenIPMIposix.la \
		$(OPENSSLLIBS)

ipmi_dump_sensors_SOURCES = dump_sensors.c
ipmi_dump_sensors_LDADD = $(top_builddir)/utils/libOpenIPMIutils.la \
		$(top_builddir)/lib/libOpenIPMI.la \
		$(top_builddir)/unix/libOpenIPMIposix.la \
		$(OPENSSLLIBS)

if HAVE_GLIB
def_os_hnd = $(top_builddir)/glib/libOpenIPMIglib.la
else
def_os_hnd = $(top_builddir)/unix/libOpenIPMIposix.la
endif

openipmicmd_SOURCES = ipmicmd.c
openipmicmd_LDADD = $(top_builddir)/utils/libOpenIPMIutils.la \
		$(top_builddir)/lib/libOpenIPMI.la $(def_os_hnd) \
		$(OPENSSLLIBS)

solterm_SOURCES = solterm.c
solterm_LDADD = $(POPTLIBS) $(top_builddir)/utils/libOpenIPMIutils.la \
                $(top_builddir)/lib/libOpenIPMI.la $(def_os_hnd) \
                $(OPENSSLLIBS)

rmcp_ping_SOURCES = rmcp_ping.c
rmcp_ping_LDADD = $(SOCKETLIB)

ipmi_serial_bmc_emu_SOURCES = ipmi_serial_bmc_emu.c
ipmi_serial_bmc_emu_LDADD = $(READLINE_LIBS) $(TERM_LIBS) $(SOCKETLIB)
ipmi_serial_bmc_emu_CFLAGS = -I $(top_srcdir)/libedit -I $(top_srcdir)/include

EXTRA_DIST = example_oem.c

# We need to make a link from ipmicmd to openipmicmd for backwards
# compatability.
install-exec-hook:
	rm -f $(DESTDIR)$(bindir)/ipmicmd
	$(LN_S) openipmicmd $(DESTDIR)$(bindir)/ipmicmd

uninstall-local:
	rm -f $(DESTDIR)$(bindir)/ipmicmd
