#
# %CopyrightBegin%
#
# Copyright Ericsson AB 1997-2021. All Rights Reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# %CopyrightEnd%
#
#

include $(ERL_TOP)/make/target.mk
include $(ERL_TOP)/make/$(TARGET)/otp.mk

# ----------------------------------------------------
# Application version
# ----------------------------------------------------
include $(ERL_TOP)/erts/vsn.mk

APPLICATION=otp-system-documentation
XMLDIR := $(XMLDIR)/design_principles

# ----------------------------------------------------
# Release directory specification
# ----------------------------------------------------
RELSYSDIR = $(RELEASE_PATH)/doc/design_principles

# ----------------------------------------------------
# Target Specs
# ----------------------------------------------------
XML_PART_FILES = part.xml

include xmlfiles.mk

XML_CHAPTER_FILES=$(DESIGN_PRINCIPLES_CHAPTER_FILES)

TOPDOCDIR=..

BOOK_FILES = book.xml

GIF_FILES = \
	clientserver.gif \
	dist1.gif \
	dist2.gif \
	dist3.gif \
	dist4.gif \
	dist5.gif \
	inclappls.gif \
	sup6.gif

SVG_FILES = \
	code_lock.svg \
	code_lock_2.svg \
	sup-one_for_all.svg \
	sup-one_for_one.svg \
	sup-rest_for_one.svg

IMAGE_FILES = $(GIF_FILES) $(SVG_FILES)

XML_FILES = \
	$(BOOK_FILES) $(XML_CHAPTER_FILES) \
	$(XML_PART_FILES)

# ----------------------------------------------------

HTML_FILES = \
	$(XML_PART_FILES:%.xml=%.html)

HTMLDIR = ../html/design_principles

HTML_UG_FILE = $(HTMLDIR)/users_guide.html

# ----------------------------------------------------
# FLAGS
# ----------------------------------------------------
XML_FLAGS +=
DVIPS_FLAGS +=

# ----------------------------------------------------
# Targets
# ----------------------------------------------------

$(HTMLDIR)/%.gif: %.gif
	$(INSTALL_DATA) $< $@

$(HTMLDIR)/%.svg: %.svg
	$(INSTALL_DATA) $< $@

DOC_TARGETS?=html

docs: $(DOC_TARGETS)

local_docs: PDFDIR=../../pdf

html: $(HTML_UG_FILE) images

images: $(IMAGE_FILES:%=$(HTMLDIR)/%)

debug opt:

clean clean_docs:
	rm -f $(XMLDIR)/*.xml
	rm -f $(HTMLDIR)/*.gif $(HTMLDIR)/*.html
	rm -f $(TOP_PDF_FILE) $(TOP_PDF_FILE:%.pdf=%.fo)
	rm -f errs core *~

# ----------------------------------------------------
# Release Target
# ----------------------------------------------------
include $(ERL_TOP)/make/otp_release_targets.mk

release_html_spec: html
	$(INSTALL_DIR) "$(RELSYSDIR)"
	$(INSTALL_DATA) $(IMAGE_FILES) $(EXTRA_FILES) $(HTMLDIR)/*.html \
		"$(RELSYSDIR)"

release_docs_spec: $(DOC_TARGETS:%=release_%_spec)

release_spec:
