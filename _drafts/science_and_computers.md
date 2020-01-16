---
title:  "Are we still doing science?"
date: 2019-10-07 8:59
categories: ["science", "machine learning"]
tags: ["art"]
mathjax: true
---

$$
    \newcommand{\bm}[1]{\boldsymbol{#1}}
$$



> Science is what we understand well enough to explain to a computer.
> Art is everything else we do.

**TOC**

1. Introduction (why this sentence)
2. Is this still true, today?
3. examples in science today (ML that we do not understand)
3. Ptolemaic system, Kepler and Netwon
4. Is this still science?
5. Maybe yes, but we are paying a price.
  1. Gedanken-experiment if ML available at Newton time



---


## Science is what we understand well enough to explain to a computer

It is 1970


## Is this still true?

Nowadays, with ML this is not true anymore.

why ML is different from the fact that we use for instance computers without
knowing how they work but we still do science?

### Particle physics


### Random ideas

There are two big problem with ML that violate the pronciples of science:
1. The reproducibility: I cannot apply the same recipe several times, even if
   you have the algorithm you miss the data for the training.
2. the accumulation of knowledge: I cannot apply the knoledge to a
   different/close problem




### Pseudo-code

To summarize, we can extract the angles with the following pseudo-code

```c++
if (abs(R31) != 1) { // cos(theta) != 0
    theta = -asin(R31);
    psi = atan2(R32/cos(theta), R33/cos(theta));
    phi = atan2(R21/cos(theta), R11/cos(theta));
} else {
    phi = 0; // this is arbitrary, could be anything
    if (R31 = -1) {
        theta = pi/2;
        psi = phi + atan2(R12, R13);
    } else {
        theta = -pi/2;
        psi = -phi + atan2(-R12, R13);
    }
}
```


---

This post ends here, if you have comments/feedbacks drop me an [email](mailto:i.moron.pirate@gmail.com),
they are appreciated.

Ahoy!


[A=B](https://www.math.upenn.edu/~wilf/AeqB.html)
