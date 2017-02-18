---
layout: post
title: "Simple Language Model"
date: 2015-07-21
category: technical
---

This is an implementation of Geoffrey Hinton\'s Neural Networks Programming Assigment 2 on [Coursera](https://www.coursera.org/course/neuralnets) in Python with GPU support by Theano. The assignment was about training a feed-forward neural networks, in order to predict the next word from 3 previous words. Training took ~10s/epoch with default parameters on a GTX 660 GPU. On the other hand, training took ~100s/epoch on a Core 2 Duo E7300 @2.67GHz CPU with the original Octave/MATLAB implementation (10x slower!). 

Source code is on [GitHub](https://github.com/hoamle/Neural-Net-PA2). Any suggestions are welcomed. 

## Files in the repo
- `data.mat`: data file that includes training, validation, and testing set for the model
- `wordModel.ipynb`: IPython Notebook that records the main ingredients, notes, and thought when I built the implementation,
- `wordModel.py`: the implementation

## Usage
- Pre-requisites: Python 2.7+, Theano, CUDA 7 (optional, for training by GPU)
- Run `THEANO_FLAGS=mode=FAST_RUN,device=gpu,floatX=float32 python wordModel.py` in the terminal. Let `device=cpu` if you want to train by CPU.
    
## Issues
- `test_model` and `validate_model` compute `cost` (average cross-entropy) on batches of test set and validation set, not the whole sets respectively. Difference should not be significant though.
- Original momentum expression did not yield expeceted cross-entropy for some reason. I had to use an alternative from [Stanford Deep Learning Tutorial](http://ufldl.stanford.edu/tutorial/supervised/OptimizationStochasticGradientDescent/) (see Momentum section).

## References
- [deeplearning.net](http://deeplearning.net) tutorials and [this](http://nbviewer.ipython.org/github/craffel/theano-tutorial/blob/master/Theano%20Tutorial.ipynb#example-mlp) for building Python code.
- [Stanford Deep Learning Tuttorial](http://ufldl.stanford.edu/tutorial/supervised/OptimizationStochasticGradientDescent/)
