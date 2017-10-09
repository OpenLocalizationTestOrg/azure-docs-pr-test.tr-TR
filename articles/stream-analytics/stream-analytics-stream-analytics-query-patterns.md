---
title: "Stream Analytics ortak kullanım desenlerini aaaQuery örnekleri | Microsoft Docs"
description: "Ortak Azure akış analizi sorgu kalıplarından"
keywords: "Sorgu örnekleri"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jenniehubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/08/2017
ms.author: jenniehubbard
ms.openlocfilehash: c8f7a8ac661eaf0281f4140b02c42141b73040fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a><span data-ttu-id="917bb-104">Örnekler ortak Stream Analytics kullanım desenlerini için sorgu</span><span class="sxs-lookup"><span data-stu-id="917bb-104">Query examples for common Stream Analytics usage patterns</span></span>
## <a name="introduction"></a><span data-ttu-id="917bb-105">Giriş</span><span class="sxs-lookup"><span data-stu-id="917bb-105">Introduction</span></span>
<span data-ttu-id="917bb-106">Azure Stream Analytics sorgularda bir SQL benzeri sorgu dili ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="917bb-106">Queries in Azure Stream Analytics are expressed in a SQL-like query language.</span></span> <span data-ttu-id="917bb-107">Bu sorguları hello belgelenen [Stream Analytics sorgu dili başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx) Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="917bb-107">These queries are documented in hello [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span></span> <span data-ttu-id="917bb-108">Bu makalede anahatları çözümleri tooseveral ortak sorgu kalıpları, göre gerçek dünya senaryoları.</span><span class="sxs-lookup"><span data-stu-id="917bb-108">This article outlines solutions tooseveral common query patterns, based on real-world scenarios.</span></span> <span data-ttu-id="917bb-109">Bu iş sürüyor ve düzenli olarak yeni desenlerle güncelleştirilmiş toobe devam eder.</span><span class="sxs-lookup"><span data-stu-id="917bb-109">It is a work in progress and continues toobe updated with new patterns on an ongoing basis.</span></span>

## <a name="query-example-convert-data-types"></a><span data-ttu-id="917bb-110">Sorgu örnek: veri türlerini dönüştürme</span><span class="sxs-lookup"><span data-stu-id="917bb-110">Query example: Convert data types</span></span>
<span data-ttu-id="917bb-111">**Açıklama**: hello giriş akışta özelliklerinin hello türlerini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="917bb-111">**Description**: Define hello types of properties on hello input stream.</span></span>
<span data-ttu-id="917bb-112">Örneğin, hello araba ağırlık hello giriş akışta dize olarak geliyor ve çok dönüştürülen toobe gerekiyor**INT** tooperform **toplam** bunun.</span><span class="sxs-lookup"><span data-stu-id="917bb-112">For example, hello car weight is coming on hello input stream as strings and needs toobe converted too**INT** tooperform **SUM** it up.</span></span>

<span data-ttu-id="917bb-113">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="917bb-113">**Input**:</span></span>

| <span data-ttu-id="917bb-114">Yapma</span><span class="sxs-lookup"><span data-stu-id="917bb-114">Make</span></span> | <span data-ttu-id="917bb-115">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-115">Time</span></span> | <span data-ttu-id="917bb-116">Ağırlık</span><span class="sxs-lookup"><span data-stu-id="917bb-116">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="917bb-117">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-117">Honda</span></span> |<span data-ttu-id="917bb-118">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-118">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="917bb-119">"1000"</span><span class="sxs-lookup"><span data-stu-id="917bb-119">"1000"</span></span> |
| <span data-ttu-id="917bb-120">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-120">Honda</span></span> |<span data-ttu-id="917bb-121">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-121">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="917bb-122">"2000"</span><span class="sxs-lookup"><span data-stu-id="917bb-122">"2000"</span></span> |

<span data-ttu-id="917bb-123">**Çıktı**:</span><span class="sxs-lookup"><span data-stu-id="917bb-123">**Output**:</span></span>

| <span data-ttu-id="917bb-124">Yapma</span><span class="sxs-lookup"><span data-stu-id="917bb-124">Make</span></span> | <span data-ttu-id="917bb-125">Ağırlık</span><span class="sxs-lookup"><span data-stu-id="917bb-125">Weight</span></span> |
| --- | --- |
| <span data-ttu-id="917bb-126">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-126">Honda</span></span> |<span data-ttu-id="917bb-127">3000</span><span class="sxs-lookup"><span data-stu-id="917bb-127">3000</span></span> |

<span data-ttu-id="917bb-128">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="917bb-128">**Solution**:</span></span>

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="917bb-129">**Açıklama**: kullanım bir **CAST** hello deyiminde **ağırlık** toospecify alan, veri türü.</span><span class="sxs-lookup"><span data-stu-id="917bb-129">**Explanation**: Use a **CAST** statement in hello **Weight** field toospecify its data type.</span></span> <span data-ttu-id="917bb-130">Desteklenen veri türlerini Hello listesini [veri türleri (Azure akış analizi)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span><span class="sxs-lookup"><span data-stu-id="917bb-130">See hello list of supported data types in [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

## <a name="query-example-use-likenot-like-toodo-pattern-matching"></a><span data-ttu-id="917bb-131">Sorgu örnek: kullanımı gibi/değil gibi toodo desen eşleştirme</span><span class="sxs-lookup"><span data-stu-id="917bb-131">Query example: Use Like/Not like toodo pattern matching</span></span>
<span data-ttu-id="917bb-132">**Açıklama**: hello olay bir alanın değerini belirli bir desene eşleşip eşleşmediğini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="917bb-132">**Description**: Check that a field value on hello event matches a certain pattern.</span></span>
<span data-ttu-id="917bb-133">Örneğin, hello sonucu ile başlamalı ve 9 ile bitmelidir lisans kalıplarını döndürür denetleyin.</span><span class="sxs-lookup"><span data-stu-id="917bb-133">For example, check that hello result returns license plates that start with A and end with 9.</span></span>

<span data-ttu-id="917bb-134">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="917bb-134">**Input**:</span></span>

| <span data-ttu-id="917bb-135">Yapma</span><span class="sxs-lookup"><span data-stu-id="917bb-135">Make</span></span> | <span data-ttu-id="917bb-136">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="917bb-136">LicensePlate</span></span> | <span data-ttu-id="917bb-137">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-137">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="917bb-138">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-138">Honda</span></span> |<span data-ttu-id="917bb-139">ABC-123</span><span class="sxs-lookup"><span data-stu-id="917bb-139">ABC-123</span></span> |<span data-ttu-id="917bb-140">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-140">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="917bb-141">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-141">Toyota</span></span> |<span data-ttu-id="917bb-142">AAA-999</span><span class="sxs-lookup"><span data-stu-id="917bb-142">AAA-999</span></span> |<span data-ttu-id="917bb-143">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-143">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="917bb-144">Nissan</span><span class="sxs-lookup"><span data-stu-id="917bb-144">Nissan</span></span> |<span data-ttu-id="917bb-145">ABC 369</span><span class="sxs-lookup"><span data-stu-id="917bb-145">ABC-369</span></span> |<span data-ttu-id="917bb-146">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-146">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="917bb-147">**Çıktı**:</span><span class="sxs-lookup"><span data-stu-id="917bb-147">**Output**:</span></span>

| <span data-ttu-id="917bb-148">Yapma</span><span class="sxs-lookup"><span data-stu-id="917bb-148">Make</span></span> | <span data-ttu-id="917bb-149">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="917bb-149">LicensePlate</span></span> | <span data-ttu-id="917bb-150">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-150">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="917bb-151">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-151">Toyota</span></span> |<span data-ttu-id="917bb-152">AAA-999</span><span class="sxs-lookup"><span data-stu-id="917bb-152">AAA-999</span></span> |<span data-ttu-id="917bb-153">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-153">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="917bb-154">Nissan</span><span class="sxs-lookup"><span data-stu-id="917bb-154">Nissan</span></span> |<span data-ttu-id="917bb-155">ABC 369</span><span class="sxs-lookup"><span data-stu-id="917bb-155">ABC-369</span></span> |<span data-ttu-id="917bb-156">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-156">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="917bb-157">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="917bb-157">**Solution**:</span></span>

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

<span data-ttu-id="917bb-158">**Açıklama**: kullanım hello **gibi** deyimi toocheck hello **LicensePlate** alan değer.</span><span class="sxs-lookup"><span data-stu-id="917bb-158">**Explanation**: Use hello **LIKE** statement toocheck hello **LicensePlate** field value.</span></span> <span data-ttu-id="917bb-159">Bu bir ile başlayan sonra sıfır veya daha fazla karakterden oluşan herhangi bir dize olması ve ardından 9 ile bitmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="917bb-159">It should start with an A, then have any string of zero or more characters, and then end with a 9.</span></span> 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a><span data-ttu-id="917bb-160">Sorgu örnek: farklı durumlarda/değerleri (CASE deyimleri) için mantığı belirtin</span><span class="sxs-lookup"><span data-stu-id="917bb-160">Query example: Specify logic for different cases/values (CASE statements)</span></span>
<span data-ttu-id="917bb-161">**Açıklama**: belirli bir ölçütü temel alan bir alan için farklı bir hesaplama sağlar.</span><span class="sxs-lookup"><span data-stu-id="917bb-161">**Description**: Provide a different computation for a field, based on a particular criterion.</span></span>
<span data-ttu-id="917bb-162">Örneğin, 1 için özel bir durum ile aynı olun Merhaba, kaç tane araba geçirilen için dize açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="917bb-162">For example, provide a string description for how many cars of hello same make passed, with a special case for 1.</span></span>

<span data-ttu-id="917bb-163">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="917bb-163">**Input**:</span></span>

| <span data-ttu-id="917bb-164">Yapma</span><span class="sxs-lookup"><span data-stu-id="917bb-164">Make</span></span> | <span data-ttu-id="917bb-165">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-165">Time</span></span> |
| --- | --- |
| <span data-ttu-id="917bb-166">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-166">Honda</span></span> |<span data-ttu-id="917bb-167">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-167">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="917bb-168">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-168">Toyota</span></span> |<span data-ttu-id="917bb-169">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-169">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="917bb-170">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-170">Toyota</span></span> |<span data-ttu-id="917bb-171">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-171">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="917bb-172">**Çıktı**:</span><span class="sxs-lookup"><span data-stu-id="917bb-172">**Output**:</span></span>

| <span data-ttu-id="917bb-173">CarsPassed</span><span class="sxs-lookup"><span data-stu-id="917bb-173">CarsPassed</span></span> | <span data-ttu-id="917bb-174">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-174">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="917bb-175">1 Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-175">1 Honda</span></span> |<span data-ttu-id="917bb-176">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-176">2015-01-01T00:00:10.0000000Z</span></span> |
| <span data-ttu-id="917bb-177">2 Toyotas</span><span class="sxs-lookup"><span data-stu-id="917bb-177">2 Toyotas</span></span> |<span data-ttu-id="917bb-178">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-178">2015-01-01T00:00:10.0000000Z</span></span> |

<span data-ttu-id="917bb-179">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="917bb-179">**Solution**:</span></span>

    SELECT
        CASE
            WHEN COUNT(*) = 1 THEN CONCAT('1 ', Make)
            ELSE CONCAT(CAST(COUNT(*) AS NVARCHAR(MAX)), ' ', Make, 's')
        END AS CarsPassed,
        System.TimeStamp AS Time
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="917bb-180">**Açıklama**: Merhaba **durumda** yan tümcesi (Bu örnekte, hello hello toplama penceresinde hello araba sayısı) bazı ölçütlere göre tooprovide farklı bir hesaplama verir.</span><span class="sxs-lookup"><span data-stu-id="917bb-180">**Explanation**: hello **CASE** clause allows us tooprovide a different computation, based on some criteria (in our case, hello count of hello cars in hello aggregate window).</span></span>

## <a name="query-example-send-data-toomultiple-outputs"></a><span data-ttu-id="917bb-181">Sorgu örnek: veri toomultiple çıkarır Gönder</span><span class="sxs-lookup"><span data-stu-id="917bb-181">Query example: Send data toomultiple outputs</span></span>
<span data-ttu-id="917bb-182">**Açıklama**: gönderme veri toomultiple tek bir iş hedeflerden çıktı.</span><span class="sxs-lookup"><span data-stu-id="917bb-182">**Description**: Send data toomultiple output targets from a single job.</span></span>
<span data-ttu-id="917bb-183">Örneğin, eşik tabanlı bir uyarı için verileri çözümlemek ve Arşiv tüm olayları tooblob depolama.</span><span class="sxs-lookup"><span data-stu-id="917bb-183">For example, analyze data for a threshold-based alert and archive all events tooblob storage.</span></span>

<span data-ttu-id="917bb-184">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="917bb-184">**Input**:</span></span>

| <span data-ttu-id="917bb-185">Yapma</span><span class="sxs-lookup"><span data-stu-id="917bb-185">Make</span></span> | <span data-ttu-id="917bb-186">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-186">Time</span></span> |
| --- | --- |
| <span data-ttu-id="917bb-187">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-187">Honda</span></span> |<span data-ttu-id="917bb-188">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-188">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="917bb-189">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-189">Honda</span></span> |<span data-ttu-id="917bb-190">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-190">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="917bb-191">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-191">Toyota</span></span> |<span data-ttu-id="917bb-192">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-192">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="917bb-193">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-193">Toyota</span></span> |<span data-ttu-id="917bb-194">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-194">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="917bb-195">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-195">Toyota</span></span> |<span data-ttu-id="917bb-196">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-196">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="917bb-197">**Output1**:</span><span class="sxs-lookup"><span data-stu-id="917bb-197">**Output1**:</span></span>

| <span data-ttu-id="917bb-198">Yapma</span><span class="sxs-lookup"><span data-stu-id="917bb-198">Make</span></span> | <span data-ttu-id="917bb-199">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-199">Time</span></span> |
| --- | --- |
| <span data-ttu-id="917bb-200">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-200">Honda</span></span> |<span data-ttu-id="917bb-201">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-201">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="917bb-202">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-202">Honda</span></span> |<span data-ttu-id="917bb-203">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-203">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="917bb-204">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-204">Toyota</span></span> |<span data-ttu-id="917bb-205">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-205">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="917bb-206">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-206">Toyota</span></span> |<span data-ttu-id="917bb-207">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-207">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="917bb-208">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-208">Toyota</span></span> |<span data-ttu-id="917bb-209">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-209">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="917bb-210">**Output2**:</span><span class="sxs-lookup"><span data-stu-id="917bb-210">**Output2**:</span></span>

| <span data-ttu-id="917bb-211">Yapma</span><span class="sxs-lookup"><span data-stu-id="917bb-211">Make</span></span> | <span data-ttu-id="917bb-212">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-212">Time</span></span> | <span data-ttu-id="917bb-213">Sayı</span><span class="sxs-lookup"><span data-stu-id="917bb-213">Count</span></span> |
| --- | --- | --- |
| <span data-ttu-id="917bb-214">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-214">Toyota</span></span> |<span data-ttu-id="917bb-215">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-215">2015-01-01T00:00:10.0000000Z</span></span> |<span data-ttu-id="917bb-216">3</span><span class="sxs-lookup"><span data-stu-id="917bb-216">3</span></span> |

<span data-ttu-id="917bb-217">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="917bb-217">**Solution**:</span></span>

    SELECT
        *
    INTO
        ArchiveOutput
    FROM
        Input TIMESTAMP BY Time

    SELECT
        Make,
        System.TimeStamp AS Time,
        COUNT(*) AS [Count]
    INTO
        AlertOutput
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)
    HAVING
        [Count] >= 3

<span data-ttu-id="917bb-218">**Açıklama**: Merhaba **INTO** yan tümcesi bu deyim hangisinin hello toowrite hello veri toofrom çıkarır Stream Analytics söyler.</span><span class="sxs-lookup"><span data-stu-id="917bb-218">**Explanation**: hello **INTO** clause tells Stream Analytics which of hello outputs toowrite hello data toofrom this statement.</span></span>
<span data-ttu-id="917bb-219">Merhaba ilk sorgudur bir geçiş diski biz adlı tooan çıkış aldık hello veri **ArchiveOutput**.</span><span class="sxs-lookup"><span data-stu-id="917bb-219">hello first query is a pass-through of hello data we received tooan output that we named **ArchiveOutput**.</span></span>
<span data-ttu-id="917bb-220">Merhaba ikinci sorgu mu bazı basit toplama ve filtreleme ve onu tooa aşağı akış uyarı sistemi hello sonuçları gönderir.</span><span class="sxs-lookup"><span data-stu-id="917bb-220">hello second query does some simple aggregation and filtering, and it sends hello results tooa downstream alerting system.</span></span>

<span data-ttu-id="917bb-221">Not hello sonuçlarını hello ortak tablo ifadelerinde (Cte'lerin) da kullanabilirsiniz (gibi **ile** deyimleri) birden çok çıktı deyimlerinde.</span><span class="sxs-lookup"><span data-stu-id="917bb-221">Note that you can also reuse hello results of hello common table expressions (CTEs) (such as **WITH** statements) in multiple output statements.</span></span> <span data-ttu-id="917bb-222">Bu seçenek daha az Okuyucular toohello giriş kaynağı açma avantaj hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="917bb-222">This option has hello added benefit of opening fewer readers toohello input source.</span></span>
<span data-ttu-id="917bb-223">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="917bb-223">For example:</span></span> 

    WITH AllRedCars AS (
        SELECT
            *
        FROM
            Input TIMESTAMP BY Time
        WHERE
            Color = 'red'
    )
    SELECT * INTO HondaOutput FROM AllRedCars WHERE Make = 'Honda'
    SELECT * INTO ToyotaOutput FROM AllRedCars WHERE Make = 'Toyota'

## <a name="query-example-count-unique-values"></a><span data-ttu-id="917bb-224">Sorgu örnek: Say benzersiz değerler</span><span class="sxs-lookup"><span data-stu-id="917bb-224">Query example: Count unique values</span></span>
<span data-ttu-id="917bb-225">**Açıklama**: saymak bir zaman penceresi içinde hello akışında görünür benzersiz alan değerlerini hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="917bb-225">**Description**: Count hello number of unique field values that appear in hello stream within a time window.</span></span>
<span data-ttu-id="917bb-226">Örneğin, kaç tane benzersiz bir 2 saniyelik penceresinde hello Ücretli Stand geçtiğini araçların yapar?</span><span class="sxs-lookup"><span data-stu-id="917bb-226">For example, how many unique makes of cars passed through hello toll booth in a 2-second window?</span></span>

<span data-ttu-id="917bb-227">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="917bb-227">**Input**:</span></span>

| <span data-ttu-id="917bb-228">Yapma</span><span class="sxs-lookup"><span data-stu-id="917bb-228">Make</span></span> | <span data-ttu-id="917bb-229">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-229">Time</span></span> |
| --- | --- |
| <span data-ttu-id="917bb-230">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-230">Honda</span></span> |<span data-ttu-id="917bb-231">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-231">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="917bb-232">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-232">Honda</span></span> |<span data-ttu-id="917bb-233">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-233">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="917bb-234">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-234">Toyota</span></span> |<span data-ttu-id="917bb-235">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-235">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="917bb-236">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-236">Toyota</span></span> |<span data-ttu-id="917bb-237">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-237">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="917bb-238">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-238">Toyota</span></span> |<span data-ttu-id="917bb-239">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-239">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="917bb-240">**Çıktı:**</span><span class="sxs-lookup"><span data-stu-id="917bb-240">**Output:**</span></span>

| <span data-ttu-id="917bb-241">Sayı</span><span class="sxs-lookup"><span data-stu-id="917bb-241">Count</span></span> | <span data-ttu-id="917bb-242">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-242">Time</span></span> |
| --- | --- |
| <span data-ttu-id="917bb-243">2</span><span class="sxs-lookup"><span data-stu-id="917bb-243">2</span></span> |<span data-ttu-id="917bb-244">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-244">2015-01-01T00:00:02.000Z</span></span> |
| <span data-ttu-id="917bb-245">1</span><span class="sxs-lookup"><span data-stu-id="917bb-245">1</span></span> |<span data-ttu-id="917bb-246">2015-01-01T00:00:04.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-246">2015-01-01T00:00:04.000Z</span></span> |

<span data-ttu-id="917bb-247">**Çözüm:**</span><span class="sxs-lookup"><span data-stu-id="917bb-247">**Solution:**</span></span>

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


<span data-ttu-id="917bb-248">**Açıklama:**
**sayısı (ayrı olun)** döndürür hello hello ayrı değerleri sayısı **olun** sütunu bir zaman penceresi içinde.</span><span class="sxs-lookup"><span data-stu-id="917bb-248">**Explanation:**
**COUNT(DISTINCT Make)** returns hello number of distinct values in hello **Make** column within a time window.</span></span>

## <a name="query-example-determine-if-a-value-has-changed"></a><span data-ttu-id="917bb-249">Sorgu örnek: bir değer değişip değişmediğini belirleyen</span><span class="sxs-lookup"><span data-stu-id="917bb-249">Query example: Determine if a value has changed</span></span>
<span data-ttu-id="917bb-250">**Açıklama**: hello geçerli değerinden farklı olması durumunda önceki bir değeri toodetermine bakın.</span><span class="sxs-lookup"><span data-stu-id="917bb-250">**Description**: Look at a previous value toodetermine if it is different than hello current value.</span></span>
<span data-ttu-id="917bb-251">Örneğin, aynı olarak hello geçerli otomobil olun hello Ücretli yol hello üzerinde hello önceki araba mi?</span><span class="sxs-lookup"><span data-stu-id="917bb-251">For example, is hello previous car on hello toll road hello same make as hello current car?</span></span>

<span data-ttu-id="917bb-252">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="917bb-252">**Input**:</span></span>

| <span data-ttu-id="917bb-253">Yapma</span><span class="sxs-lookup"><span data-stu-id="917bb-253">Make</span></span> | <span data-ttu-id="917bb-254">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-254">Time</span></span> |
| --- | --- |
| <span data-ttu-id="917bb-255">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-255">Honda</span></span> |<span data-ttu-id="917bb-256">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-256">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="917bb-257">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-257">Toyota</span></span> |<span data-ttu-id="917bb-258">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-258">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="917bb-259">**Çıktı**:</span><span class="sxs-lookup"><span data-stu-id="917bb-259">**Output**:</span></span>

| <span data-ttu-id="917bb-260">Yapma</span><span class="sxs-lookup"><span data-stu-id="917bb-260">Make</span></span> | <span data-ttu-id="917bb-261">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-261">Time</span></span> |
| --- | --- |
| <span data-ttu-id="917bb-262">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-262">Toyota</span></span> |<span data-ttu-id="917bb-263">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-263">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="917bb-264">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="917bb-264">**Solution**:</span></span>

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

<span data-ttu-id="917bb-265">**Açıklama**: kullanım **GECİKME** toopeek hello içine geri bir olay akışı giriş ve hello alma **olun** değeri.</span><span class="sxs-lookup"><span data-stu-id="917bb-265">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="917bb-266">Toohello karşılaştırmak **olun** değer hello geçerli olay ve çıktı hello olay farklı ise.</span><span class="sxs-lookup"><span data-stu-id="917bb-266">Then compare it toohello **Make** value on hello current event and output hello event if they are different.</span></span>

## <a name="query-example-find-hello-first-event-in-a-window"></a><span data-ttu-id="917bb-267">Sorgu örnek: bir penceresinde hello ilk olay Bul</span><span class="sxs-lookup"><span data-stu-id="917bb-267">Query example: Find hello first event in a window</span></span>
<span data-ttu-id="917bb-268">**Açıklama**: Bul hello ilk otomobil her 10 dakikalık zaman aralığı içinde.</span><span class="sxs-lookup"><span data-stu-id="917bb-268">**Description**: Find hello first car in every 10-minute interval.</span></span>

<span data-ttu-id="917bb-269">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="917bb-269">**Input**:</span></span>

| <span data-ttu-id="917bb-270">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="917bb-270">LicensePlate</span></span> | <span data-ttu-id="917bb-271">Yapma</span><span class="sxs-lookup"><span data-stu-id="917bb-271">Make</span></span> | <span data-ttu-id="917bb-272">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-272">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="917bb-273">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="917bb-273">DXE 5291</span></span> |<span data-ttu-id="917bb-274">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-274">Honda</span></span> |<span data-ttu-id="917bb-275">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-275">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="917bb-276">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="917bb-276">YZK 5704</span></span> |<span data-ttu-id="917bb-277">Ford</span><span class="sxs-lookup"><span data-stu-id="917bb-277">Ford</span></span> |<span data-ttu-id="917bb-278">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-278">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="917bb-279">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="917bb-279">RMV 8282</span></span> |<span data-ttu-id="917bb-280">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-280">Honda</span></span> |<span data-ttu-id="917bb-281">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-281">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="917bb-282">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="917bb-282">YHN 6970</span></span> |<span data-ttu-id="917bb-283">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-283">Toyota</span></span> |<span data-ttu-id="917bb-284">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-284">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="917bb-285">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="917bb-285">VFE 1616</span></span> |<span data-ttu-id="917bb-286">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-286">Toyota</span></span> |<span data-ttu-id="917bb-287">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-287">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="917bb-288">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="917bb-288">QYF 9358</span></span> |<span data-ttu-id="917bb-289">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-289">Honda</span></span> |<span data-ttu-id="917bb-290">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-290">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="917bb-291">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="917bb-291">MDR 6128</span></span> |<span data-ttu-id="917bb-292">BMW</span><span class="sxs-lookup"><span data-stu-id="917bb-292">BMW</span></span> |<span data-ttu-id="917bb-293">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-293">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="917bb-294">**Çıktı**:</span><span class="sxs-lookup"><span data-stu-id="917bb-294">**Output**:</span></span>

| <span data-ttu-id="917bb-295">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="917bb-295">LicensePlate</span></span> | <span data-ttu-id="917bb-296">Yapma</span><span class="sxs-lookup"><span data-stu-id="917bb-296">Make</span></span> | <span data-ttu-id="917bb-297">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-297">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="917bb-298">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="917bb-298">DXE 5291</span></span> |<span data-ttu-id="917bb-299">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-299">Honda</span></span> |<span data-ttu-id="917bb-300">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-300">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="917bb-301">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="917bb-301">QYF 9358</span></span> |<span data-ttu-id="917bb-302">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-302">Honda</span></span> |<span data-ttu-id="917bb-303">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-303">2015-07-27T00:12:02.0000000Z</span></span> |

<span data-ttu-id="917bb-304">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="917bb-304">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

<span data-ttu-id="917bb-305">Değişiklik hello sorun ve Bul hello ilk arabanızın belirli bir olalım artık her 10 dakika arayla.</span><span class="sxs-lookup"><span data-stu-id="917bb-305">Now let’s change hello problem and find hello first car of a particular make in every 10-minute interval.</span></span>

| <span data-ttu-id="917bb-306">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="917bb-306">LicensePlate</span></span> | <span data-ttu-id="917bb-307">Yapma</span><span class="sxs-lookup"><span data-stu-id="917bb-307">Make</span></span> | <span data-ttu-id="917bb-308">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-308">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="917bb-309">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="917bb-309">DXE 5291</span></span> |<span data-ttu-id="917bb-310">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-310">Honda</span></span> |<span data-ttu-id="917bb-311">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-311">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="917bb-312">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="917bb-312">YZK 5704</span></span> |<span data-ttu-id="917bb-313">Ford</span><span class="sxs-lookup"><span data-stu-id="917bb-313">Ford</span></span> |<span data-ttu-id="917bb-314">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-314">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="917bb-315">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="917bb-315">YHN 6970</span></span> |<span data-ttu-id="917bb-316">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-316">Toyota</span></span> |<span data-ttu-id="917bb-317">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-317">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="917bb-318">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="917bb-318">QYF 9358</span></span> |<span data-ttu-id="917bb-319">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-319">Honda</span></span> |<span data-ttu-id="917bb-320">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-320">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="917bb-321">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="917bb-321">MDR 6128</span></span> |<span data-ttu-id="917bb-322">BMW</span><span class="sxs-lookup"><span data-stu-id="917bb-322">BMW</span></span> |<span data-ttu-id="917bb-323">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-323">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="917bb-324">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="917bb-324">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-hello-last-event-in-a-window"></a><span data-ttu-id="917bb-325">Sorgu örnek: bir penceresinde hello son olay Bul</span><span class="sxs-lookup"><span data-stu-id="917bb-325">Query example: Find hello last event in a window</span></span>
<span data-ttu-id="917bb-326">**Açıklama**: Bul hello son otomobil her 10 dakikalık zaman aralığı içinde.</span><span class="sxs-lookup"><span data-stu-id="917bb-326">**Description**: Find hello last car in every 10-minute interval.</span></span>

<span data-ttu-id="917bb-327">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="917bb-327">**Input**:</span></span>

| <span data-ttu-id="917bb-328">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="917bb-328">LicensePlate</span></span> | <span data-ttu-id="917bb-329">Yapma</span><span class="sxs-lookup"><span data-stu-id="917bb-329">Make</span></span> | <span data-ttu-id="917bb-330">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-330">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="917bb-331">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="917bb-331">DXE 5291</span></span> |<span data-ttu-id="917bb-332">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-332">Honda</span></span> |<span data-ttu-id="917bb-333">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-333">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="917bb-334">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="917bb-334">YZK 5704</span></span> |<span data-ttu-id="917bb-335">Ford</span><span class="sxs-lookup"><span data-stu-id="917bb-335">Ford</span></span> |<span data-ttu-id="917bb-336">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-336">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="917bb-337">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="917bb-337">RMV 8282</span></span> |<span data-ttu-id="917bb-338">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-338">Honda</span></span> |<span data-ttu-id="917bb-339">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-339">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="917bb-340">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="917bb-340">YHN 6970</span></span> |<span data-ttu-id="917bb-341">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-341">Toyota</span></span> |<span data-ttu-id="917bb-342">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-342">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="917bb-343">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="917bb-343">VFE 1616</span></span> |<span data-ttu-id="917bb-344">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-344">Toyota</span></span> |<span data-ttu-id="917bb-345">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-345">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="917bb-346">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="917bb-346">QYF 9358</span></span> |<span data-ttu-id="917bb-347">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-347">Honda</span></span> |<span data-ttu-id="917bb-348">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-348">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="917bb-349">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="917bb-349">MDR 6128</span></span> |<span data-ttu-id="917bb-350">BMW</span><span class="sxs-lookup"><span data-stu-id="917bb-350">BMW</span></span> |<span data-ttu-id="917bb-351">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-351">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="917bb-352">**Çıktı**:</span><span class="sxs-lookup"><span data-stu-id="917bb-352">**Output**:</span></span>

| <span data-ttu-id="917bb-353">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="917bb-353">LicensePlate</span></span> | <span data-ttu-id="917bb-354">Yapma</span><span class="sxs-lookup"><span data-stu-id="917bb-354">Make</span></span> | <span data-ttu-id="917bb-355">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-355">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="917bb-356">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="917bb-356">VFE 1616</span></span> |<span data-ttu-id="917bb-357">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-357">Toyota</span></span> |<span data-ttu-id="917bb-358">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-358">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="917bb-359">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="917bb-359">MDR 6128</span></span> |<span data-ttu-id="917bb-360">BMW</span><span class="sxs-lookup"><span data-stu-id="917bb-360">BMW</span></span> |<span data-ttu-id="917bb-361">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-361">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="917bb-362">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="917bb-362">**Solution**:</span></span>

    WITH LastInWindow AS
    (
        SELECT 
            MAX(Time) AS LastEventTime
        FROM 
            Input TIMESTAMP BY Time
        GROUP BY 
            TumblingWindow(minute, 10)
    )
    SELECT 
        Input.LicensePlate,
        Input.Make,
        Input.Time
    FROM
        Input TIMESTAMP BY Time 
        INNER JOIN LastInWindow
        ON DATEDIFF(minute, Input, LastInWindow) BETWEEN 0 AND 10
        AND Input.Time = LastInWindow.LastEventTime

<span data-ttu-id="917bb-363">**Açıklama**: hello sorguda iki adımı vardır.</span><span class="sxs-lookup"><span data-stu-id="917bb-363">**Explanation**: There are two steps in hello query.</span></span> <span data-ttu-id="917bb-364">Merhaba ilk bir bulur hello son zaman damgası 10 dakikalık Windows.</span><span class="sxs-lookup"><span data-stu-id="917bb-364">hello first one finds hello latest time stamp in 10-minute windows.</span></span> <span data-ttu-id="917bb-365">Merhaba ikinci adım birleştirmeler olaylarla hello son zaman damgaları her penceresinde eşleşen hello özgün akış toofind hello hello ilk sorgunun sonuçlarını hello.</span><span class="sxs-lookup"><span data-stu-id="917bb-365">hello second step joins hello results of hello first query with hello original stream toofind hello events that match hello last time stamps in each window.</span></span> 

## <a name="query-example-detect-hello-absence-of-events"></a><span data-ttu-id="917bb-366">Sorgu örnek: olayları hello yokluğu Algıla</span><span class="sxs-lookup"><span data-stu-id="917bb-366">Query example: Detect hello absence of events</span></span>
<span data-ttu-id="917bb-367">**Açıklama**: bir akış belirli bir ölçütle eşleşen herhangi bir değer olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="917bb-367">**Description**: Check that a stream has no value that matches a certain criterion.</span></span>
<span data-ttu-id="917bb-368">Örneğin, aynı olun hello gelen 2 ardışık araba hello Ücretli yol hello içinde son 90 saniye girdiğiniz?</span><span class="sxs-lookup"><span data-stu-id="917bb-368">For example, have 2 consecutive cars from hello same make entered hello toll road within hello last 90 seconds?</span></span>

<span data-ttu-id="917bb-369">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="917bb-369">**Input**:</span></span>

| <span data-ttu-id="917bb-370">Yapma</span><span class="sxs-lookup"><span data-stu-id="917bb-370">Make</span></span> | <span data-ttu-id="917bb-371">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="917bb-371">LicensePlate</span></span> | <span data-ttu-id="917bb-372">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-372">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="917bb-373">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-373">Honda</span></span> |<span data-ttu-id="917bb-374">ABC-123</span><span class="sxs-lookup"><span data-stu-id="917bb-374">ABC-123</span></span> |<span data-ttu-id="917bb-375">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-375">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="917bb-376">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-376">Honda</span></span> |<span data-ttu-id="917bb-377">AAA-999</span><span class="sxs-lookup"><span data-stu-id="917bb-377">AAA-999</span></span> |<span data-ttu-id="917bb-378">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-378">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="917bb-379">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-379">Toyota</span></span> |<span data-ttu-id="917bb-380">DEF 987</span><span class="sxs-lookup"><span data-stu-id="917bb-380">DEF-987</span></span> |<span data-ttu-id="917bb-381">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-381">2015-01-01T00:00:03.0000000Z</span></span> |
| <span data-ttu-id="917bb-382">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-382">Honda</span></span> |<span data-ttu-id="917bb-383">GHI 345</span><span class="sxs-lookup"><span data-stu-id="917bb-383">GHI-345</span></span> |<span data-ttu-id="917bb-384">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-384">2015-01-01T00:00:04.0000000Z</span></span> |

<span data-ttu-id="917bb-385">**Çıktı**:</span><span class="sxs-lookup"><span data-stu-id="917bb-385">**Output**:</span></span>

| <span data-ttu-id="917bb-386">Yapma</span><span class="sxs-lookup"><span data-stu-id="917bb-386">Make</span></span> | <span data-ttu-id="917bb-387">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-387">Time</span></span> | <span data-ttu-id="917bb-388">CurrentCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="917bb-388">CurrentCarLicensePlate</span></span> | <span data-ttu-id="917bb-389">FirstCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="917bb-389">FirstCarLicensePlate</span></span> | <span data-ttu-id="917bb-390">FirstCarTime</span><span class="sxs-lookup"><span data-stu-id="917bb-390">FirstCarTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="917bb-391">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-391">Honda</span></span> |<span data-ttu-id="917bb-392">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-392">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="917bb-393">AAA-999</span><span class="sxs-lookup"><span data-stu-id="917bb-393">AAA-999</span></span> |<span data-ttu-id="917bb-394">ABC-123</span><span class="sxs-lookup"><span data-stu-id="917bb-394">ABC-123</span></span> |<span data-ttu-id="917bb-395">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-395">2015-01-01T00:00:01.0000000Z</span></span> |

<span data-ttu-id="917bb-396">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="917bb-396">**Solution**:</span></span>

    SELECT
        Make,
        Time,
        LicensePlate AS CurrentCarLicensePlate,
        LAG(LicensePlate, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarLicensePlate,
        LAG(Time, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarTime
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(second, 90)) = Make

<span data-ttu-id="917bb-397">**Açıklama**: kullanım **GECİKME** toopeek hello içine geri bir olay akışı giriş ve hello alma **olun** değeri.</span><span class="sxs-lookup"><span data-stu-id="917bb-397">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="917bb-398">Toohello karşılaştırmak **olun** hello geçerli olay ve ardından olan Merhaba, aynı çıktı hello olay değeri.</span><span class="sxs-lookup"><span data-stu-id="917bb-398">Compare it toohello **MAKE** value in hello current event, and then output hello event if they are hello same.</span></span> <span data-ttu-id="917bb-399">Aynı zamanda **GECİKME** hello önceki araba hakkında tooget veriler.</span><span class="sxs-lookup"><span data-stu-id="917bb-399">You can also use **LAG** tooget data about hello previous car.</span></span>

## <a name="query-example-detect-hello-duration-between-events"></a><span data-ttu-id="917bb-400">Sorgu örnek: olaylar arasındaki süreyi hello Algıla</span><span class="sxs-lookup"><span data-stu-id="917bb-400">Query example: Detect hello duration between events</span></span>
<span data-ttu-id="917bb-401">**Açıklama**: hello süresi belirli bir olayın bulun.</span><span class="sxs-lookup"><span data-stu-id="917bb-401">**Description**: Find hello duration of a given event.</span></span> <span data-ttu-id="917bb-402">Örneğin, bir web clickstream göz önüne alındığında, bir özellik hello zamanın belirler.</span><span class="sxs-lookup"><span data-stu-id="917bb-402">For example, given a web clickstream, determine hello time spent on a feature.</span></span>

<span data-ttu-id="917bb-403">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="917bb-403">**Input**:</span></span>  

| <span data-ttu-id="917bb-404">Kullanıcı</span><span class="sxs-lookup"><span data-stu-id="917bb-404">User</span></span> | <span data-ttu-id="917bb-405">Özellik</span><span class="sxs-lookup"><span data-stu-id="917bb-405">Feature</span></span> | <span data-ttu-id="917bb-406">Olay</span><span class="sxs-lookup"><span data-stu-id="917bb-406">Event</span></span> | <span data-ttu-id="917bb-407">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-407">Time</span></span> |
| --- | --- | --- | --- |
| user@location.com |<span data-ttu-id="917bb-408">RightMenu</span><span class="sxs-lookup"><span data-stu-id="917bb-408">RightMenu</span></span> |<span data-ttu-id="917bb-409">Başlatma</span><span class="sxs-lookup"><span data-stu-id="917bb-409">Start</span></span> |<span data-ttu-id="917bb-410">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-410">2015-01-01T00:00:01.0000000Z</span></span> |
| user@location.com |<span data-ttu-id="917bb-411">RightMenu</span><span class="sxs-lookup"><span data-stu-id="917bb-411">RightMenu</span></span> |<span data-ttu-id="917bb-412">Bitiş</span><span class="sxs-lookup"><span data-stu-id="917bb-412">End</span></span> |<span data-ttu-id="917bb-413">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-413">2015-01-01T00:00:08.0000000Z</span></span> |

<span data-ttu-id="917bb-414">**Çıktı**:</span><span class="sxs-lookup"><span data-stu-id="917bb-414">**Output**:</span></span>  

| <span data-ttu-id="917bb-415">Kullanıcı</span><span class="sxs-lookup"><span data-stu-id="917bb-415">User</span></span> | <span data-ttu-id="917bb-416">Özellik</span><span class="sxs-lookup"><span data-stu-id="917bb-416">Feature</span></span> | <span data-ttu-id="917bb-417">Süre</span><span class="sxs-lookup"><span data-stu-id="917bb-417">Duration</span></span> |
| --- | --- | --- |
| user@location.com |<span data-ttu-id="917bb-418">RightMenu</span><span class="sxs-lookup"><span data-stu-id="917bb-418">RightMenu</span></span> |<span data-ttu-id="917bb-419">7</span><span class="sxs-lookup"><span data-stu-id="917bb-419">7</span></span> |

<span data-ttu-id="917bb-420">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="917bb-420">**Solution**:</span></span>

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

<span data-ttu-id="917bb-421">**Açıklama**: kullanım hello **son** tooretrieve hello son işlev **zaman** değer hello olay türü olduğu zaman **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="917bb-421">**Explanation**: Use hello **LAST** function tooretrieve hello last **TIME** value when hello event type was **Start**.</span></span> <span data-ttu-id="917bb-422">Merhaba **son** işlev kullanır **[kullanıcı] bölümü tarafından** sonuç hello tooindicate benzersiz kullanıcı başına hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="917bb-422">hello **LAST** function uses **PARTITION BY [user]** tooindicate that hello result is computed per unique user.</span></span> <span data-ttu-id="917bb-423">Merhaba sorgu sahip hello arasındaki zaman farkı bir 1 saatlik maksimum eşik **Başlat** ve **durdurmak** olayları, ancak gerektiği gibi yapılandırılabilir **(sınırı DURATION(hour, 1)**.</span><span class="sxs-lookup"><span data-stu-id="917bb-423">hello query has a 1-hour maximum threshold for hello time difference between **Start** and **Stop** events, but is configurable as needed **(LIMIT DURATION(hour, 1)**.</span></span>

## <a name="query-example-detect-hello-duration-of-a-condition"></a><span data-ttu-id="917bb-424">Sorgu örnek: Merhaba süresi bir koşul algılama</span><span class="sxs-lookup"><span data-stu-id="917bb-424">Query example: Detect hello duration of a condition</span></span>
<span data-ttu-id="917bb-425">**Açıklama**: Bul ne kadar giden bir koşul oluştu.</span><span class="sxs-lookup"><span data-stu-id="917bb-425">**Description**: Find out how long a condition occurred.</span></span>
<span data-ttu-id="917bb-426">Örneğin, bir hata (yukarıda 20.000 sterlin) yanlış bir ağırlık sahip tüm araba kaynaklandığını varsayalım.</span><span class="sxs-lookup"><span data-stu-id="917bb-426">For example, suppose that a bug resulted in all cars having an incorrect weight (above 20,000 pounds).</span></span> <span data-ttu-id="917bb-427">Merhaba hata toocompute hello süresi istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="917bb-427">We want toocompute hello duration of hello bug.</span></span>

<span data-ttu-id="917bb-428">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="917bb-428">**Input**:</span></span>

| <span data-ttu-id="917bb-429">Yapma</span><span class="sxs-lookup"><span data-stu-id="917bb-429">Make</span></span> | <span data-ttu-id="917bb-430">Zaman</span><span class="sxs-lookup"><span data-stu-id="917bb-430">Time</span></span> | <span data-ttu-id="917bb-431">Ağırlık</span><span class="sxs-lookup"><span data-stu-id="917bb-431">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="917bb-432">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-432">Honda</span></span> |<span data-ttu-id="917bb-433">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-433">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="917bb-434">2000</span><span class="sxs-lookup"><span data-stu-id="917bb-434">2000</span></span> |
| <span data-ttu-id="917bb-435">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-435">Toyota</span></span> |<span data-ttu-id="917bb-436">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-436">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="917bb-437">25000</span><span class="sxs-lookup"><span data-stu-id="917bb-437">25000</span></span> |
| <span data-ttu-id="917bb-438">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-438">Honda</span></span> |<span data-ttu-id="917bb-439">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-439">2015-01-01T00:00:03.0000000Z</span></span> |<span data-ttu-id="917bb-440">26000</span><span class="sxs-lookup"><span data-stu-id="917bb-440">26000</span></span> |
| <span data-ttu-id="917bb-441">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-441">Toyota</span></span> |<span data-ttu-id="917bb-442">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-442">2015-01-01T00:00:04.0000000Z</span></span> |<span data-ttu-id="917bb-443">25000</span><span class="sxs-lookup"><span data-stu-id="917bb-443">25000</span></span> |
| <span data-ttu-id="917bb-444">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-444">Honda</span></span> |<span data-ttu-id="917bb-445">2015-01-01T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-445">2015-01-01T00:00:05.0000000Z</span></span> |<span data-ttu-id="917bb-446">26000</span><span class="sxs-lookup"><span data-stu-id="917bb-446">26000</span></span> |
| <span data-ttu-id="917bb-447">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-447">Toyota</span></span> |<span data-ttu-id="917bb-448">2015-01-01T00:00:06.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-448">2015-01-01T00:00:06.0000000Z</span></span> |<span data-ttu-id="917bb-449">25000</span><span class="sxs-lookup"><span data-stu-id="917bb-449">25000</span></span> |
| <span data-ttu-id="917bb-450">Honda</span><span class="sxs-lookup"><span data-stu-id="917bb-450">Honda</span></span> |<span data-ttu-id="917bb-451">2015-01-01T00:00:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-451">2015-01-01T00:00:07.0000000Z</span></span> |<span data-ttu-id="917bb-452">26000</span><span class="sxs-lookup"><span data-stu-id="917bb-452">26000</span></span> |
| <span data-ttu-id="917bb-453">Toyota</span><span class="sxs-lookup"><span data-stu-id="917bb-453">Toyota</span></span> |<span data-ttu-id="917bb-454">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-454">2015-01-01T00:00:08.0000000Z</span></span> |<span data-ttu-id="917bb-455">2000</span><span class="sxs-lookup"><span data-stu-id="917bb-455">2000</span></span> |

<span data-ttu-id="917bb-456">**Çıktı**:</span><span class="sxs-lookup"><span data-stu-id="917bb-456">**Output**:</span></span>

| <span data-ttu-id="917bb-457">StartFault</span><span class="sxs-lookup"><span data-stu-id="917bb-457">StartFault</span></span> | <span data-ttu-id="917bb-458">EndFault</span><span class="sxs-lookup"><span data-stu-id="917bb-458">EndFault</span></span> |
| --- | --- |
| <span data-ttu-id="917bb-459">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-459">2015-01-01T00:00:02.000Z</span></span> |<span data-ttu-id="917bb-460">2015-01-01T00:00:07.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-460">2015-01-01T00:00:07.000Z</span></span> |

<span data-ttu-id="917bb-461">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="917bb-461">**Solution**:</span></span>

````
    WITH SelectPreviousEvent AS
    (
    SELECT
    *,
        LAG([time]) OVER (LIMIT DURATION(hour, 24)) as previousTime,
        LAG([weight]) OVER (LIMIT DURATION(hour, 24)) as previousWeight
    FROM input TIMESTAMP BY [time]
    )

    SELECT 
        LAG(time) OVER (LIMIT DURATION(hour, 24) WHEN previousWeight < 20000 ) [StartFault],
        previousTime [EndFault]
    FROM SelectPreviousEvent
    WHERE
        [weight] < 20000
        AND previousWeight > 20000
````

<span data-ttu-id="917bb-462">**Açıklama**: kullanım **GECİKME** tooview hello Giriş akışı 24 saat ve Ara örnekler where **StartFault** ve **StopFault** hello tarafından kapsanan < 20000 ağırlık.</span><span class="sxs-lookup"><span data-stu-id="917bb-462">**Explanation**: Use **LAG** tooview hello input stream for 24 hours and look for instances where **StartFault** and **StopFault** are spanned by hello weight < 20000.</span></span>

## <a name="query-example-fill-missing-values"></a><span data-ttu-id="917bb-463">Sorgu örnek: eksik değerleri doldurma</span><span class="sxs-lookup"><span data-stu-id="917bb-463">Query example: Fill missing values</span></span>
<span data-ttu-id="917bb-464">**Açıklama**: eksik değerleri olan olayları hello akışı için düzenli aralıklarla olaylarla akışı üretir.</span><span class="sxs-lookup"><span data-stu-id="917bb-464">**Description**: For hello stream of events that have missing values, produce a stream of events with regular intervals.</span></span>
<span data-ttu-id="917bb-465">Örneğin, en son görülen hello veri noktası raporları 5 saniyede bir olayı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="917bb-465">For example, generate an event every 5 seconds that reports hello most recently seen data point.</span></span>

<span data-ttu-id="917bb-466">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="917bb-466">**Input**:</span></span>

| <span data-ttu-id="917bb-467">T</span><span class="sxs-lookup"><span data-stu-id="917bb-467">t</span></span> | <span data-ttu-id="917bb-468">değer</span><span class="sxs-lookup"><span data-stu-id="917bb-468">value</span></span> |
| --- | --- |
| <span data-ttu-id="917bb-469">"2014-01-01T06:01:00"</span><span class="sxs-lookup"><span data-stu-id="917bb-469">"2014-01-01T06:01:00"</span></span> |<span data-ttu-id="917bb-470">1</span><span class="sxs-lookup"><span data-stu-id="917bb-470">1</span></span> |
| <span data-ttu-id="917bb-471">"2014-01-01T06:01:05"</span><span class="sxs-lookup"><span data-stu-id="917bb-471">"2014-01-01T06:01:05"</span></span> |<span data-ttu-id="917bb-472">2</span><span class="sxs-lookup"><span data-stu-id="917bb-472">2</span></span> |
| <span data-ttu-id="917bb-473">"2014-01-01T06:01:10"</span><span class="sxs-lookup"><span data-stu-id="917bb-473">"2014-01-01T06:01:10"</span></span> |<span data-ttu-id="917bb-474">3</span><span class="sxs-lookup"><span data-stu-id="917bb-474">3</span></span> |
| <span data-ttu-id="917bb-475">"2014-01-01T06:01:15"</span><span class="sxs-lookup"><span data-stu-id="917bb-475">"2014-01-01T06:01:15"</span></span> |<span data-ttu-id="917bb-476">4</span><span class="sxs-lookup"><span data-stu-id="917bb-476">4</span></span> |
| <span data-ttu-id="917bb-477">"2014-01-01T06:01:30"</span><span class="sxs-lookup"><span data-stu-id="917bb-477">"2014-01-01T06:01:30"</span></span> |<span data-ttu-id="917bb-478">5</span><span class="sxs-lookup"><span data-stu-id="917bb-478">5</span></span> |
| <span data-ttu-id="917bb-479">"2014-01-01T06:01:35"</span><span class="sxs-lookup"><span data-stu-id="917bb-479">"2014-01-01T06:01:35"</span></span> |<span data-ttu-id="917bb-480">6</span><span class="sxs-lookup"><span data-stu-id="917bb-480">6</span></span> |

<span data-ttu-id="917bb-481">**Çıktı (ilk 10 satır)**:</span><span class="sxs-lookup"><span data-stu-id="917bb-481">**Output (first 10 rows)**:</span></span>

| <span data-ttu-id="917bb-482">windowend</span><span class="sxs-lookup"><span data-stu-id="917bb-482">windowend</span></span> | <span data-ttu-id="917bb-483">lastevent.t</span><span class="sxs-lookup"><span data-stu-id="917bb-483">lastevent.t</span></span> | <span data-ttu-id="917bb-484">lastevent.Value</span><span class="sxs-lookup"><span data-stu-id="917bb-484">lastevent.value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="917bb-485">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-485">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="917bb-486">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-486">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="917bb-487">1</span><span class="sxs-lookup"><span data-stu-id="917bb-487">1</span></span> |
| <span data-ttu-id="917bb-488">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-488">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="917bb-489">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-489">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="917bb-490">2</span><span class="sxs-lookup"><span data-stu-id="917bb-490">2</span></span> |
| <span data-ttu-id="917bb-491">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-491">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="917bb-492">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-492">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="917bb-493">3</span><span class="sxs-lookup"><span data-stu-id="917bb-493">3</span></span> |
| <span data-ttu-id="917bb-494">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-494">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="917bb-495">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-495">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="917bb-496">4</span><span class="sxs-lookup"><span data-stu-id="917bb-496">4</span></span> |
| <span data-ttu-id="917bb-497">2014-01-01T14:01:20.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-497">2014-01-01T14:01:20.000Z</span></span> |<span data-ttu-id="917bb-498">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-498">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="917bb-499">4</span><span class="sxs-lookup"><span data-stu-id="917bb-499">4</span></span> |
| <span data-ttu-id="917bb-500">2014-01-01T14:01:25.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-500">2014-01-01T14:01:25.000Z</span></span> |<span data-ttu-id="917bb-501">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-501">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="917bb-502">4</span><span class="sxs-lookup"><span data-stu-id="917bb-502">4</span></span> |
| <span data-ttu-id="917bb-503">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-503">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="917bb-504">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-504">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="917bb-505">5</span><span class="sxs-lookup"><span data-stu-id="917bb-505">5</span></span> |
| <span data-ttu-id="917bb-506">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-506">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="917bb-507">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-507">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="917bb-508">6</span><span class="sxs-lookup"><span data-stu-id="917bb-508">6</span></span> |
| <span data-ttu-id="917bb-509">2014-01-01T14:01:40.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-509">2014-01-01T14:01:40.000Z</span></span> |<span data-ttu-id="917bb-510">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-510">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="917bb-511">6</span><span class="sxs-lookup"><span data-stu-id="917bb-511">6</span></span> |
| <span data-ttu-id="917bb-512">2014-01-01T14:01:45.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-512">2014-01-01T14:01:45.000Z</span></span> |<span data-ttu-id="917bb-513">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="917bb-513">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="917bb-514">6</span><span class="sxs-lookup"><span data-stu-id="917bb-514">6</span></span> |

<span data-ttu-id="917bb-515">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="917bb-515">**Solution**:</span></span>

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


<span data-ttu-id="917bb-516">**Açıklama**: Bu sorguyu her 5 saniyede olaylar oluşturur ve çıkışları hello daha önce alındı son olay.</span><span class="sxs-lookup"><span data-stu-id="917bb-516">**Explanation**: This query generates events every 5 seconds and outputs hello last event that was received previously.</span></span> <span data-ttu-id="917bb-517">Merhaba [Hopping penceresi](https://msdn.microsoft.com/library/dn835041.aspx "Hopping penceresi--Azure akış analizi") süre belirler ne kadar geri hello sorgu toofind hello son olay (Bu örnekte 300 saniye) arar.</span><span class="sxs-lookup"><span data-stu-id="917bb-517">hello [Hopping window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping window--Azure Stream Analytics") duration determines how far back hello query looks toofind hello latest event (300 seconds in this example).</span></span>

## <a name="get-help"></a><span data-ttu-id="917bb-518">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="917bb-518">Get help</span></span>
<span data-ttu-id="917bb-519">Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="917bb-519">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="917bb-520">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="917bb-520">Next steps</span></span>
* [<span data-ttu-id="917bb-521">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="917bb-521">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="917bb-522">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="917bb-522">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="917bb-523">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="917bb-523">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="917bb-524">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="917bb-524">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="917bb-525">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="917bb-525">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

