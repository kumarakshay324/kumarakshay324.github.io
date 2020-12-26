---
layout: post
title:  "Deep Learning"
categories: [ Deep Learning, Machine Learning ]
tags: glossary
---

All the terminology in Deep Learning I come across and learn from tons of articles and tutorials.

<br>
<hr>

### Adam Optimizer

Adam is an adaptive rate optimizer that dynamically modifies the value of learning rates for each parameter and specifically effective in training deep neural networks. It uses the moving average of the gradient for momentum and the squared gradients to scale the learning rate, similar to SGD and RMSProp respectively. It uses the first and second moments of gradients to modify the learning rate for each parameter. It is the most commonly used optimizers and beats others in speed.

#### Gradient Descent

Gradient descent is the method to compute the gradient of the objective function/ loss function with respect to each of the model parameters. The magnitude and direction of the gradient suggests the variation in the parameters, during the training with the goal of minimizing the loss and its rate of change as well.

### Leaky-ReLU

The common rectified linear activation (ReLU) function is a piecewise function which has value constantly proportional to the input, for positive inputs and a value of 0 otherwise. This leads to a derivative of 1 for positive and 0 for otherwise inputs.

The **Leaky-ReLU** is a little modified with a very small slope value for non-positive inputs which ensures that no neurons go dead (have zero effect) on the learning during backpropogation. This little value is called _alpha_ and thus the gradient-descent is _alpha * x_ instead of 0.

### One Hot Encoding

One hot encoding is used in machine learning to represent classes, for a classication algorithm, as a combination of multiple bits with a single 1 (HIGH) for the class and rest 0s (LOW. It is a common way of defining the state of a state machine. For instance, for 3 classes of animals - dogs, cats and cows the one-hot encoding representation looks like dogs - 100, cats - 010 and cows - 001. It helps programmatically represent the classification labels and outputs for computational efficiency.

### Softmax

Softmax is an activation function that normalizes a set of K values to another set of values (between 0 and 1) that sum to up tp 1. It helps conform the output of a machine learning algorithm into a set of probabilities. It is also known as softargmax or normalized exponential function and uses exponents of the variables for normalization.


