---
layout: post
title: Modal Analysis
subtitle: Structural Resonance of Structures
description: Modes, frequency, MEMF
cover-img: /assets/img/telecom.png
thumbnail-img: # 
share-img: #/assets/img/path.jpg
tags: [Modes]
author: Biman Mondal
---

### Introduction
Determining a structure's modes is the basis of many vibrational analyses in engineering i.e. the modes of a structure determine how a system behaves under vibrational load. The fundamental mode is the first and lowest natural frequency of a given structure. 

The mode shape is the shape a structure takes at a given modal frequency. For a beam the first mode is a vertical diving board behavior motion. For a simple plate the first mode is usually the trampoline mode with a peak and trough at the center of the plate. 

The boundary conditions, the manner by which the structure is constrained, affect the mode shape and the frequency of the modes of the structure. An unconstrained structure is often called 'free-free' condition. 

In 3D space, a structure has six degrees of freedom (up/down, forward/back, left/right and the rotations about those axes roll, pitch and yaw). The first six modes of an unconstrained structure are called rigid body modes and have natural frequencies at or nearly at zero. 

### Fundamental Equations

The dynamic equation of motion for a single degree of freedom structure is given by the following equation.

$$m\ddot{u} + c\dot{u} + ku = F(t) \tag{1}$$

*Variable Definitions*:

<div class="center-list" markdown="1">

   - m: mass
   - c: damping
   - k: stiffness
   - $\ddot{u}$: acceleration ( $\frac{d^2u}{dt^2}$ )
   - $\dot{u}$: velocity ( $\frac{du}{dt}$ )
   - u: displacement
   - F(t): force

</div>

Static structural analysis is purely a function of the stiffness. However, the dynamic behavior of a system is governed by mass, damping, and its stiffness. For an undamped system, it's free vibration would be characterized by the following equation: 

$$m\ddot{u} + k u = 0 \tag{2}$$

Equation 2 has a solution of the following form. For brevity we will skip the solution. 

$$x(t) = C_1 \sin(\omega t) + C_2 \cos(\omega t) \tag{3}$$

 $\omega_n$ is the angular natural frequency of the system and for a single degree of freedom (*sdof*) problem, this  is a function of the stiffness and mass as shown below in Equation 4. 

$$\omega_n = \sqrt{\frac{k}{m}} \tag{4}$$

The angular natural frequency can be converted to the linear frequency ( usually just called frequency) is $\omega_n$



### Summary
