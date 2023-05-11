# Machine Learning Udemy Bootcamp 03 - NumPy

Numpy is a Linear Algebra Library for python.
```
conda install numpy
pip install numpy
```

## NumPy Arrays
Numpy has 2 flavors of arrays: vectors (1D) and matrices (2D)

Creation of 1D/2D numpy arrays:
```
import numpy as np

list = [1, 2, 3]

arr = np.array(list) => array([1, 2, 3])

X = [[1,2,3],[4,5,6],[7,8,9]]

arr2 = np.array(X) => array([
    [1,2,3]
    [3,4,6]
    [7,8,9]
])
```

### Generation of numpy arrays
```
import numpy as np

np.arange(0,10) => array([0,1,2,3,4,5,6,7,8,9])
# 3rd argument is desired step size
np.arange(0,11,2) => array([0,2,4,6,8])
# vector of 3 filled with zeros
np.zeros(3) => array([ 0.,0.,0.])
# matrix 3x3 filled with zeros
np.zeros((3,3)) => array([
    0., 0., 0.,
    0., 0., 0.,
    0., 0., 0.
])
# matrix 3x4 filled with ones
np.ones((3,4)) => array([
    [1., 1., 1., 1.,],
    [1., 1., 1., 1.,],
    [1., 1., 1., 1.,]
])
# similar to arange but the 3rd arg defines the number of desired points
np.linspace(0, 5, 10)

# 4x4 matrix, the argument specifies both cols and rows
np.eye(4) => array([
    [1., 0., 0., 0.],
    [0., 1., 0., 0.],
    [0., 0., 1., 0.],
    [0., 0., 0., 1.]
])
```

### Generation of random arrays
```
import numpy as np

np.random.rand(5) => 1D array of 5 random numbers
np.random.rand(5,5) => 2D matrix of both 5 cols and rows filled with random numbers
np.random.randn(2) => 1D array of 2 numbers in gaussian distribution
np.random.randn(4,5) => 2D matrix 4x4 filled with random gaussian distribution
np.random.randint(1,100) => Random integer between 1 and 100
# 3rd param is array depth
np.random.randint(1,100,10) => 1D array of length 10 containing random numbers between 1 and 100
```

### Methods of numpy arrays

#### Reshape
Adjusts array dimensions with provided rows and cols
```
arr = np.arange(25)
rand_arr = np.random.randint(0, 50, 10)

# pay attention to keep the total size of the structure or it will throw error,
# in this case a 25 items 1D random array fits a 5x5 matrix (5*5=25)
arr.reshape(5,5)
```

#### MAX & MIN
Returns the higher or lower element of the array
```
arr = np.arange(25)
arr.max() => returns higher random generated number.
arr.min() => returns lower random generated number.
```

#### ARGMAX & ARGMIN
Returns the index of the higher or lower element of array
```
arr = np.arange(25)
arr.argmax() => returns the index of higher random generated number.
arr.argmin() => returns the index of lower random generated number.
```

#### SHAPE
Returns the shape of the array, 1D or 2D
```
arr = np.arange(25)
arr.shape => 25.
arr.reshape(5,5)
arr.shape => 5., 5.
```

#### DTYPE
Returns the data type contained in the array
```
arr = np.arange(10)
arr.dtype => dtype('int32')
```

## NumPy Indexing and Selection
```
import numpy as np

arr = np.arrange(0, 11)

arr[8] => value of index 8
arr[1:5] => columns 1 to 5 (5 excluded)
arr[:6] => columns from start to 6
arr[5:] => columns 5 and beyond

```

making things harder...

```
arr_2d = np.array([[5, 10, 15], [20, 25, 30], [35, 40, 45]])

arr_2d[2][1] => 40
# shorthand [row, col]
arr_2d[2,1] => 40

# take rows 0 to 2 and columns 1 to beyond
arr[:2,1:] => array([
    [10, 15],
    [25, 30]
])
```

### Broadcasting
```
import numpy as np

arr = np.arrange(0, 11)

# broadcasting assignment of columns 0 to 5 with value 100 
arr[0:5] = 100

slice_of_arr = arr[0:6]
slice_of_arr[:] = 99

# deep copy instead of ref
arr_copy = arr.copy()
```

### Conditional selection

```
import numpy as np

arr = np.arange(1,11)
this expression returns an array of Booleans, result of comparison with each array number
bool_arr = arr > 5
# returns ref of original arr where indexes are True
arr[bool_arr] => array([6,7,8,9,10])
# shorthand
arr[arr > 5] => takes indexes matching the condition
# that's useful also for ML scaling in order to remove unnecessary out of range dots.
```

## NumPy Operation
```
import numpy as np

arr = np.arrange(0, 11)

arr + arr => take 2 times every number of the array
arr - arr => subtract itself from every number of the arr, [0, 0, 0, ...]
arr * arr
# throws err because isnt able todo 0/0
arr / arr => [ nan,1,1,1,...]
arr * 100 => every number of array * 100

1 / arr => throws err because 1/0 is infinity, array([
    inf, 1., 0.5, ...
])

arr ** 2 => elevates every number by 2
```
### NumPy Universal Functions (ufunc) 
```

np.sqrt(arr) => sqrt of 2

np.exp(arr) => exponential

np.sin(arr) => sin of all numbers of the array

np.log(arr) => logarithm for each number, it throws error because of log(0) = -inf

# same as for all trigonometric functions, math operations
```