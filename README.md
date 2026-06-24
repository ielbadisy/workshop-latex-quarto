# From LaTeX to Quarto — Presenter Guide

**Audience:** PhD students  
**Duration:** 3 hours  
**Tools needed:** Prism, RStudio, VS Code + Quarto extension, terminal


## Workshop Flow and Timing

| Time | Slide | Topic | Notes |
|---|---|---|---|
| 0:00–0:05 | — | Welcome, logistics | Open slides PDF |
| **Part 1 — LaTeX** | | | |
| 0:05–0:10 | 1 | A Brief History | Show LaTeX logo; emphasize TeX is the engine |
| 0:10–0:15 | 2 | LaTeX ≠ Overleaf | Key misconception to clear up first |
| 0:15–0:20 | 3 | Why LaTeX? | Ask: who has used Word for a thesis? |
| 0:20–0:25 | 4 | Platforms | Open Prism live; show the interface |
| 0:25–0:30 | 5 | Why Document Classes? | Show `elsarticle` vs `article` output |
| 0:30–0:38 | 6 | Document Structure | Live-type the minimal example in Prism |
| 0:38–0:43 | 7 | How to Compile | Point to the engine diagram; run `latexmk` in terminal |
| 0:43–0:50 | 8 | Mathematical Notation | Type 2–3 equations live; show custom commands |
| 0:50–0:55 | 9 | Diagrams — TikZ | Compile `demos/latex/03-template/`; show Mermaid |
| 0:55–1:00 | 10 | Debugging with AI | Demo: paste a broken snippet to Codex/Claude |
| 1:00–1:05 | 11 | AI Workflow diagram | Reinforce the loop: isolate → ask → fix |
| **Break** | | | 5 minutes |
| **Part 2 — Quarto** | | | |
| 1:10–1:15 | 12 | From LaTeX to Quarto | "Same engine, but adds code + multiple outputs" |
| 1:15–1:20 | 13 | What Quarto Solves | Show the output format table |
| 1:20–1:28 | 14 | Engines and Install | Run `quarto check` live in terminal |
| 1:28–1:35 | 15 | File Anatomy | Open `demos/quarto/01-minimal/report.qmd` in RStudio |
| 1:35–1:42 | 16 | Markdown | Side-by-side comparison with LaTeX syntax |
| 1:42–1:48 | 17 | YAML | Change format from `html` to `pdf` live |
| 1:48–1:55 | 18 | Code Chunks | Add a chunk, run it, show inline code updating |
| 1:55–2:00 | 19 | Cross-References | Open `demos/quarto/02-crossrefs/`; show `@fig-` |
| 2:00–2:05 | 20 | Output Formats | Render same `.qmd` to html, pdf, docx |
| 2:05–2:12 | 21 | Slides | Open `demos/quarto/03-slides/`; compare revealjs vs beamer |
| 2:12–2:18 | 22 | Projects | Open `demos/quarto-lecture/03-website/`; run `quarto preview` |
| 2:18–2:23 | 23 | Templates | Show `demos/quarto-lecture/05-template/`; explain `_extensions/` |
| 2:23–2:28 | 24 | Debugging | Walk through the checklist with a real error |
| 2:28–2:30 | 25 | Lab intro | Assign lab (see below) |
| **Lab** | | | 30 minutes |
| 2:30–3:00 | — | Hands-on lab | Students choose Lab 1, 2, or 3 |


## How to Compile — Quick Reference

### LaTeX

**Terminal:**

```bash
# Single pass
pdflatex paper.tex

# With bibliography (biblatex + biber)
xelatex paper.tex
biber paper
xelatex paper.tex
xelatex paper.tex

# Recommended — automates all passes
latexmk -xelatex paper.tex

# Clean auxiliary files
latexmk -c
```

**VS Code (LaTeX Workshop extension):**

1. Install extension: `LaTeX Workshop` (James Yu)
2. Open `.tex` file → `Ctrl+Alt+B` to build
3. `Ctrl+Alt+V` to open PDF preview (split view)
4. Auto-build on save: set `"latex-workshop.latex.autoBuild.run": "onSave"` in settings
5. Clean: `Ctrl+Shift+P` → `LaTeX Workshop: Clean up auxiliary files`


### Quarto

**Terminal:**

```bash
quarto check                          # verify all engines
quarto render report.qmd              # default format
quarto render report.qmd --to pdf     # specific format
quarto render report.qmd --to html
quarto render report.qmd --to revealjs
quarto preview report.qmd             # live reload in browser
quarto render                         # render entire project
quarto create project book   my-book  # new book project
quarto create project website my-site # new website
quarto use template owner/repo        # apply template
```

**VS Code (Quarto extension):**

1. Install extension: `Quarto` (Quarto Dev Team)
2. Open `.qmd` file → `Ctrl+Shift+K` to render (or click **Render** button)
3. `Ctrl+Shift+P` → `Quarto: Preview` for live reload
4. Format picker in the toolbar — switch between html / pdf / revealjs
5. Code cells run interactively with `Ctrl+Enter` (like a notebook)
6. Terminal shortcut: open integrated terminal with `` Ctrl+` ``

**RStudio:**

1. Open `.qmd` file → click **Render** button (top of editor)
2. Or: `Ctrl+Shift+K`
3. Background jobs panel shows render progress
4. Visual editor: toggle with `Ctrl+Shift+F4` for WYSIWYG editing


## Labs

| Lab | Environment | Focus |
|---|---|---|
| [Lab 1](labs/lab-01-latex-prism.md) | Prism (browser) | LaTeX document from scratch |
| [Lab 2](labs/lab-02-quarto-rstudio.md) | RStudio | Quarto report + slides |
| [Lab 3](labs/lab-03-quarto-vscode.md) | VS Code + terminal | Quarto project (website / book) |


## Resources

- LaTeX: https://www.latex-project.org
- Overleaf: https://www.overleaf.com
- Prism (OpenAI): https://openai.com/prism
- Quarto: https://quarto.org
- Quarto get started: https://quarto.org/docs/get-started/
- Quarto gallery: https://quarto.org/docs/gallery/
- TikZ examples: https://texample.net/tikz/examples/
- Zotero + Better BibTeX: https://retorque.re/zotero-better-bibtex/
