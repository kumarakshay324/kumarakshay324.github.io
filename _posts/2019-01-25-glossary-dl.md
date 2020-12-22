---
layout: post
title:  "Deep Learning"
categories: [ Deep Learning, Machine Learning ]
tags: glossary
---

All the terminology in Deep Learning I come across and learn from tons of articles and tutorials.

<br>
<hr>

#### Gradient Descent

Gradient descent is the method to compute the gradient of the objective function/ loss function with respect to each of the model parameters. The magnitude and direction of the gradient suggests the variation in the parameters, during the training with the goal of minimizing the loss and its rate of change as well.


### Leaky-ReLU

The common rectified linear activation (ReLU) function is a piecewise function which has value constantly proportional to the input, for positive inputs and a value of 0 otherwise. This leads to a derivative of 1 for positive and 0 for otherwise inputs.

The **Leaky-ReLU** is a little modified with a very small slope value for non-positive inputs which ensures that no neurons go dead (have zero effect) on the learning during backpropogation. This little value is called _alpha_ and thus the gradient-descent is _alpha * x_ instead of 0.



