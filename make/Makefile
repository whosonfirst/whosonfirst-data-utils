WHOAMI = $(shell basename `pwd`)

count:
	find ./data -name '*.geojson' -print | wc -l

prune:
	git gc --aggressive --prune

archive:
	tar --exclude='.git' -cvjf $(dest)/$(WHOAMI)-`date "+%Y%m%d"`.bz2 ./

list-empty:
	find data -type d -empty -print

rm-empty:
	find data -type d -empty -print -delete

# https://github.com/whosonfirst/go-whosonfirst-concordances
# Note: this does not bother to check whether the newly minted
# `wof-concordances-tmp.csv` file is the same as any existing
# `wof-concordances-latest.csv` file. It should but it doesn't.
# (20160420/thisisaaronland)

concordances:
	wof-concordances-write -processes 100 -source ./data > meta/wof-concordances-tmp.csv
	mv meta/wof-concordances-tmp.csv meta/wof-concordances-$(YMD).csv
	cp meta/wof-concordances-$(YMD).csv meta/wof-concordances-latest.csv
