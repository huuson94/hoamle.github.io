---
layout: post
title: "Machine learning appendix"
date: 2017-03-01
category: Technical
---
*(to be updated sporadically)*

## Back-propogation algorithm
**For what**: computes gradient 
{% m %} 
\nabla_{\theta}J=\dfrac{\partial J}{\partial\theta} {% em %} for **all** {% m %} \theta 
{% em %}'s 
of interest. 
{% marginnote 'backprop-demo' "*Conditions*: (i) J is differentiable every where w.r.t. theta; (ii) J and all thetas form a directed acyclic computational graph. " %}


*Use case(s)*: update optimal parameter {% m %} \hat{\theta} {% em %}'s of a neural network (or a certain class of probabilistic models) by gradient descent algorithms; 

[[Demo](#)]{% marginnote 'backprop-def' "TODO" %}

