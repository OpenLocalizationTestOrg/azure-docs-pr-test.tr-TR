---
title: "Kapsayıcı grupları Azure kapsayıcı örnekleri"
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
ms.openlocfilehash: 25eab41c3f0c986bcce33123f86f4c9638b77191
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="container-groups-in-azure-container-instances"></a><span data-ttu-id="2c343-103">Azure kapsayıcı durumlarda kapsayıcı grupları</span><span class="sxs-lookup"><span data-stu-id="2c343-103">Container Groups in Azure Container Instances</span></span>

<span data-ttu-id="2c343-104">Azure kapsayıcı durumlarda en üst düzey kaynak bir kapsayıcı grubudur.</span><span class="sxs-lookup"><span data-stu-id="2c343-104">The top-level resource in Azure Container Instances is a container group.</span></span> <span data-ttu-id="2c343-105">Bu makalede, kapsayıcı grupları nedir ve ne tür senaryoların bunlar etkinleştirmek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2c343-105">This article describes what container groups are and what types of scenarios they enable.</span></span>

## <a name="how-a-container-group-works"></a><span data-ttu-id="2c343-106">Kapsayıcı grubu nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="2c343-106">How a container group works</span></span>

<span data-ttu-id="2c343-107">Kapsayıcı grubu, aynı ana bilgisayar makinesinde zamanlanmış ve bir yaşam döngüsü, yerel ağ ve depolama birimleri paylaşan kapsayıcıları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="2c343-107">A container group is a collection of containers that get scheduled on the same host machine and share a lifecycle, local network, and storage volumes.</span></span> <span data-ttu-id="2c343-108">Kavramı, benzer bir *pod* içinde [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) ve [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span><span class="sxs-lookup"><span data-stu-id="2c343-108">It is similar to the concept of a *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) and [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span></span>

<span data-ttu-id="2c343-109">Aşağıdaki diyagramda, birden çok kapsayıcı içeren bir kapsayıcı grubu örneği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="2c343-109">The following diagram shows an example of a container group that includes multiple containers.</span></span>

![Kapsayıcı grupları örneği][container-groups-example]

<span data-ttu-id="2c343-111">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="2c343-111">Note that:</span></span>

- <span data-ttu-id="2c343-112">Grubun tek ana makinede zamanlandı.</span><span class="sxs-lookup"><span data-stu-id="2c343-112">The group is scheduled on a single host machine.</span></span>
- <span data-ttu-id="2c343-113">Grubun tek bir ortak IP adresi, bir kullanıma sunulan bağlantı noktası ile kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="2c343-113">The group exposes a single public IP address, with one exposed port.</span></span>
- <span data-ttu-id="2c343-114">Grup iki kapsayıcıları için yapılır.</span><span class="sxs-lookup"><span data-stu-id="2c343-114">The group is made up of two containers.</span></span> <span data-ttu-id="2c343-115">Bağlantı noktası 80 sırasında diğer dinlediği bağlantı noktası 5000 bir kapsayıcı dinler.</span><span class="sxs-lookup"><span data-stu-id="2c343-115">One container listens on port 80, while the other listens on port 5000.</span></span>
- <span data-ttu-id="2c343-116">İki Azure dosya paylaşımları birim başlatmalar olarak grubu içerir ve her kapsayıcı paylaşımları yerel olarak birini bağlar.</span><span class="sxs-lookup"><span data-stu-id="2c343-116">The group includes two Azure file shares as volume mounts, and each container mounts one of the shares locally.</span></span>

### <a name="networking"></a><span data-ttu-id="2c343-117">Ağ</span><span class="sxs-lookup"><span data-stu-id="2c343-117">Networking</span></span>

<span data-ttu-id="2c343-118">Kapsayıcı grupları, bir IP adresi ve bağlantı noktası ad alanı, IP adresi üzerinde paylaşır.</span><span class="sxs-lookup"><span data-stu-id="2c343-118">Container groups share an IP address and a port namespace on that IP address.</span></span> <span data-ttu-id="2c343-119">Grup içindeki bir kapsayıcı erişmek dış istemcileri etkinleştirmek için bağlantı noktası üzerinde IP adresi ve kapsayıcısından kullanıma gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c343-119">To enable external clients to reach a container within the group, you must expose the port on the IP address and from the container.</span></span> <span data-ttu-id="2c343-120">Grup kapsayıcılara bir bağlantı noktası ad alanı paylaştığından, bağlantı noktası eşlemesi desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="2c343-120">Because containers within the group share a port namespace, port mapping is not supported.</span></span> <span data-ttu-id="2c343-121">Bu bağlantı noktalarını grubun IP adresinde dışarıdan gösterilmeyen olsa bile bir grup kapsayıcılara bunlar sunulan bağlantı noktalarında localhost aracılığıyla birbirine ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c343-121">Containers within a group can reach each other via localhost on the ports that they have exposed, even if those ports are not exposed externally on the group's IP address.</span></span>

### <a name="storage"></a><span data-ttu-id="2c343-122">Depolama</span><span class="sxs-lookup"><span data-stu-id="2c343-122">Storage</span></span>

<span data-ttu-id="2c343-123">İçindeki bir kapsayıcı grubun bağlamak için dış birimleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c343-123">You can specify external volumes to mount within a container group.</span></span> <span data-ttu-id="2c343-124">Tek bir grup kapsayıcılarında içindeki belirli yollara içine bu birimlerin eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c343-124">You can map those volumes into specific paths within the individual containers in a group.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="2c343-125">Genel senaryolar</span><span class="sxs-lookup"><span data-stu-id="2c343-125">Common scenarios</span></span>

<span data-ttu-id="2c343-126">Birden çok kapsayıcı grupları tek bir işlev görev farklı ekip tarafından alınabilir ve ayrı kaynak gereksinimlerini kapsayıcı görüntüleri az sayıda içine bölmek istediğiniz durumlarda kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="2c343-126">Multi-container groups are useful in cases where you want to divide up a single functional task into a small number of container images, which can be delivered by different teams and have separate resource requirements.</span></span> <span data-ttu-id="2c343-127">Örnek Kullanım dahil olabilir:</span><span class="sxs-lookup"><span data-stu-id="2c343-127">Example usage could include:</span></span>

- <span data-ttu-id="2c343-128">Bir uygulama kapsayıcısı ve günlüğe kaydetme kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="2c343-128">An application container and a logging container.</span></span> <span data-ttu-id="2c343-129">Günlüğe kaydetme kapsayıcısı ana uygulama tarafından çıktısı günlükler ve ölçümleri toplar ve uzun vadeli depolama için yazar.</span><span class="sxs-lookup"><span data-stu-id="2c343-129">The logging container collects the logs and metrics output by the main application and writes them to long-term storage.</span></span>
- <span data-ttu-id="2c343-130">Bir uygulama ve izleme kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="2c343-130">An application and a monitoring container.</span></span> <span data-ttu-id="2c343-131">İzleme kapsayıcı düzenli aralıklarla çalıştığını ve düzgün yanıt ve değilse bir uyarı başlatır emin olmak için uygulamaya istekte bulunur.</span><span class="sxs-lookup"><span data-stu-id="2c343-131">The monitoring container periodically makes a request to the application to ensure that it's running and responding correctly and raises an alert if it's not.</span></span>
- <span data-ttu-id="2c343-132">Bir web uygulaması hizmet veren bir kapsayıcı ve en yeni içerik kaynak denetiminden çekme kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="2c343-132">A container serving a web application and a container pulling the latest content from source control.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c343-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2c343-133">Next steps</span></span>

<span data-ttu-id="2c343-134">Bilgi nasıl [çok kapsayıcı grubu dağıtma](container-instances-multi-container-group.md) bir Azure Resource Manager şablonu ile.</span><span class="sxs-lookup"><span data-stu-id="2c343-134">Learn how to [deploy a multi-container group](container-instances-multi-container-group.md) with an Azure Resource Manager template.</span></span>

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png