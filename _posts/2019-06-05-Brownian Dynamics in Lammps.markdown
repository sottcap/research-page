---
layout: post
title: Brownian Dynamics in Lammps
date:   2019-06-05 10:18:00
categories: Lammps Molecular Dynamics
---

Brownian dynamics is sometimes useful to simulate stochastic motions.
It is the high friction limit of Langevin dynamics (ie, massless) that enables us to take much larger time steps.

<script type="math/tex">
M \ddot{X} = - \del U \left(X \right) - gamma \dot{X} + \sqrt{2 \gamma k_{B} T} R\left( t\right)
</script>

where M is a mass, X is a position, $\gamma$ is a friction coefficient, $k_{B}$ is Boltzman coefficient.