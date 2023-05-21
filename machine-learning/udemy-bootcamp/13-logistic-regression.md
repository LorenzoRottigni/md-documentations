# 13 Logistic Regression

Logistic regression is a classification algorithm used to assign observations to a discrete set of classes.
We're not able to use linear regression with binary classification because it will produce values outside of 0 and 1.
Logisti regresion uses a curve, called the sigmoid curve, to produce values between 0 and 1.
It's possible to take the linear regression equation and transform the output using the sigmoid function in order to constrain the output to values between 0 and 1.

Linear regression equation: y = mx + b
Logistic regression equation: y = 1 / (1 + e^-(mx + b))

Is used to set a cutoff point, usually 0.5, to determine the predicted class. (higher than 0.5 = 1, lower than 0.5 = 0)
It's possible to use logistic regression to get a binary output 0 or 1.

To evaluate the performance of a classification model, it's possible to use a confusion matrix.

          | Predicted: 0   | Predicted: 1
Actual: 0 | True Negative  | False Positive
Actual: 1 | False Negative | True Positive

Confusion matrix gives an overview of:
- True Positives => predicted yes and it was yes in reality
- False Positives => predicted yes and it was no in reality
- True Negatives => predicted no and it was no in reality
- False Negatives => predicted no and it was yes in reality

## RATES

### Accuracy
It represent how often the model is correct, using this formula:
Accuracy = (True Positives + True Negatives) / (True Positives + True Negatives + False Positives + False Negatives)
The sum of true positive and true negatives is divided by the total number of observations.

### Misclassification Rate
It represent how often the model is wrong, using this formula:
Misclassification Rate = (False Positives + False Negatives) / (True Positives + True Negatives + False Positives + False Negatives)
The sum of false positives and false negatives is divided by the total number of observations.

