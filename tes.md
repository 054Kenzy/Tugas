<div align="center">

# Indonesia Provincial Digital Divide Analysis

### A reproducible statistical case study of the relationship between internet access and poverty across Indonesian provinces in 2024

</div>

---

## 📌 Overview

This repository contains a notebook-based statistical analysis of the relationship between provincial internet access and poverty in Indonesia in 2024. The workflow combines data cleaning, province-level merging, exploratory analysis, Pearson correlation, linear regression, chi-square testing, Fisher's exact test, and residual analysis.

The project is designed as a portfolio case study for technical reviewers who want to inspect both the analytical process and the statistical evidence. The emphasis is on traceable preprocessing, quantified findings, and transparent limitations rather than on deployment.

---

## ❓ Problem Statement

**Context:**  
Provincial internet access and poverty rates are both publicly available in BPS statistical tables, but the raw tables do not explain whether the two variables move together, how strong the relationship is, or whether that relationship remains visible when the data is examined from both numeric and categorical perspectives.

**Gap:**  
A direct table lookup is not enough for portfolio-grade analysis. The missing layer is a reproducible statistical workflow that cleans the data, aligns the provincial units, checks data quality, and validates the association with multiple methods.

**Solution:**  
This project merges the two BPS tables at province level, cleans inconsistent entries, removes missing values, and evaluates the relationship through correlation, regression, chi-square testing, Fisher's exact test, and residual-based interpretation. The result is a compact but evidence-driven analysis of the digital divide across Indonesian provinces.

---

## 🎥 Demo & Screenshots

The figures below should be exported from the notebooks and saved under `docs/img/`.

| Data Audit Snapshot | Regression Fit |
|:---:|:---:|
| ![Data audit snapshot](docs/img/01_data_audit_snapshot.png) | ![Regression scatter](docs/img/02_regression_scatter.png) |
| Cleaned sample, missing-value handling, and final province count. | Scatter plot with regression line, equation, and R² annotation. |

| Chi-Square Diagnostics | Fisher 2×2 Summary |
|:---:|:---:|
| ![Chi-square diagnostics](docs/img/03_chi_square_diagnostics.png) | ![Fisher summary](docs/img/04_fisher_2x2_summary.png) |
| Observed, expected, and standardized residual heatmaps. | Binary contingency table used for Fisher's exact test. |

---

## 🛠️ Tech Stack

| Layer | Technology | Role in the Project |
|:---:|:---:|---|
| Language | Python 3 | Main language for the full analytical workflow |
| Environment | Jupyter Notebook | Interactive analysis, validation, and reporting |
| Data Processing | Pandas, NumPy | Cleaning, transformation, merging, and tabulation |
| Visualization | Matplotlib, Seaborn | Distribution plots, scatter plots, heatmaps, and diagnostic charts |
| Statistics / Modeling | SciPy, Scikit-learn | Correlation, regression, chi-square, and assumption checks |
| Version Control | Git + GitHub | Repository management and portfolio presentation |

---

## 📊 Dataset

### Metadata

| Atribut | Detail |
|---|---|
| **Source** | BPS provincial statistical tables |
| **Link** | Not embedded in the notebook export |
| **Size** | Raw: 39 × 4 and 39 × 10; Final merged dataset: 37 × 5 |
| **Format** | CSV |
| **License** | Public statistical tables; code license can be added separately |
| **Coverage** | Indonesia, provincial level, 2024 |
| **Accessed on** | Not recorded in the notebook export |

### Data Dictionary (Key Columns)

| Column | Type | Description | Example Value |
|---|:---:|---|---|
| `Provinsi` | `str` | Province name used as the merge key | `ACEH` |
| `Internet_Perkotaan` | `float` | Percentage of households in urban areas that accessed the internet in the last 3 months | `92.60` |
| `Internet_Perdesaan` | `float` | Percentage of households in rural areas that accessed the internet in the last 3 months | `86.97` |
| `Internet_Total` | `float` | Overall provincial internet access percentage | `88.95` |
| `Kemiskinan_Persen` | `float` | Provincial poverty rate used in the analysis | `14.23` |

> The raw files should live in `data/raw/`, and the cleaned merged dataset should be saved in `data/processed/`.

---

## 📈 Results & Performance

1. **The cleaned analytic dataset contains 37 provinces and 5 variables.**  
   The original merged data had 38 provinces, but one row was removed because `Internet_Perdesaan` was missing for DKI Jakarta. This keeps the analysis internally consistent.  

2. **Poverty and internet access show a very strong negative linear association.**  
   Pearson correlation is `r = -0.8215`, with `p-value < 0.001`, which indicates that higher poverty rates are associated with lower internet access across provinces.  

3. **The regression model explains a substantial portion of variation.**  
   The fitted line is `Y = 108.1643 + (-1.9603)X`, with `R² = 0.6748` and adjusted `R² = 0.6655`. Interpreted practically, a 1% increase in poverty is associated with an estimated 1.9603% decrease in internet access in this dataset.  

4. **The regression is informative, but not fully clean on assumptions.**  
   Normality of residuals passes (`Shapiro-Wilk p = 0.092351`), while homoskedasticity and no-autocorrelation checks do not (`Breusch-Pagan p = 0.000006`, `Durbin-Watson = 1.0366`). That means the model is best read as an exploratory association result, not a final causal model.  

5. **The categorical view confirms the same pattern.**  
   Chi-square testing gives `χ² = 20.1823` with `p = 0.000460`, and Cramer's V is `0.5222`, which indicates a strong association. Because `77.8%` of expected frequencies are below 5, Fisher's exact test is also used and remains significant (`p = 0.035853`).  

6. **The strongest cell is the high-poverty / low-internet combination.**  
   The category `[Tinggi × Rendah]` contributes `42.50%` of the total chi-square statistic, which makes it the clearest signal in the contingency analysis.

---

## ⚠️ Notes / Limitations

- **Scope:** The analysis is limited to Indonesian provinces in 2024 and should not be generalized to other years or country-level contexts without revalidation.
- **Data:** One province was removed because of a missing rural internet value. The final dataset is still usable, but the drop should be documented clearly.
- **Assumptions:** The linear regression is statistically useful, but its residual diagnostics are not fully clean. The model should be read as association-focused rather than causal.
- **Categorical binning:** The chi-square and Fisher analyses require binning continuous values into categories, which reduces detail compared with the numeric analysis.
- **External factors:** The analysis does not model infrastructure quality, urbanization, education, or policy variables, so part of the variation remains unexplained.

---

<div align="center">
  <sub>
    Made with care by Your Name · 2026
  </sub>
</div>
