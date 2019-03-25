---
layout: single
title: >
  python virtual environment managers: which one's the best?
excerpt: functional review of 3 popular virtual environment managers
last_modified_at: 2019-03-25
tags: [intro to, programming, python]
---
<!-- reference style links -->
[intro virtual environments]: _posts\2019-03-01-intro-python-virtual-environments.md
[conda yaml]: assets/2019/03/template_conda_env.yml
[pipenv Pipfile]: assets/2019/03/Pipfile
[pip requirements.txt]: assets/2019/03/requirements.txt
<!-- end reference style links -->

<!-- #TODO
- a judgement of which is best for what?? "the verdict"
-
[conda's yaml][conda yaml], [pipenv's Pipfile][pipenv Pipfile] (weirdly doesnt allow an extension, but not pipenv's fault) and venv which uses a pip [requirements.txt][pip requirements.txt].
-->

See my [previous post][intro virtual environments] introducing virtual environments, why you should use them and a glossary of commonly used terms.
{: .notice}

> When doing anything in Python "There should be one – and preferably only one – obvious way to do it."
> <cite>Tim Peters, the Zen of Python in the `import this` Easter egg<sup id="a1">[1](#f1)</sup></cite>

Confusingly there are 3+ good virtual environment managers out there. The standard library [venv](https://docs.python.org/3/library/venv.html), now pretty established [conda](https://conda.io/en/latest/index.html), and the new kid [pipenv](https://pipenv.readthedocs.io/en/latest/). Here I compare the 3 options, focusing on the practical and functional differences in their design. This is not a tutorial or review of a specific release.

Reader objectives from this post:
- Learn the core functional differences between 3 leading virtual environment managers.
- Template environment files: a [conda envrironment.yml][conda yaml], a [pipenv Pipfile][pipenv Pipfile] and a [pip requirements.txt][pip requirements.txt] that venv uses.

![](/assets/2019/03/venv office mexican standoff - The Office US.jpg "3 way functionality shootout"){:class="img-responsive"}

## conda
[Jake VanderPlas blog on conda myths](https://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/) has an interesting section on origins of conda: Guido telling first pyData conference to "build it yourself".

I often see beginners struggle with the very similar terms and products: conda, miniconda and anaconda. Before diving into functionality, I differentiate between them below.

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

## the verdict
