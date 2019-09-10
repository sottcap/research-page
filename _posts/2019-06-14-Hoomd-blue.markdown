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
* $$M$$ ~ 2703.02 Da

# In reduced units #
* Unit charge ~ $$ q \sqrt{4 \pi \epsilon_{0} D \epsilon}^{-1} = q \times 0.165e$$
* Masses in resduced unit ~ 1 for Hinge, 23 for Fv and CH1, and 9 for CH2 and CH3.
* Unit time = $$\sqrt{M D^{2}/\epsilon} = 35.7 ps$$ when $$\epsilon=kT$$ in $$RT=4.114pN\cdot nm$$
* $$\gamma$$ = $$6 \pi \eta a = 2.566e-11 kg/s = 204.433 M/tau$$

## Hoomd tutorial ##
[Jupyter notebook](https://nbviewer.jupyter.org/github/joaander/hoomd-examples/blob/master/index.ipynb)

## Bug fixes and notes ##
Unfortunately, HOOMD-Blue contains critical bugs that totally mess up the BD simulations running on GPU.
Most of bugs were fixed by me but one thing should be noted. 
Tutorial says you can just set bonds types by bond_type = ['bond1', 'bond2'] but it doesn't work because of bugs.
It can be correct in the future but easier way is to explicitly set the bond_typeid like bond_typeid[bi] = 0 for all bonds.