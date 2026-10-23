# STAT 656 — Homework 3

Classification of telecom customer churn with logistic regression and linear discriminant analysis (LDA).

Customers who leave a service are said to churn. This homework builds two linear classifiers that predict whether a customer will churn, then compares them on a held-out test set.

## Files

| File | Description |
| --- | --- |
| `3_homework.Rmd` | R Markdown source for the assignment |
| `3_homework.html` | Knitted report |
| `trainingData.csv` | Training customers (6,340 rows) |
| `testingData.csv` | Test customers (703 rows) |

## Data

Each row is one customer. The supervisor is `Churn` (`Yes` / `No`). Features include demographics, account tenure, contract and billing choices, and optional services:

`customerID`, `gender`, `SeniorCitizen`, `Partner`, `Dependents`, `tenure`, `MultipleLines`, `InternetService`, `OnlineSecurity`, `OnlineBackup`, `DeviceProtection`, `TechSupport`, `StreamingTV`, `StreamingMovies`, `Contract`, `PaperlessBilling`, `PaymentMethod`, `MonthlyCharges`, `TotalCharges`.

`customerID` is an identifier and is dropped before modeling. `TotalCharges` is the only column with missing values.

## What the analysis does

1. **Preprocessing.** Check missingness, impute `TotalCharges` from `MonthlyCharges` with a linear model fit on the training data only, convert qualitative columns to factors, expand them to full-rank dummy variables, and drop redundant “No internet service” indicators.
2. **Logistic regression.** Fit a binomial GLM with `caret` (`method = "glm"`, no resampling). Churn (`Yes`) is the event of interest. Report calibration, the confusion matrix, ROC, AUC, and the specificity at a sensitivity of at least 0.8.
3. **LDA.** Fit the same feature matrix with `caret` (`method = "lda"`) and report the same diagnostics.
4. **Comparison.** Compare accuracy, AUC, and specificity, including specificity at a sensitivity near 0.8.

`set.seed(1)` is set at the start of the report. Models are trained once on the full training set (`trainControl(method = "none")`); the test set is used only for evaluation.

## Requirements

R with these packages:

- `dplyr`, `readr`
- `caret` (and its dependencies, including `lattice` for the calibration plot)
- `pROC`
- `ggplot2`, `reshape2` (missing-data plot)
- `corrplot`
- `rmarkdown` (to knit the report)

## Reproduce

From this directory, in R:

```r
rmarkdown::render("3_homework.Rmd")
```

Or open `3_homework.Rmd` in RStudio and knit it. The report reads `trainingData.csv` and `testingData.csv` from the working directory.
