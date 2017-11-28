---
title: "Azure kapsayıcı kayıt defterinden Azure kapsayıcı örnekleri dağıtma | Azure belgeleri"
description: "Azure kapsayıcı kayıt defterinden Azure kapsayıcı örnekleri dağıtma"
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
ms.openlocfilehash: aa1c4ea379c10dff246e2f924a345f9fa444aa64
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-container-instances-from-the-azure-container-registry"></a><span data-ttu-id="c5827-103">Azure kapsayıcı kayıt defterinden Azure kapsayıcı örnekleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="c5827-103">Deploy to Azure Container Instances from the Azure Container Registry</span></span>

<span data-ttu-id="c5827-104">Azure kapsayıcı kayıt defteri Docker kapsayıcısı görüntüleri için bir Azure tabanlı, özel kayıt defteri ' dir.</span><span class="sxs-lookup"><span data-stu-id="c5827-104">The Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="c5827-105">Bu makalede, Azure kapsayıcı örneklerine Azure kapsayıcı kayıt defterinde depolanan kapsayıcı yansımalarını dağıtmak alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c5827-105">This article covers how to deploy container images stored in the Azure Container Registry to Azure Container Instances.</span></span>

## <a name="using-the-azure-cli"></a><span data-ttu-id="c5827-106">Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="c5827-106">Using the Azure CLI</span></span>

<span data-ttu-id="c5827-107">Azure CLI oluşturmak ve Azure kapsayıcı örnekleri kapsayıcılarında yönetmek için komutlar içerir.</span><span class="sxs-lookup"><span data-stu-id="c5827-107">The Azure CLI includes commands for creating and managing containers in Azure Container Instances.</span></span> <span data-ttu-id="c5827-108">Özel bir görüntüde belirtirseniz `create` komutu, kapsayıcı kayıt defteri ile kimlik doğrulaması için gerekli görüntü kayıt defteri parola da belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c5827-108">If you specify a private image in the `create` command, you can also specify the image registry password required to authenticate with the container registry.</span></span>

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

<span data-ttu-id="c5827-109">`create` Komutu de destekler belirtme `registry-login-server` ve `registry-username`.</span><span class="sxs-lookup"><span data-stu-id="c5827-109">The `create` command also supports specifying the `registry-login-server` and `registry-username`.</span></span> <span data-ttu-id="c5827-110">Ancak, Azure kapsayıcı kayıt için oturum açma sunucusu her zaman olduğu *registryname*. azurecr.io ve varsayılan kullanıcı adı *registryname*, bu değerler görüntü adı yoksa algılanır açıkça sağlanır.</span><span class="sxs-lookup"><span data-stu-id="c5827-110">However, the login server for the Azure Container Registry is always *registryname*.azurecr.io and the default username is *registryname*, so these values are inferred from the image name if not explicitly provided.</span></span>

## <a name="using-an-azure-resource-manager-template"></a><span data-ttu-id="c5827-111">Bir Azure Resource Manager şablonu kullanarak</span><span class="sxs-lookup"><span data-stu-id="c5827-111">Using an Azure Resource Manager template</span></span>

<span data-ttu-id="c5827-112">Ekleyerek bir Azure Resource Manager şablonu Azure kapsayıcı kaydınız özelliklerini belirtebilirsiniz `imageRegistryCredentials` kapsayıcısı Grup tanımında özelliği:</span><span class="sxs-lookup"><span data-stu-id="c5827-112">You can specify the properties of your Azure Container Registry in an Azure Resource Manager template by including the `imageRegistryCredentials` property in the container group definition:</span></span>

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

<span data-ttu-id="c5827-113">Doğrudan şablonunda kapsayıcı kayıt defteri parolanızı depolamak önlemek için onu bir gizli olarak saklamanızı öneririz [Azure anahtar kasası](../key-vault/key-vault-manage-with-cli2.md) ve şablonu kullanarak referans [Azure arasında yerel tümleştirme Resource Manager ve anahtar kasası](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="c5827-113">To avoid storing your container registry password directly in the template, we recommend that you store it as a secret in [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) and reference it in the template using the [native integration between the Azure Resource Manager and Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span>

## <a name="using-the-azure-portal"></a><span data-ttu-id="c5827-114">Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="c5827-114">Using the Azure portal</span></span>

<span data-ttu-id="c5827-115">Azure kapsayıcı kayıt defteri kapsayıcı görüntülerinde bulunduruyorsanız, Azure kapsayıcı örnekleri Azure portalını kullanarak bir kapsayıcı kolayca oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c5827-115">If you maintain container images in the Azure Container Registry, you can easily create a container in Azure Container Instances using the Azure portal.</span></span>

1. <span data-ttu-id="c5827-116">Azure portalında kapsayıcı kayıt defterine gidin.</span><span class="sxs-lookup"><span data-stu-id="c5827-116">In the Azure portal, navigate to your container registry.</span></span>

2. <span data-ttu-id="c5827-117">Depoları seçin.</span><span class="sxs-lookup"><span data-stu-id="c5827-117">Choose Repositories.</span></span>

    ![Azure portalında Azure kapsayıcı kayıt defteri menüsü][acr-menu]

3. <span data-ttu-id="c5827-119">Dağıtım yapmak istediğiniz depo seçin.</span><span class="sxs-lookup"><span data-stu-id="c5827-119">Choose the repository that you want to deploy from.</span></span>

4. <span data-ttu-id="c5827-120">Dağıtmak istediğiniz kapsayıcı görüntü etiketi sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c5827-120">Right-click the tag for the container image you want to deploy.</span></span>

    ![Kapsayıcı Azure kapsayıcı örnekleri ile başlatmak için bağlam menüsü][acr-runinstance-contextmenu]

5. <span data-ttu-id="c5827-122">Kapsayıcı için bir ad ve kaynak grubu için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="c5827-122">Enter a name for the container and a name for the resource group.</span></span> <span data-ttu-id="c5827-123">İsterseniz, varsayılan değerleri de değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c5827-123">You can also change the default values if you wish.</span></span>

    ![Azure kapsayıcı örnekleri için menü oluşturma][acr-create-deeplink]

6. <span data-ttu-id="c5827-125">Dağıtım tamamlandıktan sonra kapsayıcı grubu için IP adresini ve diğer özellikleri bulmak için bildirimler bölmesinden gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c5827-125">Once the deployment completes, you can navigate to the container group from the notifications pane to find its IP address and other properties.</span></span>

    ![Azure kapsayıcı örnekleri kapsayıcı grubu için ayrıntıları görüntüle][aci-detailsview]

## <a name="next-steps"></a><span data-ttu-id="c5827-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c5827-127">Next steps</span></span>

<span data-ttu-id="c5827-128">Kapsayıcılar oluşturmak, bunları özel kapsayıcı kayıt defterine gönderme ve Azure kapsayıcı örnekleri tarafından dağıtmak öğrenin [öğreticiyi tamamlamak](container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="c5827-128">Learn how to build containers, push them to a private container registry, and deploy them to Azure Container Instances by [completing the tutorial](container-instances-tutorial-prepare-app.md).</span></span>

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
