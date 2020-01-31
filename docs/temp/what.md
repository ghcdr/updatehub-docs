# Generate key pair for UHU package signing

This is needed to validate the generated update package. Each device will contain
the public key which will validate any received package before uncompressing it
and applying an update.

```
user@dev$ mkdir p /home/user/.updatehub/keys
user@dev$ openssl genpkey algorithm RSA out /home/user/.updatehub/keys/private_key.pem pkeyopt rsa_keygen_bits:4096
user@dev$ openssl rsa pubout in /home/user/.updatehub/keys/private_key.pem out /home/user/.updatehub/keys/public_key.pem
```

!!! warning
    Keep in mind that once an update has been generated and applied with a key
    it will not validate any packages with another key, so *keeping any
    generated keys safe **MUST** be a top priority for your organization*.

 
And then include the key pair files path generated before also to
`build/conf/local.conf`:

```
UPDATEHUB_UHUPKG_PUBLIC_KEY = "/home/user/.updatehub/keys/public_key.pem"
UPDATEHUB_UHUPKG_PRIVATE_KEY = "/home/user/.updatehub/keys/private_key.pem"
```

## 1. Generate key pair

The **updatehub** verifies the authenticity of every update package prior
applying it, this ensures that the update package has not been modified or
corrupted by any means. Each device will contain the public key which will
validate any received package before uncompressing it and applying an update.

The generation of the RSA keys requires the `openssl` utility. The
private RSA key can be generated using the command below:

```bash
openssl genpkey algorithm RSA out private_key.pem pkeyopt rsa_keygen_bits:4096
```

Next we need to extract the public RSA key from the private key. This
can be done using the following command:

```bash
openssl rsa pubout in private_key.pem out public_key.pem
```

The public key, `public_key.pem`, is be included on the device image,
so it can be used to validate every update package before making any
change on the device. The private key, `private_key.pem`, is used to
sign the update package.

{% hint style="info" %}

**Important**: Once a device is deployed using a RSA key, the same key
is used to validate every update package. It is important to keep the RSA keys safe.

{% endhint %}


commit: 
### 1. `metaupdatehub`: OpenEmbedded/Yocto Project support layer for updatehub

This layer provides the core functinality needed to integrate a Yocto build
project with **updatehub** services.

You will also need to include at least another layer related to the manufacturer
of the machine you are developing to.

[github.com/updatehub/metaupdatehub](https://github.com/updatehub/metaupdatehub)

### 5. `metaupdatehubqa`: OpenEmbedded/Yocto Project updatehub QA metadata

This layer provides the functionality used for regression and as Quality
Assurance tests for **updatehub**.

It is not intended to be used by end users, although it can be used as a
reference when doing new platform integrations.

[github.com/updatehub/metaupdatehubqa](https://github.com/updatehub/metaupdatehubqa)
diff git a/docs/Yoctointegration/imageclasses.md b/docs/Yoctointegration/imageclasses


# Quick Start

On this section we show how to create a new build that is ready for
**updatehub**. We will base the quick start build on a Yoctosupported machine,
and explain every step needed to build, push and deploy a new update. By the end
of it you should have an understanding of the entire process of creating and
applying an update of devices on **updatehub**.

Before we begin, it’s important to have a background on the terms used in this
document:

 **update**: a piece of compiled software intended to replace another while
  adding features and/or bug fixes.
 **device**: a physical computing machine running a software that can be
  updated.  machine: a type of computing machine that has specifications and
  requirements for running a piece of software. A software compiled for one
  machine cannot run, or at least won’t fully support, another machine.
 **rollout**: the act of updating the software on a set of devices of a machine
  type from one specific version to another.
 **management server**: a **updatehub** service that manages and provides
  updates for devices.
 **agent**: the program running on a device that is responsible for pooling for
  new available updates of the current version of software, and in case of
  finding one perform it.

For the sake of specificity we will use the Raspberry Pi as the machine for this
quick start. To check other machines supported by **updatehub** please check this.

## Dependencies

Including **updatehub** to your project should be fairly simple, as it doesn't
require any special dependencies on the build system. Simply include the
metaupdatehub layer and the BSP support layer to your build and it will be
ready to generate a new image with the system.

## Generate key pair for UHU package signing

This is needed to validate the generated update package. Each device will contain
the public key which will validate any received package before uncompressing it
and applying an update.

```
user@dev$ mkdir p /home/user/.updatehub/keys
user@dev$ openssl genpkey algorithm RSA out /home/user/.updatehub/keys/private_key.pem pkeyopt rsa_keygen_bits:4096
user@dev$ openssl rsa pubout in /home/user/.updatehub/keys/private_key.pem out /home/user/.updatehub/keys/public_key.pem
```

{% hint style='danger' %}
Keep in mind that once an update has been generated and applied with a key
it will not validate any packages with another key, so *keeping any
generated keys safe **MUST** be a top priority for your organization*.
{% endhint %}

## Management server access

This section will show how to access the management server and retrieve the
credentials for working with updates on your Yocto project build. Your
credentials are valid for any project you can manage, so this section steps
should be done only once, or in case the credentials are lost.

The first thing you should do is to sign up for **updatehub** early access. Go
to [updatehub.io](https://updatehub.io), fill up and send the form. As of the
time of the writing of this document the approval of new sign up requests is
gradual as we add new features, expand and test the platform to accommodate new
users.

After signup you should receive a confirmation email to verify your email
shortly. After confirmation you can access
[dashboard.updatehub.io](https://dashboard.updatehub.io) to login to the web
interface, and manage your product updates.

First, you need to generate an API access ID and key. Click on your email on the
top left of the web interface and select "Settings" on the dropdown menu. You
will be directed to the user settings page. On the "Application access" area
click on the "Request Access Key" button. Fill in the key name and choose the
API key owner as "Me", then click on Save.

![updatehub access ID creation](/img/quickstart/accessidcreation.png)

The next modal windows will show you your newly created access ID and access
key:

![updatehub access ID creation](/img/quickstart/createdaccessid.png)

{% hint style='danger' %}
    Please keep in mind that **THIS IS THE ONLY TIME THE ACCESS KEY WILL EVER BE
    AVAILABLE TO YOU!** After closing the window the access key cannot be
    retrieved again, so be sure to copy and save it on a reliable medium!
{% endhint %}

With those credentials the **updatehub** Yocto layers will have the necessary
information to access the management server API and push new updates.
