---
title: "aaaAzure kapsayıcı kayıt defteri depoları | Microsoft Docs"
description: "Nasıl toouse Azure kapsayıcı kayıt defteri depoları Docker görüntüleri"
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
ms.openlocfilehash: 06172a63465838a78a607f268da116d8158789ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="52721-103">Azure kapsayıcı kayıt defteri depoları</span><span class="sxs-lookup"><span data-stu-id="52721-103">Azure container registry repositories</span></span>

<span data-ttu-id="52721-104">Azure kapsayıcı kayıt defterleri, hizmetleri ve orchestrators birçok ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="52721-104">Azure Container Registries are compatible with a multitude of services and orchestrators.</span></span> <span data-ttu-id="52721-105">toomake bunu daha kolay tootrack hello kaynak hizmet ve aracılarının içinden ACR kullanılır, biz başlatıldı hello Docker.config dosyasında hello Docker üstbilgi alanı kullanma.</span><span class="sxs-lookup"><span data-stu-id="52721-105">toomake it easier tootrack hello source services and agents from which ACR is used, we have started using hello Docker header field in hello Docker.config file.</span></span>



## <a name="viewing-repositories-in-hello-portal"></a><span data-ttu-id="52721-106">Depoları hello Portal görüntüleme</span><span class="sxs-lookup"><span data-stu-id="52721-106">Viewing repositories in hello Portal</span></span>

<span data-ttu-id="52721-107">Merhaba ACR üstbilgileri hello biçimi izleyin:</span><span class="sxs-lookup"><span data-stu-id="52721-107">hello ACR headers follow hello format:</span></span>
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* <span data-ttu-id="52721-108">Bulut: Azure, Azure yığın veya diğer kamu veya Ülkeye özel Azure bulut.</span><span class="sxs-lookup"><span data-stu-id="52721-108">Cloud: Azure, Azure Stack, or other government or country-specific Azure clouds.</span></span> <span data-ttu-id="52721-109">Azure yığını ve kamu Bulutlar şu anda desteklenmemektedir karşın, bu parametre gelecekteki destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="52721-109">Although Azure Stack and government clouds are not currently supported, this parameter enables future support.</span></span>
* <span data-ttu-id="52721-110">Hizmet: hello hizmetin adı.</span><span class="sxs-lookup"><span data-stu-id="52721-110">Service: name of hello service.</span></span>
* <span data-ttu-id="52721-111">Optionalservicename: isteğe bağlı bir parametre alt Servisleri veya toospecify bir SKU hizmetler için (örn: web uygulamaları Azure/app-service/web-apps ile karşılık gelir).</span><span class="sxs-lookup"><span data-stu-id="52721-111">Optionalservicename: optional parameter for services with subservices, or toospecify a SKU (ex: web apps correspond with Azure/app-service/web-apps).</span></span>

<span data-ttu-id="52721-112">İş ortağı Hizmetleri ve orchestrators kullanmaları toouse özel üstbilgi değerleri toohelp bizim telemetri ile markalarıdır.</span><span class="sxs-lookup"><span data-stu-id="52721-112">Partner services and orchestrators are encouraged toouse specific header values toohelp with our telemetry.</span></span> <span data-ttu-id="52721-113">Kullanıcılar, böylece isterlerse toohello üstbilgi geçirilen hello değeri değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52721-113">Users can also modify hello value passed toohello header if they so desire.</span></span>

<span data-ttu-id="52721-114">Aşağıda ACR ortakları toouse toopopulate hello "X-Meta-kaynak-Client" alan istiyoruz hello değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="52721-114">hello values we want ACR partners toouse toopopulate hello "X-Meta-Source-Client" field are below:</span></span>

| <span data-ttu-id="52721-115">Hizmet Adı</span><span class="sxs-lookup"><span data-stu-id="52721-115">Service Name</span></span>              | <span data-ttu-id="52721-116">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="52721-116">Header</span></span>                                |
| ------------------------- | ------------------------------------- |
| <span data-ttu-id="52721-117">Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="52721-117">Azure Container Service</span></span>   | <span data-ttu-id="52721-118">Azure/işlem/azure-kapsayıcı-hizmeti</span><span class="sxs-lookup"><span data-stu-id="52721-118">azure/compute/azure-container-service</span></span> |
| <span data-ttu-id="52721-119">Uygulama hizmeti - Web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="52721-119">App Service - Web Apps</span></span>    | <span data-ttu-id="52721-120">Azure/app-service/web-apps</span><span class="sxs-lookup"><span data-stu-id="52721-120">azure/app-service/web-apps</span></span>            |
| <span data-ttu-id="52721-121">Uygulama hizmeti - Logic Apps</span><span class="sxs-lookup"><span data-stu-id="52721-121">App Service - Logic Apps</span></span>  | <span data-ttu-id="52721-122">Azure/app-service/logic-apps</span><span class="sxs-lookup"><span data-stu-id="52721-122">azure/app-service/logic-apps</span></span>          |
| <span data-ttu-id="52721-123">Batch</span><span class="sxs-lookup"><span data-stu-id="52721-123">Batch</span></span>                     | <span data-ttu-id="52721-124">işlem/Azure/toplu</span><span class="sxs-lookup"><span data-stu-id="52721-124">azure/compute/batch</span></span>                   |
| <span data-ttu-id="52721-125">Bulut konsol</span><span class="sxs-lookup"><span data-stu-id="52721-125">Cloud Console</span></span>             | <span data-ttu-id="52721-126">Bulut/Azure-konsol</span><span class="sxs-lookup"><span data-stu-id="52721-126">azure/cloud-console</span></span>                   |
| <span data-ttu-id="52721-127">İşlevler</span><span class="sxs-lookup"><span data-stu-id="52721-127">Functions</span></span>                 | <span data-ttu-id="52721-128">işlem/Azure/işlevleri</span><span class="sxs-lookup"><span data-stu-id="52721-128">azure/compute/functions</span></span>               |
| <span data-ttu-id="52721-129">Nesnelerin interneti - Hub</span><span class="sxs-lookup"><span data-stu-id="52721-129">Internet of Things - Hub</span></span>  | <span data-ttu-id="52721-130">IOT/Azure/hub</span><span class="sxs-lookup"><span data-stu-id="52721-130">azure/iot/hub</span></span>                         |
| <span data-ttu-id="52721-131">HDInsight</span><span class="sxs-lookup"><span data-stu-id="52721-131">HDInsight</span></span>                 | <span data-ttu-id="52721-132">Veri/Azure/hdınsight</span><span class="sxs-lookup"><span data-stu-id="52721-132">azure/data/hdinsight</span></span>                  |
| <span data-ttu-id="52721-133">Jenkins</span><span class="sxs-lookup"><span data-stu-id="52721-133">Jenkins</span></span>                   | <span data-ttu-id="52721-134">Azure/jenkins</span><span class="sxs-lookup"><span data-stu-id="52721-134">azure/jenkins</span></span>                         |
| <span data-ttu-id="52721-135">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="52721-135">Machine Learning</span></span>          | <span data-ttu-id="52721-136">Azure/data/machile-öğrenme</span><span class="sxs-lookup"><span data-stu-id="52721-136">azure/data/machile-learning</span></span>           |
| <span data-ttu-id="52721-137">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="52721-137">Service Fabric</span></span>            | <span data-ttu-id="52721-138">Azure/işlem/service-yapı</span><span class="sxs-lookup"><span data-stu-id="52721-138">azure/compute/service-fabric</span></span>          |
| <span data-ttu-id="52721-139">VSTS</span><span class="sxs-lookup"><span data-stu-id="52721-139">VSTS</span></span>                      | <span data-ttu-id="52721-140">Azure/vsts</span><span class="sxs-lookup"><span data-stu-id="52721-140">azure/vsts</span></span>                            |


## <a name="next-steps"></a><span data-ttu-id="52721-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="52721-141">Next steps</span></span>
[<span data-ttu-id="52721-142">Kayıt defterleri, desteklenen hello hizmetler ve orchestrators hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="52721-142">Learn more about registries and hello supported services and orchestrators</span></span>](container-registry-intro.md)
