# Chapter 1: Dataset Profile & Environmental Codebook

## 1. Dataset Overview

* **Dataset Title:** Water Quality & Potability Assessment
* **Source:** Kaggle (`water_potability.csv`)
* **Author / Curator:** Aditya Kadiwal
* **Dimensions:** 3,276 observations × 10 attributes
* **Classification Target:** `Potability` (Binary: `0` = Non-Potable / Unsafe, `1` = Potable / Safe)

---

## 2. Variable Codebook & WHO Reference Standards

The table below describes the physical, chemical, and microbiological metrics present in the dataset alongside their corresponding **World Health Organization (WHO)** permissible limits:

| Variable | Data Type | Units / Scale | WHO Reference Standard / Environmental Significance |
| :--- | :--- | :--- | :--- |
| `ph` | `float64` | Scale (0–14) | Acid-base balance of water. **WHO Guideline:** 6.5 – 8.5. Extremes cause corrosion and mucosal irritation. |
| `Hardness` | `float64` | mg/L ($CaCO_3$) | Capacity to precipitate soap; driven by dissolved Calcium ($Ca^{2+}$) and Magnesium ($Mg^{2+}$). |
| `Solids` | `float64` | ppm (mg/L) | Total Dissolved Solids (TDS); aggregate mineral and salt content. High TDS impairs palatability. |
| `Chloramines` | `float64` | ppm | Secondary disinfectant formed from chlorine-ammonia reaction. **WHO Safe Limit:** $\le$ 4.0 ppm. |
| `Sulfate` | `float64` | mg/L | Naturally occurring minerals from geological rock deposits. **WHO Guideline:** $\le$ 250 mg/L. |
| `Conductivity` | `float64` | $\mu\text{S/cm}$ | Electrical conductance; proxy for dissolved ionic mineral concentration. Typical limit: $\le 400\,\mu\text{S/cm}$. |
| `Organic_carbon` | `float64` | ppm | Total Organic Carbon (TOC); indicator of decaying organic matter and precursor to toxic byproducts. |
| `Trihalomethanes` | `float64` | $\mu\text{g/L}$ | Chlorination byproducts (THMs); regulated carcinogens. **WHO Safe Limit:** $\le$ 80 $\mu\text{g/L}$. |
| `Turbidity` | `float64` | NTU | Optical clarity and suspended colloidal particulates. **WHO Safe Limit:** $\le$ 5.0 NTU. |
| `Potability` | `int64` | Binary (0 / 1) | Target indicator: `1` = Safe for human consumption, `0` = Unsafe / Contaminated. |

---

## 3. Identified Data Quality Defects

An exhaustive pre-cleaning audit of the raw dataset identified four core anomalies requiring systematic treatment:

```{admonition} Summary of Identified Anomalies
:class: warning
1. **Pervasive Chemical Test Missingness:**
   * `Sulfate`: 781 missing values (~23.84%)
   * `ph`: 491 missing values (~14.99%)
   * `Trihalomethanes`: 162 missing values (~4.95%)
   * **Cumulative Impact:** 1,265 rows (38.61% of dataset) possess at least one missing parameter.
2. **Physicochemical Boundary Violations:**
   * Out-of-bounds telemetry readings on the logarithmic pH scale ($\text{pH} < 0$ or $\text{pH} > 14$).
3. **Severe Total Dissolved Solids Skewness:**
   * Natural groundwater mineralization exhibits a heavy right tail ($> 50,000\,\text{ppm}$), requiring extreme outlier boundaries rather than standard Tukey fences.
4. **Precision and Type Standardization:**
   * Irregular floating-point rounding requiring standardization to 3 decimal places and clean integer target casting.
```
