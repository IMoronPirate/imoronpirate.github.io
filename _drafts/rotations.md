---
title:  "Everything you ever wanted to know about ~~sex~~ rotations"
date: 2019-07-05 10:26
categories: math coding
tags: Euler Rotations
mathjax: true
---

$$
    \newcommand{\bm}[1]{\boldsymbol{#1}}
    \DeclareMathOperator{\atantwo}{atan2}
$$

Almost certainty, at some point, one has to deal with rotations.
Promptly, one encounters different Euler's angles representations,
Quaternions, axis-angles representations, and so forth.

In this post, I would present which parametrization I use that I think it
it very useful in several situations I faced.

## Rodrigues' formula

To construct the rotation matrix,
given the rotation axis and the angle, the
[Rodrigues' formula](https://en.wikipedia.org/wiki/Rodrigues%27_rotation_formula) 
is excellent.

The rotation matrix around and axis $$\bm{k}$$ (where $$|\bm{k}|=1$$)
of an angle $$\theta$$ is

$$
\bm{R} = \bm{I} + (\sin\theta)\bm{K} + (1-\cos\theta)\bm{K}^2,
$$

where $$\bm{K} = [\bm{k}]_\mathrm{x}$$ is the cross-product matrix given by

$$
\bm{K} \equiv \sum_{i=1}^3 (\bm{k} \times \hat{\bm{e}}_i) \otimes \hat{\bm{e}}_i =
\begin{pmatrix}
0 &-k_3 &k_2\\
k_3 & 0 &-k_1\\
-k_2 & k_1 &0
\end{pmatrix}
$$

### Rotation matrix from one vector to another one

Usually we have two vectors, for instance describing two planes, and
we would like to rotate one vector, $$\bm{a}$$, to the other one, $$\bm{b}$$.
To extract this rotation matrix, before we need to understand how to build the
rotation matrix around an axis of a certain angle.

In the case we want to rotate the vector $$\bm{a}$$ to coincide to the
vector $$\bm{b}$$, we need to rotate $$\bm{a}$$ of an angle
$$\theta = \bm{a}\cdot \bm{b}$$ around the axis $$\bm{u} = \bm{a} \times \bm{b}$$.
Therefore, we can use the Rodrigues' formula for $$\theta$$ and $$\bm{u}$$.

## Get Euler's angles from the rotation matrix

Suppose that you used the Rodrigues' formula and you have the rotation matrix:

$$
\bm{R} = \begin{pmatrix}
R_{11} & R_{12} & R_{13} \\
R_{21} & R_{22} & R_{23} \\
R_{31} & R_{32} & R_{33} \\
\end{pmatrix}.
$$

Then, you discovery that the API you are using for the rotation accepts only
the Euler's angle. Than, the reaction is *f**k this! I quit!*

After you calm down, you ask yourself: ok how can I determined the angles from
the rotation matrix? And then you realize: which angles? There are different
representation of [Euler's angles](https://en.wikipedia.org/wiki/Euler_angles)!
*I am really done with this s**t! I am out!*

*Breath! Stay calm! Breath!*

The API is a $$ZYX$$ representation, thanks to
[Wikipedia](https://en.wikipedia.org/wiki/Euler_angles) you have
the rotation matrix as function of the angles.
The rotation $$ZYX$$ consists of a rotation of $$\phi$$ around
$$z$$-axis, then a rotation around $$y$$-axis of an angle $$\theta$$, and
finally a rotation around the $$x$$-axis of an angle $$\psi$$.
Therefore, the rotation matrix
$$\bm{R} = \bm{R}_x(\psi)\cdot \bm{R}_y(\theta)\cdot \bm{R}_z(\phi)$$
is

$$
\bm{R} = \begin{pmatrix}
c_\phi c_\theta & c_\phi s_\theta s_\psi - c_\psi s_\phi & s_\phi s_\psi + c_\phi c_\psi s_\theta \\
c_\theta s_\phi & c_\phi c_\psi + s_\phi s_\theta s_\psi & c_\psi s_\phi s_\theta - c_\phi s_\psi \\
-s_\theta & c_\theta s_\psi & c_\theta c_\psi
\end{pmatrix}.
$$

First all, before calculating the angles, we should remind ourselves there are
infinite solutions (the same rotation can be achieved with different sets
of angles). Therefore, we restrict ourselves to the following range for
the three angles

$$
\begin{aligned}
\phi &= [-\pi, \pi], \\
\theta &= [-\pi/2, \pi/2], \\
\psi &= [-\pi, \pi].
\end{aligned}
$$

### Angles calculation

We can easily see that $$R_{31} = -\sin\theta$$,
therefore,

$$
\theta = -\arcsin(R_{31})
$$.

Note that the solution is unique in the range we have chosen.
In addition, we can find $$\psi$$ from $$\psi = \arctan(R_{32}/R_{33})$$.
Numerically, it $$\psi$$ is extracted through $$\atantwo(\cdot, \cdot)$$
which returns a value in
the range $$(-\pi, \pi]$$ as we need it.
However, one must be careful since the sign is important here.
Indeed, if $$\cos\theta > 0$$ then $$\psi=\atantwo(R_{32}, R_{33})$$ but
if the cosine is negative,
$$\cos\theta <0$$ then $$\psi = \atantwo(-R_{32}, -R_{33})$$.
We can write this compactly as

$$
\psi = \atantwo\Big(\frac{R_{32}}{\cos\theta}, \frac{R_{33}}{\cos\theta}\Big),
$$

if $$\cos\theta\neq 0$$ (the case $$\cos\theta =0$$ is discussed below).
For the angle $$\phi$$, we note that $$R_{21}/R_{11} = \tan\phi$$.
Therefore,

$$
\phi = \atantwo\Big(\frac{R_{21}}{\cos\theta}, \frac{R_{11}}{\cos\theta}\Big),
$$

where again we divided for $$\cos\theta$$ for taking the correct sign.
Thus, we have a set of angles from our rotation matrix if
$$\cos\theta \neq 0$$.

### If $$\cos\theta = 0$$




This post ends here, if you have comments/feedbacks drop me an [email](mailto:i.moron.pirate@gmail.com),
they are appreciated.

Ahoy!

---
