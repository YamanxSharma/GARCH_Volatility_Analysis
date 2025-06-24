# S&P 500 GARCH(1,1) Volatility Analysis

## Project Overview

This repository contains a quantitative analysis of S&P 500 (^GSPC) daily logarithmic returns, focusing on modeling and forecasting volatility using the GARCH(1,1) model. The project demonstrates data retrieval, preliminary data analysis, GARCH model fitting with both normal and Student's t-distributions, and a comparison of GARCH forecasts against a simple rolling standard deviation.

## Contents

* `GARCH.pdf`: A detailed report (or notebook export) outlining the steps and results of the GARCH analysis.
* `garch_analysis.py` (or `garch_analysis.ipynb`): The Python code used for data retrieval, analysis, model fitting, and forecasting.

## Methodology

The analysis involves the following key steps:

1.  [cite_start]**Data Retrieval**: Daily historical price data for the S&P 500 (^GSPC) index from 2016-01-01 to 2025-05-31 was retrieved using the `yfinance` library.
2.  [cite_start]**Logarithmic Returns Calculation**: Daily logarithmic returns were calculated from the 'Adj Close' or 'Close' price column.
3.  [cite_start]**Volatility Clustering Visualization**: The daily log returns were plotted to visually observe volatility clustering, a common characteristic of financial time series.
4.  [cite_start]**Stationarity Check (Optional)**: An Augmented Dickey-Fuller (ADF) test was performed on the returns to check for stationarity, confirming a low p-value indicating stationarity.
5.  [cite_start]**Rolling Standard Deviation Calculation**: A 20-day rolling standard deviation, annualized by multiplying with $\sqrt{252}$, was calculated as a basic measure of volatility. [cite_start]This was also plotted to visualize historical volatility.
6.  **GARCH(1,1) Model Specification and Fitting**:
    * [cite_start]A GARCH(1,1) model with a 'Constant' mean and 'Garch' volatility was specified using the `arch` library.
    * [cite_start]The model was initially fitted assuming 'normal' (Gaussian) errors.
    * [cite_start]A second GARCH(1,1) model was fitted using a Student's t-distribution (`dist='t'`) to account for fat tails, which are often observed in financial returns.
    * [cite_start]Conditional volatility was extracted and plotted for both models.
7.  **Residual Analysis**:
    * [cite_start]Standardized residuals were obtained from the GARCH model.
    * [cite_start]The distribution of standardized residuals was plotted to assess their properties.
    * [cite_start]Autocorrelation Function (ACF) plots of both standardized residuals and squared standardized residuals were generated to check for any remaining autocorrelation, which would indicate uncaptured dependencies.
    * [cite_start]Ljung-Box tests were performed on standardized residuals and squared standardized residuals to formally test for autocorrelation, with the aim of having high p-values to suggest white noise.
8.  **Rolling Volatility Forecasting and Comparison**:
    * [cite_start]A rolling window of 250 days was used to train the GARCH(1,1) model.
    * [cite_start]One-step-ahead forecasts of annualized volatility were generated.
    * [cite_start]Realized volatility was proxied by the absolute value of returns, annualized.
    * [cite_start]The GARCH forecasts were compared against the rolling standard deviation and the realized volatility proxy.
    * [cite_start]Performance metrics such as Mean Absolute Error (MAE), Mean Squared Error (MSE), Root Mean Squared Error (RMSE), and correlation were calculated for both GARCH(1,1) and rolling standard deviation forecasts to evaluate their predictive accuracy.

## Libraries Used

* [cite_start]`yfinance` 
* [cite_start]`pandas` 
* [cite_start]`numpy` 
* [cite_start]`matplotlib.pyplot` 
* [cite_start]`arch` 
* [cite_start]`sklearn.metrics` 
* [cite_start]`statsmodels.graphics.tsaplots` 
* [cite_start]`statsmodels.stats.diagnostic` 
* [cite_start]`statsmodels.tsa.stattools` 

## Results and Conclusions

* The plot of daily log returns clearly indicates volatility clustering, where periods of high volatility are followed by periods of high volatility, and vice versa.
* The ADF test confirmed the stationarity of the log returns.
* The GARCH(1,1) model effectively captures the time-varying volatility of the S&P 500. The coefficients `alpha[1]` and `beta[1]` are statistically significant.
* The sum of $\alpha[1]$ and $\beta[1]$ being 0.98 for the Normal distribution GARCH model indicates highly persistent volatility.
* While the GARCH(1,1) model with a Student's t-distribution might be more appropriate for financial data due to fat tails, the provided output for the Student's t-distribution model summary seems to be the same as the Normal distribution one in the current document.
* The Ljung-Box test results on standardized residuals and squared standardized residuals had low p-values, suggesting some remaining autocorrelation, which might indicate that the GARCH(1,1) model could be further improved (e.g., by trying higher orders or different distributions).
* Comparing the GARCH(1,1) forecasts to the rolling standard deviation, the rolling standard deviation exhibited lower MAE, MSE, and RMSE, and a higher correlation with realized volatility in this specific comparison. This might suggest that for certain forecasting horizons or data characteristics, simpler models can sometimes outperform more complex ones, or that the proxy for realized volatility or the model specification could be refined.

## Usage

To reproduce this analysis:

1.  Clone this repository:
    `git clone https://github.com/YourGitHubUsername/GARCH_Volatility_Analysis.git`
2.  Navigate to the project directory:
    `cd GARCH_Volatility_Analysis`
3.  Install the required libraries:
    `pip install yfinance pandas numpy matplotlib arch scikit-learn statsmodels`
4.  Run the Python script (or Jupyter Notebook):
    `python garch_analysis.py` (or open `garch_analysis.ipynb` in Jupyter)

## Author

[Yaman Sharma]
[www.linkedin.com/in/yaman-sharma-164b68244]
[https://github.com/YamanxSharma/YamanxSharma]

## License

This project is open-source and available under the [e.g., MIT License].
