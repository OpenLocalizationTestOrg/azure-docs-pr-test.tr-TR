---
title: "aaaQuickstart - Azure Docker Swarm kümesi Linux için | Microsoft Docs"
description: "Hızlı bir şekilde toocreate Docker Swarm kümesi hello Azure CLI ile Azure kapsayıcı Hizmeti'nde Linux kapsayıcıları için öğrenin."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, Docker, Swarm
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/14/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 3028d2d00585360ec163518bf98f69bb0dd44dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-swarm-cluster"></a><span data-ttu-id="3571e-103">Docker Swarm kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="3571e-103">Deploy Docker Swarm cluster</span></span>

<span data-ttu-id="3571e-104">Bu Hızlı Başlangıç, Docker Swarm kümesi hello Azure CLI kullanarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="3571e-104">In this quick start, a Docker Swarm cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="3571e-105">Web ön uç ve bir Redis örneği oluşan çok kapsayıcı uygulama sonra dağıtılan ve hello kümede çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3571e-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="3571e-106">Tamamlandığında, Merhaba uygulaması üzerinden erişilebilen Internet hello.</span><span class="sxs-lookup"><span data-stu-id="3571e-106">Once completed, hello application is accessible over hello internet.</span></span>

<span data-ttu-id="3571e-107">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3571e-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="3571e-108">Bu hızlı başlangıç hello Azure CLI Sürüm 2.0.4 çalıştırdığınız gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="3571e-108">This quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="3571e-109">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="3571e-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3571e-110">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3571e-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="3571e-111">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="3571e-111">Create a resource group</span></span>

<span data-ttu-id="3571e-112">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="3571e-112">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="3571e-113">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği mantıksal bir gruptur.</span><span class="sxs-lookup"><span data-stu-id="3571e-113">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="3571e-114">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *westus* konumu.</span><span class="sxs-lookup"><span data-stu-id="3571e-114">hello following example creates a resource group named *myResourceGroup* in hello *westus* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="3571e-115">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="3571e-115">Output:</span></span>

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westcentralus",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="3571e-116">Docker Swarm kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="3571e-116">Create Docker Swarm cluster</span></span>

<span data-ttu-id="3571e-117">Docker Swarm kümesi Azure kapsayıcı hizmeti ile Merhaba oluşturma [az acs oluşturmak](/cli/azure/acs#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="3571e-117">Create a Docker Swarm cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="3571e-118">Merhaba aşağıdaki örnek adlı bir küme oluşturur *mySwarmCluster* ile bir Linux ana düğümü ve üç Linux Aracısı düğümleri.</span><span class="sxs-lookup"><span data-stu-id="3571e-118">hello following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type Swarm --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="3571e-119">Birkaç dakika sonra hello komut tamamlandıktan ve biçimlendirilmiş json hello kümesi hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="3571e-119">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="3571e-120">Toohello kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="3571e-120">Connect toohello cluster</span></span>

<span data-ttu-id="3571e-121">Bu hızlı başlangıç hello Docker Swarm ana ve hello Docker aracı havuzu başlangıç IP adresi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="3571e-121">Throughout this quick start, you need hello IP address of both hello Docker Swarm master and hello Docker agent pool.</span></span> <span data-ttu-id="3571e-122">Çalışma hello şu iki IP adresi tooreturn komutu.</span><span class="sxs-lookup"><span data-stu-id="3571e-122">Run hello following command tooreturn both IP addresses.</span></span>


```bash
az network public-ip list --resource-group myResourceGroup --query '[*].{Name:name,IPAddress:ipAddress}' -o table
```

<span data-ttu-id="3571e-123">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="3571e-123">Output:</span></span>

```bash
Name                                                                 IPAddress
-------------------------------------------------------------------  -------------
swarmm-agent-ip-myswarmcluster-myresourcegroup-d5b9d4agent-66066781  52.179.23.131
swarmm-master-ip-myswarmcluster-myresourcegroup-d5b9d4mgmt-66066781  52.141.37.199
```

<span data-ttu-id="3571e-124">Bir SSH tünel toohello Swarm şablonu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3571e-124">Create an SSH tunnel toohello Swarm master.</span></span> <span data-ttu-id="3571e-125">Değiştir `IPAddress` hello Swarm yöneticisinin hello IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="3571e-125">Replace `IPAddress` with hello IP address of hello Swarm master.</span></span>

```bash
ssh -p 2200 -fNL 2375:localhost:2375 azureuser@IPAddress
```

<span data-ttu-id="3571e-126">Set hello `DOCKER_HOST` ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="3571e-126">Set hello `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="3571e-127">Bu işlem, toospecify hello hello ana bilgisayar adını gerek kalmadan hello Docker Swarm karşı toorun docker komutları sağlar.</span><span class="sxs-lookup"><span data-stu-id="3571e-127">This allows you toorun docker commands against hello Docker Swarm without having toospecify hello name of hello host.</span></span>

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="3571e-128">Merhaba Docker Swarm hazır toorun Docker hizmetlerini sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="3571e-128">You are now ready toorun Docker services on hello Docker Swarm.</span></span>


## <a name="run-hello-application"></a><span data-ttu-id="3571e-129">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="3571e-129">Run hello application</span></span>

<span data-ttu-id="3571e-130">Adlı bir dosya oluşturun `docker-compose.yaml` ve kopyalama hello aşağıdaki içerik içine.</span><span class="sxs-lookup"><span data-stu-id="3571e-130">Create a file named `docker-compose.yaml` and copy hello following content into it.</span></span>

```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    container_name: azure-vote-back
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    container_name: azure-vote-front
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

<span data-ttu-id="3571e-131">Komut toocreate hello Azure oy hizmeti aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3571e-131">Run hello following command toocreate hello Azure Vote service.</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="3571e-132">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="3571e-132">Output:</span></span>

```bash
Creating network "user_default" with hello default driver
Pulling azure-vote-front (microsoft/azure-vote-front:redis-v1)...
swarm-agent-EE873B23000005: Pulling microsoft/azure-vote-front:redis-v1...
swarm-agent-EE873B23000004: Pulling microsoft/azure-vote-front:redis-v1... : downloaded
Pulling azure-vote-back (redis:latest)...
swarm-agent-EE873B23000004: Pulling redis:latest... : downloaded
Creating azure-vote-front ... 
Creating azure-vote-back ... 
Creating azure-vote-front
Creating azure-vote-back ...
```

## <a name="test-hello-application"></a><span data-ttu-id="3571e-133">Merhaba uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="3571e-133">Test hello application</span></span>

<span data-ttu-id="3571e-134">Merhaba Swarm aracı havuzu tootest Merhaba Azure oylama uygulaması çıkışı toohello IP adresine göz atın.</span><span class="sxs-lookup"><span data-stu-id="3571e-134">Browse toohello IP address of hello Swarm agent pool tootest out hello Azure Vote application.</span></span>

![TooAzure oy göz atma görüntüsü](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="3571e-136">Kümeyi silme</span><span class="sxs-lookup"><span data-stu-id="3571e-136">Delete cluster</span></span>
<span data-ttu-id="3571e-137">Merhaba küme artık gerekli olmadığında hello kullanabilirsiniz [az grubu Sil](/cli/azure/group#delete) tooremove hello kaynak grubu, kapsayıcı hizmeti ve ilgili tüm kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="3571e-137">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="3571e-138">Merhaba kod alın</span><span class="sxs-lookup"><span data-stu-id="3571e-138">Get hello code</span></span>

<span data-ttu-id="3571e-139">Bu Hızlı Başlangıç, önceden oluşturulmuş kapsayıcı görüntüleri kullanılan toocreate Docker hizmet olmuştur.</span><span class="sxs-lookup"><span data-stu-id="3571e-139">In this quick start, pre-created container images have been used toocreate a Docker service.</span></span> <span data-ttu-id="3571e-140">uygulama kodu, Dockerfile, Hello ilgili ve oluşturma dosya Github'da bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3571e-140">hello related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="3571e-141">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="3571e-141">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="3571e-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3571e-142">Next steps</span></span>

<span data-ttu-id="3571e-143">Bu Hızlı Başlangıç, Docker Swarm kümesi dağıtılan ve çok kapsayıcı uygulama tooit dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="3571e-143">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application tooit.</span></span>

<span data-ttu-id="3571e-144">Docker sıcak Visual Studio Team Services ile tümleştirme hakkında toolearn toohello CI/CD Docker Swarm ve VSTS ile devam edin.</span><span class="sxs-lookup"><span data-stu-id="3571e-144">toolearn about integrating Docker warm with Visual Studio Team Services, continue toohello CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3571e-145">Docker Swarm ve VSTS ile CI/CD</span><span class="sxs-lookup"><span data-stu-id="3571e-145">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)