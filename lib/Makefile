# SPDX-License-Identifier: LGPL-2.1-or-later

LIBNAME = libdattobd.so
SOVER = 1
SHARED_CCFLAGS = -fPIC -lc -shared -Wl,-soname,$(LIBNAME).$(SOVER)

SOURCES = libdattobd.c
ifeq (,$(wildcard /etc/debian_version))
	# rpm-based system
	LIBDIR = $(PREFIX)/lib64
else
	# Debian-based system
	LIBDIR = $(PREFIX)/lib
endif

.PHONY: all shared static install uninstall clean

all: shared static

shared:
	$(CC) $(CCFLAGS) $(SHARED_CCFLAGS) $(SOURCES) -o $(LIBNAME).$(SOVER)
	ln -sf $(LIBNAME).$(SOVER) $(LIBNAME)

static:
	$(CC) $(CCFLAGS) -c $(SOURCES)
	ar rcs libdattobd.a libdattobd.o

install: shared
	install $(LIBNAME).$(SOVER) $(LIBDIR)
	install $(LIBNAME) $(LIBDIR)
	ldconfig

uninstall:
	$(RM) $(LIBDIR)/$(LIBNAME)
	$(RM) $(LIBDIR)/$(LIBNAME).$(SOVER)
	ldconfig

clean:
	$(RM) *.a *.o *.so*
