---
title: "Principle of Modelling"
layout: post
---
{% maincolumn 'assets/img/model_structures.png' '' %}

> decision theory
> > pick highest of posterior p(y|x)
> > > reason: minimize

> parametric model -> parametric distribution: governed by a small number of adaptive parameters -> need estimate of unknown parameters
> > criterion: maximize likelhood p(y|theta)
> > > reason: desired property on (asymptotic) unbiasness and measurable low variance estimate

This weeks explains how Softmax Regression is built
## Motivation for statistical reasoning
There are several points of view to build an ML model that can achieve certain objective(s). In many case, statistical perspective provide a more complete viewpoint 

Powerful tools to predict/detect under uncertainty. All that task {marginnote "Read more: AI:IntroLecture"}

Follow statistcal reasoning would help us understand concretely why a model should work or not. Even for the models that were developed from non-probabilistic perspective (e.g. Neural Networks)

TODO Pre-requisites: 
- probability is a measure of uncertainty produced from one (or more) random process
- statistics

Watch TODO (Statistics re-explained)

## Case-study

Foundation: Decision theory {marginnote PRML:1.5}
* best predictions are which minimizing mis-classification rate (i.e. 1 - [Accuracy](ref-to-last-week)): predict y_hat = k* if k* = argmax P(y=k*|x)
* more generally, best predictions are which minimizing expected loss E[L] = error_weight * P(k*|x)

=> infer P(y|x) {marginnote "note on short-hand writing for `probability` of an outcome, and `probability distribution` of all outcomes"}

### Model structure

If no information provided i.e. P(y) {marginnote prior} =>  prior knowledge,  can be translated to the mathematical tools by using distribution P(y) to represent that knowledge => the distributions doing such thing is call **prior distributions**

If there is information provided i.e. P(y|x) {marginnote posterior} => update the model knowledge given more data to produce more accurate predicition => translated to the mathematical tools by using distribution P(y|x) => these distribution conditioned on more information are called **posterior distributions**

* score function: [[cs229:notes1:9,9.3]](TODO)

### Learning Framework

TODO why MLE?