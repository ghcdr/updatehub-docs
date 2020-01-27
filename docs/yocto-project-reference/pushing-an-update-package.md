# Pushing an update package

The **UpdateHub** works with upkg format for update package, and this is generated for *uhu*. 
Update Utilities or *uhu* is an interactive prompt and a command line utility to manage update packages for UpdateHub agent and will provide you three new **BitBake** tasks:

*uhupush*: sends the update package to the **UpdateHub** Cloud. The generation of an update package is very simple. After the integration of the **UpdateHub** with your **Yocto Project** build is complete, the **Bitbake** tool can be used to generate and upload the update package. The following command does all the needed work in order to push the packages to the **UpdateHub** Cloud:

```
bitbake <image> -c uhupush
```

After running this, the **UpdateHub** Cloud will display that there is a new *Package* to update the *Devices* and you may start a *Rollout* through the interface.

For more details or uhu install access [UpdateHub Utilities](https://github.com/UpdateHub/uhu).