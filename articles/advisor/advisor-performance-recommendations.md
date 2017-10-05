---
title: "Azure Danışmanı performans önerileri | Microsoft Docs"
description: "Azure dağıtımlarınızı performansını iyileştirmek için Danışmanı'nı kullanın."
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
ms.openlocfilehash: 5fb86c60b2d1f258dde5636ff8854b6f30f7f1c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-performance-recommendations"></a><span data-ttu-id="a7acb-103">Advisor performans önerileri</span><span class="sxs-lookup"><span data-stu-id="a7acb-103">Advisor Performance recommendations</span></span>

<span data-ttu-id="a7acb-104">Azure Danışmanı performans önerileri hızı ve kritik iş uygulamalarının yanıtlama hızını geliştirilmesine yardımcı olun.</span><span class="sxs-lookup"><span data-stu-id="a7acb-104">Azure Advisor performance recommendations help improve the speed and responsiveness of your business-critical applications.</span></span> <span data-ttu-id="a7acb-105">Performans öneriler danışmanına alın **performans** Danışmanı Pano sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a7acb-105">You can get performance recommendations from Advisor on the **Performance** tab of the Advisor dashboard.</span></span>

![Advisor performans sekmesi](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a><span data-ttu-id="a7acb-107">SQL DB Danışmanı ile veritabanı performansı</span><span class="sxs-lookup"><span data-stu-id="a7acb-107">Improve database performance with SQL DB Advisor</span></span>

<span data-ttu-id="a7acb-108">Advisor önerileri tüm Azure kaynakları için tutarlı, birleştirilmiş bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7acb-108">Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="a7acb-109">SQL Azure veritabanının performansını geliştirmek için öneriler getirmek için SQL Database Advisor ile tümleşir.</span><span class="sxs-lookup"><span data-stu-id="a7acb-109">It integrates with SQL Database Advisor to bring you recommendations for improving the performance of your SQL Azure database.</span></span> <span data-ttu-id="a7acb-110">SQL veritabanı Danışmanı, SQL Azure veritabanının performansını kullanım geçmişiniz çözümleyerek değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="a7acb-110">SQL Database Advisor assesses the performance of your SQL Azure databases by analyzing your usage history.</span></span> <span data-ttu-id="a7acb-111">Ardından, veritabanının tipik iş yükünü çalıştırmak için en uygun öneriler sunar.</span><span class="sxs-lookup"><span data-stu-id="a7acb-111">It then offers recommendations that are best suited for running the database’s typical workload.</span></span> 

> [!NOTE]
> <span data-ttu-id="a7acb-112">Önerileri almak için bir veritabanı hakkında kullanım haftada olması gerekir ve bu hafta içinde var. bazı tutarlı etkinlik olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7acb-112">To get recommendations, a database must have about a week of usage, and within that week there must be some consistent activity.</span></span> <span data-ttu-id="a7acb-113">SQL veritabanı Danışmanı daha kolay rastgele WINS'e etkinlik için tutarlı bir sorgu modelleri için en iyi duruma getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7acb-113">SQL Database Advisor can optimize more easily for consistent query patterns than for random bursts of activity.</span></span>

<span data-ttu-id="a7acb-114">SQL Database Advisor hakkında daha fazla bilgi için bkz: [SQL veritabanı Danışmanı'nı](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span><span class="sxs-lookup"><span data-stu-id="a7acb-114">For more information about SQL Database Advisor, see [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span></span>

![SQL veritabanı önerileri](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a><span data-ttu-id="a7acb-116">Redis önbelleği performansı ve güvenilirliği iyileştirmek</span><span class="sxs-lookup"><span data-stu-id="a7acb-116">Improve Redis Cache performance and reliability</span></span>

<span data-ttu-id="a7acb-117">Advisor burada performansını olumsuz yönde yüksek bellek kullanımı, sunucu iş yükü, ağ bant genişliği veya çok sayıda istemci bağlantıları tarafından etkilenebilir Redis önbelleği örnekleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a7acb-117">Advisor identifies Redis Cache instances where performance may be adversely affected by high memory usage, server load, network bandwidth, or a large number of client connections.</span></span> <span data-ttu-id="a7acb-118">Advisor en iyi yöntemler, olası sorunları önlemenize yardımcı olacak öneriler de sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7acb-118">Advisor also provides best practices recommendations to help you avoid potential issues.</span></span> <span data-ttu-id="a7acb-119">Redis önbelleği öneriler hakkında daha fazla bilgi için bkz: [Redis önbelleği Danışmanı](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span><span class="sxs-lookup"><span data-stu-id="a7acb-119">For more information about Redis Cache recommendations, see [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span></span>


## <a name="improve-app-service-performance-and-reliability"></a><span data-ttu-id="a7acb-120">Uygulama hizmeti performans ve güvenilirlik geliştirmek</span><span class="sxs-lookup"><span data-stu-id="a7acb-120">Improve App Service performance and reliability</span></span>

<span data-ttu-id="a7acb-121">Azure Danışmanı uygulama hizmetleri deneyiminizi geliştirmek ve ilgili platform özelliklerini keşfetmek için en iyi uygulama önerilerini tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="a7acb-121">Azure Advisor integrates best practices recommendations for improving your App Services experience and discovering relevant platform capabilities.</span></span> <span data-ttu-id="a7acb-122">Uygulama Hizmetleri önerileri örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a7acb-122">Examples of App Services recommendations are:</span></span>
* <span data-ttu-id="a7acb-123">Algılama, bellek veya CPU kaynaklarını azaltma seçenekleri ile uygulama çalışma zamanları tarafından tükendiği örnekleri.</span><span class="sxs-lookup"><span data-stu-id="a7acb-123">Detection of instances where memory or CPU resources are exhausted by app runtimes with mitigation options.</span></span>
* <span data-ttu-id="a7acb-124">Burada collocating kaynakları web uygulamaları ve veritabanları gibi örneklerinin algılama, performans ve düşük maliyetli artırabilir.</span><span class="sxs-lookup"><span data-stu-id="a7acb-124">Detection of instances where collocating resources like web apps and databases can improve performance and lower cost.</span></span> 

<span data-ttu-id="a7acb-125">Uygulama Hizmetleri öneriler hakkında daha fazla bilgi için bkz: [Azure App Service için en iyi uygulamaları](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span><span class="sxs-lookup"><span data-stu-id="a7acb-125">For more information about App Services recommendations, see [Best Practices for Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span></span>
<span data-ttu-id="a7acb-126">![Uygulama Hizmetleri önerileri](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span><span class="sxs-lookup"><span data-stu-id="a7acb-126">![App Services recommendations](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span></span>

## <a name="how-to-access-performance-recommendations-in-advisor"></a><span data-ttu-id="a7acb-127">Performans önerileri Danışmanı erişme</span><span class="sxs-lookup"><span data-stu-id="a7acb-127">How to access Performance recommendations in Advisor</span></span>

1. <span data-ttu-id="a7acb-128">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a7acb-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="a7acb-129">Sol bölmede **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="a7acb-129">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="a7acb-130">Hizmet menü bölmesinde altında **izleme ve Yönetim**, tıklatın **Azure Danışmanı**.</span><span class="sxs-lookup"><span data-stu-id="a7acb-130">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="a7acb-131">Advisor Panosu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a7acb-131">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="a7acb-132">Advisor Panoda tıklatın **performans** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a7acb-132">On the Advisor dashboard, click the **Performance** tab.</span></span>

5. <span data-ttu-id="a7acb-133">Önerileri almak ve ardından istediğiniz aboneliği seçin **alma önerileri**.</span><span class="sxs-lookup"><span data-stu-id="a7acb-133">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="a7acb-134">Advisor önerileri erişmek için öncelikle *aboneliğinizi kaydetmek* Danışmanı ile.</span><span class="sxs-lookup"><span data-stu-id="a7acb-134">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="a7acb-135">Bir abonelik kayıtlı olduğunda bir *abonelik sahibi* Danışmanı Pano başlatır ve tıkladığında **alma önerileri** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a7acb-135">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="a7acb-136">Bu bir *tek seferlik işlem*.</span><span class="sxs-lookup"><span data-stu-id="a7acb-136">This is a *one-time operation*.</span></span> <span data-ttu-id="a7acb-137">Abonelik kaydedildikten sonra Advisor önerileri olarak erişebilir *sahibi*, *katkıda bulunan*, veya *okuyucu* bir abonelik, bir kaynak grubu ya da belirli bir kaynak için.</span><span class="sxs-lookup"><span data-stu-id="a7acb-137">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7acb-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a7acb-138">Next steps</span></span>

<span data-ttu-id="a7acb-139">Advisor önerileri hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="a7acb-139">To learn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="a7acb-140">Advisor giriş</span><span class="sxs-lookup"><span data-stu-id="a7acb-140">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="a7acb-141">Danışman’ı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a7acb-141">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="a7acb-142">Advisor maliyet önerileri</span><span class="sxs-lookup"><span data-stu-id="a7acb-142">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="a7acb-143">Advisor yüksek kullanılabilirlik önerileri</span><span class="sxs-lookup"><span data-stu-id="a7acb-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="a7acb-144">Advisor güvenlik önerileri</span><span class="sxs-lookup"><span data-stu-id="a7acb-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)

