---
title: "aaaCreate ilk Azure kapsayıcı örnekleri kapsayıcı | Azure belgeleri"
description: "Azure Container Instances’ı dağıtma ve kullanmaya başlama"
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b57c52714933bd3b28c44d33f9af7cd1f23fb951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a><span data-ttu-id="4668e-103">Azure Container Instances’da ilk kapsayıcınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4668e-103">Create your first container in Azure Container Instances</span></span>

<span data-ttu-id="4668e-104">Azure kapsayıcı örnekleri kolay toocreate kolaylaştırır ve Azure kapsayıcı yönetin.</span><span class="sxs-lookup"><span data-stu-id="4668e-104">Azure Container Instances makes it easy toocreate and manage containers in Azure.</span></span> <span data-ttu-id="4668e-105">Bu Hızlı Başlangıç, Azure içinde bir kapsayıcı oluşturacak ve toohello kullanıma Internet ortak IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="4668e-105">In this quick start, you will create a container in Azure and expose it toohello internet with a public IP address.</span></span> <span data-ttu-id="4668e-106">Bu işlem tek bir komutla tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="4668e-106">This operation is completed in a single command.</span></span> <span data-ttu-id="4668e-107">Yalnızca birkaç saniye içinde tarayıcınızda şunu görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="4668e-107">Within just a few seconds, you will see this in your browser:</span></span>

![Azure Container Instances kullanılarak dağıtılmış uygulama tarayıcıda görüntüleniyor][aci-app-browser]

<span data-ttu-id="4668e-109">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4668e-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4668e-110">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu hızlı başlangıç hello Azure CLI Sürüm 2.0.12 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="4668e-110">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.12 or later.</span></span> <span data-ttu-id="4668e-111">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="4668e-111">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4668e-112">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4668e-112">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="4668e-113">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="4668e-113">Create a resource group</span></span>

<span data-ttu-id="4668e-114">Azure Container Instances örnekleri Azure kaynaklarıdır ve Azure kaynaklarının dağıtıldığı ve yönetildiği mantıksal bir koleksiyon olan Azure kaynak gruplarına yerleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="4668e-114">Azure Container Instances are Azure resources and must be placed in an Azure resource group, a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="4668e-115">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="4668e-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="4668e-116">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu.</span><span class="sxs-lookup"><span data-stu-id="4668e-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a><span data-ttu-id="4668e-117">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4668e-117">Create a container</span></span>

<span data-ttu-id="4668e-118">Bir ad, Docker görüntüsü ve bir Azure kaynak grubu sağlayarak kapsayıcı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4668e-118">You can create a container by providing a name, a Docker image, and an Azure resource group.</span></span> <span data-ttu-id="4668e-119">İsteğe bağlı olarak hello kapsayıcı toohello getirebilir Internet ortak IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="4668e-119">You can optionally expose hello container toohello internet with a public IP address.</span></span> <span data-ttu-id="4668e-120">Bu durumda, [Node.js](http://nodejs.org) ile yazılan, çok basit bir web uygulamasını barındıran bir kapsayıcı kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="4668e-120">In this case, we'll use a container that hosts a very simple web app written in [Node.js](http://nodejs.org).</span></span>

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

<span data-ttu-id="4668e-121">Birkaç saniye içinde bir yanıt tooyour isteği almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4668e-121">Within a few seconds, you should get a response tooyour request.</span></span> <span data-ttu-id="4668e-122">Merhaba kapsayıcı başlangıçta olacak bir **oluşturma** durumu, ancak bu işlem birkaç saniye içinde başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="4668e-122">Initially, hello container will be in a **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="4668e-123">Hello kullanarak hello durumunu kontrol edebilirsiniz `show` komutu:</span><span class="sxs-lookup"><span data-stu-id="4668e-123">You can check hello status using hello `show` command:</span></span>

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="4668e-124">Merhaba Çıktı Hello altındaki hello kapsayıcının sağlama durumunu ve IP adresini görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="4668e-124">At hello bottom of hello output, you will see hello container's provisioning state and its IP address:</span></span>

```json
...
"ipAddress": {
      "ip": "13.88.8.148",
      "ports": [
        {
          "port": 80,
          "protocol": "TCP"
        }
      ]
    },
    "osType": "Linux",
    "provisioningState": "Succeeded"
...
```

<span data-ttu-id="4668e-125">Merhaba kapsayıcı toohello taşır sonra **başarılı** durumunda, ulaşana, sağlanan başlangıç IP adresi kullanarak hello tarayıcıda.</span><span class="sxs-lookup"><span data-stu-id="4668e-125">Once hello container moves toohello **Succeeded** state, you can reach it in hello browser using hello IP address provided.</span></span> 

![Azure Container Instances kullanılarak dağıtılmış uygulama tarayıcıda görüntüleniyor][aci-app-browser]

## <a name="pull-hello-container-logs"></a><span data-ttu-id="4668e-127">Merhaba kapsayıcı günlüklerini</span><span class="sxs-lookup"><span data-stu-id="4668e-127">Pull hello container logs</span></span>

<span data-ttu-id="4668e-128">Merhaba günlükleri hello kullanılarak oluşturulan hello kapsayıcısı için çekme `logs` komutu:</span><span class="sxs-lookup"><span data-stu-id="4668e-128">You can pull hello logs for hello container you created using hello `logs` command:</span></span>

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="4668e-129">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="4668e-129">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-hello-container"></a><span data-ttu-id="4668e-130">Merhaba kapsayıcısını silmek</span><span class="sxs-lookup"><span data-stu-id="4668e-130">Delete hello container</span></span>

<span data-ttu-id="4668e-131">Merhaba kapsayıcıyla bittiğinde hello kullanarak kaldırabilirsiniz `delete` komutu:</span><span class="sxs-lookup"><span data-stu-id="4668e-131">When you are done with hello container, you can remove it using hello `delete` command:</span></span>

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="4668e-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4668e-132">Next steps</span></span>

<span data-ttu-id="4668e-133">Bu hızlı başlangıç bölümünde kullanılan hello kapsayıcısı için tüm hello kod [github'da][app-github-repo], kendi Dockerfile yanı sıra.</span><span class="sxs-lookup"><span data-stu-id="4668e-133">All of hello code for hello container used in this quick start is available [on GitHub][app-github-repo], along with its Dockerfile.</span></span> <span data-ttu-id="4668e-134">Kendiniz oluşturma ve tooAzure kapsayıcı hello Azure kapsayıcı kayıt defterini kullanarak örnekleri dağıtma tootry isterseniz, toohello Azure kapsayıcı örnekleri öğretici devam edin.</span><span class="sxs-lookup"><span data-stu-id="4668e-134">If you'd like tootry building it yourself and deploying it tooAzure Container Instances using hello Azure Container Registry, continue toohello Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4668e-135">Azure Container Instances öğreticileri</span><span class="sxs-lookup"><span data-stu-id="4668e-135">Azure Container Instances tutorials</span></span>](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png