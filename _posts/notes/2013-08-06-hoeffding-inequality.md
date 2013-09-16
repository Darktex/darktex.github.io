---
layout: post
category : notes
tags : [maths, machine learning, theory]
title: Hoeffding's inequality
languages: en
---

Consider a simple problem: we have a jar containing some red and blue balls like this:

![jar](/images/notes/jar.jpg)

We define the fraction of blue balls in the jar as $$ \mu $$. Next, we draw 1 ball from the jar, write down its color, put the ball back into the jar and repeat the whole process $$ m $$ times (we will call this action "Draw $$ m $$ balls with replacement"). We call the fraction of blue balls over the $$ m $$ balls we drew $$ \nu $$. What we want is a way to know how well can $$ \nu $$ track $$ \mu $$ or, in other terms, how well can the _in-sample mean_ $$ E_{in} $$ track the _out-of-sample mean_ $$ E_{out} $$.

Let's define $$ p $$ as the probability of getting a blue ball and $$ q = 1 - p $$ the probability of getting a red ball. Since we have replacement, the whole process is memoryless and therefore a [Bernoulli trial](http://en.wikipedia.org/wiki/Bernoulli_trial). We can then say that the probability of getting _exactly_ k blue balls in $$ n $$ draws is:

$$ P(k) = \binom n k p^k q^{n-k}$$

And the probability of getting _at most_ $$ k $$ blue balls in $$ n $$ draws is

$$ F(k;n,p) = \sum\limits_{i = 0}^k P(k) = \sum\limits_{i = 0}^k \binom n k p^k q^{n-k} $$

__Hoeffding's inequality__ states that: 

$$  F(k;n,p) \leq \exp\left(-2 \frac{(np-k)^2}{n}\right) $$

##Sketch of a (quasi)proof of Hoeffding's inequality 

I failed proving this myself (I get a slightly worse upper bound), but I can briefly sketch what I did to help you convince yourself this works.

By using [De Moivre-Laplace](http://en.wikipedia.org/wiki/De_Moivre%E2%80%93Laplace_theorem) we approximate the discrete series with an exponential[^stirling].

$$    {n \choose k}p^kq^{n-k}\simeq \frac{1}{\sqrt{2\pi npq}}e^{-\frac{(k-np)^2}{2npq}} $$ 
 
$$F(k; n, p) $$ is therefore: 

$$ F(k; n, p) = \sum\limits_{i = 0}^k {n \choose k}p^kq^{n-k}\simeq \sum\limits_{i = 0}^k \frac{1}{\sqrt{2\pi npq}}e^{-\frac{(np-i)^2}{2npq}} $$

Now, call $$\beta = \frac{1}{4pq} $$ and note that $$\beta > 1$$. Also, note that the coefficient is strictly less than 1. We then get:

$$ \sum\limits_{i = 0}^k \frac{1}{\sqrt{2\pi npq}}e^{-\frac{(np-i)^2}{2npq}} \leq \sum\limits_{i = 0}^k e^{-\frac{2\beta(np-i)^2}{n}}  $$

Now, note that when $$i$$ is growing, the negative exponent is shrinking and therefore:

$$ \sum\limits_{i = 0}^k \exp\left(-\frac{2\beta(np-i)^2}{n}\right) \leq k  \exp\left(-\frac{2(np-k)^2}{n}\right)  $$

I am not able to remove the $$ k $$ factor that separates my bound from that of Hoeffding's, but this should be enough to convince ourselves that the bound is true, where it comes from and thus reduce the height of the leap of faith required to accept it.

##Making this inequality useful in Machine Learning

We are not over yet. Now we want to use this formula to predict how much information about the out-of-sample mean we can get from the in-sample mean.

Before doing that, let us recap what we have so far. Recall that $$ k $$ is the amount of blue balls in $$ n $$ draws and that $$ p $$ is the probability of drawing a blue ball, while $$ F(k; n, p) $$ is the probability of getting _at most_ $$ k $$ draws.

Then, it follows that $$ k $$ is the in-sample mean of blue balls (integer) and $$ np $$ is the out-of-sample mean, being the expected number of blue balls (real-valued, not necessarily integer).

To make this useful, we set up a threshold $$ \epsilon $$ (not necessarily integer) on the probability we deduce from the sample. In other words, $$ \epsilon $$ is the maximum difference we can tolerate between the probability we get by dividing $$ k $$ by $$ n $$ and the ideal probability $$ p $$. We now want to obtain a measure of the probability of success when $$ k $$ is close to $$ np $$ by at most $$ \epsilon $$.

$$ \epsilon = \lvert p -  \frac{k}{n} \rvert$$.

This in turn means that we have two cases:

1. $$ \epsilon = p - \frac{k}{n} $$ 
$$ \Rightarrow k = n (p - \epsilon) $$.

    $$ F(n (p - \epsilon); n, p) \leq \exp\left(-\frac{2(np-n(p-\epsilon))^2}{n}\right) = \exp\left(-\frac{2n^2\epsilon^2}{n}\right) = \exp\left(-2n\epsilon^2\right) $$

2. $$ \epsilon = \frac{k}{n} - p $$ 
$$ \Rightarrow k = n (p + \epsilon) $$.

    $$ F(n (p + \epsilon); n, p) \leq \exp\left(-\frac{2(np-n(p+\epsilon))^2}{n}\right) = \exp\left(-\frac{2n^2\epsilon^2}{n}\right) = \exp\left(-2n\epsilon^2\right) $$

Point 2 is wrong, but I can't find why. [Wikipedia](http://en.wikipedia.org/wiki/Hoeffding%27s_inequality) points out that 2 should be the probability of drawing AT LEAST $$ k $$ blue balls, which should therefore be $$ 1 - F(n (p + \epsilon); n, p) $$. Also, $$ F(k; n, p) $$ must be symmetrical with $$ k = np $$ having the highest probability, therefore one should be able to assert that point 2 refers to drawing at least $$ k $$ blue balls, but I cannot pin this down mathematically :-(

Moving on, we have that the probability of taking LESS blue balls than $$ \epsilon $$ and that of taking MORE blue balls than $$ \epsilon $$ sum up (independent) and we obtain the final result:

$$ P(\| np - k \| > \epsilon) \leq  2 \exp\left(-2\epsilon^2 n\right) $$.


This formula is __non-asymptotic__ and can tell us how to quantify the relationship between $$ np $$ and $$ k $$ (and therefore between $$ \mu $$ and $$ \nu $$, or between $$ E_{out} $$ and $$ E_{in} $$).

[^stirling]: De Moivre-Laplace's formula uses [Stirling's approximation](http://en.wikipedia.org/wiki/Stirling%27s_formula) to convert the binomial coefficients into exponentials (in case you were wondering where the exponentials were coming from).

