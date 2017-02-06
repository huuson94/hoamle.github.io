---
layout: post
title: "Essence of Machine Learning (and Deep Learning)"
date: 2016-10-01
category: Technical
---
Training course for new members at DSLab. Pre-requisite for subsequent sessions in *Topic models* and (supervised) *Deep neural networks*. 

*Abstract*. There are literally *hundreds* of Machine Learning (ML) models/algorithms published every year. The field itself is also broad enough, with many sub-areas that require in-depth pre-requisites. While the current wave of AI/ML{% sidenote 'sn-mainstream' '(Deep Learning says "Hi")'%} has brought up numbers of ML study materials to wider audience than ever, it also create lots of noises, e.g. "sensational science" reads from mainstream articles and online discussion, or redundant "how-to" tutorials which usually neglect question "why". All of these may hinder aspiring starters who want to *get serious* on ML (and understand what Deep Learning - DL is and does exactly), making their learning pace not optimal.

This short course aims to introduce new starters to the field of ML with a principled approach, so that ones can understand the motivation and intuition behind ML (and eventually DL) concepts,  later learn advanced materials more efficiently, catch up with recent advances in the field, and be ready to do ML research and/or industrial applications.

*Intended learning objectives*: (i) understand and know what constitute of the high-level ML concepts below; (ii) be able to navigate new ML concepts in the [map of Machine Learning](#){% marginnote 'mn-map' 'TODO' %}; (iii) - *optionally* - articulate the math behind each model or concept, and implement them properly (expected from students who do the homework and join practical sessions)

## Core ML concepts
We will cover the following concepts (in ***bold italic***). Links to relevant [course notes]() to be updated. 

### Build a Machine Learning model
Principles of building a model

***Design***: Model {% sidenote 'sn-model' 'Formulate real-life problems as ***parametric models*** (non-parametric models/methods are not covered in this course)' %} = Data Type + Model "Structure"{% sidenote 'sn-structure' 'Relationships between model variables and parameters.  Relationships can either be *deterministic* or *stochastic*, and are visualized graphically by ***graphical models***.' %} + Learning Framework{% sidenote 'sn-framework' 'Examples: ***probabilistic modelling***, *metric learning* (not covered in this course)' %}

***Tasks***: Learning task and Inference task(s){% sidenote 'sn-estimate' 'Find/compute parameter point estimates (***learning task***) and other unknown quantities of interest (***inference tasks***), e.g. predicted outcome of a coin toss, full posterior distribution of model parameters' %} 

### Evaluate performance of a model

***Assessment metrics***: which metrics to measure the performance?

***Analyze results***: are the results meaningful{% sidenote 'sn-meaningful' 'in terms of *statistical* significance, interpretability, or interesting observation' %}  and legitimate{% sidenote 'sn-analyze' 'We will touch on ***experimental design***' %}? 

***Model selection***: which model to choose from, given a set of models with similar performance?

### Fight overfitting
To avoid low performance on unseen data examples. Example approaches: ***weight penalty***, ***Bayesian modelling***{% sidenote 'sn-bayes' 'We will also see Bayesian modelling, and eventually *Bayesian inference*, when building a generative model to cluster data' %}, *Dropout*, *Data augmentation* (not covered in this course)

## References

> Christopher Bishop's [Pattern Recognition and Machine Learning ](https://www.amazon.com/Pattern-Recognition-Learning-Information-Statistics/dp/0387310738)

> Andrew Ng's Machine Learning classes on [Coursera](https://www.coursera.org/learn/machine-learning) and [CS229](http://cs229.stanford.edu/)

> [Shakir Mohamed](http://shakirm.com/?section=3)'s tutorial on Deep Generative Models in Deep Learning Summer School, August 2016

> Stanford Univ's [CS231n - ConvNet for Visual Recognition](http://cs231n.stanford.edu/)

