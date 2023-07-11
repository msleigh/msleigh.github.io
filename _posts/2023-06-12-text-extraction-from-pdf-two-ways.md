---
layout: post
title: "Text extraction from PDF (with Python), two ways"
description: "Documenting ways of extracting text from PDF files (with or without OCR) in Python"
date:  2023-06-12 01:02:00 +0100
author: msleigh
---

This post documents two ways in which to extract the text from a PDF document. I'm using Python for this
task only because I ultimately want to do this within a Python application, not because for this task specifically I've
chosen Python as the best tool. A couple of the Python libraries I use here are just wrappers to a non-Python tool that
has to be installed separately.

The choice between the two ways depends on whether the PDF stores the text as text, as a PDF that was created digitally
does, or as images, as a PDF which has been scanned in does.

## Text extraction

The first way uses [`pypdf`](https://pypdf.readthedocs.io/en/stable/). To install:

```bash
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install pypdf
```

Then in the Python code:

```python
from pypdf import PdfReader
reader = PdfReader("example.pdf")
print(f"Found {len(reader.pages)} pages")
with open("example.txt", "w") as fp:
    for page in reader.pages:
        fp.write(page.extract_text())
```

## Optical character recognition

As the `pypdf` documentation says, text extraction is hard, and `pypdf` can't extract text from scanned PDFs, where the
content is stored as images. For this, you need optical character recognition (OCR). Hence the second way uses the
[Tesseract OCR software](https://github.com/tesseract-ocr/tesseract). This can be installed using
[HomeBrew](https://tesseract-ocr.github.io/tessdoc/Compiling.html#macos):

```bash
brew install tesseract
```

and since I'm using Python, I also installed the [`pytesseract` wrapper](https://github.com/madmaze/pytesseract):

```bash
python3 -m pip install pytesseract
```

Note however that Tesseract works on images, so it's first necessary to convert the pages of the PDF document into
image files.
I did this with [`pdf2image`](https://github.com/Belval/pdf2image), which is a wrapper to `pdftoppm` and `pdftocairo` which can
be found (on macOS) in the [Poppler](https://poppler.freedesktop.org/) package.:

To install what's needed:

```bash
brew install poppler
python3 -m pip install pdf2image
```

To convert a PDF to image files and extract text using Tesseract in Python:

```python
from pdf2image import convert_from_path
from pdf2image.exceptions import (
    PDFInfoNotInstalledError,
    PDFPageCountError,
    PDFSyntaxError,
)
images = convert_from_path("example.pdf")
print(f"Found {len(images)} pages")
with open("example.txt", "w") as fp:
    for image in images:
        fp.write(pytesseract.image_to_string(image))
```

## Comparison

The `pypdf` documentation addresses the question of why not to simply always use OCR; my own minimal testing so far
seems to confirm that the quality, when it works at all, of the text extracted by `pypdf` is better than that from OCR,
so this latter is best reserved as a fall-back option when extraction doesn't work.


