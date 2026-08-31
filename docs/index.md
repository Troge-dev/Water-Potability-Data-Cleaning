# Water Potability Data Cleaning Project
## Simple & Clear Data Cleaning Guide for Drinking Water Safety

```{admonition} Quick Project Info
:class: tip
* **Course:** DS311 - Exploratory Data Analysis (EDA)
* **Goal:** Clean a dataset of water test results so we can accurately check if water is safe to drink.
* **Topic:** Environment & Public Health (Clean Water for Everyone - UN SDG 6)
* **Dataset Source:** [Water Potability Dataset on Kaggle](https://www.kaggle.com/datasets/adityakadiwal/water-potability) by Aditya Kadiwal
* **Dataset Size:** 3,276 water samples tested for 9 water quality measurements.
* **Target:** `Potability` (1 = Safe to drink, 0 = Unsafe to drink)
```

---

## 1. What is this Project About?

Clean drinking water is necessary for everyone. When health and water agencies test water, they measure things like **acidity (pH)**, **chlorine levels**, **mineral hardness**, and **cloudiness**.

In this project, we analyze the [Kaggle Water Potability Dataset](https://www.kaggle.com/datasets/adityakadiwal/water-potability) created by Aditya Kadiwal, which contains real-world physicochemical metrics from 3,276 water bodies benchmarked against World Health Organization (WHO) safety standards.

However, real-world data from water sensors and lab tests is rarely perfect. It often has big problems:
1. **Missing Numbers:** Some water samples were never tested for certain chemicals because lab tests are expensive.
2. **Broken Sensors:** Water probes can break or get dirty, giving impossible readings (like a pH below 0 or above 14).
3. **Extreme Numbers:** Some natural underground wells have huge amounts of minerals, while other spikes are just sensor glitches.

In this project, we built a step-by-step **Python cleaning pipeline** to fix these errors so the data is 100% clean, accurate, and ready for charts and analysis.

---

## 2. The 4 Stages of Data Preparation

Preparing data involves four easy-to-understand steps:

| Stage | What it Means (Simple) | What We Did in This Project |
| :--- | :--- | :--- |
| **Data Wrangling** | Loading and organizing the data files. | Loading the raw CSV file (`water_potability.csv`) and setting up our tools. |
| **Data Cleaning** | Finding and fixing errors, missing numbers, and bad readings. | Fixing impossible pH numbers, filling missing values, and checking extreme spikes. |
| **Data Transformation** | Cleaning up number formats without changing the facts. | Rounding long decimals to 3 places and making sure labels are clean. |
| **Feature Engineering** | Creating new helpful columns (optional). | Preparing the cleaned data for future charts and machine learning models. |

```{admonition} Our Main Rule
:class: important
*"Never delete or change data just because it looks different. First understand what the numbers mean in real life, then apply smart rules."*
```

---

## 3. The Main Problem We Are Solving

### The Real-World Question:
> *How can we fix sensor errors and fill in missing chemical tests so we can accurately tell whether water is safe to drink?*

### Why We Can't Just Delete Incomplete Data:
* **Almost 39% of the water samples** (1,265 rows out of 3,276) have at least one missing chemical test.
* If we delete those rows, we lose more than one-third of our data!
* Instead of throwing away data, we use smart **median filling** based on whether the water is safe or unsafe.

---

## 4. Book Chapters & Navigation

Use the left sidebar or links below to explore the project:

1. **[Dataset Profile & Simple Codebook](01_dataset_codebook.md):** What each of the 9 water measurements means in plain English and the World Health Organization (WHO) safe limits.
2. **[Data Cleaning Presentation Notebook](../notebooks/presentation.ipynb):** The comprehensive Python presentation notebook showing every cleaning step, diagnostic charts, before-vs-after audit, and oral defense guides.
3. **[Presentation & Defense Guide](03_defense_guide.md):** Simple, easy-to-remember answers to common questions for your presentation.


---

## 📚 References & Attribution

* **Primary Dataset:** Kadiwal, Aditya. *Water Potability Dataset*. Hosted on Kaggle: [https://www.kaggle.com/datasets/adityakadiwal/water-potability](https://www.kaggle.com/datasets/adityakadiwal/water-potability).
* **International Standards:** World Health Organization (WHO). *Guidelines for Drinking-water Quality (4th Edition)*.

