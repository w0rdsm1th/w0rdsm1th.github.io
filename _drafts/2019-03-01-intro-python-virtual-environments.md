---
layout: single
title: >
  intro to: python virtual environments
excerpt: why you should use them and a review of 3 popular virtual environment managers functional differences
last_modified_at: 2019-03-04
header:
  overlay_image: "assets/201902/snakemassage3-COURTESY CAPTIVATINGCEBU-YOUTUBE - cropped.jpg"
  caption: "Photo credit: [**CAPTIVATINGCEBU**](https://www.youtube.com/user/captivatingcebu)"
tags: [intro to, programming, python]
---
TODO
[ ] put into a ranked table
[ ] make a requirements.txt and Pipfile for own env, prove process end to end

> When doing anything in Python "There should be one – and preferably only one – obvious way to do it."

> <cite>Guido Van Rossum, the Zen of Python in the `import this` Easter egg<sup id="a1">[1](#f1)</sup></cite>

When I first started learning Python, virtual environments seemed like an abstract and unimportant concept. I could get setup and code some badass stuff right now, why bother to learn how to use them? But learning to use them has taken away a lot of the frequent problems I was facing at the start.

Reader objectives from this post:
- Explain what virtual environments are and why you should use them.
- Learn the functional (rather than cosmetic) differences between different environment managers.

assumes: you have python installed and can activate from command line with `python`
\*\* recommend Miniconda that comes with a Python installation.


## why use virtual environments?
One of the most fun things about Python is the external libraries. With a simple `import this`<sup id="a1">[1](#f1)</sup> you can quickly use powerful chunks of other peoples pre-built code. The pros of using virtual environments massively outweigh the cons.

### pros :thumbsup:
- As soon as you start building multiple projects, you will likely need to install different versions of the same library or incompatible dependency versions. Virtual environments allow for different library versions on a single machine.

- Leaving a project be: it works, don't break it by trying to run it with a different environment.

- Don't need privileges to install packages into global site-packages directory

- Saves hours trying to figure out why some code runs on your machine but nobody else's.

- Easily resolve conflicts from having the wrong package version installed.

- Less upheaval when changing installed Python versions.

- Other people can use your code right out of the box; crucial when working on a team project.

- It is a job-marketable skill.

- Just don't install any packages to the GCC Mac system Python (located in /System/Library/Frameworks/Python.framework/Resources). Location if you type `$ where python` in new BASH. Risk cluttering up and causing unknown package dependency difficulties.

### cons :thumbsdown:
- Takes a little while to get head around what they are and how to use them.
- A little overhead to set up at the start of a project.
- Some discipline to maintain during a project.

{:refdef: .notice--warning}
**ProTip!:** keep your project's dependencies to a minimum. Even if you are superb at managing virtual environments. I have worked on client projects where they use multiple different packages for similar tasks. Their dependency list just grows and grows. This is a risk because each new dependency introduces something else to break, install and understand.
{: refdef}

## external packages protips
- `pip freeze` and direct output TO a file
- No substitute for the original package documentation. I still spend a lot of time in the docs even for packages I am very familiar with.
- I found it pretty empowering able to see the package source code. Reduces the untouchable aura around external packages. Two quick ways of seeing specific parts are:
  1. ctrl+clicking on package function or class in JetBrains and Visual Studio IDEs
  2. :key: using standard library `inspect` module

<script src="https://gist.github.com/w0rdsm1th/79c3be84ce04529db0d5fad9cd708b6d.js"></script>

## 3 way shootout and functionality review
Here I compare 3 different virtual environment managers. I focus on the practical and functional differences in their design. This is not a review of specific version and I am trying to remain unbiased.

- Can setup pyCharm to automatically use any of the options for a new project
https://www.jetbrains.com/help/pycharm/pipenv.html
- installing a specific version of a dependency with ==, or specific major version with =. or specify a minimum version with >=. See definition and link of "pinned packages" below for tips on when to use each.
- installing from github (a specific commit!) https://stackoverflow.com/a/32799944/3596968

# python foundation virtual env docs
good practical tutorial for venv, virtualenv and pipenv
https://docs.python-guide.org/dev/virtualenvs/

https://packaging.python.org/tutorials/installing-packages/#creating-virtual-environments

Virtualenv official docs
https://virtualenv.pypa.io/en/latest/

Venv official docs
https://docs.python.org/3/tutorial/venv.html

Pipenv official docs - uses pip-tools under the covers!
https://pipenv.readthedocs.io/en/latest/

The Hitchhiker's Guide to Python: Best Practices for Development
https://docs.python-guide.org/dev/virtualenvs/

## conda // miniconda // anaconda
First, its necessary to clear up different conda-suffixed terms used. [relevant SO question on differences](https://stackoverflow.com/questions/45421163/anaconda-vs-miniconda#45421527)
conda
: the command line environment manager and package installer. `conda env list`
miniconda
: lightweight bundle of conda package manager and a Python instance. You have to install and create your own environments from scratch.
anaconda
: __install__ a distribution of 200+ (and 3GB) pre-configured packages and Python instance.
: __cloud or repo__ the online package repository.

[conda docs](https://conda.io/en/latest/index.html)

referenced in conda docs - [Travis Oliphant \(creator of SciPy) conda tutorial](https://speakerdeck.com/teoliphant/packaging-and-deployment-with-conda?slide=3)

[Jake VanderPlas blog on conda myths](https://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/) Interesting section on Origins of conda: Guido at pyData saying "build it yourself"

++
brilliantly cross platform

Conda installs a brand new python.exe __in__ in the environment folder. This means you can up/down version Python compared to the system Python. E.g. you are running the latest 3.7, but a specific package needs 3.5, no problem! This is a pretty big advantage where people tie packages to specific python versions (e.g. only runs on 3.5 and no higher).

A very readable environment file. See my [template conda yml file with all the trimmings](/assets/2019-02/template_conda_env.yml). Contains the environment name or alias, Python version, conda and pip installations, hard version restrictions.

Can easily use either pip or conda to install packages from given package repo of choice.

And you can easily specify more package mirrors or channels **inside the requirements file**. This is really useful inside big organisations that have their own package repositories and block [PyPi](https://pypi.org) :shipit:

Can save your global configurations in .condarc file: organisation's proxy servers, folder location to make new environments `conda config --set`

Anaconda shell prompt: doesn't pollute PATH.

Works with R packages as well. Although I found it to be pretty buggy and R packrat the best and recognised way of performing dependency management in R.

--
Sometimes conda installs are a bit buggy or dont complete. I usually use pip to install numpy. Probably because conda installs from binaries but pip installs from source (e.g. running setup.py).
## TODO - pic of conda numpy error

The latest package versions are often not available on Anaconda Cloud. But can just install them using pip and [PyPi](https://pypi.org/).

Have to install all packages every time: the design means its not possible to share packages across environments.

# pipenv
++
combines pip and venv: installing and environment in one.

really informative and colourful command line:
- which python version being used
- still-processing indicators

Can specify different version of Python to installed Python instance. \*If have pyenv installed and configured, which is not straightforward on Windows.
https://pipenv.readthedocs.io/en/latest/advanced/#automatic-python-installation

Uses pip-tools library logic under the covers. smart dependency tracker and management
"Pipenv official docs - uses pip-tools under the covers!
https://pipenv.readthedocs.io/en/latest/"

Pipfile (no extension) is really flexible: conditional package installation (e.g. `pywinusb = {version = "*", sys_platform = "== 'win32'"}`), different mirrors, integrating with conda, injecting installing a different version of python, check security vulnerabilities
https://pipenv.readthedocs.io/en/latest/advanced/

higher level: abstracts away project creation and package installation.

lock file - reproducible and shareable. Pipfile is a Packaging Authority project: https://github.com/pypa/pipfile

Does also accept pip's requirements.txt file as inputs or outputs to environment creation.

Very similar to Ruby's bundler: per-project basis.

Give you insight into your dependency graph with `$ pipenv graph`

tracks Pipfile: readable. uses TOML https://github.com/toml-lang/toml
"The syntax for the Pipfile is TOML, and the file is separated into sections. [dev-packages] for development-only packages, [packages] for minimally required packages, and [requires] for other requirements like a specific version of Python."
https://realpython.com/pipenv-guide/#the-pipfile

Python 2.X support with --two flag: `pipenv --two install django`

--
have to update and snapshot the lockfile. takes a bit of discipline to reperform the snapshot, but a proven effective dependency management technique.

relatively poor Windows support: pyenv only got a port on Windows.

# venv, virtualenv
++
Included in standard library, see https://docs.python.org/3/library/venv.html

Similar interface to conda: activate, deactivate

Can have collection of core packages installed on base Python that dont have to re-install every time. Requires some discipline and agreement to deciding which packages should go into base and what should be per-environment.
`$ sudo apt-get install python-m2crypto
$ virtualenv env --system-site-packages`

customisable: can setup new global package channels in pip.conf. See https://superuser.com/a/1321140

--
Cannot create an environment with different versions of Python to installed Python.

requirements.txt not as readable or customisable as YAML.

People recommend [virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/en/latest/) for usability. Shortens commands needed and makes venv more flexible e.g. can ex-poste tell environment to use global Python site packages.




## glossary of terms used
Package (or library, APIs,...)
: Formal: a collection of importable functions and modules. Informal: other peoples code. Often designed for a specific purpose, documented, bundled up in a standard way for installation and hosted on a public repository. E.g. making HTTP requests, a wildly popular web framework (django), connecting to SQL databases, a testing framework.
: R calls them packages and **not** libraries (despite having a `library()` method to load them.......... :confounded:). Includes code, data, documentation and tests.
https://www.quora.com/What-is-a-Python-library-and-what-can-I-use-it-for
: Some people call them "APIs" because its an interface between your code and somebody elses.

Module
: > Importable chunks of code. Can be in a single script
-- from Python [official docs](https://docs.python.org/2/tutorial/modules.html)

Package repository (or repo, mirror)
: online collection of packages. E.g. These free, open source repos: [PyPi](https://pypi.org), [Anaconda Cloud](https://anaconda.org/anaconda/repo), [CRAN](https://cran.r-project.org/) for R. A 'mirror' is often an organisations internal controlled version E.g. big banks like to control what people are using.

Python standard library
: the collection of packages that come with Python, cover basic and essential functionality. [Docs here](https://docs.python.org/3/library/index.html). It is a flexible thing; in different major (2.X or 3.X) and minor versions of Python these are added to, renamed (e.g. urllib) or moved around.

Pinned package dependency
:
> Don’t ever use these styles in requirements.txt:
- `lxml`
- `lxml>=2.2.0`
- `lxml>=2.2.0,<2.3.0`

Instead, pin them:
- `lxml==2.3.4`
https://nvie.com/posts/pin-your-packages/
[pip-tools pypi](https://pypi.org/project/pip-tools/) A set of command line tools to help you keep your pip-based packages fresh, even when you’ve pinned them. You do pin them, right?


Dependency
: other libraries needed to make your own code or an external package run. E.g. Scikit-Learn needs or __depends on__ numpy for its numerical functions. So if you download Scikit-Learn then `pip` should identify this dependency relationship and install numpy too. Good libraries will be explicit about their dependency list.
: 'stuff' needed to run. A general concept/term used beyond Python packages. E.g. Some libraries require specific version of Python or BLAS.

**:key: key concept:** ...

Sub-dependency
: Libraries themselves often require other libraries. Fortunately good installers identify what is needed and install in one swoop. Generally **don't** go specifying every sub-dependency required to run your code, `pip` should resolve these.
E.g. Scikit-Learn depends on numpy, which itself depends on...

Virtual Environment
: self-contained, controlled collection of installed libraries. It can include a python.exe (more on this later). They are disposable, created for a specific purpose.

**'Virtual:'** because it superimposes installed resources on an installation of Python.
E.g. you download and install Python from [python.org](https://www.python.org/), create a virtual environment, 'activate' that environment, install a package (lets say `pip install requests`) and now the downloaded Python will be able to use `requests`. *BUT CRITICALLY* you have not really installed those packages to the downloaded Python. On deactivating the environment, you wont be able to use `requests`. _Its only virtual_.

There are a couple different ways of implementing this virtual nature.

**'Environment:'** because it contains the tools needed for development and execution of some code.

Global (or system) Python
: The global Python is the main python.exe used by your OS. Could be one you have downloaded. It depends on OS, but typically defined as the one on PATH.

Site packages
: the default install location for installed Python libraries.
https://stackoverflow.com/questions/31384639/what-is-pythons-site-packages-directory
https://stackoverflow.com/a/31384640/3596968

## further reading and thoughts
- packaging own code for distribution
https://realpython.com/pipenv-guide/#Package-distribution
https://snarky.ca/a-tutorial-on-python-package-building/

<!-- footnotes -->
<b id="f1">1</b> A fun Python Easter egg. Try it yourself! And then [read about it here.](https://www.python.org/dev/peps/pep-0020/#id4)[↩](#a1)

<b id="f2">2</b> footnote contents [↩](#a2)
