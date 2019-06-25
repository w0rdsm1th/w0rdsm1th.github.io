---
layout: single
title: >
  intro to python virtual environments
excerpt: why you should use them, protips and glossary of common terms
last_modified_at: 2019-05-27
header:
  overlay_image: "/assets/2019/03/snakemassage3-COURTESY CAPTIVATINGCEBU-YOUTUBE - cropped.jpg"
  caption: "Photo credit: [**CAPTIVATINGCEBU**](https://www.youtube.com/user/captivatingcebu)"
tags: [intro to, programming, python]
---

<!-- reference style links -->
[conda yaml]: assets/2019/03/template_conda_env.yml
[pipenv Pipfile]: assets/2019/03/Pipfile
[pip requirements.txt]: assets/2019/03/requirements.txt
[virtual environment managers]: _drafts\2019-03-25-python-virtual-env-shootout.md
<!-- end reference style links -->

when you have read this post, check out my [next post][virtual environment managers] differentiating functionality between the 3 leading virtual environment managers and which is best suited to your needs.
{: .notice}


![](https://imgs.xkcd.com/comics/python_environment.png "prevent Python paralysis: use virtual environments"){:class="img-responsive" .align-center}

When I first started learning to code Python, virtual environments seemed abstract and unimportant. I could get setup and code some badass stuff right now, why bother to learn about them? And they do take a little while to learn. But learning to use them has taken away a lot of the frequent problems I was facing at the start. And they have been a great way to learn about the python interpreter and associated environment that runs my code.

Reader objectives from this post:
- Understand what virtual environments are and why you should use them.
- Usability tips e.g. setting up your IDE to automatically create an environment on creating new project.
- Glossary of common terms.

What this is not: a step-by-step tutorial of specific virtual environment managers and their commands. As an individual blogger it is hard to be comprehensive compared to the package authors and keep such tutorials up-to-date. If you're looking for a tutorial, I recommend this one [for venv and pipenv](https://docs.python-guide.org/dev/virtualenvs/) and this one for [conda](https://speakerdeck.com/teoliphant/packaging-and-deployment-with-conda) (written by the legendary Travis Oliphant, the creator of SciPy and founder of Anaconda!).

## why use virtual environments?
![](/assets/2019/03/virtual_envs diagram3.png "key concept of virtual environments: isolation"){:class="img-responsive"}

One of the most fun things about Python is the external libraries. With a simple `import this`<sup id="a1">[1](#f1)</sup> you can quickly use powerful chunks of other peoples pre-built code. And as your Python experience grows, you will almost certainly start to work on different projects that require different versions of the python interpreter or different versions of the same package dependency or sub-dependencies.

In the example environment sketch above there are 3 different environments. There is a `global python` environment which is left pristine and used just to spawn working environments. And there are 2 working environments `professional_work_project` and `dev` and each has a different version of [SQLAlchemy](https://docs.sqlalchemy.org/) installed.
- `professional_work_project` uses V0.9 because the project started 2 years ago and heavily relies on some now deprecated functionality.
- `dev` uses V1.3 (latest at time of writing) because you like to live on the bleeding edge.

Virtual environments allow you to install both versions of the SQLAlchemy package simultaneously. Without virtual environments you would have to constantly up and downgrade to work on either `professional_work_project` or `dev`.

Below I list other benefits to being able to isolate and control a project's dependencies. The reasons to use virtual environments massively outweigh reasons not to use: by 11 good reasons to 3 lazy reasons.

### reasons to use :thumbsup:
1. Allows you to work on different projects needing different versions of the same library or sub-dependencies on the same machine.

2. Mothballing and restarting a project: the code will run, irrespective of what has happened to project dependency versions or your workstation setup. The exact dependencies are basically cryogenically frozen.

3. Don't need computer admin privileges to install packages into global Python's site-packages directory. Insufficient privileges to install packages is so often an issue when working on a locked-down work computer.

4. Recreate-able: potentially hours saved trying to figure out why code runs on your machine but nobody else's.

5. Dependency resolution: easily resolve conflicts due to having a wrong package version installed.

6. Less system upheaval when changing Python versions (e.g. from 3.6 to 3.7).

7. Other people can use your code right out of the box; this is crucial when working on a team project.

8. It is a job-marketable skill :moneybag:.

9. Can easily setup your favourite IDE's defaults to use the big virtual environment managers for a new project, and execute code in the environment. See [pyCharm](https://www.jetbrains.com/help/pycharm/pipenv.html) and [Visual Studio](https://docs.microsoft.com/en-us/visualstudio/python/managing-python-environments-in-visual-studio?view=vs-2017) docs.

10. They are a great primer for more advanced Python packaging tools and techniques e.g. [Docker](https://www.fullstackpython.com/docker.html). It is still best practice to use a virtual environment manager to configure your Python environment e.g. conda on [Docker](https://hub.docker.com/u/continuumio). For more on these advanced deployment methods see [Python docs](https://packaging.python.org/overview/#depending-on-a-separate-software-distribution-ecosystem).

11. If running Mac OS there is a system Python first on path (located in /System/Library/Frameworks/Python.framework/Resources). Use command `where python` in a new BASH to see its location. This is for the operating system and there is a risk using it for development and installing packages will cause unknown difficulties. Unfortunately if you forget and just type `pip install SOME_PACKAGE` into a new BASH then it installs to this Python....

### reasons not to use :thumbsdown:
1. Time to learn: Takes a little while to get head around what they are and how to use them.
2. A little overhead to set up at the start of a project.
3. Some discipline to maintain during a project.

**ProTip!:** keep your project dependencies to a minimum. Even if you are superb at managing virtual environments. I have worked on projects where the team will use multiple different packages for similar tasks. Their dependency list just grows and grows. This is a risk because each new dependency introduces something else to break, install and understand.
{: .notice--warning}

## virtual environment protips
- While you can install packages on the fly using pip `pip install this`... It is good practice and efficient to standardise virtual environment creation using a file to ensure reproducibility. To save effort, I use a template environment for each package manager: [conda's yaml][conda yaml], [pipenv's Pipfile][pipenv Pipfile] (the file name is the extension) and venv which uses a pip [requirements.txt][pip requirements.txt].
- If distributing your environment file so others can run your app, it is recommend to ["pin you packages"][https://nvie.com/posts/pin-your-packages/] or specify dependency versions with ==, or specific major version with =. or specify a minimum version with >=.
- The 3 different environment files support installing from GitHub (even a specific commit!) and the templates above contain sample syntax to perform a GitHub.

Be aware: confusingly there is no one way to activate single virtual environment manager (venv) on same OS.
![](/assets/2019/03/venv activation commands - python docs venv.html creating-virtual-environments.JPG "be aware: no one way to activate even same virtual environment manager"){:class="img-responsive"}

## glossary of common terms
Dependency
: other libraries needed to make your own code or an external package run. E.g. Scikit-Learn needs or __depends on__ numpy for its numerical functions. So if you use `pip` to download and install Scikit-Learn then `pip` should identify this dependency relationship and install numpy too. Good libraries will be explicit about their dependency list.
: 'stuff' needed to run. A general concept/term used beyond Python packages. E.g. Some libraries require specific version of Python or BLAS (Basic Linear Algebra Subprograms).

Global (or system) Python
: The "main" installed python interpreter that you are using. Could be one you have downloaded from [python.org](https://www.python.org/) or bundled with another utility. No definitive single location or python version. It depends on OS, but typically defined as first one on PATH. If you have multiple installed try to be mindful of which you are using, where it is installing libraries and what version it is!

Module
: Importable chunks of code. Can be in a single script. See the Python [official tutorial on modules](https://docs.python.org/2/tutorial/modules.html)

Package (or library, APIs,...)
: Formal: a collection of importable functions and modules.
: Informal: other peoples code. Often designed for a specific purpose, documented, bundled up in a standard way for installation and hosted on a public repository. E.g. [making HTTP requests](http://docs.python-requests.org/en/latest/), [a web framework](https://www.djangoproject.com/) or [common machine learning techniques](https://scikit-learn.org/stable/).
: Some people call them "APIs" because its an interface between your code and somebody elses.

Package repository (or repo, mirror)
: online collection of packages. For example these free, open source repos: [PyPi](https://pypi.org), [Anaconda Cloud](https://anaconda.org/anaconda/repo), [CRAN](https://cran.r-project.org/) for R. A 'mirror' is often an organisations internal controlled version E.g. big banks like to control what people are using.

Pinned dependency packages
: Once you have settled on a dependency version for your project, you should be specific about that major.minor version number in your environment file. See [this blog post](https://nvie.com/posts/pin-your-packages/) from the developer of `pip-tools` package. *Avoid* below patterns that are vague about version in your project requirements.txt (or conda.yaml or Pipfile,...):
    - `lxml`
    - `lxml>=2.2.0`
    - `lxml>=2.2.0,<2.3.0`

  Instead, pin the dependency:
    - `lxml==2.3.4`


Python standard library
: the collection of packages that come with Python, cover basic and essential functionality. [Docs here](https://docs.python.org/3/library/index.html). It is a flexible thing; in different major (2.X or 3.X) and minor versions of Python these are added to, renamed or moved.

Sub-dependency
: Libraries themselves often require other libraries. Fortunately good installers identify what is needed and install in one swoop. Generally __don't__ go specifying every sub-dependency required to run your code, `pip` should resolve these.
E.g. Scikit-Learn depends on numpy, which itself depends on...

TOML
: "Tom's Obvious, Minimal Language", a nice, legible, programmable, configuration file language syntax. "Tom" is Tom Preston-Werner, co-founder of GitHub and kind of a big deal.

Virtual Environment
: self-contained, controlled collection of installed libraries. It can include a python interpreter. They are disposable, created for a specific purpose or project. As opposed to a python environment that is shared across projects or tasks. It's not so disposable and would probably "break lots of things" if it broke or got deleted.

> "A virtual environment is a unique combination of a specific Python interpreter and a specific set of libraries that is different from other global and conda environments."
> <cite> [Microsoft Visual Studio docs][https://docs.microsoft.com/en-us/visualstudio/python/selecting-a-python-environment-for-a-project?view=vs-2017#use-virtual-environments] </cite>

Site packages
: the default install location for Python libraries.
https://stackoverflow.com/questions/31384639/what-is-pythons-site-packages-directory
https://stackoverflow.com/a/31384640/3596968

YAML / yaml / yml
: "Yaml Aint Markup Language". A readable syntax that puts things in key:value pairs. See https://yaml.org/ and the fun parody https://noyaml.com/


<!-- footnotes -->
## footnotes
<b id="f1">1</b> A fun Python Easter egg. Try it yourself and then [read about it here.](https://www.python.org/dev/peps/pep-0020) [↩](#a1)
