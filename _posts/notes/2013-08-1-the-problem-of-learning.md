---
layout: post
category : notes
title: The problem of learning
tags : [machine learning, caltech course, mooc]
comments: on
---

These notes are written in English and refer to the fantastic Caltech online course you can find here: <http://work.caltech.edu/telecourse.html>. It is also worth noting you can find it on iTunes U, and if you have an iPad this makes a fantastic combo :-) The book is here: <http://www.amazon.com/gp/product/1600490069>. I make ample use of Yaser's material, including linking the relevant lecture PDF in each note and using his pictures (this is much faster than drawing stuff myself). Please note this is just for personal use and I give ALL the due credit to him!

A disclaimer on my notes in general: they are meant for my personal use and, although I'd love to know they helped somebody else, they are not written with clarity for third parties in mind. However, if you do use them and you would like to point out any errors, please write me an email!

#The problem of learning

RELEVANT SLIDES: [Lecture 1](/assets/CaltechML/lecture1.pdf)

The problem of learning can be defined as that of learning some _function_[^def] we don't know but of which we have some data points. 

There are some basic hypotheses that need be satisfied before one can (or should) rely to a machine learning approach:

1. A pattern must exist in the data we have. If there is no pattern, there is nothing to learn.
2. We cannot pin this pattern down mathematically (for example, why should you use machine learning to predict how long an object takes to fall in the vacuum? You already have formulas for that).
3. We have __enough data__ on it. This is the less trivial of the three and it is worth a thorough discussion because we don't know what "enough" means. How much is it? A function has an __infinite__ number of points in its domain and we cannot possibly comprehend all of them, therefore if we were to resort to binary logic we should always say that there is __never__ enough data. However, if we accept a more fuzzy approach, we can say that __the performance of the machine learning model is strongly correlated with the amount of data we have__. If (and only if) we accept the possibility of getting some predictions (slightly) wrong, then we can learn. This approach falls under the name of __PAC__, "Probably, Approximately Correct"[^valiant].

[^valiant]: The definition comes from Prof. Leslie Valiant. Look at <http://www.amazon.com/dp/0465032710/ref=rdr_ext_sb_ti_sims_2>.

To express our notation and pin down some concepts, let us focus on a simple example: say we are a bank and we want to have a machine learning system handle credit card applicants.

In this problem, we have:

- __Each applicant__ is formalized as an input vector $$ \textbf{x} $$
- The decision for each applicant is a scalar $$ y \in \{0, 1\} $$ (reject, accept)
- The target function is $$ f : X \rightarrow Y $$, where $$ X \in \Re^n $$ and $$ Y \in \{0, 1\} $$.

Following this formalism, all the data relevant to previous customers is in the form $$ (\textbf{x}_1, y_1), (\textbf{x}_2, y_2), \dots, (\textbf{x}_m, y_m). $$

### Classification of machine learning problems

In general, a machine learning problem is regarded as:

- A _regression problem_ when $$ y $$ is _real-valued_ and can therefore assume an infinite amount of values. Time-series predictions in stocks fall in this category.
- A _classification problem_ when the domain of $$ y $$ is composed by a finite and __pre-determined__ number of "buckets" (for example, you may want to classify stuff among 5 classes. The number "5" is pre-determined). A common case is __binary classification__, like the one in this example.

The problem is also classified with respect to the form of the input:

- We have a __supervised learning__ problem when we have data in the form $$ (\textbf{x}_1, y_1), (\textbf{x}_2, y_2), \dots, (\textbf{x}_m, y_m) $$ i.e. we have information about $$ y $$ in the training set.
- We have a __unsupervised learning__ problem when we have data in the form $$ \textbf{x}_1, \textbf{x}_2, \dots, \textbf{x}_m $$ i.e. we have __no information__ about $$ y $$ - "Here is my previous data, please find some patterns in it". Clustering and anomaly detection fall in this category.
- We have a __reinforced learning__ problem when we don't have direct information about $$ y $$, but we do have an indication of how we performed, like "good" or "bad". This is used in chess AI, where you learn whether a move was good or bad by judging what happened later, or maybe in robotics when you have to make a robotic arm "learn" how to move.

Needless to say, there categories are orthogonal. For example, the credit card application problem is a supervised learning, binary classification problem. In general, we will focus on __supervised learning__ and __classification__ because they have generally more interesting applications.

This brings us to our first learning framework diagram.

![diagram1](/images/notes/learningdiagram1.jpg)

There is an extra element we did not talk about, which is the learning algorithm. There are multiple learning algorithms and we can expect some of them to be better than others for a certain application (this is the case). The choice of the algorithm involves making some __a priori__ assumptions about the form of your data (smoothness being probably the most common and the most general[^smoothness]). All these assumptions _restrict_ the domain in which we pick our hypotheses (i.e. our candidate functions) to a certain domain $$H$$. We pick many candidate functions $$ h \in H $$ and feed them to the learning algorithm which will elect (what it thinks it is) the __best__ function and our final hypothesis, $$g$$.

[^unionbound]: Formalization and proof: <http://en.wikipedia.org/wiki/Union_bound>

[^smoothness]: Long story short, smoothness requires that infinitesimal variations in the domain reflect in infinitesimal variations in the codomain. This can be expressed as a requirement of differentiability. For a more formal definition, look at Wikipedia: <http://en.wikipedia.org/wiki/Smoothness>.

[^def]: Later, this will be expanded to any general distribution.

[^limited]: Later, this will be expanded to a possibly infinite set.