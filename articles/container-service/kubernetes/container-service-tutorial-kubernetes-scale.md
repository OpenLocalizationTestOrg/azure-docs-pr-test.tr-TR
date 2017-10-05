---
title: "Azure kapsayıcı hizmeti Öğreticisi - uygulamayı Ölçeklendir | Microsoft Docs"
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
ms.openlocfilehash: 62e70e34d06f5220734ff85c70a0c9b475f9579b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a><span data-ttu-id="ff59d-104">Ölçek Kubernetes pod'ları ve Kubernetes altyapısı</span><span class="sxs-lookup"><span data-stu-id="ff59d-104">Scale Kubernetes pods and Kubernetes infrastructure</span></span>

<span data-ttu-id="ff59d-105">Öğreticiler takip, Azure kapsayıcı Hizmeti'nde çalışan Kubernetes küme sahip olmanız ve Azure oylama uygulaması dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="ff59d-105">If you've been following the tutorials, you have a working Kubernetes cluster in Azure Container Service and you deployed the Azure Voting app.</span></span> 

<span data-ttu-id="ff59d-106">Bu öğreticide parçası beş yedi, uygulama pod'ları ölçeğini ve pod otomatik ölçeklendirmeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="ff59d-106">In this tutorial, part five of seven, you scale out the pods in the app and try pod autoscaling.</span></span> <span data-ttu-id="ff59d-107">Ayrıca iş yüklerini barındırmak için kümenin kapasite değiştirmek için Azure VM Aracısı düğüm sayısının ölçeğini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ff59d-107">You also learn how to scale the number of Azure VM agent nodes to change the cluster's capacity for hosting workloads.</span></span> <span data-ttu-id="ff59d-108">Tamamlanan görevler aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="ff59d-108">Tasks completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ff59d-109">Kubernetes pod'ları el ile ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="ff59d-109">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="ff59d-110">Otomatik ölçeklendirme uygulaması ön ucu çalıştıran pod'ları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ff59d-110">Configuring Autoscale pods running the app front end</span></span>
> * <span data-ttu-id="ff59d-111">Kubernetes Azure Aracısı düğümleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="ff59d-111">Scale the Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="ff59d-112">Sonraki öğreticilerde, Azure oy uygulama güncelleştirilir ve Kubernetes küme izlemek için Operations Management Suite yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="ff59d-112">In subsequent tutorials, the Azure Vote application is updated, and Operations Management Suite configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ff59d-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="ff59d-113">Before you begin</span></span>

<span data-ttu-id="ff59d-114">Önceki eğitimlerine bir uygulama bir kapsayıcı görüntü, Azure kapsayıcı kayıt defterine karşıya bu görüntü ve oluşturulan Kubernetes küme paketlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff59d-114">In previous tutorials, an application was packaged into a container image, this image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="ff59d-115">Uygulama sonra Kubernetes kümede çalıştırıldı.</span><span class="sxs-lookup"><span data-stu-id="ff59d-115">The application was then run on the Kubernetes cluster.</span></span> <span data-ttu-id="ff59d-116">Bu adımları yapmadıysanız ve izlemek istediğiniz, geri dönüp [Öğreticisi 1 – Oluştur kapsayıcı görüntüleri](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="ff59d-116">If you have not done these steps, and would like to follow along, return to the [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="ff59d-117">En azından, Bu öğretici bir Kubernetes kümesi ile çalışan bir uygulama gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ff59d-117">At minimum, this tutorial requires a Kubernetes cluster with a running application.</span></span>

## <a name="manually-scale-pods"></a><span data-ttu-id="ff59d-118">Pod'ları el ile ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="ff59d-118">Manually scale pods</span></span>

<span data-ttu-id="ff59d-119">Bu nedenle şimdiye kadar Azure oy ön uç ve Redis örnek silinmiş dağıtıldı, her tek bir çoğaltma ile.</span><span class="sxs-lookup"><span data-stu-id="ff59d-119">Thus far, the Azure Vote front-end and Redis instance have been deployed, each with a single replica.</span></span> <span data-ttu-id="ff59d-120">Doğrulamak için çalıştırın [kubectl almak](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) komutu.</span><span class="sxs-lookup"><span data-stu-id="ff59d-120">To verify, run the [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="ff59d-121">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="ff59d-121">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

<span data-ttu-id="ff59d-122">El ile pod'ları içinde sayısını değiştirme `azure-vote-front` dağıtım kullanarak [kubectl ölçek](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) komutu.</span><span class="sxs-lookup"><span data-stu-id="ff59d-122">Manually change the number of pods in the `azure-vote-front` deployment using the [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) command.</span></span> <span data-ttu-id="ff59d-123">Bu örnek 5 sayısını artırır.</span><span class="sxs-lookup"><span data-stu-id="ff59d-123">This example increases the number to 5.</span></span>

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

<span data-ttu-id="ff59d-124">Çalıştırma [kubectl pod'ları alma](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) Kubernetes pod'ları oluşturmakta olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ff59d-124">Run [kubectl get pods](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) to verify that Kubernetes is creating the pods.</span></span> <span data-ttu-id="ff59d-125">Bir dakika veya bunu sonra ek pod'ları çalıştırıyorsanız:</span><span class="sxs-lookup"><span data-stu-id="ff59d-125">After a minute or so, the additional pods are running:</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="ff59d-126">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="ff59d-126">Output:</span></span>

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a><span data-ttu-id="ff59d-127">Otomatik ölçeklendirme pod'ları</span><span class="sxs-lookup"><span data-stu-id="ff59d-127">Autoscale pods</span></span>

<span data-ttu-id="ff59d-128">Kubernetes destekleyen [yatay pod otomatik ölçeklendirmeyi](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) ayarlamak için pod'ları CPU kullanımına bağlı olarak bir dağıtımda sayısı veya diğer ölçümleri seçin.</span><span class="sxs-lookup"><span data-stu-id="ff59d-128">Kubernetes supports [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) to adjust the number of pods in a deployment depending on CPU utilization or other select metrics.</span></span> 

<span data-ttu-id="ff59d-129">Autoscaler kullanmak için pod'ları CPU istekleri ve tanımlanan sınırları olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff59d-129">To use the autoscaler, your pods must have CPU requests and limits defined.</span></span> <span data-ttu-id="ff59d-130">İçinde `azure-vote-front` dağıtım, ön uç kapsayıcı 0,5 sınırına sahip istekleri 0,25 CPU CPU.</span><span class="sxs-lookup"><span data-stu-id="ff59d-130">In the `azure-vote-front` deployment, the front-end container requests 0.25 CPU, with a limit of 0.5 CPU.</span></span> <span data-ttu-id="ff59d-131">Ayarları gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="ff59d-131">The settings look like:</span></span>

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

<span data-ttu-id="ff59d-132">Aşağıdaki örnek kullanır [kubectl otomatik ölçeklendirme](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) pod'ları içinde sayısı için otomatik ölçeklendirme komutu `azure-vote-front` dağıtım.</span><span class="sxs-lookup"><span data-stu-id="ff59d-132">The following example uses the [kubectl autoscale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) command to autoscale the number of pods in the `azure-vote-front` deployment.</span></span> <span data-ttu-id="ff59d-133">Burada, CPU kullanımı % 50 aşarsa, en fazla 10 için pod'ları autoscaler artırır.</span><span class="sxs-lookup"><span data-stu-id="ff59d-133">Here, if CPU utilization exceeds 50%, the autoscaler increases the pods to a maximum of 10.</span></span>


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

<span data-ttu-id="ff59d-134">Autoscaler durumunu görmek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ff59d-134">To see the status of the autoscaler, run the following command:</span></span>

```azurecli-interactive
kubectl get hpa
```

<span data-ttu-id="ff59d-135">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="ff59d-135">Output:</span></span>

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

<span data-ttu-id="ff59d-136">Azure oy uygulama üzerinde minimum yük ile birkaç dakika sonra pod çoğaltmaların sayısı 3'e otomatik olarak azaltır.</span><span class="sxs-lookup"><span data-stu-id="ff59d-136">After a few minutes, with minimal load on the Azure Vote app, the number of pod replicas decreases automatically to 3.</span></span>

## <a name="scale-the-agents"></a><span data-ttu-id="ff59d-137">Aracıları ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="ff59d-137">Scale the agents</span></span>

<span data-ttu-id="ff59d-138">Önceki öğreticide varsayılan komutlarını kullanarak Kubernetes kümenize oluşturduysanız, üç Aracısı düğüm yok.</span><span class="sxs-lookup"><span data-stu-id="ff59d-138">If you created your Kubernetes cluster using default commands in the previous tutorial, it has three agent nodes.</span></span> <span data-ttu-id="ff59d-139">Daha fazla veya daha az sayıda kapsayıcı iş yükleri kümenizde düşünüyorsanız, aracı sayısı el ile ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff59d-139">You can adjust the number of agents manually if you plan more or fewer container workloads on your cluster.</span></span> <span data-ttu-id="ff59d-140">Kullanım [az acs ölçeklendirme](/cli/azure/acs#scale) komut ve aracılarla sayısını belirtin `--new-agent-count` parametresi.</span><span class="sxs-lookup"><span data-stu-id="ff59d-140">Use the [az acs scale](/cli/azure/acs#scale) command, and specify the number of agents with the `--new-agent-count` parameter.</span></span>

<span data-ttu-id="ff59d-141">Aşağıdaki örnek 4 adlı Kubernetes kümedeki Aracısı düğüm sayısını artırır *myK8sCluster*.</span><span class="sxs-lookup"><span data-stu-id="ff59d-141">The following example increases the number of agent nodes to 4 in the Kubernetes cluster named *myK8sCluster*.</span></span> <span data-ttu-id="ff59d-142">Komut birkaç tamamlamak için dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="ff59d-142">The command takes a couple of minutes to complete.</span></span>

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

<span data-ttu-id="ff59d-143">Komut çıktısı aracı sayısı düğümleri değerinde gösterir `agentPoolProfiles:count`:</span><span class="sxs-lookup"><span data-stu-id="ff59d-143">The command output shows the number of agent nodes in the value of `agentPoolProfiles:count`:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ff59d-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ff59d-144">Next steps</span></span>

<span data-ttu-id="ff59d-145">Bu öğreticide, farklı ölçekleme özelliklerini Kubernetes kümenizdeki kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ff59d-145">In this tutorial, you used different scaling features in your Kubernetes cluster.</span></span> <span data-ttu-id="ff59d-146">Görevleri dahil ele:</span><span class="sxs-lookup"><span data-stu-id="ff59d-146">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ff59d-147">Kubernetes pod'ları el ile ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="ff59d-147">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="ff59d-148">Otomatik ölçeklendirme uygulaması ön ucu çalıştıran pod'ları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ff59d-148">Configuring Autoscale pods running the app front end</span></span>
> * <span data-ttu-id="ff59d-149">Kubernetes Azure Aracısı düğümleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="ff59d-149">Scale the Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="ff59d-150">Kubernetes uygulamada güncelleştirmek hakkında bilgi edinmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="ff59d-150">Advance to the next tutorial to learn about updating application in Kubernetes.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ff59d-151">Bir uygulamada Kubernetes güncelleştir</span><span class="sxs-lookup"><span data-stu-id="ff59d-151">Update an application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-app-update.md)

