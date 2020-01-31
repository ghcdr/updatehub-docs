# Yocto Project Reference

## Supported version

The **UpdateHub** offers a high quality integration for the **Yocto Project** and provides a ready to use support for a number of boards (**RaspberryPi**, **Texas Instruments** e **Freescale**). Every six months, a new version of **Yocto Project** is released.

The current version is the **Yocto Project** 3.0, codename *Zeus*, and its support is provided by the *meta-updatehub* layer. This layer provides all the infrastructure code to enable the use of **Yocto Project** together with the **UpdateHub**. The minimal set of layers to use the **UpdateHub** are:

| Layer name                    | Branch name |
|-------------------------------|-------------|
| poky                          | zeus        |
| meta-openembedded/meta-oe     | zeus        |
| meta-openembedded/meta-python | zeus        |
| meta-updatehub                | zeus        |


Besides the basic support, there are many boards with **UpdateHub** support, provided by extra BSP integration layers, as shown at the table below:

|  Board full name                        | BSP layer name                                                                                              | Machine name   | Branch name |
|-----------------------------------------|-------------------------------------------------------------------------------------------------------------|----------------|-------------|
| BeagleBone Black                        | [meta-updatehub-ti](https://github.com/updatehub/meta-updatehub-ti/tree/zeus)                   | beaglebone     | zeus       |
| Raspberry Pi 3                          | [meta-updatehub-raspberrypi](https://github.com/updatehub/meta-updatehub-raspberrypi/tree/zeus) | raspberrypi3   | zeus       |
| NXP i.MX6QP/Q/DL SABRE Smart Device     | [meta-updatehub-freescale](https://github.com/updatehub/meta-updatehub-freescale/tree/zeus)     | imx6qdlsabresd | zeus       |
| Boundary Devices Nitrogen6X             | [meta-updatehub-freescale](https://github.com/updatehub/meta-updatehub-freescale/tree/zeus)     | nitrogen6x     | zeus       |
| Boundary Devices i.MX6 SABRELite        | [meta-updatehub-freescale](https://github.com/updatehub/meta-updatehub-freescale/tree/zeus)     | nitrogen6x     | zeus       |
| TechNexion i.MX7 PICO                   | [meta-updatehub-freescale](https://github.com/updatehub/meta-updatehub-freescale/tree/zeus)     | imx7d-pico     | zeus       |
| Toradex Apalis iMX6Q/D                  | [meta-updatehub-freescale](https://github.com/updatehub/meta-updatehub-freescale/tree/zeus)     | apalis-imx6    | zeus       |
| WaRP7                                   | [meta-updatehub-freescale](https://github.com/updatehub/meta-updatehub-freescale/tree/zeus)     | imx7s-warp     | zeus       |
| Wandboard i.MX6 QuadPlus/Quad/Dual/Solo | [meta-updatehub-freescale](https://github.com/updatehub/meta-updatehub-freescale/tree/zeus)     | wandboard      | zeus       |


If you need to use an earlier **Yocto Project** version, the **UpdateHub** is also supported. Currently, there is support for following previous **Yocto Project** versions:

* Yocto Project 2.1, codename _Krogoth_
* Yocto Project 2.2, codename _Morty_
* Yocto Project 2.3, codename _Pyro_
* Yocto Project 2.4, codename _Rocko_
* Yocto Project 2.5, codename _Sumo_
* Yocto Project 2.6, codename _Thud_
* Yocto Project 2.7, codename _Warrior_
* Yocto Project 3.0, codename _Zeus_

These earlier versions are actively supported by the **UpdateHub**, but features and compatible machines may vary among them.

## Using UpdateHub Platform

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

## Adding layer to your project

Including the **updatehub** Yocto layers to your build is easy just clone the
meta-updatehub layer and the machine support layer to your sources directory following the commands below:
```
git clone https://github.com/openembedded/meta-openembedded -b zeus
git clone https://github.com/UpdateHub/meta-updatehub -b zeus
```
In */build* folder of your project include:
```
bitbake-layers add-layer ../meta-openembedded/meta-oe
bitbake-layers add-layer ../meta-openembedded/meta-python
bitbake-layers add-layer ../meta-openembedded/meta-networking
bitbake-layers add-layer ../meta-updatehub
```

For **Raspberry Pi** 3, you can do that using:
```
git clone https://github.com/UpdateHub/meta-updatehub-raspberrypi
```
In */build* folder of your project include:
```
bitbake-layers add-layer ../meta-updatehub-raspberrypi/
```

For **BeagleBone Black**, you can use:
```
git clone https://github.com/UpdateHub/meta-updatehub-ti
```
In */build* folder of your project include:
```
bitbake-layers add-layer ../meta-updatehub-ti/
```

And for **imx6qdlsabresd**, use:
```
git clone https://github.com/UpdateHub/meta-updatehub-freescale
```
In */build* folder of your project include:
```
bitbake-layers add-layer ../meta-updatehub-freescale/
```

Done! Now you have a **UpdateHub** layer in your project.

## Configurating UpdateHub variables

Before generate the new image is necessary add the *update-image* class of **UpdateHub** in your project recipe for to use the setting available. For this you must include "inherit updatehub-image" in *myproject/../my-image.bb* or just to add "updatehub-image" in *inherit* if this exists.  

You should now to include *UpdateHub* system variables in *conf/local.conf*. The variables below are the basics for the correct configuration. More details and options see [Glossary](glossary.md).

*UPDATEHUB_PRODUCT_UID* - identifies the product id in use and this is used by
rollouts. It is generate in create process ends or you get this code in **UpdateHub** Dashboard, in *Product* page.

*UPDATEHUB_ACCESS_ID* and *UPDATEHUB_ACCESS_SECRET* - They can be generate in *Settings* available in right top of screen and are necessary for server connection. 

*UPDATEHUB_PACKAGE_VERSION_SUFFIX* - optionally add, advice for version organization information.

The your new image with **UpdateHub** support layer is ready. 

## Setting up RSA Key

The keys need to be enabled inside your **Yocto Project** build configuration, so **UpdateHub** can deploy the public key inside the generated image and use the private key to sign the update package. You must set the *UPDATEHUB_UHUPKG_PRIVATE_KEY* and *UPDATEHUB_UHUPKG_PRIVATE_KEY* variables inside your *conf/local.conf* file as seen next:

```
UPDATEHUB_UHUPKG_PRIVATE_KEY = "~/updatehub-keys/private_key.pem"
UPDATEHUB_UHUPKG_PUBLIC_KEY = "~/updatehub-keys/public_key.pem"
```

## Pushing an update package

The **UpdateHub** works with upkg format for update package, and this is generated for *uhu*. 
Update Utilities or *uhu* is an interactive prompt and a command line utility to manage update packages for UpdateHub agent and will provide you three new **BitBake** tasks:

*uhupush*: sends the update package to the **UpdateHub** Cloud. The generation of an update package is very simple. After the integration of the **UpdateHub** with your **Yocto Project** build is complete, the **Bitbake** tool can be used to generate and upload the update package. The following command does all the needed work in order to push the packages to the **UpdateHub** Cloud:

```
bitbake <image> -c uhupush
```

After running this, the **UpdateHub** Cloud will display that there is a new *Package* to update the *Devices* and you may start a *Rollout* through the interface.

For more details or uhu install access [UpdateHub Utilities](https://github.com/UpdateHub/uhu).

## Glossary

##### UPDATEHUB_PRODUCT_UID
 identifies the product id in use. This is used by rollouts.

##### UPDATEHUB_UHUPKG_PUBLIC_KEY   

##### UPDATEHUB_UHUPKG_PRIVATE_KEY   

  The variables are required to point to the keys which are used to validate and
sign the update package.  

  The keys may or not be stored on the layer. Commonly the keys are not available
for developers and passed to the build system using the **local.conf** file of
the autobuilder.

##### UPDATEHUB_IMAGE_TYPE 
The updatehub can operate using different setup
which can be chosen using the UPDATEHUB_IMAGE_TYPE variable. It supports
different values, as below:

  **initramfs** - Enables the updatehub gold firmware support; this adds an
  initramfs based image which is used for the upgrade process. In this mode,
  the updatehub agent is ran inside an initramfs image which allows for the
  image to be changed without the need of a spare storage space.

  **active/inactive** - Allow the use of active and inactive images schema.
  This reduces the downtime of the system as the image can be change without
  rebooting. The new image is installed in a spare storage area and in next
  reboot the new image is used. The UPDATEHUB_ACTIVE_INACTIVE_BACKEND variable
  need to set depending of the machine requirement.

##### UPDATEHUB_ACTIVE_INACTIVE_BACKEND 
The active and inactive image schema
  requires a backend to identify and choose the image to be used for next boot.
  It supports: 'u-boot', 'grub' or 'grub-efi'.

##### UPDATEHUB_INSTALL_MODE
There are multiple installation modes supported.
  This is usually machine dependent as it depends on the storate type in use.
  Supported values are: 'copy', 'flash', 'raw', 'tarball', 'ubifs' and 'imxkobs'.

##### UPDATEHUB_FILESYSTEM_SUPPORT 
When using the 'copy' or 'tarball'
installation mode, some filesystem support packages are required.
This variable controls which filesystems should be supported. It supports
different values, as 'btrfs', 'ext2', 'ext3', 'ext4', 'f2fs', 'jffs2', 'ubifs',
'vfat' and 'xfs'.   

  **Optional variables:**

##### UPDATEHUB_SERVER_URL

   Specifies the updatehub Server address to use. This is required in
   case you are running it inside your private clould.

##### UPDATEHUB_ACCESS_SECRET 

   When using the uhupush task we can override the Access Id and the
   corresponding Secret for use. This is usually used in auto builders
   as they may require different credentials depending on the product
   being build.

##### UPDATEHUB_CUSTOM_CA_CERTS
Specify the CA certificate bundle to be used
for uhupush task. It is currently used by updatehub staging server for tests but
may be interesting for other users when doing custom server deployments.

##### UPDATEHUB_DEVICE_ATTRIBUTE 

##### UPDATEHUB_DEVICE_IDENTITY 

##### UPDATEHUB_PACKAGE_VERSION  

##### UPDATEHUB_PACKAGE_VERSION_SUFFIX

##### UPDATEHUB_RUNTIME_PACKAGES


