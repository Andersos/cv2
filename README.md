# About
This repo contains the source I use to automatically generate
[my curriculum vitae](http://bamos.io/cv) as a webpage and PDF
from YAML and BibTeX input.

[generate.py][generate.py] reads from [cv.yaml][cv.yaml] and
[publications.bib][publications.bib] and outputs LaTeX and Markdown
by using Jinja templates.
Statistics about my blog and github account are obtained
using [blog-info.py][blog-info.py] and [github-info.py][github-info.py].

# Building and running
The dependencies are included in `requirements.txt` and can be
installed
using `pip` with `pip3 install -r requirements.txt`.
On Mac or Linux, `make` will call [generate.py][generate.py] and
build the LaTeX documents with `pdflatex` and `biber`.

The Makefile will also:

1. Stage to my website with `make stage`,
2. Start a local jekyll server of my website with updated
  documents with `make jekyll`, and
3. Push updated documents to my website with `make push`.

# Implementation details
## generate.py
1. Read `cv.yaml` into Python as a map and loop through the
   `order` vector,
   which maps a section key to the title to display.
   This is done so sections can be moved and hidden without
   deleting them.
2. Generate the LaTeX or Markdown content for every section by
   using the templates
   [cv-section.tmpl.tex][cv-section.tmpl.tex] and
   [cv-section.tmpl.md][cv-section.tmpl.md], which use
   [moderncv](http://www.ctan.org/pkg/moderncv).
   The conditional statements make the sections a little messy,
   but using a template for each section lets the order be changed
   solely by the `order` vector.
3. Generate the entire LaTeX or Markdown document by using
   the templates [cv.tmpl.tex][cv.tmpl.tex] and
   [cv.tmpl.md][cv.tmpl.md].

## Publications
All publications are stored as BibTeX in `publications.bib`.
The entries can be obtained from Google Scholar.
The order in the BibTeX file will be the order in
the output files.

BibTeX is built for integration with LaTeX, but producing
Markdown is not traditionally done from BibTeX files.
This repository uses [BibtexParser][bibtexparser] to load the
bibliography into a map.
The data is manually formatted to mimic the LaTeX
IEEE bibliography style.

# Similar Projects
There are many approaches to managing a resume or CV in git,
and this project uses unique Markdown and LaTeX templates.
The following list shows a short sampling of projects,
and I'm happy to merge pull requests of other projects.

<!--
To generate the following list, install https://github.com/jacquev6/PyGithub
and download the `github-repo-summary.py` script from
https://github.com/bamos/python-scripts/blob/master/python3/github-repo-summary.py.
Please add projects to the list in the comment and in the table below.

github-repo-summary.py \
  afriggeri/cv \
  cies/resume \
  deedydas/Deedy-Resume \
  divad12/resume \
  emichael/resume \
  icco/Resume \
  jsonresume/resume-schema \
  kaeluka/cv \
  mwhite/resume \
  prat0318/json_resume \
  qutebits/resume_42 \
  raphink/CV \
  sc932/resume \
  terro/CV \
  there4/markdown-resume \
  zellux/resume
-->

Name | Stargazers | Description
----|----|----
[afriggeri/cv](https://github.com/afriggeri/cv) | 768 | CV, typesetted in Helvetica Neue, using XeTeX, TikZ and Biblatex
[cies/resume](https://github.com/cies/resume) | 192 | My resume as a PDF including the well commented Latex sources and build instructions.
[deedydas/Deedy-Resume](https://github.com/deedydas/Deedy-Resume) | 501 | A one page , two asymmetric column resume template in XeTeX that caters to an undergraduate Computer Science student
[divad12/resume](https://github.com/divad12/resume) | 24 | Yaml resume compiled into multiple formats (such as LaTeX, HTML (TODO), etc.)
[emichael/resume](https://github.com/emichael/resume) | 1 | Generate LaTeX and Markdown resume from YAML with Python.
[icco/Resume](https://github.com/icco/Resume) | 214 | A markdown port of my resume
[jsonresume/resume-schema](https://github.com/jsonresume/resume-schema) | 330 | JSON-Schema is used here to define and validate our proposed resume json
[kaeluka/cv](https://github.com/kaeluka/cv) | 65 | My CV.
[mwhite/resume](https://github.com/mwhite/resume) | 546 | Markdown -> PDF/HTML resumé generator
[prat0318/json_resume](https://github.com/prat0318/json_resume) | 1026 | Generates pretty HTML, LaTeX, markdown, with biodata feeded as input in JSON
[QuteBits/resume_42](https://github.com/QuteBits/resume_42) | 4 | It generates a beautiful resume from yaml data
[raphink/CV](https://github.com/raphink/CV) | 48 | My CV
[sc932/resume](https://github.com/sc932/resume) | 296 | My CV/resume in LaTeX.
[terro/CV](https://github.com/terro/CV) | 18 | My cv template
[there4/markdown-resume](https://github.com/there4/markdown-resume) | 397 | Generate a responsive CSS3 and HTML5 resume with Markdown, with optional PDF output.
[zellux/resume](https://github.com/zellux/resume) | 97 | My resume, generated with moderncv

[generate.py]: https://github.com/bamos/cv/blob/master/generate.py
[publications.bib]: https://github.com/bamos/cv/blob/master/publications.bib
[cv.yaml]: https://github.com/bamos/cv/blob/master/cv.yaml
[blog-info.py]: https://github.com/bamos/cv/blob/master/blog-info.py
[github-info.py]: https://github.com/bamos/cv/blob/master/github-info.py
[Requirements.txt]: https://github.com/bamos/cv/blob/master/Requirements.txt
[cv-section.tmpl.tex]: https://github.com/bamos/cv/blob/master/tmpl/cv-section.tmpl.tex
[cv-section.tmpl.md]: https://github.com/bamos/cv/blob/master/tmpl/cv-section.tmpl.md
[cv.tmpl.tex]: https://github.com/bamos/cv/blob/master/tmpl/cv.tmpl.tex
[cv.tmpl.md]: https://github.com/bamos/cv/blob/master/tmpl/cv.tmpl.md
[bibtexparser]: https://bibtexparser.readthedocs.org/en/latest/index.html
