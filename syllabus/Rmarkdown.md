---
layout: lesson
root: ../..
title: R Markdown
---




> ### Learning Objectives {.objectives}
>
> * Value of reproducible reports
> * Basics of Markdown
> * R code chunks
> * Chunk options
> * Inline R code
> * LaTeX-based equations
> * Other output formats


I'm not quite sure the best way to get started with this. I'm trying
to explain

- the value of reproducible documents (literate programming)
- what knitr document looks like (chunks of code in the midst of text)
- the value of having the product be a web page
- the value of R Markdown for this

I then need to explain

- the basics of markdown syntax
- the yaml header for R Markdown
- R code chunks
- inline R
- chunk options
- global chunk options


### Data analysis reports

Data analysts tend to write a lot of reports, describing their
analyses and results, for their collaborators or to document their
work for future reference.

When I was first starting out, I'd write an R script with all of my
work, and would just send an email to my collaborator, describing the
results and attaching various graphs. In discussing the results, there
would often be confusion about which graph was which.

I moved to writing formal reports, with Word or LaTeX, but I'd have to
spend a lot of time getting the figures to look right. Mostly, the
concern is about page breaks.

Everything is easier now that I create a web page (as an html
file). It can be one long stream, so you can have as tall figures that
wouldn't ordinary fit on one page. Scrolling is your friend.


### Literate programming

Ideally, such analysis reports are _reproducible_ documents: If an
error is discovered, or if some additional subjects are added to the
data, you can just re-compile the report and get the new or corrected
results (versus having to reconstruct figures, paste them into
a Word document, and further hand-edit various detailed results).

The key tool for R is [knitr](http://yihui.name/knitr/), which allows
you to create a document that is a mixture of text and some chunks of
code. When the document is processed by knitr, chunks of R code will
be executed, and graphs or other results inserted.

This sort of idea has been called "literate programming".

knitr allows you to mix basically any sort of text with any sort of
code, but we recommend that you use R Markdown, which mixes Markdown
with R. Markdown is a light-weight mark-up language for creating web
pages.


### Creating an R Markdown file

- Within R Studio, how to use menu-bar to create a new R Markdown file

### Basic components of R Markdown

- Discuss the initial yaml header
- Point to code chunks
- Delete all of the code chunks and start out with basic discussion of
  R Markdown:
  - bold and italics
  - section headers of different sizes
  - bulleted lists
  - numbered lists
  - hyperlinks
  - inserting images (maybe insert an R icon)
  - super-scripts and subscripts
- How to compile to html file

### R code chunks

- regular code
- graphs

### Chunk options

- chunk names
- chunk options: `echo`, `results`, `include`, `fig.height`, `fig.width`
- global chunk options (e.g., `fig.path`)

### Inline R code

- don't let it get split across lines
- perhaps precede the paragraph with a larger code chunk that does
  calculations and defines things
- rounding

### LaTeX equations

- `$` vs `$$`

### Other output options

- PDF, Word, slides
- Refer to the [documentation](http://rmarkdown.rstudio.com/)