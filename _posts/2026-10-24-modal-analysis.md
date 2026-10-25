---
layout: post
title: Modal Analysis
subtitle: Structural Resonance of Structures
description: How boundary conditions fix a structure's mode shapes and natural frequencies — from the equation of motion to the frequency relation f = ωn / 2π.
cover-img: /assets/img/mode-shapes.svg
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

Static structural analysis is purely a function of the stiffness. However, the dynamic behavior of a system is governed by mass, damping, and its stiffness. For an undamped system, its free vibration would be characterized by the following equation: 

$$m\ddot{u} + k u = 0 \tag{2}$$

Equation 2 has a solution of the following form. For brevity we will skip the derivation of the solution. 

$$u(t) = C_1 \sin(\omega t) + C_2 \cos(\omega t) \tag{3}$$

 $\omega_n$ is the angular natural frequency of the system and for a single degree of freedom (*sdof*) problem, this  is a function of the stiffness and mass as shown below in Equation 4. 

$$\omega_n = \sqrt{\frac{k}{m}} \tag{4}$$

The angular natural frequency is converted to the linear frequency (usually just called frequency) using the relation below.

$$ f = \frac{\omega_n}{2\pi} \tag{5}$$

### Hand Calculation of Beam Natural Frequency

For a uniform beam, the first bending natural frequency can be predicted with the following equation: 
$$f_1 = \frac{\lambda_1^2}{2\pi L^2}\sqrt{\frac{EI}{\rho A}} \tag{6}$$

The value of $\lambda$ is determined by the boundary conditions.

<div class="center-table" markdown="1">

| End Condition | $\lambda$ |
| :---: | :---: |
| Fixed-Free | 1.8751 |
| Fixed-Fixed | 4.7300 |

</div>

### Modal Analysis in NASTRAN
Modal analysis in NASTRAN is called SOL 103 or SEMODES. 



### Summary
In summary, a static analysis depends only on stiffness, whereas the dynamic response adds mass and damping to the problem. The boundary conditions set which mode shapes are possible and at what frequencies they occur, and the lowest elastic mode — the first above the rigid body modes of an unconstrained structure — typically dominates the response to vibration.
