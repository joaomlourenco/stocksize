# stocksize — Structured control of PDF page (stock) size in LaTeX

[![CTAN](https://img.shields.io/ctan/v/aidisclose)](https://ctan.org/pkg/stocksize)
[![Version](https://img.shields.io/badge/version-2.0.0-blue)](https://github.com/joaomlourenco/stocksize)
[![Date](https://img.shields.io/badge/date-2025--12--31-orange)](https://github.com/joaomlourenco/stocksize)
[![License: LPPL 1.3c](https://img.shields.io/badge/license-LPPL%201.3c-blue)](https://www.latex-project.org/lppl/lppl-1-3c/)
[![LaTeX](https://img.shields.io/badge/LaTeX-LaTeX2e%202020%2F10%2F01%2B-brightgreen)](https://www.latex-project.org/)

---

## Purpose

The **`stocksize`** package provides **robust control of the physical PDF page size** (the *stock size*) inside a LaTeX document.

It complements the `geometry` package by managing **paper size transitions** reliably, including **nested changes**, while delegating margin and layout calculations to `geometry`.

The package is designed for documents where the **physical page size itself must change mid-document**, such as appendices, inserts, or mixed-format publications.

---

## Key Concepts

- **Stock size** = physical PDF page dimensions  
- **Layout** = (logical) paper height and width, margins, text block, headers/footers (handled by `geometry`)  
- `stocksize` coordinates both, ensuring they remain synchronized

---

## Typical Use Cases

- Appendices with different paper formats
- Mixed A4 / A5 / Letter documents
- Landscape or square inserts
- Print-ready PDFs with non-uniform stock
- Publisher workflows requiring strict PDF page dimensions

---

## Features

- **Logical page size control** (via `geometry`)
- **Physical page size control** (PDF page dimensions)
- **Fully nested size changes** (LIFO stack semantics)
- ***Optional margin preservation**
- **Reliable restoration** of previous sizes
- **Transparent integration with `geometry`**
- **Engine-independent** (pdfLaTeX, XeLaTeX, LuaLaTeX)
- **Documented design** with rationale and implementation notes

---

## Installation

Place `stocksize.sty` in your working directory or a LaTeX-visible path.

Load the package in the preamble with:
```latex
\usepackage[OPTIONS]{stocksize}
```

The package loads `geometry` automatically if needed.

---

## User Interface

### `\newstocksize{⟨options⟩}`

Starts a new physical page with the specified stock size and geometry options.

Internally:
1. Saves the current page and layout state
2. Applies `geometry` with the provided options
3. Updates the PDF page dimensions

**Options**

All options are passed directly to `geometry`, except `keepmargins` which are processed by the package.

Common examples:

| Option | Meaning |
|------|--------|
| `layoutsize={w,h}` | Set physical page size |
| `paperwidth=…` / `paperheight=…` | Alternative size specification |
| `margin=…` | Uniform margins |
| `keepmargins` | Preserve current margins |

**Example**

```latex
\newstocksize{layoutsize={20cm,25cm}, margin=2cm}
```

---

### `\restorestocksize`

Restores the **previous** stock size and layout.

- Operates in **Last-In-First-Out (stack) order**
- Safe for arbitrarily deep nesting
- Restores both geometry and PDF page size

**Example**

```latex
\newstocksize{layoutsize={15cm,10cm}, margin=1.5cm}
  Content...

  \newstocksize{layoutsize={20cm,20cm}, keepmargins}
    Nested content in 20x20 cm stock and paper size...
  \restorestocksize

Back to 15×10 cm stock and paper size...
\restorestocksize

Back to the initial stock and paper size...
```

---

## Relation to `geometry`

- `geometry` alone does **not** safely support nested page size changes
- `stocksize` provides a **stack-based abstraction** on top of `geometry`
- All layout computation remains delegated to `geometry`
- `stocksize` ensures page size and layout state remain consistent

---

## Technical Notes

- PDF page size is set using:
  - `\pdfpagewidth` / `\pdfpageheight` (pdfLaTeX)
  - `\pagewidth` / `\pageheight` (XeLaTeX, LuaLaTeX)
- Geometry states are saved and restored explicitly
- No grouping tricks or output-routine hacks are used

---

## Documentation

The full technical documentation, including design rationale and edge-case discussion, is available in:

```
stocksize-doc.pdf
```

---

## Package Information

- **Version**: 2.0.0 (2025-12-31)
- **Author**: João M. Lourenço
- **License**: LPPL v1.3c or later
- **Dependencies**: `geometry`
- **Engines**: pdfLaTeX, XeLaTeX, LuaLaTeX

---

## Contributing

Bug reports, tests, and design discussions are welcome via GitHub issues.

---

Copyright © 2025-26 João M. Lourenço.  
Crafted with 🧡 for reproducible scientific writing.
