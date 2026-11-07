---
layout: post
title: Analyzing Beams
subtitle: Shear-Moment Diagrams
description: Beam deflection, slope, shear, moment and bending stress derived from the Euler-Bernoulli equation.
cover-img: /assets/img/beam-deflection.svg
thumbnail-img: # 
share-img: #/assets/img/path.jpg
tags: [Beam]
author: Biman Mondal
---

### Introduction
One of the fundamental skills in structural analysis is to understand beam deflection and force distribution with shear-moment diagrams. Whenever there is a technical question in an interview to demonstrate knowledge, over 50% of the time for me it has been a beam question. There are countless sources of knowledge, both online and in print, which go deep into the subject of simple Euler-Bernoulli beams to Timoshenko Beam theory. This page is my personal understanding of how beams behave.

### Fundamental Mechanics
The Euler-Bernoulli equation describes the relationship between deflection and load distribution across the span of the beam. The fourth order differential equation gives the deflected shape of the beam under a distributed load q(x).

**Beam Static Deflection**

$$\frac{d^2}{dx^2}(EI\frac{d^2w(x)}{dx^2}) = q(x) \tag{1}$$

<div class="center-list" markdown="1">

   * x: length along the beam
   * w(x): deflection of the beam
   * E: material's Young's Modulus
   * I: area moment of inertia
   * q(x): distributed load per unit length of beam

</div>

The slope of the beam is defined by differentiating the deflection with respect to the length x.

$$ \theta = \frac{dw}{dx} \tag{2}$$

### Beam Loads

A beam can carry three main loads: an axial load, a shear load, and bending moment. 

**Beam Shear Load**

The shear load is defined as the derivative of the moment with respect to x.

$$ V(x) = -\frac{dM}{dx} = -(EI\frac{d^3w}{dx^3}) \tag{3}$$

**Beam Bending Moment**

The bending moment of a beam has the following definition:

$$ M(x) = -(EI\frac{d^2w}{dx^2}) \tag{4}$$

A beam is sized by looking at its loading, primarily by shear and moment diagrams, which take *w(x)* and evaluate the functions above.

### Beam Stress

**Shear Stress**

The shear stress $\tau$ is a function of the shear load $V$.

$$ \tau = \frac{VQ}{Ib} \tag{5}$$

<div class="center-list" markdown="1">

   -    V: shear load
   -    Q: first moment of area ( $Q = \int y\,dA$ )
   -    I: area moment of inertia
   -    b: vertical thickness

</div>


**Beam Bending Stress**

The bending stress in a beam is calculated as the moment (M(x)), multiplied by the distance from the neutral axis (y) divided by I, the area moment of inertia of the beam. The stress due to bending runs along the length of the beam.

$$ \sigma = -\frac{My}{I} \tag{6}$$

Note that if there is an axial load on the beam, this stress is simply $P/A$. The total normal stress in a beam is thus the sum, given by adding that normal stress to the stress caused by bending.  

$$ \sigma_{\text{axial,tot}} = \frac{P}{A} \pm \frac{My}{I} \tag{7}$$

**Natural Frequency**

The natural frequency, the first resonating tone of the beam, takes the following form. The frequency is a function of the beam's bending stiffness $(k)$, which is proportional to the product of Young's modulus and area moment of inertia. 

$$ f = \frac{\beta}{2\pi L^2}\sqrt{\frac{EI}{\rho A}} \tag{8}$$

<div class="center-list" markdown="1">
   
   * E: material's Young's modulus
   * I: area moment of inertia
   * $\rho$: density of beam material
   * A: cross sectional area 
</div>

There are many forms of the function above and the value of $\beta$ is dependent on boundary conditions.


### Summary
In summary, I have covered some of the fundamental equations governing beams; a cornerstone of engineering structural designs. Euler-Bernoulli equation ties deflection, slope, shear, moment and bending stress together through successive derivatives of the deflected shape. 
