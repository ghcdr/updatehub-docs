# What is UpdateHub?

**UpdateHub** is an enterprise-grade solution which makes simple to remotely update all your Linux-based devices in the field. It handles all aspects related to sending Firmware Over-the-Air \(FOTA\) updates with maximum security and efficiency, while you focus in adding value to your product.

![updatehub workflow](../img/workflow.png)

## Features

The **UpdateHub** has a rich features set. On the management platform side, it offers support for:

* Single and team managed products
* 2-click rollout creation for fast deployment across all your devices
* Multi-step rollout support for finner control about the rollout process across your devices \(e.g: lab, alpha testers, production\)
* HTTP API to control the system externally

The support provided by the **UpdateHub** for the device includes:

* Support for multiple Yocto Project versions
* Bootloader upgrade support \(U-Boot and GRUB\)
* Flash support \(NAND, NOR\)
* UBIFS support
* Automated rollback in case of update fail
* Conditional installation \(content, version and custom pattern support\)
* Callback support for every update step
* HTTP API to control and inquiry the local agent

## Supported Platforms

### Yocto Linux

The **Yocto Project** (YP) is an open source collaboration project that helps
developers create custom **Linux**-based systems regardless of the hardware
architecture.

### Zephyr

The **Zephyr™ Project** is a scalable real-time operating system (RTOS) supporting
multiple hardware architectures, optimized for resource constrained devices, and
built with safety and security in mind.

## Basic Concepts

There are few basic concepts that are important to understand the **UpdateHub**. Those basic concepts are detailed below:

##### Device

The *Device* represents your physical device. It has multiple characteristics which are tracked on the management platform, as such: hardware type, unique identifier, runtime attributes and more.

##### Package

A software version, including the filesystem image, bootloader or any other objects, is represented by a *Package*.

##### Rollout

The *Rollout* is essentially a deployment plan. It can be simple as "send version 2.0 for all devices" or complex selecting specific filters and enforcing a gradual deployment across the devices set.

##### Product

The basis that connects all together through the **UpdateHub** is the *Product*. Essentially the *Product* includes one or multiple *Devices* and for each of them there is a *Package* version that may be updated using a *Rollout*.

## UpdateHub Server Editions

**UpdateHub** Server is available in two editions:

* [UpdateHub Community Edition](https://github.com/UpdateHub/updatehub-ce)
* [UpdateHub Cloud](https://updatehub.io)

**UpdateHub Community Edition** is ideal for individual developers and small teams looking to get started with **UpdateHub** and experimenting with Firmware Over-the-Air (FOTA) updates.

**UpdateHub Cloud** is designed for enterprise development and IT teams who needs a end-to-end solution to build and ship Firmware Over-the-Air (FOTA) updates with maximum security and efficiency at any scale.

### UpdateHub Cloud

**UpdateHub Cloud**  have a rich but simple interface with all the tools required to:

- Create and operate your own *Products*
- Access *Products* from organizations
- Check when new *Packages* are available for updates
- Oversee a fleet of *Devices* on the field
- Deploy updates via an Over-The-Air system running the *Rollouts*

In essence the **UpdateHub Cloud**  allows the oversight over the whole **UpdateHub** plataform and operations, making it easy to manage any need that you might have.

### Comparasion Table

See the comparison table below to help you to choose which version fits you need:

| Feature                                      | UpdateHubCE | UpdateHubCloud  |
|:---                                          |    :---:    |      :---:      |
| Secure communication (HTTPS, CoAP over DTLS) | ✘           | ✔              |
| Signed packages                              | ✔           | ✔              |
| Rollouts                                     | ✔           | ✔              |
| Large scale rollouts                         | ✘           | ✔              |
| Multiple organizations                       | ✘           | ✔              |
| Fully monitored updates                      | ✔           | ✔              |
| Teams                                        | ✘           | ✔              |
| HTTP API                                     | ✘           | ✔              |
| Package upload                               | ✔           | ✔              |
| Multiple products                            | ✘           | ✔              |
| Advanced device filter                       | ✘           | ✔              |
| Multiple users                               | ✘           | ✔              |

## Syntax doc

This doc will use some rules for a better undertanding. Below we describe the syntax adopted.

### Emphasis

**bold** - in technologies and enterprises name.

*italic* - in **UpdateHub** variables and artefacts, dashboard options, system path and configurations, layers and file names.

### Box

!!! info "Information"
	Info box brings additional information about what was recently covered.


!!! warning "Important" 
	Here are informations that can directly influence the user and his interactions with our produts, for instance, needed do account upgrade for have support for more devices. 

!!! danger "Attention"
	These box type we found alerts about system configurations and behaviors, like to verify the SD card before record the image, for example. 