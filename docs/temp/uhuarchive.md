# uhu Archive

*uhuarchive*: allows you to export an update package for local usage. This is used when deploying the updates using a flash drive or during development where you can use the simple local server to test the update packages. As for the situations you need to export an update package for local usage without the internet connection, there is the option to do it by flash drive or local server. To do so use the following command line:

```
$: bitbake <image> -c uhuarchive
```