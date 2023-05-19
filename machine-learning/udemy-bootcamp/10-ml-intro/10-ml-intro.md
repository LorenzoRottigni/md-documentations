# Machine Learning

## Supervised Learning
Supervised learning consists of learning the link between two datasets: the observed data X and an external variable y that we are trying to predict, usually called “target” or “labels”. Most often, y is a 1D array of length n_samples.
It's commonly used to predict future events using historical data.

ML model development follows these steps:
1. Data acquisition
2. Data cleaning
3. Data exploration
4. Feature engineering
5. Model training
6. Model evaluation
7. Model deployment

### Classification models
Used to predict a class label, which is a choice from a predefined list of possibilities.
### Regression models
Used to predict a continuous number, or a floating-point number in programming terms (or real number in mathematical terms).

It's a common practice to split the dataset into 3 parts:
1. Training set: used to train the model.
2. Validation set: used to evaluate the model during training, adjust hyperparameters (e.g. learning rate) and pick the best model.
3. Test set: used to evaluate the model after training.

It possible to use just a training and test set, but it's not recommended because the model can overfit the training data and perform poorly on the test set.

### Model Evaluation
There are several metrics to evaluate a model for both classification and regression problems.

#### Classification model metrics

##### Accuracy
It's one of the most common classification metrics. It's the number of corrected predictions divided by the total number of predictions.
Accuracy is suitable for balanced datasets, but it's not recommended for imbalanced datasets. For balanced datasets is meant that the number of samples for each class is similar.
Ex. 1000 samples of dogs and cats, half are dogs and half are cats. In this case, accuracy is a good metric to evaluate the model.
In case of 999 dogs it would have a high accuracy score because it would predict all samples as dogs, covering 99.9% of the dataset.

##### Recall
Is the ability of the model to find all the relevant cases within a dataset.
It's the number of true positives divided by the number of true positives plus the number of false negatives.

##### Precision
Ability of classification model to identify only the relevant data points.
It's the number of true positives divided by the number of true positives plus the number of false positives.

##### F1 Score
F1 score is the harmonic mean of precision and recall.
Is used an harmonic mean instead of an arithmetic mean because it punishes extreme values.
```
F1 = 2 * (precision * recall) / (precision + recall)
```

##### Confusion Matrix
A confusion matrix is a table that is often used to describe the performance of a classification model on a set of test data for which the true values are known.
It's a 2x2 matrix that contains 4 outcomes produced by a binary classifier.

| Actual Positive | Actual Negative |
| --------------- | --------------- |
| True Positive   | False Negative  |
| False Positive  | True Negative   |

The main point of classification metrics and confusion matrix is to evaluate the model and understand if it's performing well or not.
All there metrics compare the predicted values with the actual values and good metrics depends on the specific problem.


#### Regression model metrics
Classification metrics aren't suitable for regression problems because they are used to evaluate the model's ability to predict a class label, not a continuous number.
To evalutate regression models are used metrics for continuous numbers.

##### Mean Absolute Error (MAE)
It's the historical metric for regression problems. It's the average of the absolute difference between the predicted values and the actual values.
```
MAE = (1 / n) * sum(|y - y_pred|)
```
MAR won't punish large errors and it's not suitable for datasets with outliers.

##### Mean Squared Error (MSE)
It's the average of the squared difference between the predicted values and the actual values.
```
MSE = (1 / n) * sum((y - y_pred)^2)
```
MSE punishes large errors and it's suitable for datasets with outliers so it solves the problem of MAE.
A critical point of MSE is that it's not in the same unit of the target variable, so it's not possible to interpret it. (dollars => dollars^2)

##### Root Mean Squared Error (RMSE)
Metric algorithm with the aim to solve the unit problem of MSE. It's the square root of MSE.
```
RMSE = sqrt(MSE)
```
RMSE is the most common metric for regression problems because by root squaring the units are the same of the target variable.

## Machine Learning in Python
The most common library for ML in Python is scikit-learn. It's an open source library that provides a wide range of ML algorithms.
It's built on top of NumPy, SciPy and Matplotlib.
```
pip3 install scikit-learn
conda install scikit-learn
```

Every algorithm exposed by scikit-learn is an Estimator object (Class of scikit-learn). It implements the fit() and predict() methods.
The Estimator class exposes the same API (methods, attributes, constructor args) for every algorithm, so it's easy to switch between algorithms.
```
from sklearn.linear_model import LinearRegression

model = LinearRegression()
```

Scikit-learn allows to split the dataset into training and test set using the train_test_split() function.
```
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3)
```

To train the model is used the fit() method.
```
model.fit(X_train, y_train)
```

To predict the target variable is used the predict() method.
```
y_pred = model.predict(X_test)
```

The evaluation method depends on the specific problem.

Estimator object exposes a score() method that implements the evaluation logic for the specific algorithm.
```
model.score(X_test, y_test)
```

### Choosing an algorithm
In order to choose the right algorithm for a specific problem is necessary to understand the problem and the data,
scikit-learn provides a flowchart to help in the process:

<img src="https://scikit-learn.org/stable/_static/ml_map.png" width="500">
