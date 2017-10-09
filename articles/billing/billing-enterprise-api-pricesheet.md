---
title: aaaAzure Kurumsal API'leri - faturalama fiyat listesi | Microsoft Docs
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
ms.openlocfilehash: 4cfe694c63fba266d117054b046d9caacb3b7197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a><span data-ttu-id="b4342-103">Kurumsal müşteriler - fiyat listesi için raporlama API'leri</span><span class="sxs-lookup"><span data-stu-id="b4342-103">Reporting APIs for Enterprise customers - Price Sheet</span></span>

<span data-ttu-id="b4342-104">Merhaba fiyat listesi API verilen kayıt ve faturalama dönemi hello her ölçer hello geçerli hızı sunar.</span><span class="sxs-lookup"><span data-stu-id="b4342-104">hello Price Sheet API provides hello applicable rate for each Meter for hello given Enrollment and Billing Period.</span></span>

##<a name="request"></a><span data-ttu-id="b4342-105">İstek</span><span class="sxs-lookup"><span data-stu-id="b4342-105">Request</span></span>
<span data-ttu-id="b4342-106">Eklenen toobe gereken ortak üstbilgi özelliklerini belirtilen [burada](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="b4342-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="b4342-107">Fatura döneminde belirtilmezse, veriler hello geçerli faturalama dönemi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="b4342-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span>

|<span data-ttu-id="b4342-108">Yöntem</span><span class="sxs-lookup"><span data-stu-id="b4342-108">Method</span></span> | <span data-ttu-id="b4342-109">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="b4342-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="b4342-110">AL</span><span class="sxs-lookup"><span data-stu-id="b4342-110">GET</span></span>|<span data-ttu-id="b4342-111">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / fiyat listesi</span><span class="sxs-lookup"><span data-stu-id="b4342-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span></span>|
|<span data-ttu-id="b4342-112">AL</span><span class="sxs-lookup"><span data-stu-id="b4342-112">GET</span></span>|<span data-ttu-id="b4342-113">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / fiyat listesi</span><span class="sxs-lookup"><span data-stu-id="b4342-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span></span>|

> [!Note]
> <span data-ttu-id="b4342-114">API, toouse hello önizleme sürümünü v2 URL yukarıdaki hello v1 ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b4342-114">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="b4342-115">Yanıt</span><span class="sxs-lookup"><span data-stu-id="b4342-115">Response</span></span>

    
        [
            {
                "id": "enrollments/57354989/billingperiods/201601/products/343/pricesheets",
                "billingPeriodId": "201704",
                "meterId": "dc210ecb-97e8-4522-8134-2385494233c0",
                "meterName": "A1 VM",
                "unitOfMeasure": "100 Hours",
                "includedQuantity": 0,
                "partNumber": "N7H-00015",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            {
                "id": "enrollments/57354989/billingperiods/201601/products/2884/pricesheets",
                "billingPeriodId": "201404",
                "meterId": "dc210ecb-97e8-4522-8134-5385494233c0",
                "meterName": "Locally Redundant Storage Premium Storage - Snapshots - AU East",
                "unitOfMeasure": "100 GB",
                "includedQuantity": 0,
                "partNumber": "N9H-00402",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            ...
        ]
    

> [!Note]
><span data-ttu-id="b4342-116">Merhaba Önizleme API kullanıyorsanız, meterId alan kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="b4342-116">If you are using hello Preview API, meterId field is not available.</span></span>
>

<span data-ttu-id="b4342-117">**Yanıt özellik tanımları**</span><span class="sxs-lookup"><span data-stu-id="b4342-117">**Response property definitions**</span></span>

|<span data-ttu-id="b4342-118">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="b4342-118">Property Name</span></span>| <span data-ttu-id="b4342-119">Tür</span><span class="sxs-lookup"><span data-stu-id="b4342-119">Type</span></span>| <span data-ttu-id="b4342-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b4342-120">Description</span></span>
|-|-|-|
|<span data-ttu-id="b4342-121">id</span><span class="sxs-lookup"><span data-stu-id="b4342-121">id</span></span>| <span data-ttu-id="b4342-122">Dize</span><span class="sxs-lookup"><span data-stu-id="b4342-122">string</span></span>| <span data-ttu-id="b4342-123">Merhaba belirli bir fiyat listesi öğesini (faturalama dönemi tarafından ölçer) temsil eden benzersiz kimliği</span><span class="sxs-lookup"><span data-stu-id="b4342-123">hello unique Id that represents a particular PriceSheet item (meter by billing period)</span></span>|
|<span data-ttu-id="b4342-124">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="b4342-124">billingPeriodId</span></span>| <span data-ttu-id="b4342-125">Dize</span><span class="sxs-lookup"><span data-stu-id="b4342-125">string</span></span>| <span data-ttu-id="b4342-126">Merhaba belirli bir fatura dönemi temsil eden benzersiz kimliği</span><span class="sxs-lookup"><span data-stu-id="b4342-126">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="b4342-127">meterId</span><span class="sxs-lookup"><span data-stu-id="b4342-127">meterId</span></span>| <span data-ttu-id="b4342-128">Dize</span><span class="sxs-lookup"><span data-stu-id="b4342-128">string</span></span>| <span data-ttu-id="b4342-129">Merhaba ölçer Hello tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="b4342-129">hello identifier for hello meter.</span></span> <span data-ttu-id="b4342-130">Eşlenen toohello kullanım meterId olabilir.</span><span class="sxs-lookup"><span data-stu-id="b4342-130">It can be mapped toohello usage meterId.</span></span>|
|<span data-ttu-id="b4342-131">meterName</span><span class="sxs-lookup"><span data-stu-id="b4342-131">meterName</span></span>| <span data-ttu-id="b4342-132">Dize</span><span class="sxs-lookup"><span data-stu-id="b4342-132">string</span></span>| <span data-ttu-id="b4342-133">Merhaba ölçüm adı</span><span class="sxs-lookup"><span data-stu-id="b4342-133">hello meter name</span></span>|
|<span data-ttu-id="b4342-134">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="b4342-134">unitOfMeasure</span></span>| <span data-ttu-id="b4342-135">Dize</span><span class="sxs-lookup"><span data-stu-id="b4342-135">string</span></span>| <span data-ttu-id="b4342-136">Merhaba hizmet ölçmek için ölçü hello</span><span class="sxs-lookup"><span data-stu-id="b4342-136">hello Unit of Measure for measuring hello service</span></span>|
|<span data-ttu-id="b4342-137">includedQuantity</span><span class="sxs-lookup"><span data-stu-id="b4342-137">includedQuantity</span></span>| <span data-ttu-id="b4342-138">Ondalık</span><span class="sxs-lookup"><span data-stu-id="b4342-138">decimal</span></span>| <span data-ttu-id="b4342-139">Dahil edilen miktar</span><span class="sxs-lookup"><span data-stu-id="b4342-139">Quantity that is included</span></span> |
|<span data-ttu-id="b4342-140">partNumber</span><span class="sxs-lookup"><span data-stu-id="b4342-140">partNumber</span></span>| <span data-ttu-id="b4342-141">Dize</span><span class="sxs-lookup"><span data-stu-id="b4342-141">string</span></span>| <span data-ttu-id="b4342-142">Ölçer Hello ile ilişkili hello parça numarası</span><span class="sxs-lookup"><span data-stu-id="b4342-142">hello part number associated with hello Meter</span></span>|
|<span data-ttu-id="b4342-143">unitPrice</span><span class="sxs-lookup"><span data-stu-id="b4342-143">unitPrice</span></span>| <span data-ttu-id="b4342-144">Ondalık</span><span class="sxs-lookup"><span data-stu-id="b4342-144">decimal</span></span>| <span data-ttu-id="b4342-145">Merhaba birim fiyat hello ölçmek için</span><span class="sxs-lookup"><span data-stu-id="b4342-145">hello unit price for hello meter</span></span>|
|<span data-ttu-id="b4342-146">currencyCode</span><span class="sxs-lookup"><span data-stu-id="b4342-146">currencyCode</span></span>| <span data-ttu-id="b4342-147">Dize</span><span class="sxs-lookup"><span data-stu-id="b4342-147">string</span></span>| <span data-ttu-id="b4342-148">Merhaba unitPrice Hello para birimi kodu</span><span class="sxs-lookup"><span data-stu-id="b4342-148">hello currency code for hello unitPrice</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="b4342-149">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="b4342-149">See also</span></span>

* [<span data-ttu-id="b4342-150">Faturalama nokta API</span><span class="sxs-lookup"><span data-stu-id="b4342-150">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="b4342-151">Kullanım ayrıntılarını API</span><span class="sxs-lookup"><span data-stu-id="b4342-151">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md)

* [<span data-ttu-id="b4342-152">Bakiye ve özeti API</span><span class="sxs-lookup"><span data-stu-id="b4342-152">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="b4342-153">Market deposu ücret API</span><span class="sxs-lookup"><span data-stu-id="b4342-153">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md)
