# Adding layer to your project

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