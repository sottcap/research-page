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
* $$D$$ ~ 2.98 nm
* $$\epsilon$$ ~ 0.5 kT
* $$q$$ ~ 1 - 10e
* $$\gamma$$ ~ 49967.45 $$\mathrm{nm^{2}/ps}$$
* $$M$$ ~ 675.78 Da

# In reduced units #
* Unit charge ~ $$ q \sqrt{4 \pi \epsilon_{0} D \epsilon}^{-1} = q \times 0.3419712276$$
* Unit bond length = 2.98 nm
* Unit mass = 675.78 Da
* Unit time = 69.59144 ps
* $$\eta$$ in reduced unit = $$ 890 \frac{\tau D}{M}$$ = 164.53
* $$\gamma$$ = $$6 \pi \eta a = 9241.9596$$

## Hoomd tutorial ##
[Jupyter notebook](https://nbviewer.jupyter.org/github/joaander/hoomd-examples/blob/master/index.ipynb)