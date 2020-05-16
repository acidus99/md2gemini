# md2gemini

Converter from Markdown to the [Gemini](https://gemini.circumlunar.space/) text format. It works as a Python module, or a command line application.

## Installation
```
pip3 install md2gemini
```
You may also want to use the `--user` flag after install, to only install the package for your user.

Note that this package only officially supports Python 3.

## Usage

It works directly in Python, or on the command line. The command line version can work with unix pipes as well, reading files from stdin and writing to stdout if desired.

### Command line
```
usage: md2gemini [-h] [--version] [-w] [-d DIR] [-a] [-j] [--img-tag IMG_TAG] [-i INDENT] [file [file ...]]

Convert markdown to gemini.

positional arguments:
  file                  Files to convert. If no files are specified then data will be read from stdin and printed to stdout.

optional arguments:
  -h, --help            show this help message and exit
  --version             show program's version number and exit
  -w, --write           Write output to a new file of the same name, but with a .gmi extension.
  -d DIR, --dir DIR     The directory to write files to, if --write is used.
  -a, --ascii-table     Use ASCII to create tables, not Unicode.
  -j, --jekyll          Remove jekyll frontmatter from parsing and output.
  --img-tag IMG_TAG     What text to add after image links. Defaults to '[IMG]'. Write something like --img-tag='' to remove it.
  -i INDENT, --indent INDENT
                        The number of spaces to use for list indenting. Put 'tab' to use a tab instead.
```

### In Python
```python
from md2gemini import md2gemini
# Load a markdown file's contents into memory and get conversion
with open("example.md", "r") as f:
    gemini = md2gemini(f.read())
# Now the gemini variable contains your converted text as a string
```
Options for the `md2gemini` function are similar to the command line ones above.
```python
def md2gemini(markdown, img_tag="[IMG]", indent="  ", ascii_table=False, jekyll=False):
    """Convert the provided markdown text to the gemini format.
    
    img_tag: The text added after an image link, to indicate it's an image.
    
    indent: How much to indent sub-levels of a list. Put several spaces, or \\t for a tab.
    
    ascii_table: Use ASCII to create tables, not Unicode.

    jekyll: Skip jekyll frontmatter when processing.
    """
```

## Features to add
- Footnote style links
  - Right now, inline links are converted to Gemini links, breaking up paragraph flow. It'd be better to have an option that just adds a footnote like `[2]` beside the word, and adds links at the end of the paragraph or document.