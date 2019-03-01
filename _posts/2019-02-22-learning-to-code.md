---
layout: single
title: tips for starting to learn to code
excerpt: notes from a seasoned-old-sea-dog
last_modified_at: 2019-03-01
header:
  overlay_image: "assets/201902/An-old-sea-dog-e1450900914569.jpg"
tags: [data science,
computer science, programming,
r, python,
]
---
# TODO
- a little ranked table with different virtual environment managers, pros cons and functionality: conda, venv, pipenv
- audience of somebody just starting out: what they worried about, who they are


I started programming Python in 2012. I have since gotten pretty good at it. Since then I have also coded projects/applications in R, SQL and Kotlin[^1].

This post is targeted at a relatively computer and internet savvy individual[^2], with no prior programming experience. You are interested in learning programming (logic and control, not styling like HTML and CSS) from scratch. Your learning timelines and objectives unknown (given speciality, job, hobby).

This post contains advice to those [just starting out](#at-first...), [my own learning curve](#), a suggested [approach to learning](#), and how I [setup my computer to code](#).

I hope it helps and good luck!

## at first...
You have just gotta keep plugging away persistently. Rome wasnt built in a day. Coding is a combination of logic, language syntax, maybe some math and existing ecosystem. This cannibalised Eddy Merckx quote about just doing it applies to biking and learning to code:
> ~~Ride~~ **Code** as much or as little, or as long or as short as you feel. But ~~ride~~ **code**.
> Eddy "The Cannibal" Merckx

 At first it is hard to decide which area and type of programming to learn and pursue. You can use programming to move data about, to build Machine Learning applications to make better decisions, to integrate different bits of hardware, to build applications or websites,... To solve this, I suggest a pretty general starting point and to keep your eyes peeled and ears tuned to other areas that might interest you.

It's all about consistent curiosity. Nobody can learn to code well over night. It is a sustained effort. Its also a moving target: languages and libraries and practices and "hot areas" come and go. By trying to consistently question and discuss and learn you _can_ move that mountain!

A lot of people feel intimidated by it:
- Worried they are going to mess up your computer (which is pretty hard to do as a beginner, especially if you follow these best practice guidelines and use virtual environments).
- New programmers can definitely suffer from [imposter syndrome](https://en.wikipedia.org/wiki/Impostor_syndrome). Recognise this and try to push through. I think because of how fluent some people _appear to be_, because some people cloak their expertise with impenetrable language. The best technical minds I have met or read online have an approachable style (e.g. Alex Martelli). They can explain complex stuff intuitively and without jargon.
They all do seem to love computers or what computers can do for them. But I didn't **love** computers. I had an appreciation, but it has taken me a while to see what was possible, and now I quite enjoy digging into Docs to see what is possible in quickest and cleanest way possible.


{:refdef: .notice--info}
**ProTip!:** always [read the docs](https://readthedocs.com/).
{: refdef}

## milestones in my python learning curve
-	[Codeacademy](https://www.codecademy.com) for the basics (types, keywords, looping, functions). Other seemingly equivalent providers that have nice gentle intros and have an interpreter in browser so you can code directly and don’t have to faff with a local python setup.
  - [katacoda](https://www.katacoda.com/): similar to codeacadmey, users submit courses.
  - [Datacamp](https://www.datacamp.com/home): for R and Python specifically.
-	[Coursera computer science 101 MOOC](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-00-introduction-to-computer-science-and-programming-fall-2008/) for different algorithm design patterns and what computer doing under the covers. There are a range of equivalent MOOCs out there.
-	Couple other python assisted walkthroughs: e.g. Al Sweigart’s automate the boring stuff.
-	[Project euler](https://projecteuler.net/) and [advent of code](https://adventofcode.com/) challenges for practicing algorithm design _by yourself_. You should never look at the solutions while solving but they are widely available and good to benchmark/see how others do it after solving.
  - [Project Euler optimised solutions](http://www.s-anand.net/euler.html)
  - Peter Norvig's [Advent of Code solutions](https://github.com/norvig/pytudes/blob/master/ipynb/Advent%202017.ipynb). Peter is Google CTO and co-wrote [bible of AI](http://aima.cs.berkeley.edu/). His code the gold standard: efficient, clean and modular logic. There is a lot more nicely written python in his github repo!
-	Started coding on the job
- (achieved some decent fluency, getting to the exciting stuff) doing Kaggle competitions, going to evening meetups
-	James Powell talks: James knows his python and illustrates concepts so well. I like [this one](https://www.youtube.com/watch?v=cKPlPJyQrt4) in particular, covers decorators, class methods and the very powerful double underscore methods, e.g. `python self.__init__(),  self.__init_subclass__()`

## how to learn effectively
-	Keep a log of how you solve a problem, and then once solved how your method stacks up against the “gold standard”. End goal is to build up log of lessons learned and which specific pattern solved the problem. This log can be multi-line comments in a script, e.g.

```
“””LESSONS LEARNED
- tried nested for loop that iterated over every single combination
- better solution: while loop with stride of 2 and break when found because only need to consider odd numbers
”””
```

-	Google the techniques around the problem: i.e. specific prime number tests/combinatorics. Being able to solve without any google at all pretty tough!
-	Don’t be hard on yourself about your pace. You will speed up as you go, and its a very up+down pattern.
- Learn how best to unblock when you are stuck on a problem. And ideally before you have sunk many hours into a simple problem. My suggestions:
  - Take a break. This works well for me, I like letting my subconscious chew through a problem.
  - Talk the problem over with others, even if not technical audience.
  - Sketch out the moving parts.
  - Learn to debug systematically. [This blog post has great tips for practical debugging](https://www.jackkinsella.ie/articles/7-keys-to-systematic-debugging).

## my tooling and setup
-	Intellij with the python plugin: basically the same as PyCharm but a few more IDE options and multilingual support. It is super customisable and easy to use IMO. Integrates so well with other tools e.g. virtual environment manager, version control, testing or deployment. I have recently started using Visual Studio and it does _some_ things better.
- a nice raw text editor: Notepad++ on Windows, Sublime sounds nice for mac (I've never used it). Recently started using github's [Atom](https://atom.io/) which is cross platform, really lightweight, nicely packaged out of the box (read: default dark themed and split screen), extendible, good-ish completion and really nifty shortcuts (just "A" to create a new file!!! :open_mouth:).
-	Anaconda for environment management. I really recommend investing time to understand virtual environments. In a nutshell they control all the libraries you use. Often so-so hard to replicate results because of peoples hacky-as-shit setups.
  - conda key differentiator versus venv for me is that it allows you to specify a specific version of python that is different to the base anaconda python (e.g. base version is 3.6.4 but can install any 3.X).
  - Here is a [template conda yml file](/assets/2019-02-22-template_conda_env.yml): these are really nice and readable over pip requirements.txt. You should modify this file: e.g. set the environment name and python version. [Here's the conda docs section how to to create an environment using a yml](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file)
-	pytest and unittest together for test cases. Strongly recommend getting familiar with [Test Driven Development](https://en.wikipedia.org/wiki/Test-driven_development).
-	git for version control. So important to grasp version control. You can just forget about worrying if something new will work or not.
- Docker for deployment. Same as with version control, you can forget about worrying...


<!-- footnotes -->
[^1]: I fully recognise that Python is a high level functional languages and many would scoff at it being called "programming". To these higher code-lords I bow and mumble incoherently. :wink:
[^2]: Can right click, change background, kinda familiar with idea of a [mathematical function (e.g. inputs, outputs)](https://en.wikipedia.org/wiki/Function_(mathematics))
