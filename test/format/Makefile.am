AM_CPPFLAGS = -DBERKELEY_DB_PATH=\"$(BERKELEY_DB_PATH)\" \
	-I$(top_builddir) -I$(top_srcdir)/src/include \
	-I$(BERKELEY_DB_PATH)/include

noinst_PROGRAMS = t
noinst_SCRIPTS = s_dumpcmp
t_SOURCES =\
	config.h format.h backup.c bdb.c bulk.c compact.c config.c ops.c \
	salvage.c t.c util.c wts.c

t_LDADD = $(top_builddir)/libwiredtiger.la -L$(BERKELEY_DB_PATH)/lib -ldb
t_LDFLAGS = -static

#noinst_LTLIBRARIES = lzo_compress.la

# libtool hack: noinst_LTLIBRARIES turns off building shared libraries as well
# as installation, it will only build static libraries.  As far as I can tell,
# the "approved" libtool way to turn them back on is by adding -rpath.
#lzo_compress_la_SOURCES = lzo_compress.c
#lzo_compress_la_LIBADD = -llzo2 -lm
#lzo_compress_la_LDFLAGS = -avoid-version -module -rpath /nowhere

s_dumpcmp: $(srcdir)/s_dumpcmp.sh
	cp $(srcdir)/s_dumpcmp.sh $@
	chmod +x $@

backup:
	rm -rf BACKUP && cp -p -r RUNDIR BACKUP
refresh:
	rm -rf RUNDIR && cp -p -r BACKUP RUNDIR

TESTS = smoke.sh

clean-local:
	rm -rf RUNDIR *.core
