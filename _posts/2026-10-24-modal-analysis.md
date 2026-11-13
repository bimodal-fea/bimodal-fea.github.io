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

<div align="center" class="center-table" markdown="1">

| End Condition | $\lambda$ |
| :---: | :---: |
| Fixed-Free | 1.8751 |
| Fixed-Fixed | 4.7300 |

</div>


### Modal Analysis of a Beam
Modal analysis in NASTRAN is called SOL 103 or SEMODES. 
Using EasyFEA, the same calculation is reproduced below.



**Input Parameters**

![beam input parameters]({{"/assets/post_figures/beam_modal_parameters.png" | relative_url }}){:style="width: 55%; height: auto; display: block; margin: 0 auto;"}

**Mesh**

The beam is discretised into 40 quadratic (`SEG2`) Euler–Bernoulli elements — 41 nodes and six degrees of freedom per node, three translations and three rotations, for 246 degrees of freedom in total. The cross-section is meshed separately because EasyFEA integrates the section properties from it: A = 625 mm², Iy = Iz = 32 552 mm⁴ and J = 65 104 mm⁴, giving a total mass of 4.91 kg.

![beam mesh]({{"/assets/post_figures/beam_modal_mesh.png" | relative_url }}){:style="width: 90%; height: auto; display: block; margin: 0 auto;"}

**Natural Frequencies**

Because the cantilever is clamped, K is positive definite and the eigenproblem is solved in shift-invert mode around σ = 0. Every bending frequency appears twice: the square section bends identically about y and about z, so the modes come in degenerate pairs.

![natural frequencies]({{"/assets/post_figures/beam_modal_frequencies.png" | relative_url }}){:style="width: 70%; height: auto; display: block; margin: 0 auto;"}

| Mode pair | Frequency (Hz) | Ratio to f₁ | Shape |
| :---: | ---: | :---: | :--- |
| 1–2 | 20.89 | 1.00 | first bending (y and z planes) |
| 3–4 | 130.9 | 6.27 | second bending, one node |
| 5–6 | 366.5 | 17.55 | third bending, two nodes |
| 7–8 | 718.3 | 34.39 | fourth bending, three nodes |

**Mode Shapes**

![beam mode shapes]({{"/assets/post_figures/beam_modal_mode_shapes.png" | relative_url }}){:style="width: 100%; height: auto; display: block; margin: 0 auto;"}

**Results**

The first mode lands at 20.89 Hz against 20.89 Hz from Equation 6 with λ = 1.8751, a relative error below 0.01 %. That is expected: a cubic Euler–Bernoulli element reproduces the static cubic deflection exactly and the consistent mass matrix converges quickly, so 10 elements already give the same frequency to four decimal places as 40.

Two checks are worth remembering. First, the higher modes follow the theoretical cantilever sequence 1 : 6.27 : 17.55 : 34.4 — if a model fails to reproduce those ratios, the usual culprits are the boundary conditions or the section properties. Second, the boundary condition dominates: clamping both ends replaces λ = 1.8751 by 4.73, and since the frequency scales with λ², the first mode rises by (4.73 / 1.8751)² ≈ 6.4× to roughly 133 Hz for the same beam.

Finally, Euler–Bernoulli ignores transverse shear, so it over-predicts the frequency of short, stubby members. That error becomes noticeable once the span-to-depth ratio falls below about 10; here it is 40, so the correction is negligible and a Timoshenko element would give the same answer to within rounding.

### Summary
In summary, a static analysis depends only on stiffness, whereas the dynamic response adds mass and damping to the problem. The boundary conditions set which mode shapes are possible and at what frequencies they occur, and the lowest elastic mode — the first above the rigid body modes of an unconstrained structure — typically dominates the response to vibration.
