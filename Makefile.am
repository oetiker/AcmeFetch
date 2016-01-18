#  Copyright (C) 2015 Tobias Oetiker

AUTOMAKE_OPTIONS =  foreign

MJ_SCRIPT = acmefetch

SUBDIRS = thirdparty etc

BIN = bin/$(MJ_SCRIPT)

THIRDPARTY_DIR := $(shell pwd)/thirdparty

EXTRA_DIST = VERSION PERL_MODULES COPYRIGHT LICENSE CHANGES AUTHORS bootstrap README.md $(BIN)

CHANGES: VERSION
	git log --simplify-merges --full-history --no-merges --pretty=format:'%ai %d  %s -- %an' > CHANGES

YEAR := $(shell date +%Y)
DATE := $(shell date +%Y-%m-%d)

datadir = $(prefix)

README: README.md
	cp README.md README
	
dist_bin_SCRIPTS = $(BIN)

dist-hook: thirdparty/CPAN/touch
	$(PERL) -i -p -e 's/#VERSION#/$(PACKAGE_VERSION)/g;s/#YEAR#/$(YEAR)/g;s/#DATE#/$(DATE)/g;'  $(distdir)/README.md $(distdir)/COPYRIGHT

install-exec-hook:
	[ "$(PERL5LIB)" == "" ] || cd "$(DESTDIR)$(exec_prefix)" && $(PERL) -i -p -e 's{.*# PERL5LIB}{use lib qw($(PERL5LIB)); # PERL5LIB}' $(BIN) || true
	cd "$(DESTDIR)$(exec_prefix)" && $(PERL) -i -p -e 's{.*# LIBDIR}{use lib qw($(libdir)); # LIBDIR}' $(BIN)
	cd "$(DESTDIR)$(exec_prefix)" && $(PERL) -i -p -e 's{^#!.*perl.*}{#!$(PERL)};' $(BIN)
	[ ! -d $(THIRDPARTY_DIR)/lib/perl5 ] || cp -fr $(THIRDPARTY_DIR)/lib/perl5/* $(DESTDIR)$(libdir)
