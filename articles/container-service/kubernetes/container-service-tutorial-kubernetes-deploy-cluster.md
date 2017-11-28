---
title: "aaaAzure kapsayıcı hizmeti Öğreticisi - küme dağıtma | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Öğreticisi - küme dağıtma"
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
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c4c8cc95c88d9c2077d0322f57e5d3159e2dd0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="ee3a2-104">Azure kapsayıcı Hizmeti'nde bir Kubernetes kümesini dağıtma</span><span class="sxs-lookup"><span data-stu-id="ee3a2-104">Deploy a Kubernetes cluster in Azure Container Service</span></span>

<span data-ttu-id="ee3a2-105">Kubernetes kapsayıcılı uygulamaları için Dağıtılmış bir platform sağlar.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-105">Kubernetes provides a distributed platform for containerized applications.</span></span> <span data-ttu-id="ee3a2-106">Azure kapsayıcı hizmeti ile basit ve hızlı bir üretim hazır Kubernetes kümenin sağlama.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-106">With Azure Container Service, provisioning of a production ready Kubernetes cluster is simple and quick.</span></span> <span data-ttu-id="ee3a2-107">Bu öğreticide, 7, 3 parçası Azure kapsayıcı hizmeti Kubernetes küme dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-107">In this tutorial, part 3 of 7, an Azure Container Service Kubernetes cluster is deployed.</span></span> <span data-ttu-id="ee3a2-108">Tamamlanan adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="ee3a2-108">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ee3a2-109">Kubernetes ACS kümesini dağıtma</span><span class="sxs-lookup"><span data-stu-id="ee3a2-109">Deploying a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="ee3a2-110">Merhaba Kubernetes CLI (kubectl) yükleme</span><span class="sxs-lookup"><span data-stu-id="ee3a2-110">Installation of hello Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="ee3a2-111">Kubectl yapılandırması</span><span class="sxs-lookup"><span data-stu-id="ee3a2-111">Configuration of kubectl</span></span>

<span data-ttu-id="ee3a2-112">Sonraki öğreticilerde, Azure uygulama oy toohello küme, ölçeği, dağıtılan hello güncelleştirildi ve Operations Management Suite yapılandırılmış toomonitor hello Kubernetes kümedir.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-112">In subsequent tutorials, hello Azure Vote application is deployed toohello cluster, scaled, updated, and Operations Management Suite is configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ee3a2-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="ee3a2-113">Before you begin</span></span>

<span data-ttu-id="ee3a2-114">Önceki öğreticileri, bir kapsayıcı görüntüsü oluşturuldu ve tooan Azure kapsayıcı kayıt defteri örneği karşıya.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-114">In previous tutorials, a container image was created and uploaded tooan Azure Container Registry instance.</span></span> <span data-ttu-id="ee3a2-115">Bu adımları yapmadıysanız ve boyunca toofollow istersiniz, çok dönmek[Öğreticisi 1 – Oluştur kapsayıcı görüntüleri](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="ee3a2-115">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span>

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="ee3a2-116">Kubernetes kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ee3a2-116">Create Kubernetes cluster</span></span>

<span data-ttu-id="ee3a2-117">Merhaba, [önceki öğretici](./container-service-tutorial-kubernetes-prepare-acr.md), bir kaynak grubu *myResourceGroup* oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-117">In hello [previous tutorial](./container-service-tutorial-kubernetes-prepare-acr.md), a resource group named *myResourceGroup* was created.</span></span> <span data-ttu-id="ee3a2-118">Bunu yapmadıysanız şimdi bu kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-118">If you have not done so, create this resource group now.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="ee3a2-119">Kubernetes küme Azure kapsayıcı hizmeti ile Merhaba oluşturmak [az acs oluşturmak](/cli/azure/acs#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-119">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="ee3a2-120">Merhaba aşağıdaki örnek adlı bir küme oluşturur *myK8sCluster* ile bir Linux ana düğümü ve üç Linux Aracısı düğümleri.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-120">hello following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

<span data-ttu-id="ee3a2-121">Birkaç dakika sonra hello komutu tamamlandıktan ve hello ACS dağıtımı hakkında bilgi döndürür json biçimli.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-121">After several minutes, hello command completes, and returns json formatted information about hello ACS deployment.</span></span>

## <a name="install-hello-kubectl-cli"></a><span data-ttu-id="ee3a2-122">Merhaba kubectl CLI yükleme</span><span class="sxs-lookup"><span data-stu-id="ee3a2-122">Install hello kubectl CLI</span></span>

<span data-ttu-id="ee3a2-123">tooconnect toohello Kubernetes küme kullanımı, istemci bilgisayardan [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes komut satırı istemcisi.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-123">tooconnect toohello Kubernetes cluster from your client computer, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="ee3a2-124">Azure CloudShell'i kullanıyorsanız `kubectl` zaten yüklüdür.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-124">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="ee3a2-125">Tooinstall istiyorsanız hello yerel olarak kullanmak [az acs kubernetes yükleme-CLI](/cli/azure/acs/kubernetes#install-cli) komutu.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-125">If you want tooinstall it locally, use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="ee3a2-126">Linux veya macOS çalıştırılıyorsa, sudo ile toorun gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-126">If running in Linux or macOS, you may need toorun with sudo.</span></span> <span data-ttu-id="ee3a2-127">Windows üzerinde Kabuk yönetici olarak çalıştır emin olun.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-127">On Windows, ensure your shell has been run as administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli 
```

<span data-ttu-id="ee3a2-128">Windows hello varsayılan yüklemedir *c:\program files (x86)\kubectl.exe*.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-128">On Windows, hello default installation is *c:\program files (x86)\kubectl.exe*.</span></span> <span data-ttu-id="ee3a2-129">Bu dosya toohello Windows yolu tooadd gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-129">You may need tooadd this file toohello Windows path.</span></span> 

## <a name="connect-with-kubectl"></a><span data-ttu-id="ee3a2-130">kubectl ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="ee3a2-130">Connect with kubectl</span></span>

<span data-ttu-id="ee3a2-131">tooconfigure `kubectl` tooconnect tooyour Kubernetes küme hello çalıştırmak, [az acs kubernetes get-kimlik](/cli/azure/acs/kubernetes#get-credentials) komutu.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-131">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

<span data-ttu-id="ee3a2-132">Merhaba çalıştırmak tooverify hello bağlantı tooyour küme, [kubectl alma düğümleri](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) komutu.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-132">tooverify hello connection tooyour cluster, run hello [kubectl get nodes](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="ee3a2-133">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="ee3a2-133">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

<span data-ttu-id="ee3a2-134">Eğitmen tamamlandığında, bir ACS Kubernetes küme iş yükleri için hazır olması.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-134">At tutorial completion, you have an ACS Kubernetes cluster ready for workloads.</span></span> <span data-ttu-id="ee3a2-135">Sonraki öğreticilerde, birden çok kapsayıcı uygulama çıkışı ölçeği, güncelleştirilmiş ve izlenen dağıtılan toothis kümesidir.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-135">In subsequent tutorials, a multi-container application is deployed toothis cluster, scaled out, updated, and monitored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee3a2-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ee3a2-136">Next steps</span></span>

<span data-ttu-id="ee3a2-137">Bu öğreticide, Azure kapsayıcı hizmeti Kubernetes küme dağıtıldı.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-137">In this tutorial, an Azure Container Service Kubernetes cluster was deployed.</span></span> <span data-ttu-id="ee3a2-138">Aşağıdaki adımları hello tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="ee3a2-138">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ee3a2-139">Bir Kubernetes ACS kümesi dağıtılmış</span><span class="sxs-lookup"><span data-stu-id="ee3a2-139">Deployed a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="ee3a2-140">Yüklü hello Kubernetes CLI (kubectl)</span><span class="sxs-lookup"><span data-stu-id="ee3a2-140">Installed hello Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="ee3a2-141">Yapılandırılmış kubectl</span><span class="sxs-lookup"><span data-stu-id="ee3a2-141">Configured kubectl</span></span>

<span data-ttu-id="ee3a2-142">Uygulama hello kümede çalışan hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-142">Advance toohello next tutorial toolearn about running application on hello cluster.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ee3a2-143">Kubernetes uygulamasında dağıtma</span><span class="sxs-lookup"><span data-stu-id="ee3a2-143">Deploy application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-deploy-application.md)
