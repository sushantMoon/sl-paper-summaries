# Multiple Instance Learning : A survey of problem characteristics and applications

**Authors : Marc-ANdre Carbonneau, Veronika Cheplygina, Eric Granger, Ghyslain Gagnon**

Notes from the paper are written below.

## Abstract

Multiple Instance Learning (MIL) is a form of weakly supervised learning where the training instances are arranged in sets, called bags, and a label is provided for the entire bag.

In this paper,

MIL problem characteristics are grouped into four broad categories,

1. The composition of the bags.
2. The types of the data distribution.
3. The ambiquity of the instance labels.
4. The task to be performed.

Methods specialized to address each of the category are reviewed.

Then the extend to which these characteristics manifest themselves in key MIL application areas are described.

## 1. Introduction

A limited understanding of such fundamental problem (MIL, weakly labeled dataset) characteristics affects the advancement of MIL research in many ways. Experimental results can be difficult to interpret, proposed algorithms are evaluated on inappropriate benchmark datasets and results on synthetic data often do not generalize to real world data.

This paper provides a comprehensive survey of the characteristics inherent to MIL problems, and investigates their impact on the performance of MIL algorithms. These problem characteristics are all related to unique features of MIL, namely the ambiquity of the instance labels and the grouping of data in bags. We propose to organize problem characteristics in four broad categotries:

1. Prediction level : As the instances are grouped in bags predictions can be performed at two levels, instance-level or bag-level. `(On classification with bag, groups and sets. V. Cheplygina 2015)`
2. Bag Composition : Proportion of instances from each class and the relation between the instances affects the MIL methods.
3. Label Ambiquity : This ambiquity can be related to label noise as well as to instances not belonging to clearly defined classes. `(A review of multiple instance learning assumptions. J. Flouds, 2010)`
4. Data Distribution : The shape of positive and negative distribution affect MIL algorithms depending on their assumptions about the data.

## 2. Multiple Instance Learning

### 2.1. Assumptions

Two broad categories for the assumptions are, standard and collective.`(A review of multiple instance learning assumptions. J. Flouds, 2010)`

**Standard Assumptions and Variants**

Standard assumption states that all the negative bags contain only negative instances and positive bag contains atleast one positive instance, also called witness.

Let $`X`$ be the bag defined as a set of features vectors, or instances, then $`X = \{x\_1, x\_2, ... , x\_N\}`$. Each instance $`x\_i`$ in feature space $`\Psi`$ can be mapped to a class by some process,or function, $`f : \Psi \rightarrow {0,1}`$, where the negative and positive classes correspond to 0 or 1 respectively. So the bag classifier $`g(X)`$ is defined as,

```math
g(X) = \begin{cases}
    1 &\text{if } \exists x \in X : f(X) = 1 \\
    0 &\text{otherwise}
\end{cases}
```
This was working assupmtion for `Solving the multiple instance problem with axis-parallel rectangles. T.G. Dietterich, 1997`, `Support Vector Machines for multiple-instance learning. S. Andrews, 2002`, `A framework for multiple-instance learning. O.Maron, 1998`, `Robust multiple instance learning ensembles using random subspace instance selection. M.A. Carbonneau, 2016`, `A sphere description based approach for multiple instance learning. Y.Xiao, 2017`

The standard assumption can be relaxed to address problems where positive bag cannot be identified by a single positive instance but by a distribution, interaction or accumulation of the instances it contains.

One variant would be, there needs to be certain minimum number ,$`\theta`$, of positive instances for a bag to be classified as positive.

```math
g(X) = \begin{cases}
    1 &\text{if } \theta \le \sum_{x \in X} f(X) \\
    0 &\text{otherwise}
\end{cases}
```

`(A review of multiple instance learning assumptions. J. Flouds, 2010)` gave an example for the above variant.

**Collective Assumption**

A more general case of collective assumptiom is when the bag is defined positive based on instances belonging to more than one concept. One case can be a mthod which assigns instances to a set of defined concepts $`(C)`$, and some of these concepts belong to positive class $`(C^{+} \subset C)`$, then the bag classifier is defined as,

```math
g(X) = \begin{cases}
    1 &\text{if } \forall c \in C^{+} : \theta_{c} \le \sum_{x \in X} f_c(x) \\
    0 &\text{otherwise}
\end{cases}
```
where $`f_c(x)`$ is a process that outputs 1 if $`x`$ belongs to concept $`c`$ and $`\theta_c`$ is the number of instances belonging to $`c`$ required to observe a positive bag.

In this paper, the *collective assumption* designates all the assumptions in which more than one instance is needed to identify a positive bag.

### 2.2. Tasks

1. **Classification** : It can be done at two levels, bag and instance. Loss functions for both would be very different and performance of one method on bag classificaion is not representative for instance classification.
2. **Regression** : It consists of assigning a real value to a bag (based on single instance or collective assumption or weighted average of multiple instances) or instance (based on which instance is the best fit or closest to the target concept)
3. **Ranking** : The goal is not to obtain real valued label, but to compare tha magnitude of scores to perform sorting. It can be done on bag level or instance level.
4. **Clustering** : This task consists in finding clusters or structure among the set of unlabeled bags or even among the instances within each bag.

## 3. Studies on MIL

