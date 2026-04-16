# 📊 A/B Test Analysis — E-Commerce Website Conversion Optimization

![Dashboard](dashboard.png)

---

## 👤 Author

**Oyewole Jeremiah Oladayo**
*Data Analyst*

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/oyewole-jeremiah-9711a3231/)
[![Email](https://img.shields.io/badge/Email-Contact-red?style=for-the-badge&logo=gmail)](mailto:oyewolejerry2016@gmail.com)

---

## 📌 Project Overview

In this project, I analyzed the results of an **A/B test** conducted by an e-commerce company. The company developed a **new webpage** with the goal of increasing the number of users who **"convert"** — meaning users who decide to pay for the company's product.

My goal was to work through the data and help the company make a clear, evidence-based decision on whether to:
- ✅ **Implement the new page**
- ❌ **Keep the old page**
- ⏳ **Run the experiment longer**

---

## ❓ Problem Statement

> *"Does the new webpage lead to a statistically significant increase in user conversions compared to the old webpage?"*

The company invested resources in building a new webpage and needed evidence-based guidance before making a full rollout decision. A poorly performing page could cost the company revenue, while prematurely abandoning a potentially good page could mean missed growth opportunities. My job was to remove the guesswork and let the data speak.

---

## 📁 Dataset

The dataset contains **294,478 records** of user interactions captured during the A/B test.

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

One of the first things I checked was whether both groups were balanced in size. With only a **74 user difference** between groups, the experiment was well designed from a sampling perspective — ensuring a fair and unbiased comparison.

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| **Python** | Data cleaning, analysis, statistical testing |
| **Pandas** | Data manipulation and exploration |
| **NumPy** | Numerical calculations |
| **Matplotlib / Seaborn** | Python visualizations |
| **Statsmodels** | Z-test for proportions & Power Analysis |
| **Power BI** | Interactive business dashboard |

---

## 🔍 Methodology

### 1. Data Exploration

My first step was understanding the structure and quality of the data. I confirmed:
- No missing values across all 294,478 rows
- Both groups were nearly equal in size (147,202 vs 147,276)
- The `converted` column was correctly encoded as binary (0 or 1)

A balanced dataset with no missing values gave me confidence in the integrity of the analysis from the start.

---

### 2. Conversion Rate Analysis

I calculated conversion rates using the mean of the binary `converted` column:

$$\text{Conversion Rate} = \frac{\text{Number of users who converted}}{\text{Total number of users}}$$

**Overall Conversion Rate:**

$$\text{Overall} = \frac{35,237}{294,478} = 11.97\%$$

**Per Group:**

$$p_{control} = \frac{17,723}{147,202} = 12.04\%$$

$$p_{treatment} = \frac{17,514}{147,276} = 11.89\%$$

At first glance the old page appeared to perform better — but I knew I couldn't draw conclusions from raw numbers alone without testing whether this difference was statistically meaningful.

---

### 3. Lift Calculation

To measure how much better or worse the new page performed relative to the old page, I calculated the **lift:**

$$\text{Lift} = \frac{p_{treatment} - p_{control}}{p_{control}} \times 100 = \frac{0.1189 - 0.1204}{0.1204} \times 100 = -1.2289\%$$

A **negative lift of -1.2289%** confirmed the new page was underperforming. However, the lift alone does not tell us whether this difference is real or simply due to random chance — which is why hypothesis testing was necessary.

---

### 4. Hypothesis Testing

I framed the analysis as a formal hypothesis test:

**Null Hypothesis (H₀):**
> There is no difference in conversion rates between the old page and the new page.

$$H_0: p_{treatment} = p_{control}$$

**Alternative Hypothesis (H₁):**
> There is a statistically significant difference in conversion rates between the old and new page.

$$H_1: p_{treatment} \neq p_{control}$$

**Significance Level:** α = 0.05

I chose a **two-tailed test** because I was interested in detecting a difference in either direction — the new page being either better or worse than the old page.

---

### 5. Z-Test for Proportions

I used a **Z-test for two proportions** — the appropriate test when comparing conversion rates between two independent groups.

**Step 1 — Pooled Proportion:**

The pooled proportion represents the combined conversion rate across both groups, used as the baseline for calculating variance:

$$p_{pooled} = \frac{17,514 + 17,723}{147,276 + 147,202} = \frac{35,237}{294,478} = 0.1197$$

**Step 2 — Standard Error:**

$$SE = \sqrt{p_{pooled} \times (1 - p_{pooled}) \times \left(\frac{1}{n_{treatment}} + \frac{1}{n_{control}}\right)}$$

$$SE = \sqrt{0.1197 \times 0.8803 \times \left(\frac{1}{147,276} + \frac{1}{147,202}\right)} = 0.001197$$

**Step 3 — Z-Statistic:**

$$Z = \frac{p_{treatment} - p_{control}}{SE} = \frac{0.1189 - 0.1204}{0.001197} = -1.2369$$

**Step 4 — P-Value (Two-tailed):**

$$P\text{-value} = 2 \times (1 - \Phi(|Z|)) = 2 \times (1 - 0.8919) = 2 \times 0.1081 = 0.2161$$

The Z-table gives the cumulative probability to the **left** of the Z-score. Since we want the probability in the **tail** (extreme end), we subtract from 1, then multiply by 2 to account for both tails of the distribution.

---

### 6. Power Analysis

After completing the hypothesis test, I conducted a **post-experiment power analysis** to determine whether the sample size was sufficient to reliably detect a meaningful difference.

> **Important Note:** In a real business setting, power analysis should be conducted **before** the experiment begins — not after. The correct workflow is to use historical data to establish p1, have the business team define the MDE based on revenue impact, then calculate the required sample size before any data is collected. In this case, since the experiment had already been run, I conducted the power analysis retrospectively to evaluate whether the sample was adequate.

**How p1 and p2 Are Defined in Practice:**

- **p1** is pulled from historical analytics data (e.g. Google Analytics) before the experiment starts — it represents the known baseline conversion rate
- **p2** is constructed from p1 using the **Minimum Detectable Effect (MDE):**

$$p_2 = p_1 \times (1 + MDE)$$

The MDE is a **business decision** — not a statistical one. It answers the question:

> *"What is the smallest improvement in conversion rate that would justify switching to the new page?"*

This decision involves the finance team (revenue impact per 1% improvement), the product team (cost of building the new page), and the data analyst (translating business goals into statistical requirements).

**For this analysis I assumed an MDE of 2%** — a common industry standard for e-commerce conversion experiments — giving:

$$p_2 = 0.1204 \times 1.02 = 0.1228$$

**Sample Size Formula for Two Proportions:**

$$n = \frac{(Z_{\alpha/2} + Z_{\beta})^2 \times [p_1(1-p_1) + p_2(1-p_2)]}{(p_1 - p_2)^2}$$

**Step by Step Calculation:**

**Step 1:**
$$(Z_{\alpha/2} + Z_{\beta})^2 = (1.96 + 0.842)^2 = (2.802)^2 = 7.851$$

**Step 2:**
$$p_1(1-p_1) + p_2(1-p_2) = 0.1204(0.8796) + 0.1228(0.8772) = 0.10590 + 0.10772 = 0.21362$$

**Step 3:**
$$(p_1 - p_2)^2 = (0.1204 - 0.1228)^2 = (-0.0024)^2 = 0.00000576$$

**Step 4:**
$$n = \frac{7.851 \times 0.21362}{0.00000576} = \frac{1.6771}{0.00000576} \approx 291,163 \text{ per group}$$

**Why MDE Directly Affects Sample Size:**

The MDE lives in the denominator of the formula as $(p_1 - p_2)^2$. Because it is squared, even small changes in MDE have a dramatic impact on required sample size:

| MDE | $p_2$ | Required n per group |
|-----|-------|---------------------|
| 10% improvement | 0.1324 | ~11,647 |
| 5% improvement | 0.1264 | ~46,586 |
| 2% improvement | 0.1228 | ~291,163 |
| 1% improvement | 0.1216 | ~1,197,929 |

> *"Halving the MDE roughly quadruples the required sample size — because the difference is squared in the denominator."*

This is why defining the MDE carefully is one of the most consequential decisions in experiment design.

---

## 📈 Results

### Conversion Rates

| Group | Conversions | Total Users | Conversion Rate |
|-------|-------------|-------------|----------------|
| Control (Old Page) | 17,723 | 147,202 | **12.04%** |
| Treatment (New Page) | 17,514 | 147,276 | **11.89%** |
| Overall | 35,237 | 294,478 | **11.97%** |

### Statistical Test Results

| Metric | Value |
|--------|-------|
| **Lift** | **-1.2289%** |
| **Z-Statistic** | **-1.2369** |
| **P-Value** | **0.2161** |
| Significance Level (α) | 0.05 |
| Z Critical Value (±) | 1.96 |

### Power Analysis Results

| Metric | Value |
|--------|-------|
| Baseline Conversion Rate (p1) | 12.04% |
| Target Conversion Rate (p2) | 12.28% |
| Assumed MDE | 2% |
| Required Sample Size per group | 291,163 |
| Actual Sample Size per group | 147,202 |
| Shortfall per group | 143,961 |
| Sample Adequacy | ⏳ Only 51% of required |

---

## 🔬 Interpretation

### Statistical Test
- The **P-value of 0.2161** is significantly greater than α = 0.05 — meaning there is a **21.61% chance** the observed difference is due to random chance alone
- The **Z-statistic of -1.2369** falls well within the acceptance region (|Z| < 1.96) — not far enough from zero to be considered significant
- The negative sign on the Z-statistic confirms the treatment group performed **lower** than control — though what matters for significance is the absolute value
- Therefore I **fail to reject the null hypothesis**

### Power Analysis
- To reliably detect a 2% improvement I needed **291,163 users per group**
- The experiment only collected **147,202 per group** — just **51% of what was required**
- Running the experiment with insufficient sample size increases the risk of a **Type II Error**

| Error Type | Meaning | Risk in Our Case |
|------------|---------|-----------------|
| Type I (False Positive) | Concluding pages differ when they don't | Low — P-value is high |
| **Type II (False Negative)** | **Concluding pages are same when they differ** | **High — sample too small** |

> *"A Type II error here would mean concluding the new page has no effect when it might actually have a small positive effect that we simply didn't have enough data to detect."*

---

## ✅ Conclusion

$$P\text{-value} (0.2161) > \alpha (0.05) \therefore \text{ Fail to Reject } H_0$$

Based on my analysis, the current data does not provide sufficient evidence to conclude that the new page performs significantly differently from the old page. However, I cannot confidently recommend keeping the old page either — because the experiment was stopped before collecting enough data to make a reliable decision.

The sample size of 147,202 per group represents only **51% of the 291,163 users per group** needed to detect a meaningful 2% improvement. This means the experiment lacked the statistical power to detect small but potentially business-relevant differences.

### Final Recommendation to the Company

| Question | Answer | Reason |
|----------|--------|--------|
| Launch new page? | ❌ Not yet | No significant improvement detected |
| Keep old page? | ⏳ Temporarily | Old page currently performs better |
| Run experiment longer? | ✅ **Yes** | Need 291,163 users per group (currently at 51%) |

### Action Plan
1. ⏳ **Continue the experiment** until at least **291,163 users per group** are reached
2. 📊 **Re-run the statistical test** with the larger sample
3. 🔁 **If still not significant** — keep the old page and invest in a more impactful redesign
4. ✅ **If significant** — make a confident, data-driven launch decision


---

## 📊 Dashboard

The Power BI dashboard below summarizes all key findings interactively:

![A/B Test Dashboard](dashboard.png)

**Dashboard includes:**
- Total users and group balance (Donut Chart)
- Conversion rates per group (Column Chart)
- P-value gauge vs significance threshold (0.05)
- Converted vs not converted per group (Stacked Bar Chart)
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
