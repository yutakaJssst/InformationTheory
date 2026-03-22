MAIN = ai_research
BIBS = bu1 bu2 bu3 bu4 bu5 bu6 bu7 bu8 bu9 bu10

.PHONY: all clean

all: $(MAIN).pdf

$(MAIN).pdf: $(MAIN).tex contents/*.tex references.bib
	platex $(MAIN).tex
	for b in $(BIBS); do bibtex $$b.aux 2>/dev/null || true; done
	mendex -U $(MAIN).idx 2>/dev/null || true
	platex $(MAIN).tex
	platex $(MAIN).tex
	dvipdfmx $(MAIN).dvi

clean:
	rm -f *.aux *.log *.dvi *.toc *.out *.idx *.ilg *.ind *.bbl *.blg *.fls *.synctex.gz bu*.aux bu*.bbl bu*.blg
