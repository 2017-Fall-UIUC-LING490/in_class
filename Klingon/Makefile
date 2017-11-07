all: clean tlh.pdf test 

tlh.fomabin: tlh.foma *.lexc
	foma -l tlh.foma -e "save stack tlh.fomabin" -s

tlh.dot: tlh.foma *.lexc
	foma -l tlh.foma -e "print dot > tlh.dot" -s

tlh.pairs: tlh.foma *.lexc
	foma -l tlh.foma -e "pairs > tlh.pairs" -s

tlh.pdf: tlh.dot
	dot -Tpdf tlh.dot > tlh.pdf


interactive: tlh.foma *.lexc
	foma -l tlh.foma



test: test-Ch4.2.8

test-%: tlh.%.tsv tlh.fomabin
	@cut -f 1 tlh.$*.tsv     | sort -d -f | uniq | flookup -i -w "" tlh.fomabin | sort -d -f | diff - tlh.$*.tsv     && echo "PASS" || echo "FAIL"


clean:
	rm -f tlh.dot tlh.pdf *.pairs *.pairs.tsv *.fomabin


bases.tsv: bases.tab
	cat bases.tab | sed 's,\r,\n,g' | sed 's,\v, ,g' > bases.tsv

.PHONY: all interactive clean test test-ch2
