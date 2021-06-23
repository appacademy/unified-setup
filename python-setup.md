# Python Installation Instructions

Python is the second programming language we will use in this course.

> Note: We do not install the python using the installer from the python.org
> website in this course. If you have one installed you should uninstall it before
> installing this version of python.

Currently the curriclum for this course is compatible with Python 3.9.

## Installing pyenv

The first thing we need is to install the Python version manager ([pyenv](https://github.com/pyenv/pyenv)). This is similar
to the `nvm` tool we used to install Node.JS, except it controls what versions
of python we use on our system.

To install pyenv we use the [pyenv-installer]

From the installation instructions on the [pyenv-installer] website, it says we
run the following command:

```shell
curl https://pyenv.run | bash
```

Unlike `nvm`, `pyenv` does not automatically add it's startup lines to your
shell startup file.

The files that you have to change will depend on which shell you are running (you 
can check which shell you have by running `echo $SHELL`). Follow the instructions
to update the startup files associated with the shell that you are running.

### If your shell is `zsh`
1. Open up your `.profile` file with the following command.
```shell
code ~/.profile
```
2. Add the following lines to your `.profile`.
```shell
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
```
3. Open up your `.zprofile` file with the following command.
```shell
code ~/.zprofile
```
4. Add the following lines to your `.zprofile`. (Yes, these are the same as above.)
```shell
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
```
5. Open your `.zshrc` with the following command
```shell
code ~/.zshrc
```
6. Add the following line.
```shell
eval "$(pyenv init -)"
```

### If your shell is `bash`
1. Open up your `.profile` file with the following command.
```shell
code ~/.profile
```
2. Add the following lines.
```shell
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
```
3. Check if you have a `.bash_profile`. Run the following at the command line if you don't know.
```shell
if [ -f ~/.bash_profile ]; then echo "bash_profile exists"; else echo "bash_profile does not exist"; fi
```
If you don't have a `.bash_profile`, you can skip the rest of this step. If
you do, open up your `.bash_profile` file with the following command.
```shell
code ~/.bash_profile
```
4. Add the following lines to your `.bash_profile`. (Yes, these are the same as above.)
```shell
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
```
5. Open your `.bashrc` with the following command
```shell
code ~/.bashrc
```
6. Add the following line.
```shell
eval "$(pyenv init -)"
```

To get your startup file to execute, restart your terminal.

## Installing dependencies on Windows and Ubuntu

If you use macOS you can skip this step.

For Windows and Ubuntu users you will need to install some extra dependencies
for python. (See here for more information about the prerequisites: [pyenv Prerequities](https://github.com/pyenv/pyenv/wiki/Common-build-problems))

First run this command to update your apt repositories:

```shell
sudo apt update
```

and then run this command to install the packages listed on the pyenv.

```shell
sudo apt-get install -y build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
xz-utils tk-dev libffi-dev liblzma-dev python-openssl git
```

## Installing python itself

Now we are ready to install python. We will be installing Python version 3.9.4.

Then run this command to install python (you'll notice pyenv makes us put in the
_exact_ version instead of being able to just say `3.9` or `3`)

```shell
pyenv install 3.9.4
```

After some time this should complete without any errors. It could take a while
since you are compiling python from source code.

Once this is finished we also need to tell pyenv this is our default version
of python using this command:

```shell
pyenv global 3.9.4
```

Ensure that these changes take effect by closing your terminal and opening 
a new one. Then, we can verify our python is the correct version by typing

```shell
python --version
python3 --version
```

Both of these commands should show 3.9.4

## Pipenv

Another piece of software we will use in class is Pipenv.  Don't worry about what
this is right now, it's just enough to install it.

```shell
pip install pipenv
```

Then after you have installed pipenv, add this line to your shell startup
file (either your `.bashrc` or your `.zshrc`) somewhere after 
the  `eval "$(pyenv init -)"`.

```shell
export PIPENV_VENV_IN_PROJECT=1
```

Congratulations! If you've completed all these steps you are ready to code in
Python!

[pyenv-installer]:https://github.com/pyenv/pyenv-installer
