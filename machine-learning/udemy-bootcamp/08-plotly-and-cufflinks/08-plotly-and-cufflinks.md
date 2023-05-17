# Machine Learning Udemy Bootcamp 06 - Plotly & Cufflinks

## Plotly (https://plot.ly/)
It's an open-source interactive visualization library.
They have a cloud service, to host your interactive plots online.
Plotly exposes offline functionality for local usage.

```
conda install plotly
pip install plotly
```

## Cufflinks
It connects plotly with pandas

```
conda install cufflinks
pip install cufflinks
```

## Get started
```
import numpy as np
import pandas as pd
import cufflinks as cf
import plotly as py
from plotly.offline import download_plotlyjs, init_notebook_mode, plot, iplot
%matplotlib inline

# init javascript for notebook
init_notebook_mode(connected=True)
cf.go_offline()

df = pd.DataFrame(np.random.randn(100, 4), columns='A B C D'.split())
df.iplot()
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/cufflinks-plot.png" alt="Cufflinks plot" width="400" />

## Scatter plot
```
df.iplot(kind='scatter', x='A', y='B', mode='markers', size=10)
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/cufflinks-scatterplot.png" alt="Cufflinks scatterplot" width="400" />

## Bar plot
```
df2 = pd.DataFrame({'Category': ['A', 'B', 'C'], 'Values': [32, 43, 50]})
df2.iplot(kind='bar', x='Category', y='Values')
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/cufflinks-barplot.png" alt="Cufflinks barplot" width="400" />

## Box plot
```
df.iplot(kind='box')
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/cufflinks-boxplot.png" alt="Cufflinks boxplot" width="400" />

## 3D Surface plot
```
df3 = pd.DataFrame({'x': [1, 2, 3, 4, 5], 'y': [10, 20, 30, 20, 10], 'z': [5, 4, 3, 2, 1]})
df3.iplot(kind='surface', colorscale='rdylbu')
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/cufflinks-surfaceplot.png" alt="Cufflinks surfaceplot" width="400" />

## Spread plot
```
df[['A', 'B']].iplot(kind='spread')
```

## Histogram
```
df['A'].iplot(kind='hist', bins=25)
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/cufflinks-histplot.png" alt="Cufflinks histplot" width="400" />

## Bubble plot
```
df.iplot(kind='bubble', x='A', y='B', size='C')
```
<img src="https://storage.rottigni.tech/fs/github/images/ML/cufflinks-bubbleplot.png" alt="Cufflinks bubbleplot" width="400" />

## Scatter matrix
```
df.scatter_matrix()
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/cufflinks-scatter-matrix.png" alt="Cufflinks scatter matrix" width="400" />
