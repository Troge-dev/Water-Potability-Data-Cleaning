# Chapter 3: Laboratory Defense & Evaluation Guide

This chapter provides comprehensive technical defenses and domain justifications for each data cleaning decision made in this project. Use these structured points during oral presentations, committee reviews, and lab evaluations.

---

## Question 1: Why did you choose imputation over dropping incomplete rows (`dropna()`)?

```{admonition} Methodological Defense
:class: tip
**Core Justification:** Data Preservation & Sample Representativeness.
```

* **Quantitative Impact:** Sulfate is missing in **23.84%** of records, pH in **14.99%**, and Trihalomethanes in **4.95%**. In total, **1,265 out of 3,276 observations (38.61%)** contain at least one missing chemical test.
* **Risk of Deletion:** Dropping nearly 40% of observations introduces severe **survivorship and reporting bias**, drastically reduces sample power, and distorts the underlying distribution of the target class (`Potability`).
* **Conclusion:** Preserving the complete sample size of 3,276 rows ensures downstream statistical models retain maximum generalizability.

---

## Question 2: Why did you use median imputation instead of the mean?

```{admonition} Methodological Defense
:class: tip
**Core Justification:** Robustness to Heavy-Tailed & Skewed Distributions.
```

* **Vulnerability of the Mean:** The arithmetic mean is sensitive to extreme values, sensor calibration spikes, and distribution asymmetry.
* **Robustness of the Median:** The median represents the 50th percentile (central tendency) and is mathematically immune to outliers ($L_1$ norm minimizer). For geochemical and environmental sensor data with inherent variance, the median yields a more realistic central surrogate.

---

## Question 3: Why was imputation conditioned on the target variable (`Potability`)?

```{admonition} Methodological Defense
:class: tip
**Core Justification:** Preserving Distinct Physicochemical Class Profiles.
```

* **Domain Rationale:** Safe drinking water (`Potability = 1`) and non-potable water (`Potability = 0`) naturally occupy distinct chemical regimes (e.g., controlled chloramine disinfection and permissible sulfate levels).
* **Mitigating Signal Flattening:** Performing unconditional imputation across the entire dataset blurs the separation between safe and contaminated clusters. Group-wise imputation (`df.groupby('Potability')`) preserves class-conditional variance.

---

## Question 4: Why are values outside $0 \le \text{pH} \le 14$ converted to `NaN`?

```{admonition} Methodological Defense
:class: tip
**Core Justification:** Physicochemical Impossibility & Sensor Telemetry Artifacts.
```

* **Scientific Basis:** The pH scale is defined as $-\log_{10}[H^+]$. In standard environmental aqueous systems, pH values outside $0$ to $14$ cannot occur naturally and indicate uncalibrated sensor probes or corrupted telemetry packets.
* **Treatment:** Rather than leaving erroneous negative or super-alkaline readings in the dataset, they are converted to `np.nan` and imputed via group medians.

---

## Question 5: Why apply an extreme $3.0 \times \text{IQR}$ cutoff for Total Dissolved Solids rather than the standard $1.5 \times \text{IQR}$ rule?

```{admonition} Methodological Defense
:class: tip
**Core Justification:** Distinguishing Natural Geochemical Variation from Corrupt Artifacts.
```

* **Environmental Context:** Total Dissolved Solids (`Solids`) measure inorganic salts and dissolved minerals. While municipal tap water typically ranges between $100 - 1,000\,\text{ppm}$, natural deep mineral aquifers and brackish groundwater legitimately reach $20,000 - 35,000\,\text{ppm}$.
* **Standard Tukey Fence ($1.5 \times \text{IQR}$):** A standard cutoff ($42,000\,\text{ppm}$) would erroneously delete **47 valid, high-mineral water samples**.
* **Extreme Fence ($3.0 \times \text{IQR}$):** An extreme threshold ($57,000\,\text{ppm}$) preserves legitimate mineral-rich groundwater observations while safely removing impossible telemetry spikes ($> 60,000\,\text{ppm}$).

---

## Question 6: How does this cleaning pipeline prepare the dataset for downstream EDA and Machine Learning?

1. **Zero Null Leakage:** All null values are systematically resolved, eliminating runtime exceptions in standard algorithms (e.g., Scikit-Learn pipelines).
2. **Standardized Numerical Precision:** Floating-point features are formatted to 3 decimal places, preventing floating-point precision artifacts.
3. **Integer Target Consistency:** `Potability` is cast to standard integer format (`int64`), ready for binary classification metrics (ROC-AUC, Precision-Recall, F1-Score).
4. **Reproducibility:** The entire process is codified in a standalone script (`scripts/clean_water_potability.py`) and verified with assertion checks.
