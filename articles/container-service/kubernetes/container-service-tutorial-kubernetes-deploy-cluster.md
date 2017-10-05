---
title: "Azure kapsayıcı hizmeti Öğreticisi - küme dağıtma | Microsoft Docs"
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
ms.openlocfilehash: 472697c1f0c18859087d7b448e1786d85c27aca0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="b79f5-104">Azure kapsayıcı Hizmeti'nde bir Kubernetes kümesini dağıtma</span><span class="sxs-lookup"><span data-stu-id="b79f5-104">Deploy a Kubernetes cluster in Azure Container Service</span></span>

<span data-ttu-id="b79f5-105">Kubernetes kapsayıcılı uygulamaları için Dağıtılmış bir platform sağlar.</span><span class="sxs-lookup"><span data-stu-id="b79f5-105">Kubernetes provides a distributed platform for containerized applications.</span></span> <span data-ttu-id="b79f5-106">Azure kapsayıcı hizmeti ile basit ve hızlı bir üretim hazır Kubernetes kümenin sağlama.</span><span class="sxs-lookup"><span data-stu-id="b79f5-106">With Azure Container Service, provisioning of a production ready Kubernetes cluster is simple and quick.</span></span> <span data-ttu-id="b79f5-107">Bu öğreticide, 7, 3 parçası Azure kapsayıcı hizmeti Kubernetes küme dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="b79f5-107">In this tutorial, part 3 of 7, an Azure Container Service Kubernetes cluster is deployed.</span></span> <span data-ttu-id="b79f5-108">Tamamlanan adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="b79f5-108">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b79f5-109">Kubernetes ACS kümesini dağıtma</span><span class="sxs-lookup"><span data-stu-id="b79f5-109">Deploying a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="b79f5-110">Kubernetes CLI (kubectl) yükleme</span><span class="sxs-lookup"><span data-stu-id="b79f5-110">Installation of the Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="b79f5-111">Kubectl yapılandırması</span><span class="sxs-lookup"><span data-stu-id="b79f5-111">Configuration of kubectl</span></span>

<span data-ttu-id="b79f5-112">Sonraki öğreticilerde, Azure oy uygulama olduğundan kümeye dağıtılan, ölçeği, güncelleştirilmiş ve Operations Management Suite Kubernetes küme izlemek için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="b79f5-112">In subsequent tutorials, the Azure Vote application is deployed to the cluster, scaled, updated, and Operations Management Suite is configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b79f5-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="b79f5-113">Before you begin</span></span>

<span data-ttu-id="b79f5-114">Önceki eğitimlerine bir kapsayıcı görüntüsü oluşturuldu ve Azure kapsayıcı kayıt defteri örneğine yüklenir.</span><span class="sxs-lookup"><span data-stu-id="b79f5-114">In previous tutorials, a container image was created and uploaded to an Azure Container Registry instance.</span></span> <span data-ttu-id="b79f5-115">Bu adımları yapmadıysanız ve izlemek istediğiniz, geri dönüp [Öğreticisi 1 – Oluştur kapsayıcı görüntüleri](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="b79f5-115">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span>

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="b79f5-116">Kubernetes kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b79f5-116">Create Kubernetes cluster</span></span>

<span data-ttu-id="b79f5-117">İçinde [önceki öğretici](./container-service-tutorial-kubernetes-prepare-acr.md), bir kaynak grubu *myResourceGroup* oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="b79f5-117">In the [previous tutorial](./container-service-tutorial-kubernetes-prepare-acr.md), a resource group named *myResourceGroup* was created.</span></span> <span data-ttu-id="b79f5-118">Bunu yapmadıysanız şimdi bu kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b79f5-118">If you have not done so, create this resource group now.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="b79f5-119">Azure Container Service'te [az acs create](/cli/azure/acs#create) komutuyla Kubernetes kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b79f5-119">Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="b79f5-120">Aşağıdaki örnekte, bir Linux ana düğümü ve üç Linux aracı düğümüyle *myK8sCluster* adlı bir küme oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="b79f5-120">The following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

<span data-ttu-id="b79f5-121">Birkaç dakika sonra komutu tamamlandıktan ve ACS dağıtımı hakkında bilgi döndürür json biçimli.</span><span class="sxs-lookup"><span data-stu-id="b79f5-121">After several minutes, the command completes, and returns json formatted information about the ACS deployment.</span></span>

## <a name="install-the-kubectl-cli"></a><span data-ttu-id="b79f5-122">CLI kubectl yükleyin</span><span class="sxs-lookup"><span data-stu-id="b79f5-122">Install the kubectl CLI</span></span>

<span data-ttu-id="b79f5-123">İstemci bilgisayarından Kubernetes kümeye bağlanmak için [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), Kubernetes komut satırı istemcisi.</span><span class="sxs-lookup"><span data-stu-id="b79f5-123">To connect to the Kubernetes cluster from your client computer, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span></span> 

<span data-ttu-id="b79f5-124">Azure CloudShell'i kullanıyorsanız `kubectl` zaten yüklüdür.</span><span class="sxs-lookup"><span data-stu-id="b79f5-124">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="b79f5-125">Yerel olarak yüklemek istiyorsanız, kullanmak [az acs kubernetes yükleme-CLI](/cli/azure/acs/kubernetes#install-cli) komutu.</span><span class="sxs-lookup"><span data-stu-id="b79f5-125">If you want to install it locally, use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="b79f5-126">Linux veya macOS çalıştırılıyorsa, sudo çalıştırmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="b79f5-126">If running in Linux or macOS, you may need to run with sudo.</span></span> <span data-ttu-id="b79f5-127">Windows üzerinde Kabuk yönetici olarak çalıştır emin olun.</span><span class="sxs-lookup"><span data-stu-id="b79f5-127">On Windows, ensure your shell has been run as administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli 
```

<span data-ttu-id="b79f5-128">Windows, varsayılan yüklemedir *c:\program files (x86)\kubectl.exe*.</span><span class="sxs-lookup"><span data-stu-id="b79f5-128">On Windows, the default installation is *c:\program files (x86)\kubectl.exe*.</span></span> <span data-ttu-id="b79f5-129">Bu dosyayı Windows yoluna eklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="b79f5-129">You may need to add this file to the Windows path.</span></span> 

## <a name="connect-with-kubectl"></a><span data-ttu-id="b79f5-130">kubectl ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="b79f5-130">Connect with kubectl</span></span>

<span data-ttu-id="b79f5-131">`kubectl` öğesini Kubernetes kümenize bağlanacak şekilde yapılandırmak için [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b79f5-131">To configure `kubectl` to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

<span data-ttu-id="b79f5-132">Kümenize bağlantıyı doğrulamak için Çalıştır [kubectl alma düğümleri](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) komutu.</span><span class="sxs-lookup"><span data-stu-id="b79f5-132">To verify the connection to your cluster, run the [kubectl get nodes](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="b79f5-133">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="b79f5-133">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

<span data-ttu-id="b79f5-134">Eğitmen tamamlandığında, bir ACS Kubernetes küme iş yükleri için hazır olması.</span><span class="sxs-lookup"><span data-stu-id="b79f5-134">At tutorial completion, you have an ACS Kubernetes cluster ready for workloads.</span></span> <span data-ttu-id="b79f5-135">Sonraki öğreticilerde, bir çok kapsayıcı uygulama bu kümeye dağıtılan, çıkışı ölçeği, güncelleştirilmiş ve izlenen.</span><span class="sxs-lookup"><span data-stu-id="b79f5-135">In subsequent tutorials, a multi-container application is deployed to this cluster, scaled out, updated, and monitored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b79f5-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b79f5-136">Next steps</span></span>

<span data-ttu-id="b79f5-137">Bu öğreticide, Azure kapsayıcı hizmeti Kubernetes küme dağıtıldı.</span><span class="sxs-lookup"><span data-stu-id="b79f5-137">In this tutorial, an Azure Container Service Kubernetes cluster was deployed.</span></span> <span data-ttu-id="b79f5-138">Aşağıdaki adımlar tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="b79f5-138">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b79f5-139">Bir Kubernetes ACS kümesi dağıtılmış</span><span class="sxs-lookup"><span data-stu-id="b79f5-139">Deployed a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="b79f5-140">Kubernetes CLI (kubectl) yüklü</span><span class="sxs-lookup"><span data-stu-id="b79f5-140">Installed the Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="b79f5-141">Yapılandırılmış kubectl</span><span class="sxs-lookup"><span data-stu-id="b79f5-141">Configured kubectl</span></span>

<span data-ttu-id="b79f5-142">Uygulama küme üzerinde çalışan hakkında bilgi edinmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="b79f5-142">Advance to the next tutorial to learn about running application on the cluster.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b79f5-143">Kubernetes uygulamasında dağıtma</span><span class="sxs-lookup"><span data-stu-id="b79f5-143">Deploy application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-deploy-application.md)
