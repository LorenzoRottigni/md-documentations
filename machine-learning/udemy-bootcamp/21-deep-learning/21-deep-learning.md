# 21 Deep Learning
Deep learning is a subset of machine learning that uses neural networks to learn from data. The aim of neural networks is to mimic the human brain.

## Perceptron Model to Neural Networks

### Perceptron Model
A perceptron was a form of neural network introduced in 1958 by Frank Rosenblatt.
The human brain is made up of billions of neurons that are connected to each other. Each neuron is connected to other neurons through synapses. The synapses are 
responsible for transmitting information from one neuron to another.
the following image represent a simplified model of a neuron that takes inputs and produces an output.
What's biologically called "dentrites" are the inputs of the neuron, the "nucleus" is the processing unit and the "axon" is the output of the neuron.

<img src="https://storage.rottigni.tech/fs/github/images/ML/DL-perceptron-with-neuron.png" alt="Perceptron with Neuron" width="500"/>

The mathemtical representation highlights the similarity with the biological model where the neuron takes inputs and produces an output. It's possible to imagine that inside the nucleus there is a function that takes the inputs and produces an output.


Ex. if F(x) is a sum the perceptron model will be: y=x1+x2


Is used to multiply the inputs by a weight and then sum them up. The weights are the parameters of the model and they are used to learn from the data. It's useful to think of the weights as the strength of the synapses in the biological model.


The equation becomes: y=w1*x1+w2*x2


There's still a prolem, if the input X is 0 the output will always be 0. To solve this problem is used a bias that is added to the equation. The bias is a constant value that ensures that the output is not always 0.


The equation becomes: y=(x1w1 + b) + (x2w2 + b)


The mathematical generalization of the perceptron model is:

<img src="https://storage.rottigni.tech/fs/github/images/ML/DL-perceptron-equation.png" alt="Perceptron with Neuron" width="400"/>

### Neural Networks
A neural network is a collection of perceptrons that are connected to each other.
A multi-layer perceptron model is known as basic artificial neural network.
The following image represents a neural network with 3 inputs, 2 hidden layers and 1 output.

<img src="https://storage.rottigni.tech/fs/github/images/ML/deep_learning.png" alt="Artificial neural network" width="500"/>

The output of the previous layer is the input of the next layer. The first layer is called input layer, the last layer is called output layer and the layers in between are called hidden layers.
A fully connected layer is a layer in which each neuron is connected to every neuron in the previous layer.
In case of multiclass classification the output layer will have as many neurons as the number of classes. The output of each neuron will be the probability of the input to belong to that class.


Hidden leayers are difficoult to interpret and understand because of their high interconnectivity. The weights of the hidden layers are not directly related to the input and output. The hidden layers are used to learn the features of the data.


- Neural networks become "deep neural networks" when they have more than one hidden layer.
- The width of a network is the number of neurons in a layer.
- The depth of a network is the number of layers in the network.


The incredible thing about the neural network framework is that it can be used to appoximate any function. This is known as the universal approximation theorem.
Has been proven that a neural network with a single hidden layer can approximate any function. The number of neurons in the hidden layer is the only thing that changes.

## Activation Functions

## Cost Functions

## Feed Forward Neural Networks

## Backpropagation