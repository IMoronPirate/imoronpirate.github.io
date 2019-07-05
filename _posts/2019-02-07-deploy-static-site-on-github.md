---
title:  "How to deploy a locally built Jekyll site on GitHub"
date: 2019-02-07 13:38
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
it breaks my development cycle `work -> commit -> push -> pull -> work`.
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
A possible solution is to have a repository for the source code
and a repository for the hosting of the blog. However,
I did not like the idea of having two repositories for just one project.
So, I thought to use a branch for the development into the main repository:
```bash
- dev #contains the source code to generate the blog
- master #contains the html pages 
```
The only issue is how to avoid the manually coping of the file generated
while you are in the `dev` branch and then commit those files in the `master`.
Thus, I wrote a rakefile to handle all of this
```ruby
SITE_DIR = "_site"


desc "Build Jekyll site, copy files to master and commit/push to github"

task :build, :message do |t, args|
  raise "Missing \"message\" argument for commit. Build with `rake build[\"message\"]`".red unless args.message

  build_jekyll

  # checkout master, copy files and commit
  system "git checkout master" or fail "## [FAILED] master checkout".red
  puts "## [SUCCESS] Master checked out".green

  system "cp -r #{SITE_DIR}/* ."
  system "rm -r #{SITE_DIR}"
  system "git add -A" # commit all changes 
  system "git commit -m \"#{args.message}\"" or fail "## [FAILED] commit to master ".red
  puts "## [SUCCESS] webpage committed".green

  system "git push" or fail "## [FAILED] can't push".red
  puts "## [SUCCESS] push done. Webpage is alive".green
end


def build_jekyll
  puts "## Building jekyll"
  system "jekyll build" or fail "## [FAILED] Jekyll build".red
  puts "## [SUCCESS] Jekyll Build".green
end
```

The file is pretty straightforward. 
From the `dev` branch, when you execute it, it builds
the webpage, checkouts
the `master` branch, and copies the `_site` directory
in the repository main directory. 
At the end all changes are committed and push,
then GitHub makes it live.
Therefore, this is a solution to my development cycle
since I can work in the `dev` branch and there I can commit and push
all the things I want (they not become live in the blog :+1:),
in this way I can synchronize the repositories into my two stations.
When I am happy with a post and I want to publish it,
I just lunch the `rake` task:
```shell
rake build["commit message"]
```
and my post is published automatically.


This post ends here, if you have comments/feedbacks drop me an [email](mailto:i.moron.pirate@gmail.com),
they are really appreciated.


Ciao!


---

PS the color in the output strings it is made changing the
the String attributes:
```ruby
class String
  def colorize(color_code)
    "\e[#{color_code}m#{self}\e[0m"
  end

  def red
    colorize(31)
  end

  def green
    colorize(32)
  end

  def yellow
    colorize(33)
  end

  def blue
    colorize(34)
  end

  def pink
    colorize(35)
  end

  def light_blue
    colorize(36)
  end
end
```









