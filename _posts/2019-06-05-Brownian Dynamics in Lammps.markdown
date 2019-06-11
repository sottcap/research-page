---
layout: post
title: Brownian Dynamics in Lammps
date:   2019-06-05 10:18:00
categories: Lammps Molecular Dynamics
math-engine: MathJax
---

<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript">
</script>

Brownian dynamics is sometimes useful to simulate stochastic motions.
It is the high friction limit of Langevin dynamics (ie, massless) that enables us to take much larger time steps.

$$M \ddot{X} = - \del U \left(X \right) - gamma \dot{X} + \sqrt{2 \gamma k_{B} T} R\left( t\right)$$

where M is a mass, X is a position, $$\gamma$$ is a friction coefficient, $$k_{B}$$ is Boltzman coefficient.