# Laboratory Activity 1: Data Cleaning Pipeline
# Water Potability and Drinking Water Safety Assessment

[![Jupyter Book](https://img.shields.io/badge/Jupyter%20Book-Interactive%20Site-blue)](https://troge-dev.github.io/Water-Potability-Data-Cleaning/)
[![Dataset](https://img.shields.io/badge/Dataset-Kaggle%20Water%20Quality-green)](https://www.kaggle.com/datasets/adityakadiwal/water-potability)
[![UN SDG 6](https://img.shields.io/badge/UN%20SDG%206-Clean%20Water%20%26%20Sanitation-orange)](https://sdgs.un.org/goals/goal6)

---

## 📌 Project Overview (In Simple Words)

Clean drinking water is essential for everyone's health. In this project, we analyze water quality test data to find out whether water is **safe to drink (`Potability = 1`)** or **unsafe (`Potability = 0`)**.

However, real-world data from water sensors and lab tests often has major issues:
1. **Missing Test Results:** Lab tests are expensive, so some water samples are missing chemical measurements (especially Sulfate and pH).
2. **Broken Sensor Readings:** Faulty sensors can record impossible numbers (like negative pH readings).
3. **Extreme Mineral Spikes:** Some natural wells have huge amounts of minerals, while other spikes are just sensor glitches.

In this project, we built a **step-by-step Python cleaning pipeline** to fix these problems so the data is accurate, complete, and ready for charts and predictions.

---

## 🎯 Main Question We Are Investigating

> **"How can we fix sensor errors and fill in missing test data so we can accurately determine whether water is safe to drink?"**

### Our Main Rule
> *"Never delete or change data just because it looks different. First understand what the numbers mean in real life, then apply smart rules."*

---

## 📊 The 4 Steps of Data Preparation

| Step | Simple Meaning | What We Did in This Project |
| :--- | :--- | :--- |
| **1. Data Wrangling** | Loading and organizing the files. | Loading the raw CSV file and checking its size and types. |
| **2. Data Cleaning** | Finding and fixing errors and missing values. | Fixing impossible pH readings, filling missing values with group medians, and removing crazy sensor spikes. |
| **3. Data Transformation** | Standardizing number formats. | Rounding long decimals to 3 places and making sure labels are clean integers. |
| **4. Feature Engineering** | Creating new helpful features (optional). | Preparing the data for future machine learning models. |

---

## 🧪 Dataset Details & Simple Water Guide

* **Dataset Source:** [Water Potability Dataset on Kaggle](https://www.kaggle.com/datasets/adityakadiwal/water-potability) by Aditya Kadiwal
* **Filename:** `water_potability.csv` (Raw), `water_potability_cleaned.csv` (Processed)
* **Dataset Scope:** 3,276 water samples collected across various water bodies, evaluating 9 physicochemical metrics against WHO drinking standards.
* **Size:** 3,276 water samples × 10 columns
* **Target:** `Potability` (`1` = Safe to drink, `0` = Unsafe to drink)

### What the 9 Water Measurements Mean (Plain English)

| Column Name | What it Measures | Everyday Meaning | Safe Limit (WHO Standard) |
| :--- | :--- | :--- | :--- |
| `ph` | **Acidity / Alkalinity** | How acidic or basic water is ($0 = \text{acid}$, $7 = \text{neutral}$, $14 = \text{basic}$). | **6.5 to 8.5** is safe. |
| `Hardness` | **Mineral Content** | Dissolved calcium and magnesium from rocks. | Normal in water; high levels make soap hard to bubble. |
| `Solids` | **Dissolved Minerals & Salts** | Total amount of dissolved minerals and salts (TDS). | Up to **1,000 ppm** is good. High levels taste salty. |
| `Chloramines` | **Disinfectant / Chlorine** | Chlorine added to kill bacteria and germs. | Safe limit: **$\le$ 4.0 ppm**. |
| `Sulfate` | **Natural Rock Minerals** | Natural minerals washed from rocks into water. | Safe guideline: **$\le$ 250 mg/L**. |
| `Conductivity` | **Electricity Flow** | How well electricity moves through water (indicates dissolved salts). | Typical limit: **$\le$ 400 $\mu$S/cm**. |
| `Organic_carbon` | **Plant & Organic Matter** | Amount of decaying leaves and organic matter in water. | Lower is cleaner and safer. |
| `Trihalomethanes` | **Chlorine Byproducts** | Chemical byproducts created when chlorine mixes with organic matter. | Safe limit: **$\le$ 80 $\mu$g/L**. |
| `Turbidity` | **Cloudiness / Clarity** | How clear or cloudy the water looks. | Safe limit: **$\le$ 5.0 NTU** (should be clear). |
| `Potability` | **Drinking Safety** | Final safety label: `1` = Safe to drink, `0` = Unsafe. | Target variable. |

---

## 🔍 The 4 Big Problems We Found & How We Fixed Them

### 1. Missing Values in ~39% of the Data
* **Problem:** 1,265 out of 3,276 water samples had at least one missing chemical test (Sulfate is missing in 23.8%, pH in 15.0%, Trihalomethanes in 4.95%).
* **Why not delete them?** Deleting 39% of the data would throw away more than one-third of our water samples!
* **How we fixed it:** We filled missing numbers using the **median** of each group (Safe Water vs. Unsafe Water).

### 2. Impossible pH Readings
* **Problem:** Some sensors recorded pH values below 0 or above 14 due to broken probes.
* **How we fixed it:** We replaced impossible readings with `NaN` and filled them using the group median.

### 3. Extreme Mineral Spikes (Solids)
* **Problem:** Total Dissolved Solids had values over 50,000 ppm.
* **Why not use a standard cutoff?** Deep groundwater can naturally have 20,000 to 30,000 ppm of minerals. Standard boxplot rules would delete 47 valid mineral water samples.
* **How we fixed it:** We used an **extreme cutoff ($3.0 \times \text{IQR}$)** to keep real mineral water while removing impossible spikes (> 57,000 ppm).

### 4. Messy Decimals
* **Problem:** Measurements had uneven decimal lengths.
* **How we fixed it:** We rounded all continuous measurements to **3 decimal places** and made sure `Potability` is a clean integer (`0` or `1`).

---

## 📈 Before vs. After Cleaning Comparison

| Metric / Check | Raw Dataset (Before) | Cleaned Dataset (After) | Improvement |
| :--- | :--- | :--- | :--- |
| **Total Rows** | 3,276 | 3,248 | Kept 99.1% of all water samples |
| **Total Missing Values** | **1,434** | **0** | **100% Complete** |
| **Missing Sulfate Rows** | 781 (23.84%) | 0 (0.00%) | Filled using group median |
| **Missing pH Rows** | 491 (14.99%) | 0 (0.00%) | Filled using group median |
| **Missing Trihalomethanes** | 162 (4.95%) | 0 (0.00%) | Filled using group median |
| **Impossible pH (< 0 or > 14)** | Flagged / Bad readings | 0 (Enforced 0–14) | Fixed broken sensor errors |
| **Max Solids (ppm)** | 61,227.19 ppm | 57,403.46 ppm | Removed extreme spikes |
| **Status** | 38.6% Incomplete | **100% Clean & Ready** | Ready for EDA & modeling |

---

## 🎤 Simple Defense / Q&A Guide for Presentations

1. **Q: Where does this dataset come from?**
   * *A: The dataset is sourced from the [Kaggle Water Potability Dataset](https://www.kaggle.com/datasets/adityakadiwal/water-potability) by Aditya Kadiwal, containing 3,276 water samples evaluated against World Health Organization (WHO) safety standards.*

2. **Q: Why did you fill missing values instead of deleting rows?**
   * *A: Almost 39% of our water samples had missing test results. If we deleted those rows, we would lose over one-third of our data. Filling them lets us keep all the data.*

3. **Q: Why did you use the Median instead of the Mean?**
   * *A: The average gets pulled by extreme spikes. The median finds the true middle number and represents normal water accurately.*

4. **Q: Why did you fill missing values separately for Safe and Unsafe water?**
   * *A: Safe drinking water and unsafe water naturally have different chemical levels. Grouping by Potability ensures we fill missing values with realistic numbers for each water type.*

5. **Q: Why must pH be between 0 and 14?**
   * *A: In nature, pH only exists between 0 and 14. Anything outside that range is a broken sensor reading.*

6. **Q: Why didn't you delete all high Solids as outliers?**
   * *A: Natural groundwater can legitimately have high minerals. Using a wider boundary ($3.0 \times \text{IQR}$) keeps real mineral water and only removes crazy sensor spikes.*

---

## 🛠️ Project Structure

* `notebooks/water_potability_data_cleaning.ipynb`: The main notebook for submission containing the complete data cleaning process.
* `docs/index.md`: Book overview, problem statement, and dataset attribution.
* `docs/01_dataset_codebook.md`: Plain-English chemical codebook, dataset provenance, and WHO guidelines.
* `docs/03_defense_guide.md`: Defense questions, data origin, and answers.
* `data/raw/water_potability.csv`: The raw dataset sourced from the Kaggle repository.
* `data/processed/water_potability_cleaned.csv`: The final cleaned dataset.
* `myst.yml`: Configuration file for the interactive Jupyter Book.

---

## 📚 References & Dataset Attribution

1. **Dataset Source:** Kadiwal, Aditya. *Water Potability: Drinking Water Quality Dataset*. Available on Kaggle: [https://www.kaggle.com/datasets/adityakadiwal/water-potability](https://www.kaggle.com/datasets/adityakadiwal/water-potability).
2. **Quality Guidelines:** World Health Organization (WHO). *Guidelines for Drinking-water Quality (4th Edition)*, Geneva: WHO.
3. **Global Health Target:** United Nations Sustainable Development Goal 6 (UN SDG 6): *Ensure availability and sustainable management of water and sanitation for all*.


