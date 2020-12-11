# Checking your Setup

Knowing if you've followed all the steps correctly can be tricky. There's
so many things that can go wrong, and everyone's computer is different. To help with
this problem, AppAcademy has created a script that checks your setup to verify
it is done correctly.

To run this script you simply open a terminal and run this command:

```shell
curl -s https://raw.githubusercontent.com/appacademy/aa-setup-checker/master/run.sh | bash
```

This command will download a script from our github page and if your setup is correct
you should see output like this:

```shell
――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――
Checking macOS
――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――
macOS Version: 11.0.1
――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――
Checking Shell
――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――
Shell: /bin/zsh
Shell Startup File: /Users/echo/.zshrc
――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――
Checking Node.JS
――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――
Node Binary: /Users/echo/.nvm/versions/node/v12.18.4/bin/node
Node Version: v12.18.4
NPM Binary: /Users/echo/.nvm/versions/node/v12.18.4/bin/npm
NPM Version: 6.14.6
Mocha Binary: /Users/echo/.nvm/versions/node/v12.18.4/bin/mocha
Mocha Version: 8.1.3
Node.JS is OK
――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――
Checking VSCode
――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――
Code Binary: /usr/local/bin/code
Version: 1.49.0
VSCode is OK
――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――
Checking Python
――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――
pyenv version: pyenv 1.2.21
Python Binary: /Users/echo/.pyenv/shims/python
Python3 Binary: /Users/echo/.pyenv/shims/python3
Python Version: 3.8.6
pipenv Binary: /Users/echo/.pyenv/shims/pipenv
pipenv Version: pipenv, version 2020.8.13
Python OK
――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――
Checking Docker
――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――
Docker Binary: /usr/local/bin/docker
Docker Version: Docker version 19.03.13, build 4484c46d9d
Docker is OK
――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――
Congratulations, you have everything installed properly!
――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――
```

If you get the Congratulations message you'll know you have everything setup
properly. The script tries to tell you what steps you should probably take
if some piece fails.

If you get a failure and don't know how to fix it, feel free to post your output in
Slack or to ask an instructor for help.

> Note if you have an apple silicon mac, you can't install Docker, so expect
> that piece to always fail the check.

