# Machine Learning Udemy Bootcamp 05 - Matplotlib

It's the most used plotting library in data science and it was designed to have a similar feel to MatLab's (Math programming language) graphical plotting.
It works well with NumPy arrays and Pandas DataFrames.

```
conda install matplotlib
pip install matplotlib
```

## Basics of Matplotlib
```
import matplotlib.pyplot as plt
import numpy as np
# if using Jupyter Notebook, include the following line to see plots in the notebook
%matplotlib inline

x = np.linspace(0,5,11)
y = x ** 2
```

## Functional Method
```
plt.plot(
  # X axis values
  x,
  # Y axis values
  y,
  # function red line
  'r-'
)
# Define a label for X axis
plt.xlabel('X Label')
# Define a label for Y axis
plt.ylabel('Y Label')
# Define a title for the plot
plt.title('Title')
# display the plot programattically (outside jupyer notebook)
plt.show()


# Plot multiple plots on the same canvas
plt.subplot(1,2,1)
plt.plot(x,y,'r')
plt.subplot(1,2,2)
plt.plot(y,x,'b')
```

## OOP Method
A basic Matplotlib figure is composed by two objects: a figure and axes. The figure is the canvas where the plot is drawn and the axes are the plot itself.
```
# Create a figure object, imagine it as a blank canvas
fig = plt.figure()

axes = fig.add_axes([
    # axis left
    0.1,
    # axis bottom
    0.1,
    # axis width
    0.8,
    # axis height
    0.8
])

axes.plot(x,y)
axes.set_xlabel('X Label')
axes.set_ylabel('Y Label')
axes.set_title('Title')
```
Multiple plots on the same canvas:
```
fig = plt.figure()
# Create 2 sets of axes on the same canvas
axes1 = fig.add_axes([0.1,0.1,0.8,0.8])
axes2 = fig.add_axes([
  # 20% from the left
  0.2,
  # 50% from the bottom
  0.5,
  # 40% of canvas total width
  0.4,
  # 30% of canvas total height
  0.3
])

# function
axes1.plot(x,y)
axes1.set_title('Larger Plot')
# reverse function
axes2.plot(y,x)
axes2.set_title('Smaller Plot')
```
Shorthand to create a figure with axes in OOP:
```
# automatically invoke fig.add_axes based on nrows and ncols params
# this creates a grid 1x2 containing a plot on each cell (same as with 3x3 grid)
fig, axes = plt.subplots(
  # number of rows, positional or keyworded
  nrows=1,
  # number of columns, positional or keyworded
  ncols=2
)

# improves the layout of the plots, prevents overlapping
plt.tight_layout()

# axes is a list of matplotlib axes, we're able to iterate over it
for axis in axes:
  # set same x and y values for all plots in the canvas
  axis.plot(x,y)

# manually iterate over axes
axes[0].plot(x,y)
axes[0].set_title('First Plot')
axes[1].plot(y,x)
axes[1].set_title('Second Plot')
```

## Figure Size, Aspect Ratio and DPI
```
fig = plt.figure(
    # figsize is a tuple with width and height in inches
    figsize=(8,2),
    # dpi is the dots per inch (pixel per inch)
    dpi=100
)

ax = fig.add_axes([0,0,1,1])
ax.plot(x,y)
```
Shorthand:
```
fig, axes = plt.subplots(nrows=2, ncols=1, figsize=(8,2))
axes[0].plot(x,y)
axes[1].plot(y,x)
plt.tight_layout()

fig.savefig('my_picture.png', dpi=200)
```
Multi functions on same plot:
```
fig = plt.figure()
ax = fig.add_axes([0,0,1,1])
ax.plot(x,x**2, label='X Squared')
ax.plot(x,x**3, label='X Cubed')

# show a leger the matches labes with functions color
ax.legend(
  # value 0 to 10 to define the position of the legend
  # using 0 matplotlib will understand what's the best position 
  loc=0
)
```

## Plot Appearance
```
fig = plt.figure()
ax = fig.add_axes([0,0,1,1])
ax.plot(
  # data on x
  x,
  # data on y
  y,
  # color of the line as name or hex or rgb
  color='purple',
  # line width, default is 1. Also works as lw=3
  linewidth=3,
  # opacity of the line
  alpha=0.5,
  # linestyle, - is solid, -- is dashed, -. is dashdot, : is dotted, steps is disquared. Also works as ls='-'
  linestyle='-',
  # marker, o is circle, + is plus, * is star, s is square, 1 is triangle down, 2 is triangle up, 3 is triangle left, 4 is triangle right, x is x, | is vertical line, _ is horizontal line. Also works as marker='o'
  # appearence of dots on the line
  marker='o',
  # size of the marker
  markersize=20,
  # marker color
  markerfacecolor='yellow',
  # marker border width
  markeredgewidth=3,
  # marker border color
  markeredgecolor='green'
)
```

# Plot limits
```
fig = plt.figure()
ax = fig.add_axes([0,0,1,1])
ax.plot(x,y,color='purple',linewidth=2,alpha=0.5,linestyle='--',marker='o',markersize=20,markerfacecolor='yellow',markeredgewidth=3,markeredgecolor='green')
# distribute X axis values from 0 to 1
ax.set_xlim([0,1])
# distribute Y axis values from 0 to 1
ax.set_ylim([0,2])
```
