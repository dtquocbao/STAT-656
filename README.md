# STAT 656

Homework for STAT 656. Each assignment is an R Markdown report with a knitted HTML file in this directory. Later homeworks will be added the same way.

Large data files stay on disk. `.gitignore` excludes `*.csv`, `*.Rdata`, the `database/` folder, and downloaded Bureau of Transportation Statistics extracts.

## Homeworks

### Homework 1 — Airline flight delays

| File | Description |
| --- | --- |
| `1_homeworkFlight.Rmd` | R Markdown source |
| `1_homeworkFlight.html` | Knitted report |

Build a 2023 on-time flight data set from monthly Bureau of Transportation Statistics reports, then summarize cancellations, missing values, flights by day of the week, the month with the highest proportion of late departures, and the airport pair with the worst median departure delay (at least 1,000 flights).

Download the monthly extracts into a `database/` folder next to the R Markdown file before knitting. The report uses `tidyverse` and `here`.

### Homework 2 — Bootstrap and linear regression

| File | Description |
| --- | --- |
| `2_homework.Rmd` | R Markdown source |
| `2_homework.html` | Knitted report |

Uses the combined flight object from Homework 1, saved locally as `2023flights.Rdata`. Compare winter and summer mean arrival delay with a pooled two-sample interval and a bootstrap interval, then fit a linear regression of arrival delay on departure delay and evaluate it on a train, validation, and test split.

Packages: `dplyr`, `caret`, `doParallel`.

### Homework 3 — Classification

| File | Description |
| --- | --- |
| `3_homework.Rmd` | R Markdown source |
| `3_homework.html` | Knitted report |
| `trainingData.csv` | Training customers (6,340 rows), kept locally |
| `testingData.csv` | Test customers (703 rows), kept locally |

Predict telecom customer churn (`Yes` / `No`) from account, contract, and service features. Impute missing `TotalCharges` from `MonthlyCharges` using the training data only, encode qualitative features as full-rank dummies, then compare logistic regression and linear discriminant analysis on calibration, accuracy, ROC, AUC, and specificity.

Packages: `dplyr`, `readr`, `caret`, `pROC`, `ggplot2`, `reshape2`, `corrplot`.

`set.seed(1)` is set in the report. Both models are fit once on the full training set (`trainControl(method = "none")`).

## Reproduce

From this directory, in R:

```r
rmarkdown::render("1_homeworkFlight.Rmd")
rmarkdown::render("2_homework.Rmd")
rmarkdown::render("3_homework.Rmd")
```

Or open an `.Rmd` file in RStudio and knit it. Each report reads its data from the working directory. Install the packages listed for that homework, plus `rmarkdown`, before knitting.
