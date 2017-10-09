---
title: "aaaAzure Danışmanı performans önerileri | Microsoft Docs"
description: "Advisor toooptimize hello Azure dağıtımlarınızı performansını kullanın."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: eb3d928664717f6f322132ac740f42015f56b76e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-performance-recommendations"></a><span data-ttu-id="a9f73-103">Advisor performans önerileri</span><span class="sxs-lookup"><span data-stu-id="a9f73-103">Advisor Performance recommendations</span></span>

<span data-ttu-id="a9f73-104">Azure Danışmanı performans önerileri hello hızı ve kritik iş uygulamalarının yanıtlama hızını geliştirilmesine yardımcı olun.</span><span class="sxs-lookup"><span data-stu-id="a9f73-104">Azure Advisor performance recommendations help improve hello speed and responsiveness of your business-critical applications.</span></span> <span data-ttu-id="a9f73-105">Merhaba üzerinde danışmanına performans önerileri alabilirsiniz **performans** hello Danışmanı Pano sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a9f73-105">You can get performance recommendations from Advisor on hello **Performance** tab of hello Advisor dashboard.</span></span>

![Advisor performans sekmesi](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a><span data-ttu-id="a9f73-107">SQL DB Danışmanı ile veritabanı performansı</span><span class="sxs-lookup"><span data-stu-id="a9f73-107">Improve database performance with SQL DB Advisor</span></span>

<span data-ttu-id="a9f73-108">Advisor önerileri tüm Azure kaynakları için tutarlı, birleştirilmiş bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="a9f73-108">Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="a9f73-109">Bu SQL veritabanı Danışmanı toobring ile SQL Azure veritabanı hello performansı artırmak için öneriler tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="a9f73-109">It integrates with SQL Database Advisor toobring you recommendations for improving hello performance of your SQL Azure database.</span></span> <span data-ttu-id="a9f73-110">SQL veritabanı Danışmanı'nı kullanım geçmişiniz çözümleyerek SQL Azure veritabanlarınızı hello performansını değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="a9f73-110">SQL Database Advisor assesses hello performance of your SQL Azure databases by analyzing your usage history.</span></span> <span data-ttu-id="a9f73-111">Ardından, hello veritabanının tipik iş yükünü çalıştırmak için en uygun öneriler sunar.</span><span class="sxs-lookup"><span data-stu-id="a9f73-111">It then offers recommendations that are best suited for running hello database’s typical workload.</span></span> 

> [!NOTE]
> <span data-ttu-id="a9f73-112">tooget öneriler, bir veritabanı kullanımı haftada hakkında sahip olması gerekir ve bu hafta içinde var. bazı tutarlı etkinlik olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9f73-112">tooget recommendations, a database must have about a week of usage, and within that week there must be some consistent activity.</span></span> <span data-ttu-id="a9f73-113">SQL veritabanı Danışmanı daha kolay rastgele WINS'e etkinlik için tutarlı bir sorgu modelleri için en iyi duruma getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9f73-113">SQL Database Advisor can optimize more easily for consistent query patterns than for random bursts of activity.</span></span>

<span data-ttu-id="a9f73-114">SQL Database Advisor hakkında daha fazla bilgi için bkz: [SQL veritabanı Danışmanı'nı](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span><span class="sxs-lookup"><span data-stu-id="a9f73-114">For more information about SQL Database Advisor, see [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span></span>

![SQL veritabanı önerileri](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a><span data-ttu-id="a9f73-116">Redis önbelleği performansı ve güvenilirliği iyileştirmek</span><span class="sxs-lookup"><span data-stu-id="a9f73-116">Improve Redis Cache performance and reliability</span></span>

<span data-ttu-id="a9f73-117">Advisor burada performansını olumsuz yönde yüksek bellek kullanımı, sunucu iş yükü, ağ bant genişliği veya çok sayıda istemci bağlantıları tarafından etkilenebilir Redis önbelleği örnekleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a9f73-117">Advisor identifies Redis Cache instances where performance may be adversely affected by high memory usage, server load, network bandwidth, or a large number of client connections.</span></span> <span data-ttu-id="a9f73-118">Danışmanı da iyi sağlar olası sorunları önlemek önerileri toohelp yöntemler.</span><span class="sxs-lookup"><span data-stu-id="a9f73-118">Advisor also provides best practices recommendations toohelp you avoid potential issues.</span></span> <span data-ttu-id="a9f73-119">Redis önbelleği öneriler hakkında daha fazla bilgi için bkz: [Redis önbelleği Danışmanı](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span><span class="sxs-lookup"><span data-stu-id="a9f73-119">For more information about Redis Cache recommendations, see [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span></span>


## <a name="improve-app-service-performance-and-reliability"></a><span data-ttu-id="a9f73-120">Uygulama hizmeti performans ve güvenilirlik geliştirmek</span><span class="sxs-lookup"><span data-stu-id="a9f73-120">Improve App Service performance and reliability</span></span>

<span data-ttu-id="a9f73-121">Azure Danışmanı uygulama hizmetleri deneyiminizi geliştirmek ve ilgili platform özelliklerini keşfetmek için en iyi uygulama önerilerini tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="a9f73-121">Azure Advisor integrates best practices recommendations for improving your App Services experience and discovering relevant platform capabilities.</span></span> <span data-ttu-id="a9f73-122">Uygulama Hizmetleri önerileri örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a9f73-122">Examples of App Services recommendations are:</span></span>
* <span data-ttu-id="a9f73-123">Algılama, bellek veya CPU kaynaklarını azaltma seçenekleri ile uygulama çalışma zamanları tarafından tükendiği örnekleri.</span><span class="sxs-lookup"><span data-stu-id="a9f73-123">Detection of instances where memory or CPU resources are exhausted by app runtimes with mitigation options.</span></span>
* <span data-ttu-id="a9f73-124">Burada collocating kaynakları web uygulamaları ve veritabanları gibi örneklerinin algılama, performans ve düşük maliyetli artırabilir.</span><span class="sxs-lookup"><span data-stu-id="a9f73-124">Detection of instances where collocating resources like web apps and databases can improve performance and lower cost.</span></span> 

<span data-ttu-id="a9f73-125">Uygulama Hizmetleri öneriler hakkında daha fazla bilgi için bkz: [Azure App Service için en iyi uygulamaları](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span><span class="sxs-lookup"><span data-stu-id="a9f73-125">For more information about App Services recommendations, see [Best Practices for Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span></span>
<span data-ttu-id="a9f73-126">![Uygulama Hizmetleri önerileri](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span><span class="sxs-lookup"><span data-stu-id="a9f73-126">![App Services recommendations](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span></span>

## <a name="how-tooaccess-performance-recommendations-in-advisor"></a><span data-ttu-id="a9f73-127">Nasıl tooaccess Danışmanı performans önerileri</span><span class="sxs-lookup"><span data-stu-id="a9f73-127">How tooaccess Performance recommendations in Advisor</span></span>

1. <span data-ttu-id="a9f73-128">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a9f73-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="a9f73-129">Merhaba sol bölmede **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="a9f73-129">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="a9f73-130">Hello menü bölmesi altında hizmet **izleme ve Yönetim**, tıklatın **Azure Danışmanı**.</span><span class="sxs-lookup"><span data-stu-id="a9f73-130">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="a9f73-131">Merhaba Danışmanı Panosu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a9f73-131">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="a9f73-132">Hello Danışmanı Panoda hello tıklatın **performans** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a9f73-132">On hello Advisor dashboard, click hello **Performance** tab.</span></span>

5. <span data-ttu-id="a9f73-133">Kendisi için tooreceive önerileri istediğiniz ve ardından hello aboneliği seçin **alma önerileri**.</span><span class="sxs-lookup"><span data-stu-id="a9f73-133">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="a9f73-134">tooaccess Advisor önerileri, şunları yapmalısınız ilk *aboneliğinizi kaydetmek* Danışmanı ile.</span><span class="sxs-lookup"><span data-stu-id="a9f73-134">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="a9f73-135">Bir abonelik kayıtlı olduğunda bir *abonelik sahibi* başlatır hello Danışmanı Pano ve tıklama hello **alma önerileri** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a9f73-135">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="a9f73-136">Bu bir *tek seferlik işlem*.</span><span class="sxs-lookup"><span data-stu-id="a9f73-136">This is a *one-time operation*.</span></span> <span data-ttu-id="a9f73-137">Merhaba abonelik kaydedildikten sonra Advisor önerileri olarak erişebilir *sahibi*, *katkıda bulunan*, veya *okuyucu* abonelik, bir kaynak grubu için veya bir belirli kaynak.</span><span class="sxs-lookup"><span data-stu-id="a9f73-137">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9f73-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a9f73-138">Next steps</span></span>

<span data-ttu-id="a9f73-139">Advisor önerileri hakkında daha fazla toolearn bakın:</span><span class="sxs-lookup"><span data-stu-id="a9f73-139">toolearn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="a9f73-140">Giriş tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="a9f73-140">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="a9f73-141">Danışman’ı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a9f73-141">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="a9f73-142">Advisor maliyet önerileri</span><span class="sxs-lookup"><span data-stu-id="a9f73-142">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="a9f73-143">Advisor yüksek kullanılabilirlik önerileri</span><span class="sxs-lookup"><span data-stu-id="a9f73-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="a9f73-144">Advisor güvenlik önerileri</span><span class="sxs-lookup"><span data-stu-id="a9f73-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)

