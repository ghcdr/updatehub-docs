# Yocto Project Guides

## Create project from scratch

To initialize a project with the **UpdateHub** layer support follow the steps bellow:

* Check if your [board is supported](../yocto-project-reference/#supported-version)
* [Add  layer](../yocto-project-reference/#using-updatehub-platform) of **UpdateHub**
* Create a **UpdateHub Cloud** [account](https://auth.updatehub.io/auth/login/) and a [*Product*](../updatehub-cloud/#product.md) 
* Setting up the **UpdateHub** [variables](../yocto-project-reference/#configurating-updatehub-variables)
* Generate a imagem and record this in your board
* [Generate and send](../yocto-project-reference/#pushing-an-update-package) a update package

## Integrating onto a existing project

For to add **UpdateHub Cloud** in your project follow the steps bellow:

* Check if your [board is supported](../yocto-project-reference/#supported-version)
* [Add  layer](../yocto-project-reference/#adding-layer-to-your-project) of **UpdateHub**
* Create a **UpdateHub Cloud** [account](https://auth.updatehub.io/auth/login/)
 and a [*Product*](../updatehub-cloud/#product) 
* Setting up the **UpdateHub** [variables](../yocto-project-reference/#configurating-updatehub-variables). 
* Before generate the new image is necessary add the *update-image* class of **UpdateHub** in your project recipe for to use the setting available. For this you must include "inherit updatehub-image" in *myproject/../my-image.bb* or just to add "updatehub-image" in *inherit* if this exists.  
* Generate a imagem and record this in your board
* [Generate and send](../yocto-project-reference/#pushing-an-update-package) a update package