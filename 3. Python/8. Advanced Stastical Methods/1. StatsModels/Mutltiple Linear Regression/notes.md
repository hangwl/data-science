# Multi Linear Regression

No visual way to represent data after 3 dimensions.

Same intuition. We want to minimize SSE.

How to determine optimal number of variables to use? With each additional variable, explanatory power may increase or stay the same.
    See adjusted R-squared. (adj. R^2 < R^2 as it penalizes excessive use of variables)
        See p-value for additional variables. High p-value -> cannot reject null hypothesis at the (p-value %) level of significance. Drop insignificant variables.

F-test (Test for significance of MLR model)
    Null: All betas are zero -> None of the independent variables are significant
    See Prob (F-statistic) for p-value - to reject the null at 5% (0.05) level of significance
    The lower the F-statistic, the closer to a non-significant model

# Regression Assumptions (OLS) - MUST NOT BE VIOLATED FOR MODEL TO HOLD

1. Linearity - each independent variable is multiplied by a coefficient
    Plot 2-dimensional scatter plot to check for linearity
    Transform relationship
    Consider non-linear models

2. No Endogeneity - Covariance of Error and Independent variables (X'es) are zero, for any error or x
    Could arise due to omitted variable bias (OVB) - omitted variable is correlated with both independent variable, and dependent variable
        Reflected in the Error Term (Systemic error becomes apparent)
        Hard to fix. Rethink model, expand sample data points

3. Normality and Homoscedasticity - Errors are normally distributed (0 mean) with equal variance among errors
    t-tests and F-tests work because we have assumed normality
        CLT should apply for large samples
    To prevent heteroskedasticity:
        - can look for OVB, outliers
        - try log-transformation
          - log y = b0 + b1x1 - as X increases by 1 unit, Y increases by b1 percent
          - log y = b0 + b1(logx1) - as X increases by 1 percent, Y increases by b1 percent (elasticity)

4. No auto(serial)correlation - Covariance of any 2 error terms are zero.
    Cannot be relaxed.
    Highly unlikely to find in cross-sectional data, but very common in Time-Series data.
    How to detect?
        - Plot residuals on graph and look for patterns. No pattern = good
        - Durbin-Watson Test (value should fall between 0 and 4)
          - 2 -> no autocorrelation
          - 1 and 3 -> is alarming
            - NO REMEDY
            - When in the presence of autocorrelation, avoid the linear regression model
              - Consider other models:
                - Autoregressive Model (AR model)
                - Moving Average Model (MA model)
                - Autoregressive Moving Average Model (ARMA model)
                - Autoregressive Integrated Moving Average Model (ARIMA model)
  
5. No multicollinearity - Independent variables (x'es) are not correlated
    - Otherwise, P-values will be wrong
    - Fixes:
      - Drop one of the two variables
      - Transform them into one (e.g. average price)
      - *Keep them both but treat with caution
    - Prevention:
      - Find the correlation between each two pairs of independent variables
        - Plot correlation matrix

# Dummy Variables

Use dummy variables for categorical variables

# Making predictions

To make predictions, make new dataframe, pass the new dataframe through the model to make predictions - results.predict(new_data)