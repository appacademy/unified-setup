# Getting Started with git
### What is git?

> Git is a free and open source distributed version control system designed to
> handle everything from small to very large projects with speed and efficiency.

git is a software program much like *MS Word* or *Google Chrome* but it is part
of a class of programs known as **cli tools**. This program does not have a UI
like most programs we are familiar with but instead is accessible primarily
through our **command line**/**terminal**.

Being accessible primarily only through the **command line**/**terminal** sounds
like a huge restriction but it allows us as developers to use it for what it's
good at and for it to then quickly go away. So what does git do? Well it is a
*Version Control System* or **VCS**. It keeps track of a set of files over time.


Each time changes are wanting to get recorded, they are wrapped in what we call
a 'commit' and that commit is saved to the repo as a snapshot of the files at
that time. The tracking and reconciling abilities that git has to handle
conflicts makes git an effective tool for many developers to work on the same
codebase at the same time as well as to record the history of a project in the
case an issue is introduced. 

### What is GitHub? 
Github is a company that provides hosting for git repos. It works together with
the git cli tools to manage the codebase by making or deleting branches,
creating pull requests, and sharing the git project with other developers. 

---

## Installing git
### Windows
If you have WSL already setup and are using an Ubuntu distribution, you already
have git within linux! If you are using a different distribution you may need to
manually install git. 

<!-- While we don't need git installed in Windows, we do want to have the
git-credential-manager-core installed. It comes bundled with git so we can
easily install it in Windows by using the installer found
[here][git-win]. 

Once you've downloaded one of the "Git for Windows Setup" distributions (either
32-bit or more likely 64-bit) you can launch the installer and accept all the
defaults. 

Now that git-credential-manager-core is installed, we can restart our terminal
and continue on working through this guide. -->

### Mac
Mac comes with some tools by default. git is one that we want to make sure is up
to date so we can run the following in our terminal. 

```shell
xcode-select --install
```

## Configuring git
Once you have installed git, configure the information that gets logged for each
of your commits by updating the default (global) credentials that git uses. (You
could overwrite these credentials temporarily per local repo. While that
shouldn't be necessary when working on App Academy projects, it is helpful to
know that it is an option.) You will also want to set the default branch to
`main`.

In your terminal (on Mac or WSL), run

```shell
git config --global user.name "Your Name" 
git config --global user.email "Your Email"
git config --global init.defaultBranch main
```

## Configuring github
As previously mentioned, Github provides a mechanism to share code with other
developers. Because of the nature of code, there needs to be a way to
authenticate to make sure that someone is authorized to fetch or contribute new
code. 

Thankfully for us, git handles this authentication flow automatically but for
Github, we can't use our Github accounts password. Instead, we can use a
Personal Access Token as a password to authenticate to Github and save it in a
password manager of sorts so we don't have to use the PAT every command that
requires auth. 

### Github Authentication
Below, we'll find some instructions for setting up authentication on either Mac
or Windows. Currently, it is recommended for both WSL and MacOS users to
[follow this guide](./gcm-setup.md) and set up Git Credential Manager (GCM) on
their machines. GCM provides a unified authentication experience that 
integrates into native security features offered by your operating system.

While the instructions below _will_ provide a workable result, GCM offers a 
more streamlined and hassle-free solution.

### Secrets Manager
Before we get a PAT from Github and use it for auth - we should setup our
Secrets Manager. 

#### Windows
WSL doesn't have a password manager by default in most distributions so we would
need to install one if we don't want our token saved in plain text or only
temporarily in memory. 

While we don't need git installed in Windows, we do want to have the
git-credential-manager-core installed. It comes bundled with git so we can
easily install it in Windows by using the installer found
[here][git-win]. 

Once you've downloaded one of the "Git for Windows Setup" distributions (either
32-bit or more likely 64-bit) you can launch the installer and accept all the
defaults. 

Now that git-credential-manager-core is installed, we can restart our terminal
and continue on working through this guide. Once we've finished with the Git 
for Windows install, we can make use of the credential manager in our terminal
by entering the following command in WSL:

```shell 
git config --global credential.helper "/mnt/c/Program\ Files/Git/mingw64/libexec/git-core/git-credential-manager-core.exe"
```

We now have WSL trying to use the git-credential-manager-core to facilitate our
credentials management. 

#### Mac
MacOS has a built in password/secret manager called keychain. We can tell git to
use keychain with the following line in our terminal:

```shell
git config --global credential.helper osxkeychain
```

### Personal Access Token
Once our secret manager is setup, we want to **restart our terminal/WSL Shell**.
Once restarted, we want to do two things. Generate a token from Github, and use
that as our authentication for a privileged command. 

1. To get a new token, navigate to [Personal access tokens][PAT] in Github
   settings. You can navigate there yourself by going to `settings > Developer
   settings > Personal Access Tokens`.

2. Once here, click **Generate new token**. 

3. Give your token a descriptive name. I name it for what device I will use the
   token from. This way, all of my computers have their own unique token and if
   I ever need to, I can revoke a token. We also want to use this menu to set
   when our token expires and give it the allowed permissions. For our purposes
   we want to at least have all the repo permissions. 

> Once we have our token ready to generate, we want to try running a privileged
> command in git so we get a password prompt. Once we click **Generate token**
> at the bottom of the *new token form* we will only be able to see the token
> once. 

4. Now that we have our token, we can use it when git prompts us for a password.
   If you are on Windows, you won't receive a password prompt but instead you
   will receive a pop-up that asks for you Personal Access Token. Because we
   previously configured our password/secret manager, our input will be saved
   for us. This way, we don't need to keep track of our PAT. 

[git-win]: https://git-scm.com/download/win
[PAT]: https://github.com/settings/tokens
