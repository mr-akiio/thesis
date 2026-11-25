# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

A LaTeX bachelor's thesis for the Faculty of Informatics, Masaryk University (FI MUNI), built on the `fithesis4` document class. It is still a skeleton: the metadata in `main.tex` and the chapter bodies are placeholders.

## Commands

```sh
latexmk                # build build/main.pdf (settings come from .latexmkrc)
latexmk -g             # force a full rebuild
latexmk -pvc           # rebuild on every change
latexmk -c             # remove build artifacts, keep the PDF
```

There are no tests or linters. To verify a change, build it and check `build/main.log` for errors and warnings such as undefined references or citations.

`latexmk` runs `pdflatex` and `biber`, and writes all output to the git-ignored `build/` directory. `fithesis4` and `biber` must be installed on the system.

## Structure

- `main.tex` holds the class options, metadata (`\thesissetup`), package imports, and the chapter order. A new chapter file only appears in the thesis once it has an `\input` line here.
- `chapters/*.tex` are fragments with no preamble, so they cannot be compiled on their own.
- `references.bib` is passed through the `bib` key in `\thesissetup` rather than `\addbibresource`. Citations use `\cite`, and the bibliography is printed by `\printbibliography` in `main.tex`.
- `figures/` is on `\graphicspath`, so use `\includegraphics{name}` without the directory prefix.

## Conventions

- The Introduction and Conclusion are unnumbered by FI convention. They use `\chapter*` with manual `\markright` and `\addcontentsline`, so keep that pattern if they are restructured.
- Labels are prefixed by type: `ch:`, `tab:`, `fig:`, `app:`.
- Tables use `booktabs` rules. `floatrow` places table captions above the table.
- To write in Czech or Slovak, change `main=` and add the language to the `babel` options in `main.tex`. This requires the `texlive-langczechslovak` package.
- For the printed submission, switch the class option `digital` to `printed`, and to `twoside` if printing double-sided. The scanned assignment goes in the commented-out `assignment` key in `\thesissetup`.
