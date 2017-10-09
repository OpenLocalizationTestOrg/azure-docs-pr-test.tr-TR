---
title: "aaaAzure kapsayıcı hizmeti hızlı başlangıç - DC/OS kümesi dağıtma | Microsoft Docs"
description: "Azure kapsayıcı hizmeti hızlı başlangıç - DC/OS kümesi dağıtma"
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b961f15bd73deeafda5a3fc25ab53c839195219b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-dcos-cluster"></a><span data-ttu-id="ee1e6-104">DC/OS kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="ee1e6-104">Deploy a DC/OS cluster</span></span>

<span data-ttu-id="ee1e6-105">DC/OS çalışan modern ve kapsayıcılı uygulamaları için Dağıtılmış bir platform sağlar.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="ee1e6-106">Azure kapsayıcı hizmeti ile basit ve hızlı bir üretim hazır DC/OS kümesi sağlama.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="ee1e6-107">Bu hızlı başlangıç ayrıntıları hello temel adımlar bir DC/OS kümesi ve çalışma temel iş yükü toodeploy gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-107">This quick start details hello basic steps needed toodeploy a DC/OS cluster and run basic workload.</span></span>

<span data-ttu-id="ee1e6-108">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="ee1e6-109">Bu öğretici hello Azure CLI Sürüm 2.0.4 gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-109">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ee1e6-110">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ee1e6-111">Tooupgrade gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ee1e6-111">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="log-in-tooazure"></a><span data-ttu-id="ee1e6-112">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="ee1e6-112">Log in tooAzure</span></span> 

<span data-ttu-id="ee1e6-113">Tooyour hello Azure aboneliğiyle oturum [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-113">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="ee1e6-114">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="ee1e6-114">Create a resource group</span></span>

<span data-ttu-id="ee1e6-115">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="ee1e6-116">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-116">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="ee1e6-117">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-117">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a><span data-ttu-id="ee1e6-118">DC/OS kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ee1e6-118">Create DC/OS cluster</span></span>

<span data-ttu-id="ee1e6-119">DC/OS kümesi ile Merhaba oluşturma [az acs oluşturmak](/cli/azure/acs#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-119">Create a DC/OS cluster with hello [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="ee1e6-120">Merhaba aşağıdaki örnek adlı bir DC/OS kümesi oluşturur *myDCOSCluster* ve zaten mevcut değilse SSH anahtarları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-120">hello following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="ee1e6-121">toouse belirli bir ayarla anahtarları, hello kullan `--ssh-key-value` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-121">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="ee1e6-122">Birkaç dakika sonra hello komut tamamlandıktan ve hello dağıtımı hakkında bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-122">After several minutes, hello command completes, and returns information about hello deployment.</span></span>

## <a name="connect-toodcos-cluster"></a><span data-ttu-id="ee1e6-123">TooDC/OS kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="ee1e6-123">Connect tooDC/OS cluster</span></span>

<span data-ttu-id="ee1e6-124">DC/OS kümesi oluşturulduktan sonra bir SSH tüneli üzerinden erişimleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-124">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="ee1e6-125">Çalışma hello aşağıdaki hello DC/OS ana tooreturn hello genel IP adresi komutu.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-125">Run hello following command tooreturn hello public IP address of hello DC/OS master.</span></span> <span data-ttu-id="ee1e6-126">Bu IP adresi bir değişkende depolanan ve hello sonraki adımda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-126">This IP address is stored in a variable and used in hello next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="ee1e6-127">toocreate SSH tüneli Merhaba, komutu aşağıdaki hello çalıştırın ve hello ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-127">toocreate hello SSH tunnel, run hello following command and follow hello on-screen instructions.</span></span> <span data-ttu-id="ee1e6-128">Bağlantı noktası 80 kullanımda hello komutu başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-128">If port 80 is already in use, hello command fails.</span></span> <span data-ttu-id="ee1e6-129">Güncelleştirme hello tünelli kullanılmadığı, bağlantı noktası tooone gibi `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-129">Update hello tunneled port tooone not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

<span data-ttu-id="ee1e6-130">Merhaba SSH tüneli çok göz atarak test edilmiş`http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-130">hello SSH tunnel can be tested by browsing too`http://localhost`.</span></span> <span data-ttu-id="ee1e6-131">Bir bağlantı noktası, diğer 80 oluşturulduğunu hello konumu toomatch ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-131">If a port other that 80 has been used, adjust hello location toomatch.</span></span> 

<span data-ttu-id="ee1e6-132">Merhaba SSH tüneli başarıyla oluşturulduysa hello DC/OS portal döndürülür.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-132">If hello SSH tunnel was successfully created, hello DC/OS portal is returned.</span></span>

![DCOS KULLANICI ARABİRİMİ](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a><span data-ttu-id="ee1e6-134">DC/OS CLI'yi yükleyin</span><span class="sxs-lookup"><span data-stu-id="ee1e6-134">Install DC/OS CLI</span></span>

<span data-ttu-id="ee1e6-135">Merhaba DC/OS komut satırı arabirimi kullanılan toomanage hello komut satırı DC/OS kümeden ' dir.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-135">hello DC/OS command line interface is used toomanage a DC/OS cluster from hello command-line.</span></span> <span data-ttu-id="ee1e6-136">Hello kullanarak hello DC/OS CLI'yı yükleme [az acs dcos yükleme-CLI](/azure/acs/dcos#install-cli) komutu.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-136">Install hello DC/OS cli using hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="ee1e6-137">Azure CloudShell kullanıyorsanız, hello DC/OS CLI zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-137">If you are using Azure CloudShell, hello DC/OS CLI is already installed.</span></span> 

<span data-ttu-id="ee1e6-138">Hello Azure CLI macOS ya da Linux üzerinde çalıştırıyorsanız, sudo toorun hello komutuyla gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-138">If you are running hello Azure CLI on macOS or Linux, you might need toorun hello command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="ee1e6-139">CLI hello kümeyle kullanılabilir hello önce yapılandırılmış toouse hello SSH tüneli olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-139">Before hello CLI can be used with hello cluster, it must be configured toouse hello SSH tunnel.</span></span> <span data-ttu-id="ee1e6-140">toodo, bu nedenle, aşağıdaki komut, başlangıç bağlantı noktası gerekiyorsa ayarlama hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-140">toodo so, run hello following command, adjusting hello port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="ee1e6-141">Bir uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="ee1e6-141">Run an application</span></span>

<span data-ttu-id="ee1e6-142">bir ACS DC/OS kümesi için mekanizma zamanlama hello Marathon varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-142">hello default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="ee1e6-143">Marathon kullanılan toostart bir uygulamasıdır ve Merhaba uygulaması hello DC/OS kümesinde hello durumunu yönetin.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-143">Marathon is used toostart an application and manage hello state of hello application on hello DC/OS cluster.</span></span> <span data-ttu-id="ee1e6-144">bir uygulama, Marathon aracılığıyla tooschedule adlı bir dosya oluşturmak *marathon app.json*, kopya hello izleyerek içeriği içine.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-144">tooschedule an application through Marathon, create a file named *marathon-app.json*, and copy hello following contents into it.</span></span> 

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

<span data-ttu-id="ee1e6-145">Komut tooschedule hello uygulama toorun hello DC/OS kümesinde aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-145">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="ee1e6-146">toosee hello dağıtım durumunu hello uygulama, komutu aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-146">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="ee1e6-147">Ne zaman hello **BEKLEYEN** sütun değeri geçer *True* çok*yanlış*, uygulama dağıtımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-147">When hello **WAITING** column value switches from *True* too*False*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

<span data-ttu-id="ee1e6-148">Merhaba DC/OS kümesi aracıları Hello genel IP adresi alın.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-148">Get hello public IP address of hello DC/OS cluster agents.</span></span>

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="ee1e6-149">Toothis adresi gözatma hello varsayılan NGINX site döndürür.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-149">Browsing toothis address returns hello default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a><span data-ttu-id="ee1e6-151">DC/OS kümesi Sil</span><span class="sxs-lookup"><span data-stu-id="ee1e6-151">Delete DC/OS cluster</span></span>

<span data-ttu-id="ee1e6-152">Artık gerektiğinde Merhaba kullanabilirsiniz [az grubu Sil](/cli/azure/group#delete) tooremove hello kaynak grubu, DC/OS kümesi ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-152">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="ee1e6-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ee1e6-153">Next steps</span></span>

<span data-ttu-id="ee1e6-154">Bu Hızlı Başlangıç, DC/OS kümesi dağıttıktan sonra ve basit bir Docker kapsayıcısı hello kümede çalışan.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-154">In this quick start, you’ve deployed a DC/OS cluster and have run a simple Docker container on hello cluster.</span></span> <span data-ttu-id="ee1e6-155">Azure kapsayıcı hizmeti hakkında daha fazla toolearn toohello ACS öğreticileri devam edin.</span><span class="sxs-lookup"><span data-stu-id="ee1e6-155">toolearn more about Azure Container Service, continue toohello ACS tutorials.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ee1e6-156">Bir ACS DC/OS kümesi yönetme</span><span class="sxs-lookup"><span data-stu-id="ee1e6-156">Manage an ACS DC/OS Cluster</span></span>](container-service-dcos-manage-tutorial.md)