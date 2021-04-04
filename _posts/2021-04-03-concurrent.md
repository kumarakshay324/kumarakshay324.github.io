---
layout: post
title:  "Concurret Programming In C++"
categories: [ Computer Science]
tags: blog_post
image: assets/images/projects/concurrent.png
---

A computer executes each assembly code instruction for an application, on a clock cycle. Each instruction executed, needs access to the processor's ALU and other logical units, available on each core. The multiple cores on a processor allow multiple instructions to be executed simultaenously thus utilizing the compute resources to the fullest. 

Concurrency is the concept of running multiple executions overlapping in time, across the processor. Concurret programming refers to implementing soliutions to execute processes and/or threads of a process simultaneously.  

### Introduction

Concurrent programming is achieved either through multiple threads that communicate between each other using the parent process' memory or through multiple processes running simultaneously and communicating over inter-process communication. On each clock cycle, each processor core only supports one instruction which can belong to one particular process or thread.


### Multithreading


Multithreading is the concept of spawning multiple virtual sub-processes from a main process, each responsible for executing a certain piece of the process, only loosely coupled with the rest of it and sharing data over the shared memory of the parent process. A standard computer has 6-8 cores while essentially running many more threads.

Practically, it is impossible to pack as many cores on the compute platform. Hence, time slicing is used to interleave the execution of multiple threads alternately. Time slicing usually happens unpredictably and non-deterministically trying to execute the low-level instructions interleaved on the cores.


### Challenges in Multithreading

Multithreading is susceptible to problems with conflict in management of the shared data over multiple threads. The two primary problems with data management are **race condition** and **deadlock**.

**Race condition** is when multiple threads are trying to access and modify the same memory location (variable or pointer) simultaneously. Any memory manipulation is not atomic, hence, will have multiple other atomic operations from different threads interleaved. Hence, the memory can be corrupted as none of the threads' completely modify the data before the other thread overtakes.

Race conditions can be solved by allowing threads to take ownership of a resource (basically putting a lock on it), completing all manipulation steps on it and then releasing the lock for the other thread to take over the ownership. This is implemented in code using mutexes and semaphores.

**Deadlock** happens when two threads running simultaneously are trying to get access to multiple data resources at the same time. When the first thread is holding access to a resource A needed by the second thread in order to release resource B needed by the first thread to finish, it is a deadlock  

Resource A and resource B are used by process X and process Y

* X starts to use A.
* X and Y try to start using B
* Y 'wins' and gets B first
* now Y needs to use A
* A is locked by X, which is waiting for Y

