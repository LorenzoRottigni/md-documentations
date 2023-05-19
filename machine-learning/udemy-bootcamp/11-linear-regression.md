# 11 Linear Regression
Machine Learning algorithm that predicts a continuous value, it aims to minimize the distance between the points and the line of best fit.
It is a supervised learning algorithm.

## Representing Linear Regression
The equation of a line is y = mx + b, where m is the slope and b is the y-intercept.
Good plots to represent linear regression are scatterplots, jointplots, linearmodelplots and residualplots.
It's always a good practice to also use a pairgrid to see the relationship between all the features.


## Measures for Linear Regression
Common metrics for linear regression are:
- Mean Absolute Error (MAE)
- Mean Squared Error (MSE)
- Root Mean Squared Error (RMSE)
- Explained Variance Score (EVS)

## Residuals
Residuals are the difference between the actual value and the predicted value.
Residuals are a good way to evaluate the performance of a model, and they should be normally distributed.
It's possible to represent residuals with a displot like this:

```
sns.displot((y_test-predictions),bins=50);
```

## Linear Regression with Python
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline

USAhousing = pd.read_csv('USA_Housing.csv')
USAhousing.head()
USAhousing.info()
USAhousing.describe()
USAhousing.columns

sns.pairplot(USAhousing)
sns.displot(USAhousing['Price'])

sns.heatmap(USAhousing.corr())

X = USAhousing[['Avg. Area Income', 'Avg. Area House Age', 'Avg. Area Number of Rooms',
       'Avg. Area Number of Bedrooms', 'Area Population']]

y = USAhousing['Price']

from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.4, random_state=101)

from sklearn.linear_model import LinearRegression

lm = LinearRegression()

lm.fit(X_train,y_train)

print(lm.intercept_)
print(lm.coef_)
cdf = pd.DataFrame(lm.coef_,X.columns,columns=['Coeff'])

predictions = lm.predict(X_test)

plt.scatter(y_test,predictions)

sns.displot((y_test-predictions),bins=50);

from sklearn import metrics

print('MAE:', metrics.mean_absolute_error(y_test, predictions))
print('MSE:', metrics.mean_squared_error(y_test, predictions))
print('RMSE:', np.sqrt(metrics.mean_squared_error(y_test, predictions)))
print('EVS:', metrics.explained_variance_score(y_test, predictions))
```