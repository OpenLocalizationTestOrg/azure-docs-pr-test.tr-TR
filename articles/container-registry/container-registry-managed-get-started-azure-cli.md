---
title: "aaaCreate özel Docker kapsayıcısı kayıt defteri - Azure CLI | Microsoft Docs"
description: "Oluşturma ve yönetme özel Docker kapsayıcısı kayıt defterleri hello Azure CLI 2.0 ile çalışmaya başlama"
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
ms.openlocfilehash: 2cadf42db0681a09c95486510f1e65c6f87c5280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-cli"></a><span data-ttu-id="a9176-103">Hello Azure CLI kullanarak bir yönetilen kapsayıcı kayıt defteri oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9176-103">Create a managed container registry using hello Azure CLI</span></span>

<span data-ttu-id="a9176-104">Azure Container Registry, özel Docker kapsayıcı görüntülerini depolamak için kullanılan bir yönetilen Docker kapsayıcı kayıt defteridir.</span><span class="sxs-lookup"><span data-stu-id="a9176-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="a9176-105">Bu kılavuzu ayrıntıları Hello Azure CLI kullanarak yönetilen Azure kapsayıcı kayıt defteri örneği oluşturma.</span><span class="sxs-lookup"><span data-stu-id="a9176-105">This guide details creating a managed Azure Container Registry instance using hello Azure CLI.</span></span>

<span data-ttu-id="a9176-106">Yönetilen Azure kapsayıcı kayıt defterleri önizleme aşamasındadır ve tüm bölgelerde kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="a9176-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a9176-107">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu hızlı başlangıç hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="a9176-107">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a9176-108">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="a9176-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a9176-109">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a9176-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="a9176-110">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9176-110">Create a resource group</span></span>

<span data-ttu-id="a9176-111">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="a9176-111">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="a9176-112">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="a9176-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="a9176-113">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *westcentralus* konumu.</span><span class="sxs-lookup"><span data-stu-id="a9176-113">hello following example creates a resource group named *myResourceGroup* in hello *westcentralus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a><span data-ttu-id="a9176-114">Kapsayıcı kayıt defteri oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9176-114">Create a container registry</span></span>

<span data-ttu-id="a9176-115">Hello kullanarak bir ACR örneği oluşturma [az acr oluşturmak](/cli/azure/acr#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="a9176-115">Create an ACR instance using hello [az acr create](/cli/azure/acr#create) command.</span></span>

> [!NOTE]
> <span data-ttu-id="a9176-116">Bir kayıt defteri oluştururken yalnızca harf ve sayı içeren genel olarak benzersiz bir üst düzey etki alanı adı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="a9176-116">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span>

 <span data-ttu-id="a9176-117">Merhaba kayıt defteri adı hello örnekte *myContainerRegistry1*, kendi benzersiz adı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a9176-117">hello registry name in hello example is *myContainerRegistry1*, substitute a unique name of your own.</span></span>

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

<span data-ttu-id="a9176-118">Merhaba kayıt oluşturulduğunda hello çıkış benzer toohello aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a9176-118">When hello registry is created, hello output is similar toohello following:</span></span>

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

## <a name="log-in-tooacr-instance"></a><span data-ttu-id="a9176-119">TooACR örneğinde oturum</span><span class="sxs-lookup"><span data-stu-id="a9176-119">Log in tooACR instance</span></span>

<span data-ttu-id="a9176-120">İletme ve kapsayıcı görüntüleri çekme önce toohello ACR örneğinde oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9176-120">Before pushing and pulling container images, you must log in toohello ACR instance.</span></span> <span data-ttu-id="a9176-121">toodo, kullanın hello [az acr oturum açma](/cli/azure/acr#login) komutu.</span><span class="sxs-lookup"><span data-stu-id="a9176-121">toodo so, use hello [az acr login](/cli/azure/acr#login) command.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

<span data-ttu-id="a9176-122">Merhaba komut tamamlandıktan sonra 'Başarılı oturum açma' iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="a9176-122">hello command returns a 'Login Succeeded' message once completed.</span></span>

## <a name="use-azure-container-registry"></a><span data-ttu-id="a9176-123">Azure Container Registry’yi kullanma</span><span class="sxs-lookup"><span data-stu-id="a9176-123">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="a9176-124">Kapsayıcı görüntülerini listeleme</span><span class="sxs-lookup"><span data-stu-id="a9176-124">List container images</span></span>

<span data-ttu-id="a9176-125">Kullanım hello `az acr` CLI komutları tooquery hello görüntüleri ve bir havuzda etiketler.</span><span class="sxs-lookup"><span data-stu-id="a9176-125">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="a9176-126">Şu anda, kapsayıcı kayıt defteri hello desteklemiyor `docker search` komutu tooquery görüntüler ve etiketler için.</span><span class="sxs-lookup"><span data-stu-id="a9176-126">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="a9176-127">Depoları listeleme</span><span class="sxs-lookup"><span data-stu-id="a9176-127">List repositories</span></span>

<span data-ttu-id="a9176-128">Merhaba aşağıdaki örnek JSON (JavaScript nesne gösterimi) biçiminde bir kayıt defterindeki hello depoları listeler:</span><span class="sxs-lookup"><span data-stu-id="a9176-128">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="a9176-129">Etiketleri listeleme</span><span class="sxs-lookup"><span data-stu-id="a9176-129">List tags</span></span>

<span data-ttu-id="a9176-130">Merhaba aşağıdaki örnek listeler hello hello etiketlerini **samples/nginx** JSON biçiminde deposu:</span><span class="sxs-lookup"><span data-stu-id="a9176-130">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="a9176-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a9176-131">Next steps</span></span>

<span data-ttu-id="a9176-132">Bu hızlı başlangıç bölümünde hello Azure CLI kullanarak yönetilen Azure kapsayıcı kayıt defteri örneği oluşturduğunuzu düşünün.</span><span class="sxs-lookup"><span data-stu-id="a9176-132">In this quick start, you've created a managed Azure Container Registry instance using hello Azure CLI.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a9176-133">Merhaba Docker CLI kullanarak ilk görüntünüzü bildirme</span><span class="sxs-lookup"><span data-stu-id="a9176-133">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
