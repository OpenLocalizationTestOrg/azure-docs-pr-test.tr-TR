---
title: "Özel Docker kapsayıcısı kayıt defteri oluşturma - Azure CLI| Microsoft Docs"
description: "Azure CLI 2.0 ile Docker kapsayıcısı kayıt defterleri oluşturmaya ve yönetmeye başlayın"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: c7cdb1b13bf32388d18c2a25af28337a81861c1e
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-managed-container-registry-using-the-azure-cli"></a><span data-ttu-id="e1ee8-103">Azure CLI’yı kullanarak yönetilen bir kapsayıcı kayıt defteri oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1ee8-103">Create a managed container registry using the Azure CLI</span></span>

<span data-ttu-id="e1ee8-104">Azure Container Registry, özel Docker kapsayıcı görüntülerini depolamak için kullanılan bir yönetilen Docker kapsayıcı kayıt defteridir.</span><span class="sxs-lookup"><span data-stu-id="e1ee8-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="e1ee8-105">Bu kılavuzda, Azure CLI kullanarak yönetilen bir Azure Container Registry örneği oluşturma hakkındaki ayrıntılar yer alır.</span><span class="sxs-lookup"><span data-stu-id="e1ee8-105">This guide details creating a managed Azure Container Registry instance using the Azure CLI.</span></span>

<span data-ttu-id="e1ee8-106">Yönetilen Azure kapsayıcı kayıt defterleri önizleme aşamasındadır ve tüm bölgelerde kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="e1ee8-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e1ee8-107">CLI'yi yerel olarak yükleyip kullanmayı seçerseniz bu hızlı başlangıç için Azure CLI 2.0.4 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1ee8-107">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e1ee8-108">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e1ee8-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="e1ee8-109">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e1ee8-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="e1ee8-110">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1ee8-110">Create a resource group</span></span>

<span data-ttu-id="e1ee8-111">[az group create](/cli/azure/group#create) komutuyla bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e1ee8-111">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="e1ee8-112">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="e1ee8-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="e1ee8-113">Aşağıdaki örnek *westcentralus* konumunda *myResourceGroup* adlı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e1ee8-113">The following example creates a resource group named *myResourceGroup* in the *westcentralus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a><span data-ttu-id="e1ee8-114">Kapsayıcı kayıt defteri oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1ee8-114">Create a container registry</span></span>

<span data-ttu-id="e1ee8-115">[az act create](/cli/azure/acr#create) komutunu kullanarak bir ACR örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e1ee8-115">Create an ACR instance using the [az acr create](/cli/azure/acr#create) command.</span></span>

> [!NOTE]
> <span data-ttu-id="e1ee8-116">Bir kayıt defteri oluştururken yalnızca harf ve sayı içeren genel olarak benzersiz bir üst düzey etki alanı adı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="e1ee8-116">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span>

 <span data-ttu-id="e1ee8-117">Örnekteki kayıt defterinin adını (*myContainerRegistry1*), kendi bulduğunuz benzersiz bir adla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e1ee8-117">The registry name in the example is *myContainerRegistry1*, substitute a unique name of your own.</span></span>

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

<span data-ttu-id="e1ee8-118">Kayıt defteri oluşturulduğunda çıkış aşağıdakilere benzer:</span><span class="sxs-lookup"><span data-stu-id="e1ee8-118">When the registry is created, the output is similar to the following:</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-29T04:50:28.607134+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry1",
  "location": "westcentralus",
  "loginServer": "mycontainerregistry1.azurecr.io",
  "name": "myContainerRegistry1",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Managed_Standard",
    "tier": "Managed"
  },
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

## <a name="log-in-to-acr-instance"></a><span data-ttu-id="e1ee8-119">ACR örneğinde oturum açma</span><span class="sxs-lookup"><span data-stu-id="e1ee8-119">Log in to ACR instance</span></span>

<span data-ttu-id="e1ee8-120">Kapsayıcı görüntülerini gönderip çekmeden önce ACR örneğinde oturum açmalısınız.</span><span class="sxs-lookup"><span data-stu-id="e1ee8-120">Before pushing and pulling container images, you must log in to the ACR instance.</span></span> <span data-ttu-id="e1ee8-121">Bunu yapmak için [az acr login](/cli/azure/acr#login) komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="e1ee8-121">To do so, use the [az acr login](/cli/azure/acr#login) command.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

<span data-ttu-id="e1ee8-122">Komut tamamlandığında bir “Oturum Açma Başarılı” iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="e1ee8-122">The command returns a 'Login Succeeded' message once completed.</span></span>

## <a name="use-azure-container-registry"></a><span data-ttu-id="e1ee8-123">Azure Container Registry’yi kullanma</span><span class="sxs-lookup"><span data-stu-id="e1ee8-123">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="e1ee8-124">Kapsayıcı görüntülerini listeleme</span><span class="sxs-lookup"><span data-stu-id="e1ee8-124">List container images</span></span>

<span data-ttu-id="e1ee8-125">Bir depodaki görüntüleri ve etiketleri sorgulamak için `az acr` CLI komutlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="e1ee8-125">Use the `az acr` CLI commands to query the images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="e1ee8-126">Container Kayıt Defteri şu anda görüntü ve etiket sorgulamak için `docker search` komutunu desteklememektedir.</span><span class="sxs-lookup"><span data-stu-id="e1ee8-126">Currently, Container Registry does not support the `docker search` command to query for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="e1ee8-127">Depoları listeleme</span><span class="sxs-lookup"><span data-stu-id="e1ee8-127">List repositories</span></span>

<span data-ttu-id="e1ee8-128">Aşağıdaki örnekte, bir kayıt defterindeki depolar JSON (JavaScript Nesne Gösterimi) biçiminde listelenmiştir:</span><span class="sxs-lookup"><span data-stu-id="e1ee8-128">The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="e1ee8-129">Etiketleri listeleme</span><span class="sxs-lookup"><span data-stu-id="e1ee8-129">List tags</span></span>

<span data-ttu-id="e1ee8-130">Aşağıdaki örnekte, **samples/nginx** deposundaki etiketler JSON biçiminde listelenmiştir:</span><span class="sxs-lookup"><span data-stu-id="e1ee8-130">The following example lists the tags on the **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="e1ee8-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e1ee8-131">Next steps</span></span>

<span data-ttu-id="e1ee8-132">Bu hızlı başlangıçta, Azure CLI kullanarak bir yönetilen Azure Container Registry örneği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="e1ee8-132">In this quick start, you've created a managed Azure Container Registry instance using the Azure CLI.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e1ee8-133">Docker CLI’yı kullanarak ilk görüntünüzü itme</span><span class="sxs-lookup"><span data-stu-id="e1ee8-133">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
