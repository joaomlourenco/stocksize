# stocksize

This package provides a flexible and easy interface to change the paper (stock) dimensions in LaTeX documents.
Multiple user defined stock sizes are allowed in the same document, and stock sizes can be nested (in a LIFO order).

--------
<!--
<picture>
  <source
    media="(prefers-color-scheme: dark)"
    srcset="
      https://api.star-history.com/svg?repos=joaomlourenco/stocksize&type=Date&theme=dark
    "
  />
  <source
    media="(prefers-color-scheme: light)"
    srcset="
      https://api.star-history.com/svg?repos=joaomlourenco/stocksize&type=Date
    "
  />
  <img
    width="400"
    alt="Star History Chart"
    src="https://api.star-history.com/svg?repos=joaomlourenco/stocksize&type=Date"
  />
</picture>
-->
**If you opt for using this project, please give it a star by clicking the (⭐️) at the top right of the [project's page](https://github.com/joaomlourenco/biblatex-cse).**

--------

## About

* **Package:** stocksize — A flexible and easy interface to paper (stock) dimensions.
* **Copyright:** 2024 © João M. Lourenço <joao.lourenco@fct.unl.pt>
* **CTAN:** https://ctan.org/pkg/stocksize
* **Repository:** https://github.com/joaomlourenco/stocksize
* **License:** The LaTeX Project Public License 1.3c

## Introduction

The package [geometry](https://github.com/LaTeX-Package-Repositories/geometry) is excellent for customising the page layout.  However, changing the page size in the middle of the document only changes the typing area and does not affect the real paper (stock) size.  This package circumvents this situation by resizing the paper (stock) size to the given size.


## User Interface

### Loading the Package

Simply load the package with (with no options):
```latex
\usepackage{stocksize}
```

### Starting a new Page With a Different Page/Stock Size

To start a new page with a different page/stock size use the \verb!\newstocksize! and \verb!restorestocksize! commands.
```latex
\newstocksize{options} — This command starts a new stock (and paper) size.  The `options` may include:
    `keepmargins` — The current (left, right, top, and bottom) margins will be prreseved in the new page layout;
    `other_options` — The `other_options` are passed straight to the \newgeometry command form the`geometry` package.
\restorestocksize — This command ends the current stock size and restores the previous one (in a LIFO fashion).
```

### Nesting Different Page/Stock Sizes
  
  Multiple paper/stock sizes can be nested.  With each `\restorestocksize` command, the previous size is resumed.
  
```latex
  This page has the default size  (e.g., a4paper).

    \newstocksize{layoutsize={15cm,10cm},margin=1.5cm}
    This page size is 15cm wide x 10cm high, with margins of 1.5cm.
    
      \newstocksize{layoutsize={20cm,20cm},margin=4.0cm}
      This page size is 20cm wide x 20cm high, with margins of 4.0cm.

    \restorestocksize
    Resuming the page size is 15cm wide x 10cm high, with margins of 1.5cm.
    
  \restorestocksize
  Resuming the default paper size and margins (e.g., a4paper)!
```
