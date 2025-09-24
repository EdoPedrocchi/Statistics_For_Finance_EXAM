# Statistics\_For\_Finance\_EXAM

Dataset from: [Global Macro Data](https://www.globalmacrodata.com/?utm_source=chatgpt.com)

Dataset of **46 macroeconomic variables** across **243 countries**, covering historical records starting in **1086** and extending to **2024**, with projections up to **2030**.

### 🎯 Goal

Classify and predict **banking crises** using macroeconomic variables.

### 🛠 Steps so far:

* Removed repetitive variables
* Removed variables with too many missing values (>50%)
* Result: XX rows × XX columns
* For each country/year, calculated: 5-year **moving average**, **standard deviation**, and **percentage change**
* Removed all rows with at least one missing value
* Final result: XX rows × XX columns

---

## 📊 Exploratory Data Analysis (EDA)

### **General Overview**

* 7,915 rows × 43 columns
* 0% missing values, 0% duplicates

### **Target Variable**

* **BankingCrisis**: Only 2.5% banking crises (198 out of 7,915 observations)
* Severe **class imbalance** problem (1:39 ratio)

### **Key Findings**

#### Distribution Issues:

1. **Extreme skewness** (skewness > 10):

   * `rGDP_pc_mean5y` & `rGDP_pc_std5y`: skewness \~51
   * Many USD and FX variables also heavily skewed

2. **Significant outliers**:

   * Very high kurtosis (>100) in several variables indicates extreme outliers
   * Huge ranges suggest anomalous values

#### Economic Variables of Interest:

* **GDP per capita** (`rGDP_pc_*`): very wide cross-country variability
* **Consumption** (`cons_*`): relatively stable (average \~81% of GDP)
* **Investment** (`inv_*`, `finv_*`): more volatile
* **Inflation** (`infl_*`): extremely skewed (>50), indicating episodes of hyperinflation

---

## ⚠️ Identified Problems

### 1. Data Distribution

```
- Many variables deviate strongly from normality
- Presence of extreme values that may distort models
- Some variables span huge ranges (e.g., rGDP_pc_mean5y: 0 – 1B)
```

### 2. Scale Differences

```
- Variables are on very different scales → standardization required
- Example: BankingCrisis (0–1) vs rGDP_USD_mean5y (0–20M)
```

### 3. Severe Class Imbalance

```
- Only 2.5% positive cases (banking crises)
- Models may be biased toward the majority class
- Balancing techniques (SMOTE, undersampling, etc.) are needed
```

---

## 🔎 Data Types & Missing Values

(Extract – all variables are float64, no missing values)

Example:

```
BankingCrisis       float64   7915 non-null
rGDP_pc_mean5y      float64   7915 non-null
...
imports_USD_chg     float64   7915 non-null
```

---

## 📈 Descriptive Statistics

* Banking crises extremely rare (binary target, 2.5% positive)
* Several variables with **huge ranges** and **extreme skewness/kurtosis** (e.g., GDP, inflation, FX)
* Many **USD-denominated variables** prone to large distortions from exchange rate volatility

---

## 📌 Why 5-Year Derived Features?

Banking crises depend not only on the **absolute value** of a macroeconomic variable, but on its **dynamics** over time.
To capture this, we derived three 5-year features for each variable:

1. **Moving average (mean)** → captures structural levels (e.g., persistently low GDP, persistently high inflation)
2. **Standard deviation (std)** → measures volatility/instability (e.g., fluctuating inflation)
3. **Percentage change (chg)** → measures growth/shrinkage trends (sharp booms or busts may trigger crises)



