# 12 - Bias Variance Trade-Off
Bias variance trade-off is a foundamental topic of understanding model's performance.

<img src="https://www.cs.cornell.edu/courses/cs4780/2018fa/lectures/images/bias_variance/bullseye.png" alt="bias variance trade-off">

The bias-variance trade-off is the point where we are adding just noise by adding more complexity to the model.


### Bias
Bias is the difference between the average prediction of our model and the correct value which we are trying to predict. A model with high bias pays very little attention to the training data and oversimplifies the model. It always leads to high error on training and test data.

### Variance
Variance is the variability of model prediction for a given data point or a value which tells us spread of our data. A model with high variance pays a lot of attention to training data and does not generalize on the data which it hasn’t seen before. As a result, such models perform very well on training data but has high error rates on test data.

### Bias-Variance Trade-Off
Bias Variance Trade-Off is a point where we have the right balance between bias and variance which minimizes the total error.



