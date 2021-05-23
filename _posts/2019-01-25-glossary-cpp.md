---
layout: post
title:  "C++ Concepts"
categories: [ C++ Concepts ]
tags: glossary
---

Collection Of C++ concepts and Terminology.

<br>
<hr>

### std::async

Multithreading on multi-core is an amazing programming paradigm to help speed up applications and utilize the compute resources to the maximum. C++ 11 provides an amazing suite of tools to implement multi-threading including `std::thread`, `std::future` and `std::async`. While `std::thread` wraps the underlying platform dependent `pthread` execution to build platform agnostic applications, `std::async` and `std::future` help navigate the pain of having thread-pools and manually handling lifetimes for multiple threads. 


`std::async` helps execute a funciton asynchronously, potentially on a new thread, without explicitly making new threads. The output of the function can be stored in `std::future` that can be used as and when available. The available launch policies 1. `std::launch::async` 2. `std::launch::deffered` and 3. `std::launch::async | std::launch::deferred` help define how the operation is to be performed. A new thread is created for the first, not for the second and OS made decision for the third for the policies.

### Stack vs Heap

**Stack** is the memory space in the computer which stores variables temporarily. Runtime variables are created, stored and manipulated in the stack. When the process ends or the code goes out of scope, the mempry is automatically erased, i.e. managed by the CPU. Usually functions, local variables and reference variables are declared here.

**Heap** is the memory space used to store global variables accessible throughout the scope of the program and supports dynamic memory allocation for larger objects. It is not managed by the CPU and is often called free floating memory. The programmer putting data on the heap is responsible to clear it up and could otherwise cause memory leaks. In C++, creating objects using the `new` keyword allocates memory on the heap and thus needs the `delete` call to clean it up. 

**Stack vs Heap**

* Stack is a linear data structure with occupying contihguous memory locations while heaps nd
* Stack allows high speed access while heaps are slower to access. It is because the memory modification on the stack is usually a push or a pop instruction and done on one machine cycle compared the heap which needs to call the OS code for the modification. 
* Stack is managed by the OS and CPU, thus never gets fragmented while the heap is not managed and thus get fragmented because blocks of memory are first allocated then freed
* Stack is meant for local variables only while the heap allows variable access globally
* Stack is limited in size based on the OS while the heap is not limited in size
* Stack doesn't allow the variables to be resized while the heap allows it using calls like `realloc()` in C language.
* The finite memory on the stack is allocated everytime a new thread is created while the heap is more of a runtime need-based memory. 