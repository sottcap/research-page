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
* $$D$$ ~ 6 nm
* $$\epsilon$$ ~ 0.5 kT
* charge ~ 1 - 10e
* $$\gamma$$ 

# In reduced units #
* reduced charge ~ $$ q \sqrt{4 \pi \epsilon_{0} D \epsilon}^{-1} = q \times 0.3419712276$$
* reduced bond length
* reduced mass = 1
* $$gamma$$ = $$6 \pi \eta a$$, $$\eta = 0.89Pa \cdot s = 0.89 kg/m \cdot s = 890 10^{27}kg/nm \cdot ps$$
* $$\eta$$ in reduced unit = $$ 890 \times \tau \times D / M$$


## Hoomd tutorial ##
[Jupyter notebook](https://nbviewer.jupyter.org/github/joaander/hoomd-examples/blob/master/index.ipynb)