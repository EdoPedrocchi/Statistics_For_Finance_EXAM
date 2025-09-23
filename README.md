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





----------------------------risultato eda----
analizza questi risultati dell'eda

```


1. INFORMAZIONI GENERALI DEL DATASET
--------------------------------------------------
Forma del dataset: (7915, 43)
Numero di righe: 7,915
Numero di colonne: 43
Memoria utilizzata: 2.66 MB

2. TIPI DI DATI E VALORI MANCANTI
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

3. PRIME 5 RIGHE DEL DATASET
--------------------------------------------------
     BankingCrisis  rGDP_pc_mean5y  rGDP_pc_std5y  rGDP_pc_chg  \
468            0.0    393347.61875   14409.449451    -0.027724   
469            0.0    395739.53125   14898.049072     0.044744   
470            0.0    404236.49375   14694.038733    -0.004052   
471            0.0    411540.28125    9476.005675    -0.081872   
472            0.0    408485.74375   14937.420596    -0.083050   

     rGDP_USD_mean5y  rGDP_USD_std5y  rGDP_USD_chg  cons_GDP_mean5y  \
468     14869.842773      878.371563         0.002        71.201187   
469     15098.413574      850.491728         0.081        71.203560   
470     15491.258594     1146.358662         0.031        71.231464   
471     16210.385937     1100.707588        -0.050        71.260855   
472     16580.593945      804.927382        -0.052        71.223094   

     cons_GDP_std5y  cons_GDP_chg  ...  cons_USD_chg  inv_USD_mean5y  \
468        0.030977      0.000408  ...      0.022590      956.150299   
469        0.022286      0.001501  ...      0.227543      972.424052   
470        0.058701      0.000887  ...      0.122401     1037.599625   
471        0.083087     -0.004821  ...     -0.268078     1106.445911   
472        0.132657     -0.001042  ...     -0.039893     1120.821582   

     inv_USD_std5y  inv_USD_chg  finv_USD_mean5y  finv_USD_std5y  \
468      33.300181     0.025798       919.051544       32.008105   
469      36.728138     0.227026       934.693868       35.303063   
470     133.756215     0.120592       997.340591      128.566398   
471     192.657985    -0.273079      1063.515637      185.182808   
472     178.613119    -0.035542      1077.333508      171.682905   

     finv_USD_chg  imports_USD_mean5y  imports_USD_std5y  imports_USD_chg  
468      0.025798         1128.214111         160.659350         0.025157  
469      0.227026         1212.879663         141.960331         0.229102  
470      0.120592         1340.057153         207.170148         0.123158  
471     -0.273079         1494.472046         262.928378        -0.281793  
472     -0.035541         1511.764062         245.723358        -0.022431  

[5 rows x 43 columns]

4. ULTIME 5 RIGHE DEL DATASET
--------------------------------------------------
       BankingCrisis  rGDP_pc_mean5y  rGDP_pc_std5y  rGDP_pc_chg  \
56884            0.0     6840.975488     477.548078     0.017462   
56885            0.0     7108.244043     393.956405     0.014243   
56886            0.0     7329.759961     286.789232    -0.002413   
56887            0.0     7462.063379     218.705187     0.005940   
56888            0.0     7573.955566     107.286430     0.003984   

       rGDP_USD_mean5y  rGDP_USD_std5y  rGDP_USD_chg  cons_GDP_mean5y  \
56884     12616.601758     1543.025942      0.050575        61.114182   
56885     13546.531445     1440.614755      0.046933        60.496479   
56886     14423.902344     1290.605039      0.029204        59.994283   
56887     15155.656055     1171.510018      0.037551        60.018166   
56888     15868.444922      992.759615      0.035259        60.002950   

       cons_GDP_std5y  cons_GDP_chg  ...  cons_USD_chg  inv_USD_mean5y  \
56884        1.331044      0.005261  ...      0.105403     6513.524219   
56885        1.234915      0.002035  ...     -0.030047     7218.104492   
56886        0.912258      0.030797  ...     -0.193233     8106.536621   
56887        0.954150     -0.013172  ...     -0.026179     8714.612402   
56888        0.942225     -0.113919  ...      0.093536     8773.786328   

       inv_USD_std5y  inv_USD_chg  finv_USD_mean5y  finv_USD_std5y  \
56884    1341.902090     0.179339      5478.632520      897.251619   
56885    1816.965025    -0.024392      5870.892090     1171.970347   
56886    1374.802232    -0.016651      6711.501855     1200.643059   
56887     786.164603    -0.119202      7296.074023     1004.619999   
56888     698.250703     0.324428      7510.913574      919.489776   

       finv_USD_chg  imports_USD_mean5y  imports_USD_std5y  imports_USD_chg  
56884      0.188154         6368.287109        1919.473512         0.245737  
56885      0.164478         7516.164551        2774.031432        -0.095033  
56886     -0.030346         8721.088477        2173.292752        -0.105177  
56887     -0.065342         9402.238379        1360.199933        -0.107709  
56888      0.314999         9505.847852        1196.757504         0.168926  

[5 rows x 43 columns]

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

6. STATISTICHE DESCRITTIVE - VARIABILI CATEGORICHE
--------------------------------------------------
Nessuna variabile categorica trovata.

7. ANALISI DEI DUPLICATI
--------------------------------------------------
Numero di righe duplicate: 0
Percentuale di duplicati: 0.00%

8. GRAFICI DI DISTRIBUZIONE DELLE VARIABILI NUMERICHE
```





  
