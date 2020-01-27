# Image classes

The updatehub support layer for [Yocto](https://www.yoctoproject.org/) provides
a set of classes to easily integrate your product with **updatehub**.

## updatehubimage

updatehub image integration class.

### Required Variables

* `UPDATEHUB_PRODUCT_UID` identifies the product id in use. This is
used by the updatehub server to identify the product and track the
 possible versions for rollouts.

* `UPDATEHUB_UHUPKG_PUBLIC_KEY` path to the public key which is used to
validate and sign the update package.

* `UPDATEHUB_UHUPKG_PRIVATE_KEY` path to the private key which is used to
validate and sign the update package.


**updatehub** Agent enables you to execute callback scripts in certain circumstances.

## Before State Transition

This callback is executed **before** every state changes with following arguments:

```enter <state>```

**Path**: ```/usr/share/updatehub/statechangecallback```

{% hint style='info' %}
The output of callback script are parsed to determine transition state flow.
To cancel the current state transition, the callback must write to stdout: ```cancel```
{% endhint %}

## After State Tranistion

This callback is executed **after** every state changes with following arguments:

```after <state>```

**Path**: ```/usr/share/updatehub/statechangecallback```

{% hint style='info' %}
The output of callback script are parsed to determine transition state flow.
To cancel the current state transition, the callback must write to stdout: ```cancel```
{% endhint %}
## Error

This callback is executed whenever an error occurs.

**Path**: ```/usr/share/updatehub/errorcallback```

{% hint style='info' %}
It's output is ignored.
{% endhint %}

## Validate

This callback is executed whenever a new installation is booted.

**Path**: ```/usr/share/updatehub/validatecallback```

{% hint style='danger' %}
If this callback succeeds the installation is validated and proceeds as normal.
If it fails, the agent forces a reboot into the previous installation.
{% endhint %}

## Rollback

This callback is executed whenever an installation validation fails.
After the failure, the agent reboots into the previous installation and before
entering it's normal execution, it executes the rollback callback.

**Path**: /usr/share/updatehub/rollbackcallback

**updatehub** Agent configuration file is located at ```/etc/updatehub.conf``` on the device's root filesystem.

{% hint style='tip' %}
In most of scenarios the configuration file is generated automatically by Yocto build process,
however you can change as you need.
{% endhint %}

The file is INI format. Example:

```
[Polling]
Interval=2h
Enabled=false

[Update]
DownloadDir=/tmp/download
SupportedInstallModes=mode1,mode2

[Network]
ServerAddress=http://addr:80

[Firmware]
MetadataPath=/usr/share/metadata

[Storage]
RuntimeSettingsPath=/var/lib/updatehub.conf
```

* ```Polling```
    * ```Interval``` the time interval on which each automatic poll will be done. Default: 1h
    * ```Enabled``` enable/disable the automatic polling. Default: enabled

* ```Update```
    * ```DownloadDir``` the directory on which the update files will be downloaded. Default: /tmp
    * ```SupportedInstallModes``` the install modes supported by this target. Possible values:
        * dryrun
        * copy
        * flash
        * imxkobs
        * raw
        * tarball
        * ubifs

* ```Network```
    * ```ServerAddress``` the address used in the network requests. Default: https://api.updatehub.io

* ```Firmware```
    * ```MetadataPath``` the directory on which are located the firmware metadata scripts. Default: /usr/share/updatehub

* ```Storage```
    * ```RuntimeSettingsPath``` the file on which will be saved the runtime settings along reboots. Default: /var/lib/updatehub.conf


Each device connected to **updatehub** Server must have a unique *uuid* which is generated
by *Device Identity Scripts*.

The default setup of [**updatehub** Agent](/advanced/updatehubagent/overview.md)
provides a collection of scripts to generate a unique *uuid* for each device.
These scripts are hosted in a [repository](https://github.com/updatehub/deviceidentity).