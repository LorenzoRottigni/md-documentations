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

### RUGPLOT
Rugplot draws a dash mark for every point on a univariate distribution.
```
sns.rugplot(
    tips['total_bill']
)
```

### KDEPLOT
KDEPlot represents the distribution of data in a KDE (Kernel Density Estimation) format.
Normal distribution is mathematically represented by KDE.
```
sns.kdeplot(
    tips['total_bill']
)
```
