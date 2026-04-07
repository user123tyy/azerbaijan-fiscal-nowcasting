# Azerbaijan Non-Oil Fiscal Balance Nowcasting

![Python](https://img.shields.io/badge/Python-3.11-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

## Overview

This project builds a time series forecasting model for Azerbaijan's 
non-oil fiscal balance using quarterly macroeconomic data from 2005–2023. 
It serves as the quantitative backbone of an ongoing academic article on 
fiscal data constraints in resource-dependent economies.

**Research question:** Can high-frequency oil price data improve 
nowcasts of Azerbaijan's non-oil fiscal balance beyond a simple ARIMA baseline?

---

## Repository Structure
azerbaijan-fiscal-nowcasting/
│
├── data/
│   ├── raw/        ← World Bank API + CBAR source data
│   └── clean/      ← Processed, analysis-ready datasets
│
├── notebooks/
│   ├── 01_data_collection.ipynb        ← API extraction + manual sources
│   ├── 02_eda_and_stationarity.ipynb   ← ADF tests, structural breaks
│   ├── 03_arima_baseline.ipynb         ← ARIMA model selection + diagnostics
│   └── 04_regression_with_oil.ipynb    ← Oil price as exogenous regressor
│
├── outputs/
│   ├── forecast_chart.png   ← Forecast vs actual visualization
│   └── model_results.csv    ← RMSE, MAE comparison table
│
├── requirements.txt
└── README.md
---

## Methodology

### Data Sources
| Variable | Source | Frequency |
|---|---|---|
| Government Revenue (% GDP) | World Bank API | Annual |
| Oil Price (Brent, USD/barrel) | World Bank API | Annual |
| Exchange Rate (AZN/USD) | CBAR | Annual |
| Non-Oil GDP Growth | SSCA Azerbaijan | Annual |

### Analytical Steps
1. **Data collection** — World Bank API via `wbgapi`, supplemented with CBAR data
2. **Stationarity testing** — Augmented Dickey-Fuller (ADF) test; first differencing where required
3. **Structural break identification** — 2015 oil crash, 2020 COVID shock
4. **ARIMA baseline** — Model selection via AIC/BIC; residual diagnostics
5. **Extended model** — Oil price added as exogenous regressor (ADL model)
6. **Evaluation** — RMSE and MAE comparison across models

---

## Key Findings

> Results will be updated as analysis progresses.

- Azerbaijan's fiscal revenues show strong structural dependence on oil price movements
- The 2015 devaluation represents a clear structural break requiring separate modelling
- ARIMA baseline RMSE: *[to be updated]*
- Oil-augmented model RMSE: *[to be updated]*

---

## Context & Motivation

Azerbaijan's State Oil Fund (SOFAZ) buffers oil revenue volatility, 
but non-oil fiscal balance forecasting remains underdeveloped due to 
data fragmentation across CBAR, SSCA, and the Ministry of Finance. 
This project documents those constraints empirically while building 
a reproducible forecasting pipeline.

This codebase supports the article:
> *"Fiscal Data Constraints in Azerbaijan: Barriers to Data Science 
> Model Deployment"* — Mammadov, M. (2025, working paper)

---

## Requirements
```bash
pip install -r requirements.txt
```
---

## Author

**Mammad Mammadov**  
BSc Economics, UNEC SABAH Program  
Baku, Azerbaijan  
memmedyasaroglu@gmail.com
## Data Status
- **World Bank API:** Successfully pulled GDP, Growth, and Inflation (2000-2024).
- **Known Gaps:** Government Revenue data is missing for 2000-2008. 
- **Next Steps:** Supplementing missing fiscal data using Central Bank of Azerbaijan (CBAR) statistical bulletins.