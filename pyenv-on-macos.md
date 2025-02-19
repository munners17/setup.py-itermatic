# Python3 on MacOS - Day to Day Environment Management with Pyenv

<p align="center">
  <img src="https://imgs.xkcd.com/comics/python_environment.png?raw=true" alt="XKCD Python"/>
</p>
XKCD nailed it with this comic regarding the state of Python frameworks, installations and environments.  

There are no shortage of articles out there walking through how to install Python.  This is how I do it, based on the set of requirements below I need for my day to day interaction with `:snake:`.

## My Requirements

1. A way to install software on MacOS that Python may require during project development.
2. A way to install ANY version of Python on a global or project basis.
3. The global version of Python3 should be relatively current (not used by MacOS) in order to install fun python packages like [art](https://pypi.org/project/art/).
4. Any python version installed via pyenv must support isolation via `virtualenv` so:
    1. The installed version stays untouched in case multiple instances of a single python version are required
    2. You can quickly tear down and recreate new instances during project development as necessary.
5. If I `cd` into the project, the shell automatically changes the version (or virtualenv) of Python that pertains to that project.

## Installation and Implementation

### Install homebrew and pyenv (Req #1)

1. Install [Homebrew](https://brew.sh/), you won't look back.
2. [pyenv](https://realpython.com/intro-to-pyenv/) is the lynchpin of operation "My Requirements"; follow the instructions [here](https://github.com/pyenv/pyenv#homebrew-in-macos).

At this point, you should have **homebrew** and **pyenv** installed.  The python environments maintained by pyenv should look something like this, which is pointing to the system python that MacOS uses.

```bash
~ $ pyenv versions
* system (set by /Users/user/.pyenv/version)
```

### Set the global (general use) Python3 version (Req #2, #3 and #4.1)
```bash
# Install your general use Python version
pyenv install 3.11.0

# Create a virtualenv of the global version
pyenv virtualenv 3.11.0 general3

# Set the global version
pyenv global general3

# Reload shell to refresh changes (or create a new terminal session)
exec $SHELL

# This should return the version of python set as global (ex: Python 3.11.0)
python -V

# Note:  As my global version, i'm using Python 3.11.0 but feel free to substitue the version of your choice.
```
### Set the global (general use) Python version (Req #3)

Let's set a custom python version for the itermatic project which can be found [here](https://github.com/munners17/setup.py-itermatic).

``` bash
# clone into curent directory and cd into the project
git clone https://github.com/munners17/setup.py-itermatic.git
cd setup.py-itermatic

# install the project python and create a virtualenv
pyenv install 3.8.13
pyenv virtualenv 3.8.13 itermatic3

# set it to the local project
pyenv local itermatic3

# Reload shell to refresh changes (or create a new terminal session)
exec $SHELL

# verify changes
cat .python-version     # should return 3.8.13
python -V               # should return 3.8.13

# Note:  For the itermatic project, i'm using Python 3.8.13 but feel free to substitue the version of your choice.
```



The project is now currently using python 3.8.13 installed by pyenv.  If you were using this version elsewhere (say in another project) and install packages, these packages would now pollute your current project environment.  So after a version of python is installed by pyenv, lets keep it pristine and instead setup a virtual environment based off that version.

```bash


```


#### Want to restore the currenty python version back to a somewhat default state?
```pip freeze | xargs pip uninstall -y```


