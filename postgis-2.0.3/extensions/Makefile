#############################################################################
#
# Master makefile used to build extensions
#
# Copyright (C) 2012 Sandro Santilli <strk@keybit.net>
#
# This is free software; you can redistribute and/or modify it under
# the terms of the GNU General Public Licence. See the COPYING file.
#
#############################################################################

SUBDIRS = postgis 

ifeq (topology,topology)
	SUBDIRS += postgis_topology
endif

all clean distclean install uninstall:
	for DIR in $(SUBDIRS); do \
		echo "---- Making $@ in $${DIR}"; \
		$(MAKE) -C "$${DIR}" $@; \
	done

distclean: distclean-local

distclean-local:
	rm -f Makefile


check:
	@echo "Nothing to check"

