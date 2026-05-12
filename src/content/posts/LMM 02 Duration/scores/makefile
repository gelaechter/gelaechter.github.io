# This makefile generates mp3 and svg files for each mscz
MSCZ_FILES := $(wildcard *.mscz)
MP3_FILES := $(MSCZ_FILES:.mscz=.mp3)
SVG_FILES := $(MSCZ_FILES:.mscz=.svg)

all: $(MP3_FILES) $(SVG_FILES)

# Rule to generate mp3 from .mscz
%.mp3: %.mscz
	@echo "Generating mp3 for $*"
	mscore "$<" -o "$@"
	@clear

# Rule to generate svg from .mscz (intermediate file output.svg is handled)
%.svg: %.mscz
	@echo "Generating svg for $*"
	mscore "$<" -o output.svg
	@clear
	@echo "Transforming svg for $*"
	mv output-1.svg "$@"
	inkscape "$@" --export-overwrite --batch-process --actions="select-by-id:path1;delete;select-all;transform-scale:100000.0;page-fit-to-selection;"
	@clear

.PHONY: clean

clean:
	rm -f $(MP3_FILES) $(SVG_FILES)
