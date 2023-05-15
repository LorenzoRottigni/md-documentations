# Machine Learning Udemy Bootcamp 06 - Seaborn

Seaborn is a statistical plotting library, built on top of matplotlib.
It's designed to work well with pandas dataframe objects.
It's open source and hosted on Github.

```
conda install seaborn
pip install seaborn
```

## Distribution Plots
Distribution plots allows to show the distribution of a univariate (one variable) set of observations.

### DISTPLOT
Distplot is a histogram with a line on it representing the distribution.
```
import seaborn as sns

# allow visualization in Jupyter Notebook
%matplotlib inline

tips = sns.load_dataset('tips')

tips.head()

# distribution plot
sns.distplot(
    tips['total_bill'],
    # remove kde line and display only histogram
    kde=False,
    # change number of bins
    bins=30
)
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/sns-distplot.png" alt="SNS distplot" width="340" />

### JOINTPLOT
Jointplot allows to match up two distplots for bivariate data (two variables).
It creates a canvas where are related two distplots.
```
sns.jointplot(
    # feature on X
    x='total_bill',
    # feature on Y
    y='tip',
    # dataset where to extract features
    data=tips,
    # hex => hexagonal density plot
    # ref => linear regression visualizer
    # kde => kernel density estimation
    # how data is represented
    kind='scatter'
)
```
<img src="https://storage.rottigni.tech/fs/github/images/ML/sns-jointplot.png" alt="SNS jointplot" width="340" />

### PAIRPLOT
Pairplot allows to plot pairwise relationships across an entire dataframe (for the numerical columns) and supports a color hue argument (for categorical columns).
It's a jointplot for every single combination of the numerical columns in the dataframe.
```
sns.pairplot(
    # dataset to visualize
    tips,
    # categorical columns
    hue='sex',
    # pass a predefined palette from seaborn website
    palette='coolwarm'
)
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/sns-pairplot.png" alt="SNS pairplot" width="340" />

### RUGPLOT
Rugplot draws a dash mark for every point on a univariate distribution.
```
sns.rugplot(
    tips['total_bill']
)
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/sns-rugplot.png" alt="SNS rugplot" width="340" />

### KDEPLOT
KDEPlot represents the distribution of data in a KDE (Kernel Density Estimation) format.
Normal distribution is mathematically represented by KDE.

```
sns.kdeplot(
    tips['total_bill']
)
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/sns-kdeplot.png" alt="SNS kdeplot" width="340" />

## Categorical Plots

### BARPLOT
Barplot is a general plot that allows to aggregate categorical data based off some function, by default the mean.

```
sns.barplot(
    # feature sex on X (categorical)
    x='sex',
    # feature total_bill on Y (numerical)
    y='total_bill',
    data=tips
)
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/sns-barplot.png" alt="SNS kdeplot" width="340" />

### COUNTPLOT
Countplot is the same as barplot except the estimator is explicitly counting the number of occurrences.

```
sns.countplot(
    # categorical feature
    x='sex',
    data=tips
)
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/sns-countplot.png" alt="SNS kdeplot" width="340" />

### BOXPLOT
Boxplot shows the distribution of categorical data.
It shows the quartiles of the dataset while the whiskers extend to show the rest of the distribution.
Outliers are plotted as points outside the whiskers.

```
sns.boxplot(
    # categorical feature
    x='day',
    # numerical feature
    y='total_bill',
    data=tips,
    # categorical feature
    hue='smoker'
)
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/sns-boxplot.png" alt="SNS boxplot" width="340" />

### VIOLINPLOT
Violinplot plays a combination of boxplot and kdeplot.
Allows to understand the relationship between two categorical features and a numerical feature.

```
sns.violinplot(
    # categorical feature
    x='day',
    # numerical feature
    y='total_bill',
    data=tips,
    hue='sex',
    # split the violin plot by the hue feature
    # instead of having a violin plot for each category of the hue feature
    split=True
)
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/sns-violinplot.png" alt="SNS violinplot" width="340" />

### STRIPPLOT
Stripplot draws a scatterplot where one variable is categorical.
A strip plot can be drawn on its own, but it is also a good complement to a box or violin plot in cases where you want to show all observations along with some representation of the underlying distribution.

```
sns.stripplot(
    # categorical feature
    x='day',
    # numerical feature
    y='total_bill',
    data=tips,
    # adds a random noise to the data to avoid overlapping
    jitter=True,
    hue='sex'
)
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/sns-stripplot.png" alt="SNS stripplot" width="340" />

### SWARMPLOT
Swarmplot is a combination of stripplot and violinplot, but the points are adjusted (only along the categorical axis) so that they don’t overlap.
This gives a better representation of the distribution of values, although it does not scale as well to large numbers of observations (both in terms of the ability to show all the points and in terms of the computation needed to arrange them).

```
sns.swarmplot(
    x='day',
    y='total_bill',
    data=tips,
)
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/sns-swarmplot.png" alt="SNS swarmplot" width="340" />

### FACTORPLOT
Factorplot is the most general form of a categorical plot.
It can take in a kind parameter to adjust the plot type.

```
sns.factorplot(
    x='day',
    y='total_bill',
    data=tips,
    # specify the kind of plot
    kind='bar'
)
```

## Matrix Plots
Matrix plots allow to plot data as color-encoded matrices and can also be used to indicate clusters within the data.
To be a Marix it should have categorical features on both axes.

### HEATMAP
Heatmap is a simple way to plot a matrix plot.

```
sns.heatmap(
    # dataset to plot
    flights,
    # annotates the heatmap with the numeric value
    annot=True,
    # cmap => colormap
    cmap='coolwarm'
)
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/sns-heatmap.png" alt="SNS heatmap" width="340" />

### CLUSTERMAP
Clustermap uses hierarchal clustering to produce a clustered version of the heatmap.
It will show data aggregated as similar values, heatmap uses the provided order to show the data

```
sns.clustermap(
    flights,
    # standardize the scale
    standard_scale=1
)
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/sns-clustermap.png" alt="SNS clustermap" width="340" />


