---
layout: single
title: >
  learning to code
excerpt: tips on the learning process from a seasoned, crusty, old sea dog
last_modified_at: 2019-03-12
header:
  overlay_image: "assets/2019/02/An-old-sea-dog-e1450900914569.jpg"
tags: [intro to, data science,
computer science, programming,
r, python,
]
---

I started programming Python in 2014 and have since gotten pretty good at it. I have gone on to  build applications using R, SQL and Kotlin.<sup id="a1">[1](#f1)</sup>

This post is targeted at somebody starting to learn programming from scratch. Your learning timelines and objectives unknown (e.g. specialising in a type of coding, for a job or hobby).

Reader objectives from this post:
- see what a successful "learning to code" journey looks like
- common pitfalls and feelings
- habits for learning effectively
- encouragement and setting realistic expectations

This post contains advice when [starting out](#at-first...), my own [Python learning curve](#milestones-in-my-python-learning-curve), a suggested [approach to learning](#tips-for-learning-effectively), and how I [setup my computer to code](#my-tooling-and-setup).

I hope it helps and good luck!

## at first...
You just have to keep plodding. Rome wasn't built in a day. Coding fundamentals are a combination of logic, language syntax, an ecosystem of other people's code and some maths. All time great cyclist Eddy Merckx has a quote about just doing it that applies to elite cycling and learning to code:
> ~~Ride~~ **Code** as much or as little, or as long or as short as you feel. But ~~ride~~ **code**.  
> <cite>Eddy "The Cannibal" Merckx :goat:</cite>

It's all about consistent curiosity. Coding is a moving target: languages, libraries and "hot areas" come and go. A curious mindset help keep you up-to-date.

A lot of people feel intimidated by learning to code. Some common fears or feelings to recognise:
- [Imposter syndrome](https://en.wikipedia.org/wiki/Impostor_syndrome). I think because of how fluent some people _appear to be_. These people may have been coding for a long time, are good at self advertising or using impenetrable language. Rest assured the best technical minds I have met or read online are humble and approachable (e.g. Alex Martelli).
- Messing up your computer. This is honestly pretty hard to do as a beginner, especially if you use virtual environments. See my [post on "intro to virtual environments"](_posts/2019-03-01-intro-python-virtual-environments.md).
- You feel like you don't have the raw passion to succeed. It helps to be interested in computers but I didn't **love** computers at the start. I had an appreciation, but it has taken me a while to see what was possible.

**ProTip!:** develop the ability to [read and navigate original documentation](https://readthedocs.com/).
{: .notice--info}

## milestones in my python learning curve
Here I list key turning points and supporting links in my python learning curve. Bear in mind these milestones are spread out over 5+ years and I was pretty determined to use Python as much as possible!

1.	The language basics (types, keywords, looping, functions): [Codeacademy](https://www.codecademy.com). Other seemingly equivalent providers that have nice gentle intros and have an interpreter in browser so you can code directly and don’t have to faff with a local python setup.
  - [katacoda](https://www.katacoda.com/): similar to codeacademy but users submit courses.
  - [Datacamp](https://www.datacamp.com/home): for data science, R and Python specifically.
2.	Algorithm design and what the computer is doing under the covers: [Coursera computer science 101 MOOC](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-00-introduction-to-computer-science-and-programming-fall-2008/). There are a range of equivalent MOOCs out there.
3.	Couple other python assisted walkthroughs: [Al Sweigart’s Automate the Boring Stuff](https://automatetheboringstuff.com/) and [How to Think Like a Computer Scientist](http://www.openbookproject.net/thinkcs/python/english2e/).
4.	Challenges for practicing algorithm design _by yourself_: [Project euler](https://projecteuler.net/) and [advent of code](https://adventofcode.com/). You should never look at the solutions while solving. But they are a good to benchmark how others do it.
  - [Project Euler optimised solutions](http://www.s-anand.net/euler.html)
  - Peter Norvig's [Advent of Code solutions](https://github.com/norvig/pytudes/blob/master/ipynb/Advent%202017.ipynb). Peter is Google CTO and co-wrote [bible of AI](http://aima.cs.berkeley.edu/). His code is the gold standard: efficient, clean and modular logic. There is a lot of beautifully written Python in his github repo!
5.	Achieved fluency and confidence: Started coding on the job, doing Kaggle competitions and going to evening meetups. Developed an idea of good code, different ways to solve the same problem (!) and the differences between hacking and building. Some links and reading for this point:
  - François Chollet ["Notes to Myself on Software Engineering"](https://medium.com/s/story/notes-to-myself-on-software-engineering-c890f16f4e4d)
  - Robert L. Read ["How To Be a Programmer: A Short, Comprehensive, and Personal Summary"](https://www.doc.ic.ac.uk/~susan/475/HowToBeAProgrammer.pdf).
7. More advanced techniques and topics: the internals of a language, how to interface with the OS, and application architecture. Some links and reading for this point:
  - James Powell talks: James knows Python inside and out and illustrates concepts so well. I like [this one](https://www.youtube.com/watch?v=cKPlPJyQrt4) in particular. He explains decorators, class methods and the very powerful double underscore methods, e.g. `self.__init__(),  self.__init_subclass__()`
  - Peter Van Roy's ["Programming Paradigms for Dummies: What Every Programmer Should Know"](https://www.info.ucl.ac.be/~pvr/VanRoyChapter.pdf)

## tips for learning effectively
-	Keep a log of how you solve a problem, and then once solved how your method stacks up against the “gold standard”. The end goal is to build up log of lessons learned and which specific pattern solved the problem. This log can be multi-line comments in a script, e.g.

```
“””LESSONS LEARNED
- tried nested for loop that iterated over every single combination
- better solution: while loop with stride of 2 and break when found because only need to consider odd numbers
”””
```

-	Google the techniques around the problem, not the solution. E.g. The maths to test if a number is prime or not.
-	Don’t be hard on yourself about your pace. You will speed up as you go, but its a very up+down pattern.
- Learn how best to unblock when you are stuck on a problem. And ideally before you become blocked and have sunk many hours into a simple problem. My suggestions:
  - Take a break. This works really well for me, I like going for a short walk and letting my subconscious chew through a problem.
  - Talk the problem over with others, even if not technical audience.
  - Sketch out the inputs, outputs and moving parts.
  - Learn to debug systematically. [This blog post has great tips for practical debugging](https://www.jackkinsella.ie/articles/7-keys-to-systematic-debugging).

## my tooling and setup
-	IDE: IntelliJ with the python plugin, basically the same as PyCharm but a few more IDE options and multilingual support. IntelliJ integrates so well with other tools e.g. virtual environment manager, version control, testing and deployment. Its also really easy to customise and sync using your JetBrains account e.g. [apply a badass colour scheme](http://color-themes.com/?view=index). I have also recently started using MS Visual Studio and it does _some_ things better.
- a nice raw text editor: Notepad++ on Windows, Sublime sounds nice for mac (I've never used it). Recently started using github's [Atom](https://atom.io/) which is cross platform, integrates well with version control (unsurprisingly), lightweight, nicely packaged out of the box (read: default dark themed and split screen), extendible, pretty good completion and really nifty shortcuts (just "a" to add a new file!!! :open_mouth:).
-	Environment management: conda. I really recommend investing time to understand virtual environments. They are the topic of my next post. In a nutshell they control your project's the installed library versions. Often so-so hard to replicate results because of peoples hacky-as-shit setups.
  - Here is a [template conda yml file](/assets/2019-02/template_conda_env.yml). You should modify this file: e.g. set the environment name and python version. [Here's the conda docs section how to to create an environment using a yml](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file)
-	Testing: pytest and unittest together. I strongly recommend getting familiar with [Test Driven Development](https://en.wikipedia.org/wiki/Test-driven_development).
-	Version control: git. It is so important to grasp version control. You can forget about worrying if a new change will break existing code.
- Deployment: Docker.

<!-- footnotes -->
## footnotes
<b id="f1">1</b> I fully recognise that Python is a high level functional languages and many would scoff at it being called "programming". To these higher code-lords I bow and mumble incoherently. :wink: [↩](#a1)
