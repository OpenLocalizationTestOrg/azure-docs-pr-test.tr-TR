---
title: "aaaAzure kapsayıcı hizmeti Öğreticisi - uygulamayı Ölçeklendir | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Öğreticisi - uygulamayı Ölçeklendir"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Mikro docker, kapsayıcıları, hizmetleri, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 29571eef0fd91bd6b40f00d8c018539f320179bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a><span data-ttu-id="1ec2a-104">Ölçek Kubernetes pod'ları ve Kubernetes altyapısı</span><span class="sxs-lookup"><span data-stu-id="1ec2a-104">Scale Kubernetes pods and Kubernetes infrastructure</span></span>

<span data-ttu-id="1ec2a-105">Hello öğreticileri takip, Azure kapsayıcı Hizmeti'nde çalışan Kubernetes küme sahip olmanız ve hello Azure oylama uygulaması dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-105">If you've been following hello tutorials, you have a working Kubernetes cluster in Azure Container Service and you deployed hello Azure Voting app.</span></span> 

<span data-ttu-id="1ec2a-106">Bu öğreticide parçası beş yedi, hello pod'ları hello uygulamasında ölçeğini ve pod otomatik ölçeklendirmeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-106">In this tutorial, part five of seven, you scale out hello pods in hello app and try pod autoscaling.</span></span> <span data-ttu-id="1ec2a-107">Ayrıca, nasıl Azure VM Aracısı düğümleri toochange tooscale hello sayısı hello iş yüklerini barındırmak için kümenin kapasite öğrenin.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-107">You also learn how tooscale hello number of Azure VM agent nodes toochange hello cluster's capacity for hosting workloads.</span></span> <span data-ttu-id="1ec2a-108">Tamamlanan görevler aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="1ec2a-108">Tasks completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1ec2a-109">Kubernetes pod'ları el ile ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="1ec2a-109">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="1ec2a-110">Merhaba uygulaması ön ucu çalıştıran otomatik ölçeklendirme pod'ları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1ec2a-110">Configuring Autoscale pods running hello app front end</span></span>
> * <span data-ttu-id="1ec2a-111">Merhaba Kubernetes Azure Aracısı düğümleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="1ec2a-111">Scale hello Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="1ec2a-112">Sonraki öğreticilerde, hello Azure oy uygulama güncelleştirilir ve Operations Management Suite toomonitor hello Kubernetes kümesi yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-112">In subsequent tutorials, hello Azure Vote application is updated, and Operations Management Suite configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1ec2a-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="1ec2a-113">Before you begin</span></span>

<span data-ttu-id="1ec2a-114">Önceki öğreticileri, bir uygulama bir kapsayıcı görüntüsüne paketlenmiş, tooAzure kapsayıcı kayıt defteri ve oluşturulan bir Kubernetes kümesi bu görüntüyü karşıya.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-114">In previous tutorials, an application was packaged into a container image, this image uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="1ec2a-115">Merhaba uygulaması sonra hello Kubernetes kümede çalıştırıldı.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-115">hello application was then run on hello Kubernetes cluster.</span></span> <span data-ttu-id="1ec2a-116">Bu adımları yapmadıysanız ve boyunca toofollow istersiniz, toohello dönmek [Öğreticisi 1 – Oluştur kapsayıcı görüntüleri](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="1ec2a-116">If you have not done these steps, and would like toofollow along, return toohello [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="1ec2a-117">En azından, Bu öğretici bir Kubernetes kümesi ile çalışan bir uygulama gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-117">At minimum, this tutorial requires a Kubernetes cluster with a running application.</span></span>

## <a name="manually-scale-pods"></a><span data-ttu-id="1ec2a-118">Pod'ları el ile ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="1ec2a-118">Manually scale pods</span></span>

<span data-ttu-id="1ec2a-119">Bugüne kadarki hello Azure oy ön uç ve Redis örnek dağıtıldıktan, her tek bir çoğaltma ile.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-119">Thus far, hello Azure Vote front-end and Redis instance have been deployed, each with a single replica.</span></span> <span data-ttu-id="1ec2a-120">Merhaba çalıştırmak tooverify [kubectl almak](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) komutu.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-120">tooverify, run hello [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="1ec2a-121">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="1ec2a-121">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

<span data-ttu-id="1ec2a-122">El ile pod'ları hello içinde hello sayısını değiştirme `azure-vote-front` hello kullanarak dağıtım [kubectl ölçek](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) komutu.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-122">Manually change hello number of pods in hello `azure-vote-front` deployment using hello [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) command.</span></span> <span data-ttu-id="1ec2a-123">Bu örnek hello numara too5 artırır.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-123">This example increases hello number too5.</span></span>

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

<span data-ttu-id="1ec2a-124">Çalıştırma [kubectl pod'ları alma](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify Kubernetes hello pod'ları oluşturuyor.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-124">Run [kubectl get pods](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify that Kubernetes is creating hello pods.</span></span> <span data-ttu-id="1ec2a-125">Bir dakika veya bunu sonra ek hello pod'ları çalıştırıyorsanız:</span><span class="sxs-lookup"><span data-stu-id="1ec2a-125">After a minute or so, hello additional pods are running:</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="1ec2a-126">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="1ec2a-126">Output:</span></span>

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a><span data-ttu-id="1ec2a-127">Otomatik ölçeklendirme pod'ları</span><span class="sxs-lookup"><span data-stu-id="1ec2a-127">Autoscale pods</span></span>

<span data-ttu-id="1ec2a-128">Kubernetes destekleyen [yatay pod otomatik ölçeklendirmeyi](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust hello pod'ları CPU kullanımı veya diğer bağlı olarak bir dağıtımda sayısını ölçümleri seçin.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-128">Kubernetes supports [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust hello number of pods in a deployment depending on CPU utilization or other select metrics.</span></span> 

<span data-ttu-id="1ec2a-129">toouse hello autoscaler, pod'ları CPU istekleri ve sınırları tanımlanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-129">toouse hello autoscaler, your pods must have CPU requests and limits defined.</span></span> <span data-ttu-id="1ec2a-130">Merhaba, `azure-vote-front` dağıtımı, ön uç kapsayıcı istekleri 0,25 CPU 0,5 sınırı ile Merhaba CPU.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-130">In hello `azure-vote-front` deployment, hello front-end container requests 0.25 CPU, with a limit of 0.5 CPU.</span></span> <span data-ttu-id="1ec2a-131">gibi Hello ayarlarını arayın:</span><span class="sxs-lookup"><span data-stu-id="1ec2a-131">hello settings look like:</span></span>

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

<span data-ttu-id="1ec2a-132">Merhaba aşağıdaki örnek kullanır hello [kubectl otomatik ölçeklendirme](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) komut tooautoscale hello pod'ları hello içinde sayısı `azure-vote-front` dağıtım.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-132">hello following example uses hello [kubectl autoscale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) command tooautoscale hello number of pods in hello `azure-vote-front` deployment.</span></span> <span data-ttu-id="1ec2a-133">Burada, CPU kullanımı % 50 aşarsa hello autoscaler hello pod'ları tooa en fazla 10 artırır.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-133">Here, if CPU utilization exceeds 50%, hello autoscaler increases hello pods tooa maximum of 10.</span></span>


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

<span data-ttu-id="1ec2a-134">Merhaba autoscaler, komutu aşağıdaki hello çalıştırmak toosee hello durumu:</span><span class="sxs-lookup"><span data-stu-id="1ec2a-134">toosee hello status of hello autoscaler, run hello following command:</span></span>

```azurecli-interactive
kubectl get hpa
```

<span data-ttu-id="1ec2a-135">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="1ec2a-135">Output:</span></span>

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

<span data-ttu-id="1ec2a-136">Merhaba pod çoğaltmaların sayısı hello Azure oy uygulama üzerinde minimum yük ile birkaç dakika sonra otomatik olarak too3 azaltır.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-136">After a few minutes, with minimal load on hello Azure Vote app, hello number of pod replicas decreases automatically too3.</span></span>

## <a name="scale-hello-agents"></a><span data-ttu-id="1ec2a-137">Ölçek hello aracıları</span><span class="sxs-lookup"><span data-stu-id="1ec2a-137">Scale hello agents</span></span>

<span data-ttu-id="1ec2a-138">Merhaba önceki öğreticide varsayılan komutlarını kullanarak Kubernetes kümenize oluşturduysanız, üç Aracısı düğüm yok.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-138">If you created your Kubernetes cluster using default commands in hello previous tutorial, it has three agent nodes.</span></span> <span data-ttu-id="1ec2a-139">Daha fazla veya daha az sayıda kapsayıcı iş yükleri kümenizde düşünüyorsanız, aracı hello sayısı el ile ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-139">You can adjust hello number of agents manually if you plan more or fewer container workloads on your cluster.</span></span> <span data-ttu-id="1ec2a-140">Kullanım hello [az acs ölçeklendirme](/cli/azure/acs#scale) komutu ve aracı hello sayısı ile Merhaba belirtin `--new-agent-count` parametresi.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-140">Use hello [az acs scale](/cli/azure/acs#scale) command, and specify hello number of agents with hello `--new-agent-count` parameter.</span></span>

<span data-ttu-id="1ec2a-141">Merhaba aşağıdaki örnek hello sayısını Aracısı düğümleri too4 adlı hello Kubernetes kümedeki artırır *myK8sCluster*.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-141">hello following example increases hello number of agent nodes too4 in hello Kubernetes cluster named *myK8sCluster*.</span></span> <span data-ttu-id="1ec2a-142">birkaç dakika toocomplete Hello komutu alır.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-142">hello command takes a couple of minutes toocomplete.</span></span>

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

<span data-ttu-id="1ec2a-143">Merhaba komutu çıktısı hello sayısını Aracısı düğümleri hello değerinde gösterir `agentPoolProfiles:count`:</span><span class="sxs-lookup"><span data-stu-id="1ec2a-143">hello command output shows hello number of agent nodes in hello value of `agentPoolProfiles:count`:</span></span>

```azurecli
{
  "agentPoolProfiles": [
    {
      "count": 4,
      "dnsPrefix": "myK8SCluster-myK8SCluster-e44f25-k8s-agents",
      "fqdn": "",
      "name": "agentpools",
      "vmSize": "Standard_D2_v2"
    }
  ],
...

```

## <a name="next-steps"></a><span data-ttu-id="1ec2a-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1ec2a-144">Next steps</span></span>

<span data-ttu-id="1ec2a-145">Bu öğreticide, farklı ölçekleme özelliklerini Kubernetes kümenizdeki kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-145">In this tutorial, you used different scaling features in your Kubernetes cluster.</span></span> <span data-ttu-id="1ec2a-146">Görevleri dahil ele:</span><span class="sxs-lookup"><span data-stu-id="1ec2a-146">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1ec2a-147">Kubernetes pod'ları el ile ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="1ec2a-147">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="1ec2a-148">Merhaba uygulaması ön ucu çalıştıran otomatik ölçeklendirme pod'ları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1ec2a-148">Configuring Autoscale pods running hello app front end</span></span>
> * <span data-ttu-id="1ec2a-149">Merhaba Kubernetes Azure Aracısı düğümleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="1ec2a-149">Scale hello Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="1ec2a-150">Kubernetes uygulamada güncelleştirme hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="1ec2a-150">Advance toohello next tutorial toolearn about updating application in Kubernetes.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1ec2a-151">Bir uygulamada Kubernetes güncelleştir</span><span class="sxs-lookup"><span data-stu-id="1ec2a-151">Update an application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-app-update.md)

