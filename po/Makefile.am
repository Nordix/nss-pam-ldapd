# Makefile.am - use automake to generate Makefile.in
#
# Copyright (C) 2024 OpenInfra Foundation Europe and others.
#
# This library is free software; you can redistribute it and/or
# modify it under the terms of the GNU Lesser General Public
# License as published by the Free Software Foundation; either
# version 2.1 of the License, or (at your option) any later version.
#
# This library is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# Lesser General Public License for more details.
#
# You should have received a copy of the GNU Lesser General Public
# License along with this library; if not, write to the Free Software
# Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA
# 02110-1301 USA

# Usage:
#
# Regenerate the pot file for the project:
#   make pot
#
# Recompile the po files to gmo files:
#   make gmo
#
# Create new translation (po file):
#   msginit --locale=[locale]
#
# Update existing translation with new messages:
#   msgmerge --update [po file] nss-pam-ldapd.pot
#

# List of source files containing translatable strings.
POTFILES = $(top_srcdir)/pam/pam.c

# List of languages to generate translations for.
LINGUAS = fi sv

POTFILE = $(PACKAGE).pot
POFILES = $(LINGUAS:=.po)
GMOFILES = $(LINGUAS:=.gmo)

# Files to include when running make dist.
EXTRA_DIST = $(POTFILE) $(POFILES) $(GMOFILES)

# Files to clean when running make clean.
CLEANFILES = $(GMOFILES)

all: gmo

pot: $(POTFILE)
gmo: $(GMOFILES)

$(POTFILE): $(POTFILES)
	xgettext --keyword=_ --language=C --add-comments --sort-output -o $@ $(POTFILES)

$(GMOFILES): %.gmo: %.po
	msgfmt -c -o $@ $<

install-data-local:
	for lang in $(LINGUAS) ; do \
	  $(MKDIR_P) $(DESTDIR)$(localedir)/$$lang/LC_MESSAGES ; \
	  $(INSTALL) $$lang.gmo $(DESTDIR)$(localedir)/$$lang/LC_MESSAGES/$(PACKAGE).mo ; \
	done
