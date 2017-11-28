---
title: "Örnekler için ortak kullanım desenlerini Stream Analytics sorgu | Microsoft Docs"
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
ms.openlocfilehash: a00855c200b3fb365073bad4c5773b02c4c2c7fe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a><span data-ttu-id="e17b4-104">Örnekler ortak Stream Analytics kullanım desenlerini için sorgu</span><span class="sxs-lookup"><span data-stu-id="e17b4-104">Query examples for common Stream Analytics usage patterns</span></span>
## <a name="introduction"></a><span data-ttu-id="e17b4-105">Giriş</span><span class="sxs-lookup"><span data-stu-id="e17b4-105">Introduction</span></span>
<span data-ttu-id="e17b4-106">Azure Stream Analytics sorgularda bir SQL benzeri sorgu dili ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="e17b4-106">Queries in Azure Stream Analytics are expressed in a SQL-like query language.</span></span> <span data-ttu-id="e17b4-107">Bu sorguları belgelenmiştir [Stream Analytics sorgu dili başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx) Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="e17b4-107">These queries are documented in the [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span></span> <span data-ttu-id="e17b4-108">Bu makalede gerçek senaryolarını temel alarak, birçok ortak sorgu kalıpları çözümleri özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="e17b4-108">This article outlines solutions to several common query patterns, based on real-world scenarios.</span></span> <span data-ttu-id="e17b4-109">Bu iş sürüyor ve düzenli olarak yeni desenlerle güncelleştirilmesi devam eder.</span><span class="sxs-lookup"><span data-stu-id="e17b4-109">It is a work in progress and continues to be updated with new patterns on an ongoing basis.</span></span>

## <a name="query-example-convert-data-types"></a><span data-ttu-id="e17b4-110">Sorgu örnek: veri türlerini dönüştürme</span><span class="sxs-lookup"><span data-stu-id="e17b4-110">Query example: Convert data types</span></span>
<span data-ttu-id="e17b4-111">**Açıklama**: Giriş akışı üzerinde özelliklerin türleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="e17b4-111">**Description**: Define the types of properties on the input stream.</span></span>
<span data-ttu-id="e17b4-112">Örneğin, araba ağırlık giriş akışta dize olarak geliyor ve dönüştürülmesi gerekiyor **INT** gerçekleştirmek için **toplam** bunun.</span><span class="sxs-lookup"><span data-stu-id="e17b4-112">For example, the car weight is coming on the input stream as strings and needs to be converted to **INT** to perform **SUM** it up.</span></span>

<span data-ttu-id="e17b4-113">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-113">**Input**:</span></span>

| <span data-ttu-id="e17b4-114">Yapma</span><span class="sxs-lookup"><span data-stu-id="e17b4-114">Make</span></span> | <span data-ttu-id="e17b4-115">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-115">Time</span></span> | <span data-ttu-id="e17b4-116">Ağırlık</span><span class="sxs-lookup"><span data-stu-id="e17b4-116">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e17b4-117">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-117">Honda</span></span> |<span data-ttu-id="e17b4-118">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-118">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="e17b4-119">"1000"</span><span class="sxs-lookup"><span data-stu-id="e17b4-119">"1000"</span></span> |
| <span data-ttu-id="e17b4-120">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-120">Honda</span></span> |<span data-ttu-id="e17b4-121">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-121">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="e17b4-122">"2000"</span><span class="sxs-lookup"><span data-stu-id="e17b4-122">"2000"</span></span> |

<span data-ttu-id="e17b4-123">**Çıktı**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-123">**Output**:</span></span>

| <span data-ttu-id="e17b4-124">Yapma</span><span class="sxs-lookup"><span data-stu-id="e17b4-124">Make</span></span> | <span data-ttu-id="e17b4-125">Ağırlık</span><span class="sxs-lookup"><span data-stu-id="e17b4-125">Weight</span></span> |
| --- | --- |
| <span data-ttu-id="e17b4-126">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-126">Honda</span></span> |<span data-ttu-id="e17b4-127">3000</span><span class="sxs-lookup"><span data-stu-id="e17b4-127">3000</span></span> |

<span data-ttu-id="e17b4-128">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-128">**Solution**:</span></span>

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="e17b4-129">**Açıklama**: kullanım bir **CAST** deyiminde **ağırlık** alanın veri türünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="e17b4-129">**Explanation**: Use a **CAST** statement in the **Weight** field to specify its data type.</span></span> <span data-ttu-id="e17b4-130">Desteklenen veri türleri listesini görmek [veri türleri (Azure akış analizi)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span><span class="sxs-lookup"><span data-stu-id="e17b4-130">See the list of supported data types in [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

## <a name="query-example-use-likenot-like-to-do-pattern-matching"></a><span data-ttu-id="e17b4-131">Sorgu örnek: kullanımı gibi/değil ister eşleştirme deseni</span><span class="sxs-lookup"><span data-stu-id="e17b4-131">Query example: Use Like/Not like to do pattern matching</span></span>
<span data-ttu-id="e17b4-132">**Açıklama**: olay bir alanın değerini belirli bir desene eşleşip eşleşmediğini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e17b4-132">**Description**: Check that a field value on the event matches a certain pattern.</span></span>
<span data-ttu-id="e17b4-133">Örneğin, sonuç ile başlamalı ve 9 ile bitmelidir lisans kalıplarını verir denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e17b4-133">For example, check that the result returns license plates that start with A and end with 9.</span></span>

<span data-ttu-id="e17b4-134">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-134">**Input**:</span></span>

| <span data-ttu-id="e17b4-135">Yapma</span><span class="sxs-lookup"><span data-stu-id="e17b4-135">Make</span></span> | <span data-ttu-id="e17b4-136">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="e17b4-136">LicensePlate</span></span> | <span data-ttu-id="e17b4-137">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-137">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e17b4-138">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-138">Honda</span></span> |<span data-ttu-id="e17b4-139">ABC-123</span><span class="sxs-lookup"><span data-stu-id="e17b4-139">ABC-123</span></span> |<span data-ttu-id="e17b4-140">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-140">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="e17b4-141">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-141">Toyota</span></span> |<span data-ttu-id="e17b4-142">AAA-999</span><span class="sxs-lookup"><span data-stu-id="e17b4-142">AAA-999</span></span> |<span data-ttu-id="e17b4-143">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-143">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="e17b4-144">Nissan</span><span class="sxs-lookup"><span data-stu-id="e17b4-144">Nissan</span></span> |<span data-ttu-id="e17b4-145">ABC 369</span><span class="sxs-lookup"><span data-stu-id="e17b4-145">ABC-369</span></span> |<span data-ttu-id="e17b4-146">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-146">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="e17b4-147">**Çıktı**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-147">**Output**:</span></span>

| <span data-ttu-id="e17b4-148">Yapma</span><span class="sxs-lookup"><span data-stu-id="e17b4-148">Make</span></span> | <span data-ttu-id="e17b4-149">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="e17b4-149">LicensePlate</span></span> | <span data-ttu-id="e17b4-150">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-150">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e17b4-151">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-151">Toyota</span></span> |<span data-ttu-id="e17b4-152">AAA-999</span><span class="sxs-lookup"><span data-stu-id="e17b4-152">AAA-999</span></span> |<span data-ttu-id="e17b4-153">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-153">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="e17b4-154">Nissan</span><span class="sxs-lookup"><span data-stu-id="e17b4-154">Nissan</span></span> |<span data-ttu-id="e17b4-155">ABC 369</span><span class="sxs-lookup"><span data-stu-id="e17b4-155">ABC-369</span></span> |<span data-ttu-id="e17b4-156">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-156">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="e17b4-157">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-157">**Solution**:</span></span>

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

<span data-ttu-id="e17b4-158">**Açıklama**: kullanım **gibi** denetlemek için deyimi **LicensePlate** alan değer.</span><span class="sxs-lookup"><span data-stu-id="e17b4-158">**Explanation**: Use the **LIKE** statement to check the **LicensePlate** field value.</span></span> <span data-ttu-id="e17b4-159">Bu bir ile başlayan sonra sıfır veya daha fazla karakterden oluşan herhangi bir dize olması ve ardından 9 ile bitmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e17b4-159">It should start with an A, then have any string of zero or more characters, and then end with a 9.</span></span> 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a><span data-ttu-id="e17b4-160">Sorgu örnek: farklı durumlarda/değerleri (CASE deyimleri) için mantığı belirtin</span><span class="sxs-lookup"><span data-stu-id="e17b4-160">Query example: Specify logic for different cases/values (CASE statements)</span></span>
<span data-ttu-id="e17b4-161">**Açıklama**: belirli bir ölçütü temel alan bir alan için farklı bir hesaplama sağlar.</span><span class="sxs-lookup"><span data-stu-id="e17b4-161">**Description**: Provide a different computation for a field, based on a particular criterion.</span></span>
<span data-ttu-id="e17b4-162">Örneğin, 1 için özel bir durum ile aynı kaç araba yapmak için dize açıklamasını geçirilen sağlar.</span><span class="sxs-lookup"><span data-stu-id="e17b4-162">For example, provide a string description for how many cars of the same make passed, with a special case for 1.</span></span>

<span data-ttu-id="e17b4-163">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-163">**Input**:</span></span>

| <span data-ttu-id="e17b4-164">Yapma</span><span class="sxs-lookup"><span data-stu-id="e17b4-164">Make</span></span> | <span data-ttu-id="e17b4-165">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-165">Time</span></span> |
| --- | --- |
| <span data-ttu-id="e17b4-166">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-166">Honda</span></span> |<span data-ttu-id="e17b4-167">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-167">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="e17b4-168">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-168">Toyota</span></span> |<span data-ttu-id="e17b4-169">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-169">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="e17b4-170">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-170">Toyota</span></span> |<span data-ttu-id="e17b4-171">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-171">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="e17b4-172">**Çıktı**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-172">**Output**:</span></span>

| <span data-ttu-id="e17b4-173">CarsPassed</span><span class="sxs-lookup"><span data-stu-id="e17b4-173">CarsPassed</span></span> | <span data-ttu-id="e17b4-174">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-174">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e17b4-175">1 Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-175">1 Honda</span></span> |<span data-ttu-id="e17b4-176">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-176">2015-01-01T00:00:10.0000000Z</span></span> |
| <span data-ttu-id="e17b4-177">2 Toyotas</span><span class="sxs-lookup"><span data-stu-id="e17b4-177">2 Toyotas</span></span> |<span data-ttu-id="e17b4-178">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-178">2015-01-01T00:00:10.0000000Z</span></span> |

<span data-ttu-id="e17b4-179">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-179">**Solution**:</span></span>

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

<span data-ttu-id="e17b4-180">**Açıklama**: **durumda** yan tümcesi (Bu örnekte, toplama penceresinde araba sayısı) bazı ölçütlere göre farklı bir hesaplama sağlamamız sağlar.</span><span class="sxs-lookup"><span data-stu-id="e17b4-180">**Explanation**: The **CASE** clause allows us to provide a different computation, based on some criteria (in our case, the count of the cars in the aggregate window).</span></span>

## <a name="query-example-send-data-to-multiple-outputs"></a><span data-ttu-id="e17b4-181">Sorgu örnek: birden çok çıkış veri gönderme</span><span class="sxs-lookup"><span data-stu-id="e17b4-181">Query example: Send data to multiple outputs</span></span>
<span data-ttu-id="e17b4-182">**Açıklama**: veri gönderme için birden çok çıktı hedefi tek bir işten.</span><span class="sxs-lookup"><span data-stu-id="e17b4-182">**Description**: Send data to multiple output targets from a single job.</span></span>
<span data-ttu-id="e17b4-183">Örneğin, eşik tabanlı bir uyarı için verileri çözümlemek ve blob depolama alanına tüm olayların arşivlenmesini.</span><span class="sxs-lookup"><span data-stu-id="e17b4-183">For example, analyze data for a threshold-based alert and archive all events to blob storage.</span></span>

<span data-ttu-id="e17b4-184">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-184">**Input**:</span></span>

| <span data-ttu-id="e17b4-185">Yapma</span><span class="sxs-lookup"><span data-stu-id="e17b4-185">Make</span></span> | <span data-ttu-id="e17b4-186">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-186">Time</span></span> |
| --- | --- |
| <span data-ttu-id="e17b4-187">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-187">Honda</span></span> |<span data-ttu-id="e17b4-188">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-188">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="e17b4-189">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-189">Honda</span></span> |<span data-ttu-id="e17b4-190">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-190">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="e17b4-191">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-191">Toyota</span></span> |<span data-ttu-id="e17b4-192">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-192">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="e17b4-193">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-193">Toyota</span></span> |<span data-ttu-id="e17b4-194">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-194">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="e17b4-195">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-195">Toyota</span></span> |<span data-ttu-id="e17b4-196">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-196">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="e17b4-197">**Output1**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-197">**Output1**:</span></span>

| <span data-ttu-id="e17b4-198">Yapma</span><span class="sxs-lookup"><span data-stu-id="e17b4-198">Make</span></span> | <span data-ttu-id="e17b4-199">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-199">Time</span></span> |
| --- | --- |
| <span data-ttu-id="e17b4-200">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-200">Honda</span></span> |<span data-ttu-id="e17b4-201">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-201">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="e17b4-202">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-202">Honda</span></span> |<span data-ttu-id="e17b4-203">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-203">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="e17b4-204">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-204">Toyota</span></span> |<span data-ttu-id="e17b4-205">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-205">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="e17b4-206">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-206">Toyota</span></span> |<span data-ttu-id="e17b4-207">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-207">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="e17b4-208">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-208">Toyota</span></span> |<span data-ttu-id="e17b4-209">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-209">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="e17b4-210">**Output2**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-210">**Output2**:</span></span>

| <span data-ttu-id="e17b4-211">Yapma</span><span class="sxs-lookup"><span data-stu-id="e17b4-211">Make</span></span> | <span data-ttu-id="e17b4-212">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-212">Time</span></span> | <span data-ttu-id="e17b4-213">Sayı</span><span class="sxs-lookup"><span data-stu-id="e17b4-213">Count</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e17b4-214">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-214">Toyota</span></span> |<span data-ttu-id="e17b4-215">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-215">2015-01-01T00:00:10.0000000Z</span></span> |<span data-ttu-id="e17b4-216">3</span><span class="sxs-lookup"><span data-stu-id="e17b4-216">3</span></span> |

<span data-ttu-id="e17b4-217">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-217">**Solution**:</span></span>

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

<span data-ttu-id="e17b4-218">**Açıklama**: **INTO** yan tümcesi söyler akış analizi, bu deyim için verileri yazmak için çıktı.</span><span class="sxs-lookup"><span data-stu-id="e17b4-218">**Explanation**: The **INTO** clause tells Stream Analytics which of the outputs to write the data to from this statement.</span></span>
<span data-ttu-id="e17b4-219">İlk sorguyu biz adlı bir çıktı aldık verilerin bir doğrudan sorgudur **ArchiveOutput**.</span><span class="sxs-lookup"><span data-stu-id="e17b4-219">The first query is a pass-through of the data we received to an output that we named **ArchiveOutput**.</span></span>
<span data-ttu-id="e17b4-220">Bazı basit toplama ve filtreleme ve ikinci sorguyu mu sonuçları bir aşağı akış uyarı sisteme gönderir.</span><span class="sxs-lookup"><span data-stu-id="e17b4-220">The second query does some simple aggregation and filtering, and it sends the results to a downstream alerting system.</span></span>

<span data-ttu-id="e17b4-221">Not ortak tablo ifadelerinde (Cte'lerin) sonuçlarını da kullanabilirsiniz (gibi **ile** deyimleri) birden çok çıktı deyimlerinde.</span><span class="sxs-lookup"><span data-stu-id="e17b4-221">Note that you can also reuse the results of the common table expressions (CTEs) (such as **WITH** statements) in multiple output statements.</span></span> <span data-ttu-id="e17b4-222">Bu seçenek daha az giriş kaynağı okuyucularına açma avantaj vardır.</span><span class="sxs-lookup"><span data-stu-id="e17b4-222">This option has the added benefit of opening fewer readers to the input source.</span></span>
<span data-ttu-id="e17b4-223">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="e17b4-223">For example:</span></span> 

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

## <a name="query-example-count-unique-values"></a><span data-ttu-id="e17b4-224">Sorgu örnek: Say benzersiz değerler</span><span class="sxs-lookup"><span data-stu-id="e17b4-224">Query example: Count unique values</span></span>
<span data-ttu-id="e17b4-225">**Açıklama**: bir zaman penceresi içinde akışında görünür benzersiz alan değerleri sayar.</span><span class="sxs-lookup"><span data-stu-id="e17b4-225">**Description**: Count the number of unique field values that appear in the stream within a time window.</span></span>
<span data-ttu-id="e17b4-226">Örneğin, kaç tane benzersiz bir 2 saniyelik penceresinde Ücretli Stand geçtiğini araçların yapar?</span><span class="sxs-lookup"><span data-stu-id="e17b4-226">For example, how many unique makes of cars passed through the toll booth in a 2-second window?</span></span>

<span data-ttu-id="e17b4-227">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-227">**Input**:</span></span>

| <span data-ttu-id="e17b4-228">Yapma</span><span class="sxs-lookup"><span data-stu-id="e17b4-228">Make</span></span> | <span data-ttu-id="e17b4-229">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-229">Time</span></span> |
| --- | --- |
| <span data-ttu-id="e17b4-230">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-230">Honda</span></span> |<span data-ttu-id="e17b4-231">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-231">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="e17b4-232">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-232">Honda</span></span> |<span data-ttu-id="e17b4-233">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-233">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="e17b4-234">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-234">Toyota</span></span> |<span data-ttu-id="e17b4-235">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-235">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="e17b4-236">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-236">Toyota</span></span> |<span data-ttu-id="e17b4-237">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-237">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="e17b4-238">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-238">Toyota</span></span> |<span data-ttu-id="e17b4-239">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-239">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="e17b4-240">**Çıktı:**</span><span class="sxs-lookup"><span data-stu-id="e17b4-240">**Output:**</span></span>

| <span data-ttu-id="e17b4-241">Sayı</span><span class="sxs-lookup"><span data-stu-id="e17b4-241">Count</span></span> | <span data-ttu-id="e17b4-242">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-242">Time</span></span> |
| --- | --- |
| <span data-ttu-id="e17b4-243">2</span><span class="sxs-lookup"><span data-stu-id="e17b4-243">2</span></span> |<span data-ttu-id="e17b4-244">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-244">2015-01-01T00:00:02.000Z</span></span> |
| <span data-ttu-id="e17b4-245">1</span><span class="sxs-lookup"><span data-stu-id="e17b4-245">1</span></span> |<span data-ttu-id="e17b4-246">2015-01-01T00:00:04.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-246">2015-01-01T00:00:04.000Z</span></span> |

<span data-ttu-id="e17b4-247">**Çözüm:**</span><span class="sxs-lookup"><span data-stu-id="e17b4-247">**Solution:**</span></span>

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


<span data-ttu-id="e17b4-248">**Açıklama:**
**sayısı (ayrı olun)** ayrı değerleri sayısını döndürür **olun** sütunu bir zaman penceresi içinde.</span><span class="sxs-lookup"><span data-stu-id="e17b4-248">**Explanation:**
**COUNT(DISTINCT Make)** returns the number of distinct values in the **Make** column within a time window.</span></span>

## <a name="query-example-determine-if-a-value-has-changed"></a><span data-ttu-id="e17b4-249">Sorgu örnek: bir değer değişip değişmediğini belirleyen</span><span class="sxs-lookup"><span data-stu-id="e17b4-249">Query example: Determine if a value has changed</span></span>
<span data-ttu-id="e17b4-250">**Açıklama**: geçerli değerden farklı olup olmadığını belirlemek için önceki bir değeri bakın.</span><span class="sxs-lookup"><span data-stu-id="e17b4-250">**Description**: Look at a previous value to determine if it is different than the current value.</span></span>
<span data-ttu-id="e17b4-251">Örneğin, önceki araba Ücretli yolda geçerli araba olarak aynı marka mi?</span><span class="sxs-lookup"><span data-stu-id="e17b4-251">For example, is the previous car on the toll road the same make as the current car?</span></span>

<span data-ttu-id="e17b4-252">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-252">**Input**:</span></span>

| <span data-ttu-id="e17b4-253">Yapma</span><span class="sxs-lookup"><span data-stu-id="e17b4-253">Make</span></span> | <span data-ttu-id="e17b4-254">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-254">Time</span></span> |
| --- | --- |
| <span data-ttu-id="e17b4-255">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-255">Honda</span></span> |<span data-ttu-id="e17b4-256">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-256">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="e17b4-257">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-257">Toyota</span></span> |<span data-ttu-id="e17b4-258">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-258">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="e17b4-259">**Çıktı**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-259">**Output**:</span></span>

| <span data-ttu-id="e17b4-260">Yapma</span><span class="sxs-lookup"><span data-stu-id="e17b4-260">Make</span></span> | <span data-ttu-id="e17b4-261">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-261">Time</span></span> |
| --- | --- |
| <span data-ttu-id="e17b4-262">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-262">Toyota</span></span> |<span data-ttu-id="e17b4-263">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-263">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="e17b4-264">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-264">**Solution**:</span></span>

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

<span data-ttu-id="e17b4-265">**Açıklama**: kullanım **GECİKME** Giriş akışı bir olay geri gözatma ve almak için **olun** değeri.</span><span class="sxs-lookup"><span data-stu-id="e17b4-265">**Explanation**: Use **LAG** to peek into the input stream one event back and get the **Make** value.</span></span> <span data-ttu-id="e17b4-266">Kendisine karşılaştırmak **olun** değeri geçerli olayında ve bunlar farklıysa olay çıktı.</span><span class="sxs-lookup"><span data-stu-id="e17b4-266">Then compare it to the **Make** value on the current event and output the event if they are different.</span></span>

## <a name="query-example-find-the-first-event-in-a-window"></a><span data-ttu-id="e17b4-267">Sorgu örnek: bir pencerede ilk olay Bul</span><span class="sxs-lookup"><span data-stu-id="e17b4-267">Query example: Find the first event in a window</span></span>
<span data-ttu-id="e17b4-268">**Açıklama**: ilk arabanızın her 10 dakika arayla bulun.</span><span class="sxs-lookup"><span data-stu-id="e17b4-268">**Description**: Find the first car in every 10-minute interval.</span></span>

<span data-ttu-id="e17b4-269">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-269">**Input**:</span></span>

| <span data-ttu-id="e17b4-270">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="e17b4-270">LicensePlate</span></span> | <span data-ttu-id="e17b4-271">Yapma</span><span class="sxs-lookup"><span data-stu-id="e17b4-271">Make</span></span> | <span data-ttu-id="e17b4-272">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-272">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e17b4-273">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="e17b4-273">DXE 5291</span></span> |<span data-ttu-id="e17b4-274">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-274">Honda</span></span> |<span data-ttu-id="e17b4-275">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-275">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="e17b4-276">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="e17b4-276">YZK 5704</span></span> |<span data-ttu-id="e17b4-277">Ford</span><span class="sxs-lookup"><span data-stu-id="e17b4-277">Ford</span></span> |<span data-ttu-id="e17b4-278">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-278">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="e17b4-279">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="e17b4-279">RMV 8282</span></span> |<span data-ttu-id="e17b4-280">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-280">Honda</span></span> |<span data-ttu-id="e17b4-281">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-281">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="e17b4-282">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="e17b4-282">YHN 6970</span></span> |<span data-ttu-id="e17b4-283">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-283">Toyota</span></span> |<span data-ttu-id="e17b4-284">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-284">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="e17b4-285">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="e17b4-285">VFE 1616</span></span> |<span data-ttu-id="e17b4-286">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-286">Toyota</span></span> |<span data-ttu-id="e17b4-287">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-287">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="e17b4-288">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="e17b4-288">QYF 9358</span></span> |<span data-ttu-id="e17b4-289">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-289">Honda</span></span> |<span data-ttu-id="e17b4-290">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-290">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="e17b4-291">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="e17b4-291">MDR 6128</span></span> |<span data-ttu-id="e17b4-292">BMW</span><span class="sxs-lookup"><span data-stu-id="e17b4-292">BMW</span></span> |<span data-ttu-id="e17b4-293">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-293">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="e17b4-294">**Çıktı**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-294">**Output**:</span></span>

| <span data-ttu-id="e17b4-295">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="e17b4-295">LicensePlate</span></span> | <span data-ttu-id="e17b4-296">Yapma</span><span class="sxs-lookup"><span data-stu-id="e17b4-296">Make</span></span> | <span data-ttu-id="e17b4-297">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-297">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e17b4-298">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="e17b4-298">DXE 5291</span></span> |<span data-ttu-id="e17b4-299">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-299">Honda</span></span> |<span data-ttu-id="e17b4-300">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-300">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="e17b4-301">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="e17b4-301">QYF 9358</span></span> |<span data-ttu-id="e17b4-302">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-302">Honda</span></span> |<span data-ttu-id="e17b4-303">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-303">2015-07-27T00:12:02.0000000Z</span></span> |

<span data-ttu-id="e17b4-304">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-304">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

<span data-ttu-id="e17b4-305">Şimdi şimdi sorun değiştirin ve belirli olun, ilk arabanızın her 10 dakika arayla bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e17b4-305">Now let’s change the problem and find the first car of a particular make in every 10-minute interval.</span></span>

| <span data-ttu-id="e17b4-306">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="e17b4-306">LicensePlate</span></span> | <span data-ttu-id="e17b4-307">Yapma</span><span class="sxs-lookup"><span data-stu-id="e17b4-307">Make</span></span> | <span data-ttu-id="e17b4-308">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-308">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e17b4-309">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="e17b4-309">DXE 5291</span></span> |<span data-ttu-id="e17b4-310">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-310">Honda</span></span> |<span data-ttu-id="e17b4-311">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-311">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="e17b4-312">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="e17b4-312">YZK 5704</span></span> |<span data-ttu-id="e17b4-313">Ford</span><span class="sxs-lookup"><span data-stu-id="e17b4-313">Ford</span></span> |<span data-ttu-id="e17b4-314">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-314">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="e17b4-315">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="e17b4-315">YHN 6970</span></span> |<span data-ttu-id="e17b4-316">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-316">Toyota</span></span> |<span data-ttu-id="e17b4-317">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-317">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="e17b4-318">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="e17b4-318">QYF 9358</span></span> |<span data-ttu-id="e17b4-319">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-319">Honda</span></span> |<span data-ttu-id="e17b4-320">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-320">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="e17b4-321">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="e17b4-321">MDR 6128</span></span> |<span data-ttu-id="e17b4-322">BMW</span><span class="sxs-lookup"><span data-stu-id="e17b4-322">BMW</span></span> |<span data-ttu-id="e17b4-323">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-323">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="e17b4-324">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-324">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-the-last-event-in-a-window"></a><span data-ttu-id="e17b4-325">Sorgu örnek: bir penceresinde son olayı bulun</span><span class="sxs-lookup"><span data-stu-id="e17b4-325">Query example: Find the last event in a window</span></span>
<span data-ttu-id="e17b4-326">**Açıklama**: her 10 dakika arayla son araba bulun.</span><span class="sxs-lookup"><span data-stu-id="e17b4-326">**Description**: Find the last car in every 10-minute interval.</span></span>

<span data-ttu-id="e17b4-327">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-327">**Input**:</span></span>

| <span data-ttu-id="e17b4-328">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="e17b4-328">LicensePlate</span></span> | <span data-ttu-id="e17b4-329">Yapma</span><span class="sxs-lookup"><span data-stu-id="e17b4-329">Make</span></span> | <span data-ttu-id="e17b4-330">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-330">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e17b4-331">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="e17b4-331">DXE 5291</span></span> |<span data-ttu-id="e17b4-332">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-332">Honda</span></span> |<span data-ttu-id="e17b4-333">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-333">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="e17b4-334">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="e17b4-334">YZK 5704</span></span> |<span data-ttu-id="e17b4-335">Ford</span><span class="sxs-lookup"><span data-stu-id="e17b4-335">Ford</span></span> |<span data-ttu-id="e17b4-336">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-336">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="e17b4-337">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="e17b4-337">RMV 8282</span></span> |<span data-ttu-id="e17b4-338">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-338">Honda</span></span> |<span data-ttu-id="e17b4-339">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-339">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="e17b4-340">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="e17b4-340">YHN 6970</span></span> |<span data-ttu-id="e17b4-341">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-341">Toyota</span></span> |<span data-ttu-id="e17b4-342">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-342">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="e17b4-343">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="e17b4-343">VFE 1616</span></span> |<span data-ttu-id="e17b4-344">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-344">Toyota</span></span> |<span data-ttu-id="e17b4-345">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-345">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="e17b4-346">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="e17b4-346">QYF 9358</span></span> |<span data-ttu-id="e17b4-347">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-347">Honda</span></span> |<span data-ttu-id="e17b4-348">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-348">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="e17b4-349">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="e17b4-349">MDR 6128</span></span> |<span data-ttu-id="e17b4-350">BMW</span><span class="sxs-lookup"><span data-stu-id="e17b4-350">BMW</span></span> |<span data-ttu-id="e17b4-351">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-351">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="e17b4-352">**Çıktı**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-352">**Output**:</span></span>

| <span data-ttu-id="e17b4-353">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="e17b4-353">LicensePlate</span></span> | <span data-ttu-id="e17b4-354">Yapma</span><span class="sxs-lookup"><span data-stu-id="e17b4-354">Make</span></span> | <span data-ttu-id="e17b4-355">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-355">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e17b4-356">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="e17b4-356">VFE 1616</span></span> |<span data-ttu-id="e17b4-357">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-357">Toyota</span></span> |<span data-ttu-id="e17b4-358">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-358">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="e17b4-359">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="e17b4-359">MDR 6128</span></span> |<span data-ttu-id="e17b4-360">BMW</span><span class="sxs-lookup"><span data-stu-id="e17b4-360">BMW</span></span> |<span data-ttu-id="e17b4-361">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-361">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="e17b4-362">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-362">**Solution**:</span></span>

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

<span data-ttu-id="e17b4-363">**Açıklama**: sorguda iki adımı vardır.</span><span class="sxs-lookup"><span data-stu-id="e17b4-363">**Explanation**: There are two steps in the query.</span></span> <span data-ttu-id="e17b4-364">İlk 10 dakikalık Windows'da son zaman damgası bulur.</span><span class="sxs-lookup"><span data-stu-id="e17b4-364">The first one finds the latest time stamp in 10-minute windows.</span></span> <span data-ttu-id="e17b4-365">İkinci adım her penceresinde son zaman damgalarının eşleşmesi olaylarını bulmak için özgün akış ile ilk sorgu sonuçları birleştirir.</span><span class="sxs-lookup"><span data-stu-id="e17b4-365">The second step joins the results of the first query with the original stream to find the events that match the last time stamps in each window.</span></span> 

## <a name="query-example-detect-the-absence-of-events"></a><span data-ttu-id="e17b4-366">Sorgu örnek:, olay eksikliklerini Algıla</span><span class="sxs-lookup"><span data-stu-id="e17b4-366">Query example: Detect the absence of events</span></span>
<span data-ttu-id="e17b4-367">**Açıklama**: bir akış belirli bir ölçütle eşleşen herhangi bir değer olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e17b4-367">**Description**: Check that a stream has no value that matches a certain criterion.</span></span>
<span data-ttu-id="e17b4-368">Örneğin, aynı marka gelen 2 ardışık araba Ücretli yol Son 90 saniye içinde girdiğiniz?</span><span class="sxs-lookup"><span data-stu-id="e17b4-368">For example, have 2 consecutive cars from the same make entered the toll road within the last 90 seconds?</span></span>

<span data-ttu-id="e17b4-369">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-369">**Input**:</span></span>

| <span data-ttu-id="e17b4-370">Yapma</span><span class="sxs-lookup"><span data-stu-id="e17b4-370">Make</span></span> | <span data-ttu-id="e17b4-371">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="e17b4-371">LicensePlate</span></span> | <span data-ttu-id="e17b4-372">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-372">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e17b4-373">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-373">Honda</span></span> |<span data-ttu-id="e17b4-374">ABC-123</span><span class="sxs-lookup"><span data-stu-id="e17b4-374">ABC-123</span></span> |<span data-ttu-id="e17b4-375">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-375">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="e17b4-376">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-376">Honda</span></span> |<span data-ttu-id="e17b4-377">AAA-999</span><span class="sxs-lookup"><span data-stu-id="e17b4-377">AAA-999</span></span> |<span data-ttu-id="e17b4-378">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-378">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="e17b4-379">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-379">Toyota</span></span> |<span data-ttu-id="e17b4-380">DEF 987</span><span class="sxs-lookup"><span data-stu-id="e17b4-380">DEF-987</span></span> |<span data-ttu-id="e17b4-381">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-381">2015-01-01T00:00:03.0000000Z</span></span> |
| <span data-ttu-id="e17b4-382">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-382">Honda</span></span> |<span data-ttu-id="e17b4-383">GHI 345</span><span class="sxs-lookup"><span data-stu-id="e17b4-383">GHI-345</span></span> |<span data-ttu-id="e17b4-384">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-384">2015-01-01T00:00:04.0000000Z</span></span> |

<span data-ttu-id="e17b4-385">**Çıktı**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-385">**Output**:</span></span>

| <span data-ttu-id="e17b4-386">Yapma</span><span class="sxs-lookup"><span data-stu-id="e17b4-386">Make</span></span> | <span data-ttu-id="e17b4-387">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-387">Time</span></span> | <span data-ttu-id="e17b4-388">CurrentCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="e17b4-388">CurrentCarLicensePlate</span></span> | <span data-ttu-id="e17b4-389">FirstCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="e17b4-389">FirstCarLicensePlate</span></span> | <span data-ttu-id="e17b4-390">FirstCarTime</span><span class="sxs-lookup"><span data-stu-id="e17b4-390">FirstCarTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="e17b4-391">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-391">Honda</span></span> |<span data-ttu-id="e17b4-392">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-392">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="e17b4-393">AAA-999</span><span class="sxs-lookup"><span data-stu-id="e17b4-393">AAA-999</span></span> |<span data-ttu-id="e17b4-394">ABC-123</span><span class="sxs-lookup"><span data-stu-id="e17b4-394">ABC-123</span></span> |<span data-ttu-id="e17b4-395">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-395">2015-01-01T00:00:01.0000000Z</span></span> |

<span data-ttu-id="e17b4-396">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-396">**Solution**:</span></span>

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

<span data-ttu-id="e17b4-397">**Açıklama**: kullanım **GECİKME** Giriş akışı bir olay geri gözatma ve almak için **olun** değeri.</span><span class="sxs-lookup"><span data-stu-id="e17b4-397">**Explanation**: Use **LAG** to peek into the input stream one event back and get the **Make** value.</span></span> <span data-ttu-id="e17b4-398">Kendisine karşılaştırmak **olun** değeri geçerli olayında ve aynı olmaları durumunda olay çıktı.</span><span class="sxs-lookup"><span data-stu-id="e17b4-398">Compare it to the **MAKE** value in the current event, and then output the event if they are the same.</span></span> <span data-ttu-id="e17b4-399">Aynı zamanda **GECİKME** önceki araba ilişkin veri almak için.</span><span class="sxs-lookup"><span data-stu-id="e17b4-399">You can also use **LAG** to get data about the previous car.</span></span>

## <a name="query-example-detect-the-duration-between-events"></a><span data-ttu-id="e17b4-400">Sorgu örnek: olaylar arasındaki süreyi Algıla</span><span class="sxs-lookup"><span data-stu-id="e17b4-400">Query example: Detect the duration between events</span></span>
<span data-ttu-id="e17b4-401">**Açıklama**: belirli bir olayın süresi bulun.</span><span class="sxs-lookup"><span data-stu-id="e17b4-401">**Description**: Find the duration of a given event.</span></span> <span data-ttu-id="e17b4-402">Örneğin, bir web clickstream göz önüne alındığında, bir özellik harcanan zamanı belirler.</span><span class="sxs-lookup"><span data-stu-id="e17b4-402">For example, given a web clickstream, determine the time spent on a feature.</span></span>

<span data-ttu-id="e17b4-403">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-403">**Input**:</span></span>  

| <span data-ttu-id="e17b4-404">Kullanıcı</span><span class="sxs-lookup"><span data-stu-id="e17b4-404">User</span></span> | <span data-ttu-id="e17b4-405">Özellik</span><span class="sxs-lookup"><span data-stu-id="e17b4-405">Feature</span></span> | <span data-ttu-id="e17b4-406">Olay</span><span class="sxs-lookup"><span data-stu-id="e17b4-406">Event</span></span> | <span data-ttu-id="e17b4-407">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-407">Time</span></span> |
| --- | --- | --- | --- |
| user@location.com |<span data-ttu-id="e17b4-408">RightMenu</span><span class="sxs-lookup"><span data-stu-id="e17b4-408">RightMenu</span></span> |<span data-ttu-id="e17b4-409">Başlatma</span><span class="sxs-lookup"><span data-stu-id="e17b4-409">Start</span></span> |<span data-ttu-id="e17b4-410">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-410">2015-01-01T00:00:01.0000000Z</span></span> |
| user@location.com |<span data-ttu-id="e17b4-411">RightMenu</span><span class="sxs-lookup"><span data-stu-id="e17b4-411">RightMenu</span></span> |<span data-ttu-id="e17b4-412">Bitiş</span><span class="sxs-lookup"><span data-stu-id="e17b4-412">End</span></span> |<span data-ttu-id="e17b4-413">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-413">2015-01-01T00:00:08.0000000Z</span></span> |

<span data-ttu-id="e17b4-414">**Çıktı**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-414">**Output**:</span></span>  

| <span data-ttu-id="e17b4-415">Kullanıcı</span><span class="sxs-lookup"><span data-stu-id="e17b4-415">User</span></span> | <span data-ttu-id="e17b4-416">Özellik</span><span class="sxs-lookup"><span data-stu-id="e17b4-416">Feature</span></span> | <span data-ttu-id="e17b4-417">Süre</span><span class="sxs-lookup"><span data-stu-id="e17b4-417">Duration</span></span> |
| --- | --- | --- |
| user@location.com |<span data-ttu-id="e17b4-418">RightMenu</span><span class="sxs-lookup"><span data-stu-id="e17b4-418">RightMenu</span></span> |<span data-ttu-id="e17b4-419">7</span><span class="sxs-lookup"><span data-stu-id="e17b4-419">7</span></span> |

<span data-ttu-id="e17b4-420">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-420">**Solution**:</span></span>

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

<span data-ttu-id="e17b4-421">**Açıklama**: kullanım **son** son almak için işlevi **zaman** değer olay türünü olduğu zaman **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="e17b4-421">**Explanation**: Use the **LAST** function to retrieve the last **TIME** value when the event type was **Start**.</span></span> <span data-ttu-id="e17b4-422">**Son** işlev kullandığı **[kullanıcı] bölümü tarafından** sonucu benzersiz kullanıcı başına hesaplanır belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="e17b4-422">The **LAST** function uses **PARTITION BY [user]** to indicate that the result is computed per unique user.</span></span> <span data-ttu-id="e17b4-423">1 saat maksimum eşik arasındaki zaman farkı için sorgu sahip **Başlat** ve **durdurmak** olayları, ancak gerektiği gibi yapılandırılabilir **(sınırı DURATION(hour, 1)**.</span><span class="sxs-lookup"><span data-stu-id="e17b4-423">The query has a 1-hour maximum threshold for the time difference between **Start** and **Stop** events, but is configurable as needed **(LIMIT DURATION(hour, 1)**.</span></span>

## <a name="query-example-detect-the-duration-of-a-condition"></a><span data-ttu-id="e17b4-424">Sorgu örnek: bir koşul süresini Algıla</span><span class="sxs-lookup"><span data-stu-id="e17b4-424">Query example: Detect the duration of a condition</span></span>
<span data-ttu-id="e17b4-425">**Açıklama**: Bul ne kadar giden bir koşul oluştu.</span><span class="sxs-lookup"><span data-stu-id="e17b4-425">**Description**: Find out how long a condition occurred.</span></span>
<span data-ttu-id="e17b4-426">Örneğin, bir hata (yukarıda 20.000 sterlin) yanlış bir ağırlık sahip tüm araba kaynaklandığını varsayalım.</span><span class="sxs-lookup"><span data-stu-id="e17b4-426">For example, suppose that a bug resulted in all cars having an incorrect weight (above 20,000 pounds).</span></span> <span data-ttu-id="e17b4-427">İşlem süresi hatanın istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e17b4-427">We want to compute the duration of the bug.</span></span>

<span data-ttu-id="e17b4-428">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-428">**Input**:</span></span>

| <span data-ttu-id="e17b4-429">Yapma</span><span class="sxs-lookup"><span data-stu-id="e17b4-429">Make</span></span> | <span data-ttu-id="e17b4-430">Zaman</span><span class="sxs-lookup"><span data-stu-id="e17b4-430">Time</span></span> | <span data-ttu-id="e17b4-431">Ağırlık</span><span class="sxs-lookup"><span data-stu-id="e17b4-431">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e17b4-432">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-432">Honda</span></span> |<span data-ttu-id="e17b4-433">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-433">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="e17b4-434">2000</span><span class="sxs-lookup"><span data-stu-id="e17b4-434">2000</span></span> |
| <span data-ttu-id="e17b4-435">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-435">Toyota</span></span> |<span data-ttu-id="e17b4-436">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-436">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="e17b4-437">25000</span><span class="sxs-lookup"><span data-stu-id="e17b4-437">25000</span></span> |
| <span data-ttu-id="e17b4-438">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-438">Honda</span></span> |<span data-ttu-id="e17b4-439">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-439">2015-01-01T00:00:03.0000000Z</span></span> |<span data-ttu-id="e17b4-440">26000</span><span class="sxs-lookup"><span data-stu-id="e17b4-440">26000</span></span> |
| <span data-ttu-id="e17b4-441">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-441">Toyota</span></span> |<span data-ttu-id="e17b4-442">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-442">2015-01-01T00:00:04.0000000Z</span></span> |<span data-ttu-id="e17b4-443">25000</span><span class="sxs-lookup"><span data-stu-id="e17b4-443">25000</span></span> |
| <span data-ttu-id="e17b4-444">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-444">Honda</span></span> |<span data-ttu-id="e17b4-445">2015-01-01T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-445">2015-01-01T00:00:05.0000000Z</span></span> |<span data-ttu-id="e17b4-446">26000</span><span class="sxs-lookup"><span data-stu-id="e17b4-446">26000</span></span> |
| <span data-ttu-id="e17b4-447">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-447">Toyota</span></span> |<span data-ttu-id="e17b4-448">2015-01-01T00:00:06.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-448">2015-01-01T00:00:06.0000000Z</span></span> |<span data-ttu-id="e17b4-449">25000</span><span class="sxs-lookup"><span data-stu-id="e17b4-449">25000</span></span> |
| <span data-ttu-id="e17b4-450">Honda</span><span class="sxs-lookup"><span data-stu-id="e17b4-450">Honda</span></span> |<span data-ttu-id="e17b4-451">2015-01-01T00:00:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-451">2015-01-01T00:00:07.0000000Z</span></span> |<span data-ttu-id="e17b4-452">26000</span><span class="sxs-lookup"><span data-stu-id="e17b4-452">26000</span></span> |
| <span data-ttu-id="e17b4-453">Toyota</span><span class="sxs-lookup"><span data-stu-id="e17b4-453">Toyota</span></span> |<span data-ttu-id="e17b4-454">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-454">2015-01-01T00:00:08.0000000Z</span></span> |<span data-ttu-id="e17b4-455">2000</span><span class="sxs-lookup"><span data-stu-id="e17b4-455">2000</span></span> |

<span data-ttu-id="e17b4-456">**Çıktı**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-456">**Output**:</span></span>

| <span data-ttu-id="e17b4-457">StartFault</span><span class="sxs-lookup"><span data-stu-id="e17b4-457">StartFault</span></span> | <span data-ttu-id="e17b4-458">EndFault</span><span class="sxs-lookup"><span data-stu-id="e17b4-458">EndFault</span></span> |
| --- | --- |
| <span data-ttu-id="e17b4-459">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-459">2015-01-01T00:00:02.000Z</span></span> |<span data-ttu-id="e17b4-460">2015-01-01T00:00:07.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-460">2015-01-01T00:00:07.000Z</span></span> |

<span data-ttu-id="e17b4-461">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-461">**Solution**:</span></span>

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

<span data-ttu-id="e17b4-462">**Açıklama**: kullanım **GECİKME** 24 saat için giriş akışı görüntülemek ve aramak için örnekler where **StartFault** ve **StopFault** ağırlığa göre yayılmış < 20000.</span><span class="sxs-lookup"><span data-stu-id="e17b4-462">**Explanation**: Use **LAG** to view the input stream for 24 hours and look for instances where **StartFault** and **StopFault** are spanned by the weight < 20000.</span></span>

## <a name="query-example-fill-missing-values"></a><span data-ttu-id="e17b4-463">Sorgu örnek: eksik değerleri doldurma</span><span class="sxs-lookup"><span data-stu-id="e17b4-463">Query example: Fill missing values</span></span>
<span data-ttu-id="e17b4-464">**Açıklama**: eksik değerleri olan olayları akış için düzenli aralıklarla olaylarla akışı üretir.</span><span class="sxs-lookup"><span data-stu-id="e17b4-464">**Description**: For the stream of events that have missing values, produce a stream of events with regular intervals.</span></span>
<span data-ttu-id="e17b4-465">Örneğin, en son görülen veri noktası raporları 5 saniyede bir olayı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e17b4-465">For example, generate an event every 5 seconds that reports the most recently seen data point.</span></span>

<span data-ttu-id="e17b4-466">**Giriş**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-466">**Input**:</span></span>

| <span data-ttu-id="e17b4-467">T</span><span class="sxs-lookup"><span data-stu-id="e17b4-467">t</span></span> | <span data-ttu-id="e17b4-468">değer</span><span class="sxs-lookup"><span data-stu-id="e17b4-468">value</span></span> |
| --- | --- |
| <span data-ttu-id="e17b4-469">"2014-01-01T06:01:00"</span><span class="sxs-lookup"><span data-stu-id="e17b4-469">"2014-01-01T06:01:00"</span></span> |<span data-ttu-id="e17b4-470">1</span><span class="sxs-lookup"><span data-stu-id="e17b4-470">1</span></span> |
| <span data-ttu-id="e17b4-471">"2014-01-01T06:01:05"</span><span class="sxs-lookup"><span data-stu-id="e17b4-471">"2014-01-01T06:01:05"</span></span> |<span data-ttu-id="e17b4-472">2</span><span class="sxs-lookup"><span data-stu-id="e17b4-472">2</span></span> |
| <span data-ttu-id="e17b4-473">"2014-01-01T06:01:10"</span><span class="sxs-lookup"><span data-stu-id="e17b4-473">"2014-01-01T06:01:10"</span></span> |<span data-ttu-id="e17b4-474">3</span><span class="sxs-lookup"><span data-stu-id="e17b4-474">3</span></span> |
| <span data-ttu-id="e17b4-475">"2014-01-01T06:01:15"</span><span class="sxs-lookup"><span data-stu-id="e17b4-475">"2014-01-01T06:01:15"</span></span> |<span data-ttu-id="e17b4-476">4</span><span class="sxs-lookup"><span data-stu-id="e17b4-476">4</span></span> |
| <span data-ttu-id="e17b4-477">"2014-01-01T06:01:30"</span><span class="sxs-lookup"><span data-stu-id="e17b4-477">"2014-01-01T06:01:30"</span></span> |<span data-ttu-id="e17b4-478">5</span><span class="sxs-lookup"><span data-stu-id="e17b4-478">5</span></span> |
| <span data-ttu-id="e17b4-479">"2014-01-01T06:01:35"</span><span class="sxs-lookup"><span data-stu-id="e17b4-479">"2014-01-01T06:01:35"</span></span> |<span data-ttu-id="e17b4-480">6</span><span class="sxs-lookup"><span data-stu-id="e17b4-480">6</span></span> |

<span data-ttu-id="e17b4-481">**Çıktı (ilk 10 satır)**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-481">**Output (first 10 rows)**:</span></span>

| <span data-ttu-id="e17b4-482">windowend</span><span class="sxs-lookup"><span data-stu-id="e17b4-482">windowend</span></span> | <span data-ttu-id="e17b4-483">lastevent.t</span><span class="sxs-lookup"><span data-stu-id="e17b4-483">lastevent.t</span></span> | <span data-ttu-id="e17b4-484">lastevent.Value</span><span class="sxs-lookup"><span data-stu-id="e17b4-484">lastevent.value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e17b4-485">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-485">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="e17b4-486">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-486">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="e17b4-487">1</span><span class="sxs-lookup"><span data-stu-id="e17b4-487">1</span></span> |
| <span data-ttu-id="e17b4-488">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-488">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="e17b4-489">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-489">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="e17b4-490">2</span><span class="sxs-lookup"><span data-stu-id="e17b4-490">2</span></span> |
| <span data-ttu-id="e17b4-491">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-491">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="e17b4-492">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-492">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="e17b4-493">3</span><span class="sxs-lookup"><span data-stu-id="e17b4-493">3</span></span> |
| <span data-ttu-id="e17b4-494">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-494">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="e17b4-495">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-495">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="e17b4-496">4</span><span class="sxs-lookup"><span data-stu-id="e17b4-496">4</span></span> |
| <span data-ttu-id="e17b4-497">2014-01-01T14:01:20.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-497">2014-01-01T14:01:20.000Z</span></span> |<span data-ttu-id="e17b4-498">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-498">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="e17b4-499">4</span><span class="sxs-lookup"><span data-stu-id="e17b4-499">4</span></span> |
| <span data-ttu-id="e17b4-500">2014-01-01T14:01:25.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-500">2014-01-01T14:01:25.000Z</span></span> |<span data-ttu-id="e17b4-501">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-501">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="e17b4-502">4</span><span class="sxs-lookup"><span data-stu-id="e17b4-502">4</span></span> |
| <span data-ttu-id="e17b4-503">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-503">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="e17b4-504">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-504">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="e17b4-505">5</span><span class="sxs-lookup"><span data-stu-id="e17b4-505">5</span></span> |
| <span data-ttu-id="e17b4-506">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-506">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="e17b4-507">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-507">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="e17b4-508">6</span><span class="sxs-lookup"><span data-stu-id="e17b4-508">6</span></span> |
| <span data-ttu-id="e17b4-509">2014-01-01T14:01:40.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-509">2014-01-01T14:01:40.000Z</span></span> |<span data-ttu-id="e17b4-510">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-510">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="e17b4-511">6</span><span class="sxs-lookup"><span data-stu-id="e17b4-511">6</span></span> |
| <span data-ttu-id="e17b4-512">2014-01-01T14:01:45.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-512">2014-01-01T14:01:45.000Z</span></span> |<span data-ttu-id="e17b4-513">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="e17b4-513">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="e17b4-514">6</span><span class="sxs-lookup"><span data-stu-id="e17b4-514">6</span></span> |

<span data-ttu-id="e17b4-515">**Çözüm**:</span><span class="sxs-lookup"><span data-stu-id="e17b4-515">**Solution**:</span></span>

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


<span data-ttu-id="e17b4-516">**Açıklama**: Bu sorguyu her 5 saniyede olaylar oluşturur ve daha önce alındı son olay çıkarır.</span><span class="sxs-lookup"><span data-stu-id="e17b4-516">**Explanation**: This query generates events every 5 seconds and outputs the last event that was received previously.</span></span> <span data-ttu-id="e17b4-517">[Hopping penceresi](https://msdn.microsoft.com/library/dn835041.aspx "Hopping penceresi--Azure akış analizi") süre belirler (Bu örnekte 300 saniye) en son olay bulmak için ne kadar geri sorgu arar.</span><span class="sxs-lookup"><span data-stu-id="e17b4-517">The [Hopping window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping window--Azure Stream Analytics") duration determines how far back the query looks to find the latest event (300 seconds in this example).</span></span>

## <a name="get-help"></a><span data-ttu-id="e17b4-518">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="e17b4-518">Get help</span></span>
<span data-ttu-id="e17b4-519">Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="e17b4-519">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e17b4-520">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e17b4-520">Next steps</span></span>
* [<span data-ttu-id="e17b4-521">Azure Stream Analytics'e giriş</span><span class="sxs-lookup"><span data-stu-id="e17b4-521">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="e17b4-522">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e17b4-522">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="e17b4-523">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="e17b4-523">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="e17b4-524">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="e17b4-524">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="e17b4-525">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="e17b4-525">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

