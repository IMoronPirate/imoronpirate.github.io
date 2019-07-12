---
title:  "Everything you ever wanted to know about ~~sex~~ rotations"
date: 2019-07-05 10:26
categories: ["math", "coding"]
tags: ["Euler's angles", "Rotations"]
mathjax: true
---

$$
    \newcommand{\bm}[1]{\boldsymbol{#1}}
    \DeclareMathOperator{\atantwo}{atan2}
$$

Almost certainty, at some point, one has to deal with rotations.
Promptly, one encounters different Euler's angles representations,
Quaternions, axis-angles representations, and so forth.

In this post, I would present which parametrization I use that I found
very useful in several situations I faced.

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
This is a perfect application for the Rodrigues' formula.

To rotate the vector $$\bm{a}$$ in order to coincide with the
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

Then, you discovery that the API you are using for rotations accepts only
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

We can easily see that $$R_{31} = -\sin\theta$$, therefore,

$$
\theta = -\arcsin(R_{31}).
$$

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

### If $$\bm{\cos\theta = 0}$$

If $$\cos\theta$$ is zero we cannot use the formulas above.
Thus, we need to analyze two cases $$\theta = \pm \pi/2$$.

#### $$\bm{\theta = \pi/2}$$ case

It is easy to see that

$$
\begin{aligned}
R_{12} &= \sin\psi\cos\phi - \cos\psi\sin\phi = \sin(\psi-\phi),\\
R_{13} &= \cos\psi\cos\phi + \sin\psi\sin\phi = \cos(\psi-\phi).\\
\end{aligned}
$$

The rotation matrix become

$$
\bm{R} = \begin{pmatrix}
0 & \sin(\psi-\phi) & \cos(\psi-\phi) \\
0 & \cos(\psi-\phi) & -\sin(\psi-\phi) \\
-1 & 0 & 0
\end{pmatrix}.
$$

Any $$\psi$$ and $$\phi$$ that satisfy the following equation will be a
valid solution:

$$
\psi - \phi = \atantwo(R_{12}, R_{13}),
$$

where only the difference is constrained. Thus, we can assign any value to
one of the two angles, for instance $$\phi$$
and take the value of $$\psi = \phi + \atantwo(R_{12}, R_{13})$$.

#### $$\bm{\theta = -\pi/2}$$ case

This case is similar to the previous one

$$
\begin{aligned}
R_{12} &= -\sin\psi\cos\phi - \cos\psi\sin\phi = -\sin(\psi+\phi),\\
R_{13} &= -\cos\psi\cos\phi + \sin\psi\sin\phi = -\cos(\psi+\phi).\\
\end{aligned}
$$

Therefore, the solution is

$$
\begin{aligned}
\psi + \phi &= \atantwo(-R_{12}, -R_{13}),\\
\psi &= -\phi + \atantwo(-R_{12}, -R_{13}).
\end{aligned}
$$

In both cases $$\theta = \pm \pi/2$$ we have that $$\psi$$ and $$\phi$$
are linked. This phenomenon is called
[Gimbal lock](https://en.wikipedia.org/wiki/Gimbal_lock).

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
