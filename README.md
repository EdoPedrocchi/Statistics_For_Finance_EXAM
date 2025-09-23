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

Analizzando i risultati dell'EDA del tuo dataset `df_features_clean`, ecco le principali osservazioni:

## **📊 PANORAMICA GENERALE**
- **Dataset pulito**: 7,915 righe × 43 colonne, 2.66 MB
- **Qualità eccellente**: 0% valori mancanti, 0% duplicati
- **Tutte variabili numeriche**: Dataset completamente quantitativo (finanza/economia)

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





  
