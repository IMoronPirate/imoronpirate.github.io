---
title:  "Everything you ever wanted to know about ~~sex~~ rotations"
date: 2019-07-05 10:26
categories: math coding
tags: Euler Rotations
mathjax: true
---

$$
    \newcommand{\bm}[1]{\boldsymbol{#1}}
$$

Rotations are omnipresent in several aspects from spatial rotation to
rotations in any abstract space. different 3D coordinate systems, different Euler angles representations, Quaternions, Axis angles
However, every time one has to implement
a rotation always faces the issue of conventions and parametrisation: using
the angle-axis representation, quaternions or Euler's one, and, of course,
which Euler's parametrisation.

In this post, I would present which parametrisation I use that I think it
it very useful in several situation I faced.

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
vector $$\bm{b}$$, we need to rotate $$\bm{a}$$ of an angle $$\theta = \bm{a}\cdot \bm{b}$$ around the axis $$\bm{u} = \bm{a} \times \bm{b}$$.
Therefore, we can use the Rodrigues' formula for $$\theta$$ and $$\bm{u}$$.

## Get Euler's angles from rotation matrix

A common case is when we know the rotation matrix as we can extract above
and we want to translate this in Euler's angles.
First of all, we have to define which Euler rotation since there are many of
them. In my company, we use an Euler-321 rotation.


This post ends here, if you have comments/feedbacks drop me an [email](mailto:i.moron.pirate@gmail.com),
they are appreciated.

Ahoy!

---