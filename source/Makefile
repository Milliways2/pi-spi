#
# Makefile:
#	pi-spi library for the Raspberry Pi
#

VERSION=$(shell cat ../VERSION)
DESTDIR?=/usr
PREFIX?=/local
PYLIB?=/usr/lib/python3/dist-packages

LDCONFIG?=ldconfig
V=1
ifneq ($V,1)
Q ?= @
endif

LIBNAME=pi-spi

DYNAMIC=lib$(LIBNAME).so.$(VERSION)

#DEBUG	= -g -O0
DEBUG	= -O2
INCLUDE	= -I.
DEFS	= -D_GNU_SOURCE
CFLAGS	= $(DEBUG) $(DEFS) -Wformat=2 -Wall -Wextra -Winline $(INCLUDE) -pipe -fPIC
LIBS    = -lm -lpthread -lrt -lcrypt

###############################################################################

SRC	=	spi.c

HEADERS = $(LIBNAME).h
MANPAGES = $(LIBNAME).3


OBJ	=	$(SRC:.c=.o)

all:		$(DYNAMIC)

$(DYNAMIC):	$(OBJ)
	$Q $(CC) -shared -Wl,-soname,lib$(LIBNAME).so -o lib$(LIBNAME).so.$(VERSION) $(LIBS) $(OBJ)

.c.o:
	@ echo [Compile] $<
	$Q $(CC) -c $(CFLAGS) $< -o $@

.PHONY:	clean
clean:
	@ echo "[Clean]"
	$Q rm -f $(OBJ) $(OBJ_spi) *~ core tags lib$(LIBNAME).*

.PHONY:	install
install:	$(DYNAMIC)
	@ echo "[Install Headers]"
	$Q install -m 0755 -d						$(DESTDIR)$(PREFIX)/include
	$Q install -m 0644 $(HEADERS)					$(DESTDIR)$(PREFIX)/include

	@ echo "[Install Dynamic Lib]"
	$Q install -m 0755 -d						$(DESTDIR)$(PREFIX)/lib
	$Q install -m 0755 lib$(LIBNAME).so.$(VERSION)			$(DESTDIR)$(PREFIX)/lib/lib$(LIBNAME).so.$(VERSION)
	$Q ln -sf $(DESTDIR)$(PREFIX)/lib/lib$(LIBNAME).so.$(VERSION)	$(DESTDIR)/lib/lib$(LIBNAME).so
	$Q $(LDCONFIG)

	@ echo "[Install man pages]"
	$Q mkdir -p		$(DESTDIR)$(PREFIX)/share/man/man3
	$Q install -m 0644 $(MANPAGES) 	$(DESTDIR)$(PREFIX)/share/man/man3

	@ echo "[Install python overlays]"
	mkdir -p $(PYLIB)
	install -m 0644 pi_spi.py 	$(PYLIB)/pi_spi.py

.PHONY:	uninstall
uninstall:
	@ echo "[UnInstall]"
	$Q cd $(DESTDIR)$(PREFIX)/include/ && rm -f $(HEADERS)
	$Q cd $(DESTDIR)$(PREFIX)/lib/     && rm -f lib$(LIBNAME).*
	$Q $(LDCONFIG)

	$Q cd $(DESTDIR)$(PREFIX)/share/man/man3/     && rm -f $(MANPAGES)
