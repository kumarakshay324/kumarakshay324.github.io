---
layout: post
title:  "Design Pattens in C++"
categories: [ Computer Science]
# tags: blog_post
image: assets/images/design_patterns/design.png
---

C++ is a language used in developing high-performance applications used across infustries like space, robotics, autonomous vehicles and communications. C++ software applications Have sophisticated architectures to be compute-efficient, robust and production-grade safe. The design patterns are usually based on different concepts involved in OOP.   

### Introduction

Software design pattern refers to crafting the correct strategies for classes, their objects, the variables and other entities in the code. The different patterns also define how functions behave, what data they modify and 


![Pytorch Dataloader]({{site.baseurl}}/assets/images/dataloader/pipeline.png )

### SOLID Design Principles

* **S =  Single Responsibility Principle**
A class, function or struct should be implement and execute only one task or responsibility and should not have multiple tasks intertwined.

* **O = Open-Closed Principle**
Any C++ entity should be open for extensions and they can be used to achieve additional behavior but nothing should be able to modify the existing behavior.

* **L = Liskov Substitution Principle**
An object should be replaceable with another instance of its substype without breaking any interfaces or breaking the code. This means, the interface for interacting with a derived class should be the same as for a base class, as much as possible. 

* **I = Inteface Segregation Principle**
APIs should have multiple client-specific interfaces instead of one generic interface

* **D = Dependency Injection**
Any dependency between entities should be abstract and not concrete. One entity should necessarily need its dependency to exist perfectly but a wrapped layer should be enough.

High level modules should be dependent on low level modules only via abstractions and the latter should only depend on interfaces and supertypes instead of exact implementations.

### Creational Design Patterns 

Creational design patterns provide code-level mechanisms for creating objects in the code. They define how different instances of a class can be created and modified.
 
* **Builder** - When multiple objects should be created piecewise, the API should have interface to that in a clean code manner. The *Builder* allows attaching or adding smaller pieces of an object when the consolidated object is gnarly to create. For example, to build an instance of an address, the API should allow different elements like the zip-code, state, and city to set or attached independent of the main constructor.

* **Factory** - Designing a new component that is repsonsible for creating multiple objects together instead of directly calling the constructor individually for each object. When creating an object can have limitations like multiple optional parameters and argument overloading. A *factory* could be an independent method, an independent classs or an inner static method for the class and can create objects for a class, wrapping all constructors calls with method calls and they can return those created objects.

* **Prototype** - An object which is partially or completely initialized and can be copied or cloned to use. Often, a class represents objects that could hold the most overlapping implementations of features. 


_Download and load the training data_
<script src="https://gist.github.com/kumar-akshay324/b63d0a82c6daaea7db0ede3e1dc2ca5c.js"></script>

Each next batch of the data can be accessed using the `__iter__()`. Iterating over the dataloader can also access the batches.


### Dataloaders on Custom Dataset

While the in-built datasets available in torchvision have predefined madatory methods, the `__len()__` and the `__get_item__()` functions for accessing the data. Any custom dataset definition is a derived class of the Pytorch `Dataset` and needs to have these methods defined for usage.

**Note:** - This code has been copied from somewhere I don't recall of.

<script src="https://gist.github.com/kumar-akshay324/bb20f20889388cf80e16b14bd8154de1.js"></script>