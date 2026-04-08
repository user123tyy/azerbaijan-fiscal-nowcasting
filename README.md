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

- Azerbaijan's government revenue fell sharply during the **2015 oil crash** 
  (from ~42% to ~34% of GDP), confirming strong fiscal-oil dependence
- **COVID-19 (2020)** caused a secondary fiscal contraction to ~35% of GDP
- ARIMA baseline captures the historical trend but underestimates 
  post-COVID revenue rebound
- ARIMAX + Oil Price tested as extended specification; at annual frequency, 
  oil price signal is already embedded in historical revenue data
- Structural breaks in 2015 and 2020 require explicit modelling — 
  a single ARIMA without break controls will systematically misforecast 
  during recovery phases

## Model Results

| Model | RMSE | MAE | Exogenous Variable |
|---|---|---|---|
| ARIMA(1,1,1) | 1.1816 | 0.9315 | None |
| ARIMAX(1,1,1) | 2.7121 | 2.3558 | Brent Oil Price (USD/barrel) |

Full results: [outputs/model_results.csv](outputs/model_results.csv)

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
