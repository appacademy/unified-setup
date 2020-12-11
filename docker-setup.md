# Docker Setup

We don't do Docker under much later in the course, but it is required to be installed.

## macOS and Windows

Just visit [docker.com](https://docker.com) and download and install the latest
version of Docker Desktop.  Docker for Windows requires WSL 2 to be already
configured and working.

## Ubuntu Linux

Installing Docker on Ubuntu Linux is a little more involved, there isn't a download
on the main docker page. Docker does however have an easy to use convience script
that will install docker for you using curl.

You can read [Install using the convenience-script](https://docs.docker.com/engine/install/ubuntu/#install-using-the-convenience-script) for more info about this.

But it involved running these commands:

```shell
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

Then in order for you to be able to run the docker commands without using `sudo`
you should run this command replacing `your-user` with your linux user name (type `whoami` to find out what this is)

```shell
sudo usermod -aG docker your-user
```
