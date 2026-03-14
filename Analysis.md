# Analysis: S&P 500 & NASDAQ Empirical Return Analysis, Factor Models, and Volatility Modeling

A detailed walkthrough of the methodology, results, and economic interpretation across all three parts of the analysis.

---

## Part A: Descriptive Analysis of Index Returns

### Asset Selection

The two indices selected are the S&P 500 (SPX) and the NASDAQ Composite (IXIC). The S&P 500 tracks 500 large-cap U.S. companies across diverse sectors, serving as a broad benchmark for the overall U.S. equity market. The NASDAQ Composite is more heavily weighted toward technology and growth-oriented companies, making it a useful comparison to examine how sector concentration affects return behavior and risk characteristics.

### Central Tendency

Both indices have demonstrated positive average daily returns over the last 26 years, with only minor differences between them. For both, the median is slightly higher than the mean, which may be due to occasional large negative returns pulling the mean downward without affecting the median as much. The median can be seen as a better reflection of a typical trading day, while the mean captures the long-run compounding effect and incorporates the impact of extreme events.

### Dispersion

The NASDAQ has a standard deviation of 1.56% compared to 1.22% for the S&P 500. This demonstrates higher volatility for NASDAQ since it is mainly concentrated in technology stocks which are more sensitive to changes. The S&P 500 is more diversified across sectors from utilities to healthcare, which dampens its overall volatility. This shows that concentration increases risk — which is why NASDAQ has a larger maximum gain but also a slightly larger maximum loss.

### Tail Behavior

The S&P 500 shows a slight negative skew (-0.12), while the NASDAQ has a small positive skew (0.10). The S&P 500's negative skew means its returns have a longer left tail, so big losses are a bit more likely than big gains. This is linked to the leverage effect: as stock prices drop, companies get more leveraged (their debt-to-equity goes up), which ramps up risk and makes further declines more likely.

The NASDAQ's tiny positive skew is unusual for a stock index. This probably comes from rare but massive jumps in tech stocks — the late '90s dot-com mania or the post-COVID rallies — where a handful of names soar and stretch the right tail.

Both indices have very high excess kurtosis: 10.59 for the S&P 500 and 6.79 for the NASDAQ. These values mean the return distributions are far fatter in the tails and have a sharper peak than normal. The S&P 500's kurtosis is even higher, so compared to its own spread, it gets hit with more outlier days than the NASDAQ.

### Correlation and Co-movement

The correlation between the two indices is 0.91. They move with the same big picture drivers: interest rates, GDP numbers, inflation, and many large-cap stocks appear in both indices. But since the correlation isn't exactly 1.0, there's still a bit of diversification from holding both — but not much. The 9% that isn't shared mostly comes from the NASDAQ being tech-heavy. For actual diversification, investors need to look beyond U.S. large caps entirely.

### Moving Average Analysis

The 20-day moving averages reveal clear volatility clustering in both series. Large swings around trading days 0–500 correspond to the dot-com bust, the spike near day 2000 aligns with the 2008 financial crisis, and sharp movements around day 5000 match the COVID-19 crash. During these events, the MA moves sharply as well, showing sustained periods of negative or positive momentum rather than isolated bad days.

The NASDAQ MA tends to have slightly larger peaks and dips, but the two almost never move in opposite directions — visually confirming the 0.91 correlation.

### Distribution Analysis

The histograms, KDE plots, and Q-Q plots all tell the same story: normality is strongly rejected for both indices. The KDE curves are noticeably taller and sharper at the center than the normal overlay, with tails that sit above the normal reference. The Q-Q plots show the classic S-shaped deviation — more extreme negative returns than predicted on the left, and more extreme positive returns on the right.

The practical implication is significant: standard models like mean-variance and Black-Scholes assume normally distributed returns. A normal model would underestimate returns near zero (where most days fall) and severely underestimate extreme tail events. A Gaussian VaR at the 99% confidence level would understate the true risk.

Simple returns and log returns are nearly indistinguishable at the daily frequency, since ln(1+r) ≈ r when r is small.

---

## Part B: Fama-French Factor Models

### Industry Selection

Energy and HiTec (High Technology) were chosen because they represent very different sectors. Energy is a traditional, cyclical industry tied to commodity prices and physical infrastructure, while HiTec covers technology and related firms that tend to be more growth-oriented and sensitive to innovation cycles.

### One-Factor Model (CAPM)

Energy has a beta of 0.92 (slightly below 1), meaning it moves roughly in line with the market but with a bit less sensitivity. This makes sense for a mature, capital-heavy sector partly driven by oil prices rather than purely by broad market movements.

HiTec has a beta of 1.31, well above 1, meaning it amplifies market movements. A 1% market move translates to roughly a 1.3% move in HiTec. This is expected for a sector sensitive to economic conditions, investor sentiment, and growth expectations.

Neither portfolio shows a significant alpha, meaning the one-factor model accounts for average excess returns reasonably well.

The key difference is R-squared: HiTec at 0.78 versus Energy at 0.35. The market factor alone explains 78% of HiTec's returns but only 35% of Energy's. The remaining 65% of Energy's variation comes from factors outside the broad market — most likely commodity prices, supply dynamics, and geopolitical events.

### Three-Factor Model (Fama-French)

Adding SMB and HML dramatically improves the Energy model (R-squared jumps from 0.35 to 0.48). The big driver is the HML loading of +0.75 — Energy behaves like a classic value portfolio. Energy companies tend to have high book-to-market ratios. SMB is not significant for Energy.

For HiTec, the three-factor R-squared is 0.875 (up from 0.78). The strong negative HML loading of -0.60 confirms HiTec behaves like a growth portfolio — the opposite of value. Tech companies have low book-to-market ratios because their value comes from future growth expectations. The small positive SMB loading suggests a slight tilt toward smaller firms within tech.

### Four-Factor Model (Carhart)

Adding momentum barely changes anything for Energy (momentum loading 0.07, p = 0.29; R-squared unchanged). Energy stocks are driven by commodity cycles and value characteristics, not by price momentum.

For HiTec, momentum is significant (loading -0.12, p = 0.00; R-squared improves from 0.875 to 0.882). The negative momentum loading means that when past winners outperform past losers, HiTec tends to lag slightly — reflecting periodic reversals in high-growth tech stocks.

### Five-Factor Model

The five-factor model adds RMW (profitability) and CMA (investment). For HiTec, RMW is the standout finding: a loading of -0.42 (highly significant), meaning HiTec behaves like stocks with weak current profitability. This fits the profile of tech companies that prioritize reinvestment over earnings. CMA is -0.15 (significant), indicating a tilt toward aggressive investors.

The most notable result: HiTec's alpha becomes statistically significant at 0.31% per month (p = 0.018). Across the one-factor, three-factor, and four-factor models, alpha was never significant for either portfolio. This could suggest either that the five-factor model is missing something about tech stock risk, or that the sector has genuinely outperformed its measured risk exposures over this period.

For Energy, the five-factor model only marginally improves R-squared (from 0.48 to 0.49). Even five factors leave more than half of Energy's variation unexplained — commodity-driven and geopolitical forces outside the standard model remain dominant.

### Factor Exposures Summary

The factor exposures paint opposite pictures. Energy loads positively on HML, RMW, and CMA (value, profitable, conservative). HiTec loads negatively on all three (growth, low profitability, aggressive investment). These are fundamentally different businesses, and the factor loadings capture that clearly.

---

## Part C: GARCH Volatility Modeling

### Historical Volatility (AMAT and VLO)

Both Applied Materials (AMAT) and Valero Energy (VLO) show volatility that is clearly not constant over time. It clusters in bursts — rising sharply during market stress and gradually settling back down. The highest spikes correspond to the dot-com bust (2000–2002), the 2008 financial crisis, and the COVID crash (2020).

The Parkinson estimator (using intraday high-low range) tracks Close-to-Close volatility closely but tends to be smoother and slightly lower in magnitude. This is expected because the Parkinson estimator captures intraday movement more efficiently and is less noisy than relying solely on closing prices.

Both stocks have similar average annualized volatility (roughly 30–38% depending on the measure). AMAT has a higher standard deviation of volatility (0.21 vs 0.16 for VLO), meaning its volatility itself swings more between calm and turbulent periods. The medians are lower than the means for both, confirming right-skewed volatility distributions where occasional large spikes pull the average up.

### GARCH(1,1) Results

For the S&P 500: alpha = 0.122, beta = 0.859, persistence = 0.981. For NASDAQ: alpha = 0.103, beta = 0.884, persistence = 0.986. Both show very high persistence — once volatility rises, it decays very slowly. All parameters are highly significant.

### GJR-GARCH(1,1) Results

This is where the asymmetry becomes clear. For the S&P 500: alpha drops to nearly zero while gamma = 0.177. This means positive returns barely affect future volatility — almost the entire volatility response comes from negative shocks. For NASDAQ: alpha = 0.005, gamma = 0.144. The same pattern but slightly less extreme.

### Model Selection

GJR-GARCH dominates standard GARCH for both indices by all three criteria:

| Index | Model | Log-Likelihood | AIC | BIC |
|-------|-------|---------------|-----|-----|
| S&P 500 | GARCH(1,1) | -8,977 | 17,963 | 17,990 |
| S&P 500 | GJR-GARCH(1,1) | -8,851 | 17,712 | 17,746 |
| NASDAQ | GARCH(1,1) | -10,674 | 21,357 | 21,384 |
| NASDAQ | GJR-GARCH(1,1) | -10,579 | 21,169 | 21,203 |

The AIC improvement of ~250 points for S&P 500 and ~188 points for NASDAQ is very large in information criterion terms, confirming the asymmetry term captures genuinely important dynamics.

### Cross-Index Comparison

The NASDAQ has a higher omega (higher baseline volatility) and slightly higher persistence (volatility stays elevated longer). The S&P 500 has a stronger asymmetry effect (higher gamma) — negative shocks increase volatility more sharply. Both indices clearly show the leverage effect, and both have very persistent volatility.

### Residual Diagnostics

Ljung-Box tests on the GJR-GARCH models show insignificant autocorrelation in both standardized and squared standardized residuals at the 5% level for both indices. The standard GARCH(1,1) fails for NASDAQ (significant autocorrelation in squared residuals), providing direct evidence that incorporating asymmetry captures the missing volatility component. ACF plots confirm these findings visually.

---

## Key Takeaways

1. **Normality is strongly rejected** for all U.S. equity return series examined. Fat tails and excess kurtosis are pervasive, and any risk model assuming Gaussian returns will underestimate extreme event probabilities.

2. **Factor exposures define sector character.** Energy is a value play driven by commodity cycles; Technology is a growth play driven by innovation and sentiment. The standard factor models explain nearly 90% of HiTec's returns but less than 50% of Energy's.

3. **The leverage effect is real and economically large.** GJR-GARCH captures this asymmetry — negative shocks drive almost all of the volatility response for U.S. equity indices. Standard GARCH ignores this and is clearly rejected by model selection criteria.

4. **Volatility is highly persistent.** Shocks decay very slowly (persistence near 1.0), meaning elevated volatility after a crisis should be expected to last, not revert quickly.

---

*Author: Bhawini Singh | MS Quantitative Finance, Northeastern University (2026)*
