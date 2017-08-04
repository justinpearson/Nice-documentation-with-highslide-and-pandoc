---
title: Nice documentation with highslide and pandoc
header-includes:
    <script type="text/javascript" src="highslide/highslide.js" ></script>
---

# other title

An example of writing nice documentation in markdown, converting to HTML with pandoc, and using highslide Javascript for zoomable image thumbnails.





- Pandoc is a program for converting documents from one format to another.
    - `sudo apt-get install pandoc`
- `highslide.js` is a Javascript library for displaying images as thumbnails that zoom in when you click on them.
    - `http://highslide.com/download/highslide-5.0.0.zip`
- `pandoc.css` is a CSS file with some nice styling.
- `img-to-zoomable-link.py` is a pandoc filter that wraps each HTML image tag in a highslide Javascript function to display the image as a thumbnail.

