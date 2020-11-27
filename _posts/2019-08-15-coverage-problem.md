---
layout: post
title:  "Coverage Problem In Robotics"
categories: [ Robotics,  ]
tags: blog_post
---

Mobile robots are very often supposed to move around the deployment area and complete certain tasks in specific locations of the area. Such problems where the robot is supposed to navigate to an arbitrary location in the pre-fed map and complete a task based on the tool to be used, is called a coverage problem. ​Figure 1 shows such a setup where the robot has a map for the environment, a warehouse in this case; and it is supposed to traverse to the area from any random start point and navigate the area according to the tool and task.

![Sample Coverage Area in a WareHouse Map]({{site.baseurl}}/assets/images/coverage/f1.png ) *Sample Coverage Area in a WareHouse Map*

### Introduction

Mobile robots are the driving force of the warehouses and factories. Such robots are required to complete tasks ranging from transporting goods ro routine patrolling. All these tasks are essentially to be completed autonomously with little to no interference of humans involved. Thus, the robot needs to make decisions in real-time, on its behavior while also planning to act upon the repercussions of the probabilistic effects that its current action has on the future. To delineate the previous statement, consider that the robot knows that it is supposed to be travelling straight to get to a target point and suddenly meets an obstacle. In such cases, the robot needs to decide if it should change its path to come back to the originally planned straight path or if shall compute a new path to the trajectory - depending upon which of them is computationally/otherwise expensive or not. In coverage problems, the robot faces similar issues where it is supposed to act considering the task it is doing, the tool it is using, the start and end locations fed to it and the utility constraints(time, fuel used, sensing limitations etc.) 

This article discusses the complete approach to deduce methodologies for such tasks that has contingency plans and tries to be inclusive of all the possible scenarios that the robot may run into. ​The further sections of the this document cover **robot localization techniques, coverage area decomposition techniques, coverage area navigation techniques.**

### Robot Localization

The ability of robot to recognize its current positioning in the map is of utmost importance as it determines any further action. It is the most important step for any mobile robot before it does any movement. If the robot fails to localize itself deterministically, it can try probabilistic techniques with cues from several small motions to finally determine its global position in the map. Knowledge about current position and orientation with reference to the global origin helps it to refer to landmarks in the map for assistance in navigation and task completion. ​Figure 2 shows the general approach to mobile robot localization. 

![Robot Localization]({{site.baseurl}}/assets/images/coverage/f2.png ) *Robot Localization*

The techniques for robot localization include:

#### Probabilistic Techniques

Such techniques generally draw a probable distribution of robot positioning on the map and then further reduce it down to deterministic values using sensor and trial movements. All probabilistic techniques depend upon inputs from ​perception ​model ​( robot’s idiothetic sources tell it about its own motion, proprioception and robot’s allothetic sources tell it about the world - camera, lidar and laser sensors ) and ​action model ​(like odometry information and wheel revolution based distance covered - subject to errors accrued over time)

* Markov Localization

In this technique, the robot starts with an arbitrarily defined probability distribution of the robot’s position on the map over discrete positions and updates these beliefs over time., The prior probabilities are updated using sensor data like encoder values and laser scans and given it the conditions to discard or support probabilities over the locations. The process of keeping track of probabilities over the complete map, for all discretized possible locations, and re-computing probabilities over all of them makes the process computationally expensive but still helpful as it addresses all the possibilities. The perception model is used to individually update all probabilities over the possible locations using Bayes formula. It could work for both, topological as well as grid maps, but given the generality of the algorithm, it tends to be very inefficient.

* Kalman Localization

This method considers the robot’s possible location on the map as a single Gaussian probability distribution where the mean and covariance values are repeatedly updated to get to the best representation of its pose. Kalman Localization works on using the transition model, that is the robot’s ​action model that updates its likelihood factors and the plant model that is the ​perception model ​that gives another estimate of the future pose in the map. It combines information from the two to get final localization values. The prediction step works on movement prior movement information to predict new locations and then the same is estimated via the sensors that see the environment; finally culminating the update by fusing the two information.

An example to this could be that the robot starts with a random Gaussian belief of its position, takes a small move, records this to predict new position with the existing Gaussian belief, then uses sensors to view the surroundings (distance from the edges of the maps and relative position to certain landmarks on the map) and estimate its location on the map and finally using the two hypotheses to find a better Gaussian probability representation. This iterative techniques terminates when further updates make the probabilities to converge and the resultant distribution shows where the robot could best be in the map. Very often, the high-class sensing systems help make this distribution deterministic with a very narrow region of uncertainty.

#### Landmark based Localization

Another category of localization could scenario where the environment is customized for robot navigation. These cases include easy to sense RFID tags on the floor or shelves of a warehouse, visual landmark coding that represents the corresponding position on the map or otherwise. Such practices are fairly simple but obviously not efficient to be duplicated under time and money constraints. Beacon systems, artificial floor markers and GPS based location estimation are also examples of the same. The robot processes such highly informative tags and compares it with a pre-fed look-up table for the same and finds the best match of the location, deterministically on most of the occasion.

#### Computer Vision based Localization

Use of visual feed could be incorporated in both of the above techniques but using machine vision explicitly to explore the environment while tracking own motion, building an own version of the map and then trying to fit this generated map to a subset of the global map can also be used. In our approach to solving the coverage problem, localization is the first step that determines robot’s motion. It is followed by methods to reach and decompose the arbitrary coverage area into units and reduce the complexity of the task.

### Coverage Area Decomposition Techniques

The coverage area for the task could be any arbitrary section, either continuous or sporadically distributed over the complete map. This makes robot understand the complexity of the task and reduce it to simpler individually addressable sections. 

The complex scenarios for coverage areas could be:

* The area is not a perfect polygon with standard angles on the edges. User inputs using haptic devices and other manual inputs devices or using drawing tools could form very inconsistent edges and angles. A comparative version of standard computationally defined coverage area and a manual-input defined coverage area is shown in ​Figure 3

![Coverage Area With Irregular Boundaries]({{site.baseurl}}/assets/images/coverage/f3.png ) *Coverage Area With Irregular Boundaries*

* The coverage area includes voids in centers and demands robot motion in a way that the robot should eventually find a way out of the area, doesn’t get stuck in it. An example of such scenario can also be seen in ​Figure 4

![Coverage Area With voids within]({{site.baseurl}}/assets/images/coverage/f4.png ) *Coverage Area With voids within*

* The coverage area is discontinuous and distributed all over the map and the robot needs to determine the optimal strategy where incorrect sequence of handling the zones could trap the robot. An example of this special problem is shown in Figure 5 ​. Here the blue strips are to be painted and the robot starts at one edge of the map which is its docking zone. The robot could instantly start painting but would end up in trapped on the other end of the map. So, it should understand that even though travelling to other end of the and then starting to paint involves more work, it prevents chances of getting trapped with no rescue options.

![Coverage Area with Discontinuities]({{site.baseurl}}/assets/images/coverage/f5.png ) <br> *Coverage Area with Discontinuities*

* The coverage zones are smaller than the robot footprint and navigation to such zones has only one approach. Such a problem could be seen in ​ Figure 6​.


![Coverage Area With zones with area less than robot footprint]({{site.baseurl}}/assets/images/coverage/f6.png ) <br> *Coverage Area With zones with area less than robot footprint*

All such special problems of coverage firstly need the robot to have a clear understanding of the mapping information and then start the decomposition into viable, individually approachable zones. 

The different mapping techniques include:

* Metric or Topological maps where the complete area is placed on a 2D coordinate frame and any point in the area is mapped with a particular position in the frame, either using cartesian or polar representation. While Cartesian presentation helps represent discrete points, polar representation helps in comparing robot’s current heading and distance with respect to origin with that of the target and thus aligns with navigation tasks’ necessities

* Grid based maps are where the complete are is divided into several square grids of predefined size, generally equal to the robot footprint. Since areas need not be perfectly rectangular and thus can’t have finite grids; the smaller sections are represented as a part of the grid with smaller sections of varying granularity that cover all tiny zones.

* Certain maps could also be built to overlay on the standard maps. Such a representation would be having the distances between landmarks as certain nodes on the map while the obstacle free path between them represents a traversable path called an arc.

Based on the mapping used, the robot needs to identify the best decomposition of the coverage area such that each smaller version is individually addressable and it encompasses the complete coverage area without missing zones. Following techniques are proposed to reduce the coverage area into simpler accessible zones.

#### Boustrophedon Decomposition

Here, the complete map is subdivided into several parallel strips that can be covered using the zig-zag motion that covers area equal to the width of the robot footprint. This eases out robot’s motion in each individual strip as it simply supposed to cover each strip once and that zone of the coverage area is worked upon. However, this is easily applicable easily to polygonal areas with right-angled edges no awkwardly angled edges exist on the strip. ​Figure 7 shows a comparative illustration of where this decomposition would work or where it might not work.

![]({{site.baseurl}}/assets/images/coverage/f7.png )

#### Trapezoidal Decomposition

Just like the above decomposition, here we could use trapezoidal shapes to divided the coverage area into simpler zones that can be traversed using the zig-zag motion. However, this tends to create several unnecessary smaller sections that could have been essentially merged and used in the above technique.

#### Rectangular sub-sections with grids of variable granularity for remaining zones of non-standard dimensions - A subclass of Boustrophedon Decomposition

As the heading suggest, we try to break the coverage area into large unoccupied with obstacle zones that can be covered easily by the robot’s sweeping or cyclic motion(to be discussed later). It is tried that such sections’ edges align with the polygonal edges and the broken zones allow traversal with between adjacent ones. There should exist a path that connects adjacent sections

#### Random zones for random motion

This is the easiest technique to be implemented in coverage problems where the map is divided into random zones or shapes larger than the robot footprint and the robot could make random sweeps within each of them. Theoretically, as time tends to infinity(very large time span of operation), all points would have been covered. This technique is the most extravagant one and just a theoretical approach to improve upon.