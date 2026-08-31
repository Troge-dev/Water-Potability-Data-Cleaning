# Chapter 1: Dataset Profile & Simple Water Codebook

## 1. What is this Dataset?

* **Dataset Name:** Water Potability (Drinking Water Safety)
* **Dataset Source:** [Water Potability Dataset on Kaggle](https://www.kaggle.com/datasets/adityakadiwal/water-potability)
* **Creator / Publisher:** Aditya Kadiwal
* **Raw Filename:** `water_potability.csv` (Located in `data/raw/`)
* **Cleaned Filename:** `water_potability_cleaned.csv` (Located in `data/processed/`)
* **What it contains:** 3,276 water samples collected from different water bodies (wells, lakes, taps, and treatment facilities).
* **What each row represents:** One water sample tested for 9 different water quality measurements evaluated against World Health Organization (WHO) water quality criteria.
* **The Main Goal / Target:** `Potability`
  * `1` = **Safe to drink** (Potable)
  * `0` = **Unsafe to drink** (Non-potable / Contaminated)

---

## 2. What do the 9 Water Measurements Mean? (In Plain English)

Here is what each column measures, explained simply without confusing chemistry terms:

| Column Name | What it Measures | Everyday Explanation | Safe Limits (WHO Guidelines) |
| :--- | :--- | :--- | :--- |
| `ph` | **Acidity / Alkalinity** | Measures how acidic or basic the water is (0 = acid like vinegar, 7 = neutral pure water, 14 = basic like bleach). | **6.5 to 8.5** is safe. Water outside this tastes bad or damages pipes. |
| `Hardness` | **Mineral Content** | Measures dissolved calcium and magnesium. Hard water makes it hard for soap to bubble. | Normal in water, but high levels leave chalky white stains on glasses. |
| `Solids` | **Dissolved Minerals & Salts** | Total amount of minerals and salts dissolved in the water (Total Dissolved Solids). | Up to **1,000 ppm** is good. High amounts give water an earthy or salty taste. |
| `Chloramines` | **Disinfectant / Chlorine** | Chlorine added by water treatment plants to kill bacteria and germs. | **Up to 4.0 ppm** is safe to kill germs without harming humans. |
| `Sulfate` | **Natural Rock Minerals** | Natural minerals washed from rocks and soil into water. | **Up to 250 mg/L** is safe. Too much can have a laxative effect. |
| `Conductivity` | **Electricity Flow** | How well electric current passes through the water. More dissolved minerals = higher electricity flow. | **Up to 400 $\mu$S/cm** is typical for clean water. |
| `Organic_carbon` | **Plant & Organic Matter** | Amount of broken-down plant and organic material in the water. | Low levels are safe; high levels mean dirty water from leaves or runoff. |
| `Trihalomethanes` | **Chlorine Byproducts** | Chemical byproducts created when chlorine mixes with organic matter in water. | **Up to 80 $\mu$g/L** is safe. High levels over many years are unhealthy. |
| `Turbidity` | **Cloudiness / Clarity** | How clear or cloudy the water looks to the naked eye. | **Up to 5.0 NTU** is safe. Clean drinking water should be crystal clear. |
| `Potability` | **Drinking Safety** | Final safety label: `1` means safe to drink, `0` means unsafe. | Target variable to analyze and predict. |

---

## 3. The 4 Main Problems We Found in the Raw Data

Before we can use this data, we found 4 major issues that needed fixing:

1. **Lots of Missing Test Results:**
   * Many water samples were never tested for `Sulfate` (23.8% missing), `ph` (15.0% missing), and `Trihalomethanes` (4.9% missing).
   * In total, **38.6% of the water samples** (1,265 rows) had at least one missing number.
2. **Impossible Sensor Readings:**
   * A few pH readings were negative or above 14 due to broken sensors.
3. **Extreme Mineral Spikes:**
   * Total Dissolved Solids had extreme spikes above 50,000 ppm.
4. **Messy Decimals:**
   * Numbers had too many uneven decimal places and needed rounding.

---

## 📚 References & Dataset Attribution

1. **Kaggle Source:** Kadiwal, Aditya. *Water Potability: Drinking Water Quality Dataset*. Available on Kaggle: [https://www.kaggle.com/datasets/adityakadiwal/water-potability](https://www.kaggle.com/datasets/adityakadiwal/water-potability).
2. **Benchmark Standards:** World Health Organization (WHO). *Guidelines for Drinking-water Quality (4th Edition)*, Geneva: WHO.
3. **Sustainable Development Goal:** UN SDG 6: Clean Water and Sanitation.

