all: clean epo.pdf test 

epo.fomabin: epo.foma *.lexc
	foma -l epo.foma -e "save stack epo.fomabin" -s

epo.dot: epo.foma *.lexc
	foma -l epo.foma -e "print dot > epo.dot" -s

epo.pairs: epo.foma *.lexc
	foma -l epo.foma -e "pairs > epo.pairs" -s

epo.pdf: epo.dot
	dot -Tpdf epo.dot > epo.pdf


interactive: epo.foma *.lexc
	foma -l epo.foma



test: test-Ch4.2.8

test-%: epo.%.tsv epo.fomabin
	@cut -f 1 epo.$*.tsv     | sort -d -f | uniq | flookup -i -w "" epo.fomabin | sort -d -f | diff - epo.$*.tsv     && echo "PASS" || echo "FAIL"


clean:
	rm -f epo.dot epo.pdf *.pairs *.pairs.tsv *.fomabin


bases.tsv: bases.tab
	cat bases.tab | sed 's,\r,\n,g' | sed 's,\v, ,g' > bases.tsv

.PHONY: all interactive clean test test-ch2
