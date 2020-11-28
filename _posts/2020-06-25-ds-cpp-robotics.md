---
layout: post
title:  "C++ Data Structures in Robotics - Part I"
categories: [ Robotics, Computer Science]
tags: blog_post
image: assets/images/projects/cpp_robotics.png
---

I have been working with C++ for a couple of years now. While I have not encountered use of a lot of off-the-shelf C++ algorithms used intensively in robot software stack development, certain data structures have definitely been very efficient for particular applications in robotics. I thought it was time to revisit the basic data structures in C++ and also, makes notes for future use. 

The more important reason for this article is to aggregate information of how and why differrent data structures should be used in robotics algorithms.

Standard data structures in C++ STL are:

* Vectors (`std::vector`)
* Graphs
* Matrices
* Stacks (`std::stack`)
* Queues (`std::queue`)
* List (`std::list` and `std::forward_list`)
* Heap (`std::heap`)
* Maps (`std::map` or `std::unordered_map`)
* Sets (`std::set`)
* Miscellaneous : Priority Queue(`std::priority_queue`) and Deque (`std::deque`)

### VECTORS

A vector is used for simple storage of a collection of same data type objects. It is a sequence container that supports dynamic size modification on the fly. They are similar to arrays and store data in contiguous memory locations but additionally can change size. 

Vectors are internally just simple arrays that have extra space allocations for possible growth and modification. This is because if the memory is fixed, there may be no more room for additional data when being dynamically modified and all the data has to be reallocated to a bigger memory group. Thus, to avoid such time consuming reallocation steps, vectors consume more memory but are computationally efficient is maintaining dynamic storage. 

Most common instances to use vectors for efficiency include serialization, easy traversal, index based lookup, addiiton to the end, and conversion to C-style arrays. They should be avoided for applications like arbitrary insertion/deletion and dynamically changing the location of storage. 

The most common operations on vectors are:


* Iterators: `begin()`, `end()`, `rbegin()`, `rend()`, `crbegin()`, `crend()`, `cbegin()`, `cend()`
Return the iterator or const iterator from the beginning or the reverse beginning of the vector

* Sizing: `size()`, `max_size()`, `resize()`, `capacity()`, `empty()`, `reserve()`, `shrink_to_fit()`
The first four methods return the size, maximum size, the capacity and check for the emptiness of the vector. The reserve(n) method is used to declare that the storage is needed for n elements and the vector is reallocated only if the current capacity is lesser than that, else nothing changes.

* Modification: `push_back()`, `pop_back()`, `insert()`, `erase()`, `swap()`, `emplace()`, `emplace_back()` 
First four methods are to push or remove a value from the end of the vector. Then, insert data or a data container to one index before the specified index. Data can also be removed from a particular position (iterator value) or a length of data positions using erase. 

**Vectors in Robotics** 

For the majority of my applications while storing the manipulator joints' custom data types, I have used the vector. It allows easy traversal and thus makes kinematics and dynamics operations easy on each robot joint. ROS uses arrays for such storage as it is assumes the size of the containers should be fixed. For storing all physical values of the robot parameters like joint forces, torques, limits, positions and more, I have had custom data structures and then a vector storing a collection of the same. 

The easy traversal through a vector makes it suitable for storing instruction sequences like trajectories. For example: 

<script src="https://gist.github.com/kumar-akshay324/3843532ea8f6df156b239a71182c4b35.js"></script> *Example Operations on Vectors*
<br>

<script src="https://gist.github.com/kumar-akshay324/9e24df6dd2586a629fad9e97b509fb88.js"></script> *Example Trajectory Struct using C++ Vector*

### GRAPHS

Graphs are one of the most important structures and used extensively in all domains of computer science. Graphs are essential for all sorts of search algorithms, tree traversals, optimized paths and more. 

A graph is basically a collection of several vertices connected to other via links. Each vertex in a graph is called a node and links are called edges. The adjacent nodes in a graph are those two nodes which are connected by an edge. The number of edges (essentially the other nodes) that a particular node is connected to is called degree of a node. Sequence of traversal from one node to the other via edges is called a path. 

If all the nodes are connected to atleast one other node and no node is isolated, the graph is a connected graph whereas if all nodes are connected to all other nodes resulting in a total of n(n-1)/2 nodes, it is called a complete graph. If there are weights assigned for traversal via each edge, the graph is a weighted graph. If the direction of edges from a node in the graph is fixed thus fixing the traversal direction, it is called a diagraph. 

**Graph Representation**

A graph data structure can be naively thought of as a collection of nodes and each node has a collection of the other nodes it is connnected. It may also need to store information about the weight and the direction of the edge. 

C++ does not have an in-built data structure to represent graphs. Thus, there are different ways to represent the graph programmatically.

* Sequential Representation: Adjacency matrices are used for sequential representations of relationships between the nodes in a graph. Here, the **N** nodes are laid out along the rows and the columns of a **N x N** matrix adjacency_matrix. Now, for a pair of nodes that have an undirected edge, the value of **adjacency_matrix(node<sub>A</sub>, node<sub>B</sub>)** and adjacency_matrix(node<sub>B</sub>, node<sub>A</sub>)is non-zero and often used to represent the weight of the edge. For a directed graph, from node **A** to node **B**, only adjacency_matrix(node<sub>A</sub>, node<sub>B</sub>) value is non zero and the other pair adjacency_matrix(node<sub>B</sub>, node<sub>A</sub>) is zero (rows and column node represents the start and end node respectively).

* Linked Representation: For this representation adjacency lists are used. An adjacency list for a node represents the other nodes linked to it as a linked list. It terminates in a null.

**Graphs in Robotics** 

Graphs are probably the most important data structures in robotics. Almost all planning algorithms that need some kind of search or path finding employ graphs. Graphs provide for establishing directional connectivity between two positions in space and thus extremely important for mobile robots, drones, and manipulators. 

Graphs used with cost functions between points determine traversal algorithms and decisions. Most path planning algorithms like A*, Dijikstra, RRT, RRT*, and PRMs all operate on nodes in the configuration space and they are represented using graphs. Other general search algorithms in computer science, like breadth-first or depth-first search also use graphs along with queques and stacks respectively.

<script src="https://gist.github.com/kumar-akshay324/efc3f735d2706c401baaa6e196c678c0.js"></script> *Adjacency Matrix Based Graphs*

<script src="https://gist.github.com/kumar-akshay324/36d62facc6f7b611476424d36c6419eb.js"></script> *Adjacency Lists Based Graphs*

### MATRICES

Matrices are useful data structures used to store data systematically in rows and columns. They are commonly used to represent 3D transitions, multivariate states, and covariances for systems. 

All computer vision applications use matrices while performing image processing operations because they help in condensing the data and representign it more intuively. For instance, a B/W image is represented as a 3D matrix where each value for a particular (row, column) pixel position is the RGB color for that pixel. For a depth sensing camera, there is also a fourth dimension for the depth of the pixel from the camera.

**Matrices in Robotics** 

Matrices are undoubtedly the most common data structures used in robotics regardless of the domain. Robot control uses matrices for state-space definitions, kinematics of the robot use matrices for transformations and movements, dynamics used matrices to represent the physical features, state estimation uses matrices for variances, operations and more. All computer vision and machine learning applications in robotics use matrices to appropriately represent neural networks and vectors. 

Matrices in C++ are either defined using 2-dimensional arrays or vectors of vectors. However, niether of are as efficient, intuitve and easy to use as the matrix support provided in numpy in Python. Eigen, a header only library is the most common open-source library for matrices in C++. While it does use arrays under the hood, the templated librarry provides easy to use wrapper and implementations for almost all matrix operations like transformations and even Singular Value Decomposition (SVD).

### STACK

Stacks are only of the best inbuilt containers in C++. STL provides std::stack which is a standard stack supporting first-in last-out OR last-in first-out data handling. The methods supported by std::stack are pop(), push(), and top() that remove the item on the top of the stack, push the item to the top and return the item from the top of the stack respectively. 

Stacks are useful for reversal of elements or search algorithms using graphs. Stacks have a constant O(1) complexity in all the three function calls.

**Stacks In Robotics** 

When a Depth-First Search is implemented, the children of the node being explored are all pushed into a stack and popped when explored. 

MORE ABOUT USE OF STACKS.

<script src="https://gist.github.com/kumar-akshay324/99b1360479a3c134ca8b85daa8567e17.js"></script> *Using stacks for a valid sequence of braces problem*

### QUEUE

Queues, like stacks, are also one of the best inbuilt containers in C++. STL provides std::queue which is a standard queue supporting first-in first-out OR last-in last-out data handling. The methods supported by std::queue are front(), back(), pop() and size() that returns the element at the head, returns the element at the tail, removes the element at the head and returns the size of the queue respectively. 

Queues are useful for any simple ordering based task. Queue can be used to store list of semaphores ( the identities that manage resource locking and availability in multi-threading systems) and execute them sequentially or for CPU scheduling operations.

**Queue in Robotics** 

Queues are used in a Breadth-First Search implementation where all the children of the node being explored, i.e. all the siblings are pushed into a queue and popped sequentially before exploring the children of the individual sibling (done in stacks). 

Queues are used in several filtering applications to pop the first-in item and add the new incoming data for moving average filter, exponential filter and more.

**THIS ARTICLE IS GETTING PRETTY LONG, SO TO SIMPLIFY - I AM MOVING REST OF THE TOPICS TO A PART II COMING SOON!**