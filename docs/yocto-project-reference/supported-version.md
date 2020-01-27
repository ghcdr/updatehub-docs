# Supported version

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
