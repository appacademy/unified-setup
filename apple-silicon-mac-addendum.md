# Apple Silicon Macs and Software Development

> Note this document will change often. As new software gets updated for Apple
> Silicon this document will be ever-evolving.

In November 2020, Apple released their first Macintosh computers running
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

Your Apple Silicon based Mac has a piece of software called Rosetta 2 that will translate x86 instuctions into ARM instructions, and this is mostly transparent, although the software does run with about 70% of the performance of software compiled directly for ARM.

__Luckily as of March 2021, we don't have to use Rosetta 2 for most of our development tools.__

## A Note on Universal Apps

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

If it prints `arm64` you are running natively on Apple Silicon. If it prints out
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

However, as of March 2021, several improvments have been made to how homebrew, node and python work on Apple Silicon machines, and it is possible to install them as
native ARM compiled binaries so we won't need to use Rosetta 2 much for our
development.

### Homebrew for ARM

If you run the homebrew installer on an M1 Mac. Homebrew will install the ARM version of homebrew into the `/opt/homebrew` folder instead of the usual `/usr/local` folder used on Intel macs.  So follow the normal instructions for setting
up Homebrew on macOS.

### Python 3.9 and ARM

Python 3.9 will compile under ARM, so we mostly use the regular macOS instructions
to install it, however....

Python 3.9 needs homebrew ARM versions of `openssl` and `readline` installed.

We can install these with homebrew:

```shell
brew install openssl readline
```

After this you can install the ARM version of python 3.9 (substitute the latest 3.9 version here)

```shell
pyenv install 3.9.4
```

Compiling python from source can take quite a while.

You can check what architecture your python is compiled with by running
this at the python REPL once Python is installed.

```python
>>> import platform
>>> platform.machine()
'arm64'
```

### Node.JS and ARM

Node.JS 12 and 14 have both been updated to compile correctly on Apple Silicon.

Node.JS will compile under ARM when you try to install it under nvm but
ONLY if your python is ALSO compiled as ARM. (This is because the Node.JS compile process uses python scripts to determine the architecture.)

So make sure you do the python install first.

```nvm install 12```

You can verify what architecture your node is compiled for by starting the Node.JS REPL and typing the following:

```js
> os.arch();
'arm64'
```

*Note: This will take longer to install since it must compile Node.JS.*

## Google Chrome

Google Chrome already has an Apple Silicon version of itself. You should definitely
install this version when downloading Chrome.

### __Recommendation:__ Install the Apple Chip version of Chrome

## Visual Studio Code

Visual Studio Code is available compiled as either Intel, Apple Silicon or as a Universal App.

You can install either the Apple Silicon or Universal Version and it will work well
on your Apple Silicon based Mac.

### __Recomendation:__ Install the Apple Silicon or Universal Version

### Docker

Docker is generally available for Apple Silicon. You can install it by downloading docker desktop from this location:

[Docker Desktop for M1](https://www.docker.com/products/docker-desktop)

### __Recommendation:__ Install the Docker Desktop for Mac with Apple Chip
