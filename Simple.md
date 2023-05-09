**Themes for R Markdown**
*With the powerful rmarkdown package, we could easily create nice HTML document by adding some meta information in the header, for example*
-------------
title: Nineteen Years Later
author: S M Sharif Mia
date: feb 03, 2019
output:
  rmarkdown::html_document:
    theme: lumen
----------------
*The html_document engine uses the Bootswatch theme library to support different styles of the document. This is a quick and easy way to tune the appearance of your document, yet with the price of a large file size (> 700KB) since the whole Bootstrap library needs to be packed in.
For package vignettes, we can use the html_vignette engine to generate a more lightweight HTML file that is meant to minimize the package size, but the output HTML is less stylish than the html_document ones.*

**The prettydoc Engine**
*The prettydoc package provides an alternative engine, html_pretty, to knit your R Markdown document into pretty HTML pages. Its usage is extremely easy: simply replace the rmarkdown::html_document or rmarkdown::html_vignette output engine by prettydoc::html_pretty in your R Markdown header, and use one of the built-in themes and syntax highlighters. For example*
---
title: Nineteen Years Later
author: S M Sharif Mia
date: feb 03, 2019
output:
  prettydoc::html_pretty:
    theme: cayman
    highlight: github
---
**Options and Themes**
*The options for the html_pretty engine are mostly compatible with the default html_document (see the documentation) with a few exceptions:*

 1. Currently the theme option can take the following values. More themes will be added in the future. 
  = cayman: Modified from the Cayman theme.
  = tactile: Modified from the Tactile theme.
  = architect: Modified from the Architect theme.
  = leonids: Modified from the Leonids theme.
  = hpstr: Modified from the HPSTR theme.
 2. The highlight option takes value from github and vignette.
 3. Options code_folding, code_download and toc_float are not applicable.