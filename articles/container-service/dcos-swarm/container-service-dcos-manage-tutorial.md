---
title: "Azure kapsayıcı hizmeti Öğreticisi - DC/OS yönetme | Microsoft Docs"
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
ms.openlocfilehash: e93f782c26c32f97749e817ec59ee3c2ecb7e119
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a><span data-ttu-id="54171-104">Azure kapsayıcı hizmeti Öğreticisi - DC/OS yönetme</span><span class="sxs-lookup"><span data-stu-id="54171-104">Azure Container Service tutorial - Manage DC/OS</span></span>

<span data-ttu-id="54171-105">DC/OS çalışan modern ve kapsayıcılı uygulamaları için Dağıtılmış bir platform sağlar.</span><span class="sxs-lookup"><span data-stu-id="54171-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="54171-106">Azure kapsayıcı hizmeti ile basit ve hızlı bir üretim hazır DC/OS kümesi sağlama.</span><span class="sxs-lookup"><span data-stu-id="54171-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="54171-107">Bu hızlı başlangıç ayrıntıları için temel adımlar gerekli, DC/OS kümesi ve çalışma temel iş yükü dağıtın.</span><span class="sxs-lookup"><span data-stu-id="54171-107">This quick start details basic steps needed to deploy a DC/OS cluster and run basic workload.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="54171-108">Bir ACS DC/OS kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="54171-108">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="54171-109">Kümeye bağlanma</span><span class="sxs-lookup"><span data-stu-id="54171-109">Connect to the cluster</span></span>
> * <span data-ttu-id="54171-110">DC/OS CLI'yi yükleyin</span><span class="sxs-lookup"><span data-stu-id="54171-110">Install the DC/OS CLI</span></span>
> * <span data-ttu-id="54171-111">Bir uygulamayı kümeye dağıtma</span><span class="sxs-lookup"><span data-stu-id="54171-111">Deploy an application to the cluster</span></span>
> * <span data-ttu-id="54171-112">Kümede uygulama ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="54171-112">Scale an application on the cluster</span></span>
> * <span data-ttu-id="54171-113">DC/OS küme düğümleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="54171-113">Scale the DC/OS cluster nodes</span></span>
> * <span data-ttu-id="54171-114">Temel DC/OS Yönetimi</span><span class="sxs-lookup"><span data-stu-id="54171-114">Basic DC/OS management</span></span>
> * <span data-ttu-id="54171-115">DC/OS kümesi Sil</span><span class="sxs-lookup"><span data-stu-id="54171-115">Delete the DC/OS cluster</span></span>

<span data-ttu-id="54171-116">Bu öğretici, Azure CLI 2.0.4 veya sonraki bir sürümü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="54171-116">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="54171-117">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="54171-117">Run `az --version` to find the version.</span></span> <span data-ttu-id="54171-118">Yükseltme gerekiyorsa, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="54171-118">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-dcos-cluster"></a><span data-ttu-id="54171-119">DC/OS kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="54171-119">Create DC/OS cluster</span></span>

<span data-ttu-id="54171-120">İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="54171-120">First, create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="54171-121">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="54171-121">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="54171-122">Aşağıdaki örnek *westeurope* konumunda *myResourceGroup* adlı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="54171-122">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="54171-123">Ardından, DC/OS kümesi ile oluşturma [az acs oluşturmak](/cli/azure/acs#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="54171-123">Next, create a DC/OS cluster with the [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="54171-124">Aşağıdaki örnek, adlandırılmış bir DC/OS kümesi oluşturur *myDCOSCluster* ve zaten mevcut değilse SSH anahtarları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="54171-124">The following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="54171-125">Belirli bir anahtar kümesini kullanmak için `--ssh-key-value` seçeneğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="54171-125">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="54171-126">Birkaç dakika sonra komut tamamlandıktan ve dağıtım hakkında bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="54171-126">After several minutes, the command completes, and returns information about the deployment.</span></span>

## <a name="connect-to-dcos-cluster"></a><span data-ttu-id="54171-127">DC/OS kümesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="54171-127">Connect to DC/OS cluster</span></span>

<span data-ttu-id="54171-128">DC/OS kümesi oluşturulduktan sonra bir SSH tüneli üzerinden erişimleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="54171-128">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="54171-129">DC/OS asıl ortak IP adresini döndürmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="54171-129">Run the following command to return the public IP address of the DC/OS master.</span></span> <span data-ttu-id="54171-130">Bu IP adresi bir değişkende depolanan ve sonraki adımda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="54171-130">This IP address is stored in a variable and used in the next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="54171-131">SSH tüneli oluşturmak için aşağıdaki komutu çalıştırın ve izleyin ekrandaki yönergeleri.</span><span class="sxs-lookup"><span data-stu-id="54171-131">To create the SSH tunnel, run the following command and follow the on-screen instructions.</span></span> <span data-ttu-id="54171-132">Bağlantı noktası 80 kullanımda olduğundan komut başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="54171-132">If port 80 is already in use, the command fails.</span></span> <span data-ttu-id="54171-133">Tünel bağlantı noktası gibi bir içinde değil kullanımına güncelleştirme `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="54171-133">Update the tunneled port to one not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a><span data-ttu-id="54171-134">DC/OS CLI'yi yükleyin</span><span class="sxs-lookup"><span data-stu-id="54171-134">Install DC/OS CLI</span></span>

<span data-ttu-id="54171-135">DC/OS CLI kullanarak yükleme [az acs dcos yükleme-CLI](/azure/acs/dcos#install-cli) komutu.</span><span class="sxs-lookup"><span data-stu-id="54171-135">Install the DC/OS cli using the [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="54171-136">Azure CloudShell kullanıyorsanız, DC/OS CLI zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="54171-136">If you are using Azure CloudShell, the DC/OS CLI is already installed.</span></span> <span data-ttu-id="54171-137">Azure CLI macOS ya da Linux üzerinde çalıştırıyorsanız, sudo komutu çalıştırmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="54171-137">If you are running the Azure CLI on macOS or Linux, you might need to run the command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="54171-138">CLI kümeyle kullanılabilmesi için önce SSH tüneli kullanacak şekilde yapılandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="54171-138">Before the CLI can be used with the cluster, it must be configured to use the SSH tunnel.</span></span> <span data-ttu-id="54171-139">Bunu yapmak için bağlantı noktası gerekiyorsa ayarlayarak aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="54171-139">To do so, run the following command, adjusting the port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="54171-140">Bir uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="54171-140">Run an application</span></span>

<span data-ttu-id="54171-141">Bir ACS DC/OS kümesi için mekanizma zamanlama Marathon varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="54171-141">The default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="54171-142">Marathon, uygulama başlatma ve DC/OS kümesinde uygulama durumunu yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="54171-142">Marathon is used to start an application and manage the state of the application on the DC/OS cluster.</span></span> <span data-ttu-id="54171-143">Marathon aracılığıyla bir uygulama zamanlamak için adlı bir dosya oluşturun **marathon app.json**ve aşağıdaki içeriği buraya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="54171-143">To schedule an application through Marathon, create a file named **marathon-app.json**, and copy the following contents into it.</span></span> 

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

<span data-ttu-id="54171-144">Uygulamayı DC/OS kümesinde çalışacak şekilde zamanlamak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="54171-144">Run the following command to schedule the application to run on the DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="54171-145">Uygulama dağıtımı durumunu görmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="54171-145">To see the deployment status for the app, run the following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="54171-146">Zaman **görevleri** sütun değeri geçer *0/1* için *1/1*, uygulama dağıtımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="54171-146">When the **TASKS** column value switches from *0/1* to *1/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a><span data-ttu-id="54171-147">Marathon uygulamayı Ölçeklendir</span><span class="sxs-lookup"><span data-stu-id="54171-147">Scale Marathon application</span></span>

<span data-ttu-id="54171-148">Önceki örnekte, bir tek örnek uygulaması oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="54171-148">In the previous example, a single instance application was created.</span></span> <span data-ttu-id="54171-149">Uygulamanın üç örneğine kullanılabilir olacak şekilde, bu dağıtımı güncelleştirmek için açık **marathon app.json** dosya ve 3'e örnek özelliğini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="54171-149">To update this deployment so that three instances of the application are available, open up the **marathon-app.json** file, and update the instance property to 3.</span></span>

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

<span data-ttu-id="54171-150">Uygulamayı kullanarak güncelleştirme `dcos marathon app update` komutu.</span><span class="sxs-lookup"><span data-stu-id="54171-150">Update the application using the `dcos marathon app update` command.</span></span>

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

<span data-ttu-id="54171-151">Uygulama dağıtımı durumunu görmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="54171-151">To see the deployment status for the app, run the following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="54171-152">Zaman **görevleri** sütun değeri geçer *1/3* için *3/1*, uygulama dağıtımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="54171-152">When the **TASKS** column value switches from *1/3* to *3/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a><span data-ttu-id="54171-153">Internet erişilebilir uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="54171-153">Run internet accessible app</span></span>

<span data-ttu-id="54171-154">ACS DC/OS kümesi iki düğüm kümesi, internet üzerinde erişilebilir olan bir ortak ve internet'te erişilemeyen bir özel oluşur.</span><span class="sxs-lookup"><span data-stu-id="54171-154">The ACS DC/OS cluster consists of two node sets, one public which is accessible on the internet, and one private which is not accessible on the internet.</span></span> <span data-ttu-id="54171-155">Varsayılan, Son örnekte kullanılan özel düğümleri kümesidir.</span><span class="sxs-lookup"><span data-stu-id="54171-155">The default set is the private nodes, which was used in the last example.</span></span>

<span data-ttu-id="54171-156">Bir uygulama Internet üzerinden erişilebilir olması için ortak düğüm kümesi dağıtın.</span><span class="sxs-lookup"><span data-stu-id="54171-156">To make an application accessible on the internet, deploy them to the public node set.</span></span> <span data-ttu-id="54171-157">Bunu yapmak için vermek `acceptedResourceRoles` değerini nesne `slave_public`.</span><span class="sxs-lookup"><span data-stu-id="54171-157">To do so, give the `acceptedResourceRoles` object a value of `slave_public`.</span></span>

<span data-ttu-id="54171-158">Adlı bir dosya oluşturun **nginx public.json** ve aşağıdaki içeriği buraya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="54171-158">Create a file named **nginx-public.json** and copy the following contents into it.</span></span>

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

<span data-ttu-id="54171-159">Uygulamayı DC/OS kümesinde çalışacak şekilde zamanlamak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="54171-159">Run the following command to schedule the application to run on the DC/OS cluster.</span></span>

```azurecli 
dcos marathon app add nginx-public.json
```

<span data-ttu-id="54171-160">DC/OS ortak küme aracıların genel IP adresi alın.</span><span class="sxs-lookup"><span data-stu-id="54171-160">Get the public IP address of the DC/OS public cluster agents.</span></span>

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="54171-161">Bu adrese gözatma varsayılan NGINX site döndürür.</span><span class="sxs-lookup"><span data-stu-id="54171-161">Browsing to this address returns the default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a><span data-ttu-id="54171-163">Ölçek DC/OS kümesi</span><span class="sxs-lookup"><span data-stu-id="54171-163">Scale DC/OS cluster</span></span>

<span data-ttu-id="54171-164">Önceki örneklerde, bir uygulama için birden çok örneği ölçeklendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="54171-164">In the previous examples, an application was scaled to multiple instance.</span></span> <span data-ttu-id="54171-165">DC/OS altyapı da fazla veya az işlem kapasitesini sağlamak için genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="54171-165">The DC/OS infrastructure can also be scaled to provide more or less compute capacity.</span></span> <span data-ttu-id="54171-166">Bu gerçekleştirilir [az acs ölçeklendirme]() komutu.</span><span class="sxs-lookup"><span data-stu-id="54171-166">This is done with the [az acs scale]() command.</span></span> 

<span data-ttu-id="54171-167">DC/OS aracıları geçerli sayısını görmek için [acs az göster](/cli/azure/acs#show) komutu.</span><span class="sxs-lookup"><span data-stu-id="54171-167">To see the current count of DC/OS agents, use the [az acs show](/cli/azure/acs#show) command.</span></span>

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

<span data-ttu-id="54171-168">5 sayısını artırmak için [az acs ölçeklendirme](/cli/azure/acs#scale) komutu.</span><span class="sxs-lookup"><span data-stu-id="54171-168">To increase the count to 5, use the [az acs scale](/cli/azure/acs#scale) command.</span></span> 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a><span data-ttu-id="54171-169">DC/OS kümesi Sil</span><span class="sxs-lookup"><span data-stu-id="54171-169">Delete DC/OS cluster</span></span>

<span data-ttu-id="54171-170">Artık gerekli olduğunda, kullanabileceğiniz [az grubu Sil](/cli/azure/group#delete) kaynak grubu, DC/OS kümesi kaldırmak için komut ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="54171-170">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="54171-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="54171-171">Next steps</span></span>

<span data-ttu-id="54171-172">Bu öğreticide, aşağıdakiler de dahil olmak üzere temel DC/OS yönetim görevle ilgili öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="54171-172">In this tutorial, you have learned about basic DC/OS management task including the following.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="54171-173">Bir ACS DC/OS kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="54171-173">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="54171-174">Kümeye bağlanma</span><span class="sxs-lookup"><span data-stu-id="54171-174">Connect to the cluster</span></span>
> * <span data-ttu-id="54171-175">DC/OS CLI'yi yükleyin</span><span class="sxs-lookup"><span data-stu-id="54171-175">Install the DC/OS CLI</span></span>
> * <span data-ttu-id="54171-176">Bir uygulamayı kümeye dağıtma</span><span class="sxs-lookup"><span data-stu-id="54171-176">Deploy an application to the cluster</span></span>
> * <span data-ttu-id="54171-177">Kümede uygulama ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="54171-177">Scale an application on the cluster</span></span>
> * <span data-ttu-id="54171-178">DC/OS küme düğümleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="54171-178">Scale the DC/OS cluster nodes</span></span>
> * <span data-ttu-id="54171-179">DC/OS kümesi Sil</span><span class="sxs-lookup"><span data-stu-id="54171-179">Delete the DC/OS cluster</span></span>

<span data-ttu-id="54171-180">Yük Dengeleme DC/OS Azure ile ilgili uygulamada hakkında bilgi almak için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="54171-180">Advance to the next tutorial to learn about load balancing application in DC/OS on Azure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="54171-181">Uygulamalarda yük dengeleme gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="54171-181">Load balance applications</span></span>](container-service-load-balancing.md)