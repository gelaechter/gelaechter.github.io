# This makefile generates mp3 and svg files for each mscz
MSCZ_FILES := $(wildcard **/*.mscz)
MP3_FILES := $(MSCZ_FILES:.mscz=.mp3)
PDF_FILES := $(MSCZ_FILES:.mscz=.pdf)

all: $(MP3_FILES) $(PDF_FILES)

# Rule to generate mp3 from .mscz
%.mp3: %.mscz
	@echo "Generating mp3 for $*"
	mscore "$<" -o "$@.midi"
# Pianoteq needs lame
	ln -sf $$(command -v lame) ./lame 
	pianoteq-stage9 --headless --midi "$@.midi" --mp3 "$@"
	rm "$@.midi"
	rm ./lame
	@clear

# Rule to generate pdf from .mscz
%.pdf: %.mscz
	@echo "Generating pdf for $*"
	mscore "$<" -o "$@"
	@clear

.PHONY: clean

clean:
	rm -f $(MP3_FILES) $(PDF_FILES)
