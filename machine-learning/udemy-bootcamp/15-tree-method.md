# 15 Tree Method

## Decision Tree Classifier
It consists in a tree-like model, where each node represents a feature (attribute), each link (branch) represents a decision (rule) and each leaf represents an outcome (categorical or continues value).
It's a supervised learning algorithm that can be used for both classification and regression problems, but mostly used for classification problems.
Its goal is to create a model that predicts the value of a target variable by learning simple decision rules inferred from the data features.

pros:
  - Easy to understand and interpret
  - Requires little data preparation
  - Able to handle both numerical and categorical data
  - Performs well with large datasets
  - Able to handle multi-output problems

cons:
  - Prone to overfitting
  - Unstable, as small variations in the data might result in a completely different tree being generated
  - Not fit for continuous variables

### Random Forest Classifier
It's an ensemble learning method for classification, regression and other tasks that operates by constructing a multitude of decision trees at training time and outputting the class that is the mode of the classes (classification) or mean prediction (regression) of the individual trees.
It's common to use the random forest algorithm as a baseline method to compare with other models.
It beats standard decision trees in most cases.

### Python Implementation

#### INIT
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

%matplotlib inline

df = pd.read_csv('kyphosis.csv')
df.head()

df.info()

sns.pairplot(df, hue='Kyphosis')
```

#### TRAIN TEST SPLIT

```
from sklearn.model_selection import train_test_split

X = df.drop('Kyphosis', axis=1)
y = df['Kyphosis']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3)
```

#### Decision Tree Classifier
```
from sklearn.tree import DecisionTreeClassifier

dtree = DecisionTreeClassifier()

dtree.fit(X_train, y_train)

p = dtree.predict(X_test)

from sklearn.metrics import classification_report, confusion_matrix

print(classification_report(y_test, p))
print(confusion_matrix(y_test, p))

from sklearn.ensemble import RandomForestClassifier
```

#### Random Forest Classifier
```
rfc = RandomForestClassifier(n_estimators=200)

rfc.fit(X_train, y_train)

p = rfc.predict(X_test)

from sklearn.metrics import classification_report, confusion_matrix

print(classification_report(y_test, p))
print(confusion_matrix(y_test, p))
```

#### Tree Visualization
Scikit Learn has some built-in visualization capabilities for decision trees, isnt often necessary and it requires pydot library.
```
from IPython.display import Image  
from sklearn.externals.six import StringIO  
from sklearn.tree import export_graphviz
import pydot 

features = list(df.columns[1:])
features

dot_data = StringIO()  
export_graphviz(dtree, out_file=dot_data,feature_names=features,filled=True,rounded=True)

graph = pydot.graph_from_dot_data(dot_data.getvalue())  
Image(graph[0].create_png())  
```
