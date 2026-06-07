# Coal Shadows & Clean Energy
### Does Coal Dependence Predict Renewable Energy Support? Evidence from Survey Data, EIA Production Records, and News Framing Analysis

**Alexandra Popescu** | QSS 45: AI & Machine Learning for Social Science | Dartmouth College | Spring 2026

---

## Overview

This project investigates whether a state's historical dependence on coal independently
predicts residents' support for renewable energy, or whether that relationship is fully
explained by individual-level political ideology and climate concern.

Using a cross-sectional survey (N ≈ 2,400), EIA State Energy Data System (SEDS) coal
production records (1960–2023), and a zero-shot NLP framing analysis of 122 news articles,
I find that coal dependence does **not** independently predict RE support once individual
attitudes are controlled (ICC ≈ 0). However, a significant coal × ideology interaction
reveals that conservative residents of coal-dependent states face a compounded disadvantage, their opposition to renewable energy is amplified beyond what ideology alone predicts.

---

## Repository Structure

```
coal-re-support/
│
├── README.md
│
├── code/
│   ├── 00_pull.ipynb          # Load and validate raw data files
│   ├── 01_merge.ipynb         # Merge survey + coal share + plant proximity
│   ├── 02_eda.ipynb           # Descriptive statistics and figures
│   ├── 03_regression.ipynb    # OLS, OLS + interaction, MLM, swing state
│   ├── 04_catboost_shap.ipynb # CatBoost gradient boosting + SHAP attribution
│   └── 05_framing.ipynb       # NewsAPI collection + BART-MNLI zero-shot classification
│
├── data/
│   ├── raw/                   # Original source files 
│   │   ├── renewables.xlsx    # Survey data, N ≈ 2,400, DV = Q137
│   │   ├── Prod_dataset.xlsx  # EIA SEDS coal production 1960–2023
│   │   ├── spectrum.csv       # Respondent demographics
│   │   └── plant.xlsx         # U.S. power plant locations (EIA Form 860)
│   └── processed/             # Outputs from 00_pull and 01_merge
│       └── merged_analysis.csv
│
└── output/
    ├── figures/               # All plots saved as .png
    │   ├── re_support_ranked_by_winner.png
    │   ├── state_support_bar.png
    │   ├── fossil_re_scatter.png
    │   ├── marginal_effects_interaction.png
    │   └── shap_beeswarm.png
    └── tables/                # Model outputs saved as .csv
        ├── summary_table_four_models.csv
        ├── state_framing_by_coal.csv
        └── news_framing.csv
```

---

## Key Findings

| Finding | Result |
|---|---|
| Coal share → RE support (OLS) | β = −0.018, p = .34 (not significant) |
| ICC (multilevel model) | ≈ 0.00 (place explains no additional variance) |
| Coal × Ideology interaction | β = −0.035, p = .049 (conservatives in coal states face double disadvantage) |
| Top SHAP predictor | Climate concern (strongest positive driver) |
| News framing χ² test | χ²= 5.18, p = .159 (no significant framing difference by coal share) |

---

## Data Sources

| Dataset | Source | Years |
|---|---|---|
| Renewable energy survey | Cross-sectional U.S. adult survey | 2024 |
| Coal production (SEDS) | U.S. Energy Information Administration | 1960–2023 |
| Power plant locations | EIA Form EIA-860 | 2023 |
| News articles | NewsAPI | Jan 2023 – Mar 2024 |

---

## Methods

- **OLS Regression** baseline + coal × ideology interaction (standardized predictors)
- **Multilevel Model (MLM)** random intercept by state, ICC decomposition
- **CatBoost + SHAP** gradient-boosted trees with Shapley feature attribution
- **Swing State Subgroup** restricted sample (N = 687), 12 swing states
- **Zero-Shot NLP** `facebook/bart-large-mnli` via HuggingFace, 4 frame labels

---

## Requirements

```bash
pip install pandas numpy statsmodels pymer4 catboost shap transformers newsapi-python openpyxl
```

Python 3.10+. All paths are relative — clone the repo and run notebooks in order from `code/`.

---

## How to Reproduce

```bash
git clone https://github.com/YOUR_USERNAME/coal-re-support.git
cd coal-re-support
pip install -r requirements.txt

# Run notebooks in order
jupyter notebook code/00_pull.ipynb
```

> **Note:** NewsAPI requires a free API key at [newsapi.org](https://newsapi.org).
> Set it as an environment variable: `export NEWS_API_KEY=your_key_here`

---

## Citation

Popescu, A. (2026). *Coal Shadows & Clean Energy: Does Fossil Fuel Dependence Predict
Renewable Energy Support?* QSS 45 Final Project, Dartmouth College.
