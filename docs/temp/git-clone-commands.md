# Preparing the **Yocto Project** environment

The first step is initialize the environment to build a **Linux** image
using **Yocto Project**. To start to work with **Yocto Project** we
need to fetch all the needed layers, that includes the **poky**,
*meta-openembedded*, *meta-raspberrypi*, *meta-updatehub* and
*meta-updatehub-raspberrypi* layers. The
[meta-updatehub](https://github.com/UpdateHub/meta-updatehub) is the
layer that adds support to **UpdateHub** itself, and
[meta-updatehub-raspberrypi](https://github.com/UpdateHub/meta-updatehub-raspberrypi)
includes **UpdateHub** support for **Raspberry Pi** machines. We need to get
the *meta-openembedded* layer because **UpdateHub** has some
dependencies, like **Python 3** packages to build the
[uhu](https://github.com/UpdateHub/uhu) utility that is used to manage
**UpdateHub** packages and will be cover in this guide.

Go to the directory that you want to work and run the sequence bellow
to fetch all layers:

```shell
$ git clone https://git.yoctoproject.org/git/poky -b zeus
$ git clone https://github.com/openembedded/meta-openembedded -b zeus
$ git clone https://github.com/agherzan/meta-raspberrypi -b zeus
$ git clone https://github.com/UpdateHub/meta-updatehub -b zeus
$ git clone https://github.com/UpdateHub/meta-updatehub-raspberrypi -b zeus
```

Start the **poky** build environment:

```shell
$ source poky/oe-init-build-env build
```

Add the layers to *conf/bblayers.conf*:

```shell
$ bitbake-layers add-layer ../meta-openembedded/meta-oe
$ bitbake-layers add-layer ../meta-openembedded/meta-python
$ bitbake-layers add-layer ../meta-openembedded/meta-networking
$ bitbake-layers add-layer ../meta-raspberrypi/
$ bitbake-layers add-layer ../meta-updatehub
$ bitbake-layers add-layer ../meta-updatehub-raspberrypi/
```
