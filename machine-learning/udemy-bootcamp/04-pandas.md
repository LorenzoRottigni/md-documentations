# Machine Learning Udemy Bootcamp 04 - Pandas

Pandas is an open source library built on top of NumPy.
```
conda install pandas
pip install pandas
```

## Series
Series are a pandas datatype similar to numpy array with the difference that are label-indexed.

### Defining a Series
```
import numpy as np
import pandas as pd

labels = ['a', 'b', 'c']
# python list
data = [10, 20, 30]
# numpy array
arr = np.array(data)
# python dict
d = {'a': 10, 'b': 20, 'c': 30}

pd.Series(data=data)
"""
0   10
1   20
2   30
"""
pd.Series(data=data, index=labels)
"""
a   10
b   20
c   30
"""
# positional version
pd.Series(data,labels)

# it works with both numpy arrays and python lists
pd.Series(arr, labels)
# it works also by using a python dict
pd.Series(d)

# you can store every kind of data in a pandas series, also functions
pd.Series(data=labels)
"""
0   a
1   b
2   c
"""
```

### Series Indexing & Operations
```
import pandas as pd

ser1 = pd.Series([1, 2, 3, 4], ['USA', 'Germany', 'USSR', 'Japan'])
ser2 = pd.Series([1, 2, 5, 4], ['USA', 'Germany', 'Italy', 'Japan'])
ser3 = pd.Series(data=labels)

ser1['USA'] => 1
ser1[0] => 1

ser1 + ser2
"""
Germany     4.0
Italy       NaN
Japan       8.0
USA         2.0
USSR        NaN
"""
```

## DataFrames
A dataframe is a bunch of series that share the same index. it's possible to think to each row and column of df as a pandas series.

### Defining a DataFrame
```
import numpy as np
import pandas as pd
from numpy.random import randn

df = pd.DataFrame(
  # data
  randn(5,4),
  # rows/indices
  ['A', 'B', 'C', 'D', 'E'],
  # columns
  ['W', 'X', 'Y', 'Z']
)
"""
          W         X         Y         Z
A  0.721555  0.291992 -0.424832  0.093907
B  0.281746  0.769023  1.246435  1.007189
C -1.296221  0.274992  0.228913  1.352917
D  0.886429 -2.001637 -0.371843  1.669025
E -0.438570 -0.539741  0.476985  3.248944
"""
```
### Accessing DataFrame
```
# columns are of type series
type(df['W']) => pandas.core.series.Series
# dataframe is of type dataframe
type(df) => pandas.core.frame.DataFrame

# it's to possible to access series in both following ways:
df['W'] => W series
# that makes confusion between methods and columns
df.W => W series

# accessing multiple columns
df[['W', 'Z']] => W and Z series
"""
            W         Z
A   -0.842436  0.184519
B    0.937082  0.731000
C    1.361556 -0.326238
D    0.055676  0.222400
E    0.051771  0.887163
"""

# assign a new column containing the sum of W and Y column values
df['new'] = df['W'] + df['Y']

# drop 'new' column
df.drop(
    'new',
    # by default is 0 and refers to indices not to columns
    axis=1,
    # mutate original state instead returning a transformed copy
    inplace=True
)

# drop 'E' row
df.drop(
    'E',
    # refer to X axis
    axis=0,
    inplace=True
)

# dataframe has 4 rows and 4 columns (4=rows/0-axis, 4=columns/1-axis)
df.shape => (4, 4)

# selecting rows instead of columns, also rows are series in pandas
df.loc['A'] => W, X, Y, Z series

df[<key>] => access columns
df.loc[<key>] => access rows

df.loc['C'] => access C row as a series using label index
df.iloc[2] => access C row as a series using numeric index


df.loc['B','Y'] => 1.246435, take row B and column Y intersection

# select a subset of the dataframe
df.loc[['A', 'B'], ['W', 'Y']] => take rows A and B and columns W and Y intersection
"""
          W         Y
A  0.721555 -0.424832
B  0.281746  1.246435
"""
```

### Dataframe Conditional Selection

```
df > 0 => boolean dataframe
"""
       W      X      Y      Z
A   True   True  False   True
B   True   True   True   True
C  False   True   True   True
D   True  False  False   True
"""

bool_df = df > 0
df[bool_df] => NaN where bool_df is False
"""
          W         X         Y         Z
A  0.721555  0.291992       NaN  0.093907
B  0.281746  0.769023  1.246435  1.007189
C       NaN  0.274992  0.228913  1.352917
D  0.886429       NaN       NaN  1.669025
"""
# shorthand
df[df > 0]

df['W'] > 0 => boolean series

# popular and useful expression
df[df['W'] > 0] => take rows where W column is greater than 0
"""
          W         X         Y         Z
A  0.721555  0.291992 -0.424832  0.093907
B  0.281746  0.769023  1.246435  1.007189
D  0.886429 -2.001637 -0.371843  1.669025
"""

result_df = df[df['Z'] < 0] => take rows where Z column is less than 0
"""
          W         X         Y         Z  
C -1.296221  0.274992  0.228913  1.352917
"""

result_df['X'] => take X column from result_df
# shorthand
df[df['W'] > 0]['X']

# multiple conditions
df[(df['W'] > 0) and (df['Y'] > 1)] => throws error because python "and" works with True and False not with boolean series
# & is the right operator to use in order to compare boolean series
df[(df['W'] > 0) & (df['Y'] > 1)]
# | is the or operator for boolean series
df[(df['W'] > 0) | (df['Y'] > 1)]
```

### DataFrames Indexing
```
df = pd.DataFrame(
  # data
  randn(5,4),
  # rows/indices
  ['A', 'B', 'C', 'D', 'E'],
  # columns
  ['W', 'X', 'Y', 'Z']
)

# reset label indexes to numeric indexes,
# label indexes become a "Index" column, a series containing old label indexes
df.reset_index(inplace=True/False)

new_index = 'CA NY WY OR CO'.split()
# assign new column 'States' with values from new_index states list
df['States'] = new_index

df.set_index('States', inplace=True)
transform States column into a row(index)

```

### DataFrames Index Hierarchy
```
outside = ['G1', 'G1', 'G1', 'G2', 'G2', 'G2']
inside = [1, 2, 3, 1, 2, 3]
hier_index = list(zip(outside, inside))
hier_index = pd.MultiIndex.from_tuples(hier_index)

# constructing a multi-level index dataframe
df = pd.DataFrame(
  # 6 rows and 2 columns
  randn(6,2),
  hier_index,
  ['A', 'B']
)
"""
             A         B
G1 1  0.302665  1.693723
    2 -1.706086 -1.159119
    3 -0.134841  0.390528
G2 1  0.166905  0.184502
    2  0.807706  0.072960
    3  0.638787  0.329646
"""

# accessing data from multi-level index dataframe
df.loc['G1'].loc[1]

df.index => indexes of dataframe
df.columns => columns of dataframe

# assign a name to index levels
df.index.names => [Groups, Num]

# access a single cell
df.loc['G2'].loc[2]['B'] => 0.072960

df.xs('G1') => access G1 group

# This takes both G1 and G2 groups with Num=1
df.xs(1, level='Num') => access all groups with Num=1
```

### DataFrames Missing Data
```
d = {
  'A': [1, 2, np.nan],
  'B': [5, np.nan, np.nan],
  'C': [1, 2, 3]
}
df = pd.DataFrame(d)

# drops any row(axis=0) that has any nan value
df.dropna(axis=0)
# drops any column(axis=1) that has any nan value
df.dropna(axis=1)
# drop any row that has 2 or more nan values
df.dropna(thresh=2)
# fill missing values of row with value 'FILL VALUE'
df.fillna(value='FILL VALUE')
# fill missing value of row with mean of column A (improves scaling)
df.fillna(value=df['A'].mean())
```

### DataFrames GroupBy
GroupBy statement allows to group rows together based off of a column and perform an aggregate function on them. Similar to SQL group by.
```
data = {
  'Company': ['GOOG', 'GOOG', 'MSFT', 'MSFT', 'FB', 'FB'],
  'Person': ['Sam', 'Charlie', 'Amy', 'Vanessa', 'Carl', 'Sarah'],
  'Sales': [200, 120, 340, 124, 243, 350]
}
df = pd.DataFrame(data)

# group by company column
by_company = df.groupby('Company')
# get mean of each company's sales
by_company.mean()
"""
         Sales
Company
FB       296.5
GOOG     160.0
MSFT     232.0
"""
# standard deviation
by_company.std()

# the max number for nums columns and the alphabetically last name for string columns
df.groupby('Company').max()

# get statistical info about each company's sales
df.groupby('Company').describe()

# display each company as column instead of a row
df.groupby('Company').describe().transpose()

# access signle company data
df.groupby('Company').describe().transpose()['DB']
```

### Merge, Join and Concatenate DataFrames
```
# concatenate dataframes with same columns and different indexes
pd.concat([df1, df2, df3])
# concatenate dataframes with same indexes and different columns
pd.concat([df1, df2, df3], axis=1)

# merge df1 with df2 usign key as foreign key, exactly like SQL join
pd.merge(left=df1, right=df2, how='inner', on='key')
# merge df1 with df2 using a compound key
pd.merge(left=df1, right=df2, on=['key1', 'key2'])

# join works as merge with the difference that the FK becomes the index instead of a column
df1.join(df2)
```

### DataFrame Operations
```
import pandas as pd

df = pd.DataFrame({
  'col1': [1, 2, 3, 4],
  'col2': [444, 555, 666, 444],
  'col3': ['abc', 'def', 'ghi', 'xyz']
})

# get unique values of a column
df['col2'].unique() => [444, 555, 666]
# get count of unique values of a column
df['col2'].nunique() => [444, 555, 666]
# get count of unique values of a column
df['col2'].value_counts() => 444: 2, 555: 1, 666: 1

# apply a function to a column
df['col2'].sum() => 2109
# apply a callback function to a column
df['col2'].apply(lambda num: num * 2)

df.drop('col1', axis=1) => drop column
df.drop(0, axis=0) => drop row

df.columns => get columns
df.index => get indexes

# sort dataframe rows ascending by column 2
df.sort_values(by='col2') => sort by column

# returns a boolean dataframe containing true where null value is found
df.isnull()
```

#### Pivot Table
```
df = pd.DataFrame({
  'A': ['foo', 'foo', 'foo', 'bar', 'bar', 'bar'],
  'B': ['one', 'one', 'two', 'two', 'one', 'one'],
  'C': ['x', 'y', 'x', 'y', 'x', 'y'],
  'D': [1, 3, 2, 5, 4, 1]
})

df.pivot_table(
  values='D',
  index=['A', 'B'],
  columns=['C']
)
"""
C           x    y
A   B
bar one  4.0  1.0
    two  NaN  5.0
foo one  1.0  3.0
    two  2.0  NaN
"""
```

### Data Input and Output

#### Dependencies
```
pip install sqlalchemy
pip install lxml
pip install html5lib
pip install BeautifulSoup4

#### CSV
```
df = pd.read_csv('example.csv')
df.to_csv(
  'example.csv',
  # don't handle indexes as column
  index=False
)
```

#### Excel
```
# install xlrd for reading excel files
conda install xlrd

df = pd.read_excel(
  # a set of sheets, each sheet is a dataframe
  'Excel_Sample.xlsx',
  # take Sheet1 as dataframe
  sheet_name='Sheet1'
)

df.to_excel(
  'Excel_Sample.xlsx',
  # don't handle indexes as column
  index=False,
  sheet_name='NewSheet'
)
```

#### HTML
```
# it makes its best but it's not perfect
data = pd.read_html('http://www.fdic.gov/bank/individual/failed/banklist.html')

type(data) => list
```

#### SQL
It uses SQLAlchemy ORM to connect to different kinds of SQL databases.

```
from sqlalchemy import create_engine
# DB connection handler 
engine = create_engine('sqlite:///:memory:')
# write dataframe to SQL using sqlalchemy orm
df.to_sql('my_table', engine)
# get back SQL table as dataframe
sqldf = pd.read_sql('my_table', con=engine)
```
