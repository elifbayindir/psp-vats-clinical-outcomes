# Clinical Outcomes After VATS for Primary Spontaneous Pneumothorax

A reproducible clinical data science project examining operative indication, postoperative course, and ipsilateral recurrence after VATS wedge resection with pleural abrasion.

> This repository uses a fully generated cohort of 650 records. No patient-level source data were copied, transformed, or published, and the numerical findings have no medical meaning.

![Adjusted Cox model](figures/05_cox_forest.png)

## Clinical questions

The analysis asks four practical questions.

1. How do operations for recurrent pneumothorax and prolonged air leak differ?
2. Which perioperative characteristics are associated with ipsilateral recurrence?
3. Does the operative bleb or bulla finding remain informative after adjustment?
4. Does perioperative information improve 24-month recurrence prediction?

## Analysis design

The notebook follows a complete observational workflow.

- Data dictionary, missingness review, and logical validation checks
- Median and interquartile-range summaries for skewed outcomes
- Mann-Whitney U tests with rank-biserial effect sizes and bootstrap intervals
- Chi-square or Fisher exact tests with odds ratios and Cramer's V
- Benjamini-Hochberg correction for exploratory test families
- Kaplan-Meier estimation and log-rank comparison
- Multivariable Cox proportional-hazards regression and assumption checks
- Five-fold out-of-fold prediction with ROC, precision-recall, Brier score, and calibration
- Paired bootstrap comparison of model AUCs
- Robust Poisson regression for hospital stay
- Missing-data sensitivity analysis and prospective event planning

## Result snapshot

Within the generated cohort, 177 ipsilateral recurrences occurred during follow-up. Failure to visualize a bleb or bulla was associated with a higher adjusted recurrence hazard, HR 2.72, 95% CI 1.96 to 3.77. The estimate remained similar across all missing-data sensitivity analyses.

For 24-month recurrence, the baseline model had an out-of-fold ROC AUC of 0.62. Adding perioperative information increased the AUC to 0.68. The paired difference was 0.07, 95% bootstrap CI 0.03 to 0.11. These values demonstrate the evaluation workflow and are not evidence for clinical use.

![Prediction performance](figures/06_prediction_discrimination.png)

## Repository structure

```text
.
├── README.md
├── requirements.txt
├── notebooks/
│   └── clinical_outcomes_after_vats.ipynb
├── data/
│   ├── synthetic_psp_vats_cohort.csv
│   └── data_dictionary.csv
├── figures/
│   └── 01–08 analysis figures
└── tables/
    └── validation, descriptive, model, and planning outputs
```

## Run the project

Create an environment, install the dependencies, and open the notebook from the repository root.

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
jupyter lab
```

Run all cells in `notebooks/clinical_outcomes_after_vats.ipynb`. The notebook recreates the cohort and overwrites every CSV table and PNG figure with the same fixed random seed.

## Interpretation

This project demonstrates statistical reasoning, reproducible analysis, and careful communication of observational results. It does not provide causal estimates, clinical validation, or treatment recommendations.
