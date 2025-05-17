
# 90-Day Revenue Forecasting with ARIMA Time Series Modeling  
**Author: May Cooper**

## Overview

This project uses ARIMA time series modeling to forecast daily revenue over a 90-day horizon, based on two years of historical business data. By uncovering temporal patterns and short-term trends, this project demonstrates how classical time series forecasting can support financial planning and resource allocation in a data-informed way. The methodology includes transforming the data for stationarity, parameter selection using AIC scoring, and comprehensive diagnostics to validate model assumptions.

### What is ARIMA?

ARIMA (AutoRegressive Integrated Moving Average) is a statistical modeling technique used for analyzing and forecasting time series data. It combines three components:
- **AR (AutoRegressive)**: captures relationships between an observation and prior observations.
- **I (Integrated)**: applies differencing to remove trends and achieve stationarity.
- **MA (Moving Average)**: accounts for past error terms to improve forecasting accuracy.

---

## Project Objectives

- **Primary Goal**: Forecast daily revenue for the next 90 days using a time series model.
- **Business Application**: Support budgeting, staffing, and operational planning by anticipating revenue patterns.
- **Technical Process**: Test for stationarity, perform differencing, use ACF/PACF plots, conduct ARIMA model tuning, and validate with RMSE and diagnostics.

---

## Research Question

How accurately can daily revenue be forecasted over a short-term horizon using ARIMA time series modeling?

---

## Dataset Summary

- Total records: 731 days of consecutive revenue data.
- No missing days or gaps in the sequence.
- First-order differencing was required to make the data stationary.

### Sample of the Dataset

| DayIndex  | DailyRevenueUSD | RevenueChange |
|-----------|------------------|----------------|
| 704       | 15.7097          | 0.1457         |
| 34        | 3.0424           | 0.5995         |
| 301       | 9.6471           | -0.4882        |
| 457       | 13.4186          | 0.9228         |
| 634       | 9.9462           | -0.0919        |

---

## Exploratory Data Analysis

### 1. Raw Revenue Time Series  
![image](https://github.com/user-attachments/assets/d2e4efff-823d-415d-bf17-737c941fbffc)
Revenue trends upward with variability over time, confirming non-stationarity. There are no visible gaps, and the trend justifies differencing.

### 2. ACF and PACF Plots of Differenced Series  
![image](https://github.com/user-attachments/assets/753d80bd-1ea3-43f5-8396-b8cdcb0b05e8)
The sharp drop in autocorrelation at lag 1 and lack of significant PACF spikes supports ARIMA(1,0,0) as the best-fitting model.

### 3. Smoothed Trend  
![image](https://github.com/user-attachments/assets/ebfb2048-79e5-4374-a7f2-be69b3dc0de8)
The trend confirms seasonally independent but steadily increasing revenue, reinforcing the need for differencing.

### 4. Spectral Density  
![image](https://github.com/user-attachments/assets/fc17e639-d143-4ca4-aa38-f6175878abed)
Strong low-frequency components suggest long-term cycles but no strong repeating seasonal peaks. ARIMA is appropriate without seasonal terms.

### 5. Seasonal Decomposition  
![image](https://github.com/user-attachments/assets/ff806753-77f7-4543-b863-887a8260aa26)
Trend and seasonality were isolated. Residuals appear random, suggesting a good decomposition.

### 6. Residuals of Decomposition  
![image](https://github.com/user-attachments/assets/4c6367c9-ede3-436a-a51e-56869e217d1f)
Residuals show no visible structure—this randomness confirms that the primary trend and seasonality were effectively removed.

---

## ARIMA Model Training

- **Stationarity**:
  - Original p-value (ADF): 0.32 → Non-stationary.
  - Differenced p-value (ADF): 0.00 → Stationary confirmed.

- **Train/Test Split**:  
  - Train: 584 days  
  - Test: 146 days

- **Model Fit**:  
  - Chosen model: **ARIMA(1,0,0)**  
  - AIC: 773.89  
  - Ljung-Box Test p = 0.96 (residuals uncorrelated)  
  - RMSE on test set: **0.57**

### 7. Model Diagnostics  
![image](https://github.com/user-attachments/assets/5cad3926-c14c-4702-97c1-a02d9141a387) 
- Residuals appear normally distributed.  
- Q-Q plot shows good alignment with normality.  
- No significant autocorrelation in the correlogram.

---

## Forecasting Results

### 8. ARIMA Forecast Plot  
![image](https://github.com/user-attachments/assets/b67103f5-4f9a-4fac-b1e6-4ffe91541ea4)
The forecast aligns well with the historical trend during the test window. Confidence intervals widen as expected over time, reflecting increasing uncertainty further into the forecast horizon.

---

## Forecast Table (First 3 Points)

| Day | Forecast | Lower CI | Upper CI |
|-----|----------|----------|----------|
| 732 | 13.46    | 12.54    | 14.37    |
| 740 | 13.67    | 4.54     | 22.79    |
| 821 | 15.56    | -77.03   | 108.14   |

---

## Interpretation and Insights

- The ARIMA(1,0,0) model effectively captured short-term temporal structure.
- Differencing was key to achieving stationarity.
- ACF/PACF and diagnostics validated model assumptions.
- Residuals were well-behaved, and no seasonality was detected.
- Forecasts are most reliable in the early test window; uncertainty expands with longer horizons.

---

## Tools and Technologies

- **Python** – Analysis and modeling
- **Pandas, NumPy** – Data transformation
- **Statsmodels** – ARIMA fitting and diagnostics
- **Matplotlib, Seaborn** – Visualization

---

## Conclusion

This project demonstrates how ARIMA can be used to reliably forecast daily revenue over a 90-day period based on historical financial trends. Through careful preparation—including stationarity testing, differencing, model selection, and diagnostics—the ARIMA(1,0,0) model proved to be a statistically sound choice with interpretable parameters and low forecast error (RMSE = 0.57).

The resulting forecasts offer tangible value for short-term decision-making. For example, anticipated revenue trajectories can guide operational planning, staffing levels, inventory procurement, or budget forecasting for upcoming quarters. The inclusion of confidence intervals also enables organizations to quantify forecast risk and prepare for potential fluctuations.

While ARIMA is a univariate model that does not account for external drivers, it provides a strong baseline. Future iterations could incorporate exogenous variables (e.g., promotions, holidays, or economic indicators) using models like SARIMAX. Additionally, if periodic fluctuations are more pronounced in future data, seasonal ARIMA (SARIMA) could be employed to better capture cyclical behavior.

In summary, this project highlights the utility of classical time series forecasting methods for revenue modeling and lays a foundation for more advanced predictive strategies as business complexity grows.

