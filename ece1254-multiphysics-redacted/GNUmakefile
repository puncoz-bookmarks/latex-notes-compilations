THISDIR := ece1254-multiphysics-redacted
THISBOOK := ece1254
ORIGDIR := ece1254-multiphysics

#VER := $(shell grep Version ../$(ORIGDIR)/.revinfo/gitCommitDateAsMyTime.tex | sed 's/.*{//;s/.xspace.*//;')

include ../$(ORIGDIR)/make.revision
include ../latex/make.bookvars

THISBOOK_DEPS += kbordermatrix.sty

INCOMPLETE += multiphysicsProblemSet1Problem1.tex
INCOMPLETE += multiphysicsProblemSet1Problem2.tex
INCOMPLETE += multiphysicsProblemSet1Problem3.tex
INCOMPLETE += multiphysicsProblemSet2aProblem1.tex
INCOMPLETE += multiphysicsProblemSet2bProblem1.tex
INCOMPLETE += multiphysicsProblemSet2bProblem2.tex

#ONCEFLAGS := -justonce

SOURCE_DIRS += appendix
FIGURES := ../figures/$(ORIGDIR)
SOURCE_DIRS += $(FIGURES)

# also toggle redacted classicthesis-config.tex
# FIXME: changing this flag should be a dependency of matlab.tex 
REDACTED := -redacted

GENERATED_SOURCES += matlab.tex 
GENERATED_SOURCES += mathematica.tex 

# rules for mathematica.tex, ... output to $(THISDIR) explicitly.  Depend on those files being generated first in ../ece1254
#ECE1254TEX := $(filter-out $(GENERATED_SOURCES),$(notdir $(wildcard ../$(THISBOOK)/*.tex)))

ECE1254TEX := $(notdir $(wildcard ../$(ORIGDIR)/*.tex))
ECE1254TEX += FrontBackmatter/preface.tex
ECE1254STY := thisbook.sty

THISBOOK_DEPS += $(GENERATED_SOURCES)
THISBOOK_DEPS += $(ECE1254TEX)
THISBOOK_DEPS += $(ECE1254STY)
THISBOOK_DEPS += $(PDFS_FROM_EPS)

include ../latex/make.rules

LATEXMK := ../latex/bin/make_pdflatex --oldscript -filename

$(ECE1254TEX) : %.tex : ../$(ORIGDIR)/%.tex
	mkdir -p $(dir $@)
	cp $< $@

$(ECE1254STY) : %.sty : ../$(ORIGDIR)/%.sty
	cp $< $@

clean ::
	rm -f $(ECE1254TEX) $(ECE1254STY)

myrefs.bib : 
	(cd ../$(ORIGDIR) ; make myrefs.bib)
	cp ../$(ORIGDIR)/myrefs.bib .
