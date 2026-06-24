# Lab 3 - Quarto with VS Code (Command Line + Editor)

**Environment:** VS Code + Quarto extension + integrated terminal  
**Duration:** 30 minutes  
**Goal:** create a multi-output Quarto project (website or book) from the command line, edit it in VS Code, and render all formats.


## Setup (3 min)

1. Open VS Code
2. Install the **Quarto** extension (Quarto Dev Team) if not already installed:
   - `Ctrl+Shift+X` → search "Quarto" → Install
3. Open the integrated terminal: `` Ctrl+` ``
4. Verify Quarto is installed:

```bash
quarto --version
quarto check
```

Both commands should complete without errors.


## Task 1 - Create a Website Project from the Terminal (5 min)

In the terminal:

```bash
# Create a new website project
quarto create project website my-site
cd my-site

# Preview it immediately
quarto preview
```

A browser tab opens with the default site. Leave the preview running - it reloads automatically on every save.

In VS Code: `File → Open Folder → my-site`

Explore the generated files:

```text
my-site/
  _quarto.yml      ← project config and navbar
  index.qmd        ← home page
  about.qmd        ← about page
  styles.css       ← custom CSS
```


## Task 2 - Add a Page with Code and Figures (7 min)

Create a new file `analysis.qmd` in `my-site/`:

```yaml
title: "Data Analysis"
```

````markdown
## Overview

This page shows a quick analysis of the `mtcars` dataset.
The dataset contains `r nrow(mtcars)` observations.

## Distribution of MPG

```{r}
#| label: fig-mpg
#| fig-cap: "MPG distribution across cylinder classes."
#| echo: false
#| warning: false
hist(mtcars$mpg, col = "#4e79a7", border = "white",
     main = "", xlab = "Miles per gallon")
```

As shown in @fig-mpg, most cars achieve between 15 and 25 MPG.

## Model

$$
\text{mpg}_i = \beta_0 + \beta_1 \cdot \text{hp}_i + \varepsilon_i
$$ {#eq-model}

@eq-model was fitted with ordinary least squares.
````

Add the new page to the navbar in `_quarto.yml`:

```yaml
project:
  type: website

website:
  title: "My Research Site"
  navbar:
    left:
      - href: index.qmd
        text: Home
      - href: analysis.qmd
        text: Analysis
      - href: about.qmd
        text: About

format:
  html:
    toc: true
    theme: cosmo
```

Save - the preview reloads and shows the new Analysis page.


## Task 3 - Add PDF Output to the Project (5 min)

Stop the preview (`Ctrl+C`) and add a PDF format to `_quarto.yml`:

```yaml
format:
  html:
    toc: true
    theme: cosmo
  pdf:
    toc: true
    number-sections: true
    pdf-engine: xelatex
```

Render the entire project:

```bash
quarto render
```

Check the `_site/` folder - HTML files. Check `_output/` (if set) or alongside each `.qmd` - PDF files.

Render only one format:

```bash
quarto render analysis.qmd --to pdf
quarto render analysis.qmd --to html
```


## Task 4 - Create a Book Project (5 min)

In the terminal, go back to the parent folder and create a book:

```bash
cd ..
quarto create project book my-book
cd my-book
```

Generated structure:

```text
my-book/
  _quarto.yml
  index.qmd      ← preface
  intro.qmd      ← chapter 1
  summary.qmd    ← chapter 2
  references.qmd
  references.bib
```

Render to all formats:

```bash
quarto render --to html
quarto render --to pdf
quarto render --to epub
```

Check `_book/` - you now have an HTML site, a PDF, and an EPUB from the same source.


## Task 5 - VS Code Shortcuts for Quarto (5 min)

Practice these VS Code workflows:

| Action | Method |
|---|---|
| Render current file | `Ctrl+Shift+K` |
| Preview (live reload) | `Ctrl+Shift+P` → `Quarto: Preview` |
| Run code chunk | `Ctrl+Enter` on chunk |
| Run all chunks | `Ctrl+Alt+R` |
| Insert code chunk | `Ctrl+Alt+I` |
| Toggle source / visual | Button top-right of editor |
| Open terminal | `` Ctrl+` `` |
| Render from terminal | `quarto render file.qmd --to pdf` |
| Format selector | YAML `format:` → change key |

**Live editing workflow:**

1. Open `analysis.qmd` in VS Code
2. Run `quarto preview` in terminal - browser opens
3. Edit and save → browser reloads automatically
4. When done: `quarto render --to pdf` for the final PDF


## Deliverable

You must produce:

- [ ] A working website in `my-site/` - at least 3 pages, one with a figure and one equation
- [ ] A PDF version of at least one page rendered from the terminal
- [ ] A book project in `my-book/` rendered to HTML + PDF + EPUB


## Full Compile Reference (Terminal + VS Code)

### Quarto - Terminal

```bash
quarto --version                          # check version
quarto check                              # diagnose engines
quarto render file.qmd                    # default format
quarto render file.qmd --to html          # HTML only
quarto render file.qmd --to pdf           # PDF only
quarto render file.qmd --to revealjs      # RevealJS slides
quarto render file.qmd --to beamer        # Beamer PDF slides
quarto render file.qmd --to epub          # EPUB
quarto render file.qmd --to docx          # Word
quarto render                             # entire project
quarto preview                            # live preview
quarto preview file.qmd                   # preview one file
quarto create project book      my-book   # new book
quarto create project website   my-site   # new website
quarto use template owner/repo            # apply template
```

### LaTeX - Terminal

```bash
latexmk -xelatex paper.tex        # compile (all passes, recommended)
latexmk -pdf paper.tex             # compile with pdflatex
latexmk -c                         # clean auxiliary files
latexmk -C                         # clean including PDF
xelatex paper.tex                  # single pass (xelatex)
pdflatex paper.tex                 # single pass (pdflatex)
biber paper                        # process bibliography (biblatex)
```

### VS Code keyboard shortcuts

| Tool | Action | Shortcut |
|---|---|---|
| Quarto | Render | `Ctrl+Shift+K` |
| Quarto | Preview | `Ctrl+Shift+P` → Quarto: Preview |
| Quarto | Insert chunk | `Ctrl+Alt+I` |
| Quarto | Run chunk | `Ctrl+Enter` |
| LaTeX Workshop | Build | `Ctrl+Alt+B` |
| LaTeX Workshop | View PDF | `Ctrl+Alt+V` |
| VS Code | Terminal | `` Ctrl+` `` |
| VS Code | Command palette | `Ctrl+Shift+P` |
| VS Code | Explorer | `Ctrl+Shift+E` |
