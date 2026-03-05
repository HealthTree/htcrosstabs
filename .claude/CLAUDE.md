# htcrosstabs

R package (v1.1.0) that takes survey data as a data frame and formats it into cross-tabulation tables in HealthTree's preferred style. Authored by Alex Brown.

## What It Does

Pipeline: create a `crosstab` object → extract summary statistics → add formatted rows → run statistical tests → render to HTML/LaTeX.

1. `crosstab()` or `crosstab_stacked()` — create crosstab object from data frame
2. `get_*()` — extract stats (mean, median, SD, counts, proportions, percentages, quartiles)
3. `add_*_row()` / `add_*_table()` — add formatted rows or pre-built templates
4. Statistical tests: ANOVA, chi-square, Rao-Scott chi-square with post-hoc comparisons
5. `kbl()` — render to HTML/LaTeX via kableExtra wrapper with auto-footnotes and row groupings

## Data Type System (S3 classes)

- **Categorical** — character/factor/logical
- **Numeric** — numeric
- **Likert** — categorical with named numeric mapping
- **Multi-response** — list-column (multiple answers per row)

## Directory Structure

```
├── R/              # 21 source files (constructors, getters, validation, stats, formatting)
├── data/           # 7 example .rda datasets
├── man/            # roxygen2-generated documentation
├── tests/testthat/ # 18 test files (testthat edition 3)
├── DESCRIPTION     # Package metadata
└── NAMESPACE       # Exports
```

## Dependencies

**Runtime**: dplyr, tidyr, rlang, assertthat, crayon, kableExtra, knitr, Hmisc, rstatix, stats, survey
**Testing**: testthat >= 3.0.0
**Requires**: R >= 3.5

## How to Use

```r
devtools::install_github("HealthTree/htcrosstabs")
library(htcrosstabs)

# Quick stacked crosstab
crosstab_stacked(your_df, "cohort_col")

# Manual pipeline
ct <- crosstab(your_df, "cohort_col")
ct <- add_count_row(ct)
ct <- add_percent_row(ct, "some_variable")
kbl(ct)
```

Run tests: `devtools::test()`
