---
layout: post
title: Analyzing Beams
subtitle: Shear-Moment Diagrams
description: Beam deflection, slope, shear, moment and bending stress derived from the Euler-Bernoulli equation — the foundation for the hand calculation and FEA comparison that follow.
cover-img: /assets/img/telecom.png
thumbnail-img: # 
share-img: #/assets/img/path.jpg
tags: [Beam]
author: Biman Mondal
---

### Introduction
One of the fundamental skills in structural analysis is to understand beam deflection and force distribution with shear-moment diagrams. Whenever there is a take home question in an interview to demonstrate knowledge, over 50% of the time for me it has been a beam question.

### Fundamental Mechanics
The Euler-Bernoulli equation describes the relationship between deflection and load distribution across the span of the beam. The fourth order differential equation gives the deflected shape of the beam under a distributed load q(x).

**Beam Static Deflection**

$$\frac{d^2}{dx^2}(EI\frac{d^2w}{dx^2}) = q(x)$$

Where I is the area moment of inertia, E represents the Young's modulus, w(x) deflection on the beam as a function of x along the length of the beam, and q(x) is the distributed load per unit length of the beam.

The slope of the beam is defined by differentiating the deflection with respect to the length x.

$$ \theta = \frac{dw}{dx} $$

**Beam Shear Load**

The shear load is the differential of the moment with respect to x.

$$ V(x) = -\frac{dM}{dx} = -(EI\frac{d^3w}{dx^3}) $$

**Beam Bending Moment**

The bending moment of the beam is given by the following:

$$ M(x) = -(EI\frac{d^2w}{dx^2}) $$

**Beam Bending Stress**

The normal stress in a beam is calculated as the moment (M(x)), multiplied by the distance from the neutral axis (y) divided by I, the area moment of inertia of the beam.

$$ \sigma = -\frac{My}{I} $$

**Natural Frequency**

$$ f = \frac{1}{2\pi}\sqrt{\frac{k}{m}} $$


### Results from FEA


### Summary
