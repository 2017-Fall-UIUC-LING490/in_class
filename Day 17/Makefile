
all: epo.fomabin epo.pairs epo.pdf

epo.fomabin: epo.foma epo.lexc
	foma -l epo.foma -e "save stack epo.fomabin" -s

epo.dot: epo.foma epo.lexc
	foma -l epo.foma -e "print dot > epo.dot" -s

epo.pairs: epo.foma epo.lexc
	foma -l epo.foma -e "pairs > epo.pairs" -s

epo.pdf: epo.dot
	dot -Tpdf epo.dot > epo.pdf

interactive:
	foma -l epo.foma

test: epo.foma epo.lexc epo.pairs.gold
	cut -f 1 epo.pairs.gold | sort -d -f | flookup -i -w "" epo.fomabin | sort -d -f | diff - epo.pairs.gold

clean:
	rm -f epo.dot epo.pdf epo.fomabin epo.pairs


.PHONY: all interactive clean test
