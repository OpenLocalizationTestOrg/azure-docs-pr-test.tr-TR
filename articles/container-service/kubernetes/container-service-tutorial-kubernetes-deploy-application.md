---
title: "Azure kapsayıcı hizmeti Öğreticisi - uygulama dağıtma | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Öğreticisi - uygulama dağıtma"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Container’lar, Mikro hizmetler, Kumernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ea67f0beb6a5926393b26e7590302ad0f46a63f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="run-applications-in-kubernetes"></a><span data-ttu-id="3d181-104">Kubernetes çalışma uygulamaları</span><span class="sxs-lookup"><span data-stu-id="3d181-104">Run applications in Kubernetes</span></span>

<span data-ttu-id="3d181-105">Bu öğreticide yedi dördünü kısım, örnek bir uygulama Kubernetes kümesine dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="3d181-105">In this tutorial, part four of seven, a sample application is deployed into a Kubernetes cluster.</span></span> <span data-ttu-id="3d181-106">Tamamlanan adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="3d181-106">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3d181-107">Kubernetes bildirim dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="3d181-107">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="3d181-108">Kubernetes Çalıştırma uygulaması</span><span class="sxs-lookup"><span data-stu-id="3d181-108">Run application in Kubernetes</span></span>
> * <span data-ttu-id="3d181-109">Uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="3d181-109">Test the application</span></span>

<span data-ttu-id="3d181-110">Sonraki öğreticilerde, bu uygulama, güncelleştirilmiş, ölçeklenir ve Kubernetes küme izlemek için Operations Management Suite yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="3d181-110">In subsequent tutorials, this application is scaled out, updated, and Operations Management Suite configured to monitor the Kubernetes cluster.</span></span>

<span data-ttu-id="3d181-111">Bu öğretici Kubernetes kavramlar, Kubernetes bakın hakkında ayrıntılı bilgi için temel bir anlayış varsayar [Kubernetes belgelerine](https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="3d181-111">This tutorial assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see the [Kubernetes documentation](https://kubernetes.io/docs/home/).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3d181-112">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="3d181-112">Before you begin</span></span>

<span data-ttu-id="3d181-113">Önceki öğreticileri, bir uygulama bir kapsayıcı görüntüsüne paketlenmiş ve bu görüntüyü Azure kapsayıcı kayıt defterine karşıya Kubernetes küme oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="3d181-113">In previous tutorials, an application was packaged into a container image, this image was uploaded to Azure Container Registry, and a Kubernetes cluster was created.</span></span> <span data-ttu-id="3d181-114">Bu adımları yapmadıysanız ve izlemek istediğiniz, geri dönüp [Öğreticisi 1 – Oluştur kapsayıcı görüntüleri](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="3d181-114">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="3d181-115">En azından, Bu öğretici Kubernetes kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3d181-115">At minimum, this tutorial requires a Kubernetes cluster.</span></span>

## <a name="get-manifest-file"></a><span data-ttu-id="3d181-116">Bildirim dosyası al</span><span class="sxs-lookup"><span data-stu-id="3d181-116">Get manifest file</span></span>

<span data-ttu-id="3d181-117">Bu öğretici için [Kubernetes nesneleri](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) Kubernetes bildirimi kullanılarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="3d181-117">For this tutorial, [Kubernetes objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) are deployed using a Kubernetes manifest.</span></span> <span data-ttu-id="3d181-118">Kubernetes bildirim Kubernetes nesne dağıtım ve yapılandırma yönergeleri içeren bir YAML veya JSON biçimli dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="3d181-118">A Kubernetes manifest is a YAML or JSON formatted file containing Kubernetes object deployment and configuration instructions.</span></span>

<span data-ttu-id="3d181-119">Bu öğretici için uygulama bildirim dosyasının önceki öğreticide kopyalandı Azure oy uygulama depodaki kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3d181-119">The application manifest file for this tutorial is available in the Azure Vote application repo, which was cloned in a previous tutorial.</span></span> <span data-ttu-id="3d181-120">Zaten yapmadıysanız, aşağıdaki komutla depoyu kopyalama:</span><span class="sxs-lookup"><span data-stu-id="3d181-120">If you have not already done so, clone the repo with the following command:</span></span> 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="3d181-121">Bildirim dosyası kopyalanan depoyu şu dizinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="3d181-121">The manifest file is found in the following directory of the cloned repo.</span></span>

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a><span data-ttu-id="3d181-122">Güncelleştirme bildirim dosyası</span><span class="sxs-lookup"><span data-stu-id="3d181-122">Update manifest file</span></span>

<span data-ttu-id="3d181-123">Azure kapsayıcı kayıt defteri kapsayıcı görüntüleri depolamak için kullanıyorsanız, bildirim ACR loginServer adıyla güncelleştirilmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="3d181-123">If using Azure Container Registry to store the container images, the manifest needs to be updated with the ACR loginServer name.</span></span>

<span data-ttu-id="3d181-124">ACR oturum açma sunucu adıyla alma [az acr listesi](/cli/azure/acr#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="3d181-124">Get the ACR login server name with the [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="3d181-125">Örnek bildirimi bir havuz adı ile önceden oluşturulmuş *microsoft*.</span><span class="sxs-lookup"><span data-stu-id="3d181-125">The sample manifest has been pre-created with a repository name of *microsoft*.</span></span> <span data-ttu-id="3d181-126">Dosyayı ile herhangi bir metin düzenleyicisinde açın ve değiştirme *microsoft* ACR örneğinizi oturum açma sunucu adı değeri.</span><span class="sxs-lookup"><span data-stu-id="3d181-126">Open the file with any text editor, and replace the *microsoft* value with the login server name of your ACR instance.</span></span>

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a><span data-ttu-id="3d181-127">Uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="3d181-127">Deploy application</span></span>

<span data-ttu-id="3d181-128">Uygulamayı çalıştırmak için [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="3d181-128">Use the [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command to run the application.</span></span> <span data-ttu-id="3d181-129">Bu komut, bildirim dosyası ayrıştırır ve tanımlanmış Kubernetes nesneleri oluşturma.</span><span class="sxs-lookup"><span data-stu-id="3d181-129">This command parses the manifest file and create the defined Kubernetes objects.</span></span>

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

<span data-ttu-id="3d181-130">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="3d181-130">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a><span data-ttu-id="3d181-131">Uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="3d181-131">Test application</span></span>

<span data-ttu-id="3d181-132">A [Kubernetes hizmet](https://kubernetes.io/docs/concepts/services-networking/service/) hangi uygulamanın Internet'e gösterir oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3d181-132">A [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created which exposes the application to the internet.</span></span> <span data-ttu-id="3d181-133">Bu işlem birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="3d181-133">This process can take a few minutes.</span></span> 

<span data-ttu-id="3d181-134">İlerleme durumunu izlemek için [kubectl get service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) komutunu `--watch` bağımsız değişkeniyle birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="3d181-134">To monitor progress, use the [kubectl get service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) command with the `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="3d181-135">Başlangıçta, **dış IP** için *azure oy ön* hizmeti görünür olarak *bekleyen*.</span><span class="sxs-lookup"><span data-stu-id="3d181-135">Initially, the **EXTERNAL-IP** for the *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="3d181-136">EXTERNAL-IP adresi *pending* durumundan *IP address* değerine değiştiğinde kubectl izleme işlemini durdurmak için `CTRL-C` komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="3d181-136">Once the EXTERNAL-IP address has changed from *pending* to an *IP address*, use `CTRL-C` to stop the kubectl watch process.</span></span>

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

<span data-ttu-id="3d181-137">Uygulama görmek için dış IP adresine göz atın.</span><span class="sxs-lookup"><span data-stu-id="3d181-137">To see the application, browse to the external IP address.</span></span>

![Azure’da Kubernetes kümesinin görüntüsü](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a><span data-ttu-id="3d181-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3d181-139">Next steps</span></span>

<span data-ttu-id="3d181-140">Bu öğreticide, Azure oy uygulama için bir Azure kapsayıcı hizmeti Kubernetes kümesi dağıtıldı.</span><span class="sxs-lookup"><span data-stu-id="3d181-140">In this tutorial, the Azure vote application was deployed to an Azure Container Service Kubernetes cluster.</span></span> <span data-ttu-id="3d181-141">Tamamlanan görevler aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="3d181-141">Tasks completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="3d181-142">Kubernetes bildirim dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="3d181-142">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="3d181-143">İçinde Kubernetes uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="3d181-143">Run the application in Kubernetes</span></span>
> * <span data-ttu-id="3d181-144">Uygulamayı test</span><span class="sxs-lookup"><span data-stu-id="3d181-144">Tested the application</span></span>

<span data-ttu-id="3d181-145">Kubernetes uygulama ve Kubernetes altyapının ölçeklendirme hakkında bilgi edinmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="3d181-145">Advance to the next tutorial to learn about scaling both a Kubernetes application and the underlying Kubernetes infrastructure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="3d181-146">Ölçek Kubernetes uygulama ve altyapı</span><span class="sxs-lookup"><span data-stu-id="3d181-146">Scale Kubernetes application and infrastructure</span></span>](./container-service-tutorial-kubernetes-scale.md)