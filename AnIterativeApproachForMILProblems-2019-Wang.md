# An Iterative Approach for Multiple Instance Learning Problem

    <b>Authors : Kaili Wang, Jose Oramas, Tinne Tuytelaars</b>

    Written are the points which felt important.

## Abstract

    The sugessested method iteratively looks into and analyzes set elements enabling the proposed model to update the set representation so that it reflects whether relevant elements have been detected and whether the underlying structure has been matched.

## Introduction

    Most common and standard assumption for MIL problems, states that a set is positive if it contains at least one positive (generally refered as witness) element otherwise negative.

Challenges faced by MIL,

1. The label of a set can be defined as a function of specific instance level characteristics of the elements that compose it.
2. The label of a set can be defined as the function of the relationships occuring between the constituent elements.

As many relationships are possible between the elements the second scenario constitutes a more challenging problem.

The proposed method on high level follows 2 step method,

1. Given a set of elements, each of the element is encoded by an `Instance Descriptor Unit`.
2. Each of the feature encoded is passed to the `Iterative Set Pooling Unit`. This unit is tasked with embedding and iteratively aggregating all the information from the different elements into a set level representation.

By analysis of the author, following were the obeservtions,

1. Model several MI assumptions, eg. single, multiple witness element detection, counting or collective assumptions.
2. It can address classification as well as regression problems.
3. Results are competetive or superior to state-of-the-art.
4. With deeper analysis of the `Iterative Set Pooling Unit` suggests that it is capable of highlighting, internally, the element or group of element that triggers the given predictions.

Contributions :

1. A novel iterative method powered with feedback mechanisms that is capable of modelling the underlying assumptions/relationships that characterizes the elements in a set without the need of explicit heuristics.
2. A frame work for classification and regression.
3. An approach to address MIL problems powered with explainability capabilities.


## Multiple Instance Assumptions

1. <b>Standard Multiple Instance Assumption</b>

    Given a set X_j = {x_1, x_2, ... ,x_m} of instances x_i with latent instance-level labels C_j = {c_1, c_2, ... ,c_m}, traditional MIL problems aim at prediction of binary set-level labels y_j for each X_j.

    A set X_j is positive, i.e. y_j = 1, iff, at least one of the instances x_i that compose it statisfies a predefined desired property alpha.

    `y_j = (1 if there exist x_i belonging to X_j where c_i = alpha) OR (0 if for all x_i belonging to X_j, no c_i = alpha)`

2. <b>Collective Multiple Instance Assumption</b>

    As opposed to standard's single element possessing certain property, in collective, all the elements x_i contribute equally to the predicted set label.

    `y_j = (1 if Prob( y_j | X_j ) > tau OR) (0 otherwise)`

    tau is the threshold value and set-level score Prob( y_j | X_j ) is computed from the contributions Prob( c_i=alpha | x_i ) of each of the m elements x_i as follows:

    `Prob( y_j | X_j) = 1/m summation where i goes from 1 to m ( Prob( c_i=alpha | x_i ) )`

    Weighted sum of Prob( c_i=alpha | x_i ) is also possible, if suppose w(x_i) is weight of x_i element on the set level score and z = summation of i goes from 1 to m ( w(x_i) )

    `Prob( y_j | X_j ) = 1/z summation where i goes from 1 to m ( w(x_i) * Prob( c_i=alpha | x_i ) )`

3. <b>Rank Based MI Assumption</b>

    This assumption assumes that there esist a property r(.) for every x_i in the set under which the elements ,or a subset of them, can be ranked on a fixed order. Taking the property r() into account, a set is positive if its elements follow a specific order (as in sequential data), otherwise negative.

    `y_j = (1 if r(x_1) < r(x_2) < ... < r(x_m) ) OR (0 otherwise)`


## Proposed Method

Given a set of X_j's for may j, we want to predict y_j, where X_j = {x_1, x_2, ... , x_m}.

In this method, Each of the x_i is encoded into a feature representation f_i through `Instance Description Unit`. Then each of the element level representation f_i is fed to `Iterative Set Pooling Unit`, producing aggregated set representation S_j. Finally, a prediction y_j_hat is obtained by evaluating the set representation via the `Prediction Unit`.

### Instance Description Unit

Each of the instance x_i ,in X_j, in its original format is fed to feature encoder which generates instance-level representation f_i.

Now this feature encoder depends on the modality of the data to be processed.
Some are,

1. VGG or ResNet features for still images.
2. Word2Vec or TF-IDF for text data.
3. Rank-pooled features (Fernando 2016) of dynamic images (Bilen 2018) for video data.

### Iterative Set Pooling Unit

The main goal of this component is to derive a set-level representation S_j,from instance level representation F_j = {f_1, f_2, ... , f_m}, of X_j.

In this unit, for each F_j, each of the element wise encoding f_i from i=1 to m are looked in ascending order one after another. In each iteration i, an updated set-level representation S{^i}_j is computed from f_i and previous set-level representation from (i-1)th iteration S{^(i-1)}_j, also a feed back loop takes it back as an input for the next iteration (Think recurrent networks). Finally after all the m instances are observed, S_j = S{^m}_j.

This is done cause set-level representation from previous instances can be very much useful to calculate more informed set-level representation of the current instance.

While this iteration and feed-back loop suggest at a sequence like structure requirement within each of the set X_j, the emperical observations by the authors strongly suggest that it is not a hard constraint.

Authors used Bi-LSTM for their purpose.

### Prediction Unit

From the set level representation S_j, now depending on the task at hand we need to use appropriate function g(.), which can be used to calculate y_j_hat, `y_j_hat = g(S_j)`

### Explaining Model Prediction

To know which of the x_i of X_j contributed most for making the prediction y_j_hat, each of the set level representation after each iteration i.e. each of S{^i}_j is stored. Then it can be checked which of the S{^i}_j is contributing most to the S_j. This can also be verified by calculating `y{^i}_j_hat = g(S{^i}_j)` and relating it with y_j_hat.





