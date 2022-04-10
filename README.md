# Pandoc book template

![Release](https://github.com/nguyenvanduocit/ebook-template/workflows/Release/badge.svg)

> Modified from [pandoc-book-template](https://github.com/wikiti/pandoc-book-template)

## Description

This repository contains a simple template for building [Pandoc](http://pandoc.org/) documents into ebook;
Pandoc is a suite of tools to compile markdown files into EPUB file.

## Usage

### Installing

Please, check [this page](http://pandoc.org/installing.html) for more information.

### Folder structure

Here's a folder structure for a Pandoc book:

```
my-book/         # Root directory.
|- build/        # Folder used to store builded (output) files.
|- chapters/     # Markdowns files; one for each chapter.
|- images/       # Images folder.
|  |- cover.png  # Cover page for epub.
|- style.css     # Css file
|- metadata.yml  # Metadata content (title, author...).
```

### Setup generic data

Edit the *metadata.yml* file to set configuration data (note that it must start and end with `---`):

```yml
---
title: My book title
author: Daniel Herzog
rights: MIT License
lang: en-US
tags: [pandoc, book, my-book, etc]
abstract: |
  Your summary.
mainfont: DejaVu Sans

# Filter preferences:
# - pandoc-crossref
linkReferences: true
---
```

You can find the list of all available keys on
[this page](http://pandoc.org/MANUAL.html#extension-yaml_metadata_block).

### Creating chapters

Creating a new chapter is as simple as creating a new markdown file in the *chapters/* folder;
you'll end up with something like this:

```
chapters/01-introduction.md
chapters/02-installation.md
chapters/03-usage.md
chapters/04-references.md
```

Pandoc and Make will join them automatically ordered by name; that's why the numeric prefixes are
being used.

All you need to specify for each chapter at least one title:

```md
# Introduction

This is the first paragraph of the introduction chapter.

## First

This is the first subsection.

## Second

This is the second subsection.
```

Each title (*#*) will represent a chapter, while each subtitle (*##*) will represent a chapter's
section. You can use as many levels of sections as markdown supports.

## Export to EPUB

Use this command:

```sh
mkdir -p build
pandoc --toc --toc-depth=2 --webtex --css=style.css --metadata-file=metadata.yml  --verbose --wrap=none --epub-cover-image=images/cover.png -o build/epub.epub $(printf '"%s" ' chapters/*.md)
```

or with fishshell

```sh
mkdir -p build
pandoc --toc --toc-depth=2 --webtex --css=style.css --metadata-file=metadata.yml  --verbose --wrap=none --epub-cover-image=images/cover.png -o build/epub.epub chapters/*.md
```

The generated file will be placed in *build/epub.epub*.

## Release

Make a tag to release your book.

#### Extra configuration

If you want to configure the output, you'll probably have to look the
[Pandoc Manual](http://pandoc.org/MANUAL.html) for further information about pdf (LaTeX) generation,
custom styles, etc, and modify the Makefile file accordingly.

#### Templates

Output files are generated using [pandoc templates](https://pandoc.org/MANUAL.html#templates). All
templates are located under the `templates/` folder, and may be modified as you will. Some basic
format templates are already included on this repository, ion case you need something to start
with.

## References

- [Pandoc](http://pandoc.org/)
- [Pandoc Manual](http://pandoc.org/MANUAL.html)
- [Wikipedia: Markdown](http://wikipedia.org/wiki/Markdown)

## Action Secrets

Setup for Google SMTP

```
MAIL_USERNAME: youremail@gmail.com
MAIL_PASSWORD: your password or app password
MAIL_TO: your_kindle_email@kindle,your_friend_email@example.com
MAIL_FROM: your_verified_email@gmail.com
```

## Contributors

This project has been developed by:

| Avatar | Name | Nickname | Email |
| ------ | ---- | -------- | ----- |
| ![](http://www.gravatar.com/avatar/2ae6d81e0605177ba9e17b19f54e6b6c.jpg?s=64)  | Daniel Herzog | Wikiti | [info@danielherzog.es](mailto:info@danielherzog.es)
