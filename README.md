# S&P 500 & NASDAQ: Empirical Return Analysis, Factor Models, and Volatility Modeling

A three-part empirical study of U.S. equity market returns covering descriptive analysis, Fama-French factor regressions, and GARCH-family volatility modeling across 26 years of daily and monthly data.

## Overview

This project analyzes the statistical properties of S&P 500 and NASDAQ Composite returns (2000–2026, ~6,500 daily observations), estimates factor models for Energy and Technology industry portfolios using Kenneth French data, and fits GARCH and GJR-GARCH models to capture time-varying volatility and asymmetric shock effects.

## Part A: Descriptive Analysis of Index Returns

Examines the return distributions of S&P 500 and NASDAQ Composite using 26 years of daily data.

**Key results:**
- Both indices show negative skewness and elevated excess kurtosis (10.6 for S&P 500, 6.8 for NASDAQ), confirming fat tails and leptokurtic distributions
- Correlation between the two indices is 0.91 — high but not perfect, with the gap driven by NASDAQ's tech concentration
- NASDAQ is more volatile (1.56% daily std dev vs 1.22% for S&P 500), consistent with its sector concentration
- Q-Q plots show the classic S-shaped deviation from normality in both tails for all return series
- 20-day moving average analysis reveals clear volatility clustering around the dot-com bust, 2008 crisis, and COVID crash

## Part B: Fama-French Factor Models

Runs one-factor, three-factor (FF3), four-factor (Carhart), and five-factor (FF5) regressions on Energy and HiTec industry portfolios using monthly Kenneth French data (2000–2025, 312 observations).

**Key results:**
- Energy loads positively on HML (+0.75) — classic value play. HiTec loads negatively (-0.60) — classic growth play
- HiTec has a market beta of 1.31 (amplifies market moves); Energy has 0.92 (slightly defensive)
- The market factor explains 78% of HiTec's returns but only 35% of Energy's — commodity and geopolitical drivers dominate Energy
- Momentum is significant for HiTec (negative loading, -0.12) but not for Energy
- In the five-factor model, HiTec shows a statistically significant alpha of 0.31% per month (p = 0.018), suggesting either a pricing anomaly or missing risk factors for tech stocks
- Energy's R-squared tops out at 49% even with five factors — more than half of its variation comes from forces outside standard factor models

## Part C: GARCH Volatility Modeling

Fits GARCH(1,1) and GJR-GARCH(1,1) models to S&P 500 and NASDAQ daily log returns, plus historical volatility analysis (Close-to-Close and Parkinson) on Applied Materials (AMAT) and Valero Energy (VLO).

**Key results:**
- GJR-GARCH dominates standard GARCH for both indices by all selection criteria (AIC, BIC, log-likelihood), confirming the leverage effect
- In the GJR-GARCH, the S&P 500's alpha drops to near zero while gamma = 0.177 — almost all volatility response comes from negative shocks
- Volatility persistence is near 1.0 for both indices (0.977 for S&P 500, 0.981 for NASDAQ), meaning shocks decay very slowly
- NASDAQ has higher baseline volatility (omega) but the S&P 500 has stronger asymmetry (higher gamma)
- Ljung-Box diagnostics confirm the GJR-GARCH adequately captures volatility dynamics for both indices

## How to Run

1. Clone this repository
2. Install dependencies: `pip install -r requirements.txt`
3. Place the required data files in a `data/` folder (see Data section below)
4. Run: `python main.py`

Charts are automatically saved to an `output/` folder.

### Data Requirements

- **Part A:** Daily price data for S&P 500 and NASDAQ Composite (Excel file with separate sheets)
- **Part B:** Kenneth French 10 Industry Portfolios (monthly), Fama-French 3-factor and 5-factor data, Momentum factor data (all available from [Kenneth French's data library](https://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html))
- **Part C:** Daily stock price data for Applied Materials (AMAT) and Valero Energy (VLO)

## Methodology

- **Returns:** Log returns used throughout for time-additivity; returns scaled by 100 for GARCH estimation
- **Factor models:** OLS regression via statsmodels; excess returns computed as portfolio return minus risk-free rate
- **Volatility estimators:** Close-to-Close (rolling 21-day standard deviation, annualized) and Parkinson (high-low range estimator)
- **GARCH estimation:** Maximum likelihood via the `arch` library; robust standard errors
- **Model selection:** AIC, BIC, and log-likelihood comparison; Ljung-Box residual diagnostics on standardized and squared standardized residuals

## Visualizations Generated

- Daily log returns with 20-day moving average overlay
- Return distribution histograms, KDE plots, and Q-Q plots (simple and log returns)
- Historical volatility time series (Close-to-Close vs Parkinson)
- Factor model comparison tables and regression outputs
- GARCH conditional volatility series
- ACF plots of standardized and squared residuals

## Built With

Python, pandas, numpy, scipy, matplotlib, seaborn, statsmodels, arch

## Author

**Bhawini Singh**
MS Quantitative Finance, Northeastern University (2026)

> **Full analysis write-up:** See [ANALYSIS.md](ANALYSIS.md) for the complete methodology, economic interpretation, and investment rationale behind each section.
