---
layout: post
category : notes
title: Learning with errors
tags : [machine learning, caltech course, mooc]
comments: on
languages: en
---

These notes are written in English and refer to the fantastic Caltech online course you can find here: <http://work.caltech.edu/telecourse.html>. It is also worth noting you can find it on iTunes U, and if you have an iPad this makes a fantastic combo :-) The book is here: <http://www.amazon.com/gp/product/1600490069>. I make ample use of Yaser's material, including linking the relevant lecture PDF in each note and using his pictures (this is much faster than drawing stuff myself). Please note this is just for personal use and I give ALL the due credit to him!

A disclaimer on my notes in general: they are meant for my personal use and, although I'd love to know they helped somebody else, they are not written with clarity for third parties in mind. However, if you do use them and you would like to point out any errors, please write me an email!

#Learning and error

RELEVANT SLIDES: [Lecture 4](/assets/CaltechML/lecture4.pdf)

The learning diagram as we left it:

![learning diagram](/images/notes/learningdiagram2.png)

Now, we are going to expand on it a lot more.

###Error measure: theory

The first part that was overlooked last time was our error measure (or performance measure). To us, "doing well" in the task of learning means that we find some function $$ h $$ for which $$ h \approx f $$, where $$ f $$ is the target function (unknown). However, you can say a function $$ h $$ is doing badly or well only with respect to a certain error metric.

Therefore, there must exist (in general) an __error measure__ $$ E(h, f) $$ which is 0 when $$ h = f $$ and increseases if the two functions are "different". However, this definition is too general: $$ E(h, f) $$ is not a function itself, but a functional. It is not a object easy to deal with, and therefore we always resort to a _pointwise error metric_, $$e(h(\textbf{x}), f(\textbf{x})) $$, where $$ \textbf{x} $$ is a point.

Examples of pointwise error are the squared error in regression and the binary error in classification:

Squared Error: $$ e(h(\textbf{x}), f(\textbf{x})) = (h(\textbf{x}) - f(\textbf{x}))^2 $$

Binary error: $$ e(h(\textbf{x}), f(\textbf{x})) = \begin{cases} 1 & \mbox{if }  h(\textbf{x}) \neq f(\textbf{x})  \\ 0  & \mbox{if } h(\textbf{x}) = f(\textbf{x}). \end{cases}   $$

To obtain a overall $$ E(h, f) $$ we average the pointwise errors $$ e(h(\textbf{x}), f(\textbf{x})) $$ for all the examples we have got.

In-sample error:

$$ E_{in}(h) = \frac{1}{N} \sum_{i = 1}^m e(h(\textbf{x}_i), f(\textbf{x}_i)) $$

where each example $$ \textbf{x}_i \in \Re^n $$ ($$n$$ is the number of features).

Out-of-sample error:

$$ E_{out}(h) = {\mathbb E}_x [e(h(\textbf{x}), f(\textbf{x}))] $$

Notice that this time we don't get a specific point in the training set $$ \textbf{x}_i $$ but instead we pick a completely generic point $$ \textbf{x} \in X $$. Now, instead of a computer average on the sample, we compute the __expected value__ of the error by using the probability distribution generating the examples (like we did in [the previous article about feasibility](/notes/feasibility-of-learning)).

The difference is subtle but crucial: $$ E_{in} $$ is the _frequency_ of errors (in the sample), while $$ E_{out} $$ is the _probability_ of error (in the input space $$ X $$).

We can now add this to the learning diagram:

![learning diagram](/images/notes/learningdiagram3.png)

###Error measure in practice: precision and recall

The error measure need not be symmetric. Sometimes __precision__ and __recall__ are much more important. For example:

![error1](/images/notes/error1.png)

In case a supermarket uses this to quickly identify customers without needing them to use cards, we can assume that pissing a customer is far more costly than giving them a discount he did not reject $$ \Rarrow $$ prefer __recall__ to precision.

![error2](/images/notes/error2.png)

In case the CIA uses this, they definitely prefer to shut down an authorized officer a few times (and have another one try instead if need be) than having an intruder stealing their secrets!

![error3](/images/notes/error3.png)

The take-home lesson is that __the error measure should be specified by the user__. Only the client knows what it wants.

However, when this is not possible, you can resort to:

__Plausible__ measures: squared error is the best when the noise is Gaussian

__Friendly__ measures: closed-form solution, convex optimization.

This causes another addition to the learning diagram:

![learning diagram](/images/notes/learningdiagram4.png)

###Noisy data

Machine Learning deals with real data, which often involves people. This means that there can be inconsistencies we may have to deal with. 

For example, if we were to build a machine learning system for credit card approval, we may have two "identical" customers (two customers whose features have the very same values) and still have one labeled as "approved" and the other labeled as "rejected". After all, two different people made the two decisions, and maybe it was a close call. If this is the case, then we have a different value for the same point! This means that the target function $$f$$ is not really a function!

The theory can be (slightly) stretched to accommodate these problems.

Instead of a target function $$ f(\textbf{x}) $$, we now think of a _target distribution_ $$ P(y\| x) $$.

The couple example and output $$(\textbf{x}, y) $$ is now generated by the joint distribution $$ P(\textbf{x}) P(y\| x) $$.

NOTE: My website does not support a single bar \| inside math mode. Just consider $$\|$$ as being \|.

Our previous deterministic target $$ f(\textbf{x}) $$ is included in this theory by defining
$$ P(y\|\textbf{x}) = f(\textbf{x}) + n(\textbf{x}) $$, where $$ n(\textbf{x}) $$ is the noise "responsible" for the confusion. We also define $$ f(\textbf{x}) = {\mathbb E}(y\|\textbf{x})$$ (in other terms, we assume the noise is zero-averaged and symmetric).

The deterministic case is still there: it is sufficient to assume $$ n(\textbf{x}) = 0 $$.

Guess what? This changes the learning diagram once more:

![learning diagram](/images/notes/learningdiagram5.png)

There is an important distinction between these distributions:

![distrib](/images/notes/distrib.png)

###Wrapping up

Let us wrap up what we know so far.

The aim of the game of learning is to find a function $$g$$ such that:

$$ g \approx f $$ (nevermind about the noise now)

This in turn means that we want

$$ E_{out}(g) \approx 0 $$

$$ E_{out}(g) \approx 0 $$ is achieved through:

1. $$ E_{out}(g) \approx E_{in}(g) $$
2. $$ E_{in}(g) \approx 0 $$

The first point is achieved through sound statistics about significativity of the training set, while the second is achieved through a good learning algorithm.

Learning is thus split into 2 questions:

1. Can we make sure that $$E_{out}(g)$$ is close enough to $$E_{in}(g)$$? This is also called __generalization__.
2. Can we make $$E_{in}(g)$$ small enough? This is also called __fitness__ of the model.

###Next steps

![theorynext](/images/notes/theorynext.png)





