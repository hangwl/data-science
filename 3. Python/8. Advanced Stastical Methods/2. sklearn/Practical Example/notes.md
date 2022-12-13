In real life, data sets are messy. Usually we follow these steps.

1. Clean the data
2. Relax assumptions
3. Log-transform the data
4. Create a model
5. Create dummies

1.04. Real-life example.csv contains raw carsales data

As usual, the modelling process is a follows:

1. Importing relevant libraries
    import numpy as np
    import pandas as pd
    import statsmodels.api as sm
    import matplotlib.pyplot as plt
    from sklearn.linear_model import LinearRegression
    import seaborn as sns
    sns.set()

2. Loading the raw data
    raw_data = pd.read_csv('1.04. Real-life example.csv')
    raw_data.head()

3. Preprocessing the data
   a. Exploring the descriptive statistics of the variables
        raw_data.describe(include='all')
            - count: notice missing values in 'EngineV'
            - unique (entries for categorical variables): 312 unique models is difficult to implement in regression (too many dummies)
            - top (most common)
            - 90% of entries in 'Registration' are 'yes' -> this variable won't be useful

   b. Determining the variables of interest
       - a lot of information from 'Model' could be engineered from 'Brand', 'Year', 'Engine', so we won't lose too much variability from omitting this variable
           data = raw_data.drop(['Model], axis=1) # 0-rows; 1-cols

   c. Dealing with missing values
       - data.isnull().sum() # show a df with null data information
       - data_no_mv = data.dropna(axis=0) # adhoc method to drop missing values # rule of thumb: free to drop observations if <5% of total

   d. Exploring the PDFs
       - for optimal result, we should be looking for a normal distribution
       - sns.distplot(data_no_mv['Price]) shows an exponential distribution, which is a problem for our regression
           - possibly due to outliers (observations that lie on abnormal distance from other observations in the data)

   e. Dealing with outliers
       - in this case, we can remove top 1% of data (price)
         - q = data_no_mv['Price].quantile(0.99)
         - data_1 = data_no_mv['Price'<q]
       - 'Mileage' has the same problem, use the same treatment
         - q = data_1['Mileage'].quantile(0.99)
         - data_2 = data_1[data_1['Mileage']<q]
       - 'Engine' volumes are usually below 6.51
         - data_3 = data_2[data_2['EngineV]'<6.5]
       - Treat 'Year' with same concept
         - q = data_3['Year'].quantile(0.01)
         - data_4 = data_3[data_3['Year']>q]

4. Checking the OLS assumptions
   1. Linearity
        Plot log-price on individual variables of interest
   2. No Endogeneity
        To test if assumption is violated, can take the residuals and plot them against individual variables
   3. Normality and Homoskedasticity (constant variance of errors)
        Normality is assumed for big samples following CLT
        The zero mean of the distribution of errors in accomplished through the inclusion of the intercept in the regression
        Heteroskedasticity is addressed by log-transform on y
   4. No Serial Correlation
        No necessary in this case. (We are not dealing with time-series or panel data)
        No reason for observations to be dependent on each other
   5. No Multicollinearity
        Logical for year and mileage to be correlated
        sklearn does not have dedicated method to check this assumption.
          need to rely on statsmodels:
            VIF (variance inflation factor) can used to check for multicollinearity <https://statisticalhorizons.com/multicollinearity/>
              - VIF produces a measure to estimate how much larger the square root of the std. error of an estimate is compared to a situation where it was completed uncorrelated with the other predictors
              - VIF = 1 : no multicollinearity
              - VIF = 1-5 : perfectly okay
              - VIF = >10 : unacceptable
  
    -   See practical example with comments

5. Create dummy variables - need to create N-1 dummies if we have N categories for a feature
      By convention, we also want to arrange variables in order of: dependent variable, independent numerical variables, dummy variables
      Check VIF
        See Dummies and VIF for example