---
title: "Primer on building ML solutions"
layout: post
category: technical
---

This week, we will introduce **high-level overview of building a Machine Learning (ML) solution** for a problem, summarized by the following diagram and demo'ed with [`scikit-learn`](http://scikit-learn.org/stable/index.html).
![](assets/img/week1-2.png)


***N.B.***{% marginnote 'mn-id-glossary' "Visit [MLglossary](https://hoamle.github.io/articles/17/machine-learning-appendix/#glossary) for a summary of the math notations. Because ML is an interdisplinary field, there are many ML terminologies that are equivalent. The MLglossary also lists common terms and their synonyms or strongly related concepts." %} We will gradually *rephrase* every-day language with equivalent ML terminologies and their *math notations*. 

Don't be afraid of Math, embrace it. Math is (1) an **efficient, universal and unanimously understood** language. Once we rephrase a problem in mathematical toungue, we may see hidden  connections between numerous of *supposedly* unrelated problems in different fields [[ref-DAslides-pp22-38](https://1drv.ms/b/s!ApOZHae4ogqZ3AJg76xtDPEzSlH-)]. Further more, Math is (2) **non-ambiguous** so that we can approach a solution of a problem with transparent and concrete reasoning. Nevertheless, always explain the math we use (or encounter) in our usual natural language if possible, so that we can imprint the **underlying intuition** and not getting lost in the technical details that follow.


## Case-study

<font color="blue"><strong> <em>Identify a flower type based on its attributes
</em>
 </strong> </font>, *such as petal length, sepal width, ...*

Ref: [http://scikit-learn.org/stable/tutorial/basic/tutorial.html](http://scikit-learn.org/stable/tutorial/basic/tutorial.html)

![](assets/img/Petal-sepal.jpg)
(*"which flower is this?" - photo from [bing](https://www.bing.com/images/search?view=detailV2&ccid=E8dlW334&id=690CFCA2C5419961A77E0534DC3B6AD1B61FA711&q=sepal&simid=608048017631022285&selectedIndex=5&ajaxhist=0))*
 

**Experience** i.e ***Training data***: `iris` dataset - a dataset that contain information about certain types of flower 


```python
from sklearn import datasets 
iris_dataset = datasets.load_iris()
```

First, study our data, so that we can **pre-process** the data provided. In this step, we might need to manipulate the raw data to extract important information, or normalize following certain standard. The purpose is (but not limited to) to prepare the data in proper formats for later implementation.

For demonstration purpose, we are using a "*clean"* dataset (already stored in structured format, no missing or suspicious values), so we only need to do minimal data pre-processing. Reminded that it is mostly *not* the case in practice [[ref-DAslides-p11](https://1drv.ms/b/s!ApOZHae4ogqZ3AJg76xtDPEzSlH-)].

### Study the data

Read the "docs" i.e. data description


```python
# print(iris_dataset)
print(iris_dataset['DESCR'][:1000])  # the "doc" is quite long, so I 
                                  # only extract the first 1000 
                                  # characters for demonstration purpose    
```

    Iris Plants Database
    
    Notes
    -----
    Data Set Characteristics:
        :Number of Instances: 150 (50 in each of three classes)
        :Number of Attributes: 4 numeric, predictive attributes and the class
        :Attribute Information:
            - sepal length in cm
            - sepal width in cm
            - petal length in cm
            - petal width in cm
            - class:
                    - Iris-Setosa
                    - Iris-Versicolour
                    - Iris-Virginica
        :Summary Statistics:
    
        ============== ==== ==== ======= ===== ====================
                        Min  Max   Mean    SD   Class Correlation
        ============== ==== ==== ======= ===== ====================
        sepal length:   4.3  7.9   5.84   0.83    0.7826
        sepal width:    2.0  4.4   3.05   0.43   -0.4194
        petal length:   1.0  6.9   3.76   1.76    0.9490  (high!)
        petal width:    0.1  2.5   1.20  0.76     0.9565  (high!)
        ============== ==== ==== ======= ===== ====================
    
        :Missing Attribute Values: None
      
    

* There are 150 examples i.e. *data points*
* Each flower is described by $P=4$ attributes i.e. ***features*** or *predictors*: `sepal length` ($x_{1}$), `sepal width` ($x_{2}$), `petal length` ($x_{3}$), `petal width` ($x_{4}$). 
* All 4 features' measures are conceptually similar (numeric, real values that lie in the same domain), so no **data normalization** required.
* There are $K=3$ types i.e. **classes** of flower, which are `setosa`, `versicolor`, and  `virginica` - represented by ID `0`, `1`, `2` respectively. Note: each flower is ***labelled*** by a *single* ID, indicating that a flower can only be member of 1 type.




```python
print(iris_dataset['data'].shape)  
# each row in `iris_dataset['data']` is 
# a feature vector of the respective flower

print(iris_dataset['target_names'])
print(iris_dataset['target'])
```

    (150L, 4L)
    ['setosa' 'versicolor' 'virginica']
    [0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
     0 0 0 0 0 0 0 0 0 0 0 0 0 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
     1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2 2
     2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
     2 2]
    

We write the features as a feature vector $x=\left(x_{1},x_{2},x_{3},x_{4}\right)^{T}$. Vector $x$ is a **representation** of a flower i.e. a summary of this flower attributes. We extract and store all feature vectors to a 2D-array $X$, where the $n$-th row is feature vector $x^{\left(n\right)}$. 

{% sidenote 'sn-id-2d' "`2D-array` can be understood as a table-like data structure" %}

*<font color="red">Note</font>*: In this course, we use capital letters e.g. $X$ to represent set of data points rather than a matrix as usual. If we imply the latter, it should be clear from the context.




```python
D = {}
D['X'] = iris_dataset['data']
print(D['X'].shape)
```

    (150L, 4L)
    

We extract and store all the labels to an 1D-array $Y$, where the $n$-th element indicates flower type $y^{\left(n\right)}$. *<font color="red">Note</font>*: the order of all $n$'s in $Y$ must match with the counterparts in $X$.

{% sidenote 'sn-id-labels' "In actual implementation (which we won't see in this week example), $Y$ is almost always converted to an equivalent 2D-array implicitly, where each column is a binary indicator (e.g. {1, 0}) of a respective class in all examples." %}


```python
D['Y'] = iris_dataset['target']
print(D['Y'].shape)
```

    (150L,)
    

Now we can define our problem more precisely by the language of math

### Define the problem

Given any attribute $x$, we would like to **predict** a corresponding prediction $\hat{y}\in$  {`setosa`, `versicolor`, `virginica`} by a ML **Model**. In order to know if our model has good predictive performance, we need an **Assessment** to measure the performance.  In this problem, we can measure the performance by an ***evaluation metric*** called [*Accuracy*](http://scikit-learn.org/stable/modules/model_evaluation.html#accuracy-score), which

$$\text{Accuracy}=\dfrac{1}{N}\sum_{n}\mathbb{1}\left(\hat{y}^{\left(n\right)}=y^{\left(n\right)}\right)$$

The value of this metric increases every time we correctly identify a flower type. A prediction is correct if predicted type $\hat{y}$ of a flower is the same as its actual type $y$.

![](assets/img/week1-1.png)
*<font color="red">Note</font>*: while Accuracy is appropriate for this particular problem, other problems may require some other evaluation metric {% marginnote 'mn-id-metrics' "Many problems require 2 or more metrics for an objective assessment." %} For example, in case wewant to identify whether a patient has cancer or not, we may want to minimize the risk of missing true cases (patients who actually have cancer - True Positive cases) as much as possible. In this case, [*Recall*](http://scikit-learn.org/stable/modules/model_evaluation.html#precision-recall-f-measure-metrics) is a better measure of performance than Accuracy.

In order to build a model that perform well, we need to **train** it by utilizing the *experience* that the model has. In other word, the model needs to improve its performance by *learning* from the *training data* $\mathcal{D}_{\text{train}}=\left\{ x^{\left(n\right)},y^{\left(n\right)}\right\}$ from an initial "naive" state. This task is called, unsurprisingly, ***learning***, and is also commonly called ***fitting***. 
![](assets/img/week1-2.png)

{% marginnote 'mn-id-knn' "*k-nearest neighbours* - a common ML algorithm - is an exception such that the algorithm virtually does not perform any kind of learning. While the algorithm has its own mertis, it does not scale to address high-dimensional inputs or non-trivial semantic recognition problems. Read more: [[ref-cs231n](http://cs231n.github.io/classification/#nn)]" %}


A ML algorithm is not only required to perform well on the training data, but also on the *new, unseen data* that it has never encountered (i.e. not in the training set). Those unseen data that could be used to assess a model performance are called ***test data***. High performance on test data is what we aim for, because it is an indicator for the model's ability to  **generalize** to arbitrary data examples.

For demonstration purpose, we will use a small subset of `iris` dataset as test data. The remaining will serve as training data.  



```python
# Randomly pick 20% of the examples as test data, and train
# on the remaining 80%.

from sklearn.cross_validation import train_test_split
# note: sklearn 0.18 moved `train_test_split` to 
# `sklearn.model_selection` module 

indicies = [i for i in xrange(len(iris_dataset['data']))]
train_idx, test_idx = train_test_split(indicies, train_size=0.8,
                                     random_state=1)  
# Each time we run `train_test_split`, a new split is produced 
# randomly and is different from the previous run. Therefore, 
# it is essential to assign a `random_state` to make our work 
# reproducible on other machines or for later use. 

# Use capital letter e.g. `X` to indicate set of data points.
D_train = {'X': D['X'][train_idx],
           'Y': D['Y'][train_idx]
           }
D_test = {'X': D['X'][test_idx],
         'Y': D['Y'][test_idx]
        }
print("Test set size: {} examples".format(len(test_idx)))
```

    Test set size: 30 examples
    

In this week example, we demo the `Model` box(es) in above diagrams with a model called ***Softmax Regression***. For now, we can simply understand Softmax Regression as a "black-box" ML algorithm that can do our prediction problem. *"What are assumptions on model structure? How was learning task done? Can we do better than standard Softmax Regression?, etc"* are the topics for next weeks.


```python
from sklearn.linear_model import LogisticRegression
# Softmax regression is a multi-class generalization of 
# Logistic Regression model

# initialize a "naive" model
model = LogisticRegression(multi_class="multinomial",
                          solver="lbfgs")  
```

### Learning


```python
model.fit(D_train['X'], D_train['Y']);  # after `.fit`, the model has finished its learning
```

Learning finished! 

### Prediction
Now try indentifying a new, unseen flower with feature $x^{\left(\text{test}\right)}$


```python
x_test = D_test['X'][0]
print(x_test)
```

    [ 5.8  4.   1.2  0.2]
    


```python
y_pred = model.predict(x_test)  
print(y_pred)
```

    [0]
    

    C:\Users\hoa\Anaconda2\lib\site-packages\sklearn\utils\validation.py:386: DeprecationWarning: Passing 1d arrays as data is deprecated in 0.17 and willraise ValueError in 0.19. Reshape your data either using X.reshape(-1, 1) if your data has a single feature or X.reshape(1, -1) if it contains a single sample.
      DeprecationWarning)
    

### Assessment

Our model `predict`s that the flower whose petal and sepal size are as described by $x^{\left(\text{test}\right)}$ is a "setosa" (`id: 0`). ***Is this true?***


```python
print(y_pred == D_test['Y'][0])
```

    [ True]
    

Good news! But what about prediction for other flowers?


```python
Y_pred = model.predict(D_test['X'])

print("Flower\tPredict\tActual\tCorrect prediction?")
for i in xrange(len(test_idx)):
    print("{}\t{}\t{}\t{}\t".format(
            test_idx[i], 
            Y_pred[i],
            D_test['Y'][i],
            Y_pred[i] == D_test['Y'][i]
        ))
```

    Flower  Predict Actual  Correct prediction?
    14  0   0   True    
    98  1   1   True    
    75  1   1   True    
    16  0   0   True    
    131 2   2   True    
    56  1   1   True    
    141 2   2   True    
    44  0   0   True    
    29  0   0   True    
    120 2   2   True    
    94  1   1   True    
    5   0   0   True    
    102 2   2   True    
    51  1   1   True    
    78  1   1   True    
    42  0   0   True    
    92  1   1   True    
    66  1   1   True    
    31  0   0   True    
    35  0   0   True    
    90  1   1   True    
    84  1   1   True    
    77  2   1   False   
    40  0   0   True    
    125 2   2   True    
    99  1   1   True    
    33  0   0   True    
    19  0   0   True    
    73  1   1   True    
    146 2   2   True    
    

Our model correctly indentifies 29 examples and makes 1 errors out of 30 testing examples, achieving an Accuracy of $\dfrac{1}{N}_{\text{test}}\sum_{n}\mathbb{1}\left(\hat{y}^{\left(n\right)}=y^{\left(n\right)}\right)=29/30=96.7\%$ 




```python
sum(Y_pred == D_test['Y']) / float(len(test_idx))
```




    0.96666666666666667



*(comment: The performance is pretty impressive, but let hold off from a pre-matured assessment! See [Conclusion](#conclusion))*

## <a href="#conclusion">Conclusion</a>

To summarize, we have completed the most basic steps to build a ML solution for our problem as specified by this diagram
![](assets/img/week1-2.png)

Specifically, we used and trained a Softmax Regression `Model`, and did `Assessment` on a *single* split of test set. However, there still exist *fundamental* questions that we need to address:
1. Is $96.7\%$ a *reliable* estimate for our model accuracy on **other test sets**? {% sidenote 'sn-id-assess' "TODO link to Lecture 4" %}
1. How is Softmax Regression model **constructed**? {% sidenote 'sn-id-buildmodel' "TODO link to Lecture 2" %}
1. In a problem for which **assumptions** imposed by Softmax Regression model do ***not suffice***, how can we do better? {% sidenote 'sn-id-nonlinear' "TODO link to Lecture 3" %}
1. *(other issues that would arise when approaching above questions)*


These questions will define the topics for next parts of this series.
