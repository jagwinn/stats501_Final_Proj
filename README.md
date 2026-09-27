# Files

1. new_dataset.csv: 
   1. The Kaggle data for the project
2. Project.Rmd: 
   1. Full rmarkdown analysis
3. Stats501_FinalProject_latex_proj.zip:
   1. Compressed Latex Code for the Paper
4. Stats501_FinalPaper.pdf
   1. Complied PDF of the report

---

# Reproducibility Instructions

This repository contains the code and report for our final project on modeling credit card fraud using generalized linear models (GLMs), generalized additive models (GAMs), and mixed-effects GAMs (GAMMs).

The main analysis is in:

- `Project.Rmd`

Running this R Markdown file will reproduce all results, tables, and figures in the report.

---

## 1. Software Requirements

- **R** (version 4.1 or later recommended)
- **RStudio** (recommended for knitting the R Markdown file)

### Required R Packages

Please install the following packages before running the code:

```r
install.packages(c(
  "dplyr",
  "ggplot2",
  "mgcv",
  "pROC",
  "performance",
  "effects",
  "gridExtra"
))
```
