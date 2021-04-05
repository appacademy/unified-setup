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

Remember, if your shell is `zsh` your startup file will be `~/.zshrc`
If you shell is `bash` your startup file will be `~/.bashrc`

You can check which shell you have by running `echo $SHELL`

Open up the correct file for your system by using VSCode.

```shell
code ~/.zshrc
```

and add the lines pyenv told you to add.

```shell
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

To get your startup file to execute, restart your terminal.

## Installing dependencies on Windows and Ubuntu

If you use macOS you can skip this step.

For Windows and Ubuntu users you will need to install some extra dependencies
for python. These are listed on this page:

[pyenv Prerequities](https://github.com/pyenv/pyenv/wiki/Common-build-problems)

Since we are using Ubunut under Windows, you will just use the Ubuntu instructions
and run this command to update your apt repositories:

```shell
sudo apt update
```

and then run this command to install the packages listed on that page.

```shell
sudo apt-get install -y build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
xz-utils tk-dev libffi-dev liblzma-dev python-openssl git
```

## Installing python itself

Now we are ready to install python. Look on python.org and find the latest version
of Python 3.9.  (It's 3.9.4 as of this writing)

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

We can verify our python is the correct version by typing

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

Then after you have installed pipenv, add this line to your shell startup file
somewhere after the pyenv lines.

```shell
export PIPENV_VENV_IN_PROJECT=1
```

Congratulations! If you've completed all these steps you are ready to code in
Python!

[pyenv-installer]:https://github.com/pyenv/pyenv-installer