---
title: "aaaAzure kapsayıcı hizmeti Öğreticisi - İzleyici Kubernetes | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Öğreticisi - İzleyici Kubernetes Microsoft Operations Management Suite (OMS)"
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
ms.openlocfilehash: 54fa789453768529deaf25d7575e5b21d0e41882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a><span data-ttu-id="5ef76-104">Operations Management Suite Kubernetes kümeyle izleme</span><span class="sxs-lookup"><span data-stu-id="5ef76-104">Monitor a Kubernetes cluster with Operations Management Suite</span></span>

<span data-ttu-id="5ef76-105">Özellikle birden çok uygulama ile ölçekli üretim kümesi yönetirken izleme Kubernetes küme ve kapsayıcıları, önemlidir.</span><span class="sxs-lookup"><span data-stu-id="5ef76-105">Monitoring your Kubernetes cluster and containers is critical, especially when you manage a production cluster at scale with multiple apps.</span></span> 

<span data-ttu-id="5ef76-106">Birkaç Kubernetes izleme çözümlerinin, Microsoft veya diğer sağlayıcıları avantajından yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ef76-106">You can take advantage of several Kubernetes monitoring solutions, either from Microsoft or other providers.</span></span> <span data-ttu-id="5ef76-107">Bu öğreticide, Kubernetes kümenizi Merhaba kapsayıcılara çözümde kullanarak izlemenizi [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Microsoft'un bulut tabanlı BT yönetim çözümü.</span><span class="sxs-lookup"><span data-stu-id="5ef76-107">In this tutorial, you monitor your Kubernetes cluster by using hello Containers solution in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Microsoft's cloud-based IT management solution.</span></span> <span data-ttu-id="5ef76-108">(Merhaba OMS kapsayıcıları çözüm önizlemede değil.)</span><span class="sxs-lookup"><span data-stu-id="5ef76-108">(hello OMS Containers solution is in preview.)</span></span>

<span data-ttu-id="5ef76-109">Bu öğretici, parçası yedi yedi, görevleri aşağıdaki hello kapsar:</span><span class="sxs-lookup"><span data-stu-id="5ef76-109">This tutorial, part seven of seven, covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5ef76-110">OMS çalışma ayarlarını al</span><span class="sxs-lookup"><span data-stu-id="5ef76-110">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="5ef76-111">Merhaba Kubernetes düğümlerdeki OMS aracılarını ayarlama</span><span class="sxs-lookup"><span data-stu-id="5ef76-111">Set up OMS agents on hello Kubernetes nodes</span></span>
> * <span data-ttu-id="5ef76-112">İzleme bilgilerini hello OMS portalında veya Azure portalına erişim</span><span class="sxs-lookup"><span data-stu-id="5ef76-112">Access monitoring information in hello OMS portal or Azure portal</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5ef76-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="5ef76-113">Before you begin</span></span>

<span data-ttu-id="5ef76-114">Önceki öğreticileri, bir uygulama kapsayıcı görüntülere paketlenmiş, bu görüntüleri tooAzure kapsayıcı kayıt defteri ve oluşturulan Kubernetes küme karşıya.</span><span class="sxs-lookup"><span data-stu-id="5ef76-114">In previous tutorials, an application was packaged into container images, these images uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="5ef76-115">Bu adımları yapmadıysanız ve boyunca toofollow istersiniz, çok dönmek[Öğreticisi 1 – Oluştur kapsayıcı görüntüleri](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="5ef76-115">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="5ef76-116">En azından, Bu öğretici Linux Aracısı düğümleri ve bir Operations Management Suite (OMS) hesap Kubernetes kümeyle gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5ef76-116">At minimum, this tutorial requires a Kubernetes cluster with Linux agent nodes, and an Operations Management Suite (OMS) account.</span></span> <span data-ttu-id="5ef76-117">Gerekirse, kaydolun bir [ücretsiz OMS deneme](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span><span class="sxs-lookup"><span data-stu-id="5ef76-117">If needed, sign up for a [free OMS trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span></span>

## <a name="get-workspace-settings"></a><span data-ttu-id="5ef76-118">Çalışma alanı ayarlarını al</span><span class="sxs-lookup"><span data-stu-id="5ef76-118">Get Workspace settings</span></span>

<span data-ttu-id="5ef76-119">Ne zaman erişebilirsiniz hello [OMS portalı](https://mms.microsoft.com), çok Git**ayarları** > **bağlı kaynakları** > **Linux sunucuları**.</span><span class="sxs-lookup"><span data-stu-id="5ef76-119">When you can access hello [OMS portal](https://mms.microsoft.com), go too**Settings** > **Connected Sources** > **Linux Servers**.</span></span> <span data-ttu-id="5ef76-120">Merhaba, bulabilirsiniz *çalışma alanı kimliği* ve birincil veya ikincil *çalışma alanı anahtarı*.</span><span class="sxs-lookup"><span data-stu-id="5ef76-120">There, you can find hello *Workspace ID* and a primary or secondary *Workspace Key*.</span></span> <span data-ttu-id="5ef76-121">Gereksinim duyduğunuz bu değerleri not edin tooset hello kümede OMS Aracısı ayarlama.</span><span class="sxs-lookup"><span data-stu-id="5ef76-121">Take note of these values, which you need tooset up OMS agents on hello cluster.</span></span>

## <a name="set-up-oms-agents"></a><span data-ttu-id="5ef76-122">OMS aracılarını ayarlama</span><span class="sxs-lookup"><span data-stu-id="5ef76-122">Set up OMS agents</span></span>

<span data-ttu-id="5ef76-123">Burada, OMS Aracısı hello Linux küme düğümlerinde yukarı YAML dosya tooset verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="5ef76-123">Here is a YAML file tooset up OMS agents on hello Linux cluster nodes.</span></span> <span data-ttu-id="5ef76-124">Bir Kubernetes oluşturur [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), her küme düğümünde tek aynı pod çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="5ef76-124">It creates a Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), which runs a single identical pod on each cluster node.</span></span> <span data-ttu-id="5ef76-125">Merhaba DaemonSet kaynak izleme aracısını dağıtmak için idealdir.</span><span class="sxs-lookup"><span data-stu-id="5ef76-125">hello DaemonSet resource is ideal for deploying a monitoring agent.</span></span> 

<span data-ttu-id="5ef76-126">Aşağıdaki metin tooa dosyasına adlı hello Kaydet `oms-daemonset.yaml`ve hello yer tutucu değerlerini değiştirme *myWorkspaceID* ve *myWorkspaceKey* OMS çalışma alanı kimliği ve anahtarı.</span><span class="sxs-lookup"><span data-stu-id="5ef76-126">Save hello following text tooa file named `oms-daemonset.yaml`, and replace hello placeholder values for *myWorkspaceID* and *myWorkspaceKey* with your OMS Workspace ID and Key.</span></span> <span data-ttu-id="5ef76-127">(Üretimde, bu değerleri gizlilikleri olarak şifreleyebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="5ef76-127">(In production, you can encode these values as secrets.)</span></span>

```YAML
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
 name: omsagent
spec:
 template:
  metadata:
   labels:
    app: omsagent
    agentVersion: v1.3.4-127
    dockerProviderVersion: 10.0.0-25
  spec:
   containers:
     - name: omsagent 
       image: "microsoft/oms"
       imagePullPolicy: Always
       env:
       - name: WSID
         value: myWorkspaceID
       - name: KEY 
         value: myWorkspaceKey
       - name: DOMAIN
         value: opinsights.azure.com
       securityContext:
         privileged: true
       ports:
       - containerPort: 25225
         protocol: TCP 
       - containerPort: 25224
         protocol: UDP
       volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /var/log 
          name: host-log
       livenessProbe:
        exec:
         command:
         - /bin/bash
         - -c
         - ps -ef | grep omsagent | grep -v "grep"
        initialDelaySeconds: 60
        periodSeconds: 60
   volumes:
    - name: docker-sock 
      hostPath:
       path: /var/run/docker.sock
    - name: host-log
      hostPath:
       path: /var/log
```

<span data-ttu-id="5ef76-128">Merhaba DaemonSet komutu aşağıdaki hello ile oluşturun:</span><span class="sxs-lookup"><span data-stu-id="5ef76-128">Create hello DaemonSet with hello following command:</span></span>

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

<span data-ttu-id="5ef76-129">toosee DaemonSet oluşturulur, bu hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5ef76-129">toosee that hello DaemonSet is created, run:</span></span>

```azurecli-interactive
kubectl get daemonset
```

<span data-ttu-id="5ef76-130">Çıktı benzer toohello aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5ef76-130">Output is similar toohello following:</span></span>

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

<span data-ttu-id="5ef76-131">Merhaba aracılar çalışan sonra OMS tooingest ve işlem hello veriler için birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="5ef76-131">After hello agents are running, it takes several minutes for OMS tooingest and process hello data.</span></span>

## <a name="access-monitoring-data"></a><span data-ttu-id="5ef76-132">İzleme verilerine erişim</span><span class="sxs-lookup"><span data-stu-id="5ef76-132">Access monitoring data</span></span>

<span data-ttu-id="5ef76-133">Görüntüleme ve hello OMS kapsayıcı hello verilerle izleme çözümleme [kapsayıcı çözüm](../../log-analytics/log-analytics-containers.md) hello OMS portalında veya hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="5ef76-133">View and analyze hello OMS container monitoring data with hello [Container solution](../../log-analytics/log-analytics-containers.md) in either hello OMS portal or hello Azure portal.</span></span> 

<span data-ttu-id="5ef76-134">Hello kullanarak tooinstall hello kapsayıcı çözüm [OMS portalı](https://mms.microsoft.com), çok Git**Çözümleri Galerisi**.</span><span class="sxs-lookup"><span data-stu-id="5ef76-134">tooinstall hello Container solution using hello [OMS portal](https://mms.microsoft.com), go too**Solutions Gallery**.</span></span> <span data-ttu-id="5ef76-135">Ardından ekleyin **kapsayıcı çözüm**.</span><span class="sxs-lookup"><span data-stu-id="5ef76-135">Then add **Container Solution**.</span></span> <span data-ttu-id="5ef76-136">Alternatif olarak, hello Merhaba kapsayıcılara Çözüm Ekle [Azure Marketi](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span><span class="sxs-lookup"><span data-stu-id="5ef76-136">Alternatively, add hello Containers solution from hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span></span>

<span data-ttu-id="5ef76-137">Merhaba OMS portalında aramak bir **kapsayıcıları** hello OMS Pano Özet kutucuğu.</span><span class="sxs-lookup"><span data-stu-id="5ef76-137">In hello OMS portal, look for a **Containers** summary tile on hello OMS dashboard.</span></span> <span data-ttu-id="5ef76-138">Gibi ayrıntıları Hello kutucuğa tıklayın: kapsayıcı olayları, hatalar, durumu, görüntü stok ve CPU ve bellek kullanımı.</span><span class="sxs-lookup"><span data-stu-id="5ef76-138">Click hello tile for details including: container events, errors, status, image inventory, and CPU and memory usage.</span></span> <span data-ttu-id="5ef76-139">Daha ayrıntılı bilgi için herhangi bir kutucuğu satırındaki'ı tıklatın veya gerçekleştirmek bir [günlük arama](../../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="5ef76-139">For more granular information, click a row on any tile, or perform a [log search](../../log-analytics/log-analytics-log-searches.md).</span></span>

![OMS portalında kapsayıcıları Panosu](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

<span data-ttu-id="5ef76-141">Benzer şekilde, çok hello Azure portal, Git**günlük analizi** ve çalışma alanı adı seçin.</span><span class="sxs-lookup"><span data-stu-id="5ef76-141">Similarly, in hello Azure portal, go too**Log Analytics** and select your workspace name.</span></span> <span data-ttu-id="5ef76-142">toosee hello **kapsayıcıları** Özet kutucuğuna tıklayın **çözümleri** > **kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="5ef76-142">toosee hello **Containers** summary tile, click **Solutions** > **Containers**.</span></span> <span data-ttu-id="5ef76-143">toosee Ayrıntılar hello kutucuğu'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5ef76-143">toosee details, click hello tile.</span></span>

<span data-ttu-id="5ef76-144">Merhaba bkz [Azure günlük analizi belgeleri](../../log-analytics/index.md) sorgulama ve izleme verilerini analiz etme konusunda ayrıntılı yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="5ef76-144">See hello [Azure Log Analytics documentation](../../log-analytics/index.md) for detailed guidance on querying and analyzing monitoring data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ef76-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5ef76-145">Next steps</span></span>

<span data-ttu-id="5ef76-146">Bu öğreticide, OMS Kubernetes kümenizle izlenen.</span><span class="sxs-lookup"><span data-stu-id="5ef76-146">In this tutorial, you monitored your Kubernetes cluster with OMS.</span></span> <span data-ttu-id="5ef76-147">Görevleri dahil ele:</span><span class="sxs-lookup"><span data-stu-id="5ef76-147">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5ef76-148">OMS çalışma ayarlarını al</span><span class="sxs-lookup"><span data-stu-id="5ef76-148">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="5ef76-149">Merhaba Kubernetes düğümlerdeki OMS aracılarını ayarlama</span><span class="sxs-lookup"><span data-stu-id="5ef76-149">Set up OMS agents on hello Kubernetes nodes</span></span>
> * <span data-ttu-id="5ef76-150">İzleme bilgilerini hello OMS portalında veya Azure portalına erişim</span><span class="sxs-lookup"><span data-stu-id="5ef76-150">Access monitoring information in hello OMS portal or Azure portal</span></span>


<span data-ttu-id="5ef76-151">Kod örnekleri için kapsayıcı hizmeti önceden oluşturulmuş Bu bağlantı toosee izleyin.</span><span class="sxs-lookup"><span data-stu-id="5ef76-151">Follow this link toosee pre-built script samples for Container Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5ef76-152">Azure kapsayıcı hizmeti kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="5ef76-152">Azure Container Service script samples</span></span>](cli-samples.md)
