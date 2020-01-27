# Configurating UpdateHub variables

Before generate the new image is necessary add the *update-image* class of **UpdateHub** in your project recipe for to use the setting available. For this you must include "inherit updatehub-image" in *myproject/../my-image.bb* or just to add "updatehub-image" in *inherit* if this exists.  

You should now to include *UpdateHub* system variables in *conf/local.conf*. The variables below are the basics for the correct configuration. More details and options see [Glossary](glossary.md).

*UPDATEHUB_PRODUCT_UID* - identifies the product id in use and this is used by
rollouts. It is generate in create process ends or you get this code in **UpdateHub** Dashboard, in *Product* page.

*UPDATEHUB_ACCESS_ID* and *UPDATEHUB_ACCESS_SECRET* - They can be generate in *Settings* available in right top of screen and are necessary for server connection. 

*UPDATEHUB_PACKAGE_VERSION_SUFFIX* - optionally add, advice for version organization information.

The your new image with **UpdateHub** support layer is ready. 
