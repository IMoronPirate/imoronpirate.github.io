---
title:  "How to deploy a locally built Jekyll site on GitHub"
date: 2018-12-19 14:19
categories: coding
tags: github jekyll rakefile
---



You may ask why I should build the blog locally when GitHub does it for me.
Well there are several reasons, for instance if you use some unsupported plugins,
but here I will discuss only one practical reason that it made me spent some
time to fix it.

I work usually on two PCs one in the office and one at home. 
I have all my code in several git repositories hosted on [GitLab](https://about.gitlab.com/){:target="_blank"} and 
[GitHub](https://github.com/){:target="_blank"}. 
Thus, when I implement some feature, let say in the office, 
I `push` the code to the host and then at 
home I `pull` the new code and *vice versa*.
In this way, I have always my code up-to-date in both stations.

When the idea of starting this blog come out, I found that it was not possible
to do such a thing with the 
[GitHub Pages](https://pages.github.com/){:target="_blank"}. 
Of course, GitHub Pages is a cheap and easy way to host a blog using 
[Jekyll](https://jekyllrb.com/){:target="_blank"} but unfortunately 
it breaks my development cycle `commit -> push -> pull`.
As a matter of facts, if you use Jekyll hosted in GitHub Pages the blog is
built every time you push the code on the branch master.
There you can see the problem. If you are working on a post in the office,
then you want to review it at home before publishing this is not possible.
When you push it (to have the draft at home) 
GitHub build and publish your post (:angry:).


As mentioned, GitHub host a blog/webpage/whatever so one does not need to
let GitHub build it. One can build a blog in whatever way you
want and put in the master branch of the repository the html files for
the generated site. The issue now is where to keep the files needed for
the generation of the blog.






In this way, you decided when you want to publish something 
since you have to build it locally and then commit the changes in the master 
branch. However, this creates another issue since you have to keep your 


Still does not solve my problem since I wanted to push the problem, 




but I build it locally on my personal **computer**.
You may ask why I do this. 

a local builded 
site on GitHub. Being this only my first post, 


As my first post, I think is important 




[Pelican]: https://blog.getpelican.com/
