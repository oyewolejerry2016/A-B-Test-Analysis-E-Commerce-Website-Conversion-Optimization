# 📊 A/B Test Analysis — E-Commerce Website Conversion Optimization

![Dashboard](dashboard.png)

---

## 👤 Author

**Oyewole Jeremiah Oladayo**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/oyewole-jeremiah-9711a3231/)
[![Email](https://img.shields.io/badge/Email-Contact-red?style=for-the-badge&logo=gmail)](mailto:oyewolejerry2016@gmail.com)

---

## 📌 Project Overview

This project analyzes the results of an **A/B test** conducted by an e-commerce company. The company developed a **new webpage** with the goal of increasing the number of users who **"convert"** — meaning users who decide to pay for the company's product.

The objective of this analysis is to help the company make a data-driven decision on whether to:
- ✅ **Implement the new page**
- ❌ **Keep the old page**
- ⏳ **Run the experiment longer**

---

## ❓ Problem Statement

> *"Does the new webpage lead to a statistically significant increase in user conversions compared to the old webpage?"*

The company invested resources in building a new webpage and needed evidence-based guidance before making a full rollout decision. A poorly performing page could cost the company revenue, while prematurely abandoning a good page could mean missed growth opportunities.

---

## 📁 Dataset

The dataset contains **294,478 records** of user interactions during the A/B test.

| Column | Description |
|--------|-------------|
| `id` | Unique identifier for each user |
| `time` | Timestamp of when the user visited the page |
| `con_treat` | Whether the user was in the **control** or **treatment** group |
| `page` | Which page the user saw (**old_page** or **new_page**) |
| `converted` | Whether the user converted — **1 = Yes**, **0 = No** |

### Dataset Summary

| Metric | Value |
|--------|-------|
| Total Users | 294,478 |
| Control Group (Old Page) | 147,202 users |
| Treatment Group (New Page) | 147,276 users |
| Missing Values | None |

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| **Python** | Data cleaning, analysis, statistical testing |
| **Pandas** | Data manipulation and exploration |
| **NumPy** | Numerical calculations |
| **Matplotlib / Seaborn** | Data visualization |
| **Statsmodels** | Z-test for proportions |
| **Power BI** | Interactive dashboard |

---

## 🔍 Methodology

### 1. Data Exploration
- Loaded and inspected the dataset
- Checked for missing values (none found)
- Verified group balance between control and treatment

### 2. Conversion Rate Analysis
- Calculated overall conversion rate
- Calculated conversion rate per group
- Computed **lift** to measure relative performance

### 3. Hypothesis Testing

**Null Hypothesis (H₀):**
> There is no difference in conversion rates between the old page and the new page.
$$H_0: p_{treatment} = p_{control}$$

**Alternative Hypothesis (H₁):**
> There is a significant difference in conversion rates between the old page and the new page.
$$H_1: p_{treatment} \neq p_{control}$$

**Significance Level:** α = 0.05

### 4. Z-Test for Proportions

The Z-statistic was calculated as:

$$Z = \frac{p_{treatment} - p_{control}}{SE}$$

Where the Standard Error (SE) is:

$$SE = \sqrt{p_{pooled} \times (1 - p_{pooled}) \times \left(\frac{1}{n_{treatment}} + \frac{1}{n_{control}}\right)}$$

The P-value was derived as:

$$P\text{-value} = 2 \times (1 - \Phi(|Z|))$$

---

## 📈 Results

| Metric | Value |
|--------|-------|
| Control Conversion Rate | 12.04% |
| Treatment Conversion Rate | 11.89% |
| Overall Conversion Rate | 11.97% |
| **Lift** | **-1.2289%** |
| **Z-Statistic** | **-1.2369** |
| **P-Value** | **0.2161** |
| Significance Level (α) | 0.05 |

### Key Findings

- The **old page (control)** outperformed the new page with a conversion rate of **12.04%** vs **11.89%**
- The new page produced a **negative lift of -1.2289%** meaning it performed worse than the old page
- The **Z-statistic of -1.2369** is within the acceptance region (|Z| < 1.96), indicating no significant difference
- The **P-value of 0.2161** is significantly greater than the significance level of 0.05

---

## ✅ Conclusion

$$P\text{-value} (0.2161) > \alpha (0.05) \therefore \text{ Fail to Reject } H_0$$

> *"There is **no statistically significant difference** between the old page and the new page. The observed difference in conversion rates could easily be due to random chance."*

### Recommendation to the Company

| Decision | Recommendation |
|----------|---------------|
| Launch new page? | ❌ No |
| Keep old page? | ✅ Yes |
| Run longer? | ⏳ Not necessary — sample size is sufficient |

The company should:
1. **Keep the old page** — it currently performs better
2. **Redesign the new page** — the current version shows no meaningful improvement
3. **Run a new A/B test** — after making more significant changes to the new page

---

## 📊 Dashboard

The Power BI dashboard below summarizes all key findings interactively:

![A/B Test Dashboard](dashboard.png)

**Dashboard includes:**
- Total users and group balance
- Conversion rates per group
- P-value gauge vs significance threshold
- Converted vs not converted per group
- Z-statistic and lift KPI cards

---

## 📂 Project Structure

```
ab-test-analysis/
│
├── data/
│   ├── ab_test_data.csv          # Original dataset
│   └── ab_test_results.csv       # Statistical results
│
├── notebook/
│   └── ab_test_analysis.ipynb    # Jupyter Notebook
│
├── dashboard/
│   └── ab_test_dashboard.pbix    # Power BI Dashboard
│
├── images/
│   └── dashboard.png             # Dashboard screenshot
│
└── README.md                     # Project documentation
```

---

## 📬 Contact

Feel free to reach out if you have any questions or feedback about this project!

**Oyewole Jeremiah Oladayo**

| Platform | Link |
|----------|------|
| 💼 LinkedIn | [oyewole-jeremiah-9711a3231](https://www.linkedin.com/in/oyewole-jeremiah-9711a3231/) |
| 📧 Email | [oyewolejerry2016@gmail.com](mailto:oyewolejerry2016@gmail.com) |

---

*This project was completed as part of a data analysis portfolio. All analysis was performed using Python and Power BI.*
