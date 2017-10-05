---
title: "İlk Azure Container Instances kapsayıcınızı oluşturma | Azure Docs"
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
ms.openlocfilehash: 905f69e5e1e237a31d9bb1e326969ec83292c244
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a><span data-ttu-id="5889a-103">Azure Container Instances’da ilk kapsayıcınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5889a-103">Create your first container in Azure Container Instances</span></span>

<span data-ttu-id="5889a-104">Azure Container Instances, Azure’da kapsayıcı oluşturmayı ve yönetmeyi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="5889a-104">Azure Container Instances makes it easy to create and manage containers in Azure.</span></span> <span data-ttu-id="5889a-105">Bu hızlı başlangıç içeriğinde, bir kapsayıcı oluşturacak ve bu kapsayıcıyı genel IP adresi ile İnternet üzerinden kullanıma sunacaksınız.</span><span class="sxs-lookup"><span data-stu-id="5889a-105">In this quick start, you will create a container in Azure and expose it to the internet with a public IP address.</span></span> <span data-ttu-id="5889a-106">Bu işlem tek bir komutla tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="5889a-106">This operation is completed in a single command.</span></span> <span data-ttu-id="5889a-107">Yalnızca birkaç saniye içinde tarayıcınızda şunu görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="5889a-107">Within just a few seconds, you will see this in your browser:</span></span>

![Azure Container Instances kullanılarak dağıtılmış uygulama tarayıcıda görüntüleniyor][aci-app-browser]

<span data-ttu-id="5889a-109">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5889a-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5889a-110">CLI'yi yerel olarak yükleyip kullanmayı seçerseniz bu hızlı başlangıç için Azure CLI 2.0.12 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5889a-110">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.12 or later.</span></span> <span data-ttu-id="5889a-111">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5889a-111">Run `az --version` to find the version.</span></span> <span data-ttu-id="5889a-112">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5889a-112">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="5889a-113">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="5889a-113">Create a resource group</span></span>

<span data-ttu-id="5889a-114">Azure Container Instances örnekleri Azure kaynaklarıdır ve Azure kaynaklarının dağıtıldığı ve yönetildiği mantıksal bir koleksiyon olan Azure kaynak gruplarına yerleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="5889a-114">Azure Container Instances are Azure resources and must be placed in an Azure resource group, a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="5889a-115">[az group create](/cli/azure/group#create) komutuyla bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5889a-115">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="5889a-116">Aşağıdaki örnek *eastus* konumunda *myResourceGroup* adlı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5889a-116">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a><span data-ttu-id="5889a-117">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5889a-117">Create a container</span></span>

<span data-ttu-id="5889a-118">Bir ad, Docker görüntüsü ve bir Azure kaynak grubu sağlayarak kapsayıcı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5889a-118">You can create a container by providing a name, a Docker image, and an Azure resource group.</span></span> <span data-ttu-id="5889a-119">İsteğe bağlı olarak, kapsayıcıyı genel IP adresi ile İnternet üzerinden kullanıma sunabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5889a-119">You can optionally expose the container to the internet with a public IP address.</span></span> <span data-ttu-id="5889a-120">Bu durumda, [Node.js](http://nodejs.org) ile yazılan, çok basit bir web uygulamasını barındıran bir kapsayıcı kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="5889a-120">In this case, we'll use a container that hosts a very simple web app written in [Node.js](http://nodejs.org).</span></span>

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

<span data-ttu-id="5889a-121">Birkaç saniye içinde isteğinize yanıt almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5889a-121">Within a few seconds, you should get a response to your request.</span></span> <span data-ttu-id="5889a-122">Kapsayıcı başlangıçta **oluşturma** durumunda olacaktır ancak birkaç saniye içinde başlar.</span><span class="sxs-lookup"><span data-stu-id="5889a-122">Initially, the container will be in a **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="5889a-123">Durumu `show` komutunu kullanarak denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5889a-123">You can check the status using the `show` command:</span></span>

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="5889a-124">Çıktının alt kısmında kapsayıcının sağlama durumunu ve IP adresini görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="5889a-124">At the bottom of the output, you will see the container's provisioning state and its IP address:</span></span>

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

<span data-ttu-id="5889a-125">Kapsayıcı **başarılı** durumuna geçtiğinde, sağlanan IP adresini kullanarak tarayıcınızdan kapsayıcıya ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5889a-125">Once the container moves to the **Succeeded** state, you can reach it in the browser using the IP address provided.</span></span> 

![Azure Container Instances kullanılarak dağıtılmış uygulama tarayıcıda görüntüleniyor][aci-app-browser]

## <a name="pull-the-container-logs"></a><span data-ttu-id="5889a-127">Kapsayıcı günlüklerini çekme</span><span class="sxs-lookup"><span data-stu-id="5889a-127">Pull the container logs</span></span>

<span data-ttu-id="5889a-128">Oluşturduğunuz kapsayıcı için günlükleri `logs` komutunu kullanarak çekebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5889a-128">You can pull the logs for the container you created using the `logs` command:</span></span>

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="5889a-129">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="5889a-129">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-the-container"></a><span data-ttu-id="5889a-130">Kapsayıcıyı silme</span><span class="sxs-lookup"><span data-stu-id="5889a-130">Delete the container</span></span>

<span data-ttu-id="5889a-131">Kapsayıcıyla işiniz bittiğinde `delete` komutunu kullanarak kapsayıcıyı kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5889a-131">When you are done with the container, you can remove it using the `delete` command:</span></span>

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="5889a-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5889a-132">Next steps</span></span>

<span data-ttu-id="5889a-133">Bu hızlı başlangıç bölümünde kullanılan kapsayıcısı için tüm kodlar [GitHub'da][app-github-repo], ilgili Dockerfile ile birlikte bulunur.</span><span class="sxs-lookup"><span data-stu-id="5889a-133">All of the code for the container used in this quick start is available [on GitHub][app-github-repo], along with its Dockerfile.</span></span> <span data-ttu-id="5889a-134">Kapsayıcıyı kendiniz oluşturup Azure Container Registry’yi kullanarak Azure Container Instances’a dağıtmayı denemek istiyorsanız Azure Container Instances öğreticisine geçin.</span><span class="sxs-lookup"><span data-stu-id="5889a-134">If you'd like to try building it yourself and deploying it to Azure Container Instances using the Azure Container Registry, continue to the Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5889a-135">Azure Container Instances öğreticileri</span><span class="sxs-lookup"><span data-stu-id="5889a-135">Azure Container Instances tutorials</span></span>](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png