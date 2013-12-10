BIB  = refs.bib theses.bib reports.bib licenses.bib csrg.bib url.bib
ALL  = refs,theses,reports,licenses,csrg,url
TEX  = allbib.tex $(BIB:.bib,.tex)
EXTS = aux bbl blg dvi log

all: $(TEX:.tex=.pdf)

allbib.pdf:  allbib.tex $(BIB:.bib=.pdf)
%.pdf:    %.tex %.bib

$(BIB:.bib=.tex): skeleton.tex

clean:
	rm -f $(foreach ext,$(EXTS),$(TEX:.tex=.$(ext)))
	rm -f $(TEX)

distclean: clean
	rm -f $(TEX:.tex=.pdf)

.PHONY: all clean distclean

allbib.tex: $(BIB) skeleton.tex
	-rm -f $@
	perl -p -e 's/%%TITLE%%/Full Bibliography/; \
                    s/%%BIBS HERE%%/$(ALL)/' skeleton.tex > $@

%.tex: %.bib skeleton.tex
	-rm -f $@
	perl -p -e \
          's/%%TITLE%%/ucfirst("$(basename $<)") . " Publications"/e; \
           s/%%BIBS HERE%%/$(basename $<)/' skeleton.tex > $@

%.pdf: %.tex
	pdflatex -halt-on-error $<
	BIBINPUTS=. bibtex $(basename $<)
	pdflatex -halt-on-error $<
	pdflatex -halt-on-error $<
