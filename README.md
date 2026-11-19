# Vorhersage des Einkommens auf Basis von Bildungsmerkmalen (Predicting Income from Educational Characteristics) – NEPScomp

Data project in the Social Data Science & Communication program, TH Nürnberg Georg Simon Ohm

| | |
|---|---|
| Student | Temirlan Anarkulov |
| Supervision | Prof. Julia Plaß (TH Nürnberg), content advisor Michael Bergrab (LIfBi) |
| Period | October 2026 to January 2027 |

## Research Question

Can a person's later income be predicted from their educational characteristics?

- Describe the data (summary statistics and visualizations)
- Build predictive models for income and compare different methods
- Evaluate the approaches and select a model

## Data

German National Educational Panel Study (NEPS), NEPScomp, Starting Cohort 6 (Adults), version 17.0.0, published by the Leibniz Institute for Educational Trajectories (LIfBi), Bamberg: https://www.neps-data.de

| File | Variables used |
|---|---|
| SC6_Basics | Gender, year of birth, parents' education |
| SC6_Education | Highest degree (ISCED-2011) |
| SC6_spEmp | Net income, weekly working hours, mini-job |
| SC6_spSchool | Final grade |

**Data protection:** The NEPS data is subject to a data use agreement and is not included in this repository. `data/` and `output/` (personal data) are excluded via `.gitignore`. `figures/` and `tables/` contain aggregated results only.

## How to Run

Requirements: Python 3.12

```bash
pip install pandas numpy pyreadstat matplotlib seaborn scipy scikit-learn joblib
```

Put the NEPS files (.dta) into a `data/` folder, then run the scripts in order:

```bash
python 01_data_preparation.py
python 02_descriptive_analysis.py
python 03_models.py
python 04_evaluation.py
```

The `output/` folder is created automatically.

## Approach

| Step | Content |
|---|---|
| Preparation | NEPS missing codes (negative values) treated as missing; last valid net income per person (excluding mini-jobs); highest degree in 7 groups; academic family = at least one parent with a university / university of applied sciences degree |
| Sample | Net income €300–15,000, full-time only (≥ 35 hrs/week): n = 8,667 |
| Descriptive | Median/quartiles, histogram, boxplots + eta², Spearman correlation, group means |
| Models | Baseline (median), linear regression, Lasso, random forest, gradient boosting; target variable log(income), metrics in euros |
| Evaluation | 80/20 train/test split, 5-fold cross-validation, RMSE, MAE, R², permutation importance |

## Key Results

- The highest degree alone explains about 18% of income differences (η² = 0.18).
- All models reach a test R² of about 0.30 (RMSE about €1,320) and clearly beat the baseline.
- Complex models (random forest, gradient boosting) are barely better than linear regression.
- The most important predictor is the degree; final grade and parents' education add little once the degree is known.

## Use of AI

As required, AI-generated parts are labeled. AI-generated code blocks are marked like this:

```python
# >>> KI-generiert (Claude), von mir ausgeführt und nachvollzogen
...
# <<< Ende KI
```

| File | Lines | Type | Tool |
|---|---|---|---|
| README.md | entire file | AI-generated, reviewed and adapted by me | Claude (Anthropic) |
| .gitignore | entire file | written by me | – |
| 01_data_preparation.py | entire file | AI-generated, run and understood by me | Claude (Anthropic) |
| 02_descriptive_analysis.py | entire file | AI-generated, run and understood by me | Claude (Anthropic) |
| 03_models.py | entire file | AI-generated, run and understood by me | Claude (Anthropic) |
| 04_evaluation.py | entire file | AI-generated, run and understood by me | Claude (Anthropic) |
