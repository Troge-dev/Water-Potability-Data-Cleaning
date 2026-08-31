# Chapter 3: Simple Presentation & Defense Guide

This guide gives you simple, easy-to-explain answers for your presentation. You can use these plain-English answers if your teacher or classmates ask why you made certain cleaning choices.

---

### Question 1: Where does this dataset come from and what does it measure?

```{admonition} Simple Answer
:class: tip
**"It is the Kaggle Water Potability Dataset by Aditya Kadiwal, measuring 3,276 water samples against WHO drinking safety limits."**
```

* **Dataset Origin:** Sourced from the public [Water Potability Dataset on Kaggle](https://www.kaggle.com/datasets/adityakadiwal/water-potability) created by Aditya Kadiwal.
* **Content:** 3,276 water samples collected from diverse water bodies (wells, taps, lakes, facilities) with 9 chemical/physical indicators and 1 binary label (`Potability`: 1 = Safe, 0 = Unsafe).
* **Evaluation Standards:** Chemical limits are based on World Health Organization (WHO) Guidelines for Drinking-water Quality.

---

### Question 2: Why did you fill in missing values instead of deleting rows?

```{admonition} Simple Answer
:class: tip
**"Deleting rows would throw away nearly 40% of our data!"**
```

* **The Problem:** 1,265 rows out of 3,276 have at least one missing chemical test (especially Sulfate and pH). That is almost **39% of the whole dataset**.
* **Why deleting is bad:** If we delete 39% of the data using `dropna()`, our dataset becomes too small and our results become biased.
* **Our Solution:** We filled in the missing numbers so we could keep **all 3,276 water samples** for analysis.

---

### Question 2.1: Is the missing data MCAR, MAR, or MNAR?

```{admonition} Simple Answer
:class: tip
**"It is MCAR / MAR (Missing Completely at Random & Missing at Random) — meaning tests were skipped due to lab costs and sensor limitations, not because the water was dangerously toxic (which would be MNAR)."**
```

* **MCAR Evidence:** Missing slots are scattered randomly with near-zero correlation ($r < 0.03$) across other measurements.
* **MAR Evidence:** Non-potable samples had slightly different lab testing rates than potable samples (24.4% vs 22.9%), justifying class-conditional imputation.
* **Why it is NOT MNAR:** Recorded values span full, normal bell curves without truncation at the extremes, proving samples were not skipped due to off-the-scale contamination.
* **Key Takeaway:** Because data is MCAR/MAR, statistical median imputation is valid, unbiased, and mathematically sound.

---

### Question 3: Why did you use the Median instead of the Mean (Average)?

```{admonition} Simple Answer
:class: tip
**"The average gets pulled by extreme numbers. The median gives the true middle value."**
```

* **Example:** If 4 water samples have a mineral level of 200, but 1 sample has a crazy spike of 50,000, the *average* becomes 10,160 (which is completely misleading!).
* **Why the Median is better:** The *median* simply picks the middle number (200), which accurately represents normal water.

---

### Question 4: Why did you fill missing values separately for Safe Water and Unsafe Water?

```{admonition} Simple Answer
:class: tip
**"Safe water and unsafe water naturally have different chemical levels."**
```

* **Why it matters:** Water that is safe to drink (`Potability = 1`) has different amounts of chlorine and minerals compared to dirty or contaminated water (`Potability = 0`).
* **Our Solution:** We grouped the data by `Potability`. If a safe water sample was missing a value, we filled it with the safe water median. If an unsafe sample was missing a value, we filled it with the unsafe water median.

---

### Question 5: Why did you check that pH is between 0 and 14?

```{admonition} Simple Answer
:class: tip
**"pH can scientifically only exist between 0 and 14. Anything else is a broken sensor."**
```

* **Scientific Rule:** The pH scale only goes from 0 (very acidic like battery acid) to 14 (very basic like bleach). Pure water is 7.
* **Our Solution:** If a sensor recorded a negative number or a number above 14, we knew the sensor was broken. We converted those impossible numbers to missing values and filled them properly.

---

### Question 6: Why didn't you delete all high mineral levels (Solids) as outliers?

```{admonition} Simple Answer
:class: tip
**"Natural groundwater is full of minerals. Using a standard cutoff would wrongly delete 47 valid water samples."**
```

* **The Reality:** Tap water usually has 500 ppm of solids, but natural mineral-rich spring water or deep wells can easily reach 20,000 to 30,000 ppm.
* **Why standard boxplot rules fail:** A standard cutoff ($1.5 \times \text{IQR} = 44,832\text{ ppm}$) would delete 47 perfectly valid, natural water samples.
* **Our Solution:** We used an **extreme boundary ($3.0 \times \text{IQR} \approx 62,331\text{ ppm}$)**. This protects 100% of real mineral water and retains all 3,276 water samples.

---

### Summary Checklist to Remember for Presentation:
1. **Source & Origin:** [Kaggle Water Potability Dataset](https://www.kaggle.com/datasets/adityakadiwal/water-potability) by Aditya Kadiwal (3,276 water samples, 9 water quality features + 1 target).
2. **Goal:** Clean missing chemical assays and validate sensor readings to determine drinking water safety.
3. **Biggest Problem:** ~39% of water samples (1,265 rows) had missing test results.
4. **Main Action:** Filled missing values using class-conditional group medians, enforced physical pH bounds [0, 14], and applied extreme IQR validation.
5. **Final Result:** 100% complete dataset with 0 missing values and 100% sample retention (3,276 / 3,276 samples), ready for EDA and machine learning.


