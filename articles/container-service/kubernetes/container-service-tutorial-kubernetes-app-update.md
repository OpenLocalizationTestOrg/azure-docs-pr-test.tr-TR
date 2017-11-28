---
title: "aaaAzure kapsayıcı hizmeti Öğreticisi - güncelleştirme uygulaması | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Öğreticisi - güncelleştirme uygulaması"
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
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c467498bab7952926a18e45ffbb21051a98739d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="update-an-application-in-kubernetes"></a><span data-ttu-id="ca996-104">Bir uygulamada Kubernetes güncelleştir</span><span class="sxs-lookup"><span data-stu-id="ca996-104">Update an application in Kubernetes</span></span>

<span data-ttu-id="ca996-105">Bir uygulamada Kubernetes dağıttıktan sonra yeni kapsayıcı resim veya görüntü sürümü belirterek güncelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="ca996-105">After you deploy an application in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="ca996-106">Bir uygulama'ı güncelleştirdiğinizde hello güncelleştirme dağıtımının hello dağıtım yalnızca bir kısmını eşzamanlı olarak güncelleştirilebilmesi için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="ca996-106">When you update an application, hello update rollout is staged so that only a portion of hello deployment is concurrently updated.</span></span> <span data-ttu-id="ca996-107">Hazırlanan bu güncelleştirmeyi hello güncelleştirme sırasında çalışan hello uygulama tookeep sağlar ve bir dağıtım hatası oluşursa, bir geri alma mekanizması sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca996-107">This staged update enables hello application tookeep running during hello update, and provides a rollback mechanism if a deployment failure occurs.</span></span> 

<span data-ttu-id="ca996-108">Bu öğreticide, yedi, hello örnek Azure oylama uygulaması altı parçası güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ca996-108">In this tutorial, part six of seven, hello sample Azure Vote app is updated.</span></span> <span data-ttu-id="ca996-109">Tamamlamanız görevler aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="ca996-109">Tasks that you complete include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ca996-110">Merhaba ön uç uygulamasındaki kod güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="ca996-110">Updating hello front-end application code</span></span>
> * <span data-ttu-id="ca996-111">Güncelleştirilmiş kapsayıcı görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="ca996-111">Creating an updated container image</span></span>
> * <span data-ttu-id="ca996-112">Koymadan hello kapsayıcı görüntü tooAzure kapsayıcı kayıt defteri</span><span class="sxs-lookup"><span data-stu-id="ca996-112">Pushing hello container image tooAzure Container Registry</span></span>
> * <span data-ttu-id="ca996-113">Merhaba güncelleştirilmiş kapsayıcı görüntü dağıtma</span><span class="sxs-lookup"><span data-stu-id="ca996-113">Deploying hello updated container image</span></span>

<span data-ttu-id="ca996-114">Sonraki öğreticilerde Operations Management Suite yapılandırılmış toomonitor hello Kubernetes kümedir.</span><span class="sxs-lookup"><span data-stu-id="ca996-114">In subsequent tutorials, Operations Management Suite is configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ca996-115">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="ca996-115">Before you begin</span></span>

<span data-ttu-id="ca996-116">Önceki öğreticileri, bir uygulama bir kapsayıcı görüntüsüne paketlenmiş, tooAzure kapsayıcı kayıt defteri ve oluşturulan Kubernetes küme hello görüntüyü karşıya.</span><span class="sxs-lookup"><span data-stu-id="ca996-116">In previous tutorials, an application was packaged into a container image, hello image uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="ca996-117">Merhaba uygulaması sonra hello Kubernetes kümede çalıştırıldı.</span><span class="sxs-lookup"><span data-stu-id="ca996-117">hello application was then run on hello Kubernetes cluster.</span></span> 

<span data-ttu-id="ca996-118">Bu adımları tamamladıysanız henüz ve boyunca toofollow istediğiniz çok dönmek[Öğreticisi 1 – Oluştur kapsayıcı görüntüleri](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="ca996-118">If you haven't completed these steps, and want toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-application"></a><span data-ttu-id="ca996-119">Uygulamayı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="ca996-119">Update application</span></span>

<span data-ttu-id="ca996-120">toocomplete hello adımları Bu öğreticide, hello Azure oy uygulama kopyasını kopyalanmış gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca996-120">toocomplete hello steps in this tutorial, you must have cloned a copy of hello Azure Vote application.</span></span> <span data-ttu-id="ca996-121">Gerekirse, kopyalanan bu kopya komut aşağıdaki hello ile oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ca996-121">If necessary, create this cloned copy with hello following command:</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="ca996-122">Açık hello `config_file.cfg` herhangi bir kod ya da metin düzenleyicisi ile dosya.</span><span class="sxs-lookup"><span data-stu-id="ca996-122">Open hello `config_file.cfg` file with any code or text editor.</span></span> <span data-ttu-id="ca996-123">Bu dosyayı klonlanmış hello deposu dizinini aşağıdaki hello altında bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca996-123">You can find this file under hello following directory of hello cloned repo.</span></span>

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="ca996-124">Değiştirmek için hello değerleri `VOTE1VALUE` ve `VOTE2VALUE`ve hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ca996-124">Change hello values for `VOTE1VALUE` and `VOTE2VALUE`, and then save hello file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="ca996-125">Kullanım [docker compose'u](https://docs.docker.com/compose/) toore-hello ön uç görüntü ve güncelleştirilmiş çalışma Merhaba uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ca996-125">Use [docker-compose](https://docs.docker.com/compose/) toore-create hello front-end image and run hello updated application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a><span data-ttu-id="ca996-126">Uygulamayı yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="ca996-126">Test application locally</span></span>

<span data-ttu-id="ca996-127">Çok Gözat`http://localhost:8080` toosee hello uygulama güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="ca996-127">Browse too`http://localhost:8080` toosee hello updated application.</span></span>

![Azure’da Kubernetes kümesinin görüntüsü](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a><span data-ttu-id="ca996-129">Etiket ve anında iletme görüntüleri</span><span class="sxs-lookup"><span data-stu-id="ca996-129">Tag and push images</span></span>

<span data-ttu-id="ca996-130">Etiket hello *azure oy ön* hello loginServer hello kapsayıcı kayıt defteri görüntüsüyle.</span><span class="sxs-lookup"><span data-stu-id="ca996-130">Tag hello *azure-vote-front* image with hello loginServer of hello container registry.</span></span>

<span data-ttu-id="ca996-131">Azure kapsayıcı kayıt defteri kullanıyorsanız, hello hello oturum açma sunucu adıyla alma [az acr listesi](/cli/azure/acr#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="ca996-131">If you're using Azure Container Registry, get hello login server name with hello [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="ca996-132">Kullanım [docker etiketi](https://docs.docker.com/engine/reference/commandline/tag/) tootag hello görüntü.</span><span class="sxs-lookup"><span data-stu-id="ca996-132">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) tootag hello image.</span></span> <span data-ttu-id="ca996-133">Değiştir `<acrLoginServer>` Azure kapsayıcı kayıt defteri oturum açma sunucu adı veya ortak kayıt defteri ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="ca996-133">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="ca996-134">Kullanım [docker itme](https://docs.docker.com/engine/reference/commandline/push/) tooupload hello görüntü tooyour kayıt defteri.</span><span class="sxs-lookup"><span data-stu-id="ca996-134">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) tooupload hello image tooyour registry.</span></span> <span data-ttu-id="ca996-135">Değiştir `<acrLoginServer>` Azure kapsayıcı kayıt defteri oturum açma sunucu adı veya ortak kayıt defteri ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="ca996-135">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a><span data-ttu-id="ca996-136">Güncelleştirme uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="ca996-136">Deploy update application</span></span>

<span data-ttu-id="ca996-137">tooensure en fazla çalışma süresi, birden çok örneğini hello uygulama pod çalıştırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca996-137">tooensure maximum uptime, multiple instances of hello application pod must be running.</span></span> <span data-ttu-id="ca996-138">Bu yapılandırma ile Merhaba doğrulayın [kubectl alma pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) komutu.</span><span class="sxs-lookup"><span data-stu-id="ca996-138">Verify this configuration with hello [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```bash
kubectl get pod
```

<span data-ttu-id="ca996-139">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="ca996-139">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="ca996-140">Birden çok pod'ları hello azure oy ön görüntüsünü çalıştıran yoksa, hello ölçeklendirme *azure oy ön* dağıtım.</span><span class="sxs-lookup"><span data-stu-id="ca996-140">If you don't have multiple pods running hello azure-vote-front image, scale hello *azure-vote-front* deployment.</span></span>


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="ca996-141">tooupdate Merhaba uygulaması, kullanım hello [kubectl kümesi](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) komutu.</span><span class="sxs-lookup"><span data-stu-id="ca996-141">tooupdate hello application, use hello [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) command.</span></span> <span data-ttu-id="ca996-142">Güncelleştirme `<acrLoginServer>` hello oturum açma sunucusu veya ana bilgisayar adı, kapsayıcı kayıt defteri.</span><span class="sxs-lookup"><span data-stu-id="ca996-142">Update `<acrLoginServer>` with hello login server or host name of your container registry.</span></span>

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="ca996-143">toomonitor hello dağıtım, kullanım hello [kubectl alma pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) komutu.</span><span class="sxs-lookup"><span data-stu-id="ca996-143">toomonitor hello deployment, use hello [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span> <span data-ttu-id="ca996-144">Güncelleştirilmiş hello uygulamanın dağıtıldığını gibi pod'ları sonlandırıldı ve hello yeni kapsayıcı görüntüsü ile yeniden oluşturulacak.</span><span class="sxs-lookup"><span data-stu-id="ca996-144">As hello updated application is deployed, your pods are terminated and re-created with hello new container image.</span></span>

```azurecli-interactive
kubectl get pod
```

<span data-ttu-id="ca996-145">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="ca996-145">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a><span data-ttu-id="ca996-146">Güncelleştirilmiş uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="ca996-146">Test updated application</span></span>

<span data-ttu-id="ca996-147">Merhaba Hello dış IP adresi al *azure oy ön* hizmet.</span><span class="sxs-lookup"><span data-stu-id="ca996-147">Get hello external IP address of hello *azure-vote-front* service.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front
```

<span data-ttu-id="ca996-148">Gözat toohello IP adresi toosee hello uygulama güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="ca996-148">Browse toohello IP address toosee hello updated application.</span></span>

![Azure’da Kubernetes kümesinin görüntüsü](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="ca996-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ca996-150">Next steps</span></span>

<span data-ttu-id="ca996-151">Bu öğreticide, bir uygulamanın güncelleştirilmiş ve bu güncelleştirme tooa Kubernetes küme alındı.</span><span class="sxs-lookup"><span data-stu-id="ca996-151">In this tutorial, you updated an application and rolled out this update tooa Kubernetes cluster.</span></span> <span data-ttu-id="ca996-152">görevleri aşağıdaki hello tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="ca996-152">hello following tasks were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ca996-153">Güncelleştirilmiş hello ön uç uygulamasındaki kod</span><span class="sxs-lookup"><span data-stu-id="ca996-153">Updated hello front-end application code</span></span>
> * <span data-ttu-id="ca996-154">Güncelleştirilmiş kapsayıcı görüntüyü oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="ca996-154">Created an updated container image</span></span>
> * <span data-ttu-id="ca996-155">Merhaba kapsayıcı görüntü tooAzure kapsayıcı kayıt defteri gönderilir</span><span class="sxs-lookup"><span data-stu-id="ca996-155">Pushed hello container image tooAzure Container Registry</span></span>
> * <span data-ttu-id="ca996-156">Dağıtılan hello güncelleştirilmiş uygulama</span><span class="sxs-lookup"><span data-stu-id="ca996-156">Deployed hello updated application</span></span>

<span data-ttu-id="ca996-157">İlerlemek toohello sonraki öğretici toolearn konusunda toomonitor Kubernetes Operations Management Suite ile.</span><span class="sxs-lookup"><span data-stu-id="ca996-157">Advance toohello next tutorial toolearn about how toomonitor Kubernetes with Operations Management Suite.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ca996-158">OMS ile Kubernetes’i izleme</span><span class="sxs-lookup"><span data-stu-id="ca996-158">Monitor Kubernetes with OMS</span></span>](./container-service-tutorial-kubernetes-monitor.md)