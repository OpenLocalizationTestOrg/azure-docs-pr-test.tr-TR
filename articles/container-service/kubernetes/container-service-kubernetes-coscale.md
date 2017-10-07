---
title: "bir Azure Kubernetes aaaMonitor CoScale ile küme | Microsoft Docs"
description: "İzleyici CoScale kullanarak Azure kapsayıcı hizmeti Kubernetes kümede"
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a><span data-ttu-id="0fb85-103">Azure kapsayıcı hizmeti Kubernetes küme CoScale ile izleme</span><span class="sxs-lookup"><span data-stu-id="0fb85-103">Monitor an Azure Container Service Kubernetes cluster with CoScale</span></span>

<span data-ttu-id="0fb85-104">Bu makalede, nasıl gösteriyoruz toodeploy hello [CoScale](https://www.coscale.com/) tüm düğümler ve, Kubernetes kapsayıcılarında Azure kapsayıcı Hizmeti'nde küme Aracısı toomonitor.</span><span class="sxs-lookup"><span data-stu-id="0fb85-104">In this article, we show you how toodeploy hello [CoScale](https://www.coscale.com/) agent toomonitor all nodes and containers in your Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="0fb85-105">Bu yapılandırma için CoScale sahip bir hesap gerekir.</span><span class="sxs-lookup"><span data-stu-id="0fb85-105">You need an account with CoScale for this configuration.</span></span> 


## <a name="about-coscale"></a><span data-ttu-id="0fb85-106">CoScale hakkında</span><span class="sxs-lookup"><span data-stu-id="0fb85-106">About CoScale</span></span> 

<span data-ttu-id="0fb85-107">CoScale birkaç orchestration platformlarda tüm kapsayıcıları gelen ölçümleri ve olayları toplayan izleme bir platformdur.</span><span class="sxs-lookup"><span data-stu-id="0fb85-107">CoScale is a monitoring platform that gathers metrics and events from all containers in several orchestration platforms.</span></span> <span data-ttu-id="0fb85-108">CoScale Kubernetes ortamlar için tam yığını izleme sunar.</span><span class="sxs-lookup"><span data-stu-id="0fb85-108">CoScale offers full-stack monitoring for Kubernetes environments.</span></span> <span data-ttu-id="0fb85-109">Merhaba yığınındaki tüm katmanlar için görselleştirme ve analizi sağlar: işletim sistemi, Kubernetes, Docker ve kapsayıcıların içinde çalışan uygulamaların hello.</span><span class="sxs-lookup"><span data-stu-id="0fb85-109">It provides visualizations and analytics for all layers in hello stack: hello OS, Kubernetes, Docker, and applications running inside your containers.</span></span> <span data-ttu-id="0fb85-110">Birkaç yerleşik izleme panoları, coScale sunar ve yerleşik anomali algılama tooallow işleçleri sahiptir ve geliştiricilerin toofind altyapı ve uygulama sorunlarını hızlı.</span><span class="sxs-lookup"><span data-stu-id="0fb85-110">CoScale offers several built-in monitoring dashboards, and it has built-in anomaly detection tooallow operators and developers toofind infrastructure and application issues fast.</span></span>

![UI coScale](./media/container-service-kubernetes-coscale/coscale.png)

<span data-ttu-id="0fb85-112">Bu makalede gösterildiği gibi aracıları Kubernetes küme toorun CoScale bir SaaS çözümü olarak yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0fb85-112">As shown in this article, you can install agents on a Kubernetes cluster toorun CoScale as a SaaS solution.</span></span> <span data-ttu-id="0fb85-113">Verilerinizi şirkete tookeep istiyorsanız CoScale de şirket içi yükleme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0fb85-113">If you want tookeep your data on-site, CoScale is also available for on-premises installation.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="0fb85-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0fb85-114">Prerequisites</span></span>

<span data-ttu-id="0fb85-115">İlk çok gereksinim[CoScale hesabı oluşturma](https://www.coscale.com/free-trial).</span><span class="sxs-lookup"><span data-stu-id="0fb85-115">You first need too[create a CoScale account](https://www.coscale.com/free-trial).</span></span>

<span data-ttu-id="0fb85-116">Bu kılavuz, sahibi olduğunuzu varsayar [Azure kapsayıcı hizmeti kullanarak Kubernetes küme oluşturulan](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="0fb85-116">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="0fb85-117">Ayrıca, hello sahibi olduğunuzu varsayar `az` Azure CLI ve `kubectl` araçları yüklü.</span><span class="sxs-lookup"><span data-stu-id="0fb85-117">It also assumes that you have hello `az` Azure CLI and `kubectl` tools installed.</span></span>

<span data-ttu-id="0fb85-118">Merhaba varsa test edebilirsiniz `az` çalıştırarak yüklü aracı:</span><span class="sxs-lookup"><span data-stu-id="0fb85-118">You can test if you have hello `az` tool installed by running:</span></span>

```azurecli
az --version
```

<span data-ttu-id="0fb85-119">Merhaba yoksa `az` yüklü, aracı yönergeler vardır [burada](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0fb85-119">If you don't have hello `az` tool installed, there are instructions [here](/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="0fb85-120">Merhaba varsa test edebilirsiniz `kubectl` çalıştırarak yüklü aracı:</span><span class="sxs-lookup"><span data-stu-id="0fb85-120">You can test if you have hello `kubectl` tool installed by running:</span></span>

```bash
kubectl version
```

<span data-ttu-id="0fb85-121">Sahip değilseniz `kubectl` yüklü çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0fb85-121">If you don't have `kubectl` installed, you can run:</span></span>

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a><span data-ttu-id="0fb85-122">DaemonSet ile Merhaba CoScale Aracısı yükleniyor</span><span class="sxs-lookup"><span data-stu-id="0fb85-122">Installing hello CoScale agent with a DaemonSet</span></span>
<span data-ttu-id="0fb85-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) olan hello kümedeki her ana bilgisayarda bir kapsayıcı tek bir örneğini Kubernetes toorun tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0fb85-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="0fb85-124">Bunlar hello CoScale aracı gibi izleme aracıları çalıştırmak için mükemmel.</span><span class="sxs-lookup"><span data-stu-id="0fb85-124">They're perfect for running monitoring agents such as hello CoScale agent.</span></span>

<span data-ttu-id="0fb85-125">İçinde tooCoScale oturum sonra toohello gidin [Aracısı sayfası](https://app.coscale.com/) tooinstall CoScale aracıları bir DaemonSet kullanarak kümenizde.</span><span class="sxs-lookup"><span data-stu-id="0fb85-125">After you log in tooCoScale, go toohello [agent page](https://app.coscale.com/) tooinstall CoScale agents on your cluster using a DaemonSet.</span></span> <span data-ttu-id="0fb85-126">Merhaba CoScale UI destekli yapılandırma adımları toocreate bir aracı ve başlangıç tam Kubernetes kümenizi izleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="0fb85-126">hello CoScale UI provides guided configuration steps toocreate an agent and start monitoring your complete Kubernetes cluster.</span></span>

![CoScale Aracısı yapılandırması](./media/container-service-kubernetes-coscale/installation.png)

<span data-ttu-id="0fb85-128">toostart hello Aracısı hello kümede sağlanan hello komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0fb85-128">toostart hello agent on hello cluster, run hello supplied command:</span></span>

![Merhaba CoScale aracısını başlatın](./media/container-service-kubernetes-coscale/agent_script.png)

<span data-ttu-id="0fb85-130">İşte bu kadar!</span><span class="sxs-lookup"><span data-stu-id="0fb85-130">That's it!</span></span> <span data-ttu-id="0fb85-131">Merhaba aracıları ve çalışıyor olduktan sonra birkaç dakika içinde veri hello konsolunda görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0fb85-131">Once hello agents are up and running, you should see data in hello console in a few minutes.</span></span> <span data-ttu-id="0fb85-132">Merhaba ziyaret [Aracısı sayfası](https://app.coscale.com/) toosee kümenizde özetini ek yapılandırma adımları uygulayın ve panolar hello gibi bkz **Kubernetes küme genel bakış**.</span><span class="sxs-lookup"><span data-stu-id="0fb85-132">Visit hello [agent page](https://app.coscale.com/) toosee a summary of your cluster, perform additional configuration steps, and see dashboards such as hello **Kubernetes cluster overview**.</span></span>

![Kubernetes küme genel bakış](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

<span data-ttu-id="0fb85-134">Merhaba CoScale Aracısı hello kümedeki yeni makinelere otomatik olarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="0fb85-134">hello CoScale agent is automatically deployed on new machines in hello cluster.</span></span> <span data-ttu-id="0fb85-135">otomatik olarak yeni bir sürümü yayımlandığında hello aracı güncelleştirmeleri.</span><span class="sxs-lookup"><span data-stu-id="0fb85-135">hello agent updates automatically when a new version is released.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0fb85-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0fb85-136">Next steps</span></span>

<span data-ttu-id="0fb85-137">Merhaba bkz [CoScale belgelerine](http://docs.coscale.com/) ve [blog](https://www.coscale.com/blog) CoScale çözümlerini izleme hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="0fb85-137">See hello [CoScale documentation](http://docs.coscale.com/) and [blog](https://www.coscale.com/blog) for more more information about CoScale monitoring solutions.</span></span> 

