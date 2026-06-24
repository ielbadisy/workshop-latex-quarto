# Lab 1 - LaTeX with Prism

**Environment:** Prism (browser - no installation needed)  
**Duration:** 30 minutes  
**Goal:** write, compile, and export a minimal scientific document entirely in the browser using Prism's AI-assisted LaTeX editor.


## Setup (2 min)

1. Go to **https://openai.com/prism** and sign in with your OpenAI account
2. Click **New Project** → name it `lab-latex`
3. Prism creates a default `main.tex` - leave it open


## Task 1 - Minimal Document (5 min)

Replace the default content with:

```latex
\documentclass[12pt, a4paper]{article}

\usepackage{amsmath, amssymb}
\usepackage{graphicx}
\usepackage{booktabs}
\usepackage[style=apa, backend=biber]{biblatex}
\addbibresource{references.bib}

\title{My First \LaTeX{} Document}
\author{Your Name}
\date{\today}

\begin{document}
\maketitle
\tableofcontents

\section{Introduction}
This document was written in \LaTeX{} using Prism.

\section{Methods}
We describe our approach here.

\printbibliography
\end{document}
```

Click **Compile** (top right). Verify the PDF appears on the right panel.


## Task 2 - Add a Math Equation (5 min)

Inside `\section{Methods}`, add:

```latex
Let $Y_1, \ldots, Y_n \overset{iid}{\sim} N(\mu, \sigma^2)$.
The log-likelihood is:

\begin{equation}
  \ell(\mu, \sigma^2) = -\frac{n}{2}\log(2\pi\sigma^2)
  - \frac{1}{2\sigma^2} \sum_{i=1}^n (y_i - \mu)^2
  \label{eq:loglik}
\end{equation}

See Equation~\ref{eq:loglik} for the full expression.
```

Compile. Verify the equation is numbered and the reference resolves.


## Task 3 - Add a Table (5 min)

Add a new section and insert a publication-quality table:

```latex
\section{Results}

\begin{table}[htbp]
  \centering
  \caption{Descriptive statistics by group.}
  \label{tab:desc}
  \begin{tabular}{lrr}
    \toprule
    Variable & Control & Treatment \\
    \midrule
    Age (years) & $45.2 \pm 12.1$ & $46.8 \pm 11.4$ \\
    BMI         & $27.3 \pm 4.8$  & $26.9 \pm 5.1$  \\
    n           & 42              & 39              \\
    \bottomrule
  \end{tabular}
\end{table}

See Table~\ref{tab:desc} for descriptive statistics.
```


## Task 4 - Add a Bibliography Entry (5 min)

Create a new file `references.bib` in Prism and add:

```bibtex
@article{cox1972,
  author  = {Cox, D. R.},
  title   = {Regression Models and Life-Tables},
  journal = {Journal of the Royal Statistical Society B},
  year    = {1972},
  volume  = {34},
  pages   = {187--220}
}
```

In `main.tex`, add to the Introduction:

```latex
The Cox proportional hazards model \parencite{cox1972}
is widely used in survival analysis.
```

Compile. Verify the reference appears in the bibliography.


## Task 5 - Use AI Assistance in Prism (5 min)

Try one of the following with Prism's built-in GPT-5.2:

- **Ask:** "Add a TikZ flowchart showing patient inclusion → randomization → follow-up"
- **Ask:** "Convert this table to a three-column layout with a footnote"
- **Debug:** introduce a deliberate error (e.g., `\end{equaton}`) and ask Prism to fix it


## Challenge (if time allows)

Adapt the document to use the `elsarticle` class:

```latex
\documentclass[review, 12pt]{elsarticle}
```

- Observe how the title page, abstract block, and section headings change
- Add `\begin{abstract}...\end{abstract}` before `\section{Introduction}`
- Compile and compare with the `article` output


## Deliverable

Export your compiled PDF from Prism. It must contain:

- [ ] Title page with your name and today's date
- [ ] Table of contents
- [ ] At least one numbered equation with a cross-reference
- [ ] A `booktabs` table with caption and label
- [ ] At least one citation in the bibliography
