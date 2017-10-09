---
title: "aaaTroubleshoot performans sorunları ve veritabanınızı en iyi duruma getirme | Microsoft Docs"
description: "Performans önerileri tooyour SQL veritabanı yanı sıra Temizle toogain performansınızla ilgili bilgiler hello sorguları veritabanına karşı çalıştırma performansını nasıl hello Uygula"
metakeywords: azure sql database performance monitoring recommendation
services: sql-database
documentationcenter: 
manager: jhubbard
author: jan-eng
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,monitor & tune
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: janeng
ms.openlocfilehash: e948d30ac74eecf45420d5d77ef55e3c0b6f3f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a><span data-ttu-id="9ad7a-103">Performans sorunlarını gidermek ve veritabanınızı en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="9ad7a-103">Troubleshoot performance issues and optimize your database</span></span>

<span data-ttu-id="9ad7a-104">Veritabanı performansının düşük olmasına yol açan yaygın nedenler, dizinlerin eksik olması ve sorguların hatalı bir şekilde iyileştirilmesidir.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-104">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="9ad7a-105">Bu öğreticide, öğrenin:</span><span class="sxs-lookup"><span data-stu-id="9ad7a-105">In this tutorial you learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="9ad7a-106">Gözden geçirin, uygulayın ve performans geliştirme önerileri geri</span><span class="sxs-lookup"><span data-stu-id="9ad7a-106">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="9ad7a-107">Yüksek kaynak kullanımı sorgularıyla Bul</span><span class="sxs-lookup"><span data-stu-id="9ad7a-107">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="9ad7a-108">Uzun süre çalışan sorgular Bul</span><span class="sxs-lookup"><span data-stu-id="9ad7a-108">Find long running queries</span></span>

> <span data-ttu-id="9ad7a-109">Performans sorunlarını – örneğin tooreceive bir öneri dizin eksik olan bir veritabanı üzerinde sürekli bir iş yükü gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-109">You need a continuous workload on a database with performance issues – missing an index for example tooreceive a recommendation.</span></span>
>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="9ad7a-110">Toohello Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="9ad7a-110">Log in toohello Azure portal</span></span>

<span data-ttu-id="9ad7a-111">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9ad7a-111">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="review-and-apply-a-recommendation"></a><span data-ttu-id="9ad7a-112">Gözden geçirin ve öneri uygulayın</span><span class="sxs-lookup"><span data-stu-id="9ad7a-112">Review and apply a recommendation</span></span>

<span data-ttu-id="9ad7a-113">Bu adımları tooapply bir öneri, veritabanınız için hello sisteminden izleyin:</span><span class="sxs-lookup"><span data-stu-id="9ad7a-113">Follow these steps tooapply a recommendation from hello system for your database:</span></span>

1. <span data-ttu-id="9ad7a-114">Merhaba tıklatın **performans önerileri** hello veritabanı Dikey Menüde.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-114">Click hello **Performance recommendations** menu in hello database blade.</span></span>

    ![Performans önerisi](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. <span data-ttu-id="9ad7a-116">Öneriler Hello listeden etkin bir öneri seçin.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-116">From hello list of recommendations, select an active recommendation.</span></span> <span data-ttu-id="9ad7a-117">Bu örnekte, dizin oluştur.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-117">In this example, Create Index.</span></span>

    ![öneri seçin](./media/sql-database-performance-tutorial/create_index.png)

3. <span data-ttu-id="9ad7a-119">Merhaba tıklayarak Hello öneriyi uygulamak **Uygula** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-119">Apply hello recommendation by clicking hello **Apply** button.</span></span> <span data-ttu-id="9ad7a-120">İsteğe bağlı olarak, hello öneri ayrıntılarını gözden geçirin ve çok tıklayarak yürütülebilir hello T-SQL betiği bkz **betiği görüntüle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-120">Optionally, review hello recommendation details and see hello T-SQL script too be executed by clicking on **View Script** button.</span></span>

    ![öneriyi](./media/sql-database-performance-tutorial/apply.png)

4. <span data-ttu-id="9ad7a-122">[İsteğe bağlı] Otomatik olarak uygulanan önerileri toobe için otomatik olarak ayarlamayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-122">[Optional] Enable automatic tuning for recommendations toobe applied automatically.</span></span>

    ![otomatik olarak ayarlama](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a><span data-ttu-id="9ad7a-124">Bir öneri geri</span><span class="sxs-lookup"><span data-stu-id="9ad7a-124">Revert a recommendation</span></span>

<span data-ttu-id="9ad7a-125">Merhaba veritabanı Danışmanı uygulanan her bir öneri izler.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-125">hello Database Advisor monitors every recommendation implemented.</span></span> <span data-ttu-id="9ad7a-126">Otomatik olarak bir öneri hello iş yükünü artırmak değil ise döndürülecek.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-126">If a recommendation doesn't improve hello workload it will be automatically reverted.</span></span> <span data-ttu-id="9ad7a-127">El ile bir öneri dönme mümkün olsa da çoğu durumda şart değildir.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-127">Manually reverting a recommendation is possible, but not necessary in most cases.</span></span> <span data-ttu-id="9ad7a-128">toorevert bir öneri:</span><span class="sxs-lookup"><span data-stu-id="9ad7a-128">toorevert a recommendation:</span></span>

1. <span data-ttu-id="9ad7a-129">Toohello performans önerileri menü gidin ve uygulanan hello önerileri birini seçin.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-129">Go toohello performance recommendations menu and select one of hello applied recommendations.</span></span>

    ![öneri seçin](./media/sql-database-performance-tutorial/select.png)

2. <span data-ttu-id="9ad7a-131">Merhaba Ayrıntıları Görüntüle'yi tıklatın **Revert**.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-131">In hello details view, click **Revert**.</span></span>

    ![öneri geri](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a><span data-ttu-id="9ad7a-133">Merhaba tüketir hello sorgu çoğu kaynakları bulun</span><span class="sxs-lookup"><span data-stu-id="9ad7a-133">Find hello query that consumes hello most resources</span></span>

<span data-ttu-id="9ad7a-134">Merhaba tüketen bu adımları toofind hello sorgu en fazla kaynak izleyin:</span><span class="sxs-lookup"><span data-stu-id="9ad7a-134">Follow these steps toofind hello query consuming hello most resources:</span></span>

1. <span data-ttu-id="9ad7a-135">Tıklatın hello üzerinde **sorgu performansı öngörüleri** hello veritabanı Dikey Menüde.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-135">Click on hello **Query Performance Insight** menu in hello database blade.</span></span>

    ![Sorgu öngörüleri](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. <span data-ttu-id="9ad7a-137">Bir kaynak türü seçin.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-137">Select a resource type.</span></span>

    ![Sorgu öngörüleri](./media/sql-database-performance-tutorial/select_resource_type.png)

3. <span data-ttu-id="9ad7a-139">Merhaba ilk sorgu hello tablosunda seçin.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-139">Select hello first query in hello table.</span></span>

    ![Sorgu öngörüleri](./media/sql-database-performance-tutorial/select_query.png)

4. <span data-ttu-id="9ad7a-141">Merhaba sorgu ayrıntılarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-141">Review hello query details.</span></span>

    ![Sorgu öngörüleri](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a><span data-ttu-id="9ad7a-143">Merhaba uzun çalışan sorgu Bul</span><span class="sxs-lookup"><span data-stu-id="9ad7a-143">Find hello longest running query</span></span>

1. <span data-ttu-id="9ad7a-144">TooQuery performansı öngörüleri gidin ve seçin hello **uzun süre çalışan sorgular** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-144">Go tooQuery Performance Insight and select hello **Long running queries** tab.</span></span>

    ![Sorgu öngörüleri](./media/sql-database-performance-tutorial/long_running.png)

3. <span data-ttu-id="9ad7a-146">Merhaba ilk sorgu hello tablosunda seçin.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-146">Select hello first query in hello table.</span></span>

    ![Sorgu öngörüleri](./media/sql-database-performance-tutorial/select_first_query.png)

4. <span data-ttu-id="9ad7a-148">Merhaba sorgu ayrıntılarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-148">Review hello query details.</span></span>

    ![Sorgu öngörüleri](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a><span data-ttu-id="9ad7a-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9ad7a-150">Next steps</span></span> 
<span data-ttu-id="9ad7a-151">Veritabanı performansının düşük olmasına yol açan yaygın nedenler, dizinlerin eksik olması ve sorguların hatalı bir şekilde iyileştirilmesidir.</span><span class="sxs-lookup"><span data-stu-id="9ad7a-151">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="9ad7a-152">Bu öğreticide için öğrenilen:</span><span class="sxs-lookup"><span data-stu-id="9ad7a-152">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="9ad7a-153">Gözden geçirin, uygulayın ve performans geliştirme önerileri geri</span><span class="sxs-lookup"><span data-stu-id="9ad7a-153">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="9ad7a-154">Yüksek kaynak kullanımı sorgularıyla Bul</span><span class="sxs-lookup"><span data-stu-id="9ad7a-154">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="9ad7a-155">Uzun süre çalışan sorgular Bul</span><span class="sxs-lookup"><span data-stu-id="9ad7a-155">Find long running queries</span></span>

[<span data-ttu-id="9ad7a-156">SQL veritabanı performans ayarlama ipuçları</span><span class="sxs-lookup"><span data-stu-id="9ad7a-156">SQL Database performance tuning tips</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
