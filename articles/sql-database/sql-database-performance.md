---
title: "aaaMonitor ve performansı - Azure SQL veritabanı | Microsoft Docs"
description: "Azure SQL veritabanı performans sağlar hello geçerli sorgu performansını iyileştirebilir alanlarını tanımlayacak toohelp araçları."
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
ms.openlocfilehash: 84b8a1bc62698a29deb49e765f208bd7e14d0870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-improve-performance"></a><span data-ttu-id="630c5-103">İzleme ve performansı</span><span class="sxs-lookup"><span data-stu-id="630c5-103">Monitor and improve performance</span></span>
<span data-ttu-id="630c5-104">Azure SQL veritabanı veritabanınızdaki olası sorunlar tanımlanmakta ve akıllı ayarlama Eylemler ve öneriler sağlayarak İş yükünüzün performansını geliştirebilirsiniz Eylemler önerir.</span><span class="sxs-lookup"><span data-stu-id="630c5-104">Azure SQL Database identifies potential problems in your database and recommends actions that can improve performance of your workload by providing intelligent tuning actions and recommendations.</span></span>

<span data-ttu-id="630c5-105">tooreview veritabanı performansı, kullanım hello **performans** döşeme hello genel bakış sayfasında veya aşağı çok gidin "Destek + sorun giderme" bölümüne:</span><span class="sxs-lookup"><span data-stu-id="630c5-105">tooreview your database performance, use hello **Performance** tile on hello Overview page, or navigate down too"Support + troubleshooting" section:</span></span>

   ![Performans görünümü](./media/sql-database-performance/entries.png)

<span data-ttu-id="630c5-107">Merhaba "Destek + sorun giderme" bölümünde sayfaları aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="630c5-107">In hello "Support + troubleshooting" section, you can use hello following pages:</span></span>


1. <span data-ttu-id="630c5-108">[Performans genel bakış](#performance-overview) veritabanınızın toomonitor performansını.</span><span class="sxs-lookup"><span data-stu-id="630c5-108">[Performance overview](#performance-overview) toomonitor performance of your database.</span></span> 
2. <span data-ttu-id="630c5-109">[Performans önerileri](#performance-recommendations) İş yükünüzün performansını artırabilir toofind performans önerileri.</span><span class="sxs-lookup"><span data-stu-id="630c5-109">[Performance recommendations](#performance-recommendations) toofind performance recommendations that can improve performance of your workload.</span></span>
3. <span data-ttu-id="630c5-110">[Sorgu performansı öngörüleri](#query-performance-insight) kaynak tüketen sorguları toofind üst kaynak.</span><span class="sxs-lookup"><span data-stu-id="630c5-110">[Query Performance Insight](#query-performance-insight) toofind top resource consuming queries.</span></span>
4. <span data-ttu-id="630c5-111">[Otomatik ayarlama](#automatic-tuning) toolet Azure SQL veritabanı, veritabanınızı otomatik olarak en iyi duruma getirme.</span><span class="sxs-lookup"><span data-stu-id="630c5-111">[Automatic tuning](#automatic-tuning) toolet Azure SQL Database automatically optimize your database.</span></span>

## <a name="performance-overview"></a><span data-ttu-id="630c5-112">Performans genel bakış</span><span class="sxs-lookup"><span data-stu-id="630c5-112">Performance Overview</span></span>
<span data-ttu-id="630c5-113">Bu görünüm, veritabanınızın performansını özetini sağlar ve ve sorun gidermeyi performansla yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="630c5-113">This view provides a summary of your database performance, and helps you with performance tuning and troubleshooting.</span></span> 

![Performans](./media/sql-database-performance/performance.png)

* <span data-ttu-id="630c5-115">Merhaba **önerileri** kutucuğu veritabanınız için öneriler ayarlama bir dökümünü sağlar (ilk üç önerileri gösterilen olup olmadığını daha fazla).</span><span class="sxs-lookup"><span data-stu-id="630c5-115">hello **Recommendations** tile provides a breakdown of tuning recommendations for your database (top three recommendations are shown if there are more).</span></span> <span data-ttu-id="630c5-116">Bu kutucuğa tıklayarak alır, çok**[performans önerileri](#performance-recommendations)**.</span><span class="sxs-lookup"><span data-stu-id="630c5-116">Clicking this tile takes you too**[Performance recommendations](#performance-recommendations)**.</span></span> 
* <span data-ttu-id="630c5-117">Merhaba **etkinlik ayarlama** kutucuğu hello devam eden ve veritabanınız için Eylemler ayarlama, etkinlik ayarlama, hello geçmişi hızlı bir görünüme vererek tamamlanan özetini sağlar.</span><span class="sxs-lookup"><span data-stu-id="630c5-117">hello **Tuning activity** tile provides a summary of hello ongoing and completed tuning actions for your database, giving you a quick view into hello history of tuning activity.</span></span> <span data-ttu-id="630c5-118">Bu kutucuğa tıklamak toohello veritabanınız için Geçmiş görünümünü ayarlama tam götürür.</span><span class="sxs-lookup"><span data-stu-id="630c5-118">Clicking this tile takes you toohello full tuning history view for your database.</span></span>
* <span data-ttu-id="630c5-119">Merhaba **otomatik ayarı** kutucuğunda gösterilir hello [otomatik ayarı yapılandırma](sql-database-automatic-tuning-enable.md) (otomatik olarak uygulanan tooyour veritabanı seçenekleri ayarlama) veritabanı.</span><span class="sxs-lookup"><span data-stu-id="630c5-119">hello **Auto-tuning** tile shows hello [auto-tuning configuration](sql-database-automatic-tuning-enable.md) for your database (tuning options that are automatically applied tooyour database).</span></span> <span data-ttu-id="630c5-120">Bu kutucuğa tıklayarak hello Otomasyon yapılandırması iletişim kutusunu açar.</span><span class="sxs-lookup"><span data-stu-id="630c5-120">Clicking this tile opens hello automation configuration dialog.</span></span>
* <span data-ttu-id="630c5-121">Merhaba **veritabanı sorguları** kutucuğunda gösterilir hello hello sorgu performansı (kaynak tüketen sorguları genel DTU kullanımı ve üst kaynak) veritabanı özeti.</span><span class="sxs-lookup"><span data-stu-id="630c5-121">hello **Database queries** tile shows hello summary of hello query performance for your database (overall DTU usage and top resource consuming queries).</span></span> <span data-ttu-id="630c5-122">Bu kutucuğa tıklayarak alır, çok**[sorgu performansı öngörüleri](#query-performance-insight)**.</span><span class="sxs-lookup"><span data-stu-id="630c5-122">Clicking this tile takes you too**[Query Performance Insight](#query-performance-insight)**.</span></span>

## <a name="performance-recommendations"></a><span data-ttu-id="630c5-123">Performans önerileri</span><span class="sxs-lookup"><span data-stu-id="630c5-123">Performance recommendations</span></span>
<span data-ttu-id="630c5-124">Bu sayfa akıllı sağlar [önerileri ayarlama](sql-database-advisor.md) veritabanınızın performansı geliştirebilir.</span><span class="sxs-lookup"><span data-stu-id="630c5-124">This page provides intelligent [tuning recommendations](sql-database-advisor.md) that can improve your database's performance.</span></span> <span data-ttu-id="630c5-125">Bu sayfada şu önerilerin türlerini hello gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="630c5-125">hello following types of recommendations are shown on this page:</span></span>

* <span data-ttu-id="630c5-126">Hangi dizin toocreate veya bırakma öneriler sunar.</span><span class="sxs-lookup"><span data-stu-id="630c5-126">Recommendations on which indexes toocreate or drop.</span></span>
* <span data-ttu-id="630c5-127">Şema sorunları hello veritabanında belirlendiğinde öneriler sunar.</span><span class="sxs-lookup"><span data-stu-id="630c5-127">Recommendations when schema issues are identified in hello database.</span></span>
* <span data-ttu-id="630c5-128">Sorguları parametreli sorgularından yararlanabilir kullanmayla ilgili öneriler.</span><span class="sxs-lookup"><span data-stu-id="630c5-128">Recommendations when queries can benefit from parameterized queries.</span></span>

![Performans](./media/sql-database-performance/recommendations.png)

<span data-ttu-id="630c5-130">Merhaba son uygulanan eylemler ayarlama, tam geçmişini de bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="630c5-130">You can also find complete history of tuning actions that were applied in hello past.</span></span>

<span data-ttu-id="630c5-131">Bilgi nasıl toofind apply performans önerileri [bulmak ve performans önerileri uygulamak](sql-database-advisor-portal.md) makale.</span><span class="sxs-lookup"><span data-stu-id="630c5-131">Learn how toofind an apply performance recommendations in [Find and apply performance recommendations](sql-database-advisor-portal.md) article.</span></span>

## <a name="automatic-tuning"></a><span data-ttu-id="630c5-132">Otomatik ayarlama</span><span class="sxs-lookup"><span data-stu-id="630c5-132">Automatic tuning</span></span>
<span data-ttu-id="630c5-133">Azure SQL veritabanları otomatik olarak ayarlamak veritabanı performansını uygulayarak [performans önerileri](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="630c5-133">Azure SQL Databases can automatically tune database performance by applying [performance recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="630c5-134">toolearn daha fazlasını okuyun [otomatik ayarlama makale](sql-database-automatic-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="630c5-134">toolearn more, read [Automatic tuning article](sql-database-automatic-tuning.md).</span></span> <span data-ttu-id="630c5-135">tooenable, okuma [nasıl tooenable otomatik ayarlama](sql-database-automatic-tuning-enable.md).</span><span class="sxs-lookup"><span data-stu-id="630c5-135">tooenable it, read [how tooenable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>

## <a name="query-performance-insight"></a><span data-ttu-id="630c5-136">Sorgu Performansı Öngörüleri</span><span class="sxs-lookup"><span data-stu-id="630c5-136">Query Performance Insight</span></span>
<span data-ttu-id="630c5-137">[Sorgu performansı öngörüleri](sql-database-query-performance.md) toospend sağlayarak veritabanı performans sorunlarını giderme daha az zaman verir:</span><span class="sxs-lookup"><span data-stu-id="630c5-137">[Query Performance Insight](sql-database-query-performance.md) allows you toospend less time troubleshooting database performance by providing:</span></span>

* <span data-ttu-id="630c5-138">Veritabanları (DTU) kaynak tüketimi daha derin bir anlayış.</span><span class="sxs-lookup"><span data-stu-id="630c5-138">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="630c5-139">Merhaba üst CPU potansiyel olarak performansı için ayarlanmış sorguları kullanma.</span><span class="sxs-lookup"><span data-stu-id="630c5-139">hello top CPU consuming queries, which can potentially be tuned for improved performance.</span></span> 
* <span data-ttu-id="630c5-140">özelliği toodrill aşağı sorgu hello ayrıntılarını hello.</span><span class="sxs-lookup"><span data-stu-id="630c5-140">hello ability toodrill down into hello details of a query.</span></span> 

  ![Performans Panosu](./media/sql-database-query-performance/performance.png)

<span data-ttu-id="630c5-142">Bu sayfa hakkında daha fazla bilgi hello makalesinde Bul  **[nasıl toouse sorgu performansı öngörüleri](sql-database-query-performance.md)**.</span><span class="sxs-lookup"><span data-stu-id="630c5-142">Find more information about this page in hello article **[How toouse Query Performance Insight](sql-database-query-performance.md)**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="630c5-143">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="630c5-143">Additional resources</span></span>
* [<span data-ttu-id="630c5-144">Tek veritabanları için Azure SQL Database performans rehberi</span><span class="sxs-lookup"><span data-stu-id="630c5-144">Azure SQL Database performance guidance for single databases</span></span>](sql-database-performance-guidance.md)
* [<span data-ttu-id="630c5-145">Bir esnek havuz ne zaman kullanılmalı?</span><span class="sxs-lookup"><span data-stu-id="630c5-145">When should an elastic pool be used?</span></span>](sql-database-elastic-pool-guidance.md)

