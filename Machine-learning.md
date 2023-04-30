# MACHINE LEARNING

## Background explanations
- In normal programming we have y = f(x) and the programmer given an input writes the algoritmh that calculates the output. In ML a big input of x and y is given and the function is generated from the ML model.
- A big amount of data is used to "feed" the ML algoritmh, it uses the data to create and train the model that will interact with the final user.

## Algorithms
### Linear regression
- returns a function that relates X and y where y must a number

## Metrics
### MAE - mean_absolute_error
Error measure that executes subtractions between predictions and and desired outputs.
It takes for each calculated offset the absolute value (|x|, removes +/-) and then it calculates the average between all offsets.
The more MAE is near 0 the more we're near the success.
It's a good error measure because it keeps the measure unit of the input data.

## Data validation
It's important to subdivide the allocated big data taken as input in 2 parts in order to validate the model generated output.
The first part that usually takes the 70/75% of the total is used for the training, the model will be generated based on this data.
The second part is used for testing once the model is ready.
It's a best practice to test both testing and training datasets.

## Python environment
The library the provides machine learning and data mining utils is named scikit-learn.

### Code convertions
- Is used to name the variable that contains the x of the function "X" because it's a numeric matrix.
- The output variable is simply named "Y"
- Is used to name the algorithm class with the name of the ML algorithm and its istance as "model"
- All ML algorithm classes expose 2 methods: fit() to train the model and predict() to ...
