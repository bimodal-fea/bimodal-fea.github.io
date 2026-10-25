---
layout: post
title: Analyzing Beams
subtitle: Shear-Moment Diagrams
cover-img: /assets/img/telecom.png
thumbnail-img: # 
share-img: #/assets/img/path.jpg
tags: [Beam, ]
author: Biman Mondal
---

<script type="text/javascript" id="MathJax-script" async
  src="https://jsdelivr.net">
</script>
</script>

### Introduction
One of the fundamental skills in structural analysis is to understand beam deflection and force distribution with shear-moment diagrams. Whenever there is a take home question in an interview to demonstrate knowledge, over 50% of the time for me it has been a beam question.

### Fundamental Mechanics
Euler-Bernoulli equation describes the relationship between deflection and load distribution across the span of the beam. The fourth order differential equation gives the 

**Beam Static Deflection** </break>

$$\frac{d^2}{dx^2}(EI\frac{d^2w}{dx^2}) = q(x) $$

Where I is the area moment of inertia, E represents the Young's modulus, w(x) deflection on the beam as a function of x along the length of the beam, and q(x) is the distributed load per unit length of the beam.

The slope of the beam is defined by differentiating the deflection with respect to the length x.  

$$ \theta = \frac{dw}{dx} $$


**Beam Shear Load** </break>

The shear load is the differential of the moment with respect to x.

$$ V(x) = -\frac{dM}{dx} = -(EI\frac{d^3w}{dx^3})  $$

**Beam Bending Moment** </break>

The bending moment of the beam is given by the following:


$$ M(x) = -(EI\frac{d^2w}{dx^2}) $$
 
**Beam Bending Stress**</break>

The normal stress in a beam is calculated the moment (M(x)), multiplied by the distance from the neutral axis (y) divided by I the area moment of intertia of the beam.

$$ \sigma = -\frac{My}{I}) $$


### Deflection Of A Beam



### Hand Calculation


### Results from FEA


### Summary
