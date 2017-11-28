---
title: "Azure kapsayıcı hizmeti DC/OS Aracısı havuzlarında | Microsoft Docs"
description: "Ortak ve özel aracı havuzları, Azure kapsayıcı hizmeti DC/OS kümesi ile nasıl çalışır?"
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
ms.openlocfilehash: da4a196b1a73c78dfff7d8310edcc349b8d10665
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a><span data-ttu-id="6ab6c-104">Azure kapsayıcı hizmeti DC/OS aracısı havuzları</span><span class="sxs-lookup"><span data-stu-id="6ab6c-104">DC/OS agent pools for Azure Container Service</span></span>
<span data-ttu-id="6ab6c-105">Azure kapsayıcı hizmeti DC/OS kümelerde iki havuzları, ortak bir havuzu ve özel bir havuzu Aracısı düğümleri içerir.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-105">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span></span> <span data-ttu-id="6ab6c-106">Bir uygulama ya da havuzuna kapsayıcı hizmetiniz makinelerinizde arasında erişilebilirlik etkileyen dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-106">An application can be deployed to either pool, affecting accessibility between machines in your container service.</span></span> <span data-ttu-id="6ab6c-107">Makineler (Genel) Internet'e açık veya dahili (özel) tutulur.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-107">The machines can be exposed to the internet (public) or kept internal (private).</span></span> <span data-ttu-id="6ab6c-108">Bu makalede vardır neden ortak ve özel havuzları kısa bir genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-108">This article gives a brief overview of why there are public and private pools.</span></span>


* <span data-ttu-id="6ab6c-109">**Özel aracılar**: özel aracı düğümleri yönlendirilemeyen bir ağ üzerinden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-109">**Private agents**: Private agent nodes run through a non-routable network.</span></span> <span data-ttu-id="6ab6c-110">Bu ağ, yalnızca yönetici bölgeden veya genel bölge sınır yönlendiricisi aracılığıyla erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-110">This network is only accessible from the admin zone or through the public zone edge router.</span></span> <span data-ttu-id="6ab6c-111">Varsayılan olarak, DC/OS özel aracı düğümlerde uygulamaları başlatır.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-111">By default, DC/OS launches apps on private agent nodes.</span></span> 

* <span data-ttu-id="6ab6c-112">**Ortak aracıları**: ortak aracı düğümleri, genel olarak erişilebilir bir ağ üzerinden DC/OS uygulamaları ve Hizmetleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-112">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span></span> 

<span data-ttu-id="6ab6c-113">DC/OS ağ güvenliği hakkında daha fazla bilgi için bkz: [DC/OS belgelerine](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-113">For more information about DC/OS network security, see the [DC/OS documentation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span></span>

## <a name="deploy-agent-pools"></a><span data-ttu-id="6ab6c-114">Aracı havuzu dağıtma</span><span class="sxs-lookup"><span data-stu-id="6ab6c-114">Deploy agent pools</span></span>

<span data-ttu-id="6ab6c-115">Azure kapsayıcı hizmeti DC/OS aracısı havuzları şu şekilde oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="6ab6c-115">The DC/OS agent pools In Azure Container Service are created as follows:</span></span>

* <span data-ttu-id="6ab6c-116">**Özel havuzu** ne zaman belirtin Aracısı düğüm sayısını içerir, [DC/OS kümesi dağıtma](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-116">The **private pool** contains the number of agent nodes that you specify when you [deploy the DC/OS cluster](container-service-deployment.md).</span></span> 

* <span data-ttu-id="6ab6c-117">**Ortak havuzu** başlangıçta Aracısı düğümleri sayısı önceden belirlenmiştir içerir.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-117">The **public pool** initially contains a predetermined number of agent nodes.</span></span> <span data-ttu-id="6ab6c-118">DC/OS kümesi sağlandığında bu havuzu otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-118">This pool is added automatically when the DC/OS cluster is provisioned.</span></span>

<span data-ttu-id="6ab6c-119">Özel havuzu ve ortak havuzu Azure sanal makine ölçek kümeleridir.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-119">The private pool and the public pool are Azure virtual machine scale sets.</span></span> <span data-ttu-id="6ab6c-120">Dağıtımdan sonra bu havuzlarını yeniden boyutlandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-120">You can resize these pools after deployment.</span></span>

## <a name="use-agent-pools"></a><span data-ttu-id="6ab6c-121">Aracı havuzlarını kullanın</span><span class="sxs-lookup"><span data-stu-id="6ab6c-121">Use agent pools</span></span>
<span data-ttu-id="6ab6c-122">Varsayılan olarak, **Marathon** herhangi yeni bir uygulama dağıtır *özel* Aracısı düğümleri.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-122">By default, **Marathon** deploys any new application to the *private* agent nodes.</span></span> <span data-ttu-id="6ab6c-123">Açıkça uygulamayı dağıtmak zorunda *ortak* uygulama oluşturulması sırasında düğüm.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-123">You have to explicitly deploy the application to the *public* nodes during the creation of the application.</span></span> <span data-ttu-id="6ab6c-124">Seçin **isteğe bağlı** sekmesinde ve girin **slave_public** için **kabul edilen kaynak rolleri** değeri.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-124">Select the **Optional** tab and enter **slave_public** for the **Accepted Resource Roles** value.</span></span> <span data-ttu-id="6ab6c-125">Bu işlem belgelenen [burada](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) ve [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-125">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in the [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ab6c-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6ab6c-126">Next steps</span></span>
* <span data-ttu-id="6ab6c-127">Daha fazla bilgi edinin [DC/OS kapsayıcılarınızı yönetme](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-127">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

* <span data-ttu-id="6ab6c-128">Bilgi nasıl [Güvenlik Duvarı](container-service-enable-public-access.md) DC/OS kapsayıcılarınızı ortak erişmesine izin vermek için Azure tarafından sağlanan.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-128">Learn how to [open the firewall](container-service-enable-public-access.md) provided by Azure to allow public access to your DC/OS containers.</span></span>

