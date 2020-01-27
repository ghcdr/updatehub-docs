# Integrating onto a existent project

Integrate the **UpdateHub** in your project is very simple, just include **UpdateHub** layer and choose the BSP integration layer you need with configuration used.
Below follow the commands for include **UpdateHub** together with your **Yocto Project**:

## Add layers support
```
$ git clone https://github.com/openembedded/meta-openembedded -b zeus
$ git clone https://github.com/UpdateHub/meta-updatehub -b zeus
```
```
$ bitbake-layers add-layer ../meta-openembedded/meta-oe
$ bitbake-layers add-layer ../meta-openembedded/meta-python
$ bitbake-layers add-layer ../meta-openembedded/meta-networking
$ bitbake-layers add-layer ../meta-updatehub
```

For **Raspberry Pi** 3, you can do that using:
```
$ git clone https://github.com/UpdateHub/meta-updatehub-raspberrypi
```
```
$ bitbake-layers add-layer ../meta-updatehub-raspberrypi/
```

For **BeagleBone Black**, you can use:
```
$ git clone https://github.com/UpdateHub/meta-updatehub-ti
```
```
$ bitbake-layers add-layer ../meta-updatehub-ti/
```

And for **imx6qdlsabresd**, use:
```
$ git clone https://github.com/UpdateHub/meta-updatehub-freescale
```
```
$ bitbake-layers add-layer ../meta-updatehub-freescale/
```
You should now to include *UpdateHub* system variables in *conf/local.conf*. The variables below are the basics for the correct configuration. More details and options see [References](yocto-project-references.md).

*UPDATEHUB_PRODUCT_UID* - identifies the product id in use and this is used by
rollouts. It is generate in create process ends or you get this code in **UpdateHub** Dashboard, in *Product* page.

*UPDATEHUB_ACCESS_ID* and *UPDATEHUB_ACCESS_SECRET* - They can be generate in *Settings* available in right top of screen and are necessary for server connection. 

*UPDATEHUB_PACKAGE_VERSION_SUFFIX* - optionally add, advice for version organization information.

The your new image with **UpdateHub** support layer is ready. 

When a new build with changes has successfully finished another commands must be
run to push the changes to the updatehub management server.

```
user@dev:~/project/sources$ bitbake core-image-base -c uhupush
```

After that is done the update should appear in the management server web
interface.

