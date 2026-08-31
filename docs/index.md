# Laboratory Activity 1: Data Cleaning Pipeline
## Water Potability and Chemical Safety Assessment

```{admonition} Course & Project Information
:class: tip
**Course:** DS311 - Exploratory Data Analysis  
**Domain:** Environment & Public Health (Aligned with UN SDG 6: Clean Water and Sanitation)  
**Primary Dataset:** `data/raw/water_potability.csv` (3,276 water samples × 10 features)  
**Target Variable:** `Potability` (0 = Non-Potable / Unsafe, 1 = Potable / Safe)
```

---

## 1. Project Overview

Clean drinking water is an indispensable prerequisite for human health, sanitation, and environmental sustainability. In environmental quality monitoring, laboratory and field sensors record continuous physical and chemical parameters—including **pH balance**, **mineral hardness**, **chloramine disinfection agents**, and **dissolved solids**—to assess whether a water source is safe for human consumption (`Potability = 1`) or poses chemical hazard (`Potability = 0`).

However, real-world environmental datasets are prone to significant data quality defects:
1. **Missing Chemical Assays:** Costly laboratory analyses (such as Sulfate and Trihalomethanes) are frequently omitted or incomplete across testing batches.
2. **Sensor Calibration Artifacts:** Faulty telemetry probes can produce physically impossible measurements (e.g., pH values outside the fundamental $[0, 14]$ scale).
3. **Extreme Mineral Concentration Variations:** Natural geochemical mineral variations vs. corrupt telemetry spikes must be carefully distinguished.

This interactive Jupyter Book presents a **principled, domain-informed data cleaning pipeline** in Python and Pandas to audit, sanitize, impute, and validate water safety records in accordance with **World Health Organization (WHO)** standards.

---

## 2. Data Preparation Framework

In data science workflows, data preparation is a structured, multi-stage discipline:

| Stage | Objective | Implementation in this Lab |
| :--- | :--- | :--- |
| **Data Wrangling** | Ingesting, restructuring, and managing raw input streams into tabular structures. | End-to-end data ingestion, type standardization, and reproducible pipeline design. |
| **Data Cleaning** | Identifying and resolving anomalies, missing values, duplicates, and boundary violations. | Sanitizing out-of-scale pH readings, class-conditional median imputation, and extreme IQR outlier pruning. |
| **Data Transformation** | Modifying numeric representation and precision without altering underlying semantics. | Standardizing floating-point precision to 3 decimal places and integer target casting. |
| **Feature Engineering** | Deriving domain-specific indicators to enrich predictive capability. | Preserving natural chemical interaction ratios for downstream classification models. |

```{admonition} Core Guiding Principle
:class: important
*"We do not modify or discard data simply because it appears atypical. We first audit the data, understand the underlying physicochemical phenomenon, and apply justified domain rules."*
```

---

## 3. Research Questions & Problem Statement

### The Real-World Environmental Problem
Access to safe drinking water is threatened by industrial runoff, inadequate sanitation, and chemical contamination. Public health authorities require trustworthy data to classify water potability, but missing assays and sensor probe errors introduce unacceptable misclassification risks.

### Primary Investigation Question
> *How can we systematically detect, audit, and clean sensor probe anomalies, missing chemical tests, and mineral concentration outliers to ensure that water safety classification strictly adheres to World Health Organization (WHO) safety standards?*

### Plain-Language Summary
> *How can we fix sensor errors and fill in missing test data so we can accurately determine whether water is safe to drink?*

---

## 4. Book Structure & Navigation

This Jupyter Book is organized into the following chapters:

1. **[Dataset Profile & Codebook](01_dataset_codebook.md):** Detailed variable definitions, units of measurement, and WHO reference standards.
2. **[Data Cleaning Pipeline](../notebooks/water_potability_data_cleaning.ipynb):** Interactive computational notebook executing the end-to-end ingestion, missingness visualization (`missingno`), pH boundary enforcement, class-conditional imputation, and verification.
3. **[Presentation & Defense Guide](03_defense_guide.md):** Structured Q&A addressing methodological choices for oral lab defense and evaluation.
