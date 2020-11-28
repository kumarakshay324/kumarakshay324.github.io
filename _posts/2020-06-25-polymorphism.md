---
layout: post
title:  "Polymorphism in C++"
categories: [ Computer Science,  ]
tags: blog_post
image: assets/images/projects/poly.png
---
Among the most common imperative, object-oriented and functional programming paradigms, OOP is perhaps the most used paradigm in the industry today. OOP allows for desired levels of abstraction, modularity, safety and data management. Large project architectures are able to thrive and expand fairly easily due to the OOP design. Inheritance, polymorphism, encapsulation, asbtraction operational principles of OOP that makes it so famous.

![OOP Principles]({{site.baseurl}}/assets/images/polymorphism/oop.png )<br> *OOP Principles*

### Introduction

OOP concepts are applicable at the class level and not at the object level in C++. Classes are the user-defined data types with member functions and variables and they C++ form the backbone of all OOP programming. Inheritance is defining classes that could derive/inherit properties from other base classes. The derived class inherits from the base class and is used when the derived class IS-A base class. Inheritance using classes in C++ lays the foundation of implementation of all other OOP princicples. 

Abstraction is essentially limiting the data visibility and is achieved by access modifiers like public, protected and private. Encapsulation refers to wrappig up information and functions together. It is basically implemented to allow programs to access data while hiding the manipulation of data. 

Finally, polymorphism is the feature that can invoke different behavior of a function in the inheritance hierarchy. Polymorphism executes different function implementations depending on the type of object that calls the method. It is basically about which kind of object(base or derived class object) calls a method defined in multiple classes throughout the hierarchy. 

Function overriding and overloading are special features of C++. Virtual and pure-virtual functions are the correct implementations of polymorphism.

### Function Overloading

Function overloading is a C++ feature that allows defining multiple functions with the same name but different signatures i.e., different arguments, can be defined in the same class. When called with different arguments, the compiler resolves which function is to be called. Function overloading is not possible depending on the return type. 

<br>`int sum(int a, int b) { return a + b; } `
<br>`float sum(float a, float b) { return a + b; } `
<br>`float sum(float a, float b, float c) { return a + b + c; } `

**It is not an implementation of polymorphism in C++.**

### Polymorphism

Polymorphism resolves the correct function being called, at runtime; via the process called dynamic linking. A function declared in the base class using the virtual prefix is a virtual function and its definitions in base class as well as derived class informs the compiler to avoid static compile-time linkage.If the base class has a pure virtual function, i.e. the function signature has = 0 in the end, then it is mandatory to define it in the derived class and override the base class implementation. 

The base class shall have **virtual** functions that are redefined in the derived classes.

<script src="https://gist.github.com/kumar-akshay324/5a830045bbb6f2909a49633c9af06bb1.js"></script> *Example Code*

Output of the above code is: 
<br>`Square area: `
<br>`Pentagon area: `
<br>`Dummy called in base class `
<br>`Dummy called in base class `

In the code, the `area()` function is a pure virtual method in the base class `RegularPolygon` and has overriding definitions in derived classes. Even though the calls to the `area()` function are made from base class pointer poly (that stores the derived object pointers), it still resolves to the implementations from the individual derived classes via dynamic linking at runtime, using vtables. Here, the compiler looks inside the contents of the pointer to know the type of object calling the method and resolves it correctly. It is all because the function was declared with the virtual keyword indicating polymorphism. 

On the other hand, the dummy() method is a normal method with definitions in the base as well as derived classes. However, calls to such methods depend on the type of pointer making the call and thus, when the poly object of `RegularPolygon` type calls the method, it only calls the implementation from the base RegularPolygon class and not from their individual derived classes due to static linking.

Polymorphism is a very useful tool to implement abstract classes (classes with atleast one pure virtual function) or interfaces. They are helpful in architecting the fundamental structure of base classes correctly. Virtual methods are useful to avoid incorrect pointer handling.

