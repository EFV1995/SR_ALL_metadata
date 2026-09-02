# Pediatric ALL microbiota — reproducible analysis

This repository contains the reproducible quantitative and structured-synthesis analysis supporting the manuscript on microbiota alterations in pediatric acute lymphoblastic leukemia (ALL).

## Files

- `ALL_microbiota_analysis.Rmd` — final R Markdown analysis script.
- `ALL_microbiota_ultimate_input.xlsx` — curated analysis input containing study metadata, risk-of-bias information, cohort-overlap audit, meta-analysis inputs, digitisation provenance, and structured-synthesis inputs.

## Main quantitative analyses

The script performs exploratory random-effects meta-analyses for:

1. Diagnosis-time gut Shannon diversity.
2. Diagnosis-time gut Chao1 richness.
3. Extended Shannon sensitivity analysis including the De Pietri early-induction cohort.
4. Extended richness sensitivity analysis including observed species from De Pietri.

Effect sizes are Hedges' g standardized mean differences. Negative values indicate lower diversity or richness in ALL. Random-effects models use REML estimation with Hartung-Knapp inference.

The primary diagnosis-time analyses include Gao 2020, Rajagopala 2020, and Chua 2020. Extended sensitivity analyses add De Pietri early-induction data.

## Requirements

R and RStudio are recommended. Install the required packages before rendering:

```r
install.packages(c(
  "rmarkdown", "tibble", "readxl", "dplyr", "tidyr", "ggplot2",
  "stringr", "metafor", "openxlsx", "knitr"
))
```

## How to run

Place the `.Rmd` and `.xlsx` files in the same directory and run:

```r
rmarkdown::render("ALL_microbiota_analysis_GitHub_final.Rmd")
```

By default, outputs are written to:

```text
analysis_outputs/
```

The script also records `sessionInfo.txt` for reproducibility.

## Main outputs

The analysis generates:

- `forest_Shannon_main.png` / `.pdf`
- `forest_Shannon_extended.png` / `.pdf`
- `forest_Richness_main.png` / `.pdf`
- `forest_Richness_extended.png` / `.pdf`
- descriptive direction heatmaps
- taxon-direction heatmap
- `analysis_results.xlsx`
- `analysis_manifest.csv`
- `sessionInfo.txt`

The final manuscript multi-panel figures may be assembled or cosmetically reformatted from these vector outputs without altering the underlying numerical analyses.

## Interpretation and analysis guardrails

- The meta-analyses are exploratory.
- Primary analyses are restricted to diagnosis-time, pretreatment gut samples and metric-specific comparisons.
- Oral and gut microbiota are not pooled together.
- Shannon and Chao1 are not pooled into a single effect.
- Repeated time points, samples, taxa, or overlapping publications are not treated as independent studies.
- Publication-bias tests, funnel plots, and meta-regression are not used because the number of studies is too small.
- Descriptive heatmaps are not inferential pooled analyses.
- Risk of bias should be interpreted using design-appropriate JBI item-level judgments rather than an aggregate quality score.

## Data provenance

The workbook contains the numerical inputs and provenance information used for the analysis, including reconstructed values where applicable. Figure-derived or converted summary statistics should not be described as originally reported means and standard deviations.

## Reproducibility

The analysis uses relative paths and contains no user-specific absolute paths, credentials, or API keys. Keep the workbook filename unchanged unless the `input_xlsx` parameter in the R Markdown file is also changed.

