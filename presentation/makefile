UNAME := $(shell uname -s)
REL=bash
PDF=$(REL).pdf
TEX=$(REL).tex

all:$(PDF)

# Compile the PDF file
$(PDF):$(TEX) $(SECS)
ifeq ($(UNAME),Darwin)
	latexmk -e '$$pdflatex=q/pdflatex -synctex=1 %T/' -pdf $(TEX)
endif
ifeq ($(UNAME),Linux)
	latexmk -pdf $(TEX)
endif

# Silly rules
$(SUBSECS):
$(SECS):

# open PDF file
open:$(PDF)
ifeq ($(UNAME),Darwin)
	open $(PDF)
endif
ifeq ($(UNAME),Linux)
	xpdf $(PDF)
endif

# Clean rules
clean:
	@echo "Cleaning the shop"
	@find . -maxdepth 1 \(  \! -iname "*.pdf" \! -iname README* \! -iname .gitignore \! -iname "*.bib" \! -iname "*.tex" -type f \! -iname "makefile" \! -iname "*.sty" \! -iname "*.cls" \) -exec rm '{}' \;
	@find . \( -name *~ -or -name *.*~ \) -exec rm '{}' \;

cleanAll:
	@echo "Cleaning the shop"
	@find . -maxdepth 1 \( \! -iname README* \! -iname .gitignore \! -iname "*.bib" \! -iname "*.tex" -type f \! -iname "makefile" \! -iname "*.sty" \! -iname "*.cls" \) -exec rm '{}' \;
	@find . \( -name *~ -or -name *.*~ \) -exec rm '{}' \;












# extra
me:
	latex  $(REL)
	bibtex $(REL)
	latex  $(REL)
	latex  $(REL)
	make open
	make clean

update:
	git pull
	git commit -a
	git push
