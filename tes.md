<div align="center">

# Digital Divide in Indonesia: Poverty and Internet Access

### Quantifying the statistical association between provincial poverty rates and household internet access across 37 Indonesian provinces using Chi-Square testing, OLS regression, and Pearson correlation on 2024 BPS government data.

<br>

[![Status](https://img.shields.io/badge/status-completed-blue?style=flat-square)]()
[![Python](https://img.shields.io/badge/python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/jupyter-notebook-F37626?style=flat-square&logo=jupyter&logoColor=white)](notebooks/)
[![Open in Colab](https://img.shields.io/badge/Open%20in-Colab-F9AB00?style=flat-square&logo=googlecolab&logoColor=white)](https://colab.research.google.com/github/[username]/digital-divide-indonesia-2024/blob/main/notebooks/poverty_internet_access_indonesia_bps2024.ipynb)
[![Last Commit](https://img.shields.io/github/last-commit/[username]/digital-divide-indonesia-2024?style=flat-square)](https://github.com/[username]/digital-divide-indonesia-2024/commits)

</div>

---

## 📌 Overview

This project presents a multi-method statistical analysis of Indonesia's digital divide, examining whether provincial poverty rates are significantly associated with household internet access rates and how strong that relationship is. Using 2024 data from Badan Pusat Statistik (BPS), the analysis covers 37 of Indonesia's 38 provinces and applies a structured six-stage workflow: exploratory data analysis, Pearson correlation, OLS linear regression with full assumption diagnostics, Chi-Square test of independence, Fisher's Exact Test, and Cramer's V effect size estimation. The analysis is intended for data scientists, researchers, and policy analysts who want empirical, quantified evidence on the socioeconomic determinants of internet access disparity in Indonesia. Output includes nine publication-quality figures and a complete statistical summary embedded in the notebook.

---

## ❓ Problem Statement

**Context:** Indonesia's internet penetration rate varies dramatically across provinces in 2024, ranging from 97.57% (Kepulauan Riau) to just 12.15% (Papua Pegunungan) — a gap of over 85 percentage points. Poverty rates show a comparable spread, from 4.00% (Bali) to 32.97% (Papua Pegunungan). These patterns suggest a potential structural link between economic deprivation and digital exclusion, but the statistical nature and quantified strength of this relationship had not been formally examined using current data and a rigorous multi-method approach.

**Gap:** BPS publishes both datasets independently at the provincial level, but limited analytical work integrates them using methods that cover both parametric (Pearson r, OLS regression with assumption diagnostics) and non-parametric (Chi-Square, Fisher's Exact Test) approaches alongside effect size estimation. Without this, the "digital divide" narrative in Indonesia remains descriptive rather than statistically grounded.

**Solution:** This analysis merges both 2024 BPS datasets at the provincial level and applies a rigorous statistical workflow to quantify the direction, magnitude, and significance of the poverty-internet relationship. The results provide an evidence base for digital equity discussions, infrastructure policy prioritization, and poverty alleviation program design in Indonesia.

---

## 🎥 Demo & Screenshots

> 📓 **Notebook:** &nbsp;[Open in Colab](https://colab.research.google.com/github/[username]/digital-divide-indonesia-2024/blob/main/notebooks/poverty_internet_access_indonesia_bps2024.ipynb) &nbsp;|&nbsp; [Render on nbviewer](https://nbviewer.org/github/[username]/digital-divide-indonesia-2024/blob/main/notebooks/poverty_internet_access_indonesia_bps2024.ipynb)

<br>

| Univariate Distribution | Bivariate Scatter Plot |
|:---:|:---:|
| ![Univariate Distribution](docs/img/01_univariate_distribution.png) | ![Bivariate Scatter](docs/img/02_bivariate_scatter.png) |
| *Distribution and spread of internet access (mean: 85.95%) and poverty rate (mean: 11.33%) across 37 provinces, with mean markers and IQR-based outlier detection.* | *Poverty rate vs. internet access (r = −0.82): a strong negative trend with Papua provinces as structural outliers at the lower-right extreme.* |

| OLS Regression Analysis | Chi-Square Panel |
|:---:|:---:|
| ![Regression Line] <img width="1139" height="490" alt="image" src="https://github.com/user-attachments/assets/219b1f47-d796-46bc-b4d4-204ff2246dd8" />
 | ![Chi-Square Panels](docs/img/04_chisquare_panels.png) |
| *OLS regression line (R² = 0.6748, p < 0.001) with annotated equation. Intercept exceeds 100% — a documented extrapolation artifact outside the observed data range (4.00%–32.97%).* | *Four-panel Chi-Square visualization: observed frequencies, expected frequencies, standardized residuals, and grouped bar chart. Cell [High Poverty × Low Internet] contributes 42.5% of total χ².* |

> 📂 All generated figures are stored in `outputs/figures/`. Export each figure from the notebook using `plt.savefig()` before committing.

---

## 🛠️ Tech Stack

| Layer | Technology | Role in Project |
|:---:|:---:|---|
| Language | Python 3.10+ | Primary language for the entire analysis pipeline |
| Environment | Google Colab / Jupyter Notebook | Interactive execution, EDA, and inline reporting |
| Data Processing | Pandas, NumPy | Data loading, column renaming, inner merge on province name, missing value handling, IQR outlier detection |
| Visualization | Matplotlib, Seaborn | Nine output figures: histograms, boxplots, scatter plots, heatmaps, regression plot, diagnostic panels, GoF charts |
| Statistical Analysis | SciPy (stats) | Pearson correlation, Chi-Square, Fisher's Exact Test, Shapiro-Wilk, Breusch-Pagan, Durbin-Watson |
| Regression Modeling | Scikit-learn | OLS linear regression, R² scoring, residual extraction |
| Version Control | Git + GitHub | Source control and documentation |

---

## 📊 Dataset

### Metadata

**Dataset 1 — Internet Access**

| Attribute | Detail |
|---|---|
| **Source** | Badan Pusat Statistik (BPS) Indonesia |
| **Link** | [Persentase Rumah Tangga yang Pernah Mengakses Internet, 2024](https://www.bps.go.id/id/statistics-table/2/Mzk4IzI=/persentase-rumah-tangga-yang-pernah-mengakses-internet-dalam-3-bulan-terakhir-menurut-provinsi-dan-klasifikasi-daerah.html) |
| **Size** | 39 rows × 4 columns (raw); 37 provinces × 4 columns (after cleaning) |
| **Format** | CSV |
| **License** | Public government data (BPS) |
| **Time Coverage** | 2024 |

**Dataset 2 — Poverty Rate**

| Attribute | Detail |
|---|---|
| **Source** | Badan Pusat Statistik (BPS) Indonesia |
| **Link** | [Persentase Penduduk Miskin (P0) Menurut Provinsi dan Daerah, 2024](https://www.bps.go.id/id/statistics-table/2/MTkyIzI=/persentase-penduduk-miskin--p0--menurut-provinsi-dan-daerah.html) |
| **Size** | 39 rows × 10 columns (raw); 37 provinces × 2 columns (after cleaning) |
| **Format** | CSV |
| **License** | Public government data (BPS) |
| **Time Coverage** | March 2024 (Semester 1) |

> Raw data files are not included in this repository. Download both CSVs directly from the BPS links above, place them in the `data/` folder, and follow the instructions in [`data/README.md`](data/README.md) before running the notebook.

### Data Dictionary (Final Merged Dataset — 37 Provinces × 5 Columns)

| Column | Data Type | Description | Example Values |
|---|:---:|---|---|
| `Provinsi` | `str` | Province name (uppercase, 37 provinces after removing DKI Jakarta) | `"ACEH"`, `"BALI"` |
| `Internet_Perkotaan` | `float64` | Urban household internet access rate (%) | `92.60`, `98.68` |
| `Internet_Perdesaan` | `float64` | Rural household internet access rate (%) | `86.97`, `8.81` |
| `Internet_Total` | `float64` | **Dependent variable (Y)** — overall internet access rate per province (%) | `88.95`, `12.15` |
| `Kemiskinan_Persen` | `float64` | **Independent variable (X)** — poverty rate per province, March 2024 (%) | `14.23`, `4.00` |

---

## 📈 Results & Performance

### Key Findings

1. **Very strong negative correlation (r = −0.8215, p < 0.001)** — Provinces with higher poverty rates consistently show lower internet access rates. The association is statistically significant at all conventional significance levels (n = 37, two-tailed).

2. **OLS regression explains 67.48% of variance** — The simple linear model (Ŷ = 108.16 − 1.96X) yields R² = 0.6748 (adj. R² = 0.6655, F = 72.62, p < 0.001). Each 1-percentage-point increase in poverty rate is associated with a 1.96% decrease in internet access (β₁ = −1.9603, SE = 0.2300, 95% CI: [−2.43, −1.49]).

3. **Chi-Square independence test confirmed by Fisher's Exact Test** — The 3×3 Chi-Square test (χ² = 20.18, df = 4, p = 0.000460) was supplemented by Fisher's Exact Test (p = 0.036) as the appropriate fallback, since 77.8% of expected frequency cells fell below 5. Both tests reject H₀ at α = 0.05.

4. **Large effect size: Cramer's V = 0.5222** — Classified as "Very Strong" for a 3×3 contingency table (df = 2), fully consistent with the Pearson correlation result. Both categorical and continuous approaches converge on the same conclusion.

5. **No high-poverty province has high internet access** — The cell [High Poverty × High Internet Access] = 0 observed vs. 2.7 expected. This zero-cell finding indicates an absolute structural barrier: no province in the highest poverty tier achieves high internet access in the 2024 data.

6. **The [High Poverty × Low Internet Access] cell drives 42.5% of total χ²** — Seven of 10 high-poverty provinces fall in the low internet access category (expected under independence: 2.4 provinces), with a standardized residual of 2.929. This single cell is the primary statistical engine behind the significant Chi-Square result.

| OLS Assumption Diagnostics | Crosstab Standardized Residuals |
|:---:|:---:|
| ![Diagnostic Plots](docs/img/05_diagnostic_plots.png) | *[Screenshot: Standardized residuals heatmap — place `outputs/figures/04_crosstab_heatmap.png` here after exporting from notebook]* |
| *Four-panel OLS diagnostics. Fan-shaped pattern in Residuals vs Fitted confirms heteroscedasticity. Q-Q plot shows near-normal residuals with tail deviation driven by Papua outliers.* | *3×3 heatmap with standardized residuals. Cell [Tinggi × Rendah] (res = 2.93) and cell [Tinggi × Tinggi] (res = −1.64) show the strongest deviations from independence.* |

> 📂 All output figures are stored in `outputs/figures/`.

---

## ⚠️ Notes / Limitations

- **Scope:** Cross-sectional analysis at the provincial level using a single year of data (2024). No causal claims can be made from this design. The findings describe association strength and direction only.

- **Data:** DKI Jakarta was excluded due to a missing `Internet_Perdesaan` value (97.37% of data retained). The three Papua provinces — Papua Pegunungan (Internet: 12.15%, Poverty: 32.97%), Papua Tengah (36.08%, 29.76%), and Papua Selatan (65.71%, 17.44%) — are structural outliers that substantially influence correlation strength, residual variance, and effect size estimates. Their inclusion reflects real-world conditions, but a robustness check excluding these provinces is recommended.

- **Statistical Assumptions:** Two of three OLS classical assumptions are violated: homoscedasticity (Breusch-Pagan p < 0.001) and no autocorrelation (Durbin-Watson = 1.04, indicating positive autocorrelation likely caused by geographic clustering of Papua provinces). Normality of residuals is satisfied (Shapiro-Wilk p = 0.092). Robust standard errors or Weighted Least Squares were not applied in this version; coefficient confidence intervals should be interpreted with caution.

- **Generalizability:** Findings reflect 2024 provincial-level averages and may not generalize to sub-provincial or district-level patterns, or to years outside the study period. Multi-year panel data would be needed to assess the temporal stability of this relationship.

- **Reproducibility:** The notebook uses Google Colab's `files.upload()` mechanism for data loading, which requires manual file upload at runtime. To run locally, replace the upload block with `pd.read_csv('data/[filename].csv', skiprows=n)` after downloading both BPS datasets and placing them in `data/`. Full instructions are in [`data/README.md`](data/README.md).

- **Missing Variable Bias:** The model uses a single predictor. Known confounders — telecommunications infrastructure investment, geographic terrain, education levels, local government digital policy — are acknowledged but not controlled for. The remaining 32.52% unexplained variance (1 − R²) is attributed to these omitted factors.

---

<div align="center">
  <sub>
    ⭐ If this analysis was useful, consider giving the repository a star.
    <br>
    Made with ❤️ by <a href="https://github.com/[username]">[Your Name]</a> · 2024
  </sub>
</div>
