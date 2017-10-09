---
title: "Azure kapsayıcı hizmeti için aaaDC/OS aracısı havuzları | Microsoft Docs"
description: "Merhaba ortak ve özel aracı havuzları, Azure kapsayıcı hizmeti DC/OS kümesi ile nasıl çalışır?"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Kapsayıcılar, Mikro hizmetler, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: c7d3889db07cb9908e8b68b668bd8a14ef3c2552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a><span data-ttu-id="e9639-104">Azure kapsayıcı hizmeti DC/OS aracısı havuzları</span><span class="sxs-lookup"><span data-stu-id="e9639-104">DC/OS agent pools for Azure Container Service</span></span>
<span data-ttu-id="e9639-105">Azure kapsayıcı hizmeti DC/OS kümelerde iki havuzları, ortak bir havuzu ve özel bir havuzu Aracısı düğümleri içerir.</span><span class="sxs-lookup"><span data-stu-id="e9639-105">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span></span> <span data-ttu-id="e9639-106">Bir uygulama dağıtılabilir kapsayıcı hizmetiniz makinelerinizde arasında erişilebilirlik etkileyen tooeither havuzu.</span><span class="sxs-lookup"><span data-stu-id="e9639-106">An application can be deployed tooeither pool, affecting accessibility between machines in your container service.</span></span> <span data-ttu-id="e9639-107">Merhaba makineler gösterilen toohello olabilir Internet (Genel) veya dahili (özel) tutulur.</span><span class="sxs-lookup"><span data-stu-id="e9639-107">hello machines can be exposed toohello internet (public) or kept internal (private).</span></span> <span data-ttu-id="e9639-108">Bu makalede vardır neden ortak ve özel havuzları kısa bir genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="e9639-108">This article gives a brief overview of why there are public and private pools.</span></span>


* <span data-ttu-id="e9639-109">**Özel aracılar**: özel aracı düğümleri yönlendirilemeyen bir ağ üzerinden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e9639-109">**Private agents**: Private agent nodes run through a non-routable network.</span></span> <span data-ttu-id="e9639-110">Bu ağ, yalnızca hello yönetici bölgeden veya hello genel bölge sınır yönlendiricisi aracılığıyla erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="e9639-110">This network is only accessible from hello admin zone or through hello public zone edge router.</span></span> <span data-ttu-id="e9639-111">Varsayılan olarak, DC/OS özel aracı düğümlerde uygulamaları başlatır.</span><span class="sxs-lookup"><span data-stu-id="e9639-111">By default, DC/OS launches apps on private agent nodes.</span></span> 

* <span data-ttu-id="e9639-112">**Ortak aracıları**: ortak aracı düğümleri, genel olarak erişilebilir bir ağ üzerinden DC/OS uygulamaları ve Hizmetleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e9639-112">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span></span> 

<span data-ttu-id="e9639-113">DC/OS ağ güvenliği hakkında daha fazla bilgi için bkz: Merhaba [DC/OS belgelerine](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span><span class="sxs-lookup"><span data-stu-id="e9639-113">For more information about DC/OS network security, see hello [DC/OS documentation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span></span>

## <a name="deploy-agent-pools"></a><span data-ttu-id="e9639-114">Aracı havuzu dağıtma</span><span class="sxs-lookup"><span data-stu-id="e9639-114">Deploy agent pools</span></span>

<span data-ttu-id="e9639-115">Merhaba DC/OS aracısı havuzları, Azure kapsayıcı hizmeti şu şekilde oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="e9639-115">hello DC/OS agent pools In Azure Container Service are created as follows:</span></span>

* <span data-ttu-id="e9639-116">Merhaba **özel havuzu** ne zaman belirtin Aracısı düğümleri hello sayısını içerir, [hello DC/OS kümesi dağıtma](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="e9639-116">hello **private pool** contains hello number of agent nodes that you specify when you [deploy hello DC/OS cluster](container-service-deployment.md).</span></span> 

* <span data-ttu-id="e9639-117">Merhaba **ortak havuzu** başlangıçta Aracısı düğümleri sayısı önceden belirlenmiştir içerir.</span><span class="sxs-lookup"><span data-stu-id="e9639-117">hello **public pool** initially contains a predetermined number of agent nodes.</span></span> <span data-ttu-id="e9639-118">Merhaba DC/OS kümesi sağlandığında bu havuzu otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="e9639-118">This pool is added automatically when hello DC/OS cluster is provisioned.</span></span>

<span data-ttu-id="e9639-119">Merhaba özel havuzu ve hello ortak havuzu Azure sanal makine ölçek kümeleridir.</span><span class="sxs-lookup"><span data-stu-id="e9639-119">hello private pool and hello public pool are Azure virtual machine scale sets.</span></span> <span data-ttu-id="e9639-120">Dağıtımdan sonra bu havuzlarını yeniden boyutlandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9639-120">You can resize these pools after deployment.</span></span>

## <a name="use-agent-pools"></a><span data-ttu-id="e9639-121">Aracı havuzlarını kullanın</span><span class="sxs-lookup"><span data-stu-id="e9639-121">Use agent pools</span></span>
<span data-ttu-id="e9639-122">Varsayılan olarak, **Marathon** herhangi yeni uygulama toohello dağıtır *özel* Aracısı düğümleri.</span><span class="sxs-lookup"><span data-stu-id="e9639-122">By default, **Marathon** deploys any new application toohello *private* agent nodes.</span></span> <span data-ttu-id="e9639-123">Merhaba uygulama toohello dağıtmak tooexplicitly sahip *ortak* Merhaba uygulaması hello oluşturulması sırasında düğüm.</span><span class="sxs-lookup"><span data-stu-id="e9639-123">You have tooexplicitly deploy hello application toohello *public* nodes during hello creation of hello application.</span></span> <span data-ttu-id="e9639-124">Select hello **isteğe bağlı** sekmesinde ve girin **slave_public** hello için **kabul edilen kaynak rolleri** değeri.</span><span class="sxs-lookup"><span data-stu-id="e9639-124">Select hello **Optional** tab and enter **slave_public** for hello **Accepted Resource Roles** value.</span></span> <span data-ttu-id="e9639-125">Bu işlem belgelenen [burada](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) ve hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="e9639-125">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9639-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e9639-126">Next steps</span></span>
* <span data-ttu-id="e9639-127">Daha fazla bilgi edinin [DC/OS kapsayıcılarınızı yönetme](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="e9639-127">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

* <span data-ttu-id="e9639-128">Nasıl çok öğrenin[hello Güvenlik Duvarı'nı açın](container-service-enable-public-access.md) Azure tooallow genel erişim tooyour DC/OS kapsayıcıları tarafından sağlanan.</span><span class="sxs-lookup"><span data-stu-id="e9639-128">Learn how too[open hello firewall](container-service-enable-public-access.md) provided by Azure tooallow public access tooyour DC/OS containers.</span></span>

