---
title: "aaaQuickstart - Linux Azure Docker CE küme | Microsoft Docs"
description: "Hızlı bir şekilde toocreate hello Azure CLI ile Azure kapsayıcı Hizmeti'nde Linux kapsayıcıları bir Docker CE küme öğrenin."
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
ms.date: 08/25/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 6c26c12ed085ec379c3486095a5fa51379afc5a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-ce-cluster"></a><span data-ttu-id="d55d1-103">Docker CE kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="d55d1-103">Deploy Docker CE cluster</span></span>

<span data-ttu-id="d55d1-104">Bu Hızlı Başlangıç, Docker CE küme hello Azure CLI kullanarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="d55d1-104">In this quick start, a Docker CE cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="d55d1-105">Web ön uç ve bir Redis örneği oluşan çok kapsayıcı uygulama sonra dağıtılan ve hello kümede çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d55d1-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="d55d1-106">Tamamlandığında, Merhaba uygulaması üzerinden erişilebilen Internet hello.</span><span class="sxs-lookup"><span data-stu-id="d55d1-106">Once completed, hello application is accessible over hello internet.</span></span>

<span data-ttu-id="d55d1-107">Azure Container Service’teki Docker CE önizlemededir ve **üretim iş yükleri için kullanılmamalıdır**.</span><span class="sxs-lookup"><span data-stu-id="d55d1-107">Docker CE on Azure Container Service is in preview and **should not be used for production workloads**.</span></span>

<span data-ttu-id="d55d1-108">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d55d1-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="d55d1-109">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu hızlı başlangıç hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="d55d1-109">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d55d1-110">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="d55d1-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d55d1-111">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d55d1-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="d55d1-112">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d55d1-112">Create a resource group</span></span>

<span data-ttu-id="d55d1-113">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="d55d1-113">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d55d1-114">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği mantıksal bir gruptur.</span><span class="sxs-lookup"><span data-stu-id="d55d1-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="d55d1-115">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *ukwest* konumu.</span><span class="sxs-lookup"><span data-stu-id="d55d1-115">hello following example creates a resource group named *myResourceGroup* in hello *ukwest* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
```

<span data-ttu-id="d55d1-116">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="d55d1-116">Output:</span></span>

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

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="d55d1-117">Docker Swarm kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d55d1-117">Create Docker Swarm cluster</span></span>

<span data-ttu-id="d55d1-118">Docker CE küme Azure kapsayıcı hizmeti ile Merhaba oluşturmak [az acs oluşturmak](/cli/azure/acs#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="d55d1-118">Create a Docker CE cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="d55d1-119">Merhaba aşağıdaki örnek adlı bir küme oluşturur *mySwarmCluster* ile bir Linux ana düğümü ve üç Linux Aracısı düğümleri.</span><span class="sxs-lookup"><span data-stu-id="d55d1-119">hello following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="d55d1-120">Birkaç dakika sonra hello komut tamamlandıktan ve biçimlendirilmiş json hello kümesi hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="d55d1-120">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="d55d1-121">Toohello kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="d55d1-121">Connect toohello cluster</span></span>

<span data-ttu-id="d55d1-122">Bu hızlı başlangıç hello FQDN'si hello Docker Swarm ana ve hello Docker aracı havuzu gerekir.</span><span class="sxs-lookup"><span data-stu-id="d55d1-122">Throughout this quick start, you need hello FQDN of both hello Docker Swarm master and hello Docker agent pool.</span></span> <span data-ttu-id="d55d1-123">Tooreturn, her ikisi de hello ana ve aracısını FQDN'lere komutu aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d55d1-123">Run hello following command tooreturn both hello master and agent FQDNs.</span></span>


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

<span data-ttu-id="d55d1-124">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="d55d1-124">Output:</span></span>

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

<span data-ttu-id="d55d1-125">Bir SSH tünel toohello Swarm şablonu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d55d1-125">Create an SSH tunnel toohello Swarm master.</span></span> <span data-ttu-id="d55d1-126">Değiştir `MasterFQDN` hello Swarm yöneticisinin hello FQDN adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="d55d1-126">Replace `MasterFQDN` with hello FQDN address of hello Swarm master.</span></span>

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

<span data-ttu-id="d55d1-127">Set hello `DOCKER_HOST` ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="d55d1-127">Set hello `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="d55d1-128">Bu işlem, toospecify hello hello ana bilgisayar adını gerek kalmadan hello Docker Swarm karşı toorun docker komutları sağlar.</span><span class="sxs-lookup"><span data-stu-id="d55d1-128">This allows you toorun docker commands against hello Docker Swarm without having toospecify hello name of hello host.</span></span>

```bash
export DOCKER_HOST=localhost:2374
```

<span data-ttu-id="d55d1-129">Merhaba Docker Swarm hazır toorun Docker hizmetlerini sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="d55d1-129">You are now ready toorun Docker services on hello Docker Swarm.</span></span>


## <a name="run-hello-application"></a><span data-ttu-id="d55d1-130">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="d55d1-130">Run hello application</span></span>

<span data-ttu-id="d55d1-131">Adlı bir dosya oluşturun `azure-vote.yaml` ve kopyalama hello aşağıdaki içerik içine.</span><span class="sxs-lookup"><span data-stu-id="d55d1-131">Create a file named `azure-vote.yaml` and copy hello following content into it.</span></span>


```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

<span data-ttu-id="d55d1-132">Merhaba çalıştırmak [docker yığın dağıtmak](https://docs.docker.com/engine/reference/commandline/stack_deploy/) toocreate hello Azure oy hizmet komutu.</span><span class="sxs-lookup"><span data-stu-id="d55d1-132">Run hello [docker stack deploy](https://docs.docker.com/engine/reference/commandline/stack_deploy/) command toocreate hello Azure Vote service.</span></span>

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

<span data-ttu-id="d55d1-133">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="d55d1-133">Output:</span></span>

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

<span data-ttu-id="d55d1-134">Kullanım hello [docker yığın ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) komut tooreturn hello hello uygulama dağıtım durumu.</span><span class="sxs-lookup"><span data-stu-id="d55d1-134">Use hello [docker stack ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) command tooreturn hello deployment status of hello application.</span></span>

```bash
docker stack ps azure-vote
```

<span data-ttu-id="d55d1-135">Bir kez hello `CURRENT STATE` her hizmetidir `Running`, Merhaba uygulaması hazır.</span><span class="sxs-lookup"><span data-stu-id="d55d1-135">Once hello `CURRENT STATE` of each service is `Running`, hello application is ready.</span></span>

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-hello-application"></a><span data-ttu-id="d55d1-136">Merhaba uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="d55d1-136">Test hello application</span></span>

<span data-ttu-id="d55d1-137">Toohello hello Swarm aracı havuzu tootest hello Azure oy uygulama çıkışı FQDN'sini göz atın.</span><span class="sxs-lookup"><span data-stu-id="d55d1-137">Browse toohello FQDN of hello Swarm agent pool tootest out hello Azure Vote application.</span></span>

![TooAzure oy göz atma görüntüsü](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="d55d1-139">Kümeyi silme</span><span class="sxs-lookup"><span data-stu-id="d55d1-139">Delete cluster</span></span>
<span data-ttu-id="d55d1-140">Merhaba küme artık gerekli olmadığında hello kullanabilirsiniz [az grubu Sil](/cli/azure/group#delete) tooremove hello kaynak grubu, kapsayıcı hizmeti ve ilgili tüm kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="d55d1-140">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="d55d1-141">Merhaba kod alın</span><span class="sxs-lookup"><span data-stu-id="d55d1-141">Get hello code</span></span>

<span data-ttu-id="d55d1-142">Bu Hızlı Başlangıç, önceden oluşturulmuş kapsayıcı görüntüleri kullanılan toocreate Docker hizmet olmuştur.</span><span class="sxs-lookup"><span data-stu-id="d55d1-142">In this quick start, pre-created container images have been used toocreate a Docker service.</span></span> <span data-ttu-id="d55d1-143">uygulama kodu, Dockerfile, Hello ilgili ve oluşturma dosya Github'da bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d55d1-143">hello related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="d55d1-144">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="d55d1-144">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="d55d1-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d55d1-145">Next steps</span></span>

<span data-ttu-id="d55d1-146">Bu Hızlı Başlangıç, Docker Swarm kümesi dağıtılan ve çok kapsayıcı uygulama tooit dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="d55d1-146">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application tooit.</span></span>

<span data-ttu-id="d55d1-147">Docker sıcak Visual Studio Team Services ile tümleştirme hakkında toolearn toohello CI/CD Docker Swarm ve VSTS ile devam edin.</span><span class="sxs-lookup"><span data-stu-id="d55d1-147">toolearn about integrating Docker warm with Visual Studio Team Services, continue toohello CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d55d1-148">Docker Swarm ve VSTS ile CI/CD</span><span class="sxs-lookup"><span data-stu-id="d55d1-148">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)