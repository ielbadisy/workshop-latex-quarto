# Lab 2 - Quarto with RStudio

**Environment:** RStudio (desktop)  
**Duration:** 30 minutes  
**Goal:** create a reproducible report in HTML and PDF, then convert it to a RevealJS slide deck - all from the same `.qmd` source in RStudio.


## Setup (2 min)

1. Open RStudio
2. Check Quarto is available: run in the **Console**

```r
system("quarto check")
```

3. Create a new folder `lab-quarto-rstudio/` (File → New Project → New Directory → Quarto Project)
4. RStudio generates `lab-quarto-rstudio.qmd` - open it


## Task 1 - Minimal HTML Report (5 min)

Replace the default content with:

```yaml
title: "Reproducible Analysis Report"
author: "Your Name"
date: today
format:
  html:
    toc: true
    code-fold: true
    theme: cosmo
execute:
  warning: false
  message: false
```

```markdown
## Introduction

This report was built with Quarto in RStudio.
All results update automatically when the data changes.

## Data

We use the built-in `mtcars` dataset.
It contains `r nrow(mtcars)` cars and `r ncol(mtcars)` variables.
```

Click **Render** (or `Ctrl+Shift+K`). The HTML opens in the Viewer pane.


## Task 2 - Add a Figure with Cross-Reference (5 min)

Add below the Data section:

````markdown
## Results

```{r}
#| label: fig-mpg
#| fig-cap: "Miles per gallon by number of cylinders."
#| echo: false
boxplot(mpg ~ cyl, data = mtcars,
        xlab = "Cylinders", ylab = "MPG",
        col = c("#4e79a7", "#f28e2b", "#e15759"))
```

@fig-mpg shows that cars with fewer cylinders achieve higher fuel efficiency.
````

Render. Verify the figure appears with a caption and the `@fig-mpg` reference resolves correctly.


## Task 3 - Add PDF Output (5 min)

Extend the YAML to produce both HTML and PDF:

```yaml
format:
  html:
    toc: true
    code-fold: true
    theme: cosmo
  pdf:
    toc: true
    number-sections: true
    pdf-engine: xelatex
```

Render with `Ctrl+Shift+K`. RStudio renders the default format (HTML).

To render PDF explicitly, run in the **Terminal** tab (not Console):

```bash
quarto render lab-quarto-rstudio.qmd --to pdf
```

Open the PDF in the Files pane. Verify figure and table of contents.


## Task 4 - Add an Equation and Citation (5 min)

Add to `references.bib` (create the file in the project folder):

```bibtex
@book{tufte2001,
  author    = {Tufte, Edward R.},
  title     = {The Visual Display of Quantitative Information},
  publisher = {Graphics Press},
  year      = {2001}
}
```

Add to the YAML: `bibliography: references.bib`

Add to the Results section:

```markdown
The linear model fitted is:

$$
\text{mpg}_i = \beta_0 + \beta_1 \cdot \text{cyl}_i + \varepsilon_i
$$ {#eq-lm}

@eq-lm was estimated by ordinary least squares [@tufte2001].
```

Render both formats. Verify equation numbering and citation.


## Task 5 - Convert to RevealJS Slides (5 min)

Create a new file `slides.qmd` in the same folder:

```yaml
title: "Analysis Highlights"
author: "Your Name"
format:
  revealjs:
    theme: default
    slide-number: true
    incremental: true
execute:
  echo: false
  warning: false
```

```markdown
## Key Finding

- `r nrow(mtcars)` cars in the dataset
- Cylinders strongly predict fuel efficiency

## MPG by Cylinders
```

````markdown
```{r}
#| label: fig-slide-mpg
#| fig-cap: "MPG distribution."
boxplot(mpg ~ cyl, data = mtcars, col = c("#4e79a7","#f28e2b","#e15759"))
```
````

Render:

```bash
quarto render slides.qmd --to revealjs
```

Open the `.html` in a browser. Navigate slides with arrow keys.


## Deliverable

You must produce three output files from the same data:

- [ ] `lab-quarto-rstudio.html` - report with figure, equation, citation
- [ ] `lab-quarto-rstudio.pdf` - same content as PDF
- [ ] `slides.html` - RevealJS slide deck with at least 2 slides and one figure


## Compile Reference (RStudio)

| Action | Shortcut |
|---|---|
| Render (default format) | `Ctrl+Shift+K` |
| Run current chunk | `Ctrl+Enter` |
| Run all chunks | `Ctrl+Alt+R` |
| Toggle visual editor | `Ctrl+Shift+F4` |
| Open terminal | `Alt+Shift+R` |
| Render specific format | Terminal: `quarto render file.qmd --to pdf` |
