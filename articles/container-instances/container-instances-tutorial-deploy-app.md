---
title: "aaaAzure kapsayıcı örnekleri Öğreticisi - app dağıtma | Microsoft Docs"
description: "Azure kapsayıcı örnekleri Öğreticisi - app dağıtma"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b9fb098d9491e1073f0be4b14a0b9b1a18f16095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-tooazure-container-instances"></a><span data-ttu-id="feeba-103">Kapsayıcı tooAzure kapsayıcı örnekleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="feeba-103">Deploy a container tooAzure Container Instances</span></span>

<span data-ttu-id="feeba-104">Merhaba budur üç bölümlük öğreticinin son.</span><span class="sxs-lookup"><span data-stu-id="feeba-104">This is hello last of a three-part tutorial.</span></span> <span data-ttu-id="feeba-105">Önceki bölümlerde [bir kapsayıcı görüntüsü oluşturuldu](container-instances-tutorial-prepare-app.md) ve [tooan Azure kapsayıcı kayıt defteri gönderilen](container-instances-tutorial-prepare-acr.md).</span><span class="sxs-lookup"><span data-stu-id="feeba-105">In previous sections, [a container image was created](container-instances-tutorial-prepare-app.md) and [pushed tooan Azure Container Registry](container-instances-tutorial-prepare-acr.md).</span></span> <span data-ttu-id="feeba-106">Bu bölümde, hello kapsayıcı tooAzure kapsayıcı örnekleri dağıtarak hello öğretici tamamlar.</span><span class="sxs-lookup"><span data-stu-id="feeba-106">This section completes hello tutorial by deploying hello container tooAzure Container Instances.</span></span> <span data-ttu-id="feeba-107">Tamamlanan adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="feeba-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="feeba-108">Bir Azure Resource Manager şablonu kullanarak bir kapsayıcı grubu tanımlama</span><span class="sxs-lookup"><span data-stu-id="feeba-108">Defining a container group using an Azure Resource Manager template</span></span>
> * <span data-ttu-id="feeba-109">Hello Azure CLI kullanarak hello kapsayıcı grubu dağıtma</span><span class="sxs-lookup"><span data-stu-id="feeba-109">Deploying hello container group using hello Azure CLI</span></span>
> * <span data-ttu-id="feeba-110">Kapsayıcı günlükleri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="feeba-110">Viewing container logs</span></span>

## <a name="deploy-hello-container-using-hello-azure-cli"></a><span data-ttu-id="feeba-111">Hello Azure CLI kullanarak hello kapsayıcı dağıtma</span><span class="sxs-lookup"><span data-stu-id="feeba-111">Deploy hello container using hello Azure CLI</span></span>

<span data-ttu-id="feeba-112">Hello Azure CLI tek bir komut bir kapsayıcı tooAzure kapsayıcı örnekleri dağıtımını sağlar.</span><span class="sxs-lookup"><span data-stu-id="feeba-112">hello Azure CLI enables deployment of a container tooAzure Container Instances in a single command.</span></span> <span data-ttu-id="feeba-113">Merhaba kapsayıcı görüntü barındırılan beri içinde özel Azure kapsayıcı kayıt defteri Merhaba, hello kimlik bilgileri gerekli tooaccess içermelidir.</span><span class="sxs-lookup"><span data-stu-id="feeba-113">Since hello container image is hosted in hello private Azure Container Registry, you must include hello credentials required tooaccess it.</span></span> <span data-ttu-id="feeba-114">Gerekirse, aşağıda gösterildiği gibi bunları sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="feeba-114">If necessary, you can query them as shown below.</span></span>

<span data-ttu-id="feeba-115">Kapsayıcı kayıt defteri oturum açma sunucusu (kayıt defteri adınızı güncelleştirmesiyle):</span><span class="sxs-lookup"><span data-stu-id="feeba-115">Container registry login server (update with your registry name):</span></span>

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

<span data-ttu-id="feeba-116">Kapsayıcı kayıt defteri parola:</span><span class="sxs-lookup"><span data-stu-id="feeba-116">Container registry password:</span></span>

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

<span data-ttu-id="feeba-117">toodeploy kapsayıcı görüntünüzü bir kaynakla hello kapsayıcı kayıt defterinden 1 CPU Çekirdeği ve 1 GB bellek, komutu aşağıdaki hello çalıştırma isteği:</span><span class="sxs-lookup"><span data-stu-id="feeba-117">toodeploy your container image from hello container registry with a resource request of 1 CPU core and 1GB of memory, run hello following command:</span></span>

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

<span data-ttu-id="feeba-118">Birkaç saniye içinde Azure Kaynak Yöneticisi'nden bir ilk yanıtı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="feeba-118">Within a few seconds, you will receive an initial response from Azure Resource Manager.</span></span> <span data-ttu-id="feeba-119">tooview hello durumu hello dağıtımının kullanın:</span><span class="sxs-lookup"><span data-stu-id="feeba-119">tooview hello state of hello deployment, use:</span></span>

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

<span data-ttu-id="feeba-120">Biz hello durumu değişiklikleri kadar bu komut çalışmaya devam *bekleyen* çok*çalıştıran*.</span><span class="sxs-lookup"><span data-stu-id="feeba-120">We can continue running this command until hello state changes from *pending* too*running*.</span></span> <span data-ttu-id="feeba-121">Ardından biz geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="feeba-121">Then we can proceed.</span></span>

## <a name="view-hello-application-and-container-logs"></a><span data-ttu-id="feeba-122">Merhaba uygulama ve kapsayıcı günlüklerini görüntüle</span><span class="sxs-lookup"><span data-stu-id="feeba-122">View hello application and container logs</span></span>

<span data-ttu-id="feeba-123">Merhaba dağıtım başarılı olduktan sonra komutu aşağıdaki hello hello çıktıda gösterilen tarayıcı toohello IP adresiniz açın:</span><span class="sxs-lookup"><span data-stu-id="feeba-123">Once hello deployment succeeds, open your browser toohello IP address shown in hello output of hello following command:</span></span>

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Hello world hello tarayıcı uygulamasında][aci-app-browser]

<span data-ttu-id="feeba-125">Merhaba kapsayıcı hello günlük çıktısı de görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="feeba-125">You can also view hello log output of hello container:</span></span>

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

<span data-ttu-id="feeba-126">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="feeba-126">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a><span data-ttu-id="feeba-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="feeba-127">Next steps</span></span>

<span data-ttu-id="feeba-128">Bu öğreticide, kapsayıcıları tooAzure kapsayıcı örnekleri dağıtma hello işlemi tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="feeba-128">In this tutorial, you completed hello process of deploying your containers tooAzure Container Instances.</span></span> <span data-ttu-id="feeba-129">Aşağıdaki adımları hello tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="feeba-129">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="feeba-130">Azure CLI hello Azure kapsayıcı kayıt defteri hello kullanarak hello kapsayıcı dağıtma</span><span class="sxs-lookup"><span data-stu-id="feeba-130">Deploying hello container from hello Azure Container Registry using hello Azure CLI</span></span>
> * <span data-ttu-id="feeba-131">Merhaba uygulaması hello tarayıcıda görüntüleme</span><span class="sxs-lookup"><span data-stu-id="feeba-131">Viewing hello application in hello browser</span></span>
> * <span data-ttu-id="feeba-132">Görüntüleme hello kapsayıcı günlükleri</span><span class="sxs-lookup"><span data-stu-id="feeba-132">Viewing hello container logs</span></span>

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
