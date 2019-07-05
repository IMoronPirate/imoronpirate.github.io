---
title:  "Everything you ever wanted to know about ~~sex~~ rotations"
date: 2019-07-05 10:26
categories: math coding
tags: Euler matrix Rotations
mathjax: true
---

## Rotation matrix from one vector to another

Usually we have two vectors, for instance describing two planes, and
we would like to rotate one vector, $$\vec{p}$$, to the other one, $$\vec{d}$$.
The rotation matrix for this rotation is given by the 



I work usually on two PCs one in the ~~office~~ and one at home. 
I have all my code in several git repositories hosted on [GitLab](https://about.gitlab.com/){:target="_blank"} and 
[GitHub](https://github.com/){:target="_blank"}. 
Thus, when I implement some feature, let say in the office, 
I `push` the code to the host and then at 
home I `pull` the new code and *vice versa*.
In this way, I have always my code up-to-date in both stations.

A possible solution is to have a repository for the source code
and a repository for the hosting of the blog. However,
I did not like the idea of having two repositories for just one project.
So, I tought to use a branch for the developement into the main repository:

```bash
- dev #contains the source code to generate the blog
- master #contains the html pages 
```

The only issue is how to avoid the manually coping of the file generated
while you are in the `dev` branch and then commit those files in the `master`.
Thus, I wrote a rakefile to handle all of this

This post ends here, if you have comments/feedbacks drop me an [email](mailto:i.moron.pirate@gmail.com),
they are really appreciated.

Ciao!

---
