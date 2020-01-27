# Using UpdateHub Platform

The first step is initialize the environment to build a **Linux** image
using **Yocto Project**. To start to work with **Yocto Project** we
need to fetch all the needed layers, that includes the **poky**,
*meta-openembedded*, *meta-raspberrypi*, *meta-updatehub* and
*meta-updatehub-raspberrypi* layers. 

The [meta-updatehub](https://github.com/UpdateHub/meta-updatehub) is the
layer that adds support to **UpdateHub** itself, and
[meta-updatehub-raspberrypi](https://github.com/UpdateHub/meta-updatehub-raspberrypi)
includes **UpdateHub** support for **Raspberry Pi** machines. We need to get
the *meta-openembedded* layer because **UpdateHub** has some
dependencies, like **Python 3** packages to build the
[uhu](https://github.com/UpdateHub/uhu) utility that is used to manage
**UpdateHub** packages and will be cover in this guide.

To get the platform you need to have [*Repo*](https://gerrit.googlesource.com/git-repo/) installed. *Repo* is a tool built on top of Git and helps manage many Git repositories.

Install the repo utility:
```
mkdir ~/bin
curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```
Download the platform source:
```
PATH=${PATH}:~/bin
mkdir updatehub-platform
cd updatehub-platform
repo init -u https://github.com/UpdateHub/updatehub-yocto-project-reference-platform.git -b zeus
repo sync
```
At the end of the commands you have every metadata you need to start work with.

Setup the environment:
```
source ./setup-environment build
```

At the end of the commands you have every metadata you need to start work with.