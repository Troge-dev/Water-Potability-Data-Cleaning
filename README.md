# Water Potability Data Cleaning Pipeline & Quality Assurance
### DS311 - Exploratory Data Analysis (EDA) | Laboratory Activity 1

[![Jupyter Book](https://img.shields.io/badge/Jupyter%20Book-Live%20Documentation-blue)](https://troge-dev.github.io/Water-Potability-Data-Cleaning)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-brightgreen)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![WHO Standards](https://img.shields.io/badge/Standards-WHO%20Guidelines-teal)](https://www.who.int/publications/i/item/9789241549950)
[![Dataset: Kaggle](https://img.shields.io/badge/Dataset-Kaggle%20Water%20Potability-blue)](https://www.kaggle.com/datasets/adityakadiwal/water-potability)

An end-to-end, domain-informed data cleaning, exploratory analysis, and diagnostic quality assurance pipeline for drinking water safety assessment, benchmarked against World Health Organization (WHO) standards.

---

## I. Project Overview & Scope

Clean drinking water is fundamental to human life and disease prevention (UN Sustainable Development Goal 6). Municipal utilities and environmental agencies measure chemical and physical indicators — including **pH**, **chlorine residuals**, **dissolved minerals**, and **clarity** — to determine whether water is potable.

This project evaluates the [Kaggle Water Potability Dataset](https://www.kaggle.com/datasets/adityakadiwal/water-potability) by Aditya Kadiwal (3,276 water samples across 9 physicochemical features + 1 potability classification target).

### Key Data Quality Challenges Identified:
* **Severe Missingness:** 1,265 samples (38.61% of dataset) had missing values across `Sulfate` (23.84%), `ph` (14.99%), and `Trihalomethanes` (4.95%).
* **Sensor Anomalies:** Uncalibrated sensor voltages produced impossible pH readings outside the physical range of $[0, 14]$.
* **Extreme Mineral Concentrations:** Heavy mineral groundwater exhibited Total Dissolved Solids (TDS) up to 61,227 ppm.

### Pipeline Remediation & Results:
* **100% Sample Preservation:** Applied class-conditional median imputation and extreme IQR fences ($3.0\times\text{IQR}$), retaining all 3,276 water samples (0 samples lost).
* **Zero Missing Values:** Resolved all 1,434 missing entries while preserving class-specific chemical baselines.
* **Standardized Clean Dataset:** Standardized continuous features to 3 decimal places and exported to `data/processed/water_potability_cleaned.csv`.

---

## II. Jupyter Book Structure & Navigation

The Jupyter Book documentation is structured into **3 core pages**:

| Page | File Path | Focus & Content |
| :--- | :--- | :--- |
| **I. Landing Page & Codebook** | `docs/index.md` | Executive overview, project background, 9-feature physicochemical codebook, WHO drinking limits, and 4 preparation stages. |
| **II. Interactive Pipeline** | `notebooks/presentation.ipynb` | Full executable Python pipeline, missingness matrix, MCAR/MAR diagnostics, benchmark comparison tables, and before-vs-after audit dashboards. |
| **III. Defense & Q&A Guide** | `docs/03_defense_guide.md` | 13 oral defense questions with two-tier answers (Spoken Summary & Technical Rationale) and presentation cheat sheet. |

---

## III. Dataset Codebook & Physicochemical Reference

| Column Name | Metric / Unit | WHO Safe Benchmark | Everyday Description |
| :--- | :--- | :--- | :--- |
| `ph` | pH ($0\text{ to }14$) | **6.5 to 8.5** | Acidity / alkalinity measure. Values $<6.5$ corrode pipes; $>8.5$ cause mineral scaling. |
| `Hardness` | mg/L | *No strict limit* ($<200$) | Dissolved calcium and magnesium from mineral deposits. |
| `Solids` | ppm | **$< 500\text{ to }1,000$** | Total Dissolved Solids (TDS); natural mineral aquifers can reach extreme levels. |
| `Chloramines` | ppm | **Up to 4.0 ppm** | Chlorine-ammonia disinfectant added to kill pathogens. |
| `Sulfate` | mg/L | **$< 250\text{ mg/L}$** | Natural dissolved rock minerals. High levels cause a bitter taste and laxative effects. |
| `Conductivity` | $\mu$S/cm | **$< 400\ \mu\text{S/cm}$** | Electrical conductivity indicating dissolved ionic mineral content. |
| `Organic_carbon` | ppm | **$< 2.0\text{ to }4.0$** | Total Organic Carbon from decaying vegetation. |
| `Trihalomethanes` | $\mu$g/L | **$< 80\ \mu\text{g/L}$** | Chemical byproducts formed when chlorine reacts with organic matter. |
| `Turbidity` | NTU | **$< 5.0\text{ NTU}$** | Cloudiness caused by suspended sediments. Clean water is crystal clear. |
| `Potability` | Binary | `1` = Safe, `0` = Unsafe | Classification target. |

---

## IV. Summary Quality Audit Matrix

| Metric | Raw Dataset (Before) | Pipeline Action | Cleaned Dataset (After) | Status |
| :--- | :--- | :--- | :--- | :--- |
| **Sample Count** | 3,276 samples | Domain-informed filtering | **3,276 samples (100.0%)** | Preserved |
| **Missing Values** | 1,434 missing entries | Class-conditional median imputation | **0 missing entries (0.0%)** | Resolved |
| **pH Range** | Sensor errors outside $[0, 14]$ | Bounded $[0, 14]$ & imputed | Strictly within **$[0.00, 14.00]$** | Validated |
| **Mineral Outliers (Solids)** | 47 flagged by $1.5\times\text{IQR}$ | Extreme fence ($3.0\times\text{IQR} = 62,331\text{ ppm}$) | **0 authentic samples deleted** | Preserved |
| **Float Precision** | Inconsistent decimal places | Precision standardization | **Standardized 3 decimals** | Cleaned |

---

## V. Quickstart & Installation

```bash
# 1. Clone the repository
git clone https://github.com/Troge-dev/Water-Potability-Data-Cleaning.git
cd Water-Potability-Data-Cleaning

# 2. Install dependencies
pip install -r requirements.txt

# 3. Build and view the Jupyter Book locally
jupyter-book build --html
```

---

## VI. References & Attribution

1. **Dataset Source:** Kadiwal, Aditya. *Water Potability: Drinking Water Quality Dataset*. Available on Kaggle: [https://www.kaggle.com/datasets/adityakadiwal/water-potability](https://www.kaggle.com/datasets/adityakadiwal/water-potability).
2. **Missing Data in Environmental Monitoring:** Liu, X., Zhang, X., & Wang, X. (2022). Handling missing data in near real-time environmental monitoring: A system and a review of selected methods. *Future Generation Computer Systems*, 128, 63–72. [https://doi.org/10.1016/j.future.2021.09.033](https://doi.org/10.1016/j.future.2021.09.033)
3. **Global SDG Target:** United Nations. (n.d.). *Water and sanitation*. United Nations Sustainable Development Goals. [https://www.un.org/sustainabledevelopment/water-and-sanitation/](https://www.un.org/sustainabledevelopment/water-and-sanitation/)
4. **Water Quality Guidelines:** World Health Organization. (2017). *Guidelines for drinking-water quality: Fourth edition incorporating the first addendum*. Geneva: World Health Organization. [https://www.who.int/publications/i/item/9789241549950](https://www.who.int/publications/i/item/9789241549950)
