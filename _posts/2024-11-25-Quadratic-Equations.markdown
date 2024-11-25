---
layout: post
title: Quadratic Equations
date: 2024-11-25
categories: jekyll update
---

# Quadratic Equations

## Description

The formula you may familiar with:

$$
ax^2 + bx + c = 0
$$

And the solution is given:

$$
x_1 = \frac{-b + \sqrt{b^2 - 4ac}}{2a} \quad \text{and} \quad x_2 = \frac{-b - \sqrt{b^2 - 4ac}}{2a}
$$

But why how they mathematicians produced this solution formula?

## Prof

The idea and work through are all from the book [No bullshit guide to linear algebra](https://a.co/d/hqavzcX). It's very interesting

Ok let's work through it.

$$
ax^2 + bx + c = 0
$$

$$
ax^2 + bx = -c
$$

$$
x^2 + \frac{b}{a}x = -\frac{c}{a}
$$

Now from the left of expression, we'll use [_Complete the square_](https://en.wikipedia.org/wiki/Completing_the_square) method.

$$
(x - h)^2 + k = x^2 + \frac{b}{a}x \tag{1}
$$

$$
x^2 - 2hx + h^2 + k = x^2 + \frac{b}{a}x 
$$

Observe this: 

$$
-2hx = \frac{b}{a}x
$$

$$
-2h = \frac{b}{a}
$$

$$
h = -\frac{b}{2a}
$$

so we got

$$
(x + \frac{b}{2a})^2
$$

which can be express to:

$$
\left(x + \frac{b}{2a}\right)^2 = \left(x + \frac{b}{2a}\right)\left(x + \frac{b}{2a}\right) = x^2 + \frac{b}{2a}x + x\frac{b}{2a} + \frac{b^2}{4a^2} = x^2 + \frac{b}{a}x + \frac{b^2}{4a^2}
$$

$$
\left(x + \frac{b}{2a}\right)^2  -  \left(\frac{b^2}{4a^2}\right) = \left(x^2 + \frac{b}{a}x\right)
$$

Continue where we left: 

$$
\left(x^2 + \frac{b}{a}x\right) = \left(-\frac{c}{a}\right)
$$

$$
\left(x + \frac{b}{2a}\right)^2  -  \left(\frac{b^2}{4a^2}\right) = \left(-\frac{c}{a}\right)
$$

$$
\left(x + \frac{b}{2a}\right)^2 = \left(-\frac{c}{a}\right) + \left(\frac{b^2}{4a^2}\right)
$$

$$
\left(x + \frac{b}{2a}\right) = \pm \sqrt{ \left(-\frac{c}{a}\right) + \left(\frac{b^2}{4a^2}\right)}
$$

$$
\left(x + \frac{b}{2a}\right) = \pm \sqrt{ \left(-\frac{(4a)c}{(4a)a}\right) + \left(\frac{b^2}{4a^2}\right)}
$$

$$
\left(x + \frac{b}{2a}\right) = \pm \sqrt{ \left(\frac{-4ac + b^2}{4a^2}\right)}
$$

$$
\left(x + \frac{b}{2a}\right) = \pm \left(\frac{\sqrt{b^2 -4ac}}{2a}\right)
$$

$$
x = \frac{-b}{2a} \pm \left(\frac{\sqrt{b^2 -4ac}}{2a}\right)
$$

$$
x = \left(\frac{-b \pm \sqrt{b^2 -4ac}}{2a}\right)
$$
