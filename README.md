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



.-------------
To approach this machine learning project, you should follow a structured methodology that includes data preprocessing, exploratory data analysis, feature engineering, model selection, and evaluation. Since you're dealing with macroeconomic data across countries and years, your approach must also account for the time-series and panel data nature of the dataset.

### Project Approach

The project can be broken down into the following key phases:

1.  **Data Preprocessing and Preparation**:
    * **Handling Missing Values**: Since macroeconomic datasets often have missing data, you'll need to decide how to handle them. Options include **imputation** (e.g., using mean, median, or more advanced methods like K-nearest neighbors) or **removal** of rows/columns with a high percentage of missing values. The choice depends on the amount and pattern of missingness.
    * **Data Scaling**: Most machine learning algorithms, particularly those based on distance like K-means or SVM, are sensitive to the scale of the features. You should **normalize** or **standardize** the numerical variables to ensure they are on a similar scale.
    * **Feature and Target Separation**: Clearly define your **target variable**, "Bank crisis," and your **features** (all other macroeconomic variables).

2.  **Exploratory Data Analysis (EDA)**:
    * **Univariate Analysis**: Examine the distribution of individual variables. For "Bank crisis," a binary target, you should check for **class imbalance**. If one class (e.g., "no crisis") is much more frequent than the other, you'll need to address this later.
    * **Bivariate Analysis**: Investigate the relationship between features and the target variable. You can use **correlation matrices** or plots to see which macroeconomic indicators are most correlated with "Bank crisis." This gives you initial insights into potential predictors.
    * **Time-Series and Panel Data Aspects**:
        * **Time Plots**: Plot key macroeconomic variables over time to identify trends, seasonality, or sudden shifts that might precede a crisis.
        * **Cross-Country Comparisons**: Compare variable distributions and trends across different countries to understand heterogeneity.

3.  **Feature Engineering**:
    * **Creating Lagged Variables**: Bank crises are often preceded by specific macroeconomic conditions. You can create new features by lagging existing variables (e.g., `GDP_growth_lag_1`, `inflation_lag_2`). The lag period (e.g., 1 year, 2 years) should be chosen based on economic theory and insights from your EDA.
    * **Interaction Features**: Combine features to capture more complex relationships. For instance, the ratio of debt to GDP might be a more powerful predictor than either variable alone.
    * **Moving Averages**: Calculate **rolling means** or **moving averages** of variables to smooth out short-term fluctuations and capture long-term trends.
    * **Handling Time and Country**: Since this is panel data, you may need to include **country-specific dummy variables** or a **year-variable** to account for fixed effects or global trends that affect all countries.

4.  **Model Selection and Training**:
    * **Addressing Class Imbalance**: If you found significant class imbalance during EDA, you must address it. Techniques include:
        * **Resampling**: **Oversampling** the minority class (e.g., using SMOTE) or **undersampling** the majority class.
        * **Algorithmic Approach**: Using models that are robust to imbalance, such as **XGBoost** or **LightGBM**, which allow you to adjust class weights.
    * **Model Choices**: Given the classification nature of the problem, consider a variety of models:
        * **Logistic Regression**: A good baseline model that's easy to interpret.
        * **Decision Trees, Random Forests, and Gradient Boosting Machines (e.g., XGBoost)**: Powerful, non-linear models that can capture complex interactions. They are often excellent for this type of problem.
        * **Support Vector Machines (SVMs)**: Effective for high-dimensional data.
    * **Time-Series Split**: Since your data has a temporal component, a standard **random train-test split is not appropriate**. You must use a **time-series split**, where you train the model on data up to a certain year and test it on subsequent years. This ensures your model is evaluated on its ability to predict future crises, which is a more realistic and robust assessment.

5.  **Model Evaluation and Interpretation**:
    * **Evaluation Metrics**: For an imbalanced dataset, simple accuracy is a poor metric. Use metrics that focus on the minority class:
        * **Precision**: The proportion of predicted crises that were actually crises.
        * **Recall**: The proportion of actual crises that were correctly identified.
        * **F1-Score**: The harmonic mean of precision and recall.
        * **ROC AUC**: Measures the model's ability to distinguish between classes.
    * **Feature Importance**: Once you have a final model, especially with tree-based models like Random Forests or XGBoost, analyze the **feature importance scores** to understand which macroeconomic variables were most influential in predicting a bank crisis. This step is crucial for gaining macroeconomic insights.     * **Validation**: It's essential to validate the model's performance on unseen data, which is why the time-series split is so critical. You could even use a **walk-forward validation** strategy where you retrain and test the model iteratively on new time periods.

6.  **Refinement and Deployment**:
    * Based on the evaluation, you can refine your feature engineering or try different models. The final model could then be used for forecasting or policy analysis.


