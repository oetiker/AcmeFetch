#  Copyright (C) 2015 Tobias Oetiker

AUTOMAKE_OPTIONS =  foreign

SUFFIXES = .1 .man

MJ_SCRIPT = acmefetch

SUBDIRS = thirdparty etc

BIN = bin/$(MJ_SCRIPT)

THIRDPARTY_DIR := $(shell pwd)/thirdparty

MAN = man/$(MJ_SCRIPT).1
POD = doc/$(MJ_SCRIPT).pod

EXTRA_DIST = VERSION PERL_MODULES COPYRIGHT LICENSE CHANGES AUTHORS bootstrap README.md $(BIN) $(POD)

CHANGES: VERSION
	git log --simplify-merges --full-history --no-merges --pretty=format:'%ai %d  %s -- %an' > CHANGES

YEAR := $(shell date +%Y)
DATE := $(shell date +%Y-%m-%d)

datadir = $(prefix)

README: README.md
	cp README.md README

imandir = $(mandir)/man1
iman_DATA = $(MAN)

doc/%.pod: bin/% VERSION
	$(AM_V_GEN)mkdir -p doc;grep -A100000 '=head1 NAME' $< > $@

man/%.1: bin/% VERSION
	$(AM_V_GEN)mkdir -p man; test $(POD2MAN) = "no" || $(POD2MAN) --release=$(VERSION) --center=$(PACKAGE_NAME) $<  > $@

dist_bin_SCRIPTS = $(BIN)

dist-hook: $(POD)
	$(PERL) -i -p -e 's/#VERSION#/$(PACKAGE_VERSION)/g;s/#YEAR#/$(YEAR)/g;s/#DATE#/$(DATE)/g;'  $(distdir)/README.md $(distdir)/COPYRIGHT
	$(PERL) -i -p -e 's/^my .*# VERSION/my \$$VERSION = q{$(PACKAGE_VERSION)}; # VERSION/' $(distdir)/$(BIN)

install-exec-hook:
	[ "$(PERL5LIB)" = "" ] || cd "$(DESTDIR)$(exec_prefix)" && $(PERL) -i -p -e 's{.*# PERL5LIB}{use lib qw($(PERL5LIB)); # PERL5LIB}' $(BIN) || true
	cd "$(DESTDIR)$(exec_prefix)" && $(PERL) -i -p -e 's{^use .*# LIBDIR}{use lib qw($(libdir)); # LIBDIR}' $(BIN)
	cd "$(DESTDIR)$(exec_prefix)" && $(PERL) -i -p -e 's{^#!.*perl.*}{#!$(PERL)};' $(BIN)
	mkdir -p $(DESTDIR)$(libdir)
	[ ! -d $(THIRDPARTY_DIR)/lib/perl5 ] || cp -fr $(THIRDPARTY_DIR)/lib/perl5/* $(DESTDIR)$(libdir)
