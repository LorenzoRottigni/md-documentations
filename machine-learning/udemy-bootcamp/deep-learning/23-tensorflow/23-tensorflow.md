# 23 Tensorflow

# Tensorflow Deep Learning

Tensorflow is a library for numerical computation and large-scale machine learning. It is a framework for defining and running computations involving tensors. A tensor is a generalization of vectors and matrices to potentially higher dimensions. Internally, TensorFlow represents tensors as n-dimensional arrays of base datatypes.

Tensorflow is a low-level library, which means that it provides a lot of flexibility but it requires a lot of code to build a model. Keras is a high-level library that runs on top of TensorFlow, which means that it provides less flexibility but it requires less code to build a model.

Building a model with tensorflow:

```
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense

model = Sequential()

model.add(
    Dense(
        # number of neurons same as number of features
        19,
        # rectified linear unit
        activation='relu'
    )
)
model.add(Dense(19, activation='relu'))
model.add(Dense(19, activation='relu'))
model.add(Dense(19, activation='relu'))
model.add(Dense(19, activation='relu'))

# output layer
model.add(Dense(1))

model.compile(optimizer='adam', loss='mse')

model.fit(
    x=X_train,
    y=y_train,
    # validation data is used to evaluate the loss function
    validation_data=(X_test, y_test),
    # batch size is the number of samples per gradient update.
    # the lower the batch size, the longer it takes to train.
    batch_size=128,
    epochs=400
)
```

In the code above, the model is a sequential model, which means that the layers are stacked on top of each other. The first layer is the input layer, which has 19 neurons because the dataset has 19 features. The activation function is rectified linear unit (relu). The output layer has 1 neuron because the target feature is a continuous variable. The loss function is mean squared error (mse) because the target feature is a continuous variable. The optimizer is adam, which is a good optimizer for most cases. The model is trained for 400 epochs, which means that the model is trained 400 times. The batch size is 128, which means that the model is trained 128 samples at a time. The validation data is used to evaluate the loss function.

The model can be evaluated using the .evaluate() method:

```
model.evaluate(X_test, y_test, verbose=0)
```

The model can be used to make predictions using the .predict() method:

```
predictions = model.predict(X_test)
```

The model can be saved using the .save() method:

```
model.save('model.h5')
```

The model can be loaded using the .load_model() method:

```
from tensorflow.keras.models import load_model

model = load_model('model.h5')
```

It's possible to predict a new value using the .predict() method:

```
single_house = df.drop('price', axis=1).iloc[0]

# it's necessary to reshape the data because the model expects a 2D array
single_house = scaler.transform(single_house.values.reshape(-1, 19))

model.predict(single_house)

df.head(1)['price']
```

It's possible to evaluate the model using usual metrics such as mean absolute error (mae), mean squared error (mse), and root mean squared error (rmse):

```
from sklearn.metrics import mean_absolute_error, mean_squared_error

predictions = model.predict(X_test)

mae = mean_absolute_error(y_test, predictions)

mse = mean_squared_error(y_test, predictions)

rmse = np.sqrt(mse)
```

It's possible to plot the loss function using the .history attribute:

```
losses = pd.DataFrame(model.history.history)

losses.plot()
```

Explained variance score (R^2) is a metric that measures how well future samples are likely to be predicted by the model. The best possible score is 1.0 and it can be negative. A constant model that always predicts the expected value of y, disregarding the input features, would get a R^2 score of 0.0.

```
from sklearn.metrics import explained_variance_score

explained_variance_score(y_test, predictions)
```
