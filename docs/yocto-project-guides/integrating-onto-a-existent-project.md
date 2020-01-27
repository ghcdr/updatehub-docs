# Integrating onto a existing project

For to add **UpdateHub Cloud** in your project follow the steps bellow:

* Check if your [board is supported](../yocto-project-reference/supported-version.md)
* [Add  layer](../yocto-project-reference/adding-layer-to-your-project.md) of **UpdateHub**
* Create a **UpdateHub Cloud** [account](https://auth.updatehub.io/auth/login/)
 and a [*Product*](../updatehub-cloud/product.md) 
* Setting up the **UpdateHub** [variables](../yocto-project-reference/configurating-updatehub-variables.md). 
* Before generate the new image is necessary add the *update-image* class of **UpdateHub** in your project recipe for to use the setting available. For this you must include "inherit updatehub-image" in *myproject/../my-image.bb* or just to add "updatehub-image" in *inherit* if this exists.  
* Generate a imagem and record this in your board
* [Generate and send](../yocto-project-reference/pushing-an-update-package.md) a update package