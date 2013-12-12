# Makefile
TEXFILES = $(wildcard *.tex)
PDFFILES = $(TEXFILES:.tex=.pdf)

all: pdflatex clean

pdf: $(PDFFILES)

%.pdf: %.tex
	@rubber --pdf $<
	@if [ -d publish ];then mv *.pdf publish; else mkdir publish; mv *.pdf publish/;fi

pdflatex: $(TEXFILES)
	@pdflatex $(TEXFILES:.tex=)
	#@TEXMFOUTPUT=`pwd` bibtex `pwd`/$(TEXFILES:.tex=)
	@TEXMFOUTPUT=`pwd` bibtex `pwd`/publications
	@TEXMFOUTPUT=`pwd` bibtex `pwd`/theses
	@TEXMFOUTPUT=`pwd` bibtex `pwd`/reports
	@pdflatex $(TEXFILES:.tex=)
	@if [ -d publish ];then mv *.pdf publish; else mkdir publish; mv *.pdf publish/;fi

clean:
	@rubber --clean $(TEXFILES:.tex=)
	@rm -f *.out *.bbl *.blg *.aux

distclean: clean
	@rubber --clean --pdf $(TEXFILES:.tex=)
	@rm -rf publish
	@rm -f $(PDFFILES)

x:
	@open publish/$(PDFFILES) &> /dev/null &
