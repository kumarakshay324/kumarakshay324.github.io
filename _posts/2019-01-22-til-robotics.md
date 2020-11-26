---
layout: post
title:  "Robotics"
categories: [ Robotics ]
tags: featured
---

I browse tons of robotics and related stuff everyday and now I will be dumping a short description of all that interesting stuff here! 

**Robotics is huge and I am not efficient enough to sort these topics appropriately until the D-Day is here!**

### null space optimization `(January 1, 2020)` 

Manipulator arms have several degrees of freedom, usually 6 or more. To attain a desired 3D cartesian pose, a robot arm needs to have atleast 6 degrees of freedom. Often the task may require using less than the 6 DoFs or a redundant manipulator may have spare DoFs not used actively. In either cases, the robot could use the remaining degrees of freedom to achieve secondary tasks and the possible motion space for the secondary task is called the robot null space. 

**Null Space Optimization** refers to the process of using the null space to augment the primary controller solution towwards a more refined solutions with secondary benefits. If a robot is supposed to obtain a 3D pose from the current pose, null space optimization could be used to find the IK solution that minimizes amount of energy the robot uses during the motion or find the IK solution that doesn't need the robot to flip over the elbow joint. For redundant robots, the second case is largely obsvered and null space optimization is employed to avoid singularities or other mischievous IK solutions. 

However, it is important to ensure that the secondary null space optimizer does not affect the primary controller and inhibit the attempt to achieve the primary goals. Hopefully I will soon read and write something more elaborate on this topic!

### impedance control `(December 10, 2019)` 

Robots and specially manipulators often interact with the environment and the nature of interaction is to be modeled for efficient robot performance. Knowledge of how the environment is going to react if the robot approaches it helps the robot decide its actions better. 

**Impedance control** is a robot control technique where the force-position relationship is defined for the interaction. The end of the manipulator is considered to have a virtual impedance defined by a spring-mass-damper system related by force and mass while the environment is considered to a have an admittance. 

For the manipulator, the end-effector force and cartesian coordinate positions are related by this equation to model the impedance 
<br> `Fext = K(Xdesired - X) + D(Ẋdesired - Ẋ) + M(Ẍdesired - Ẍ)` 

This external force is added to the dynamics model of the manipulator(in cartesian space) to selectively control positions and forces in different directions while robot-environment interaction.