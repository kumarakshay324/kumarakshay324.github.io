---
layout: post
title:  "An Introduction To Visual SLAM"
categories: [ Robotics,  ]
tags: blog_post
---

**Visual SLAM** is the most researched topic in all of SLAM technology today. Visual sensing has made feature extraction extremely easy and provided rich information for autonomous navigation. Visual SLAM techniques generally track features in images over successive frames and use the triangulation or other techniques to obtain their 3D position which thus helps create the map while also working backwards to predict the camera pose(eventually the robot pose) that observed the map features.

![Sample of Visual SLAM features]({{site.baseurl}}/assets/images/slam/visual_slam.png ) <br>*Sample of Visual SLAM features*

### Introduction

The observation point, properties of the camera and the estimation of camera motion is used to reconstruct the 3D scene of the environment, i.e. the map. 

SLAM has two components - a sensor data processing and modeling system and secondly the observed data inference system. Using corresponding frames of images, the map features are discovered and created while during the complete run, the features are compared with each other for loop closure(event of the robot revisiting an old location) 

Visual SLAM also has several methods and employs different technologies in conjunction for autonomous navigation. Visual odometry, visual data usage and camera type and type of image processing are parts of the complete SLAM puzzle wherein specific algorithms for each of them are used to implement an end-to-end SLAM setup.

### Visual SLAM Nuances

Visual SLAM has different kinds of data interpretation and data processing methods. A camera sees a lot of information but needs a trade-off between the quantity of pixel information to be used, information that can be encapsulated and how computationally viability of the involved processes can be ensured.

* Map Data Quality

**Sparse visual SLAM** utilizes only a portion of the complete image pixels while **dense visual SLAM** utilizes almost all of the pixels of the incoming image. Given the difference in quantity of pixels used and thus the quality of features observed, sparse and dense visual SLAM methods generate very different maps. 

Sparse methods generate point cloud maps that are basically points in 3D space at a depth suggesting the presence of an obstacle in the environment. Point clouds are coarse representations of the environment with very limited information and thus, post processing of information is computationally expensive. Dense maps on the other hand have loads of pixels to use, so their handling and interpretation needs more powerful hardware.

* Direct & Indirect Methods

**Indirect methods** also called feature-based methods for SLAM use the input images, obtain a few sparse features from them and then compare the features to solve for SLAM. **SIFT(Scale-invariant feature transform)**, **SURF(Speeded up robust feature)**, **BRIEF(Binary Robust Independent Elementary Features)** and **ORB(Oriented FAST and rotated BRIEF)** are some of those algorithms that are used to extract features for images and compare them against the different features from different poses. Finally, tracking procedures are used to minimize the error in a the pose of a feature as tracked and the expected pose from the camera estimate, i.e. feature reprojection error, over all the points. 

Features are those special regions in an image that tend to be present uniquely/distinctively in the canvas. Generally these features could be corners of walls or objects like tables and chairs in the scene or windows and doors around. 

Feature extraction obtains the useful information in images. All features observed are converted into compact descriptors to be matched against other descriptors. These descriptors are generally the appearance, pixel gradient around the feature or otherwise, nearby the feature. 

After the features are extracted, feature matching/comparison for the descriptors is done. Features are matched over several frames and tracking different features over long sequences helps in understanding motion. Matching of features uing techniques like RANSAC(RANdom SAmple Consensus) eventually leads to pose estimation for the robot. 

Cameras can see everything and a lot more. Wide angle cameras include even more information. Images with features/interesting information concentrated in a small area of the image canvas are difficult to use for feature matching than others with features spread all over the canvas. While storage requirements make it difficult maintain a database of all the features, it is still better than the direct methods as it still discards the larger parts of the images, the non-feature parts of the image. 

**Direct Methods** compare complete images against each other and then find the overlapping parts to observe motion. Several semi-dense 3D maps can be created using semi-dense filtering algorithms and thus provide more information about the environment. However, they can't handle intermittent noise because those noisy pixels would also be considered as regular parts of the image and thus possibly presented in the final map. Given that they compare complete images, they are slower than the feature-based version as well.


### Loop Closure

Loop Closure is one of the most important aspects of SLAM that ensures that the solutionsa are consistent over the complete work area and over long durations of operation. Loop closure refers to the processing of comparing previously visited scenes/features with the ones from the incoming scenes such that the pose estimation errors are corrected. 

The easiest form of loop closure is matching the incoming image frame with all the previous ones for similar features. However, the storage and computational requirements make it very difficult for real-time applications. Defining key frames( frames of high interest and with more information enclosed within) from the previous frames helps in reducing this computational needs. 

Out of the several frames, for a frame to be selected as key frame, the feature descriptors are hierarchically quantized and represented by a Bag of Visual Words (BOW) called a vocabulary tree. Thereafter, a place recognition approach based on this vocabulary tree is used. Clustering of feature descriptors makes comparison a mere step of observing the frequency and comparing the similarity of the histogram of frequencies. 

False positive and false negative are two kinds of loop closure problems better known as perceptual aliasing and perceptual variability respectively. Perceptual aliasing declares two different places, to be the same while perceptual variability is where one same place is thought of as two different places. Precision-recall curves are useful when predicting the probability of a binary outcome (here if frames match or not) and using the same here in loop closure helps define the performance better. 

### Back-End Optimization

Camera pose optimization is an obvious process to obtain camera motion while dealing with drift pose estimation. EKF is used to minimize the noise in motion prediction and motion observation. 

Bundle adjustment or graph optimization is another method that combinedly optimizes the pose of the camera(hence the robot pose) and the 3D structure paraneters viewed in multiple frames, by minimizing a cost function. Inconsistency in models and processing of filtering techniques make way for this method.

