# Credit Card Fraud Modeling with GLMs, GAMs, and GAMMs

This repository contains a University of Michigan STATS 501 final project investigating which transaction, customer, and card characteristics are associated with credit card fraud. The project compares three statistical modeling approaches and uses a simulation study to show how model performance changes as the underlying data-generating process becomes more complex.

## Project Overview

Fraud detection is a rare-event classification problem: only about 1.4% of the transactions in this dataset are labeled as fraudulent. In addition to this class imbalance, fraud risk may depend on nonlinear relationships and on groups such as merchants, merchant categories, and geographic regions.

The analysis asks two main questions:

1. Which transaction and customer characteristics are most strongly associated with fraud?
2. Do models that capture nonlinear patterns and group-level variation outperform standard logistic regression?

To answer these questions, we compare:

- **Generalized Linear Model (GLM):** logistic regression used as an interpretable baseline.
- **Generalized Additive Model (GAM):** extends logistic regression with smooth functions for nonlinear continuous effects.
- **Generalized Additive Mixed Model (GAMM):** adds random effects for merchants, merchant category codes (MCCs), and states to account for group-level heterogeneity.

## Data

The project uses a public Kaggle dataset of transaction records from 2017-2019. The data combine:

- Transaction information, including amount, time, merchant, and location
- Customer characteristics, such as income, debt, credit score, and account age
- Card characteristics, including brand, type, credit limit, and number of cards
- A binary indicator identifying whether each transaction was fraudulent

Key preprocessing steps included checking multicollinearity, engineering account-age and time-based features, log-transforming skewed variables, and filtering in-state transactions because the dataset contained no in-state fraud cases.

## Analysis

The empirical analysis first fits the three candidate models to the fraud data. Continuous predictors such as transaction amount, income, total debt, credit limit, and time since the previous transaction are modeled linearly in the GLM and with penalized smooths in the GAM and GAMM. The GAMM additionally models variation across merchants, MCCs, and states.

We also conducted a numerical simulation under three data-generating scenarios:

1. A linear relationship between predictors and the response
2. Nonlinear predictor effects
3. Nonlinear predictor effects with additional group-level random effects

Models were compared using two complementary metrics:

- **AUC**, which measures the ability to distinguish fraudulent from non-fraudulent transactions
- **Brier score**, which measures the accuracy and calibration of predicted probabilities

## Key Findings

- The GLM performed well when the simulated relationship was truly linear, but its performance declined when nonlinear effects were introduced.
- The GAM and GAMM handled nonlinear relationships more effectively than the GLM.
- The GAMM performed best in the most complex simulation scenario, achieving the highest AUC and lowest Brier score when both nonlinear effects and group-level variation were present.
- Fraud risk varied substantially across merchants, merchant categories, and geographic regions, supporting the use of a mixed-effects model.
- Transaction amount showed a U-shaped relationship with fraud risk: both very small transactions, which may represent card-testing behavior, and unusually large transactions were riskier than moderate-sized purchases.
- The fitted models also identified seasonal differences and associations with card characteristics, including a higher estimated risk for customers with more credit cards and a lower estimated risk for debit-card transactions.

Overall, the results suggest that fraud risk is not adequately represented by a single linear relationship. A model that accounts for both nonlinear effects and clustered observations provides a more realistic description of the data.

## Limitations and Future Work

Because fraud cases are rare, standard maximum-likelihood estimates may understate event probabilities and produce too many false negatives. The paper recommends evaluating rare-event methods such as Firth penalized logistic regression and resampling approaches such as SMOTE or majority-class undersampling in future work.

## Repository Contents

| File | Description |
| --- | --- |
| `new_dataset.csv` | Kaggle transaction data used in the analysis |
| `Project.Rmd` | Complete R Markdown analysis, including preprocessing, modeling, simulation, tables, and figures |
| `Stats501_FinalPaper.pdf` | Final project paper |
| `Stats501_FinalProject_latex_proj.zip` | LaTeX source files for the paper |

## Reproducing the Analysis

The complete analysis is contained in `Project.Rmd`. Place `new_dataset.csv` in the repository's root directory, open the project in RStudio, and knit the R Markdown file. Alternatively, run:

```r
rmarkdown::render("Project.Rmd")
```

### Software Requirements

- R 4.1 or later
- RStudio (recommended)

Install the required packages with:

```r
install.packages(c(
  "dplyr",
  "ggplot2",
  "mgcv",
  "pROC",
  "performance",
  "effects",
  "gridExtra",
  "rmarkdown"
))
```

## Authors

- Jake Gwinn
- Jiacheng You
- Huan Wang
- Li Wang
