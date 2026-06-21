# Crop Yield

<!-- badges: start -->
![GitHub last commit](https://img.shields.io/github/last-commit/USERNAME/REPO_NAME?style=flat-square)
![Language](https://img.shields.io/badge/Language-R-blue?style=flat-square)
![Analysis](https://img.shields.io/badge/Method-IPTW-orange?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)
<!-- badges: end -->

## Table of Contents

- [Description](#description)
- [Research Question](#research-question)
- [Methodology](#methodology)
- [Files](#files)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Interpreting the IPTW Result](#interpreting-the-iptw-result)
- [License](#license)
- [Author](#author)

## Description

This project estimates the causal effect of cover crop adoption on wheat yields using inverse probability of treatment weighting (IPTW). The analysis uses county-level data adapted from the 2017 Census of Agriculture and compares counties with at least 10% of farms using cover crops to counties with less than 10% using cover crops.

## Research Question

Does cover crop use increase wheat crop yields?

## Methodology

The analysis follows these steps:

1. Load and inspect the data.
2. Assess initial covariate balance between treatment groups.
3. Estimate IPTW weights using a propensity score model.
4. Recheck balance after weighting.
5. Fit a weighted regression model to estimate the causal effect of cover crop use on wheat yield.

## Files

- `notebook.Rmd` — main analysis notebook.
- `farms.csv` — dataset used for the analysis.
- `solution.Rmd` — reference solution file, if provided.

## Requirements

This project uses the following R packages:

- `cobalt`
- `WeightIt`
- `lmtest`
- `sandwich`

## Installation

Install the required packages in R:

```r
install.packages(c("cobalt", "WeightIt", "lmtest", "sandwich"))
```

## Usage

1. Open `notebook.Rmd` in RStudio.
2. Make sure `farms.csv` is in your working directory.
3. Run the notebook from top to bottom.
4. Review the balance plots, weighting results, and final model output.

## Interpreting the IPTW Result

The final weighted regression estimates the **average treatment effect** of cover crop adoption on wheat yield. The coefficient for `cover_10` shows the expected difference in wheat yield, measured in bushels per acre, between counties with at least 10% cover crop adoption and counties with less than 10% adoption, after adjustment for confounding variables through IPTW.

- If the coefficient is **positive**, the result suggests that cover crop adoption is associated with higher wheat yields after weighting.
- If the coefficient is **negative**, the result suggests lower wheat yields after weighting.
- The robust standard errors from `coeftest()` should be used for inference because they account for the weighted regression setup.

In short, this estimate should be interpreted as a causal effect under the assumptions of the IPTW design.

## License

MIT License.

## Author

Torbjorn Carlsen
