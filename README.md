# 📄 stocksize — A flexible LaTeX package for dynamic paper size management in PDF documents

[![License: LPPL](https://img.shields.io/badge/license-LPPL%201.3c-blue.svg)](https://www.latex-project.org/lppl/)
[![LaTeX](https://img.shields.io/badge/LaTeX-package-orange.svg)](https://www.ctan.org/pkg/stocksize)
[![Build Status](https://img.shields.io/badge/build-passing-brightgreen.svg)](#)

---

## 🧠 Overview

`stocksize` is a lightweight LaTeX package that provides an easy-to-use interface to change paper (stock) dimensions in LaTeX documents. Unlike the popular `geometry` package, `stocksize` actually changes the physical PDF paper size, not just the typing area. This is particularly useful when you need multiple pages with different dimensions in a single document.

---

## 🎯 Use Cases

- **📑 Mixed-format documents**: Combine A4, A5, and custom sizes in one PDF.
- **🎨 Design layouts**: Create brochures, flyers, or booklets with varying page sizes.
- **📋 Reports with appendices**: Different page sizes for different sections.
- **🌐 International documents**: Mix different paper standards (A4, Letter, etc.)

------

## ✨ Features

- ✨ **Dynamic page sizing**: Change paper dimensions mid-document.
- 🪆 **Nested sizes**: Stack multiple page sizes with automatic LIFO restoration.
- 🧮 **Margin preservation**: Optionally keep and restore existing margins when resizing.
- ⚙️ **Compatible**: Minimal dependencies and easy integration.
- 🔍 **Debugging support**: Provides macros for easy querying of paper width and height.
- 🧰 **Simple API**: Minimal commands to master.
- 🧩 **Geometry integration**: Works with standard LaTeX classes and geometry setups.
- 🧠 **Multi-engine support**: Works with pdfLaTeX, XeLaTeX, and LuaLaTeX.
- 🧾 **Documented**: Companion documentation (`stocksize-doc.tex`) included.

---

## 🚀 Quick Start

### Installation

Place `stocksize.sty` in your project directory or LaTeX package path.

### 📖 Commands

### => `\newstocksize{options}`

Starts a new page with the given paper (stock) size.  The subsequent pages will keep this new paper size.

**Options:**




| Option                      | Description                                           |
| --------------------------- | ----------------------------------------------------- |
| `layoutsize={width,height}` | Sets the page dimensions.                             |
| `margin=value`              | Sets uniform margins on all sides.                    |
| `keepmargins`               | Preserves current margins in the new layout.          |
| *Any other option*          | Passed to `\newgeometry` from the `geometry` package. |

**Example:**

```latex
\newstocksize{layoutsize={20cm,25cm}, margin=2cm}
\newstocksize{a5paper, margin=1cm}  % Using preset sizes
\newstocksize{layoutsize={10cm,15cm}, keepmargins}  % Keep current margins
```

### => `\restorestocksize`

Restores the previous page size. Works in *Last In First Out* (LIFO) fashion, allowing nested size changes to be unwound correctly.

**Example:**

```latex
\newstocksize{layoutsize={15cm,10cm}, margin=1.5cm}
  Content here...

  \newstocksize{layoutsize={20cm,20cm}, margin=4cm}
    Content here...
  \restorestocksize

  Back to 15cm×10cm
\restorestocksize

Back to default size
```

---

## 🔧 How It Works

The `stocksize` package modifies the actual PDF page size using engine-specific commands:

- **pdfLaTeX**: changes `\pdfpageheight` and `\pdfpagewidth`.
- **XeLaTeX/LuaLaTeX**: changes `\pageheight` and `\pagewidth`.

When you use `\newstocksize`, the package:

1. Saves the current layout configuration.
2. Applies your new geometry settings via the `geometry` package.
3. Updates the physical PDF page dimensions accordingly.

When you use `\restorestocksize`, it reverses these steps in order.

---

## 📦 Package Information

- **Version**: 1.0.3 (2024/11/23)
- **Author**: João M. Lourenço
- **License**: LaTeX Project Public License (LPPL) v1.3c or later
- **Dependencies**: `geometry` package (automatically loaded if needed)
- **Compatibility**: pdfLaTeX, XeLaTeX, LuaLaTeX

---

## 📚 Documentation

For detailed examples and advanced usage, see `stocksize-doc.tex` in the repository.

---

## 🤝 Contributing

Found a bug or have a feature request? 
Please open an issue on the [GitHub repository](https://github.com/joaomlourenco/stocksize).

---

## 📜 License

This package is distributed under the **LaTeX Project Public License (LPPL) v1.3c** or later.

---

**Made with ❤️ by João M. Lourenço**