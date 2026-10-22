# 🚖 Smart Mobility & Ride Analytics

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/hasanulazad-cloud/-Smart-Mobility-Ride-Analytics-/blob/main/Smart_Mobility_%26_Ride_Analytics.ipynb)
![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-Statistics-8CAAE6?logo=scipy&logoColor=white)
![Statsmodels](https://img.shields.io/badge/Statsmodels-Z--tests-4c72b0)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

> A statistical deep-dive into 200 ride-hailing trips: descriptive statistics, correlation, confidence intervals, hypothesis tests, outlier detection and probability, used to test whether distance, surge, ride type and peak hours really drive fares.

---

## 📌 Project Overview

A ride-hailing company wants evidence, not assumptions, about pricing and service. This project applies a full statistical toolkit to a trip dataset and answers eight business questions, from "does distance affect fare?" to "can statistics support pricing decisions?".

**Dataset:** 200 trips, 6 columns, no missing values

| Column | Description |
|---|---|
| `Trip_Distance` | Distance travelled (2 to 29) |
| `Fare_Amount` | Fare charged (37.59 to 468.75) |
| `Ride_Category` | Economy, Shared or Premium |
| `Surge_Multiplier` | 1.0 to 2.5 |
| `Customer_Rating` | 1 to 5 |
| `Ride_Time` | Peak or Non-Peak |

---

## 📂 Repository Contents

| File | Description |
|---|---|
| `Smart_Mobility_&_Ride_Analytics.ipynb` | Main notebook: cleaning, statistics, tests, outliers, probability (opens in Colab via the badge) |
| `Analysis_answers.ipynb` | Written answers and conclusions for the eight business questions |

---

## 🧰 Techniques Used

| Area | Methods |
|---|---|
| **Linear algebra** | Correlation matrix, determinant, eigenvalues and eigenvectors |
| **Descriptive statistics** | Mean, median, mode, standard deviation, variance, skewness, kurtosis |
| **Correlation** | Pearson, Spearman, covariance, heatmap |
| **Estimation** | Point estimate, 95% confidence interval, Central Limit Theorem, bootstrapping |
| **Hypothesis tests** | Z-test, one-sample t-test, two-sample t-test, chi-square, ANOVA |
| **Outliers** | Percentile (1st and 99th), IQR and Z-score methods |
| **Probability** | Basic and conditional probability, Bayes' theorem |

---

## 📊 Key Findings

### Descriptive summary
| Variable | Mean | Median | Std dev |
|---|---|---|---|
| Fare amount | 260.31 | 256.91 | 78.71 |
| Trip distance | 15.64 | 15 | 8.43 |
| Surge multiplier | 1.68 | 1.5 | 0.55 |
| Customer rating | 2.93 | 3 | 1.44 |

Skewness is close to zero for every variable, so the data are roughly symmetric.

### Business questions

| Question | Result | Conclusion |
|---|---|---|
| Does distance affect fare? | Pearson r = 0.017 | ❌ No meaningful relationship |
| Are Premium rides more expensive than Economy? | t = −0.41, p = 0.684 | ❌ No significant difference |
| Does surge affect ratings? | r = −0.041 | ➖ Very weak negative link |
| Do Peak and Non-Peak fares differ? | Z = −0.60, p = 0.549 | ❌ No significant difference |
| Is average fare different from 270? | t = −1.74, p = 0.083 | ❌ Not significant at 5% |
| Are ride category and ride time related? | χ² = 1.48, p = 0.477 | ❌ Independent |
| Are there pricing anomalies? | IQR: 1 outlier (fare 37.59); Z-score: 0 | ✅ Essentially clean |

### Estimating the average fare

| Method | 95% interval |
|---|---|
| Sample of 100 (confidence interval) | 241.7 to 269.2 |
| Bootstrap (1,000 resamples) | 249.6 to 271.4 |

The bootstrap mean (260.29) is almost identical to the actual mean (260.31).

### Probabilities

| Event | Probability |
|---|---|
| High fare (300 or more) | 0.325 |
| Good rating (4 or 5) | 0.375 |
| Peak-time trip | 0.515 |
| Surge trip (multiplier above 1) | 0.710 |
| Economy / Shared / Premium | 0.41 / 0.30 / 0.29 |
| Surge given Peak | 0.718 |
| High fare given Surge and Peak | 0.284 |
| **Premium given Peak (Bayes)** | **0.311** |

### 🎯 Takeaways
1. **Fares in this dataset are not explained by distance, ride category, surge or time of day.** All correlations are close to zero and none of the group comparisons is significant.
2. **Operational factors are independent.** The correlation matrix has a determinant of 0.987 and eigenvalues close to 1 (0.89 to 1.11), so there is little multicollinearity and no single dominant factor.
3. **Surge applies to 71% of trips yet is unrelated to fare**, which is worth investigating before any pricing change.
4. **Ride mix is stable across peak and off-peak**, so demand by category does not shift with time of day.

---

## 🚀 How to Run

**Option 1: Google Colab.** Click the *Open in Colab* badge at the top.

**Option 2: Locally**

```bash
# 1. Clone the repository
git clone https://github.com/hasanulazad-cloud/-Smart-Mobility-Ride-Analytics-.git
cd -- -Smart-Mobility-Ride-Analytics-

# 2. Install the dependencies
pip install numpy pandas matplotlib seaborn scipy statsmodels openpyxl jupyter

# 3. Open the notebook (an internet connection is needed to load the dataset)
jupyter notebook "Smart_Mobility_&_Ride_Analytics.ipynb"
```

> ℹ️ Cell 4 uses Google Colab's sheet viewer and only works in Colab. Skip it when running locally; the analysis does not depend on it.

---

## ⚠️ Known Limitations

- **Colab-only cell.** The `google.colab` import in cell 4 fails outside Colab.
- **Outlier removal is not applied to the data.** `clean_data` is created but never used, so the fare of 37.59 stays in the later analysis.
- **Random sampling without a seed.** The 100-row confidence interval and the bootstrap change on every run, so exact figures vary slightly.
- **Redundant ANOVA.** With only two groups (Economy and Premium), ANOVA gives the same p-value as the t-test (0.684). A three-group ANOVA including Shared would add information.
- **Near-zero relationships.** The data behave as if the variables were generated independently, so the "no effect" conclusions may reflect the dataset rather than real ride-hailing behaviour.

---

## 🔮 Future Improvements

- Compare all three ride categories with ANOVA and a post-hoc test
- Check test assumptions (normality, equal variance)
- Add regression to quantify the effect of each variable on fare
- Test on a larger, real-world trip dataset

---

## 👤 Author

**Hasanul H Azad**
Medical billing / RCM professional upskilling in Data Science, AI and Machine Learning
GitHub: [@hasanulazad-cloud](https://github.com/hasanulazad-cloud)

---

⭐ If you found this useful, consider starring the repo.
