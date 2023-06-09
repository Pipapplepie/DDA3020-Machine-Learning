# Decision Tree

## Motivition

Till now, we have learnt 3 **parametric models**; linear regression, logistic regression, and SVM. (they are also supervised learning models) Their **limitations**:

1. The adopted model is determined by the trainer, which may be far from the ground-truth relationship between the input and the output.

2. The dicision/ prediction is difficult to understand/ explain.

Thus, we introduce **nonparametric models**, for example, KNN classification model, and decision tree (DT). They don't need strong assumptions and the data are allowed to speak for themselves. 

## Definition of DT

_Def._ DT is a **hierarchical** nonparameric model for supervised learning whereby the local region is identified in a sequence of **recursive spilits**. 

In a **univariate** tree, in each internal node, the test uses only one of the input dimensions.

<img src="https://user-images.githubusercontent.com/107236740/224930552-207ad562-ad75-49e7-990d-309d3d2d7356.png" width="500">

## (Univariate) Tree Learning

Tree induction (also Tree Learning or Growing) is the construction of tree given a training set.

**Goal:** For a given set, there are many trees that code it with no error, but we are only interested in the **smallest tree**. (the tree size is measured by # nodes in the tree and the complexity of the decision node.)

**Difficulty:** Finding the samllest tree is NP-hard. (Quinlan, 1968)

## Build the Tree

1. Select an attribute and split the data into its children in a tree;
2. Continue splitting with available attributes;

**Until,**

3. Leaf node(s) are pure (only one class remains);

  Or, A maximum depth is reached;
  
  Or, A performance metric is achieved.
  
The tree is constructed in a  **recursive** way, but: What is the **best attribute**? What is the **best split**?

### Best Attribute:

**Impurity Measure Rule**: the attribute that has the **largest reduction of impurity**.

Impurity:

$$\hat{P}(C_i|x,m) = p_m^i = \frac{N_m^i}{N_m}$$

This means for node m, $N_m$: # training instances reaching node m.

$N_m^i$ of $N_m$ belong to $C_i$, i = 1,...,k with $\sum_i N_m^i = N_m$.

Node m is **pure** if $p^i_m$ for all i are either 0 or 1.

### Impurity Measure:

1. For classifiction tree, the goodness of split/ impurity can be quantified by the **classification error**.
i.e., 1 - max(p, 1-p)

2. **Entropy** (for multi-class node): $I_m = - \sum_{i=1}^K \ p^i_m  log_2 p_m^i$.

3. **Information Gain**: 

<img src='https://user-images.githubusercontent.com/107236740/229416962-4031c671-26ba-4ccb-81b6-2670344d6eae.png' width=650>

Often, we exploit the relationship: **I(x;y) = H(x) - H(x|y)** to compute the **information gain**.

e.g.,

<img src='https://user-images.githubusercontent.com/107236740/229418962-e68e83bf-f3b9-42fd-bd7f-bc8592e5bfd1.png' width=600>

We want to choose the attribute that contributes **the largest information gain**!

<img src='https://user-images.githubusercontent.com/107236740/229420893-155df1c4-1d1f-494e-b099-7a7234ce8ca9.png' width=400>

### Common Impurity Measures for Binary Problem

- Entropy: $\phi (p) = - \sum_{i=1}^K \ p_i  log_2 p_i$

- Gini Index: $\phi (p) = \sum_{i=1}^K \ p_i(1 - p_i) = 1 - \sum_{i=1}^K \ p_i^2$

- Misclassification Error: $\phi (p, 1-p) = 1 - max(p, 1-p)$

<img src='https://user-images.githubusercontent.com/107236740/229420176-4a806c29-9a59-489a-a817-d644cf90db30.png' width=550>

## Regression Trees

For regression modelling, our measure for the "goodness of the split" is **mean squared error (MSE)** or the **sum of squared errors. (SSE)**

where MSE within each leaf $e = \frac{\sum_{i=1}^n \ (y_i - \bar{y})}{n}$.

Total MSE $S = \sum_{m \in leaves(Tree)} \ e_m$

The **prediction** for leaf c is $\bar{y}_c$.

<img src='https://user-images.githubusercontent.com/107236740/229423640-e2496b5a-1afb-4294-b648-6a82697a850d.png' width=500>

<img src='https://user-images.githubusercontent.com/107236740/229423688-c466284e-3c15-4448-aa61-e24243f88a83.png' width=700>

### Overfitting

<img src='https://user-images.githubusercontent.com/107236740/229425161-ce04df72-9d9c-4a64-b916-5459073289be.png' width=400>

### Pruning

Idea: Split the training data further into training and validation sets. Grow the tree based on the training set, and evaluate its impact on validation set. Greedily remove the node that most improves validation set accuracy.

<img src='https://user-images.githubusercontent.com/107236740/229425268-8369a2f4-3ba5-441a-85b3-29c119363fb8.png' width=600>

## Multivariate Trees
