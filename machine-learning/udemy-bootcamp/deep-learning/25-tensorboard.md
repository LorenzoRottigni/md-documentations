# 25 - Tensorboard

Tensorboard is a visualization tool from Google designed to work in conjunction with TensorFlow to visualize various aspect of the model. It can be used to visualize the graph, plot quantitative metrics about the execution of the graph, and show additional data like images that pass through it.

Tensorboard is a web application that can be accessed through the browser. It is automatically installed with TensorFlow. To start Tensorboard, run the following command in the terminal:

```
tensorboard --logdir=/tmp/tensorflow_logs
```

This will start Tensorboard on port 6006. You can access it by opening the following URL in the browser:

```
http://localhost:6006
```

In order to start tensorboard with python, you can use the following code:

```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

%matplotlib inline

df = pd.read_csv('cancer_classification.csv')

X = df.drop('benign_0__mal_1', axis=1).values
y = df['benign_0__mal_1'].values

from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X,y,test_size=0.25,random_state=101)

from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()

X_train = scaler.fit_transform(X_train)

X_test = scaler.transform(X_test)

import tensorflow as tf
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Activation, Dropout
from tensorflow.keras.callbacks import EarlyStopping, TensorBoard

early_stop = EarlyStopping(monitor='val_loss', mode='min', verbose=1, patience=25)

log_dir = 'logs/fit'

board = TensorBoard(
    log_dir=log_dir,
    histogram_freq=1,
    write_graph=True,
    write_images=True,
    update_freq='epoch',
    profile_batch=2,
    embeddings_freq=1
)

model = Sequential()

model.add(Dense(units=30, activation='relu'))
model.add(Dropout(0.5))

model.add(Dense(units=15, activation='relu'))
model.add(Dropout(0.5))

model.add(Dense(units=1, activation='sigmoid'))

model.compile(loss='binary_crossentropy', optimizer='adam')

model.fit(
    x=X_train,
    y=y_train,
    epochs=600,
    validation_data=(X_test, y_test),
    verbose=1,
    callbacks=[early_stop, board]
)
```

Once the model is fitted using tensorboard callback it's possible to start tensorboard server using the following command:

```
tensorboard --logdir logs/fit --host localhost --port 8088
```
