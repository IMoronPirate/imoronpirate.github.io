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

## Get Euler's angles from rotation matrix

Suppose that you use the Rodrigues' formula and you have the rotation matrix:

$$
\bm{R} = \begin{pmatrix}
R_{11} & R_{12} & R_{13} \\
R_{21} & R_{22} & R_{23} \\
R_{31} & R_{32} & R_{33} \\
\end{pmatrix}.
$$

Then, you discovery that the API ou are using for the rotation accepts only
the Euler's angle. Than, the reaction is *f**k this! I quit!*

After you calm down, you ask yourself: ok how can I determined the angles from
the rotation matrix? And the you realize which angles? There are different
representation of [Euler's angles](https://en.wikipedia.org/wiki/Euler_angles)!
*I am really done with this s**t!*

*Breath! Stay calm! Breath!*

The API is a $$ZYX$$ representation, thanks to
[Wikipedia](https://en.wikipedia.org/wiki/Euler_angles) you
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

The angles can be extracted if we know the element of the rotation matrix
$$R_{i,j}$$, $$j = 1,2,3$$ and $$j=1,2,3$$

$$
\bm{R} = \begin{pmatrix}
R_{11} & R_{12} & R_{13} \\
R_{21} & R_{22} & R_{23} \\
R_{31} & R_{32} & R_{33} \\
\end{pmatrix}
$$



This post ends here, if you have comments/feedbacks drop me an [email](mailto:i.moron.pirate@gmail.com),
they are appreciated.

Ahoy!

---


