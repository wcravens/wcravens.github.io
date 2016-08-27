#  I make use of the inkscape command line version and on OSX it's a bit
#  nasty.
#	 So in here we make use of an INKSCAPE variable so that the user can set explicitely
#  e.g.
#  INKSCAPE=/Applications/Inkscape.app/Contents/Resources/bin/inkscape-bin make
#  We also have to be very explicite about path names because of this hence $(realpath ...) and $(shell pwd)
#  I don't think that these will impact linux but I haven't tried it yet.

default: \
	build/img/icons \
	build/img/logos \
	build/Quill_and_Shadow_Clipped.png \
	build/Quill_and_Shadow_Square.png \
	build/img/icons/last_built \
	build/img/logos/last_built 

build/img/icons:
	mkdir -p build/img/icons

build/img/logos:
	mkdir -p build/img/logos

build/Quill_and_Shadow_Clipped.png: $(realpath Quill.svg)
	$(INKSCAPE) -e $(shell pwd)/build/Quill_and_Shadow_Clipped.png \
		-y 0 -z -h 580 -i 'quill-and-shadow' -j $(realpath Quill.svg)

build/Quill_and_Shadow_Square.png: build/Quill_and_Shadow_Clipped.png
	convert build/Quill_and_Shadow_Clipped.png -gravity center \
		-background transparent -extent 600x600 \
		build/Quill_and_Shadow_Square.png

build/img/icons/last_built: build/Quill_and_Shadow_Square.png
	convert build/Quill_and_Shadow_Square.png \
		-resize 32x32 \
		build/img/icons/favicon.png
	convert build/Quill_and_Shadow_Square.png -background white \
		-resize 57x57 -extent 57x57 \
		build/img/icons/apple-touch-icon-57-precomposed.png
	convert build/Quill_and_Shadow_Square.png -background white \
		-resize 72x72	-extent 72x72 \
		build/img/icons/apple-touch-icon-72-precomposed.png
	convert build/Quill_and_Shadow_Square.png -background white \
		-resize 114x114 -extent 114x114 \
		build/img/icons/apple-touch-icon-114-precomposed.png
	convert build/Quill_and_Shadow_Square.png -background white \
		-resize 144x144 -extent 144x144 \
		build/img/icons/apple-touch-icon-144-precomposed.png
	touch build/img/icons/last_built

build/img/logos/last_built: $(realpath Quill.svg)
	$(INKSCAPE) -e $(shell pwd)/build/wcravens_logo_export.png \
		-y 0 -D -z -h 600 $(realpath Quill.svg)
	$(INKSCAPE) -E $(shell pwd)/build/wcravens_logo_export.eps \
		-y 0 -D -z $(realpath Quill.svg)
	convert build/wcravens_logo_export.png -resize x60 \
		build/img/logos/wcravens_logo_x60.png
	convert build/wcravens_logo_export.png -resize x120 \
		build/img/logos/wcravens_logo.png
	touch build/img/logos/last_built

clean:
	-rm -rf build/*
