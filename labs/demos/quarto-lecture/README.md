# Clean Quarto Lecture Demos

These demos follow the lecture progression:

1. `01-report` - one `.qmd` rendered to HTML and PDF
2. `02-slides` - one `.qmd` rendered to RevealJS and Beamer
3. `03-website` - small website project
4. `04-book` - small book project with HTML, PDF, and EPUB formats
5. `05-template` - reusable report starter

Run commands from this repository root unless a demo says otherwise.

```bash
quarto render demos/quarto-lecture/01-report/report.qmd --to html
quarto render demos/quarto-lecture/01-report/report.qmd --to pdf
quarto render demos/quarto-lecture/02-slides/slides.qmd --to revealjs
quarto render demos/quarto-lecture/02-slides/slides.qmd --to beamer
quarto render demos/quarto-lecture/03-website
quarto render demos/quarto-lecture/04-book --to html
quarto render demos/quarto-lecture/04-book --to pdf
quarto render demos/quarto-lecture/04-book --to epub
quarto render demos/quarto-lecture/05-template/quarto-report-template/template.qmd --to html
quarto render demos/quarto-lecture/05-template/quarto-report-template/template.qmd --to pdf
```

Render the two slide formats one after the other, not at the same time, because they share temporary intermediate filenames.
