# 18 - Principal Component Analysis

Principal Component Analysis (PCA) is a dimensionality reduction technique that can be used to reduce a large set of variables to a small set that still contains most of the information in the large set.
Using PCA it's possible to transform a set of features into principal components. These principal components are linear combinations of the original features. The first principal component is the linear combination that accounts for the largest possible variance in the data set. The second principal component must be orthogonal to the first principal component and must account for the largest possible variance given this restriction. The third principal component must be orthogonal to the first two and so on.
Principal components don't have a 1 to 1 correlation with the original features, it's a combination of all the features and doesn't have a direct interpretation.
PCA is an unsupervised learning algorithm, it doesn't use the labels.

## Python Implementation
Scikit-learn has a PCA class that can be used to perform PCA in Python. The PCA class takes a parameter n_components that specifies the number of principal components to return. If n_components is not set then all components are returned.

### Dataset
```
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

%matplotlib inline

from sklearn.datasets import load_breast_cancer

cancer = load_breast_cancer()

df = cancer['data']
```

### Scaling
Once data is scaled, we can use PCA to find the first two principal components, that means we are going to find the first two principal components that explain the most variance in the data.
It's important to scale data firstly because PCA is affected by scale, so you need to scale the features in your data before applying PCA. Use StandardScaler to help you standardize the dataset’s features onto unit scale (mean = 0 and variance = 1) which is a requirement for the optimal performance of many machine learning algorithms.
```
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
scaler.fit(df)
scaled_df = scaler.transform(df)
```

### PCA
```
from sklearn.decomposition import PCA

pca = PCA(
    # number of components to keep
    n_components=2
)

pca.fit(scaled_df)

x_pca = pca.transform(scaled_df)
```
Dataset before transformation has 30 features:
```
df.shape
#(569, 30)
```
Dataset after transformation has 2 features:
```
x_pca.shape
#(569, 2)
```

### Plotting
By plotting the first two principal components, we can see a clear separation between the two classes, malignant and benign
```
plt.scatter(
    # all the rows of col 1 on x axis
    x_pca[:,0],
    # all the rows of col 2 on y axis
    x_pca[:,1],
    # color the points based on the target, color points based on malignant or benign
    c=cancer['target'],
    cmap='plasma'
)
plt.xlabel('First Principal Component')
plt.ylabel('Second Principal Component')
```
the power of PCA is that by compressing the data into two dimensions, we still have a very good separation between the two classes and a big variance explained.

We can also look at the components themselves, each row represents a principal component, and each column relates back to the original features:
```
pca.components_

# array([[ 0.21890244,  0.10372458,  0.22753729,  0.22099499,  0.14258969,
#          0.23928535,  0.25840048,  0.26085376,  0.13816696,  0.06436335,
#          0.20597878,  0.01742803,  0.21132592,  0.20286964,  0.01453145,
#          0.17039345,  0.15358979,  0.1834174 ,  0.04249842,  0.10256832,
#          0.22799663,  0.10446933,  0.23663968,  0.22487053,  0.12795256,
#          0.21009588,  0.22876753,  0.25088597,  0.12290456,  0.13178394],
#        [-0.23385713, -0.05970609, -0.21518136, -0.23107671,  0.18611302,
#          0.15189161,  0.06016536, -0.0347675 ,  0.19034877,  0.36657547,
#         -0.10555215,  0.08997968, -0.08945723, -0.15229263,  0.20443045,
#          0.2327159 ,  0.19720728,  0.13032156,  0.183848  ,  0.28009203,
#         -0.21986638, -0.0454673 , -0.19987843, -0.21935186,  0.17230435,
#          0.14359317,  0.09796411, -0.00825724,  0.14188335,  0.27533947]])
```

In order to get back to the original features, we can use inverse_transform:
```
pca.inverse_transform(x_pca)
```
or simply:
```
df_comp = pd.DataFrame(pca.components_, columns=cancer['feature_names'])

# mean radius	mean texture	mean perimeter	mean area	mean smoothness	mean compactness	mean concavity	mean concave points	mean symmetry	mean fractal dimension	...	worst radius	worst texture	worst perimeter	worst area	worst smoothness	worst compactness	worst concavity	worst concave points	worst symmetry	worst fractal dimension
# 0	0.218902	0.103725	0.227537	0.220995	0.142590	0.239285	0.258400	0.260854	0.138167	0.064363	...	0.227997	0.104469	0.236640	0.224871	0.127953	0.210096	0.228768	0.250886	0.122905	0.131784
# 1	-0.233857	-0.059706	-0.215181	-0.231077	0.186113	0.151892	0.060165	-0.034768	0.190349	0.366575	...	-0.219866	-0.045467	-0.199878	-0.219352	0.172304	0.143593	0.097964	-0.008257	0.141883	0.275339
```
We can visualize this better using a heatmap that represents the correlation between the various feature and the principal component itself.
```
plt.figure(figsize=(12,6))
sns.heatmap(df_comp, cmap='plasma')
```

It's finally possible to use a classification algorithm to predict the target using the PCA components instead of the original data.
```
x_pca.shape
```