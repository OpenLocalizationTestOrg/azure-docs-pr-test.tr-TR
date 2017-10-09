---
title: "hello Azure kapsayıcı kayıt defteri gelen aaaDeploy tooAzure kapsayıcı örnekleri | Azure belgeleri"
description: "Hello Azure kapsayıcı kayıt defteri tooAzure kapsayıcı örneklerinden dağıtma"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2667f91db8ed92a9ccc9ba722a2b1f5c5ea93886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-container-instances-from-hello-azure-container-registry"></a><span data-ttu-id="99e63-103">Hello Azure kapsayıcı kayıt defteri tooAzure kapsayıcı örneklerinden dağıtma</span><span class="sxs-lookup"><span data-stu-id="99e63-103">Deploy tooAzure Container Instances from hello Azure Container Registry</span></span>

<span data-ttu-id="99e63-104">Hello Azure kapsayıcı kayıt defteri Docker kapsayıcısı görüntüleri için bir Azure tabanlı, özel kayıt defteri ' dir.</span><span class="sxs-lookup"><span data-stu-id="99e63-104">hello Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="99e63-105">Bu makalede nasıl toodeploy kapsayıcı görüntüleri hello Azure kapsayıcı kayıt defteri tooAzure kapsayıcı örnekleri depolanan yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="99e63-105">This article covers how toodeploy container images stored in hello Azure Container Registry tooAzure Container Instances.</span></span>

## <a name="using-hello-azure-cli"></a><span data-ttu-id="99e63-106">Hello Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="99e63-106">Using hello Azure CLI</span></span>

<span data-ttu-id="99e63-107">Hello Azure CLI oluşturmak ve Azure kapsayıcı örnekleri kapsayıcılarında yönetmek için komutlar içerir.</span><span class="sxs-lookup"><span data-stu-id="99e63-107">hello Azure CLI includes commands for creating and managing containers in Azure Container Instances.</span></span> <span data-ttu-id="99e63-108">Özel bir görüntü hello belirtirseniz, `create` komut ayrıca belirtebilirsiniz hello görüntü kayıt defteri parola gerekli tooauthenticate hello kapsayıcı kayıt defteri ile.</span><span class="sxs-lookup"><span data-stu-id="99e63-108">If you specify a private image in hello `create` command, you can also specify hello image registry password required tooauthenticate with hello container registry.</span></span>

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

<span data-ttu-id="99e63-109">Merhaba `create` de destekler hello belirterek komutu `registry-login-server` ve `registry-username`.</span><span class="sxs-lookup"><span data-stu-id="99e63-109">hello `create` command also supports specifying hello `registry-login-server` and `registry-username`.</span></span> <span data-ttu-id="99e63-110">Ancak, hello oturum açma hello Azure kapsayıcı kayıt defteri için her zaman sunucusudur *registryname*. azurecr.io ve hello varsayılan kullanıcı adı *registryname*, bu değerler, hello resim adından algılanır açıkça sağlanmadı.</span><span class="sxs-lookup"><span data-stu-id="99e63-110">However, hello login server for hello Azure Container Registry is always *registryname*.azurecr.io and hello default username is *registryname*, so these values are inferred from hello image name if not explicitly provided.</span></span>

## <a name="using-an-azure-resource-manager-template"></a><span data-ttu-id="99e63-111">Bir Azure Resource Manager şablonu kullanarak</span><span class="sxs-lookup"><span data-stu-id="99e63-111">Using an Azure Resource Manager template</span></span>

<span data-ttu-id="99e63-112">Merhaba ekleyerek bir Azure Resource Manager şablonu Azure kapsayıcı kaydınız hello özelliklerini belirtebilirsiniz `imageRegistryCredentials` hello kapsayıcısı Grup tanımında özelliği:</span><span class="sxs-lookup"><span data-stu-id="99e63-112">You can specify hello properties of your Azure Container Registry in an Azure Resource Manager template by including hello `imageRegistryCredentials` property in hello container group definition:</span></span>

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

<span data-ttu-id="99e63-113">kapsayıcı kayıt defteri parolanızı doğrudan hello şablonunda depolama tooavoid bunu bir gizli olarak saklamanızı öneririz [Azure anahtar kasası](../key-vault/key-vault-manage-with-cli2.md) ve hello kullanılarak hello şablonunda başvuru [arasında yerel tümleştirme Azure Resource Manager ve anahtar kasası hello](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="99e63-113">tooavoid storing your container registry password directly in hello template, we recommend that you store it as a secret in [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) and reference it in hello template using hello [native integration between hello Azure Resource Manager and Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="99e63-114">Hello Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="99e63-114">Using hello Azure portal</span></span>

<span data-ttu-id="99e63-115">Hello Azure kapsayıcı kayıt defteri kapsayıcı görüntülerinde bulunduruyorsanız, Azure kapsayıcı örnekleri hello Azure portal kullanarak bir kapsayıcı kolayca oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99e63-115">If you maintain container images in hello Azure Container Registry, you can easily create a container in Azure Container Instances using hello Azure portal.</span></span>

1. <span data-ttu-id="99e63-116">Hello Azure portal, tooyour kapsayıcı kayıt defteri gidin.</span><span class="sxs-lookup"><span data-stu-id="99e63-116">In hello Azure portal, navigate tooyour container registry.</span></span>

2. <span data-ttu-id="99e63-117">Depoları seçin.</span><span class="sxs-lookup"><span data-stu-id="99e63-117">Choose Repositories.</span></span>

    ![Hello Azure kapsayıcı kayıt defteri menüsünde hello Azure portalı][acr-menu]

3. <span data-ttu-id="99e63-119">Gelen toodeploy istediğiniz hello depo seçin.</span><span class="sxs-lookup"><span data-stu-id="99e63-119">Choose hello repository that you want toodeploy from.</span></span>

4. <span data-ttu-id="99e63-120">Merhaba etiketi sağ hello kapsayıcı görüntü için toodeploy istiyor.</span><span class="sxs-lookup"><span data-stu-id="99e63-120">Right-click hello tag for hello container image you want toodeploy.</span></span>

    ![Kapsayıcı Azure kapsayıcı örnekleri ile başlatmak için bağlam menüsü][acr-runinstance-contextmenu]

5. <span data-ttu-id="99e63-122">Merhaba kapsayıcı için bir ad ve hello kaynak grubu için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="99e63-122">Enter a name for hello container and a name for hello resource group.</span></span> <span data-ttu-id="99e63-123">İsterseniz, ayrıca hello varsayılan değerleri değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99e63-123">You can also change hello default values if you wish.</span></span>

    ![Azure kapsayıcı örnekleri için menü oluşturma][acr-create-deeplink]

6. <span data-ttu-id="99e63-125">Merhaba dağıtım işlemi tamamlandıktan sonra IP adresini ve diğer özellikleri toohello kapsayıcı hello bildirimleri bölmesinde toofind grubundan gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99e63-125">Once hello deployment completes, you can navigate toohello container group from hello notifications pane toofind its IP address and other properties.</span></span>

    ![Azure kapsayıcı örnekleri kapsayıcı grubu için ayrıntıları görüntüle][aci-detailsview]

## <a name="next-steps"></a><span data-ttu-id="99e63-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="99e63-127">Next steps</span></span>

<span data-ttu-id="99e63-128">Nasıl toobuild kapsayıcıları, bunları tooa özel kapsayıcı kayıt defteri gönderme ve tooAzure kapsayıcı örnekleri tarafından dağıtmadan öğrenin [hello öğreticiyi tamamlamak](container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="99e63-128">Learn how toobuild containers, push them tooa private container registry, and deploy them tooAzure Container Instances by [completing hello tutorial](container-instances-tutorial-prepare-app.md).</span></span>

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
