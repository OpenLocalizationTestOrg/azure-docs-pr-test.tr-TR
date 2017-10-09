---
title: "aaaAzure kapsayıcı hizmeti Öğreticisi - DC/OS yönetme | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Öğreticisi - DC/OS yönetme"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Container’lar, Mikro hizmetler, Kumernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/17/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b91c433bfd7e48ec405cc62be1486d9d4662839d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a><span data-ttu-id="5c3ac-104">Azure kapsayıcı hizmeti Öğreticisi - DC/OS yönetme</span><span class="sxs-lookup"><span data-stu-id="5c3ac-104">Azure Container Service tutorial - Manage DC/OS</span></span>

<span data-ttu-id="5c3ac-105">DC/OS çalışan modern ve kapsayıcılı uygulamaları için Dağıtılmış bir platform sağlar.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="5c3ac-106">Azure kapsayıcı hizmeti ile basit ve hızlı bir üretim hazır DC/OS kümesi sağlama.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="5c3ac-107">Bu hızlı başlangıç ayrıntıları temel adımlar, bir DC/OS kümesi ve çalışma temel iş yükü toodeploy gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-107">This quick start details basic steps needed toodeploy a DC/OS cluster and run basic workload.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5c3ac-108">Bir ACS DC/OS kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c3ac-108">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="5c3ac-109">Toohello kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="5c3ac-109">Connect toohello cluster</span></span>
> * <span data-ttu-id="5c3ac-110">Merhaba DC/OS CLI yükleme</span><span class="sxs-lookup"><span data-stu-id="5c3ac-110">Install hello DC/OS CLI</span></span>
> * <span data-ttu-id="5c3ac-111">Bir uygulama toohello kümeyi dağıtma</span><span class="sxs-lookup"><span data-stu-id="5c3ac-111">Deploy an application toohello cluster</span></span>
> * <span data-ttu-id="5c3ac-112">Merhaba kümede uygulama ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="5c3ac-112">Scale an application on hello cluster</span></span>
> * <span data-ttu-id="5c3ac-113">Merhaba DC/OS küme düğümleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="5c3ac-113">Scale hello DC/OS cluster nodes</span></span>
> * <span data-ttu-id="5c3ac-114">Temel DC/OS Yönetimi</span><span class="sxs-lookup"><span data-stu-id="5c3ac-114">Basic DC/OS management</span></span>
> * <span data-ttu-id="5c3ac-115">Merhaba DC/OS kümesi Sil</span><span class="sxs-lookup"><span data-stu-id="5c3ac-115">Delete hello DC/OS cluster</span></span>

<span data-ttu-id="5c3ac-116">Bu öğretici hello Azure CLI Sürüm 2.0.4 gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-116">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="5c3ac-117">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-117">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5c3ac-118">Tooupgrade gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5c3ac-118">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-dcos-cluster"></a><span data-ttu-id="5c3ac-119">DC/OS kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c3ac-119">Create DC/OS cluster</span></span>

<span data-ttu-id="5c3ac-120">İlk olarak, bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-120">First, create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="5c3ac-121">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-121">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="5c3ac-122">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *westeurope* konumu.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-122">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="5c3ac-123">Ardından, DC/OS kümesi ile Merhaba oluşturun [az acs oluşturmak](/cli/azure/acs#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-123">Next, create a DC/OS cluster with hello [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="5c3ac-124">Merhaba aşağıdaki örnek adlı bir DC/OS kümesi oluşturur *myDCOSCluster* ve zaten mevcut değilse SSH anahtarları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-124">hello following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="5c3ac-125">toouse belirli bir ayarla anahtarları, hello kullan `--ssh-key-value` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-125">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="5c3ac-126">Birkaç dakika sonra hello komut tamamlandıktan ve hello dağıtımı hakkında bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-126">After several minutes, hello command completes, and returns information about hello deployment.</span></span>

## <a name="connect-toodcos-cluster"></a><span data-ttu-id="5c3ac-127">TooDC/OS kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="5c3ac-127">Connect tooDC/OS cluster</span></span>

<span data-ttu-id="5c3ac-128">DC/OS kümesi oluşturulduktan sonra bir SSH tüneli üzerinden erişimleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-128">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="5c3ac-129">Çalışma hello aşağıdaki hello DC/OS ana tooreturn hello genel IP adresi komutu.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-129">Run hello following command tooreturn hello public IP address of hello DC/OS master.</span></span> <span data-ttu-id="5c3ac-130">Bu IP adresi bir değişkende depolanan ve hello sonraki adımda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-130">This IP address is stored in a variable and used in hello next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="5c3ac-131">toocreate SSH tüneli Merhaba, komutu aşağıdaki hello çalıştırın ve hello ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-131">toocreate hello SSH tunnel, run hello following command and follow hello on-screen instructions.</span></span> <span data-ttu-id="5c3ac-132">Bağlantı noktası 80 kullanımda hello komutu başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-132">If port 80 is already in use, hello command fails.</span></span> <span data-ttu-id="5c3ac-133">Güncelleştirme hello tünelli kullanılmadığı, bağlantı noktası tooone gibi `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-133">Update hello tunneled port tooone not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a><span data-ttu-id="5c3ac-134">DC/OS CLI'yi yükleyin</span><span class="sxs-lookup"><span data-stu-id="5c3ac-134">Install DC/OS CLI</span></span>

<span data-ttu-id="5c3ac-135">Hello kullanarak hello DC/OS CLI'yı yükleme [az acs dcos yükleme-CLI](/azure/acs/dcos#install-cli) komutu.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-135">Install hello DC/OS cli using hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="5c3ac-136">Azure CloudShell kullanıyorsanız, hello DC/OS CLI zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-136">If you are using Azure CloudShell, hello DC/OS CLI is already installed.</span></span> <span data-ttu-id="5c3ac-137">Hello Azure CLI macOS ya da Linux üzerinde çalıştırıyorsanız, sudo toorun hello komutuyla gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-137">If you are running hello Azure CLI on macOS or Linux, you might need toorun hello command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="5c3ac-138">CLI hello kümeyle kullanılabilir hello önce yapılandırılmış toouse hello SSH tüneli olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-138">Before hello CLI can be used with hello cluster, it must be configured toouse hello SSH tunnel.</span></span> <span data-ttu-id="5c3ac-139">toodo, bu nedenle, aşağıdaki komut, başlangıç bağlantı noktası gerekiyorsa ayarlama hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-139">toodo so, run hello following command, adjusting hello port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="5c3ac-140">Bir uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="5c3ac-140">Run an application</span></span>

<span data-ttu-id="5c3ac-141">bir ACS DC/OS kümesi için mekanizma zamanlama hello Marathon varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-141">hello default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="5c3ac-142">Marathon kullanılan toostart bir uygulamasıdır ve Merhaba uygulaması hello DC/OS kümesinde hello durumunu yönetin.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-142">Marathon is used toostart an application and manage hello state of hello application on hello DC/OS cluster.</span></span> <span data-ttu-id="5c3ac-143">bir uygulama, Marathon aracılığıyla tooschedule adlı bir dosya oluşturmak **marathon app.json**, kopya hello izleyerek içeriği içine.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-143">tooschedule an application through Marathon, create a file named **marathon-app.json**, and copy hello following contents into it.</span></span> 

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

<span data-ttu-id="5c3ac-144">Komut tooschedule hello uygulama toorun hello DC/OS kümesinde aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-144">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="5c3ac-145">toosee hello dağıtım durumunu hello uygulama, komutu aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-145">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="5c3ac-146">Ne zaman hello **görevleri** sütun değeri geçer *0/1* çok*1/1*, uygulama dağıtımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-146">When hello **TASKS** column value switches from *0/1* too*1/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a><span data-ttu-id="5c3ac-147">Marathon uygulamayı Ölçeklendir</span><span class="sxs-lookup"><span data-stu-id="5c3ac-147">Scale Marathon application</span></span>

<span data-ttu-id="5c3ac-148">Merhaba önceki örnekte, bir tek örnek uygulaması oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-148">In hello previous example, a single instance application was created.</span></span> <span data-ttu-id="5c3ac-149">Bu dağıtım hello uygulamanın üç örneğine kullanılabilir, böylece hello açmak tooupdate **marathon app.json** dosya ve hello örnek özellik too3 güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-149">tooupdate this deployment so that three instances of hello application are available, open up hello **marathon-app.json** file, and update hello instance property too3.</span></span>

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 3,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

<span data-ttu-id="5c3ac-150">Merhaba uygulaması Hello kullanarak güncelleştirme `dcos marathon app update` komutu.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-150">Update hello application using hello `dcos marathon app update` command.</span></span>

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

<span data-ttu-id="5c3ac-151">toosee hello dağıtım durumunu hello uygulama, komutu aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-151">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="5c3ac-152">Ne zaman hello **görevleri** sütun değeri geçer *1/3* çok*3/1*, uygulama dağıtımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-152">When hello **TASKS** column value switches from *1/3* too*3/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a><span data-ttu-id="5c3ac-153">Internet erişilebilir uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5c3ac-153">Run internet accessible app</span></span>

<span data-ttu-id="5c3ac-154">Merhaba ACS DC/OS kümesi oluşan iki düğüm kümesi üzerinde erişilebilir olan bir ortak hello Internet ve Internet üzerinde erişilemeyen bir özel hello.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-154">hello ACS DC/OS cluster consists of two node sets, one public which is accessible on hello internet, and one private which is not accessible on hello internet.</span></span> <span data-ttu-id="5c3ac-155">Merhaba varsayılan hello özel düğümler, hangi hello Son örnekte kullanılan kümesidir.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-155">hello default set is hello private nodes, which was used in hello last example.</span></span>

<span data-ttu-id="5c3ac-156">toomake erişilebilir bir uygulama üzerinde Internet Merhaba, bunları toohello ortak düğüm kümesi dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-156">toomake an application accessible on hello internet, deploy them toohello public node set.</span></span> <span data-ttu-id="5c3ac-157">toodo, bu nedenle, hello vermek `acceptedResourceRoles` değerini nesne `slave_public`.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-157">toodo so, give hello `acceptedResourceRoles` object a value of `slave_public`.</span></span>

<span data-ttu-id="5c3ac-158">Adlı bir dosya oluşturun **nginx public.json** ve kopyalama hello aşağıdaki içeriği içine.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-158">Create a file named **nginx-public.json** and copy hello following contents into it.</span></span>

```json
{
  "id": "demo-app",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  },
  "acceptedResourceRoles": [
    "slave_public"
  ]
}
```

<span data-ttu-id="5c3ac-159">Komut tooschedule hello uygulama toorun hello DC/OS kümesinde aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-159">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli 
dcos marathon app add nginx-public.json
```

<span data-ttu-id="5c3ac-160">Merhaba DC/OS ortak küme aracıları Hello genel IP adresi alın.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-160">Get hello public IP address of hello DC/OS public cluster agents.</span></span>

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="5c3ac-161">Toothis adresi gözatma hello varsayılan NGINX site döndürür.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-161">Browsing toothis address returns hello default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a><span data-ttu-id="5c3ac-163">Ölçek DC/OS kümesi</span><span class="sxs-lookup"><span data-stu-id="5c3ac-163">Scale DC/OS cluster</span></span>

<span data-ttu-id="5c3ac-164">Merhaba önceki örneklerde, ölçeklendirilmiş toomultiple örnek bir uygulama oluştu.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-164">In hello previous examples, an application was scaled toomultiple instance.</span></span> <span data-ttu-id="5c3ac-165">Merhaba DC/OS altyapı da daha fazla veya daha az işlem kapasitesini ölçeklendirilmiş tooprovide olabilir.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-165">hello DC/OS infrastructure can also be scaled tooprovide more or less compute capacity.</span></span> <span data-ttu-id="5c3ac-166">Bu hello ile yapılır [az acs ölçeklendirme]() komutu.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-166">This is done with hello [az acs scale]() command.</span></span> 

<span data-ttu-id="5c3ac-167">DC/OS aracılarının toosee hello geçerli sayısını hello kullan [acs az göster](/cli/azure/acs#show) komutu.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-167">toosee hello current count of DC/OS agents, use hello [az acs show](/cli/azure/acs#show) command.</span></span>

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

<span data-ttu-id="5c3ac-168">tooincrease sayısı too5 Merhaba, hello kullan [az acs ölçeklendirme](/cli/azure/acs#scale) komutu.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-168">tooincrease hello count too5, use hello [az acs scale](/cli/azure/acs#scale) command.</span></span> 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a><span data-ttu-id="5c3ac-169">DC/OS kümesi Sil</span><span class="sxs-lookup"><span data-stu-id="5c3ac-169">Delete DC/OS cluster</span></span>

<span data-ttu-id="5c3ac-170">Artık gerektiğinde Merhaba kullanabilirsiniz [az grubu Sil](/cli/azure/group#delete) tooremove hello kaynak grubu, DC/OS kümesi ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-170">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="5c3ac-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5c3ac-171">Next steps</span></span>

<span data-ttu-id="5c3ac-172">Bu öğreticide, hello aşağıdakileri içeren temel DC/OS yönetim görevle ilgili öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-172">In this tutorial, you have learned about basic DC/OS management task including hello following.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="5c3ac-173">Bir ACS DC/OS kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c3ac-173">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="5c3ac-174">Toohello kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="5c3ac-174">Connect toohello cluster</span></span>
> * <span data-ttu-id="5c3ac-175">Merhaba DC/OS CLI yükleme</span><span class="sxs-lookup"><span data-stu-id="5c3ac-175">Install hello DC/OS CLI</span></span>
> * <span data-ttu-id="5c3ac-176">Bir uygulama toohello kümeyi dağıtma</span><span class="sxs-lookup"><span data-stu-id="5c3ac-176">Deploy an application toohello cluster</span></span>
> * <span data-ttu-id="5c3ac-177">Merhaba kümede uygulama ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="5c3ac-177">Scale an application on hello cluster</span></span>
> * <span data-ttu-id="5c3ac-178">Merhaba DC/OS küme düğümleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="5c3ac-178">Scale hello DC/OS cluster nodes</span></span>
> * <span data-ttu-id="5c3ac-179">Merhaba DC/OS kümesi Sil</span><span class="sxs-lookup"><span data-stu-id="5c3ac-179">Delete hello DC/OS cluster</span></span>

<span data-ttu-id="5c3ac-180">Gelişmiş toohello sonraki öğretici toolearn hakkında Yük Dengeleme uygulamada DC/OS Azure üzerinde.</span><span class="sxs-lookup"><span data-stu-id="5c3ac-180">Advance toohello next tutorial toolearn about load balancing application in DC/OS on Azure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="5c3ac-181">Uygulamalarda yük dengeleme gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="5c3ac-181">Load balance applications</span></span>](container-service-load-balancing.md)