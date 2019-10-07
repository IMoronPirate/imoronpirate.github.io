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



> Science is what we understand well enough to explain to a computer.  Art is
> everything else we do.



---


## Rodrigues' formula

To construct the rotation matrix,
given the rotation axis and the angle, the
[Rodrigues' formula](https://en.wikipedia.org/wiki/Rodrigues%27_rotation_formula)
is excellent.


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