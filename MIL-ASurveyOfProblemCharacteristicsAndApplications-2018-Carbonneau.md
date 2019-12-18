# Multiple Instance Learning : A survey of problem characteristics and applications

<b>Authors : Marc-ANdre Carbonneau, Veronika Cheplygina, Eric Granger, Ghyslain Gagnon</b>

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

## Introduction

A limited understanding of such fundamental problem (MIL, weakly labeled dataset) characteristics affects the advancement of MIL research in many ways. Experimental results can be difficult to interpret, proposed algorithms are evaluated on inappropriate benchmark datasets and results on synthetic data often do not generalize to real world data.

This paper provides a comprehensive survey of the characteristics inherent to MIL problems, and investigates their impact on the performance of MIL algorithms. These problem characteristics are all related to unique features of MIL, namely the ambiquity of the instance labels and the grouping of data in bags. We propose to organize problem characteristics in four broad categotries:

1. Prediction level : As the instances are grouped in bags predictions can be performed at two levels, instance-level or bag-level. `(On classification with bag, groups and sets. V. Cheplygina 2015)`
2. Bag Composition : Proportion of instances from each class and the relation between the instances affects the MIL methods.
3. Label Ambiquity : This ambiquity can be related to label noise as well as to instances not belonging to clearly defined classes. `(A review of multiple instance learning assumptions. J. Flouds, 2010)`
4. Data Distribution : The shape of positive and negative distribution affect MIL algorithms depending on their assumptions about the data.



