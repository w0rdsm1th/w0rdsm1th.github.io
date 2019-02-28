---
layout: single
title: "starting to learn programming"
excerpt: notes from a seasoned-old-sea-dog-veteran. what I wish somebody had told me at the start
last_modified_at: 2019-02-27
header:
  overlay_image: "assets/201902/An-old-sea-dog-e1450900914569.jpg"
tags: [data science,
computer science, programming,
r, python,
]
---
# TODO
- little ranked table with different virtual environment managers, pros cons and functionality
- view of somebody just starting out


I started programming Python in 2012. I have since gotten pretty good at it. Since then I have also coded projects/applications in R, SQL and Kotlin.<sup id="a1">[1](#f1)</sup>

This post is targeted at a relatively internet/computer savvy individual, with no prior programming experience. You are interested in learning programming (logic and control, not styling like HTML and CSS) from scratch. Your learning timelines and objectives unknown (given speciality, job, hobby).

This post contains advice to those [just starting out](#at-first...), [my own learning curve](#), how I [setup my computer to code](#) and a suggested [approach to learning](#).

I hope it helps and good luck!

## at first...
Just gotta keep plugging away persistently. This cannibalised Eddy Merckx quote about just doing it applies to biking and learning to code:
> ~~Ride~~ **Code** as much or as little, or as long or as short as you feel. But ~~ride~~ **code**.
> Eddy "The Cannibal" Merckx

 At first it is hard to decide which area and type of programming to learn and pursue. You can use programming to move data about, to build Machine Learning applications to make better decisions, to integrate different bits of hardware, to build applications or websites,... To solve this, I suggest a pretty general starting point and to keep your eyes peeled and ears tuned to other areas that might interest you.

It's all about consistent curiosity. Nobody can learn to code well over night. It is a sustained effort. Its also a moving target: languages and libraries and practices and "hot areas" come and go. By trying to consistently question and discuss and learn you _can_ move that mountain!

A lot of people feel intimidated by it:
- Worried they are going to mess up your computer (which is pretty hard to do as a beginner, especially if you follow these best practice guidelines and use virtual environments).
- New programmers can definitely suffer from [imposter syndrome](https://en.wikipedia.org/wiki/Impostor_syndrome). Recognise this and try to push through. I think because of how fluent some people _appear to be_, because some people cloak their expertise with impenetrable language. The best technical minds I have met or read online have an approachable style (e.g. Alex Martelli). They can explain complex stuff intuitively and without jargon.

## My own rough python learning curve:
-	Codeacademy for the basics (types, keywords, looping, functions). Other seemingly equivalent providers I have since heard of: https://www.katacoda.com/ - similar to codeacadmey, has a managed online interpreter (don’t have to faff with a local python setup), Datacamp.
-	Project euler and advent of code for autonomous algorithm design, problem solving: https://adventofcode.com/ and https://projecteuler.net/. Goes without saying but you should never ever look at solutions but they are widely available and good to benchmark/see how others do it.
  - [Project Euler optimised solutions](http://www.s-anand.net/euler.html)
  - Peter Norvig's [Advent of Code solutions](https://github.com/norvig/pytudes/blob/master/ipynb/Advent%202017.ipynb). Peter is Google CTO and co-wrote [bible of AI](http://aima.cs.berkeley.edu/). His code the gold standard: efficient, clean and modular logic. There is a lot more nicely written python in his github repo!
-	[Coursera computer science 101 MOOC](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-00-introduction-to-computer-science-and-programming-fall-2008/) for different algorithm design patterns and what computer doing under the covers. There are a range of equivalent MOOCs out there.
-	Couple other python assisted walkthroughs: e.g. Al Sweigart’s automate the boring stuff.
-	Started coding on the job
- (Data science specific) doing Kaggle competitions
-	James Powell talks: James knows his python and illustrates concepts so well. I like [this one](https://www.youtube.com/watch?v=cKPlPJyQrt4) in particular, covers decorators, class methods and the very powerful double underscore methods, e.g.
```python
self.__init__(),  self.__init_subclass__()
```

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
  - Learn to debug systematically. [See this blog post for a good primer](https://www.jackkinsella.ie/articles/7-keys-to-systematic-debugging).

## tooling and setup
-	Intellij with the python plugin: basically the same as PyCharm but a few more IDE options and multilingual support. It is super customisable and easy to use IMO. Integrates so well with other tools e.g. virtual environment manager, version control, testing or deployment. I have started using Visual Studio and it does _some_ things better
- a nice raw text editor: Notepad ++ on Windows, sublime sounds nice for mac (I've never used it). Really impressed with github's Atom which is cross platform.
-	Anaconda for environment management. I really recommend investing time to understand virtual environments. In a nutshell they control all the libraries you use. Often so-so hard to replicate results because of peoples hacky-as-shit setups.
  - conda key differentiator versus venv for me is that it allows you to specify a specific version of python that is different to the base anaconda python (e.g. base version is 3.6.4 but can install any 3.X).
  - Here is a [template conda yml file](/assets/2019-02-22-template_conda_env.yml): these are really nice and readable over pip requirements.txt. You should modify this file: e.g. set the environment name and python version. [Here's the conda docs section how to to create an environment using a yml](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file)
-	pytest and unittest together for test cases. Strongly recommend looking into [Test Driven Development](https://en.wikipedia.org/wiki/Test-driven_development).
-	whatever version control: git, Atlassian


<!-- footnotes -->
<b id="f1">1</b> I fully recognise that Python and Kotlin are quite high level languages and many would scoff at them being called "programming". To these higher code-lords I bow and mumble incoherently. [↩](#a1)
