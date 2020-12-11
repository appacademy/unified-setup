# Apple Silicon Macs and Software Development

In November 2020, Apple releases their first Macintosh computers running
custom Apple designed CPUs instead of using the Intel CPUs they had used
in the prior decade. These CPUs run an architecture called ARM (Acorn Risc Machine)

## What is an architecture?

At the lowest level, the CPU (Central Processing Unit) of a computer uses something
called an _instruction set_ to actually do the work of running programs.

In this course we learn JavaScript and Python which are both _high-level languages_.

So we don't have to worry about the instruction set of our CPUs do we?

Not directly, but since we've had more than a decade of Apple computers using
the Intel x86 instruction set (sometimes abbreviated x86, x64, x86_64 or i386)
much of the software we use hasn't been _compiled_ for the new Apple Silicon
architecture called ARM (Acorn Risc Machines, sometimes abbreviated as arm64).

You are in luck though! Your Apple Silicon based Mac has a piece of software
called Rosetta 2 that will translate x86 instuctions into ARM instructions, and
this is mostly transparent, although the software does run with about 70% of the
performance of software compiled directly for ARM. So when possible we should
try to use ARM native software as it will run faster, but right now, we will
be force to use Rosetta 2 for most of our tools.

> Note this document will change often. As new software gets updated for Apple
> Silicon this document will be ever-evolving.

## Universal Apps

Some apps are 'universal' on macOS. This means they've been compiled for BOTH
Intel and ARM architectures, and the file for the app contains BOTH sets of
instructions. An example of this is the zsh shell. You can use the `file` command
in macOS to determine if an apple is intel, arm or universal.

```shell
file /bin/zsh
/bin/zsh: Mach-O universal binary with 2 architectures: [x86_64:Mach-O 64-bit executable x86_64] [arm64e:Mach-O 64-bit executable arm64e]
/bin/zsh (for architecture x86_64):     Mach-O 64-bit executable x86_64
/bin/zsh (for architecture arm64e):     Mach-O 64-bit executable arm64e
```

You can see zsh is universal since it lists both x86_64 and arm64e architectures.

## What this means for developers

Whenever we compile software from the command prompt, that software must be turned
into _machine code_ for whatever processor our computer has.  Since macOS can
run both x86 programs and ARM programs, we need a way to tell our computer
we would like to run things in Rosetta or not from the command line.

macOS ships with a command to do just that, the `arch` command.

You can run it at anytime and it will print out the current architecture of
your shell.

```shell
> arch
arm64
```

If it prints `arm64` you are runnig natively on Apple Silicon. If it prints out
`i386` you are running under Rosetta 2.

You can also preface any command with `arch` to force it to run under any particular
architecture. For instance if we would like to run our shell `zsh` under Rosetta
2 we can do this:

```shell
arch -x86_64 zsh
```

This starts a brand new shell that is running in Rosetta 2. If you use the `arch` 
command by itself now, you'll see it prints out `i386`.

This is handy for when we want to run something in Rosetta 2.

## The workaround

For now, as of December 2020, the recommended workaround for dealing with the
confusion of runing things as arm or intel is to just setup a Terminal
to run in Rosetta most of the time. This is guaranteed to work for all the
software we use in this course, including Node.JS and Python.

In order to do this, open up your Applications folder on your Mac, then find
the Utility folder and open that up.

In this folder you will see the Terminal app. Right click on it and choose
"Duplicate". This will ask for your password.  When this is finished you will have
two terminal apps.  Find the new one and rename it to something like `Rosetta Terminal`.

Now right click on it and choose _Get Info_.  In the get info window check the box named
"Open using Rosetta" and close the window.

Now you can put this Terminal on your Dock.  If you open this terminal and type
`arch` you'll see it will print `i386`.

### __Recommendation:__ Use this Rosetta Terminal now instead of the regular Terminal app.

## The Future

In the future we fully expect all software to be compiled for Apple Silicon.
If history is any indication, eventually Rosetta 2 will be removed from some
future version of macOS in the next few years.

Once this happens, your Rosetta 2 terminal and all the intel software you've
installed will probably need to be uninstalled and replaced with ARM versions.

The good thing about this is your software will get 30% faster!

## Google Chrome

Google Chrome already has an Apple Silicon version of itself. You should definitely
install this version when downloading Chrome.

### __Recommendation:__ Install the Apple Chip version of Chrome.

## Visual Studio Code

As of now, in December 2020, the Stable and Insider versions of VSCode are not
compiled for ARM.  However there is an Exploration version on the VSCode site
that is compiled for ARM and the peformance of it is significantly better than
the Intel version under Rosetta 2.  Feel free to try this version out, but be
aware that the arch command will return `arm64` when running that version.

This means that the integrated terminal in VSCode will be like running the regular
terminal and not the Rosetta Terminal.  In the stable version the `arch` command
in the interated terminal returns `i386`.

Things are changing fast though, and I expect VSCode to be updated for Apple
Silicon in a few months.

### __Recommendation:__ Install the stable version of VSCode which uses Rosetta.

## Homebrew

Homebrew works under Apple Silicon but there are some things to know about it.

Currently the Homebrew maintainers are recommending you only run homebrew under
Rosetta. This means either prefacing all `brew` commands with `arch -x86_64` 
or only running them inside your Rosetta Terminal application.

There is an ARM version of homebrew in the works, however it installs into a
different path on your system.

Homebrew install installs into `/usr/local` while homebrew for ARM installs in 
`/opt/homebrew`.

### __Recommendation:__ Use the Rosetta Terminal you created for all homebrew installs.

## Node.JS

Node.JS installs fine using `nvm` in a Rosetta Terminal.  Node 12 and 14 do
not currently compile in an ARM terminal. Node 15 (experimental) does compile 
and work on ARM.

### __Recommendation:__ Install nvm and node 12 in a Rosetta Terminal

## Python

Python does not currently compile on Apple Silicon. This means you need to 
compile it under Rosetta.

### __Recommendation:__ Install pyenv and python in a Rosetta Terminal

### Docker

Docker currently does not work _AT ALL_ on Apple Silicon. We do not use Docker until later
in the course, so hopefully this will be resolved by the time cohorts get to the
Docker curriculum. We will keep owners of Apple Silicon Macs informed as the situation changes.

### __Recommendation:__ Do not install Docker for now

## Video

Watch this video walkthrough explaining Apple Silicon

[Apple Silicon Setup](https://vimeo.com/489701378/9cbbbde806)
