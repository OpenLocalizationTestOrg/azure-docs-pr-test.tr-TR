---
title: "aaaIntroduction tooAzure Kubernetes için kapsayıcı hizmeti | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Kubernetes için basit toodeploy kolaylaştırır ve Azure kapsayıcı tabanlı uygulamayı yönetin."
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kubernetes, Docker, Kapsayıcılar, Mikro Hizmetler, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a><span data-ttu-id="acda4-104">Giriş tooAzure Kubernetes için kapsayıcı hizmeti</span><span class="sxs-lookup"><span data-stu-id="acda4-104">Introduction tooAzure Container Service for Kubernetes</span></span>
<span data-ttu-id="acda4-105">Azure kapsayıcı hizmeti Kubernetes için basit toocreate kolaylaştırır, yapılandırabilir ve küme sanal makinelerin kapsayıcılı önceden yapılandırılmış toorun uygulamaları yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acda4-105">Azure Container Service for Kubernetes makes it simple toocreate, configure, and manage a cluster of virtual machines that are preconfigured toorun containerized applications.</span></span> <span data-ttu-id="acda4-106">Bu, toouse varolan yeteneklerinizi sağlar veya topluluk uzmanlık toodeploy büyük ve artan gövde çizme ve Microsoft Azure üzerinde kapsayıcı tabanlı uygulamalar yönetin.</span><span class="sxs-lookup"><span data-stu-id="acda4-106">This enables you toouse your existing skills, or draw upon a large and growing body of community expertise, toodeploy and manage container-based applications on Microsoft Azure.</span></span>

<span data-ttu-id="acda4-107">Azure kapsayıcı hizmeti kullanarak, hello Azure, kurumsal düzeyde özelliklerini hala Kubernetes aracılığıyla uygulama taşınabilirliği korurken yararlanmak ve Docker görüntü biçimi hello.</span><span class="sxs-lookup"><span data-stu-id="acda4-107">By using Azure Container Service, you can take advantage of hello enterprise-grade features of Azure, while still maintaining application portability through Kubernetes and hello Docker image format.</span></span>

## <a name="using-azure-container-service-for-kubernetes"></a><span data-ttu-id="acda4-108">Kubernetes için Azure Container Service’i Kullanma</span><span class="sxs-lookup"><span data-stu-id="acda4-108">Using Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="acda4-109">Amacımız Azure kapsayıcı hizmeti ile tooprovide bir kapsayıcı barındırma ortamı açık kaynaklı araçları ve bugün müşterilerimizin arasında popüler teknolojileri kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="acda4-109">Our goal with Azure Container Service is tooprovide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span></span> <span data-ttu-id="acda4-110">toothis son biz hello standart Kubernetes API uç noktalarını kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="acda4-110">toothis end, we expose hello standard Kubernetes API endpoints.</span></span> <span data-ttu-id="acda4-111">Bu standart uç noktaları kullanarak tooa Kubernetes küme Konuşmayı yeteneğine sahip herhangi bir yazılım yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acda4-111">By using these standard endpoints, you can leverage any software that is capable of talking tooa Kubernetes cluster.</span></span> <span data-ttu-id="acda4-112">Örneğin [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/) veya [draft](https://github.com/Azure/draft) arasından seçim yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acda4-112">For example, you might choose [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), or [draft](https://github.com/Azure/draft).</span></span>

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a><span data-ttu-id="acda4-113">Azure Container Service kullanan bir Kubernetes kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="acda4-113">Creating a Kubernetes cluster using Azure Container Service</span></span>
<span data-ttu-id="acda4-114">Azure kapsayıcı hizmeti kullanarak toobegin hello ile Azure kapsayıcı hizmeti kümesini dağıtma [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) veya hello Portalı aracılığıyla (arama hello Market için **Azure kapsayıcı hizmeti**).</span><span class="sxs-lookup"><span data-stu-id="acda4-114">toobegin using Azure Container Service, deploy an Azure Container Service cluster with hello [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) or via hello portal (search hello Marketplace for **Azure Container Service**).</span></span> <span data-ttu-id="acda4-115">Hello Azure Resource Manager şablonları hakkında daha fazla denetime gereksinim duyan İleri düzey bir kullanıcı varsa, hello açık kaynak kullanabilirsiniz [acs altyapısı](https://github.com/Azure/acs-engine) proje toobuild kendi özel Kubernetes küme ve hello dağıtma `az` CLI.</span><span class="sxs-lookup"><span data-stu-id="acda4-115">If you are an advanced user who needs more control over hello Azure Resource Manager templates, you can use hello open source [acs-engine](https://github.com/Azure/acs-engine) project toobuild your own custom Kubernetes cluster and deploy it via hello `az` CLI.</span></span>

### <a name="using-kubernetes"></a><span data-ttu-id="acda4-116">Kubernetes kullanma</span><span class="sxs-lookup"><span data-stu-id="acda4-116">Using Kubernetes</span></span>
<span data-ttu-id="acda4-117">Kubernetes, kapsayıcılı uygulamaların dağıtımını, ölçeklendirmesini ve yönetimini otomatikleştirir.</span><span class="sxs-lookup"><span data-stu-id="acda4-117">Kubernetes automates deployment, scaling, and management of containerized applications.</span></span> <span data-ttu-id="acda4-118">Aşağıdaki zengin özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="acda4-118">It has a rich set of features including:</span></span>
* <span data-ttu-id="acda4-119">Otomatik bin paketleme</span><span class="sxs-lookup"><span data-stu-id="acda4-119">Automatic binpacking</span></span>
* <span data-ttu-id="acda4-120">Kendi kendini iyileştirme</span><span class="sxs-lookup"><span data-stu-id="acda4-120">Self-healing</span></span>
* <span data-ttu-id="acda4-121">Yatay ölçekleme</span><span class="sxs-lookup"><span data-stu-id="acda4-121">Horizontal scaling</span></span>
* <span data-ttu-id="acda4-122">Hizmet bulma ve yük dengeleme</span><span class="sxs-lookup"><span data-stu-id="acda4-122">Service discovery and load balancing</span></span>
* <span data-ttu-id="acda4-123">Otomatik piyasaya çıkarma ve geri alma işlemleri</span><span class="sxs-lookup"><span data-stu-id="acda4-123">Automated rollouts and rollbacks</span></span>
* <span data-ttu-id="acda4-124">Gizli dizi ve yapılandırma yönetimi</span><span class="sxs-lookup"><span data-stu-id="acda4-124">Secret and configuration management</span></span>
* <span data-ttu-id="acda4-125">Depolama düzenleme</span><span class="sxs-lookup"><span data-stu-id="acda4-125">Storage orchestration</span></span>
* <span data-ttu-id="acda4-126">Toplu iş yürütme</span><span class="sxs-lookup"><span data-stu-id="acda4-126">Batch execution</span></span>

<span data-ttu-id="acda4-127">Azure Container Service aracılığıyla dağıtılan Kubernetes mimari diyagramı:</span><span class="sxs-lookup"><span data-stu-id="acda4-127">Architectural diagram of Kubernetes deployed via Azure Container Service:</span></span>

![Azure kapsayıcı hizmeti toouse Kubernetes yapılandırılmış.](media/acs-intro/kubernetes.png)

## <a name="videos"></a><span data-ttu-id="acda4-129">Videolar</span><span class="sxs-lookup"><span data-stu-id="acda4-129">Videos</span></span>

<span data-ttu-id="acda4-130">Azure Container Services'daki Kubernetes Desteği (Azure Friday, Ocak 2017):</span><span class="sxs-lookup"><span data-stu-id="acda4-130">Kubernetes Support in Azure Container Services (Azure Friday, January 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

<span data-ttu-id="acda4-131">Kubernetes’te Uygulama Geliştirme ve Dağıtma Araçları (Azure OpenDev, Haziran 2017):</span><span class="sxs-lookup"><span data-stu-id="acda4-131">Tools for Developing and Deploying Applications on Kubernetes (Azure OpenDev, June 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a><span data-ttu-id="acda4-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="acda4-132">Next steps</span></span>

<span data-ttu-id="acda4-133">Merhaba keşfedin [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) Azure kapsayıcı hizmeti bugün keşfetme toobegin.</span><span class="sxs-lookup"><span data-stu-id="acda4-133">Explore hello [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin exploring Azure Container Service today.</span></span>
