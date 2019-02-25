---
layout: post
title: "learning to code: notes from a 'veteran'"
tags: [data science,
computer science, programming,
r, python,
lecture notes,
]
---

I started programming Python in 2012.

Since gotten pretty good at it. Picked up R, SQL, some Java/Kotlin.

Not so targeted because I don’t know what level you are at now or your objectives and timelines.

Rough curve:

## at first
Hard to decide what

curiosity and consistency.

Imposter syndrome:

 Eddy Merckx quote about perseverance and just doing it:
> Ride as much or as little, or as long or as short as you feel. But ride.
> Eddy "The Cannibal" Merckx

A lot of people feel intimidated by it.
Worried they are going to mess up your computer (which is pretty hard to do as a beginner, especially if you use virtual environments)


## My own rough python learning curve:
-	Codeacademy for the basics (types, keywords). Seemingly equivalent providers:
  - https://www.katacoda.com/ - similar to codeacadmey, has a managed online interpreter (don’t have to faff with a local python setup).
  - Datacamp
  - Others???
-	Project euler and advent of code for autonomous algorithm design, problem solving: https://adventofcode.com/ and https://projecteuler.net/. Should never ever look at solutions but they are widely available and good to benchmark/see how others do it.
  - Project euler solutions: http://www.s-anand.net/euler.html
  - Advent of Code solutions: http://norvig.com/ipython/README.html. Peter is Google CTO and wrote [bible of AI](). His code the gold standard: clean and modular logic. Lots of other nicely written python in his repository as well.
-	Coursera computer science 101 MOOC for more rigorous algorithm design and what computer doing under the covers: https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-00-introduction-to-computer-science-and-programming-fall-2008/
-	Couple other python assisted walkthroughs: e.g. Al Sweigart’s automate the boring stuff
-	Started coding on job and Kaggle competitions
-	James Powell talks: James knows his python and illustrates concepts so well. I like this one in particular, covers decorators, class methods and the very powerful double underscore methods, e.g. ```python self.__init__(),  self.__init_subclass__()``` https://www.youtube.com/watch?v=cKPlPJyQrt4&t=3s


## tooling and setup
-	Intellij with python plugin: basically the same as PyCharm but a few more options and multilingual support. It is super customisable and easy to use IMO. Integrates so well with other tools e.g. virtual environment manager, version control, testing or deployment.
- a nice raw text editor: Notepad ++ on Windows, sublime sounds nice for mac (I've never used it). Really impressed with Atom which is cross platform.
-	Anaconda for environment management. Really investing time to understand virtual environments. Often so-so hard to replicate results because of peoples hacky as shit setups.
  - key differentiator versus venv for me is that it allows you to specify a specific version of python that is different to the base anaconda python (e.g. base version is 3.6.4 but can install any 3.X).
  - attached a template yml file: these really nice and readable over pip requirements.txt
  - Process to install new packages to conda environment: https://conda.io/docs/user-guide/tasks/manage-environments.html
-	pytest and unittest together for test
-	whatever version control: git, Atlassian

## keeping track while you learn by doing
-	Keep a log of how you solve a problem, and then once solved how your method stacks up against the “gold standard”. End goal is to build up log of lessons learned and which specific pattern solved the problem. This log can be multi-line comments in a script, e.g.

```python
“””LESSONS LEARNED
- tried nested for loop that iterated over every single combination
- better solution: while loop with stride of 2 and break when found because only need to consider odd numbers
”””
```

-	Google the techniques around the problem: i.e. specific prime number tests/combinatorics. Being able to solve without any google at all pretty tough!
-	Don’t be hard on yourself about the pace achieved
  - getting stuck on a problem
