# Statistics_For_Finance_EXAM

Dataset from here https://www.globalmacrodata.com/?utm_source=chatgpt.com

Dtaset of 46 macroeconomic variables across 243 countries from historical records beginning in the year 1086 and extending to 2024 with projections up to 2030.

My goal:
- classify and predict bank crisis using macroeconmic variables

i made the following steps:
- eliminted ripetitive variables
- elimninated variables with too much missing values (>50%)
- Result: XX rows x XX columns
- For each country in each year, calculated moving average, standard deviation and percentage change in 5 years.
- eliminated all rows with at least one missing values
- Result: xx rows x XX columns





## EDA

## **📊 PANORAMICA GENERALE**
- 7,915 righe × 43 colonne, 
-  0% valori mancanti, 0% duplicati

## **🎯 VARIABILE TARGET**
- **BankingCrisis**: Solo 2.5% di crisi bancarie (198 su 7,915 osservazioni)
- **Problema di class imbalance** molto pronunciato (1:39 rapporto)

## **📈 CARATTERISTICHE PRINCIPALI**

### **Problematiche di Distribuzione:**
1. **Estrema asimmetria** (skewness > 10):
   - `rGDP_pc_mean5y` e `rGDP_pc_std5y`: skewness ~51 (distribuzioni molto skewed)
   - Molte variabili USD e di cambio: skewness > 10

2. **Outliers significativi**:
   - Kurtosis molto elevata (>100) in diverse variabili indica presenza di outliers estremi
   - Range enormi suggeriscono valori anomali

### **Variabili Economiche Chiave:**
- **PIL pro capite** (`rGDP_pc_*`): Ampia variabilità tra paesi
- **Consumi** (`cons_*`): Relativamente stabili (media ~81% del PIL)
- **Investimenti** (`inv_*`, `finv_*`): Più volatili
- **Inflazione** (`infl_*`): Skewness estrema (>50) indica episodi iperinflazionistici

## **⚠️ PROBLEMI IDENTIFICATI**

### **1. Distribuzione dei Dati:**
```
- Molte variabili non seguono distribuzione normale
- Presenza di valori estremi che possono distorcere i modelli
- Alcune variabili hanno range enormi (es: rGDP_pc_mean5y: 0 - 1B)
```

### **2. Scale Diverse:**
```
- Variabili su scale molto diverse richiedono standardizzazione
- Es: BankingCrisis (0-1) vs rGDP_USD_mean5y (0-20M)
```

### **3. Class Imbalance Critico:**
```
- Solo 2.5% crisi bancarie → modelli potrebbero essere biased
- Necessarie tecniche di bilanciamento (SMOTE, undersampling, ecc.)





----------------------------risultato eda----
analizza questi risultati dell'eda

```


1.  TIPI DI DATI E VALORI MANCANTI
--------------------------------------------------
                       Tipo  Valori_Non_Null  Valori_Null  Percentuale_Null
BankingCrisis       float64             7915            0               0.0
rGDP_pc_mean5y      float64             7915            0               0.0
rGDP_pc_std5y       float64             7915            0               0.0
rGDP_pc_chg         float64             7915            0               0.0
rGDP_USD_mean5y     float64             7915            0               0.0
rGDP_USD_std5y      float64             7915            0               0.0
rGDP_USD_chg        float64             7915            0               0.0
cons_GDP_mean5y     float64             7915            0               0.0
cons_GDP_std5y      float64             7915            0               0.0
cons_GDP_chg        float64             7915            0               0.0
inv_GDP_mean5y      float64             7915            0               0.0
inv_GDP_std5y       float64             7915            0               0.0
inv_GDP_chg         float64             7915            0               0.0
finv_GDP_mean5y     float64             7915            0               0.0
finv_GDP_std5y      float64             7915            0               0.0
finv_GDP_chg        float64             7915            0               0.0
exports_GDP_mean5y  float64             7915            0               0.0
exports_GDP_std5y   float64             7915            0               0.0
exports_GDP_chg     float64             7915            0               0.0
USDfx_mean5y        float64             7915            0               0.0
USDfx_std5y         float64             7915            0               0.0
USDfx_chg           float64             7915            0               0.0
CPI_mean5y          float64             7915            0               0.0
CPI_std5y           float64             7915            0               0.0
CPI_chg             float64             7915            0               0.0
infl_mean5y         float64             7915            0               0.0
infl_std5y          float64             7915            0               0.0
infl_chg            float64             7915            0               0.0
pop_mean5y          float64             7915            0               0.0
pop_std5y           float64             7915            0               0.0
pop_chg             float64             7915            0               0.0
cons_USD_mean5y     float64             7915            0               0.0
cons_USD_std5y      float64             7915            0               0.0
cons_USD_chg        float64             7915            0               0.0
inv_USD_mean5y      float64             7915            0               0.0
inv_USD_std5y       float64             7915            0               0.0
inv_USD_chg         float64             7915            0               0.0
finv_USD_mean5y     float64             7915            0               0.0
finv_USD_std5y      float64             7915            0               0.0
finv_USD_chg        float64             7915            0               0.0
imports_USD_mean5y  float64             7915            0               0.0
imports_USD_std5y   float64             7915            0               0.0
imports_USD_chg     float64             7915            0               0.0



5. STATISTICHE DESCRITTIVE - VARIABILI NUMERICHE
--------------------------------------------------
       BankingCrisis  rGDP_pc_mean5y  rGDP_pc_std5y  rGDP_pc_chg  \
count    7915.000000    7.915000e+03   7.915000e+03  7915.000000   
mean        0.025016    1.414226e+06   4.222297e+05     0.021330   
std         0.156183    1.545262e+07   1.751520e+07     0.063414   
min         0.000000    2.866879e-07   0.000000e+00    -0.575186   
25%         0.000000    1.313480e+04   5.883084e+02    -0.000658   
50%         0.000000    3.863872e+04   1.750897e+03     0.022684   
75%         0.000000    2.767438e+05   1.249298e+04     0.046372   
max         1.000000    1.032515e+09   9.556203e+08     1.404906   

       rGDP_USD_mean5y  rGDP_USD_std5y  rGDP_USD_chg  cons_GDP_mean5y  \
count     7.915000e+03    7.915000e+03   7915.000000      7915.000000   
mean      2.712884e+05    1.491240e+04      0.038342        80.934914   
std       1.165524e+06    6.375110e+04      0.065362        16.603394   
min       1.106541e-01    2.069750e-03     -0.569937        17.643313   
25%       5.274551e+03    3.242654e+02      0.015034        72.757378   
50%       2.236985e+04    1.594054e+03      0.039064        80.091684   
75%       1.313527e+05    8.078847e+03      0.063569        88.964082   
max       2.074736e+07    1.148588e+06      1.499730       261.385736   

       cons_GDP_std5y  cons_GDP_chg  ...  cons_USD_chg  inv_USD_mean5y  \
count     7915.000000   7915.000000  ...   7915.000000    7.915000e+03   
mean         3.356976      0.002462  ...      1.673595    4.631586e+04   
std          4.171815      0.079465  ...    114.334633    2.256524e+05   
min          0.000000     -0.589400  ...     -0.990148    2.089152e-08   
25%          1.159657     -0.020457  ...      0.009653    3.295098e+02   
50%          2.176149     -0.001269  ...      0.078304    2.000806e+03   
75%          4.079491      0.018503  ...      0.158797    1.404206e+04   
max         89.669341      2.078348  ...  10017.883751    4.546966e+06   

       inv_USD_std5y   inv_USD_chg  finv_USD_mean5y  finv_USD_std5y  \
count   7.915000e+03   7915.000000     7.915000e+03    7.915000e+03   
mean    7.844407e+03      2.086713     4.463180e+04    7.302249e+03   
std     4.345605e+04    132.696707     2.206949e+05    4.193422e+04   
min     1.467811e-09   -112.095581     1.726363e-08    8.082422e-10   
25%     6.932197e+01     -0.036552     3.119707e+02    6.063935e+01   
50%     4.476544e+02      0.088194     1.720996e+03    3.694847e+02   
75%     2.753423e+03      0.223099     1.307221e+04    2.457828e+03   
max     1.301762e+06  11461.690394     4.386621e+06    1.282413e+06   

       finv_USD_chg  imports_USD_mean5y  imports_USD_std5y  imports_USD_chg  
count   7915.000000        7.915000e+03        7915.000000      7915.000000  
mean       2.213234        4.425921e+04        6825.077617         2.071112  
std      143.575173        1.676572e+05       26183.206209       145.907771  
min       -2.733210        1.435996e-08           0.000000        -0.988107  
25%       -0.024333        5.534287e+02          89.034974        -0.011646  
50%        0.088518        2.524202e+03         503.922954         0.086983  
75%        0.209627        1.599082e+04        2961.294247         0.196736  
max    12350.480205        2.942696e+06      695366.689068     12841.317851  

[8 rows x 43 columns]

STATISTICHE AGGIUNTIVE:
                     Skewness     Kurtosis         Range            IQR
BankingCrisis        6.083949    35.023284  1.000000e+00       0.000000
rGDP_pc_mean5y      50.958101  3060.772620  1.032515e+09  263609.015527
rGDP_pc_std5y       51.790090  2699.221441  9.556203e+08   11904.671901
rGDP_pc_chg          3.158519    75.806528  1.980092e+00       0.047031
rGDP_USD_mean5y     10.548516   137.645313  2.074736e+07  126078.114063
rGDP_USD_std5y      10.737841   139.340385  1.148588e+06    7754.581748
rGDP_USD_chg         3.359734    80.398998  2.069666e+00       0.048535
cons_GDP_mean5y      2.436757    23.980825  2.437424e+02      16.206705
cons_GDP_std5y       6.380904    81.532849  8.966934e+01       2.919834
cons_GDP_chg         6.641610   143.562365  2.667748e+00       0.038960
inv_GDP_mean5y       1.361266     6.752311  1.115321e+02      10.639718
inv_GDP_std5y        3.834515    27.448616  4.528575e+01       2.307496
inv_GDP_chg        -40.090990  2945.671791  4.227631e+01       0.147231
finv_GDP_mean5y      2.141749    15.123139  1.275218e+02       9.724352
finv_GDP_std5y       4.449368    35.352819  4.382798e+01       2.138011
finv_GDP_chg         7.256607   139.148667  9.054158e+00       0.123030
exports_GDP_mean5y   2.611124    11.718060  2.201679e+02      24.556558
exports_GDP_std5y    3.210291    16.239902  4.256473e+01       3.004469
exports_GDP_chg     12.940404   346.209357  9.376211e+00       0.130571
USDfx_mean5y        10.047685   118.490269  2.334455e+04      50.154116
USDfx_std5y         16.235998   344.725123  8.143797e+03       4.512589
USDfx_chg           82.501141  7099.598595  2.631522e+03       0.087882
CPI_mean5y          25.011289   671.030114  9.243000e+03      71.668705
CPI_std5y           28.879845   879.507511  5.786120e+03       5.059979
CPI_chg             37.918384  1787.044173  2.387313e+02       0.096870
infl_mean5y         52.307614  2956.053318  2.824330e+09       9.995309
infl_std5y          46.512144  2224.523895  3.994206e+09       5.516375
infl_chg                  NaN          NaN           inf       0.843334
pop_mean5y           8.263374    75.372082  1.371347e+03      20.486837
pop_std5y            8.022225    72.124248  3.480685e+01       0.551700
pop_chg             -0.662095    29.381063  4.500345e-01       0.019694
cons_USD_mean5y     12.826786   209.351681  1.610635e+07   38458.680713
cons_USD_std5y      15.841159   378.254438  2.893676e+06    6374.595292
cons_USD_chg        85.309258  7448.697157  1.001887e+04       0.149143
inv_USD_mean5y      11.208550   157.120967  4.546966e+06   13712.549490
inv_USD_std5y       16.986430   378.518347  1.301762e+06    2684.100597
inv_USD_chg         82.365579  7047.812730  1.157379e+04       0.259651
finv_USD_mean5y     11.185546   155.563266  4.386621e+06   12760.242836
finv_USD_std5y      17.559668   401.454496  1.282413e+06    2397.188850
finv_USD_chg        81.677091  6941.971493  1.235321e+04       0.233961
imports_USD_mean5y   9.010936   110.253914  2.942696e+06   15437.389691
imports_USD_std5y   11.696733   208.563133  6.953667e+05    2872.259274
imports_USD_chg     86.325212  7580.942378  1.284231e+04       0.208383




### 📌 Why we created 5-year derived features (mean, std, change)

Banking crises do not only depend on the point-in-time value of a macroeconomic variable in a given year (e.g., GDP, inflation, consumption), but mainly on its **temporal dynamics**.
To capture this dimension, we built three types of features over the **previous 5 years**:

1. **Moving average (mean)**

   * Represents the **average level** of the variable over the past years.
   * Example: a persistently low GDP or consistently high inflation can indicate structural weaknesses.

2. **Standard deviation (std)**

   * Measures the **volatility** of the variable.
   * High values indicate macroeconomic instability (e.g., strongly fluctuating inflation), which is often linked to stress in the financial system.

3. **Change (percentage difference from 5 years earlier)**

   * Captures the **direction and intensity of the trend**.
   * Strong growth or sharp contraction can signal imbalances that increase the risk of a banking crisis.



-----
Here’s a clean English version of your GitHub project description and EDA results:

---

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

---

👉 Would you like me to also **summarize the statistical results table** (skewness, kurtosis, ranges) into a concise narrative, so that instead of raw stats you have insights directly usable in your GitHub README?




G
  
