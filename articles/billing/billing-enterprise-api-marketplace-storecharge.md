---
title: "aaaAzure Kurumsal API'leri - faturalama Market ücretleri | Microsoft Docs"
description: "Kuruluş Azure müşterilerin toopull Tüketim verileri programlı olarak sağlayan raporlama API Hello hakkında bilgi edinin."
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: cdf2836b52df06a4bf5ed71a476fe33662c5363c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a><span data-ttu-id="0f43f-103">Kurumsal müşteriler - Market deposu Ücret için raporlama API'leri</span><span class="sxs-lookup"><span data-stu-id="0f43f-103">Reporting APIs for Enterprise customers - Marketplace Store Charge</span></span>

<span data-ttu-id="0f43f-104">Merhaba Market deposu ücret API döndürür hello kullanım tabanlı Market ücretleri dökümü hello için günlük belirtilen fatura dönemi veya başlangıç ve bitiş tarihleri (bir kez ücretler dahil değildir).</span><span class="sxs-lookup"><span data-stu-id="0f43f-104">hello Marketplace Store Charge API returns hello usage-based marketplace charges breakdown by day for hello specified Billing Period or start and end dates (one time fees are not included).</span></span>

##<a name="request"></a><span data-ttu-id="0f43f-105">İstek</span><span class="sxs-lookup"><span data-stu-id="0f43f-105">Request</span></span> 
<span data-ttu-id="0f43f-106">Eklenen toobe gereken ortak üstbilgi özelliklerini belirtilen [burada](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="0f43f-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="0f43f-107">Fatura döneminde belirtilmezse, veriler hello geçerli faturalama dönemi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="0f43f-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span> <span data-ttu-id="0f43f-108">Özel zaman aralıkları ile Merhaba başlangıç belirtilebilir ve hello biçimi yyyy-aa-gg, desteklenen maksimum hello zamanında 36 ay aralığı olduğu tarih parametrelerine bitmelidir.</span><span class="sxs-lookup"><span data-stu-id="0f43f-108">Custom time ranges can be specified with hello start and end date parameters that are in hello format yyyy-MM-dd, hello maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="0f43f-109">Yöntem</span><span class="sxs-lookup"><span data-stu-id="0f43f-109">Method</span></span> | <span data-ttu-id="0f43f-110">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="0f43f-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="0f43f-111">AL</span><span class="sxs-lookup"><span data-stu-id="0f43f-111">GET</span></span>|<span data-ttu-id="0f43f-112">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="0f43f-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span></span>|
|<span data-ttu-id="0f43f-113">AL</span><span class="sxs-lookup"><span data-stu-id="0f43f-113">GET</span></span>|<span data-ttu-id="0f43f-114">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="0f43f-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span></span>|
|<span data-ttu-id="0f43f-115">AL</span><span class="sxs-lookup"><span data-stu-id="0f43f-115">GET</span></span>|<span data-ttu-id="0f43f-116">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / marketplacechargesbycustomdate? startTime 2017-01-01 = & endTime 2017-01-10 =</span><span class="sxs-lookup"><span data-stu-id="0f43f-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="0f43f-117">API, toouse hello önizleme sürümünü v2 URL yukarıdaki hello v1 ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0f43f-117">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="0f43f-118">Yanıt</span><span class="sxs-lookup"><span data-stu-id="0f43f-118">Response</span></span>
 
    
        [
            {
                "id": "id",
                "subscriptionGuid": "00000000-0000-0000-0000-000000000000",
                "subscriptionName": "subName",
                "meterId": "2core",
                "usageStartDate": "2015-09-17T00:00:00Z",
                "usageEndDate": "2015-09-17T23:59:59Z",
                "offerName": "Virtual LoadMaster™ (VLM) for Azure",
                "resourceGroup": "Res group",
                "instanceId": "id",
                "additionalInfo": "{\"ImageType\":null,\"ServiceType\":\"Medium\"}",
                "tags": "",
                "orderNumber": "order",
                "unitOfMeasure": "",
                "costCenter": "100",
                "accountId": 100,
                "accountName": "Account Name",
                "accountOwnerId": "account@live.com",
                "departmentId": 101,
                "departmentName": "Department 1",
                "publisherName": "Publisher 1",
                "planName": "Plan name",
                "consumedQuantity": 1.15,
                "resourceRate": 0.1,
                "extendedCost": 1.11
            },
            ...
        ]
    

<span data-ttu-id="0f43f-119">**Yanıt özellik tanımları**</span><span class="sxs-lookup"><span data-stu-id="0f43f-119">**Response property definitions**</span></span>

|<span data-ttu-id="0f43f-120">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="0f43f-120">Property Name</span></span>| <span data-ttu-id="0f43f-121">Tür</span><span class="sxs-lookup"><span data-stu-id="0f43f-121">Type</span></span>| <span data-ttu-id="0f43f-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0f43f-122">Description</span></span>
|-|-|-|
|<span data-ttu-id="0f43f-123">id</span><span class="sxs-lookup"><span data-stu-id="0f43f-123">id</span></span>|<span data-ttu-id="0f43f-124">Dize</span><span class="sxs-lookup"><span data-stu-id="0f43f-124">string</span></span>|<span data-ttu-id="0f43f-125">Merhaba Market ücret öğesi için benzersiz kimliği</span><span class="sxs-lookup"><span data-stu-id="0f43f-125">Unique Id for hello marketplace charge item</span></span>|
|<span data-ttu-id="0f43f-126">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="0f43f-126">subscriptionGuid</span></span>|<span data-ttu-id="0f43f-127">GUID</span><span class="sxs-lookup"><span data-stu-id="0f43f-127">Guid</span></span>|<span data-ttu-id="0f43f-128">Merhaba abonelik GUID</span><span class="sxs-lookup"><span data-stu-id="0f43f-128">hello Subscription Guid</span></span>|
|<span data-ttu-id="0f43f-129">varlığıyla subscriptionName</span><span class="sxs-lookup"><span data-stu-id="0f43f-129">subscriptionName</span></span>|<span data-ttu-id="0f43f-130">Dize</span><span class="sxs-lookup"><span data-stu-id="0f43f-130">string</span></span>|<span data-ttu-id="0f43f-131">Merhaba abonelik adı</span><span class="sxs-lookup"><span data-stu-id="0f43f-131">hello Subscription Name</span></span>|
|<span data-ttu-id="0f43f-132">meterId</span><span class="sxs-lookup"><span data-stu-id="0f43f-132">meterId</span></span>|<span data-ttu-id="0f43f-133">Dize</span><span class="sxs-lookup"><span data-stu-id="0f43f-133">string</span></span>|<span data-ttu-id="0f43f-134">Ölçer hello kimliği yayılan</span><span class="sxs-lookup"><span data-stu-id="0f43f-134">Id for hello emitted Meter</span></span>|
|<span data-ttu-id="0f43f-135">usageStartDate</span><span class="sxs-lookup"><span data-stu-id="0f43f-135">usageStartDate</span></span>|<span data-ttu-id="0f43f-136">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="0f43f-136">DateTime</span></span>|<span data-ttu-id="0f43f-137">Merhaba kullanım kaydı için başlangıç zamanı</span><span class="sxs-lookup"><span data-stu-id="0f43f-137">Start time for hello usage record</span></span>|
|<span data-ttu-id="0f43f-138">usageEndDate</span><span class="sxs-lookup"><span data-stu-id="0f43f-138">usageEndDate</span></span>|<span data-ttu-id="0f43f-139">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="0f43f-139">DateTime</span></span>|<span data-ttu-id="0f43f-140">Merhaba kullanım kaydı için bitiş zamanı</span><span class="sxs-lookup"><span data-stu-id="0f43f-140">End time for hello usage record</span></span>|
|<span data-ttu-id="0f43f-141">offerName</span><span class="sxs-lookup"><span data-stu-id="0f43f-141">offerName</span></span>|<span data-ttu-id="0f43f-142">Dize</span><span class="sxs-lookup"><span data-stu-id="0f43f-142">string</span></span>|<span data-ttu-id="0f43f-143">Merhaba teklif adı</span><span class="sxs-lookup"><span data-stu-id="0f43f-143">hello Offer name</span></span>|
|<span data-ttu-id="0f43f-144">kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="0f43f-144">resourceGroup</span></span>|<span data-ttu-id="0f43f-145">Dize</span><span class="sxs-lookup"><span data-stu-id="0f43f-145">string</span></span>|<span data-ttu-id="0f43f-146">Merhaba kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="0f43f-146">hello resource Group</span></span>|
|<span data-ttu-id="0f43f-147">örnek kimliği</span><span class="sxs-lookup"><span data-stu-id="0f43f-147">instanceId</span></span>|<span data-ttu-id="0f43f-148">Dize</span><span class="sxs-lookup"><span data-stu-id="0f43f-148">string</span></span>|<span data-ttu-id="0f43f-149">Örnek kimliği</span><span class="sxs-lookup"><span data-stu-id="0f43f-149">Instance Id</span></span>|
|<span data-ttu-id="0f43f-150">additionalınfo alanına</span><span class="sxs-lookup"><span data-stu-id="0f43f-150">additionalInfo</span></span>|<span data-ttu-id="0f43f-151">Dize</span><span class="sxs-lookup"><span data-stu-id="0f43f-151">string</span></span>|<span data-ttu-id="0f43f-152">Ek bilgi JSON dizesi</span><span class="sxs-lookup"><span data-stu-id="0f43f-152">Additional info JSON string</span></span>|
|<span data-ttu-id="0f43f-153">etiketler</span><span class="sxs-lookup"><span data-stu-id="0f43f-153">tags</span></span>|<span data-ttu-id="0f43f-154">Dize</span><span class="sxs-lookup"><span data-stu-id="0f43f-154">string</span></span>|<span data-ttu-id="0f43f-155">Etiket JSON dizesi</span><span class="sxs-lookup"><span data-stu-id="0f43f-155">Tag JSON string</span></span>|
|<span data-ttu-id="0f43f-156">orderNumber</span><span class="sxs-lookup"><span data-stu-id="0f43f-156">orderNumber</span></span>|<span data-ttu-id="0f43f-157">Dize</span><span class="sxs-lookup"><span data-stu-id="0f43f-157">string</span></span>|<span data-ttu-id="0f43f-158">Merhaba sipariş numarası</span><span class="sxs-lookup"><span data-stu-id="0f43f-158">hello order number</span></span>|
|<span data-ttu-id="0f43f-159">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="0f43f-159">unitOfMeasure</span></span>|<span data-ttu-id="0f43f-160">Dize</span><span class="sxs-lookup"><span data-stu-id="0f43f-160">string</span></span>|<span data-ttu-id="0f43f-161">Ölçü hello ölçer</span><span class="sxs-lookup"><span data-stu-id="0f43f-161">Unit of measure for hello meter</span></span>|
|<span data-ttu-id="0f43f-162">costCenter</span><span class="sxs-lookup"><span data-stu-id="0f43f-162">costCenter</span></span>|<span data-ttu-id="0f43f-163">Dize</span><span class="sxs-lookup"><span data-stu-id="0f43f-163">string</span></span>|<span data-ttu-id="0f43f-164">Merhaba maliyet merkezi</span><span class="sxs-lookup"><span data-stu-id="0f43f-164">hello cost center</span></span>|
|<span data-ttu-id="0f43f-165">Hesap Kimliği</span><span class="sxs-lookup"><span data-stu-id="0f43f-165">accountId</span></span>|<span data-ttu-id="0f43f-166">Int</span><span class="sxs-lookup"><span data-stu-id="0f43f-166">int</span></span>|<span data-ttu-id="0f43f-167">Merhaba hesap kimliği</span><span class="sxs-lookup"><span data-stu-id="0f43f-167">hello account Id</span></span>|
|<span data-ttu-id="0f43f-168">accountName</span><span class="sxs-lookup"><span data-stu-id="0f43f-168">accountName</span></span>|<span data-ttu-id="0f43f-169">Dize</span><span class="sxs-lookup"><span data-stu-id="0f43f-169">string</span></span> |<span data-ttu-id="0f43f-170">Merhaba hesap adı</span><span class="sxs-lookup"><span data-stu-id="0f43f-170">hello Account Name</span></span>|
|<span data-ttu-id="0f43f-171">accountOwnerId</span><span class="sxs-lookup"><span data-stu-id="0f43f-171">accountOwnerId</span></span>|<span data-ttu-id="0f43f-172">Dize</span><span class="sxs-lookup"><span data-stu-id="0f43f-172">string</span></span>|<span data-ttu-id="0f43f-173">Merhaba hesap sahibinin kimliği</span><span class="sxs-lookup"><span data-stu-id="0f43f-173">hello Account Owner Id</span></span>|
|<span data-ttu-id="0f43f-174">departmentId</span><span class="sxs-lookup"><span data-stu-id="0f43f-174">departmentId</span></span>|<span data-ttu-id="0f43f-175">Int</span><span class="sxs-lookup"><span data-stu-id="0f43f-175">int</span></span>|<span data-ttu-id="0f43f-176">Merhaba bölüm kimliği</span><span class="sxs-lookup"><span data-stu-id="0f43f-176">hello department Id</span></span>|
|<span data-ttu-id="0f43f-177">departmentName</span><span class="sxs-lookup"><span data-stu-id="0f43f-177">departmentName</span></span>|<span data-ttu-id="0f43f-178">Dize</span><span class="sxs-lookup"><span data-stu-id="0f43f-178">string</span></span>|<span data-ttu-id="0f43f-179">Merhaba bölüm adı</span><span class="sxs-lookup"><span data-stu-id="0f43f-179">hello department name</span></span>|
|<span data-ttu-id="0f43f-180">publisherName</span><span class="sxs-lookup"><span data-stu-id="0f43f-180">publisherName</span></span>|<span data-ttu-id="0f43f-181">Dize</span><span class="sxs-lookup"><span data-stu-id="0f43f-181">string</span></span>|<span data-ttu-id="0f43f-182">Merhaba Yayımcı adı</span><span class="sxs-lookup"><span data-stu-id="0f43f-182">hello publisher name</span></span>|
|<span data-ttu-id="0f43f-183">planName</span><span class="sxs-lookup"><span data-stu-id="0f43f-183">planName</span></span>|<span data-ttu-id="0f43f-184">Dize</span><span class="sxs-lookup"><span data-stu-id="0f43f-184">string</span></span>|<span data-ttu-id="0f43f-185">Merhaba planı adı</span><span class="sxs-lookup"><span data-stu-id="0f43f-185">hello Plan name</span></span>|
|<span data-ttu-id="0f43f-186">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="0f43f-186">consumedQuantity</span></span>|<span data-ttu-id="0f43f-187">Ondalık</span><span class="sxs-lookup"><span data-stu-id="0f43f-187">decimal</span></span>|<span data-ttu-id="0f43f-188">Bu süre boyunca Tüketilen Miktar</span><span class="sxs-lookup"><span data-stu-id="0f43f-188">Consumed Quantity during this time period</span></span>|
|<span data-ttu-id="0f43f-189">resourceRate</span><span class="sxs-lookup"><span data-stu-id="0f43f-189">resourceRate</span></span>|<span data-ttu-id="0f43f-190">Ondalık</span><span class="sxs-lookup"><span data-stu-id="0f43f-190">decimal</span></span>|<span data-ttu-id="0f43f-191">Birim Fiyat hello ölçmek için</span><span class="sxs-lookup"><span data-stu-id="0f43f-191">Unit price for hello meter</span></span>|
|<span data-ttu-id="0f43f-192">extendedCost</span><span class="sxs-lookup"><span data-stu-id="0f43f-192">extendedCost</span></span>|<span data-ttu-id="0f43f-193">Ondalık</span><span class="sxs-lookup"><span data-stu-id="0f43f-193">decimal</span></span>|<span data-ttu-id="0f43f-194">Tüketilen Miktar ve genişletilmiş maliyet göre ücret tahmini</span><span class="sxs-lookup"><span data-stu-id="0f43f-194">Estimated charge based on Consumed Quantity and Extended cost</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="0f43f-195">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="0f43f-195">See also</span></span>

* [<span data-ttu-id="0f43f-196">Faturalama nokta API</span><span class="sxs-lookup"><span data-stu-id="0f43f-196">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="0f43f-197">Kullanım ayrıntılarını API</span><span class="sxs-lookup"><span data-stu-id="0f43f-197">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="0f43f-198">Bakiye ve özeti API</span><span class="sxs-lookup"><span data-stu-id="0f43f-198">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="0f43f-199">Fiyat listesi API'si</span><span class="sxs-lookup"><span data-stu-id="0f43f-199">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)