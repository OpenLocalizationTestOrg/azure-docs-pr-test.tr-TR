---
title: "İzleme ve performansı - Azure SQL veritabanı | Microsoft Docs"
description: "Azure SQL veritabanı geçerli sorgu performansını iyileştirebilir alanları tanımlamanıza yardımcı olması için performans araçları sağlar."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: a60b75ac-cf27-4d73-8322-ee4d4c448aa2
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2016
ms.author: sstein
ms.openlocfilehash: 522b932ab055978c52f085dbaa36095bb6b77962
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-improve-performance"></a><span data-ttu-id="49daf-103">İzleme ve performansı</span><span class="sxs-lookup"><span data-stu-id="49daf-103">Monitor and improve performance</span></span>
<span data-ttu-id="49daf-104">Azure SQL veritabanı veritabanınızdaki olası sorunlar tanımlanmakta ve akıllı ayarlama Eylemler ve öneriler sağlayarak İş yükünüzün performansını geliştirebilirsiniz Eylemler önerir.</span><span class="sxs-lookup"><span data-stu-id="49daf-104">Azure SQL Database identifies potential problems in your database and recommends actions that can improve performance of your workload by providing intelligent tuning actions and recommendations.</span></span>

<span data-ttu-id="49daf-105">Veritabanı performansınızı gözden geçirmek için kullanın **performans** döşeme genel bakış sayfasında veya gidin "Destek + sorun giderme için" bölümüne:</span><span class="sxs-lookup"><span data-stu-id="49daf-105">To review your database performance, use the **Performance** tile on the Overview page, or navigate down to "Support + troubleshooting" section:</span></span>

   ![Performans görünümü](./media/sql-database-performance/entries.png)

<span data-ttu-id="49daf-107">İçindeki "Destek + sorun giderme" bölümüne, şu sayfaları kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="49daf-107">In the "Support + troubleshooting" section, you can use the following pages:</span></span>


1. <span data-ttu-id="49daf-108">[Performans genel bakış](#performance-overview) veritabanınızın performansını izlemek için.</span><span class="sxs-lookup"><span data-stu-id="49daf-108">[Performance overview](#performance-overview) to monitor performance of your database.</span></span> 
2. <span data-ttu-id="49daf-109">[Performans önerileri](#performance-recommendations) İş yükünüzün performansını artırabilir performans önerileri bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="49daf-109">[Performance recommendations](#performance-recommendations) to find performance recommendations that can improve performance of your workload.</span></span>
3. <span data-ttu-id="49daf-110">[Sorgu performansı öngörüleri](#query-performance-insight) kaynak tüketen sorguları üst kaynak bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="49daf-110">[Query Performance Insight](#query-performance-insight) to find top resource consuming queries.</span></span>
4. <span data-ttu-id="49daf-111">[Otomatik ayarlama](#automatic-tuning) Azure SQL veritabanı otomatik olarak veritabanınızı en iyi duruma izin vermek için.</span><span class="sxs-lookup"><span data-stu-id="49daf-111">[Automatic tuning](#automatic-tuning) to let Azure SQL Database automatically optimize your database.</span></span>

## <a name="performance-overview"></a><span data-ttu-id="49daf-112">Performans genel bakış</span><span class="sxs-lookup"><span data-stu-id="49daf-112">Performance Overview</span></span>
<span data-ttu-id="49daf-113">Bu görünüm, veritabanınızın performansını özetini sağlar ve ve sorun gidermeyi performansla yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="49daf-113">This view provides a summary of your database performance, and helps you with performance tuning and troubleshooting.</span></span> 

![Performans](./media/sql-database-performance/performance.png)

* <span data-ttu-id="49daf-115">**Önerileri** kutucuğu veritabanınız için öneriler ayarlama bir dökümünü sağlar (ilk üç önerileri gösterilen olup olmadığını daha fazla).</span><span class="sxs-lookup"><span data-stu-id="49daf-115">The **Recommendations** tile provides a breakdown of tuning recommendations for your database (top three recommendations are shown if there are more).</span></span> <span data-ttu-id="49daf-116">Bu kutucuğa tıklamak, götürür size  **[performans önerileri](#performance-recommendations)**.</span><span class="sxs-lookup"><span data-stu-id="49daf-116">Clicking this tile takes you to **[Performance recommendations](#performance-recommendations)**.</span></span> 
* <span data-ttu-id="49daf-117">**Etkinlik ayarlama** kutucuğu devam eden ve veritabanınız için Eylemler ayarlama, etkinlik ayarlama geçmişini hızlı bir görünüme vererek tamamlanan bir özetini sağlar.</span><span class="sxs-lookup"><span data-stu-id="49daf-117">The **Tuning activity** tile provides a summary of the ongoing and completed tuning actions for your database, giving you a quick view into the history of tuning activity.</span></span> <span data-ttu-id="49daf-118">Bu kutucuğa tıklamak veritabanınızın tam ayarlama geçmişini görüntülemek için götürür.</span><span class="sxs-lookup"><span data-stu-id="49daf-118">Clicking this tile takes you to the full tuning history view for your database.</span></span>
* <span data-ttu-id="49daf-119">**Otomatik ayarı** döşeme gösterir [otomatik ayarı yapılandırma](sql-database-automatic-tuning-enable.md) (veritabanınızı otomatik olarak uygulanan seçeneklerini ayarlama) veritabanı.</span><span class="sxs-lookup"><span data-stu-id="49daf-119">The **Auto-tuning** tile shows the [auto-tuning configuration](sql-database-automatic-tuning-enable.md) for your database (tuning options that are automatically applied to your database).</span></span> <span data-ttu-id="49daf-120">Bu kutucuğa tıklayarak Otomasyon yapılandırması iletişim kutusunu açar.</span><span class="sxs-lookup"><span data-stu-id="49daf-120">Clicking this tile opens the automation configuration dialog.</span></span>
* <span data-ttu-id="49daf-121">**Veritabanı sorguları** döşeme veritabanınız (kaynak tüketen sorguları genel DTU kullanımı ve üst kaynak) için sorgu performansı özetini gösterir.</span><span class="sxs-lookup"><span data-stu-id="49daf-121">The **Database queries** tile shows the summary of the query performance for your database (overall DTU usage and top resource consuming queries).</span></span> <span data-ttu-id="49daf-122">Bu kutucuğa tıklamak, götürür size  **[sorgu performansı öngörüleri](#query-performance-insight)**.</span><span class="sxs-lookup"><span data-stu-id="49daf-122">Clicking this tile takes you to **[Query Performance Insight](#query-performance-insight)**.</span></span>

## <a name="performance-recommendations"></a><span data-ttu-id="49daf-123">Performans önerileri</span><span class="sxs-lookup"><span data-stu-id="49daf-123">Performance recommendations</span></span>
<span data-ttu-id="49daf-124">Bu sayfa akıllı sağlar [önerileri ayarlama](sql-database-advisor.md) veritabanınızın performansı geliştirebilir.</span><span class="sxs-lookup"><span data-stu-id="49daf-124">This page provides intelligent [tuning recommendations](sql-database-advisor.md) that can improve your database's performance.</span></span> <span data-ttu-id="49daf-125">Bu sayfada aşağıdaki önerileri türleri gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="49daf-125">The following types of recommendations are shown on this page:</span></span>

* <span data-ttu-id="49daf-126">Öneri oluşturmak veya bırakma için hangi dizinlerin.</span><span class="sxs-lookup"><span data-stu-id="49daf-126">Recommendations on which indexes to create or drop.</span></span>
* <span data-ttu-id="49daf-127">Şema sorunları veritabanında belirlendiğinde öneriler sunar.</span><span class="sxs-lookup"><span data-stu-id="49daf-127">Recommendations when schema issues are identified in the database.</span></span>
* <span data-ttu-id="49daf-128">Sorguları parametreli sorgularından yararlanabilir kullanmayla ilgili öneriler.</span><span class="sxs-lookup"><span data-stu-id="49daf-128">Recommendations when queries can benefit from parameterized queries.</span></span>

![Performans](./media/sql-database-performance/recommendations.png)

<span data-ttu-id="49daf-130">Geçmişte uygulanan eylemler ayarlama, tam geçmişini de bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49daf-130">You can also find complete history of tuning actions that were applied in the past.</span></span>

<span data-ttu-id="49daf-131">Apply performans önerileri bulmayı öğrenin [bulmak ve performans önerileri uygulamak](sql-database-advisor-portal.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="49daf-131">Learn how to find an apply performance recommendations in [Find and apply performance recommendations](sql-database-advisor-portal.md) article.</span></span>

## <a name="automatic-tuning"></a><span data-ttu-id="49daf-132">Otomatik ayarlama</span><span class="sxs-lookup"><span data-stu-id="49daf-132">Automatic tuning</span></span>
<span data-ttu-id="49daf-133">Azure SQL veritabanları otomatik olarak ayarlamak veritabanı performansını uygulayarak [performans önerileri](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="49daf-133">Azure SQL Databases can automatically tune database performance by applying [performance recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="49daf-134">Daha fazla bilgi edinmek için okuma [otomatik ayarlama makale](sql-database-automatic-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="49daf-134">To learn more, read [Automatic tuning article](sql-database-automatic-tuning.md).</span></span> <span data-ttu-id="49daf-135">Etkinleştirmek için okuma [otomatik ayarlamayı etkinleştirmek nasıl](sql-database-automatic-tuning-enable.md).</span><span class="sxs-lookup"><span data-stu-id="49daf-135">To enable it, read [how to enable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>

## <a name="query-performance-insight"></a><span data-ttu-id="49daf-136">Sorgu Performansı Öngörüleri</span><span class="sxs-lookup"><span data-stu-id="49daf-136">Query Performance Insight</span></span>
<span data-ttu-id="49daf-137">[Sorgu performansı öngörüleri](sql-database-query-performance.md) sağlayarak veritabanı performans sorunlarını giderme daha az süre beklemesini sağlar:</span><span class="sxs-lookup"><span data-stu-id="49daf-137">[Query Performance Insight](sql-database-query-performance.md) allows you to spend less time troubleshooting database performance by providing:</span></span>

* <span data-ttu-id="49daf-138">Veritabanları (DTU) kaynak tüketimi daha derin bir anlayış.</span><span class="sxs-lookup"><span data-stu-id="49daf-138">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="49daf-139">Potansiyel olarak performansı için ayarlanmış sorguları tüketen üst CPU.</span><span class="sxs-lookup"><span data-stu-id="49daf-139">The top CPU consuming queries, which can potentially be tuned for improved performance.</span></span> 
* <span data-ttu-id="49daf-140">Bir sorgu ayrıntıları detaya yeteneği.</span><span class="sxs-lookup"><span data-stu-id="49daf-140">The ability to drill down into the details of a query.</span></span> 

  ![Performans Panosu](./media/sql-database-query-performance/performance.png)

<span data-ttu-id="49daf-142">Bu sayfa hakkında daha fazla bilgi makalesinde Bul  **[sorgu performansı öngörüleri kullanmayı](sql-database-query-performance.md)**.</span><span class="sxs-lookup"><span data-stu-id="49daf-142">Find more information about this page in the article **[How to use Query Performance Insight](sql-database-query-performance.md)**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="49daf-143">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="49daf-143">Additional resources</span></span>
* [<span data-ttu-id="49daf-144">Tek veritabanları için Azure SQL Database performans rehberi</span><span class="sxs-lookup"><span data-stu-id="49daf-144">Azure SQL Database performance guidance for single databases</span></span>](sql-database-performance-guidance.md)
* [<span data-ttu-id="49daf-145">Bir esnek havuz ne zaman kullanılmalı?</span><span class="sxs-lookup"><span data-stu-id="49daf-145">When should an elastic pool be used?</span></span>](sql-database-elastic-pool-guidance.md)

