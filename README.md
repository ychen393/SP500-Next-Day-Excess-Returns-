# Market State Variables & Next-Day Excess Returns of the S&P 500

STAT 306 group project examining whether simple recent market-state variables help explain **next-day S&P 500 excess returns**.

## Overview

This project studies a classic empirical finance question: **do very recent market conditions contain useful information about what happens the next trading day?**

Using daily S&P 500 data and a short-term risk-free rate, we construct next-day excess returns and test whether three variables observed at the end of day \(t\) are associated with the excess return on day \(t+1\):

- current-day excess return
- 5-day rolling mean of excess returns
- 5-day rolling volatility of excess returns

The analysis is mainly **explanatory**, not a trading system. The goal is to see whether these simple market-state summaries contain any stable linear signal.

## Research Question

**Do recent market state variables help explain next-day S&P 500 excess returns?**

More specifically, we ask whether:

- **ExcessReturn_t** captures short-term momentum or reversal
- **RollingMean_5** reflects recent market direction
- **RollingVolatility_5** reflects recent instability or risk

## Data

The dataset was built from two public sources:

- **Yahoo Finance**: daily S&P 500 closing prices for ticker `^GSPC`
- **FRED**: 3-Month Treasury Bill Secondary Market Rate (`DTB3`) used as the risk-free rate

After feature construction, lag alignment, rolling-window calculations, and removal of incomplete rows, the final sample contains **1,053 complete daily observations** spanning **early 2022 to early 2026**.

## Variables

### Response
- **NextDayExcessReturn**: S&P 500 excess return on day \(t+1\)

### Predictors
- **ExcessReturn_t**: excess return observed on day \(t\)
- **RollingMean_5**: mean of excess returns over the most recent 5 trading days
- **RollingVolatility_5**: standard deviation of excess returns over the most recent 5 trading days

All predictors are constructed using only information available by the end of day \(t\), which avoids look-ahead bias.

## Methods

We estimate and compare four linear regression models:

1. **Model 1**: `NextDayExcessReturn ~ ExcessReturn_t`
2. **Model 2**: `NextDayExcessReturn ~ RollingMean_5`
3. **Model 3 (main model)**: `NextDayExcessReturn ~ RollingMean_5 + RollingVolatility_5`
4. **Model 4**: `NextDayExcessReturn ~ ExcessReturn_t + RollingMean_5 + RollingVolatility_5`

We then evaluate:

- coefficient significance
- adjusted \(R^2\)
- nested model comparisons
- multicollinearity using correlations and VIF
- diagnostic plots
- robustness checks using alternative rolling windows
- sensitivity to influential observations

## Main Findings

### 1. Current-day excess return is not useful in this linear setup
Model 1 shows no evidence that same-day excess return predicts next-day excess return.

### 2. The 5-day rolling mean shows the only repeated signal
The rolling mean has a **negative coefficient**, which suggests a mild **short-run reversal** effect rather than momentum.

### 3. Rolling volatility is not significant
Recent volatility does not appear to add meaningful independent linear explanatory power.

### 4. Overall explanatory power is extremely weak
Even the best model explains **far less than 1%** of the variation in next-day excess returns. From a practical perspective, this is the main takeaway.

### 5. The reversal signal is fragile
Robustness checks show that the weak negative rolling-mean effect depends on modeling choices and influential observations. Once the five most influential observations are removed, the apparent significance disappears.

## Conclusion

The project finds **little evidence that simple recent market-state variables strongly explain next-day S&P 500 excess returns**.

The most defensible conclusion is:

- there may be a **small and unstable short-run reversal pattern**
- but the effect is **too weak and too fragile** to support strong claims of useful day-ahead predictability in a simple linear model

In other words, **next-day excess returns remain very difficult to explain using only a few recent return-based summaries**.

## Repository Contents

Suggested structure for this repository:

```text
.
├── STAT_306_GitHub_Version_Notebook.ipynb   # main notebook with code + written explanation
├── STAT306 Project Report1.pdf              # final project report
├── README.md                                # project overview
```

## How to Run

1. Open the notebook:
   - `STAT_306_GitHub_Version_Notebook.ipynb`
2. Make sure the required Python packages are installed.
3. Run the notebook from top to bottom to reproduce the workflow.

## Possible Package Requirements

Depending on the notebook version, you may need:

- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `statsmodels`
- `yfinance`
- `pandas_datareader`

## Limitations

- The analysis uses a **simple linear framework**
- Financial returns often show **nonlinearity** and **time-varying volatility**
- The predictor set is intentionally narrow
- Results are mainly **in-sample**
- Statistical significance here does **not** imply trading usefulness

## Future Improvements

Possible extensions include:

- adding macroeconomic or cross-asset predictors
- using robust standard errors
- modeling volatility more directly with GARCH-type methods
- testing nonlinear models
- evaluating true out-of-sample forecasting performance

## Authors

- Winnie Chen
- Jeffrey Deng
- Wendy Xiao
- Jingyi Yang

## Acknowledgment

This repository is based on the STAT 306 group project report and supporting notebook developed for the course project.
