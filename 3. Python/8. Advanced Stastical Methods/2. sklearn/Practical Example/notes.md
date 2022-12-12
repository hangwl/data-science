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
      -   See practical example with comments