# 🏦 Loan Application Risk Analysis

## ⚖️ Project Summary

This project delivers a comprehensive **exploratory data analysis (EDA)** of a real-world loan application dataset. The primary goal is to uncover **risk factors for loan default**, assess **data integrity**, and generate **actionable insights** that can assist financial institutions in optimizing their lending strategies.

By applying rigorous data preprocessing, outlier detection, class imbalance investigation, and correlation analysis, the project builds a solid foundation for future predictive modeling or business rule development.

---

## ✨ Key Deliverables

* Cleaned and preprocessed dataset with >30% missing-value columns dropped
* Outlier detection across numerical features using IQR and Z-score
* Class imbalance identification and visualization for binary target variable
* Univariate, segmented univariate, and bivariate analysis
* Segment-wise correlation analysis with business-focused interpretations
* Visual storytelling of all key findings using Python and Excel

---

## 🚀 Technologies & Libraries

* **Python 3.10+**
* **Pandas**: Data wrangling and transformation
* **NumPy**: Numerical operations and statistical analysis
* **Matplotlib & Seaborn**: High-quality visualizations
* **Jupyter Notebook**: Interactive development
* **Excel**: Supplemental reporting and executive visuals

---

## 📚 Dataset Overview

| Feature Category    | Example Features                               |
| ------------------- | ---------------------------------------------- |
| Client Demographics | `AGE`, `GENDER`, `EDUCATION`, `INCOME`         |
| Loan Attributes     | `LOAN_AMOUNT`, `DAYS_EMPLOYED`, `CREDIT_SCORE` |
| Target Variable     | `TARGET` (0: Non-default, 1: Default)          |

---

## 📊 Data Cleaning & Missing Value Strategy

1. **Missing Value Analysis**

   ```python
   missing_percentage = df.isnull().sum() / len(df) * 100
   df = df.loc[:, missing_percentage < 30]  # Drop columns >30% missing
   ```

2. **Imputation Techniques**

   * **Numerical**: Mean/Median
   * **Categorical**: Mode or domain-defined constant

---

## ⚠️ Outlier Detection & Handling

* **IQR Method**:

  ```python
  Q1 = df[col].quantile(0.25)
  Q3 = df[col].quantile(0.75)
  IQR = Q3 - Q1
  outliers = df[(df[col] < Q1 - 1.5*IQR) | (df[col] > Q3 + 1.5*IQR)]
  ```

* **Z-Score Method**:

  ```python
  from scipy.stats import zscore
  df['zscore'] = zscore(df['LOAN_AMOUNT'])
  df = df[df['zscore'].abs() < 3]
  ```

* **Visualization**: Boxplots, scatter plots, histograms

---

## ⚖️ Class Imbalance Analysis

* **Target Distribution**:

  ```python
  df['TARGET'].value_counts(normalize=True)
  ```
* **Findings**: \~92% non-defaults, \~8% defaults (Imbalance Ratio ≈ 11.5:1)
* **Visuals**: Pie Chart, Bar Plot, Countplot

---

## 📊 Univariate, Segmented & Bivariate Analysis

### A. **Univariate**

* Histograms and density plots for `INCOME`, `AGE`, `LOAN_AMOUNT`
* Categorical bar charts for `GENDER`, `EDUCATION`

### B. **Segmented Univariate**

* Compare income distribution for `TARGET == 0` vs `TARGET == 1`
* Visualize skewness and concentration for defaulters

### C. **Bivariate**

* Scatterplots: `LOAN_AMOUNT` vs `INCOME` color-coded by `TARGET`
* Boxplots: Loan risk by `EDUCATION`, `EMPLOYMENT_TYPE`
* Heatmaps of feature-to-target correlations

---

## 🔗 Correlation Analysis by Segment

```python
segment_0 = df[df['TARGET'] == 0]
segment_1 = df[df['TARGET'] == 1]
correlations_0 = segment_0.corr()['TARGET'].sort_values(ascending=False)
correlations_1 = segment_1.corr()['TARGET'].sort_values(ascending=False)
```

* **Insights**: Default drivers differ by segment (e.g., income stability, previous loans)
* Use cases: Customized scoring or risk model tuning per segment

---

## 📊 Key Business Insights

* High default probability in clients with:

  * Low and inconsistent income
  * Higher loan amounts relative to income
  * Certain employment types and education levels

* Outliers and missing values, if ignored, can distort risk predictions

* Class imbalance must be addressed before modeling (SMOTE, ADASYN recommended)

---

## 🚨 Limitations & Future Enhancements

* No time series tracking of customer behavior
* Predictive models (e.g., logistic regression, random forest) can be built as next step
* Integrate Power BI or Tableau dashboards for stakeholder presentation

---

## 👨‍💼 Author & Contact

**Name**: Your Name
**LinkedIn**: [linkedin.com/in/your-profile](https://linkedin.com/in/your-profile)
**GitHub**: [github.com/your-username](https://github.com/your-username)
**Email**: [your.email@example.com](mailto:your.email@example.com)

---

## 💾 How to Run

1. Clone repository:

```bash
git clone https://github.com/your-username/loan-risk-analysis.git
cd loan-risk-analysis
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Run Jupyter Notebook:

```bash
jupyter notebook notebooks/Loan_Application_Analysis.ipynb
```

---

## 🎓 License

MIT License. See `LICENSE` file.

> 💭 "Behind every default is a data story — decode it smart, mitigate it early."

| 🧠 **Key Insights & Recommendations** |
| ------------------------------------- |

### 📌 Behavioral Patterns of Defaulters:

* Tend to be **younger**, **lower income**, and **less stable employment**
* Often have **lower external credit scores**

### ⚠️ Risk Management Tips:

* Apply **stricter criteria** or deeper assessment for applicants:

  * Younger than 30
  * Earning under 100k
  * With short employment history (< 1 year)
* Consider **data balancing techniques** (e.g., SMOTE or weighted models) before training classifiers.

### 📈 Feature Importance:

* `EXT_SOURCE_3`, `DAYS_BIRTH`, and `AMT_INCOME_TOTAL` are **high-value predictors** for model building.

---

## ✅ Final Thoughts:

Your analysis has revealed key factors that can help **predict and prevent loan defaults**, making it possible to build **targeted risk models** and **policy rules** to safeguard the institution’s loan portfolio.
