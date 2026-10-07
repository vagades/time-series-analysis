# Time Series Analysis

Homework projects for the **Time Series Analysis** course at Lomonosov Moscow State University (CMC faculty, semester 7, fall 2026). New assignments are added as the course goes on.

| # | Project | Methods |
|---|---------|---------|
| 1 | [Holt-Winters vs SARIMA: retail demand forecasting](hw1-holt-winters-sarima) | Decomposition, exponential smoothing, ACF/PACF, stationarity tests, ARIMA/SARIMA |

## HW1: Holt-Winters vs SARIMA

Sales of one item (`item = 29`) from the [Store Item Demand Forecasting](https://www.kaggle.com/competitions/demand-forecasting-kernels-only/data) dataset (10 stores, 2013–2017) are analysed as **four series**:

| Series | Aggregation | Frequency | Seasonal period |
|--------|-------------|-----------|-----------------|
| A | store 1 | daily | 7 |
| B | store 1 | monthly | 12 |
| C | sum over 10 stores | daily | 7 |
| D | sum over 10 stores | monthly | 12 |

The same steps are applied to each series:
1. Exploratory analysis: trend, seasonality, coefficient of variation by year
2. Naive (classical) additive and multiplicative decomposition
3. Holt-Winters exponential smoothing
4. ACF / PACF and stationarity tests (ADF, KPSS)
5. ARIMA / SARIMA order selection and residual diagnostics
6. Forecast comparison on a hold-out set by RMSE, MAE and MAPE

### Results (hold-out set)

| Series | Holt-Winters RMSE / MAPE | SARIMA RMSE / MAPE | Better |
|--------|--------------------------|--------------------|--------|
| A: daily, store 1 | 9.72 / 15.76 % | 9.83 / 15.49 % | ≈ tie |
| B: monthly, store 1 | 73.23 / 2.73 % | **59.87 / 2.15 %** | SARIMA |
| C: daily, all stores | **31.05 / 4.48 %** | 99.90 / 14.92 % | Holt-Winters |
| D: monthly, all stores | 896.66 / 3.40 % | **583.63 / 2.29 %** | SARIMA |

**Takeaway:** no single model wins everywhere. Holt-Winters is better on the long daily series, and SARIMA is better on the short monthly ones, so the model has to be chosen per series.

### Files
- `hw1_time_series.ipynb`: the full analysis (in Russian)
- `hw1_time_series.pdf`: the notebook exported to PDF

To reproduce, download `train.csv` from Kaggle, rename it to `data_hw_1.csv` and place it next to the notebook.

## Stack
Python, pandas, NumPy, statsmodels, pmdarima, Matplotlib
