---
title: "aaaAzure kapsayıcı örnekleri kapsayıcı grupları"
description: "Kapsayıcı grupları Azure kapsayıcı durumlarda nasıl çalıştığını anlamak"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2b0e784609979045c8f77d7b6d0987ec3fee714c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="container-groups-in-azure-container-instances"></a><span data-ttu-id="5807e-103">Azure kapsayıcı durumlarda kapsayıcı grupları</span><span class="sxs-lookup"><span data-stu-id="5807e-103">Container Groups in Azure Container Instances</span></span>

<span data-ttu-id="5807e-104">Merhaba en üst düzey Azure kapsayıcı durumlarda bir kapsayıcı grubu kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="5807e-104">hello top-level resource in Azure Container Instances is a container group.</span></span> <span data-ttu-id="5807e-105">Bu makalede, kapsayıcı grupları nedir ve ne tür senaryoların bunlar etkinleştirmek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5807e-105">This article describes what container groups are and what types of scenarios they enable.</span></span>

## <a name="how-a-container-group-works"></a><span data-ttu-id="5807e-106">Kapsayıcı grubu nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="5807e-106">How a container group works</span></span>

<span data-ttu-id="5807e-107">Bir kapsayıcı grubun bir koleksiyondur hello üzerinde zamanlanmış kapsayıcıların aynı ana bilgisayar makine ve bir yaşam döngüsü, yerel ağ ve depolama birimleri paylaşın.</span><span class="sxs-lookup"><span data-stu-id="5807e-107">A container group is a collection of containers that get scheduled on hello same host machine and share a lifecycle, local network, and storage volumes.</span></span> <span data-ttu-id="5807e-108">Benzer toohello kavramı olan bir *pod* içinde [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) ve [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span><span class="sxs-lookup"><span data-stu-id="5807e-108">It is similar toohello concept of a *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) and [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span></span>

<span data-ttu-id="5807e-109">Merhaba Aşağıdaki diyagramda birden çok kapsayıcı içeren bir kapsayıcı grubu örneği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5807e-109">hello following diagram shows an example of a container group that includes multiple containers.</span></span>

![Kapsayıcı grupları örneği][container-groups-example]

<span data-ttu-id="5807e-111">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="5807e-111">Note that:</span></span>

- <span data-ttu-id="5807e-112">Merhaba Grup tek ana makinede zamanlandı.</span><span class="sxs-lookup"><span data-stu-id="5807e-112">hello group is scheduled on a single host machine.</span></span>
- <span data-ttu-id="5807e-113">Merhaba grubu tek bir ortak IP adresi, bir kullanıma sunulan bağlantı noktası ile kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="5807e-113">hello group exposes a single public IP address, with one exposed port.</span></span>
- <span data-ttu-id="5807e-114">Merhaba Grup iki kapsayıcıları için yapılır.</span><span class="sxs-lookup"><span data-stu-id="5807e-114">hello group is made up of two containers.</span></span> <span data-ttu-id="5807e-115">Merhaba diğer 5000 bağlantı noktasını dinler sırasında bir kapsayıcı bağlantı noktası 80 üzerinde dinler.</span><span class="sxs-lookup"><span data-stu-id="5807e-115">One container listens on port 80, while hello other listens on port 5000.</span></span>
- <span data-ttu-id="5807e-116">iki Azure dosya paylaşımları birim başlatmalar olarak Hello grubu içerir ve her kapsayıcı yerel olarak hello paylaşımları birini bağlar.</span><span class="sxs-lookup"><span data-stu-id="5807e-116">hello group includes two Azure file shares as volume mounts, and each container mounts one of hello shares locally.</span></span>

### <a name="networking"></a><span data-ttu-id="5807e-117">Ağ</span><span class="sxs-lookup"><span data-stu-id="5807e-117">Networking</span></span>

<span data-ttu-id="5807e-118">Kapsayıcı grupları, bir IP adresi ve bağlantı noktası ad alanı, IP adresi üzerinde paylaşır.</span><span class="sxs-lookup"><span data-stu-id="5807e-118">Container groups share an IP address and a port namespace on that IP address.</span></span> <span data-ttu-id="5807e-119">tooenable dış istemcilere tooreach hello grup içindeki bir kapsayıcı, başlangıç bağlantı noktası başlangıç IP adresi ve hello kapsayıcısından kullanıma gerekir.</span><span class="sxs-lookup"><span data-stu-id="5807e-119">tooenable external clients tooreach a container within hello group, you must expose hello port on hello IP address and from hello container.</span></span> <span data-ttu-id="5807e-120">Grup Merhaba kapsayıcılara bir bağlantı noktası ad alanı paylaştığından, bağlantı noktası eşlemesi desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="5807e-120">Because containers within hello group share a port namespace, port mapping is not supported.</span></span> <span data-ttu-id="5807e-121">Bu bağlantı noktalarını hello grubun IP adresinde dışarıdan gösterilmeyen olsa bile bir grup kapsayıcılara birbirine hello üzerinde localhost aracılığıyla bunlar açık bağlantı noktaları ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5807e-121">Containers within a group can reach each other via localhost on hello ports that they have exposed, even if those ports are not exposed externally on hello group's IP address.</span></span>

### <a name="storage"></a><span data-ttu-id="5807e-122">Depolama</span><span class="sxs-lookup"><span data-stu-id="5807e-122">Storage</span></span>

<span data-ttu-id="5807e-123">Bir kapsayıcı grubundaki dış birimleri toomount belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5807e-123">You can specify external volumes toomount within a container group.</span></span> <span data-ttu-id="5807e-124">Bu birimlerin hello tek tek bir grup kapsayıcılarında içindeki belirli yollara içine eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5807e-124">You can map those volumes into specific paths within hello individual containers in a group.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="5807e-125">Genel senaryolar</span><span class="sxs-lookup"><span data-stu-id="5807e-125">Common scenarios</span></span>

<span data-ttu-id="5807e-126">Birden çok kapsayıcı grupları tek bir işlev görev yukarı toodivide küçük bir sayıya farklı ekip tarafından alınabilir ve ayrı kaynak gereksinimlerini kapsayıcı görüntülerinin istediğiniz durumlarda kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="5807e-126">Multi-container groups are useful in cases where you want toodivide up a single functional task into a small number of container images, which can be delivered by different teams and have separate resource requirements.</span></span> <span data-ttu-id="5807e-127">Örnek Kullanım dahil olabilir:</span><span class="sxs-lookup"><span data-stu-id="5807e-127">Example usage could include:</span></span>

- <span data-ttu-id="5807e-128">Bir uygulama kapsayıcısı ve günlüğe kaydetme kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="5807e-128">An application container and a logging container.</span></span> <span data-ttu-id="5807e-129">Merhaba günlük kapsayıcı hello günlükleri ve ölçümleri çıktı hello ana uygulama tarafından toplar ve toolong vadeli depolama yazar.</span><span class="sxs-lookup"><span data-stu-id="5807e-129">hello logging container collects hello logs and metrics output by hello main application and writes them toolong-term storage.</span></span>
- <span data-ttu-id="5807e-130">Bir uygulama ve izleme kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="5807e-130">An application and a monitoring container.</span></span> <span data-ttu-id="5807e-131">kapsayıcı düzenli aralıklarla izleme hello çalıştığını ve düzgün yanıt ve değilse bir uyarı başlatır bir istek toohello uygulama tooensure yapar.</span><span class="sxs-lookup"><span data-stu-id="5807e-131">hello monitoring container periodically makes a request toohello application tooensure that it's running and responding correctly and raises an alert if it's not.</span></span>
- <span data-ttu-id="5807e-132">Bir web uygulaması hizmet veren bir kapsayıcı ve kaynak denetiminden hello son içerik çekme kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="5807e-132">A container serving a web application and a container pulling hello latest content from source control.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5807e-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5807e-133">Next steps</span></span>

<span data-ttu-id="5807e-134">Nasıl çok öğrenin[çok kapsayıcı grubu dağıtma](container-instances-multi-container-group.md) bir Azure Resource Manager şablonu ile.</span><span class="sxs-lookup"><span data-stu-id="5807e-134">Learn how too[deploy a multi-container group](container-instances-multi-container-group.md) with an Azure Resource Manager template.</span></span>

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png