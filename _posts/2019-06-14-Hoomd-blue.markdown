---
layout: post
title: Hoomd-blue Summary
date:   2019-06-14 07:00:00
categories: Hoomd Molecular Dynamics
math-engine: MathJax
---

<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript">
</script>

## Units ##
* distance - $$D$$
* energy - $$\epsilon$$
* mass - $$M$$
* temperature - reduced ($$T^{*} = \frac{kT}{\epsilon} $$)
* charge - reduced $$ \sqrt{4 \pi \epsilon_{0} D \epsilon } $$
* time - $$ \sqrt{\frac{M D^{2}}{\epsilon}} $$

## In mAbs ##

# In real units #
* $$D$$ ~ 1.53 nm
* $$\epsilon$$ ~ 1.0 kT
* $$q$$ ~ 1 - 10e
* $$M$$ ~ 1351.56 Da

# In reduced units #
* Unit charge ~ $$ q \sqrt{4 \pi \epsilon_{0} D \epsilon}^{-1} = q \times 0.169
* Masses in resduced unut ~ 1 for Hinge, 23 for Fv and CH1, and 9 for CH2 and CH3.
* Unit time = $$\sqrt{M D^{2}/\epsilon}$$ = 35.7 ps when $$epsilon=kT in RT=4.114pN\cdot nm$$
* $$\gamma$$ = $$6 \pi \eta a = 9241.9596$$

## Hoomd tutorial ##
[Jupyter notebook](https://nbviewer.jupyter.org/github/joaander/hoomd-examples/blob/master/index.ipynb)