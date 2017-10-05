---
title: "Azure kapsayıcı kayıt defteri depoları | Microsoft Docs"
description: "Azure kapsayıcı kayıt defteri depoları için Docker görüntüleri kullanma"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: dd4feff057269ed7106990bb63eed7fcffa2dbec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="ff5bd-103">Azure kapsayıcı kayıt defteri depoları</span><span class="sxs-lookup"><span data-stu-id="ff5bd-103">Azure container registry repositories</span></span>

<span data-ttu-id="ff5bd-104">Azure kapsayıcı kayıt defterleri, hizmetleri ve orchestrators birçok ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="ff5bd-104">Azure Container Registries are compatible with a multitude of services and orchestrators.</span></span> <span data-ttu-id="ff5bd-105">ACR kullanıldığı aracıları ve kaynak hizmetleri izlemek kolaylaştırmak için biz Docker üstbilgi alanı Docker.config dosyasında kullanmaya.</span><span class="sxs-lookup"><span data-stu-id="ff5bd-105">To make it easier to track the source services and agents from which ACR is used, we have started using the Docker header field in the Docker.config file.</span></span>



## <a name="viewing-repositories-in-the-portal"></a><span data-ttu-id="ff5bd-106">Portalda depoları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="ff5bd-106">Viewing repositories in the Portal</span></span>

<span data-ttu-id="ff5bd-107">ACR üstbilgi biçimi izleyin:</span><span class="sxs-lookup"><span data-stu-id="ff5bd-107">The ACR headers follow the format:</span></span>
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* <span data-ttu-id="ff5bd-108">Bulut: Azure, Azure yığın veya diğer kamu veya Ülkeye özel Azure bulut.</span><span class="sxs-lookup"><span data-stu-id="ff5bd-108">Cloud: Azure, Azure Stack, or other government or country-specific Azure clouds.</span></span> <span data-ttu-id="ff5bd-109">Azure yığını ve kamu Bulutlar şu anda desteklenmemektedir karşın, bu parametre gelecekteki destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff5bd-109">Although Azure Stack and government clouds are not currently supported, this parameter enables future support.</span></span>
* <span data-ttu-id="ff5bd-110">Hizmet: hizmetin adını.</span><span class="sxs-lookup"><span data-stu-id="ff5bd-110">Service: name of the service.</span></span>
* <span data-ttu-id="ff5bd-111">Optionalservicename: isteğe bağlı bir parametre alt servisleri ile ya da bir SKU belirlemek için hizmetler için (örn: web uygulamaları Azure/app-service/web-apps ile karşılık gelir).</span><span class="sxs-lookup"><span data-stu-id="ff5bd-111">Optionalservicename: optional parameter for services with subservices, or to specify a SKU (ex: web apps correspond with Azure/app-service/web-apps).</span></span>

<span data-ttu-id="ff5bd-112">İş ortağı Hizmetleri ve orchestrators bizim telemetri ile yardımcı olmak için özel üstbilgi değerleri kullanmak için önerilir.</span><span class="sxs-lookup"><span data-stu-id="ff5bd-112">Partner services and orchestrators are encouraged to use specific header values to help with our telemetry.</span></span> <span data-ttu-id="ff5bd-113">Kullanıcılar, bu nedenle isterlerse başlığına geçirilen değeri değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff5bd-113">Users can also modify the value passed to the header if they so desire.</span></span>

<span data-ttu-id="ff5bd-114">"X-Meta-kaynak-Client" alanını doldurmak için kullanılacak ACR ortakları istiyoruz değerleri aşağıdaki şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ff5bd-114">The values we want ACR partners to use to populate the "X-Meta-Source-Client" field are below:</span></span>

| <span data-ttu-id="ff5bd-115">Hizmet Adı</span><span class="sxs-lookup"><span data-stu-id="ff5bd-115">Service Name</span></span>              | <span data-ttu-id="ff5bd-116">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="ff5bd-116">Header</span></span>                                |
| ------------------------- | ------------------------------------- |
| <span data-ttu-id="ff5bd-117">Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="ff5bd-117">Azure Container Service</span></span>   | <span data-ttu-id="ff5bd-118">Azure/işlem/azure-kapsayıcı-hizmeti</span><span class="sxs-lookup"><span data-stu-id="ff5bd-118">azure/compute/azure-container-service</span></span> |
| <span data-ttu-id="ff5bd-119">Uygulama hizmeti - Web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="ff5bd-119">App Service - Web Apps</span></span>    | <span data-ttu-id="ff5bd-120">Azure/app-service/web-apps</span><span class="sxs-lookup"><span data-stu-id="ff5bd-120">azure/app-service/web-apps</span></span>            |
| <span data-ttu-id="ff5bd-121">Uygulama hizmeti - Logic Apps</span><span class="sxs-lookup"><span data-stu-id="ff5bd-121">App Service - Logic Apps</span></span>  | <span data-ttu-id="ff5bd-122">Azure/app-service/logic-apps</span><span class="sxs-lookup"><span data-stu-id="ff5bd-122">azure/app-service/logic-apps</span></span>          |
| <span data-ttu-id="ff5bd-123">Batch</span><span class="sxs-lookup"><span data-stu-id="ff5bd-123">Batch</span></span>                     | <span data-ttu-id="ff5bd-124">işlem/Azure/toplu</span><span class="sxs-lookup"><span data-stu-id="ff5bd-124">azure/compute/batch</span></span>                   |
| <span data-ttu-id="ff5bd-125">Bulut konsol</span><span class="sxs-lookup"><span data-stu-id="ff5bd-125">Cloud Console</span></span>             | <span data-ttu-id="ff5bd-126">Bulut/Azure-konsol</span><span class="sxs-lookup"><span data-stu-id="ff5bd-126">azure/cloud-console</span></span>                   |
| <span data-ttu-id="ff5bd-127">İşlevler</span><span class="sxs-lookup"><span data-stu-id="ff5bd-127">Functions</span></span>                 | <span data-ttu-id="ff5bd-128">işlem/Azure/işlevleri</span><span class="sxs-lookup"><span data-stu-id="ff5bd-128">azure/compute/functions</span></span>               |
| <span data-ttu-id="ff5bd-129">Nesnelerin interneti - Hub</span><span class="sxs-lookup"><span data-stu-id="ff5bd-129">Internet of Things - Hub</span></span>  | <span data-ttu-id="ff5bd-130">IOT/Azure/hub</span><span class="sxs-lookup"><span data-stu-id="ff5bd-130">azure/iot/hub</span></span>                         |
| <span data-ttu-id="ff5bd-131">HDInsight</span><span class="sxs-lookup"><span data-stu-id="ff5bd-131">HDInsight</span></span>                 | <span data-ttu-id="ff5bd-132">Veri/Azure/hdınsight</span><span class="sxs-lookup"><span data-stu-id="ff5bd-132">azure/data/hdinsight</span></span>                  |
| <span data-ttu-id="ff5bd-133">Jenkins</span><span class="sxs-lookup"><span data-stu-id="ff5bd-133">Jenkins</span></span>                   | <span data-ttu-id="ff5bd-134">Azure/jenkins</span><span class="sxs-lookup"><span data-stu-id="ff5bd-134">azure/jenkins</span></span>                         |
| <span data-ttu-id="ff5bd-135">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ff5bd-135">Machine Learning</span></span>          | <span data-ttu-id="ff5bd-136">Azure/data/machile-öğrenme</span><span class="sxs-lookup"><span data-stu-id="ff5bd-136">azure/data/machile-learning</span></span>           |
| <span data-ttu-id="ff5bd-137">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ff5bd-137">Service Fabric</span></span>            | <span data-ttu-id="ff5bd-138">Azure/işlem/service-yapı</span><span class="sxs-lookup"><span data-stu-id="ff5bd-138">azure/compute/service-fabric</span></span>          |
| <span data-ttu-id="ff5bd-139">VSTS</span><span class="sxs-lookup"><span data-stu-id="ff5bd-139">VSTS</span></span>                      | <span data-ttu-id="ff5bd-140">Azure/vsts</span><span class="sxs-lookup"><span data-stu-id="ff5bd-140">azure/vsts</span></span>                            |


## <a name="next-steps"></a><span data-ttu-id="ff5bd-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ff5bd-141">Next steps</span></span>
[<span data-ttu-id="ff5bd-142">Kayıt defterleri ve desteklenen Hizmetleri ve orchestrators hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="ff5bd-142">Learn more about registries and the supported services and orchestrators</span></span>](container-registry-intro.md)
