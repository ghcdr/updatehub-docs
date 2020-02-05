# Meet the UpdateHub Cloud

Through the dashboard you, as the **UpdateHub** [user](https://auth.updatehub.io/auth/login/), have a rich but simple interface with all the tools required to:

* Create and operate your own *Products*
* Access *Products* from *Organizations*
* Check when new *Packages* are available for updates
* Oversee a fleet of *Devices* on the field
* Deploy updates via an Over-The-Air system running the *Rollouts*

In essence the dashboard allows the oversight over the whole **UpdateHub** platform and operations, making it easy to manage any need that you might have.

## Product

The base that connects everything together through the **UpdateHub** is the *Product*. Essentially the *Product* includes one or multiple *Devices* and for each of them there is a *Package* version that may be updated using a *Rollout*.

### Create 

After you login in [UpdateHub](https://auth.updatehub.io/auth/login/) in the *Products* page click *Add Product*.

![product add](../img/dashboard/addProduct.png)

By doing that the following dialog will be displayed. 

![product modal](../img/dashboard/modalProduct.png)

You should choose a *Product* name and who will have control over it by choosing  *Owner* (*Me* or a *Organization*) of the product. 

!!! danger "About the name and owner"
	Bear in the mind that after you create a *Product* you can not renamed or deleted it, and you can not transfer it to a organization or vice versa, so have sure you are choosing the correct name and  the owner.

![](../img/dashboard/accesskey.png)

After the *Product* has been created a *Unique Identifier Number* \(*UPDATEHUB_PRODUCT_UID*\) is generated to identify it. This number, should be added to your build in order to allow the **UpdateHub** agent, which runs inside the target device, to communicate with the **UpdateHub Cloud**. It will look as:

```
UPDATEHUB_PRODUCT_UID = "05344b71c3e9f8..."
```

For convenience, you can add the *UPDATEHUB_PRODUCT_UID* to your  *build/conf/local.conf* configuration file when prototyping.

However, as this is a information that will be permanent for the whole product life cycle, it should be put inside your distribution configuration file, or image recipe.

After you press the *OK* button you will be into the *Products* screen where you can see all your *Product*, *Rollouts*, *Devices* and *Packages*.

![First Product Screen](../img/getting-started/productscreen.png)

If you make changes in your product and send this changes to your **UpdateHub** the package will be appear in the *Package List*.

### Details

Once you have logged in, the *Products* page will display the list of your own products and the other products you have access to.

![product list](../img/dashboard/productList.png)

Clicking on any product card, you will be taken to the *Product Overview* page. In this page you find useful information about the *Product*, as which *Devices* you have deployed on the field, the two last *Packages* sent for that particular *Product* and the *Rollouts* status.

![overview](../img/dashboard/overview.png)

!!! info ""
	In case you didn't copy the *Product Unique Identifier Number* in the moment that you create it on the **UpdateHub Cloud** don't worry. To get access to this information again you must click on the *Product* icon and the *Unique Identifier Number* will be shown to you.

## Device 

The *Device* represents your physical device. It has multiple characteristics which are tracked on the management platform, as such: hardware type, unique identifier, runtime attributes and more.

The *Devices* page displays the list of registered devices for the *Product*.

### Include

For include device in your account, just put the correct variables in *build/conf/local.conf* before generate an image with **Yocto Project**.
The devices automatically connect in **UpdateHub** server which verify for update package. 
Optionally we can create a *RSA* Key for add security in comunication.  

### Details

The *Device Details* page provides you access to detailed information about a specific *Device* such as:

- The *Unique Identifier* (UID)
- The device identity values (e.g. MAC* address, CPU serial number or other)
- Current installed package version
- Hardware model
- Device state (enabled or disabled)
- Device attributes

Besides the device information, the *Rollout* history of the device allow an easy access to the current and previous device's update status, such as duration, logs about errors and date of the events.

![device details](../img/dashboard/deviceDetails.png)

During a normal situation the device *Rollout* will be displayed showing the moment that started, going through all the process until the point that is finished, like in the image below:

![device finished](../img/dashboard/finished.png)

In the case of some kind of problem happens during the update process, the **UpdateHub** will provide a visual feedback of the moment it occurred. To examine the failure you need to select *See Device Log*.

![device installation](../img/dashboard/deviceLog.png)

This data about the device ensures the user has all information needed for any upcoming situation, being capable of manage his devices within the entire *Product* lifetime.

### List

The **UpdateHub** allows the selection of *Devices* to be displayed on the list through the use of filters, therefore granting the user excellent capacity for organization even when managing a great number of them at once. The user has the option to filter *Devices* by their status as active or inactive, identity values, hardware, package version and custom attributes.

![device list](../img/dashboard/deviceList.png)

### Checking out

If to check if the *Rollout* worked and the device is up to date you just need type in your device the command below.

```
cat /etc/os-release
```

And it will show the version you use in the *Rollout*.

## Package

A software version, including the filesystem image, bootloader or any other objects, is represented by a *Package*.  Is a update package that are put in server and wait the command for init the update process. Them take a specifid format and are generate after modifications for patchs or features aditions in original image.

In dashboard, the *Package* is available after you join in a specific *Product*.

### Details

In the *Package Details* page the user may have a deeper look into a particular *Package* and its information.

Beyond the information already present on the *Package List*, you will find more data about the *Objects* and their details which is used by the **UpdateHub** agent during the object's installation.

Once you entered in the *Package Details* you have the option to remove the package from the *Rollout* if necessary by clicking on the *trash can* icon. The package will be visible and accessible but won't be available anymore.

![packages details](../img/dashboard/package.png)

### List

The *Packages* page, in the same fashion of the *Devices* page, exhibit a list with information about the packages inside a specific *Product* the user selected, such as:

- *Package Unique Identifier* (UID)
- Version
- Supported hardware list
- Status
- Size
- Upload date

Each one of these items help the user find a specific package. To filter more efficiently the packages you can select and associate them by the following items during the search:

- Status of each package can be found depending on the situation for the *Rollout*
  	- *Available*: the package is ready to be downloaded
  	- *Upload in Progress*: package during the uploaded process
  	- *Removed*: packages that were removed from the packages list
  	- *Pending Progress*: packages being checked by the server
  	- *Packages with Error*: packages that failed the system checksum
- Version for the package
- Supported hardware

![packages list](../img/dashboard/packageList.png)

## Rollout 

The *Rollout* is the process of deploying a specific version of your software, a *Package*, to a set of *Devices*. It can be simple as "send version 2.0 for all devices" or complex selecting specific filters and enforcing a gradual deployment across the devices set. 

All the process happens over-the-air (OTA) and can update a great number of *Devices* effortlessly.

In *Rollout* page we may have acess to update package information as well. Look at the image below. 
![new package](../img/getting-started/rollout-new2.png)

If you like you can see details of the *Package* just clicking on the version information.

![new package](../img/getting-started/package-new.png)

### Create

There are two methods to execute the *Rollout*.

The simpler way shows all the versions of the *Devices* present on the field to be updated at once.

You just need to go to the *Overview* or *Rollouts* page and click on *Create Rollout*. A box to choose the *version* will appear. After you make this choice just click on *Save* to initiate the *Rollout* later or *Save and Start* launch it straightaway.

![create rollout advanced](../img/dashboard/createRollout.png)

Keep in mind that this method will trigger the *Rollout* for all the *Devices* accessible for the *Product* chosen, with no restrictions concerning the different hardware or other aspects of the fleet on the field. 

The other way is to select which equipment receives the *Rollout* the **UpdateHub** offers the *Advanced Mode* option. 

A *Task* will be automatically generated and you can use the filters offered by the **UpdateHub** for select the *Devices*. We indicate to use *Fault Tolerance* percentage because this is safe measure. The **UpdateHub** will abort the *Rollout* automatically if the failure rate goes over the threshould specified, providing a safe and fast update plan for your necessities.

The *Devices*  can be filter by their Version, Hardware, Device Identifier (e.g: the MAC address) and Device Attributes (e.g: kernel version, device total memory). With multiple *Tasks* you can define the policy to begin new update processes by setting the starting point when a selected percentage of it is reached and the user can set if it must begin automatically or manually. Finally *Save* the *Rollout* to start later or *Save and Start* it immediately.

![create rollout advanced](../img/dashboard/createRolloutAdvanced.png)

It is important to bear in mind that you can create as many *Tasks* as possible as long there is *Devices* available for the *Rollout* and choose names for each individual *Task* in order to organize and identify them.

### Details

The **UpdateHub** also gives all the information with the details of each specific *Rollout*, allowing a complete overview of the individual process. Among the information displayed inside the *Rollout Details* you will find:

- *Version*: the version of *Rollout* that the *Device* will receive
- *Creation Date*: the date that the *Rollout* was created
- *Tasks*: this area shows the each task that is part of the *Rollout*. Each task includes a number of information, such as:
    - *Number of Devices*: all the *Devices* available for the *Rollout*, including the number of process concluded, failed, and remaining in one or various tasks are displayed here
    - *Fault tolerance*: that's the percentage limit of failures which can occur during the *Rollout* until the **UpdateHub** aborts the running rollout process, including any pending tasks
- *Play/Pause Rollout*: whenever the user wants to play or pause the *Rollout* the option is available, unless the process is aborted or the user chooses to archive it
- *Archive the Rollout*: once the rollout is not necessary anymore it can be archived and stopped definitely

![rollout details](../img/dashboard/rolloutDetails.png)

### List

The *Rollout List* exhibit every *Rollouts* available for the *Product* chosen and a brief information about them, such as name, version, creation, status and progress.

![rollout list](../img/dashboard/rolloutList.png)

## Settings

At the *Settings* menu you will find the your information, and you will be able to manage your *Account*, the *Aplication Access*, as well as manage the *Organizations* you belongs to.

Sign in your account and go to settings screen by clicking on the drop down menu on the right of your name and select *Settings*.  

![Menu dropdown](../img/dashboard/dropdownnewusr.png)

- *Account*: includes the user name and e-mail address
- *Application Access*: contains different keys to access your data or a organization specific data
- *Organizations*: a space for all the organizations that the user participates

![settings](../img/dashboard/settings.png)

### Account

Here you can edit your data or add and remove e-mail. 

![Editing email](../img/dashboard/editaccount.png)

### Applications access

To authenticate and authorize requests for a project build with the **UpdateHub** you must have a security credential in the form of an application access key. Each access key is specific to your user and is used to upload the packages update or any other external integration which needs to access the **UpdateHub** API.

#### Creating an Access Key

In order to generate an *Access Key* you must enter the *Settings* menu and click on the *+ Request Access Key* button. Choose a name for the key and select the API Key owner as *Me* or a *Organization*.

Once the access key is created a dialog will appear to show the security credentials. 
!!! danger "Save your keys"
	On the moment that this window is closed the keys will not be showm again and if you lose them you must revoke the Access Key and generate a new one.

![](../img/dashboard/accesskey.png)

### Organization

In addition to the *Access Key* created for the user to work individually, the **UpdateHub** grants the possibility of more than one user to have access to the same *Product*.

#### Creating an Organization

Create an *Organization* is simple, as you just need to click on the *+ Create Organization* button and select a name for it. You will be automatically be set as *Owner*. After the creation of an *Organization* invitations for new members can be easily sent. The invite must contain the user's e-mail and the level of access allowed to him.

![organization](../img/dashboard/organization.png)

There are three users access levels inside the *Organization*, each one with a particular set of permissions:

- *Owner* - has all the permissions to normally create products, start rollouts and invite other members for the *Organization*
- *Release Manager* - limited to manage the rollouts
- *Developer* - has the permission to only create the packages

Each *Organization* will display a list with all of its members, showing their name, e-mail address, access level of permission, and a list with all the pending invites waiting to be answered.


