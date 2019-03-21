---
layout: single
title: >
  intro to: python virtual environments
excerpt: why you should use them and a functional difference review of 3 popular virtual environment managers
last_modified_at: 2019-03-19
header:
  overlay_image: "/assets/2019/03/snakemassage3-COURTESY CAPTIVATINGCEBU-YOUTUBE - cropped.jpg"
  caption: "Photo credit: [**CAPTIVATINGCEBU**](https://www.youtube.com/user/captivatingcebu)"
tags: [intro to, programming, python]
---
<!-- #TODO
- a judgement of which is best for what??
- define isolated environment as per Travis CI: contains a python executible
in contrast: a shim
- project workflow diagram? create env, update env,
- module definition is correct according to https://packaging.python.org/overview/#python-modules
- Hash checks by pipenv
-->

<!-- reference style links -->
[conda yaml]: assets/2019/03/template_conda_env.yml
[pipenv Pipfile]: assets/2019/03/Pipfile
[pip requirements.txt]: assets/2019/03/requirements.txt


![](https://imgs.xkcd.com/comics/python_environment.png "prevent Python paralysis: use virtual environments"){:class="img-responsive"}

When I first started learning Python virtual environments seemed abstract and unimportant. I could get setup and code some badass stuff right now, why bother to learn about them? And they take a little while to learn. But learning to use them has taken away a lot of the frequent problems I was facing at the start. And they have been a great primer for thinking about the interpreter and environment that is actually making my code run.

Reader objectives from this post:
- Understand what virtual environments are and why you should use them.
- Learn the core functional differences between 3 leading environment managers.
- Usability tips e.g. setting up your IDE to automatically create an environment on creating new project, template environment files: a [conda envrironment.yml][conda yaml], a [pipenv Pipfile][pipenv Pipfile] and a [pip requirements.txt][pip requirements.txt] that venv uses.
- Glossary of common term definitions.

What this is not: a step-by-step tutorial of specific virtual environment managers and their commands. As an individual blogger it is hard to keep such tutorials up-to-date. I do recommend these tutorials [for venv and pipenv](https://docs.python-guide.org/dev/virtualenvs/) and [conda](https://speakerdeck.com/teoliphant/packaging-and-deployment-with-conda) (written by Travis Oliphant, the creator of SciPy and founder of Anaconda!).

## why use virtual environments?
![](/assets/2019/03/virtual_envs diagram3.png "key concept of virtual environments: isolation"){:class="img-responsive"}

One of the most fun things about Python is the external libraries. With a simple `import this`<sup id="a1">[1](#f1)</sup> you can quickly use powerful chunks of other peoples pre-built code. And as your Python experience grows, you will almost certainly start to work on different projects that require different versions of the python interpreter or different versions of the same package dependency or sub-dependencies.

In the example environment sketch above there are 3 different environments. There is a `global python` environment which is left pristine and used just to spawn working environments. And there are 2 working environments `professional_work_project` and `dev` and each has a different version of [SQLAlchemy](https://docs.sqlalchemy.org/) installed.
- `professional_work_project` uses V0.9 because the project started 2 years ago and heavily relies on some now deprecated functionality.
- `dev` uses V1.3 (latest at time of writing) because you like to live on the bleeding edge.

Virtual environments allow you to install both versions of the SQLAlchemy package simultaneously. Without virtual environments you would have to constantly up and downgrade to work on either `professional_work_project` or `dev`.

Below I list other benefits to being able to isolate and control a project's dependencies. The reasons to use virtual environments massively outweigh reasons not to use: by 10 good reasons to 3 lazy reasons.

### reasons to use :thumbsup:
1. Allows you to work on different projects needing different versions of the same library or sub-dependencies on the same machine.

2. Mothballing and restarting a project: the code will run, irrespective of what has happened to project dependency versions or your workstation setup. The exact dependencies are basically cryogenically frozen.

3. Don't need computer admin privileges to install packages into global Python's site-packages directory. Insufficient privileges to install packages is so often an issue when working on a locked down work computer.

4. Potentially hours saved trying to figure out why code runs on your machine but nobody else's.

5. Easily resolve conflicts due to having a wrong package version installed.

6. Less upheaval when changing Python versions (e.g. from 3.6 to 3.7).

7. Other people can use your code right out of the box; this is crucial when working on a team project.

8. It is a job-marketable skill :moneybag:.

9. Can easily setup your favourite IDE's defaults to use the big virtual environment managers for a new project, and execute code in the environment. See [pyCharm](https://www.jetbrains.com/help/pycharm/pipenv.html) and [Visual Studio](https://docs.microsoft.com/en-us/visualstudio/python/managing-python-environments-in-visual-studio?view=vs-2017) docs.

10. They are a great primer for more advanced Python packaging tools and techniques e.g. [Docker](https://www.fullstackpython.com/docker.html). It is still best practice to use a virtual environment manager to configure your Python environment e.g. conda on [Docker](https://hub.docker.com/u/continuumio). For more on these advanced deployment methods see [Python docs](https://packaging.python.org/overview/#depending-on-a-separate-software-distribution-ecosystem).

11. If running Mac OS there is a system Python first on path (located in /System/Library/Frameworks/Python.framework/Resources). Use command `where python` in a new BASH to see its location. This is for the operating system and there is a risk using it for development and installing packages will cause unknown difficulties. Unfortunately if you forget and just type `pip install SOME_PACKAGE` into a new BASH then it installs to this Python....

### reasons not to use :thumbsdown:
1. Time to learn: Takes a little while to get head around what they are and how to use them.
2. A little overhead to set up at the start of a project.
3. Some discipline to maintain during a project.

{:refdef: .notice--warning}
**ProTip!:** keep your project dependencies to a minimum. Even if you are superb at managing virtual environments. I have worked on projects where the team will use multiple different packages for similar tasks. Their dependency list just grows and grows. This is a risk because each new dependency introduces something else to break, install and understand.
{: refdef}

## virtual environment protips
- While you can install packages on the fly using pip, it is good practice and efficient to standardise virtual environment creation using a file to ensure reproducibility. I use a template for each manager which contains the structure and syntax of the more advanced usages: [conda's yaml][conda yaml], [pipenv's Pipfile][pipenv Pipfile] (doesnt allow an extension) and venv which uses a pip [requirements.txt][pip requirements.txt].
- If distributing your environment file so others can run your app, or , it is recommend to specify dependency versions with ==, or specific major version with =. or specify a minimum version with >=.
- All the environment files support installing from GitHub (even a specific commit!) and the templates above contain sample syntax.

Be aware: no one way to activate single virtual environment manager (venv) on same OS (Windows).
![](/assets/2019/03/venv activation commands - python docs venv.html creating-virtual-environments.JPG "be aware: no one way to activate even same virtual environment manager"){:class="img-responsive"}

## 3 way shootout and functionality review
> When doing anything in Python "There should be one – and preferably only one – obvious way to do it."
> <cite>Tim Peters, the Zen of Python in the `import this` Easter egg<sup id="a1">[1](#f1)</sup></cite>

Confusingly there are 3+ different and good virtual environment managers out there. The standard library [venv](https://docs.python.org/3/library/venv.html), now pretty established Anaconda's [conda](https://conda.io/en/latest/index.html), and the new kid [pipenv](https://pipenv.readthedocs.io/en/latest/). Here I compare the 3 options, focusing on the practical and functional differences in their design. This is not a tutorial or review of a specific release.

![](/assets/2019/03/venv office mexican standoff - The Office US.jpg "3 way functionality shootout"){:class="img-responsive"}

## conda
[Jake VanderPlas blog on conda myths](https://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/) has an interesting section on origins of conda: Guido telling first pyData conference to "build it yourself".

I often see beginners struggle with the very similar terms and products: conda, miniconda and anaconda. I differentiate between them below.

conda
: command line environment manager and package installer e.g. `conda env list`. The [conda docs](https://conda.io/en/latest/index.html).

miniconda
: lightweight bundle of conda package manager *and* a Python interpreter. You have to download and install packages to create your own environments from scratch.

anaconda
: __install__ a distribution of 200+ (and 3GB) pre-configured packages, conda package manager and Python interpreter. You don't have to create a development environment for analytical Python, it has already been built!
: __cloud, repo or .org__ an online package and data science notebook repository [here](http://anaconda.org).
: __Inc__ the organisation behind it all, see [Anaconda's about us](https://www.anaconda.com/about-us/).

### good stuff ++ :thumbsup:
Brilliantly cross platform: tried and tested effortless across Windows, Mac and Unix.

Totally isolated environments: Conda installs a brand new python interpreter __in__ in the environment folder! This means you can up/down version Python compared to the system Python. E.g. you are running the latest 3.7, but a specific package needs 3.5, no problem! This is a pretty big advantage where people tie packages to specific python versions (e.g. this package only runs on 3.5 and no higher).

Flexible and backwards compatible: can easily use either pip or conda to install packages on the command line interactive shell OR in the [conda yaml][].

A readable and flexible environment file. See my [template conda yml file with all the optional section trimmings][conda yaml]. You can specify the environment name, Python version, and conda and pip installed packages.

You can easily specify more package mirrors or channels **inside the requirements file**. This is really useful inside big organisations that have their own package repositories and block [PyPi](https://pypi.org) :shipit:

Lasting configurations across environments: Can save your global configurations in .condarc file: e.g. organisation's proxy servers, folder location to make new environments, use `conda config --set`.

Miniconda comes with its own shell so it doesn't pollute your PATH.

Works with R packages as well. Although I found it to be pretty buggy and R [packrat](https://rstudio.github.io/packrat/) is currently best way of performing dependency management in R.

### bad stuff -- :thumbsdown:
Sometimes conda installs are a bit buggy or don't complete. For example I usually use pip to install numpy. Probably because conda installs from binaries but pip installs from source (e.g. running setup.py).

The latest package versions are often not available on Anaconda Cloud. But can just install them using pip and [PyPi](https://pypi.org/).

Have to install all packages every time: the design means its not possible to share packages across environments. You would have to use full Anaconda install for that.

## pipenv
Pipenv was the motivation for writing this post. Its a new package with great pedigree from the Python community, using best-in-class methods.

After a controversial and somewhat catty reception in [reddit.com/r/python](https://www.reddit.com/r/Python/comments/5pmb8o/announcing_pipenv_from_kenneth_reitz/)
http://journal.kennethreitz.org/entry/r-python
Video https://www.reddit.com/r/Python/comments/8jfmv8/kenneth_reitz_pipenv_the_future_of_python/

### good stuff ++ :thumbsup:
Combines pip and venv: installing packages and creating environment in one.

Higher level: abstracts away project creation and package installation. A proven project workflow similar to Ruby's bundler: per-project basis environment creation.

Installs packages concurrently: if you have 45 dependencies it installs them together, which makes for a faster install time compared to conda or venv.

Creates a very pretty and colourful shell with really informative user messages:
- which python version is used to create the environment
- what step of environment creation
- still-processing indicators

Can specify different version of Python to installed Python interpreter. \*\*If have pyenv installed and configured, which is not straightforward on Windows. See https://pipenv.readthedocs.io/en/latest/advanced/#automatic-python-installation

Smart dependency tracker and resolution: uses pip-tools library logic under the covers.

Pipfile (no extension) is really flexible: conditional package installation (e.g. `pywinusb = {version = "*", sys_platform = "== 'win32'"}`), different mirrors, integrating with conda, injecting installing a different version of python.

Pipfile has sections for development and actual app packages: single file to setup development workstations and distribute with your final app. This reduces maintenance overhead.

Pipfile.lock: a reproducible and shareable environment snapshot that you know will install and should be tied to a version of code that executes. With a requirements.txt there is no guarantee it will actually complete installing or is coupled as tightly with your code development. Replicates successful workflow in other languages e.g. Node.js, Rust and Ruby.

Pipfile is a Packaging Authority project and the long term replacement for requirements.txt. See Python Packaging Authority [project page](https://github.com/pypa/pipfile).

Flexible and backwards compatible: also accepts a pip requirements.txt file as an input or output to environment creation.

Informative: see your project's dependency graph with `pipenv graph`

Can do quick check security vulnerabilities in your project's dependencies with `pipenv check`

Pipfile is very readable, uses TOML https://github.com/toml-lang/toml
"The syntax for the Pipfile is TOML, and the file is separated into sections. [dev-packages] for development-only packages, [packages] for minimally required packages, and [requires] for other requirements like a specific version of Python."
https://realpython.com/pipenv-guide/#the-pipfile

Python 2.X support with --two flag: `pipenv --two install django`

### bad stuff -- :thumbsdown:
Cannot share environments across projects: abstracting away project and environment creation combines the steps and ties your hands.

have to update and snapshot the lockfile. takes a bit of discipline to reperform the snapshot, but a proven effective dependency management technique borrowed from other languages.

Generally good cross platform support. However depends on pyenv to automatically resolve required Python interpreter version that is unsupported on Windows.

## venv // virtualenv
### good stuff ++ :thumbsup:
Included in standard library as of Python 3.3. So you can start using straightaway with recent Python interpreters.

Because project creation and environment creation are de-coupled, you can share an environment across projects.

Can have collection of core packages installed in base Python site-packages folder that don't have to re-install for a project. Using command `virtualenv env --system-site-packages`
\*\*Can only be run __during__ environment creation. But virtualenvwrapper which sits on top of venv can change this setting in an already created environment.
\*\*Requires some discipline and agreement to deciding which packages should go into base and what should be per-environment.

global configuration file pip.conf to setup preferences that persist: e.g. can change global package channels. See https://superuser.com/a/1321140

### bad stuff -- :thumbsdown:
Cannot create an environment with different versions of Python to installed Python.

requirements.txt not as readable or customisable as conda's YAML and pipenv's TOML format.
https://pip.pypa.io/en/latest/user_guide/#requirements-files

People recommend [virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/en/latest/) for usability. It shortens commands needed and makes venv more flexible e.g. can toggle environment setting to use global Python site packages, a setting only possible to choose on creation with venv.

## glossary of common terms
Package (or library, APIs,...)
: Formal: a collection of importable functions and modules.
: Informal: other peoples code. Often designed for a specific purpose, documented, bundled up in a standard way for installation and hosted on a public repository. E.g. [making HTTP requests](http://docs.python-requests.org/en/latest/), [a web framework](https://www.djangoproject.com/) or [common machine learning techniques](https://scikit-learn.org/stable/).
: Some people call them "APIs" because its an interface between your code and somebody elses.

Module
: > Importable chunks of code. Can be in a single script.
-- from Python [official docs](https://docs.python.org/2/tutorial/modules.html)

Package repository (or repo, mirror)
: online collection of packages. For example these free, open source repos: [PyPi](https://pypi.org), [Anaconda Cloud](https://anaconda.org/anaconda/repo), [CRAN](https://cran.r-project.org/) for R. A 'mirror' is often an organisations internal controlled version E.g. big banks like to control what people are using.

Python standard library
: the collection of packages that come with Python, cover basic and essential functionality. [Docs here](https://docs.python.org/3/library/index.html). It is a flexible thing; in different major (2.X or 3.X) and minor versions of Python these are added to, renamed (e.g. urllib) or moved around.

Pinned dependency packages
: Tying to a specific dependency major.minor version number. See [this blog post](See https://nvie.com/posts/pin-your-packages/) from the developer of `pip-tools` package.
*Avoid* below patterns that are vague about version in your project requirements.txt (or conda.yaml or Pipfile,...):
- `lxml`
- `lxml>=2.2.0`
- `lxml>=2.2.0,<2.3.0`

Instead, pin the dependency:
- `lxml==2.3.4`

Dependency
: other libraries needed to make your own code or an external package run. E.g. Scikit-Learn needs or __depends on__ numpy for its numerical functions. So if you download Scikit-Learn then `pip` should identify this dependency relationship and install numpy too. Good libraries will be explicit about their dependency list.
: 'stuff' needed to run. A general concept/term used beyond Python packages. E.g. Some libraries require specific version of Python or BLAS.

Sub-dependency
: Libraries themselves often require other libraries. Fortunately good installers identify what is needed and install in one swoop. Generally __don't__ go specifying every sub-dependency required to run your code, `pip` should resolve these.
E.g. Scikit-Learn depends on numpy, which itself depends on...

Virtual Environment
: self-contained, controlled collection of installed libraries. It can include a python interpreter. They are disposable, created for a specific purpose or project.

As opposed to: a python environment that is shared across projects or tasks. It's not so disposable and would probably "break many things" if it got deleted.

> "A virtual environment is a unique combination of a specific Python interpreter and a specific set of libraries that is different from other global and conda environments."
> <cite> https://docs.microsoft.com/en-us/visualstudio/python/selecting-a-python-environment-for-a-project?view=vs-2017#use-virtual-environments </cite>

**'Virtual:'** because it superimposes installed resources on an installation of Python.
E.g. you download and install Python from [python.org](https://www.python.org/), create a virtual environment, 'activate' that environment, install a package (lets say `pip install requests`) and now the downloaded Python will be able to use `requests`. *BUT CRITICALLY* you have not really installed those packages to the downloaded Python. On deactivating the environment, you wont be able to use `requests`. *Its only virtual*.

**'Environment:'** because it contains the tools needed for development and execution of some code.

Global (or system) Python
: The "main" installed python interpreter that you are using. Could be one you have downloaded from [python.org](https://www.python.org/) or bundled with another utility. No definitive single location or python version. It depends on OS, but typically defined as first one on PATH. If you have multiple installed try to be mindful of which you are using, where it is installing libraries and what version it is!

Site packages
: the default install location for installed Python libraries.
https://stackoverflow.com/questions/31384639/what-is-pythons-site-packages-directory
https://stackoverflow.com/a/31384640/3596968

YAML / yaml / yml
: "Yaml Aint Markup Language". https://noyaml.com/
Abbreviated as yml for 3 letter file extensions.



<!-- footnotes -->
<b id="f1">1</b> A fun Python Easter egg. Try it yourself! And then [read about it here.](https://www.python.org/dev/peps/pep-0020)[↩](#a1)
