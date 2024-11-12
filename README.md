# stocksize

This package provides a flexible and easy interface to change the paper (stock) dimensions in LaTeX documents.
Multiple user defined stock sizes are allowed in the same document, and sock sizes can be nested (in a LIFO order).

## About

* **Package:** stocksize — A flexible and easy interface to paper (stock) dimensions.
* **Copyright:** 2024 © João M. Lourenço <joao.lourenco@fct.unl.pt>
* **CTAN:** https://ctan.org/pkg/stocksize
* **Repository:** https://github.com/joaomlourenco/stocksize
* **License:** The LaTeX Project Public License 1.3c

## Introduction

The package [geometry](https://github.com/LaTeX-Package-Repositories/geometry) is excellent for customuzing the page layout. However, changing the page size in the middle of the document changes the typing area, but does not affect the real paper (sock) size. This package ains to circunvent this situation.

## User Interface

### Loading the Package

Simply load the package with (with no options):
```latex
\usepackage{stocksize}
```

### Starting a new Page With a Different Page/Stock Size

To start a new page with a different page/stock size, use the newstocksize environment:
```latex
\begin(newstocksize}[options]{height}{width}
Your contents here
\end (newstocksize}
```

The options given to `newstocksize` will be passed to the `\newgeometry` command from the `geometry` package.

### Nesting Different Page/Stock Sizes
  
  Multiple paper/stock sizes can be nested.  When the \verb!newstocksize! environment, the previous size is resmued.
  
```latex
  This page has the default size  (e.g., a4paper).

  \begin{newstocksize}[margin=0pt]{10cm}{8cm}
    This page size is 10cm by 8cm.
    
    \begin{newstocksize}[margin=0pt]{5cm}{15cm}
      This page size is 5cm by 15cm.
    \end{newstocksize}

    Resuming the page size to 10cm by 8cm.
  \end{newstocksize}

  Resuming the default paper size and margins!
  This page size is back to the default page size (e.g., a4paper).
```
