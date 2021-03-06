#############################################################################
# $Id$
#
# Copyright (c) 2009 Sandro Santilli <strk@keybit.net>, Pierre Racine <pierre.racine@sbf.ulaval.ca>
# Copyright (c) 2011 Jorge Arevalo <jorge.arevalo@deimos-space.com>
# Copyright (c) 2011 Regents of the University of California
#   <bkpark@ucdavis.edu>
#
# This is free software; you can redistribute and/or modify it under
# the terms of the GNU General Public Licence. See the COPYING file.
#
#############################################################################

POSTGIS_SRC=../../..

# MingW hack: rather than use PGSQL_BINDIR directly, we change
# to the directory and then use "pwd" to return the path. This
# ensures that the returned path is in MSYS format, otherwise
# colons in drive letters will break PATH.
PGSQL_BINDIR=$(shell cd "/usr/lib/postgresql/9.1/bin" && pwd)

# Where we put our regression installation
REGRESS_INSTALLDIR=$(POSTGIS_SRC)/regress/00-regress-install

#
# Put path from pg_config into front of search path
#
PATH := $(PGSQL_BINDIR):$(PATH)
export PATH

TEST_FIRST = \
	check_gdal

TEST_METADATA = \
	check_raster_columns \
	check_raster_overviews

TEST_IO = \
	rt_io

TEST_FUNC = \
	rt_bytea \
	box3d \
	rt_addband \
	rt_band \
	rt_asgdalraster \
	rt_astiff \
	rt_asjpeg \
	rt_aspng \
	rt_union

TEST_PROPS = \
	create_rt_properties_test \
	rt_dimensions \
	rt_scale \
	rt_pixelsize \
	rt_upperleft \
	rt_rotation \
	rt_georeference \
	rt_set_properties \
	drop_rt_properties_test \
	create_rt_empty_raster_test \
	rt_isempty \
	rt_hasnoband \
	drop_rt_empty_raster_test \
	rt_metadata

TEST_BANDPROPS = \
	create_rt_band_properties_test \
	rt_band_properties \
	rt_set_band_properties \
	rt_summarystats \
	rt_count \
	rt_histogram \
	rt_quantile \
	rt_valuecount \
	rt_valuepercent \
	rt_bandmetadata \
	rt_pixelvalue \
	drop_rt_band_properties_test

TEST_UTILITY = \
	rt_utility \
	create_rt_mapalgebra_test \
	rt_mapalgebraexpr \
	rt_mapalgebrafct \
	rt_mapalgebraexpr_2raster \
	rt_mapalgebrafct_2raster \
	drop_rt_mapalgebra_test \
	create_rt_mapalgebrafctngb_test \
	rt_mapalgebrafctngb \
	rt_mapalgebrafctngb_userfunc \
	drop_rt_mapalgebrafctngb_test \
	rt_reclass \
	rt_resample \
	rt_asraster \
	rt_intersection \
	rt_clip

TEST_GIST = \
	create_rt_gist_test \
	rt_above \
	rt_below \
	rt_contained \
	rt_contain \
	rt_left \
	rt_overabove \
	rt_overbelow \
	rt_overlap \
	rt_overleft \
	rt_overright \
	rt_right \
	rt_same \
	drop_rt_gist_test
	
TEST_SREL = \
	rt_spatial_relationship \
	rt_intersects \
	rt_samealignment
	
TEST_BUGS = \
	bug_test_car5 \
	tickets

TEST_LOADER = \
	loader/Basic \
	loader/BasicCopy \
	loader/Tiled10x10 \
	loader/Tiled10x10Copy

TESTS = $(TEST_FIRST) $(TEST_METADATA) $(TEST_IO) $(TEST_FUNC) \
		$(TEST_PROPS) $(TEST_BANDPROPS) \
		$(TEST_UTILITY) $(TEST_GIST) $(TEST_SREL) \
		$(TEST_BUGS) \
		$(TEST_LOADER)

all:
	@echo "Use 'make check' to run all tests"

distclean: clean
	rm -f Makefile

clean:
	$(RM) -f rtpostgis.sql

rtpostgis.sql: ../../rt_pg/rtpostgis.sql
	sed 's,$$libdir,$(REGRESS_INSTALLDIR)/lib,g' ../../rt_pg/rtpostgis.sql > rtpostgis.sql

check: 
	$(MAKE) -C ../../../regress staged-install
	../../../regress/run_test --raster $(RUNTESTFLAGS) $(TESTS)
	../../../regress/run_test --upgrade --raster $(RUNTESTFLAGS) $(TESTS)

#all: run_test

#run_test: run_test.in Makefile
#	sed -e "s#@POSTGIS_SRC@#$(POSTGIS_SRC)#" $< > $@
#	chmod +x $@

#post-install-check check: run_test
#	./run_test $(TESTS)

#clean:
#	$(RM) run_test
#	$(RM) testgdalraster

testgdalraster:
	chmod +x $@
	chmod +x ../../scripts/python/rtgdalraster.py
	./testgdalraster
