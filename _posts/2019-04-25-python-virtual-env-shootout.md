---
layout: single
title: >
  python virtual environment managers: 3 way shootout
excerpt: functional review of 3 popular virtual environment managers
header:
  overlay_image: "assets/2019/03/venv shootout - 1280px-Duel_between_Aaron_Burr_and_Alexander_Hamilton.jpg"
  caption: "Photo credit: [Wikipedia](https://en.wikipedia.org/wiki/File:Duel_between_Aaron_Burr_and_Alexander_Hamilton.jpg)"
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

If you don't know what python virtual environments are, see my [previous post][intro virtual environments] introducing virtual environments, why you should use them and a glossary of commonly used terms.
{: .notice}

> When doing anything in Python "There should be one – and preferably only one – obvious way to do it."
> <cite>Tim Peters, the Zen of Python in the `import this` Easter egg<sup id="a1">[1](#f1)</sup></cite>

Confusingly there are 3+ good virtual environment managers.<sup id="a1">[2](#f2)</sup> Here I compare the 3 mainstream options, focusing on the practical and functional differences in their design. This is not a tutorial or a review of a specific release. They are, in my new order of preference:
  1. the new kid [pipenv](https://pipenv.readthedocs.io/en/latest/)
  1. now pretty established [conda](https://conda.io/en/latest/index.html)
  1. standard library [venv](https://docs.python.org/3/library/venv.html)


  ![](/assets/2019/03/venv office mexican standoff - The Office US.jpg "3 way functionality shootout"){:class="img-responsive"}

Reader objectives from this post:
- Learn the core functional differences between 3 leading virtual environment managers.
- Usability tips for each library e.g. template environment files. A [conda envrironment.yml][conda yaml], a [pipenv Pipfile][pipenv Pipfile] and a [venv pip requirements.txt][pip requirements.txt]. These files are just templates, you should modify these files with your own environment name and dependencies.

## conda
I often see beginners struggle with the very similar terms and products: conda, miniconda and anaconda. Before diving into functionality, I differentiate between them below.

conda
: command line environment manager and package installer e.g. `conda env list`. The [conda docs](https://conda.io/en/latest/index.html).

miniconda
: lightweight bundle of conda package manager *and* a Python interpreter. You have to download and install packages to create your own environments from scratch.

anaconda
: __install__ a distribution of 200+ (and ~3GB) pre-configured packages, conda package manager and Python interpreter. You don't have to curate a development environment for analytical Python, it has already been built!
: __cloud, repo or .org__ an [online package and data science notebook repository](http://anaconda.org).
: __Inc__ the organisation behind it all, see [Anaconda's about us](https://www.anaconda.com/about-us/).

### good stuff ++ :thumbsup:
Brilliantly cross platform: tried and tested effortless across Windows, Mac and Unix.

Totally isolated environments: Conda installs a brand new python interpreter __in__ in the environment folder! This means you can up/down version Python compared to the system Python. E.g. you are running the latest 3.7, but a specific package needs 3.5, no problem! This is a pretty big advantage where people tie packages to specific python versions (e.g. this package only runs on 3.5 and no higher).

Flexible and backwards compatible: can easily use either pip or conda to install packages on the command line interactive shell OR in the [conda yaml][].

A readable and flexible environment file. See my [template conda yml file with all the optional section trimmings][conda yaml]. You can specify the new environment's name, Python version, and conda and pip installed packages.

You can easily specify more package mirrors or channels **inside the requirements file**. This is really useful inside big organisations that have their own package repositories and block [PyPi](https://pypi.org) :shipit:

Lasting configurations across environments: Can save your global configurations in the user's .condarc configuration file: e.g. organisation's proxy servers, folder location to make new environments, use `conda config --set`.

Miniconda comes with its own shell so it doesn't pollute your PATH.

Works with R environments as well. Although I found it to be pretty buggy and R [packrat](https://rstudio.github.io/packrat/) is currently best way of performing dependency management in R.

### bad stuff -- :thumbsdown:
Sometimes conda installs are a bit buggy or don't complete. For example I recently have had to use pip to install numpy on Windows 10. This is because conda installs from binaries but pip (which stands for "Pip Installs Python") installs in python (e.g. running setup.py).

The latest package versions are often not available on conda repositories. But can just install them using pip and [PyPi](https://pypi.org/).

You have to install all packages every time: the design means its not possible to share packages across environments. You would have to use full Anaconda install for that.

## pipenv
Pipenv was the motivation for writing this post. Pipenv is new, authored by big names in the python community and uses best-in-class methods. I wanted to compare this upstart and contrast against my old favourite conda.

After a controversial and somewhat catty reception in [reddit.com/r/python](https://www.reddit.com/r/Python/comments/5pmb8o/announcing_pipenv_from_kenneth_reitz/)
and [Kenneth's response](http://journal.kennethreitz.org/entry/r-python).

### good stuff ++ :thumbsup:
Combines pip and venv: installing packages and creating environment in one. This combination is a "higher level abstraction" in programming parlance. It is a proven workflow similar to Ruby's bundler: per-project basis environment creation.

Installs packages concurrently: if you have 45 dependencies it installs them together. Although in practice I found that installs are much slower than Conda.

Creates a very pretty and colourful shell with really informative user messages. E.g. which python interpreter and version is used to create the environment and what step of environment creation.

It is theoretically possible to specify different version of Python to the global Python. \*\*If have pyenv installed and configured, which is not straightforward on Windows. See https://pipenv.readthedocs.io/en/latest/advanced/#automatic-python-installation

Pipfile (no file extension) is really flexible. For example allowing package installation conditional on the host operating system (e.g. `pywinusb = {version = "*", sys_platform = "== 'win32'"}`), different mirrors, integrating with conda, and different versions of python.

Pipfile has different sections for packages needed for development and distribution. This reduces maintenance overhead, you can specify a single file to setup development workstations and distribute with your final app.

Pipfile.lock: guaranteed reproducible and shareable environment snapshot that you know will install and should be tied to a version of code that executes. With a requirements.txt there is no guarantee it will actually complete installing or is coupled as tightly with your code development. Replicates successful workflow in other languages e.g. Node.js, Rust and Ruby.

Long term and generally endorsed future best practice: Pipfile is a Packaging Authority project and the long term replacement for requirements.txt. See Python Packaging Authority [project page](https://github.com/pypa/pipfile).

Flexible and backwards compatible: also accepts a pip requirements.txt file as an input or output to environment creation.

Smart dependency tracker and resolution: uses pip-tools library logic under the covers.

Informative: see your project's dependency graph with `pipenv graph`

Can do quick check security vulnerabilities in your project's dependencies with `pipenv check`

Pipfile is very readable, uses TOML https://github.com/toml-lang/toml
"The syntax for the Pipfile is TOML, and the file is separated into sections. [dev-packages] for development-only packages, [packages] for minimally required packages, and [requires] for other requirements like a specific version of Python."
https://realpython.com/pipenv-guide/#the-pipfile

Python 2.X support with --two flag e.g. `pipenv --two install django`

### bad stuff -- :thumbsdown:
Cannot share a projects environment for another project's work: abstracting away project and environment creation combines the steps and ties your hands. This really hurts automated repeated testing that needs to create a Python environment as part of testing. The number of environments increases wildly and need manually deleting.

Have to update and snapshot the lockfile. It takes a bit of discipline to reperform the snapshot, but a proven effective dependency management technique borrowed from other languages.

Generally good cross platform support. However I run into issues instlaling different Python versions to global on Windows because this functionality depends on pyenv which is unsupported on Windows.

## venv // virtualenv
### good stuff ++ :thumbsup:
Included in standard library as of Python 3.3. So you can start using out of the box, no dependency on .

Can have collection of core packages installed in base Python site-packages folder that don't have to re-install for a project. Using command `virtualenv env --system-site-packages`
\*\*Can only be run __during__ environment creation. But virtualenvwrapper which sits on top of venv can change this setting in an already created environment.
\*\*Requires some discipline and agreement to deciding which packages should go into base and what should be per-environment.

Can set global configurations in pip.conf for preferences that persist: e.g. can change global package channels. See https://superuser.com/a/1321140.

### bad stuff -- :thumbsdown:
Cannot create an environment with a different version of Python to global Python.

requirements.txt not as readable or customisable as conda's YAML and pipenv's TOML format.
https://pip.pypa.io/en/latest/user_guide/#requirements-files

[virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/en/latest/) makes venv more usable. It shortens commands needed and makes venv more flexible e.g. can toggle environment setting to use global Python site packages, a setting only possible to choose on creation with venv.

## the verdict // TLDR;
So which environment manager is best? Ultimately it comes down to your own preferences and type of Python you write and projects you work on.

If you are heavily cross Operating System, I'd recommend conda.

If you are interested in "project workflows" to develop websites then I'd recommend Pipenv. And I _quite like_ Pipenv. It uses best-in-class resources (e.g. TOML file format and pip-tools library), and it follows other language's approach to environment management.

I personally rank them Conda, Pipenv, then Venv for high level reasons below.

1. Conda
  - Scientific environment and packages support.
  - Windows support for different versions of python interpreters.
  - Highly customisable development inside company's infrastructure.


1. Pipenv
  - Project-environment coupling means starting a project and creating an environment is a slick single step but the architecture means you cannot use an environment for multiple projects. This can be a real pain depending on your work habits. E.g. setting up automated tests, creating lots of envs that are then orphaned. See:  https://github.com/pypa/pipenv/issues/796#issuecomment-374211264

1. Venv
  - Comews with python standard library so no need to download anything more. Useful if you're behind a firewall.
  - Quite primitive and relatively less user friendly.

<!-- footnotes -->
## footnotes
<b id="f1">1</b> A fun Python Easter egg. Try it yourself and then [read about it here.](https://www.python.org/dev/peps/pep-0020) [↩](#a1)

<b id="f2">2</b> Other notable mentions are [Poetry](https://github.com/sdispater/poetry) and [Hatch](https://github.com/ofek/hatch)  [↩](#a2)
