# Machine Learning Udemy Bootcamp 06 - Pandas data visualization
Pandas has some built-in data-visualization tool that allows to easily display dataframe plots based on the dataframe itself or one of its features.
It's possible to choose if draw plots using matplotlib, seaborn or pandas built-in.

## Plotting with Pandas

A simple plot:
```
df1['A'].hist(bins=30)
```

It's possible to choose what kind of syntax to use:

```
# df columns expose plot method
df1['A'].plot(
    # what kind of plot
    kind='hist',
    bins=30
)
# shorthand
df1['A'].plot.hist(bins=30)
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/pandas-histplot-1.png" alt="Pandas histplot 1" width="340" />

## AREA PLOT

```
df2.plot.area(
    # transparency
    alpha=0.4
)
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/pandas-histplot-2.png" alt="Pandas histplot 2" width="340" />

## BAR PLOT

```
# considers categorical indexes, if number they will be treated as categories
df2.plot.bar()
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/pandas-barplot-1.png" alt="Pandas barplot 1" width="340" />

```
# onlw shows the offset between bars
df2.plot.bar(stacked=True)
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/pandas-barplot-2.png" alt="Pandas barplot 2" width="340" />

## SCATTER PLOT

```
df1.plot.scatter(
    # feature A on x axis
    x='A',
    # feature B on y axis
    y='B',
    # color based on feature C, adds 3rd dimension
    c='C',
    # adjust size of dots based on feature C
    s=df1['C'] * 100,
    cmap='coolwarm'
)
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/pandas-scatteplot.png" alt="Pandas scatteplot" width="340" />

## BOX PLOT

```
df2.plot.box()
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/pandas-boxplot.png" alt="Pandas boxplot" width="340" />

## HEXBIN PLOT

```
df = pd.DataFrame(np.random.randn(1000, 2), columns=['a', 'b'])
df.plot.hexbin(x='a', y='b', gridsize=25, cmap='coolwarm')
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/pandas-hexbinplot.png" alt="Pandas hexbinplot" width="340" />

## KDE PLOT (Kernel Density Estimation)

```
df2['a'].plot.kde()
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/pandas-kdeplot.png" alt="Pandas kdeplot" width="340" />

## DENSITY PLOT

```
df2.plot.density()
```

<img src="https://storage.rottigni.tech/fs/github/images/ML/pandas-densityplot.png" alt="Pandas density plot" width="340" />
