# Temperature Anomaly & CO₂ Analysis (1880–2025)

**Tools:** Python · pandas · NumPy · scipy · statsmodels · matplotlib · seaborn  

**Data:** NASA GISS Surface Temperature Analysis · NOAA Mauna Loa CO₂ Observatory  

**Coverage:** 145+ years of global temperature anomalies · 1958–2025 CO₂ records

## Overview

Analyses long-term global temperature anomalies and their relationship with atmospheric CO₂ levels to identify climate trend acceleration. The analysis tests whether post-1980 warming represents a **structural break** from historical patterns, and forecasts temperature anomalies to 2050 using multiple modelling approaches.

## Key Findings

- **Post-1980 structural break confirmed:** mean temperature anomaly rose ~0.70°C relative to the 1900–1980 baseline — statistically significant (ANOVA p < 0.05, Tukey HSD)
- **No significant difference** between pre-1900 and 1900–1980 periods — the acceleration is distinctly post-1980
- **Warming rate post-1980** is substantially steeper than any prior period (linear regression by era)
- **Strong CO₂–temperature correlation** — higher CO₂ concentration bands consistently correspond to higher mean temperature anomalies
- **Three forecast models agree** on continued warming to 2050; CO₂-based projection shows the steepest trajectory


## Methodology

| Step | Approach |
|---|---|
| Data cleaning | Replaced invalid CO₂ values (-99.99), coerced types, dropped nulls |
| Period segmentation | Pre-1900 · 1900–1980 · Post-1980 |
| Statistical testing | One-way ANOVA + Tukey HSD post-hoc across three periods |
| Trend analysis | Linear regression by era (slope = °C/decade) + 10-year rolling mean |
| CO₂ correlation | Pearson correlation + linear regression (CO₂ → temperature) + residual analysis |
| Forecasting | ARIMA(1,2,1) · linear extrapolation · CO₂-based projection · quadratic regression |
| Validation | Train/test split at 2015 — ARIMA forecast vs actuals (2015–2025) |


## Forecasting approaches compared

| Model | Basis | Horizon |
|---|---|---|
| ARIMA(1,2,1) | Time series structure (AIC-selected) | 2025–2035 |
| Linear extrapolation | Historical trend slope | 2025–2050 |
| CO₂-based projection | CO₂ trend → temperature regression | 2025–2050 |
| Quadratic regression | Non-linear acceleration fit | 2025–2050 |

All four models are compared on a single chart. ARIMA(1,2,1) selected over (1,1,1) by AIC; validated on 2015–2025 holdout data.


## Data sources

| Dataset | Source | Notes |
|---|---|---|
| `GLB.Ts+dSST.csv` | NASA GISS | Global surface temperature anomalies, J–D annual mean |
| `co2_mm_mlo.csv` | NOAA / Mauna Loa | Monthly atmospheric CO₂ (ppm), 1958–present |

Both datasets are publicly available and not included in this repository.


## Limitations

- Linear and quadratic forecasts assume continuation of historical trends — no policy or feedback mechanisms modelled
- CO₂-based projection assumes a linear CO₂ growth rate, which may understate future accumulation
- ARIMA captures time series structure only — not physical climate dynamics
- Analysis uses global mean anomaly; regional variation is not examined
