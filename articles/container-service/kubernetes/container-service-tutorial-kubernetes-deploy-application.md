---
title: "aaaAzure kapsayıcı hizmeti Öğreticisi - uygulama dağıtma | Microsoft Docs"
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
ms.openlocfilehash: 7e2fa06d359caf83e684df3966624a6e9a8e7efa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-applications-in-kubernetes"></a><span data-ttu-id="6b8d4-104">Kubernetes çalışma uygulamaları</span><span class="sxs-lookup"><span data-stu-id="6b8d4-104">Run applications in Kubernetes</span></span>

<span data-ttu-id="6b8d4-105">Bu öğreticide yedi dördünü kısım, örnek bir uygulama Kubernetes kümesine dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-105">In this tutorial, part four of seven, a sample application is deployed into a Kubernetes cluster.</span></span> <span data-ttu-id="6b8d4-106">Tamamlanan adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="6b8d4-106">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6b8d4-107">Kubernetes bildirim dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="6b8d4-107">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="6b8d4-108">Kubernetes Çalıştırma uygulaması</span><span class="sxs-lookup"><span data-stu-id="6b8d4-108">Run application in Kubernetes</span></span>
> * <span data-ttu-id="6b8d4-109">Merhaba uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="6b8d4-109">Test hello application</span></span>

<span data-ttu-id="6b8d4-110">Sonraki öğreticilerde, bu uygulama, güncelleştirilmiş, ölçeklenir ve Operations Management Suite toomonitor hello Kubernetes küme yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-110">In subsequent tutorials, this application is scaled out, updated, and Operations Management Suite configured toomonitor hello Kubernetes cluster.</span></span>

<span data-ttu-id="6b8d4-111">Bu öğretici Kubernetes kavramları temel bir anlayış varsayar, hello Kubernetes hakkında ayrıntılı bilgi için bkz: [Kubernetes belgelerine](https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="6b8d4-111">This tutorial assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see hello [Kubernetes documentation](https://kubernetes.io/docs/home/).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6b8d4-112">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="6b8d4-112">Before you begin</span></span>

<span data-ttu-id="6b8d4-113">Önceki öğreticileri, bir uygulama bir kapsayıcı görüntüsüne paketlenmiş ve bu görüntüyü karşıya yüklenen tooAzure kapsayıcı kayıt defteri edildi Kubernetes küme oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-113">In previous tutorials, an application was packaged into a container image, this image was uploaded tooAzure Container Registry, and a Kubernetes cluster was created.</span></span> <span data-ttu-id="6b8d4-114">Bu adımları yapmadıysanız ve boyunca toofollow istersiniz, çok dönmek[Öğreticisi 1 – Oluştur kapsayıcı görüntüleri](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="6b8d4-114">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="6b8d4-115">En azından, Bu öğretici Kubernetes kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-115">At minimum, this tutorial requires a Kubernetes cluster.</span></span>

## <a name="get-manifest-file"></a><span data-ttu-id="6b8d4-116">Bildirim dosyası al</span><span class="sxs-lookup"><span data-stu-id="6b8d4-116">Get manifest file</span></span>

<span data-ttu-id="6b8d4-117">Bu öğretici için [Kubernetes nesneleri](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) Kubernetes bildirimi kullanılarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-117">For this tutorial, [Kubernetes objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) are deployed using a Kubernetes manifest.</span></span> <span data-ttu-id="6b8d4-118">Kubernetes bildirim Kubernetes nesne dağıtım ve yapılandırma yönergeleri içeren bir YAML veya JSON biçimli dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-118">A Kubernetes manifest is a YAML or JSON formatted file containing Kubernetes object deployment and configuration instructions.</span></span>

<span data-ttu-id="6b8d4-119">önceki bir öğreticide kopyalandı hello Azure oy uygulama depodaki Hello uygulama bildirim dosyasının Bu öğretici için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-119">hello application manifest file for this tutorial is available in hello Azure Vote application repo, which was cloned in a previous tutorial.</span></span> <span data-ttu-id="6b8d4-120">Zaten yapmadıysanız, komutu aşağıdaki hello ile Merhaba depoyu kopyalama:</span><span class="sxs-lookup"><span data-stu-id="6b8d4-120">If you have not already done so, clone hello repo with hello following command:</span></span> 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="6b8d4-121">kopyalanmış hello deposu dizinini aşağıdaki hello Hello bildirim dosyası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-121">hello manifest file is found in hello following directory of hello cloned repo.</span></span>

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a><span data-ttu-id="6b8d4-122">Güncelleştirme bildirim dosyası</span><span class="sxs-lookup"><span data-stu-id="6b8d4-122">Update manifest file</span></span>

<span data-ttu-id="6b8d4-123">Azure kapsayıcı kayıt defteri toostore hello kapsayıcı görüntüleri kullanıyorsanız, hello bildirim gereksinimlerini toobe ACR loginServer adı ile Merhaba güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-123">If using Azure Container Registry toostore hello container images, hello manifest needs toobe updated with hello ACR loginServer name.</span></span>

<span data-ttu-id="6b8d4-124">Merhaba ACR oturum açma sunucu hello adıyla alma [az acr listesi](/cli/azure/acr#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-124">Get hello ACR login server name with hello [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="6b8d4-125">Merhaba örnek bildirimi bir havuz adı ile önceden oluşturulmuş *microsoft*.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-125">hello sample manifest has been pre-created with a repository name of *microsoft*.</span></span> <span data-ttu-id="6b8d4-126">Merhaba dosya ile herhangi bir metin düzenleyicisinde açın ve hello değiştirin *microsoft* hello oturum açma sunucusu adlı ACR örneğinin değeri.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-126">Open hello file with any text editor, and replace hello *microsoft* value with hello login server name of your ACR instance.</span></span>

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a><span data-ttu-id="6b8d4-127">Uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="6b8d4-127">Deploy application</span></span>

<span data-ttu-id="6b8d4-128">Kullanım hello [kubectl oluşturma](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) toorun Merhaba uygulaması komutu.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-128">Use hello [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command toorun hello application.</span></span> <span data-ttu-id="6b8d4-129">Bu komut ayrıştırıyor hello bildirim dosyası ve tanımlanan hello Kubernetes nesneleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-129">This command parses hello manifest file and create hello defined Kubernetes objects.</span></span>

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

<span data-ttu-id="6b8d4-130">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="6b8d4-130">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a><span data-ttu-id="6b8d4-131">Uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="6b8d4-131">Test application</span></span>

<span data-ttu-id="6b8d4-132">A [Kubernetes hizmet](https://kubernetes.io/docs/concepts/services-networking/service/) hangi hello uygulama toohello sunan oluşturulan Internet.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-132">A [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created which exposes hello application toohello internet.</span></span> <span data-ttu-id="6b8d4-133">Bu işlem birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-133">This process can take a few minutes.</span></span> 

<span data-ttu-id="6b8d4-134">toomonitor ilerleme, kullanım hello [kubectl alma hizmeti](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) hello komutunu `--watch` bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-134">toomonitor progress, use hello [kubectl get service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) command with hello `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="6b8d4-135">Başlangıçta, hello **dış IP** hello için *azure oy ön* hizmeti görünür olarak *bekleyen*.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-135">Initially, hello **EXTERNAL-IP** for hello *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="6b8d4-136">Merhaba dış IP adresi değiştiğinden sonra *bekleyen* tooan *IP adresi*, kullanın `CTRL-C` toostop hello kubectl izleme işlemi.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-136">Once hello EXTERNAL-IP address has changed from *pending* tooan *IP address*, use `CTRL-C` toostop hello kubectl watch process.</span></span>

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

<span data-ttu-id="6b8d4-137">toosee Merhaba uygulaması, Gözat toohello dış IP adresi.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-137">toosee hello application, browse toohello external IP address.</span></span>

![Azure’da Kubernetes kümesinin görüntüsü](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a><span data-ttu-id="6b8d4-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6b8d4-139">Next steps</span></span>

<span data-ttu-id="6b8d4-140">Bu öğreticide, dağıtılan tooan Azure kapsayıcı hizmeti Kubernetes küme hello Azure oy uygulama oluştu.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-140">In this tutorial, hello Azure vote application was deployed tooan Azure Container Service Kubernetes cluster.</span></span> <span data-ttu-id="6b8d4-141">Tamamlanan görevler aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="6b8d4-141">Tasks completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="6b8d4-142">Kubernetes bildirim dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="6b8d4-142">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="6b8d4-143">İçinde Kubernetes Hello uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="6b8d4-143">Run hello application in Kubernetes</span></span>
> * <span data-ttu-id="6b8d4-144">Sınanan Merhaba uygulaması</span><span class="sxs-lookup"><span data-stu-id="6b8d4-144">Tested hello application</span></span>

<span data-ttu-id="6b8d4-145">Bir Kubernetes uygulama ve Kubernetes altyapısını temel hello ölçeklendirme hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="6b8d4-145">Advance toohello next tutorial toolearn about scaling both a Kubernetes application and hello underlying Kubernetes infrastructure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="6b8d4-146">Ölçek Kubernetes uygulama ve altyapı</span><span class="sxs-lookup"><span data-stu-id="6b8d4-146">Scale Kubernetes application and infrastructure</span></span>](./container-service-tutorial-kubernetes-scale.md)