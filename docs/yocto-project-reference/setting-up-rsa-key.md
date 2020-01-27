# Setting up RSA Key

The keys need to be enabled inside your **Yocto Project** build configuration, so **UpdateHub** can deploy the public key inside the generated image and use the private key to sign the update package. You must set the *UPDATEHUB_UHUPKG_PRIVATE_KEY* and *UPDATEHUB_UHUPKG_PRIVATE_KEY* variables inside your *conf/local.conf* file as seen next:

```
UPDATEHUB_UHUPKG_PRIVATE_KEY = "~/updatehub-keys/private_key.pem"
UPDATEHUB_UHUPKG_PUBLIC_KEY = "~/updatehub-keys/public_key.pem"
```
