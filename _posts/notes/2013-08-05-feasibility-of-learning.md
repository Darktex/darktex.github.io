---
layout: post
category : notes
title: Feasibility of learning
tags : [machine learning, caltech course, mooc]
comments: on
---

These notes are written in English and refer to the fantastic Caltech online course you can find here: <http://work.caltech.edu/telecourse.html>. It is also worth noting you can find it on iTunes U, and if you have an iPad this makes a fantastic combo :-) The book is here: <http://www.amazon.com/gp/product/1600490069>. I make ample use of Yaser's material, including linking the relevant lecture PDF in each note and using his pictures (this is much faster than drawing stuff myself). Please note this is just for personal use and I give ALL the due credit to him!

A disclaimer on my notes in general: they are meant for my personal use and, although I'd love to know they helped somebody else, they are not written with clarity for third parties in mind. However, if you do use them and you would like to point out any errors, please write me an email!

# The problem of learning

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

##Refining the theory 1: feasibility

RELEVANT SLIDES: [Lecture 2](/assets/CaltechML/lecture2.pdf)

What the previous diagram lacks is an explanation about the __feasibility__ of the learning process. What we would like to have is a mathematical explanation to tell us _how well_ we can learn with the data we have.

###Hoeffding's inequality

To do that, we need a mathematical tool, __Hoeffding's inequality__. I failed to prove this formula, but the derivation carries nonetheless some interesting insights. It would be long to post here, so just look at [the note about the theory of Hoeffding's inequality](/notes/hoeffding-inequality/).

Here, we are just content with looking at the formula:


$$ P(\| \mu - \nu \| > \epsilon) \leq 2 e^{-2 \epsilon^2 m} $$

![bins](/images/notes/bins1.png)

__Notation:__ The notation for the formula is different here than in the note about Hoeffding's inequality. Here, we have $$ m $$ instead of $$ n $$ to be consistent with the notation I used before. You have $$ m $$ training examples, and this is the same $$ m $$ you want to plug in the formula.

This inequality is important because it puts an __upper bound__ on a __bad__ event (that the in-sample mean is too far away from the out-of-sample mean that we wanted to learn, i.e. our model sucks).

Now the question becomes: "How do I use this in learning?".

###Applying Hoeffding to the learning process

The learning process involves using a learning algorithm to search the space $$ H $$ (the __hypothesis set__), trying various $$ h $$ functions until it finds what it thinks is the best function, and call it $$ g $$ and output it.

However, the performance of $$ g $$ does not depend on this process alone: it depends on the __data__ as well (if not more!). For example, if you only have 1 training example, or if you have lots of useless data (for example, full of points that are all close to each other, but then you want to predict a point which is very far away), then there is no hypothesis set and no algorithm that will help you!

This is where __Hoeffding's inequality__ kicks in: instead of thinking about balls in a jar, we now think about how well a function can predict outcomes.

This time, the bin becomes the domain $$ X $$ and each marble ball is therefore a point $$ \textbf{x} \in X $$. We still define $$ \mu $$ as the fraction of green marble balls out of sample (in the whole $$X$$ now) and $$ \nu $$ as the fraction of green marble balls in sample (of length $$ m $$), but this time we change the  __meaning__ of the balls color. Now a green ball means $$ h(\textbf{x}) = f(\textbf{x}) $$ and a red ball means $$ h(\textbf{x}) \neq f(\textbf{x}) $$, therefore we see $$ f $$ and $$ h $$ as responsible of the coloring of the balls, altough not directly: none of them colors a ball alone, you need both to determine the color of the ball. They do not appear directly in the process: they are somewhere, like Platonic ideas, and together they influence the color of the marbles, which in turn give us a value of $$ \mu $$ for the whole bin and a value of $$ \nu $$ in each sample we draw. Notice how __the meaning of the accordance between $$ \mu $$ and $$ \nu $$ is not accuracy of the model, but rather accuracy of the TEST__. In other words, we use a test set of limited size and find out its performance $$ \nu $$. Then, Hoeffding will help us tell how indicative $$ \nu $$ is of the performance out-of-sample $$ \mu $$. Without this, there can be no __verification__, let alone learning!

Summing up:

all the marble balls in a bin -> $$ X $$

each marble -> $$ \textbf{x} \in X $$

green ball -> $$ h(\textbf{x}) = f(\textbf{x}) $$

red ball -> $$ h(\textbf{x}) \neq f(\textbf{x}) $$

However, __this is not learning__. Learning involves using an algorithm to search a space $$ H $$ and try different functions $$ h \in H $$. Here, we have already pick some specific function and are testing its performance on a sample, using maths to guarantee the accuracy of the test within some threshold we are willing to tolerate.

![bins](/images/notes/bins2.png)

###Moving on to learning

Since one bin is clearly not enough, we use more bins. Each bin contains exactly the same marble balls ($$X$$ is the same), but the __colors will be different__ because each bin will have a different function $$ h $$ associated with it ($$ f $$ of course remains the same). For now, we assume the bins are in limited number M[^limited].


![bins](/images/notes/bins3.png)


[^smoothness]: Long story short, smoothness requires that infinitesimal variations in the domain reflect in infinitesimal variations in the codomain. This can be expressed as a requirement of differentiability. For a more formal definition, look at Wikipedia: <http://en.wikipedia.org/wiki/Smoothness>.

[^def]: Later, this will be expanded to any general distribution.

[^limited]: Later, this will be expanded to a possibly infinite set.
