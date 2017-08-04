# Nice documentation with highslide and pandoc

An example of writing nice documentation in markdown, converting to HTML with pandoc, and using the "highslide" Javascript library for zoomable image thumbnails.


Example
----------


Start with this Markdown file `example.md`:

![](Images/2017-08-04-11-35-45.png)

Run pandoc:

    pandoc --standalone --table-of-contents \
        --from=markdown --to=html \
        --filter=img-to-zoomable-link.py --css=pandoc.css \
        --output=example.html example.md

This creates `example.html` with a table of contents, nice CSS, and zoomable images:

![](Images/highslide-example.gif)

- (You may have to enable Javascript on your browser.)
- (In the Chrome browser, it is easiest to run a local webserver and allow Javascript on 0.0.0.0:) 
    - From this repo directory:
    - `$ python -m SimpleHTTPServer`
    - Then browse to `0.0.0.0:8000/example.html`


Repo Contents
---------------

- Pandoc is a program for converting documents from one format to another.
    - `sudo apt-get install pandoc`
- `highslide.js` is a Javascript library for displaying images as thumbnails that zoom in when you click on them.
    - `http://highslide.com/download/highslide-5.0.0.zip`
- `pandoc.css` is a CSS file with some nice styling.
- `img-to-zoomable-link.py` is a pandoc filter that wraps each HTML image tag in a highslide Javascript function to display the image as a zoomable thumbnail.
    - This pandoc filter requires the `pandocfilters` Python package:
        - `pip install pandocfilters`
        - <https://github.com/jgm/pandocfilters>



Notes
------

- By default, the file `img-to-zoomable-link.py` needs to be in the same directory as the generated HTML file. To prevent copying `img-to-zoomable-link.py` multiple places, consider putting it into `~/Utilities/` and providing the absolute path to the `pandoc` command.

- The file `pandoc.css` and the folder `highslide/` need to be in the same directory as the HTML file.

- Each markdown file needs to start with a little YAML that instructs pandoc to include the highslide JS library:

        ---
        title: Example document
        header-includes:
            <script type="text/javascript" src="highslide/highslide.js" ></script>
        ---

    - Note: YAML wasn't supported in old versions of pandoc; I'm using 1.19.2.1.

- For PDF output, need "backslash space" after each img to put img placement precisely, like this:

    `![](Images/ScreenShot2017-02-01-16-52-05.png)\ `

- Using Submline Text? Assign a keystroke to convert markdown to HTML:
    - Tools > Build System > New Build System...
    - Paste this text:

            {
                "shell_cmd": "pandoc -s --toc -f markdown -t html --filter img-to-zoomable-link.py -c pandoc.css -o \"$file_base_name.html\" \"$file_name\" " 
            }

    - Save as `my-markdown-to-html`, now it appears in `Tools` > `Build System`.
