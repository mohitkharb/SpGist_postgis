#############################################################################
# $Id: Makefile.in 9523 2012-03-21 21:36:59Z pramsey $
#
# Copyright (c) 2009 Pierre Racine <pierre.racine@sbf.ulaval.ca>
#
# This is free software; you can redistribute and/or modify it under
# the terms of the GNU General Public Licence. See the COPYING file.
#
#############################################################################
CP = cp -p

# Filenames with extension as determined by the OS
RASTER2PGSQL=raster2pgsql.py

# PostgreSQL executable directory
PGSQL_BINDIR=/usr/lib/postgresql/9.1/bin

all:

install:
#	$(CP) $(RASTER2PGSQL) $(DESTDIR)$(PGSQL_BINDIR)/$(RASTER2PGSQL)

uninstall:
#	$(RM) $(DESTDIR)$(PGSQL_BINDIR)/$(RASTER2PGSQL)

clean:
	rm -f *.o

distclean: clean
	rm -f Makefile
