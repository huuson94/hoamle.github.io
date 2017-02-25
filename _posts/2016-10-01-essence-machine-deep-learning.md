---
layout: post
title: "Essence of Machine Learning (and Deep Learning)"
date: 2016-10-01
category: technical
---
Preliminary course for new members at DSLab-HUST. Pre-requisite for courses in *Topic models* and (supervised) *Deep neural networks*. 

This short course aims to introduce new starters to the field of *Machine Learning* (ML) with a principled approach, so that ones can understand the motivation and intuition behind ML (and eventually *Deep Learning* - DL) concepts,  later learn advanced materials \*efficiently\*, catch up with recent advances in the field, and be ready to do ML research and/or industrial applications.

*Intended learning objectives*: (i) understand and know what constitute of the high-level ML concepts below; (ii) be able to navigate new ML concepts in [the Map of Machine Learning](#map); (iii) - *optionally* - articulate the math behind each model or concept, and implement the ML models/algorithms covered in the course properly (expected from students who do the homework and ["Study-group" sessions](#study))

## <a name="map">Core ML concepts</a>
{% marginnote 'mn-map' 'TODO draw the Map' %} We will cover the following concepts. <font color="red">Note</font>: if not stated otherwise, concepts in ***bold italic*** are covered in the prelim course. [Course notes](#notes) is be expected in respective blog posts. 

### Build a Machine Learning model
**Design principle**: Model {% sidenote 'sn-model' '*"Model is a simplification of reality"*. Formulate real-life problems as ***parametric models*** (non-parametric models/methods are not covered in this training course series)' %} = Model "Structure"{% sidenote 'sn-structure' 'Relationships between model elements: data, parameters, and hyperparameters.  Relationships can either be *deterministic* or *stochastic*, and are visualized graphically by ***graphical models***.' %} + Learning Framework{% sidenote 'sn-framework' 'Examples: ***probabilistic modelling***, *metric learning* (not covered in prelim course)' %}

***Learning task*** and ***Inference task(s)***{% sidenote 'sn-estimate' 'Find/compute point estimates of *unknown* parameters (*learning task*) of the model, and other quantities of interest (*inference tasks*), e.g. posterior distribution of model parameters, predictive outcomes, etc.' %} 

### Evaluate performance of a model

***Assessment metrics***: which metrics to measure the performance?

***Analyze results***: are the results meaningful{% sidenote 'sn-meaningful' 'in terms of *statistical* significance, interpretability, or interesting observation' %}  and legitimate{% sidenote 'sn-analyze' 'We will touch on ***experimental design***' %}? 

### Regularize a model
`>` to fight ***overfitting*** issue. Example approaches: weight penalty, ***Bayesian modelling***{% sidenote 'sn-bayes' 'We will also see Bayesian modelling, and eventually *Bayesian inference*, when building ***generative models*** for clustering problem' %}, Early-stopping, Data augmentation, Dropout; or

`>` to achieve some interpretability via *sparsity*{% sidenote 'sn-sparse' "covered in Topic Models course" %}; or

`>` to achieve [other objectives](https://en.wikipedia.org/wiki/Regularization*(mathematics)).

### Optimize for more performance
***Model selection*** and *Ensemble* techniques



## References
Course content is partially taken from the following sources:

> Christopher Bishop's [Pattern Recognition and Machine Learning](https://www.amazon.com/Pattern-Recognition-Learning-Information-Statistics/dp/0387310738) <- Comprehensive textbook on Probabilistic modelling with focus on Bayesian methods.

> Andrew Ng's Machine Learning class ([Coursera](https://www.coursera.org/learn/machine-learning) or [CS229](http://cs229.stanford.edu/)) <- Practical introduction to Machine Learning and common learning algorithms.

> Stanford Univ's [CS231n - ConvNet for Visual Recognition](http://cs231n.stanford.edu/) <- Practical course on Deep neural networks (DNN) with the context of computer vision problems.

> [Shakir Mohamed](http://shakirm.com/?section=3)'s tutorial on Deep Generative Models in Deep Learning Summer School, 2016 <- Terrific summary of modelling principles and categorization of model classes. Also introduce recent advances in marrying Probabilistic modelling with DNN. 


## <a name="study">Course logistics</a>
2 sessions/week: 1x "**Lecture**" session + 1x optional "**Study-group**" session.
`>` ***Lectures*** are meant to lead you in the right direction --- just to get your started. They are **not** meant to tell you *everything* in *every details*. 

> Therefore you should utilize the reference reading materials, online resources for missing details *<- (the role of **self-study**)*

`>` It should be reckoned that we do not know everything (in *many cases*, we don't even know what we don't know), so utilize the course instructors, the Teaching Assistant - TAs, your classmates for further support/discussion/...  *<- (the importance of **Study-group**)* 

> **Tip**: Use comment sections in *relevant* blog posts to reach this course instructor(s). The advantage: other audience (e.g. TAs, classmates, passing-by experts) can also contribute to your questions or discussion. Use email as secondary option.

## <a name="notes">Course notes</a>
WEEK 1 - [Introduction](https://raw.githubusercontent.com/hoamle/essence_ml/e788aef7617fed6911bcfd710ebbccd8ed34eae6/essence_ml.pdf) (with [Notes](https://raw.githubusercontent.com/hoamle/essence_ml/e788aef7617fed6911bcfd710ebbccd8ed34eae6/essence_ml_with_notes.pdf)) & [Primer on Building a Machine Learning solution](/articles/17/primer-on-building-ml-solutions)

WEEK 2 - Principles of Modelling: Model structure, Learning framework

WEEK 3 - Principles of Modelling: Regularization, "Deep" Model structure

WEEK 4 - Bayesian inference

WEEK 5 - TBE