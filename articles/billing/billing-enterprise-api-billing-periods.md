---
title: aaaAzure faturalama Kurumsal nokta faturalama API'leri - | Microsoft Docs
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
ms.openlocfilehash: d4e17f25b22729a7f213306fb019ee0dbeca87ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a><span data-ttu-id="f597a-103">Kurumsal müşteriler - faturalama nokta için raporlama API'leri</span><span class="sxs-lookup"><span data-stu-id="f597a-103">Reporting APIs for Enterprise customers - Billing Periods</span></span>

<span data-ttu-id="f597a-104">Merhaba nokta API faturalama verileriniz tüketim hello nokta faturalama listesi kayıt ters kronolojik sırada belirtilen döndürür.</span><span class="sxs-lookup"><span data-stu-id="f597a-104">hello Billing Periods API returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="f597a-105">Her dönem toohello API rota verilerini - BalanceSummary, UsageDetails, Marktplace ücretleri ve fiyat listesi hello dört kümeleri için işaret eden bir özellik içerir.</span><span class="sxs-lookup"><span data-stu-id="f597a-105">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marktplace Charges, and PriceSheet.</span></span> <span data-ttu-id="f597a-106">Merhaba dönem veri yoksa hello karşılık gelen özelliği null olur.</span><span class="sxs-lookup"><span data-stu-id="f597a-106">If hello period does not have data, hello corresponding property is null.</span></span> 


##<a name="request"></a><span data-ttu-id="f597a-107">İstek</span><span class="sxs-lookup"><span data-stu-id="f597a-107">Request</span></span> 
<span data-ttu-id="f597a-108">Eklenen toobe gereken ortak üstbilgi özelliklerini belirtilen [burada](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="f597a-108">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> 

|<span data-ttu-id="f597a-109">Yöntem</span><span class="sxs-lookup"><span data-stu-id="f597a-109">Method</span></span> | <span data-ttu-id="f597a-110">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="f597a-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="f597a-111">AL</span><span class="sxs-lookup"><span data-stu-id="f597a-111">GET</span></span>| <span data-ttu-id="f597a-112">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / billingperiods</span><span class="sxs-lookup"><span data-stu-id="f597a-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span></span>|

> [!Note]
> <span data-ttu-id="f597a-113">API, toouse hello önizleme sürümünü v2 URL yukarıdaki hello v1 ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f597a-113">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="f597a-114">Yanıt</span><span class="sxs-lookup"><span data-stu-id="f597a-114">Response</span></span>
 
    
    
      [
            {
                "billingPeriodId": "201704",
                "billingStart": "2017-04-01T00:00:00Z",
                "billingEnd": "2017-04-30T11:59:59Z",
                "balanceSummary": "/v1/enrollments/100/billingperiods/201704/balancesummary",
                "usageDetails": "/v1/enrollments/100/billingperiods/201704/usagedetails",
                "marketplaceCharges": "/v1/enrollments/100/billingperiods/201704/marketplacecharges",
                "priceSheet": "/v1/enrollments/100/billingperiods/201704/pricesheet"
            },          
            ....
      ]
    

<span data-ttu-id="f597a-115">**Yanıt özellik tanımları**</span><span class="sxs-lookup"><span data-stu-id="f597a-115">**Response property definitions**</span></span>

|<span data-ttu-id="f597a-116">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="f597a-116">Property Name</span></span>| <span data-ttu-id="f597a-117">Tür</span><span class="sxs-lookup"><span data-stu-id="f597a-117">Type</span></span>| <span data-ttu-id="f597a-118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f597a-118">Description</span></span>
|-|-|-|
|<span data-ttu-id="f597a-119">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="f597a-119">billingPeriodId</span></span>| <span data-ttu-id="f597a-120">Dize</span><span class="sxs-lookup"><span data-stu-id="f597a-120">string</span></span>| <span data-ttu-id="f597a-121">Merhaba belirli bir fatura dönemi temsil eden benzersiz kimliği</span><span class="sxs-lookup"><span data-stu-id="f597a-121">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="f597a-122">billingStart</span><span class="sxs-lookup"><span data-stu-id="f597a-122">billingStart</span></span>| <span data-ttu-id="f597a-123">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="f597a-123">datetime</span></span>| <span data-ttu-id="f597a-124">Merhaba dönem başlangıç tarihi temsil eden ISO 8601 dize</span><span class="sxs-lookup"><span data-stu-id="f597a-124">ISO 8601 string representing hello period start date</span></span>|
|<span data-ttu-id="f597a-125">billingEnd</span><span class="sxs-lookup"><span data-stu-id="f597a-125">billingEnd</span></span>| <span data-ttu-id="f597a-126">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="f597a-126">datetime</span></span>| <span data-ttu-id="f597a-127">Merhaba dönem bitiş tarihi temsil eden ISO 8601 dize</span><span class="sxs-lookup"><span data-stu-id="f597a-127">ISO 8601 string representing hello period end date</span></span>|
|<span data-ttu-id="f597a-128">balanceSummary</span><span class="sxs-lookup"><span data-stu-id="f597a-128">balanceSummary</span></span>| <span data-ttu-id="f597a-129">Dize</span><span class="sxs-lookup"><span data-stu-id="f597a-129">string</span></span>| <span data-ttu-id="f597a-130">Bu dönem için toohello bakiye özeti verilerini yönlendirir hello URL yolu</span><span class="sxs-lookup"><span data-stu-id="f597a-130">hello URL path that routes toohello Balance Summary data for this period</span></span>|
|<span data-ttu-id="f597a-131">usageDetails</span><span class="sxs-lookup"><span data-stu-id="f597a-131">usageDetails</span></span>| <span data-ttu-id="f597a-132">Dize</span><span class="sxs-lookup"><span data-stu-id="f597a-132">string</span></span>| <span data-ttu-id="f597a-133">Bu dönem için toohello kullanım ayrıntılarını veri yolları hello URL yolu</span><span class="sxs-lookup"><span data-stu-id="f597a-133">hello URL path that routes toohello Usage Details data for this period</span></span>|
|<span data-ttu-id="f597a-134">marketplaceCharges</span><span class="sxs-lookup"><span data-stu-id="f597a-134">marketplaceCharges</span></span>| <span data-ttu-id="f597a-135">Dize</span><span class="sxs-lookup"><span data-stu-id="f597a-135">string</span></span>| <span data-ttu-id="f597a-136">Bu dönem için toohello Market ücretleri veri yolları hello URL yolu</span><span class="sxs-lookup"><span data-stu-id="f597a-136">hello URL path that routes toohello Marketplace Charges data for this period</span></span>|
|<span data-ttu-id="f597a-137">Fiyat listesi</span><span class="sxs-lookup"><span data-stu-id="f597a-137">priceSheet</span></span>| <span data-ttu-id="f597a-138">Dize</span><span class="sxs-lookup"><span data-stu-id="f597a-138">string</span></span>| <span data-ttu-id="f597a-139">Bu dönem için toohello fiyat listesi veri yolları hello URL yolu</span><span class="sxs-lookup"><span data-stu-id="f597a-139">hello URL path that routes toohello PriceSheet data for this period</span></span>|

<br/>
## <a name="see-also"></a><span data-ttu-id="f597a-140">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="f597a-140">See also</span></span>

* [<span data-ttu-id="f597a-141">Bakiye ve özeti API</span><span class="sxs-lookup"><span data-stu-id="f597a-141">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="f597a-142">Kullanım ayrıntılarını API</span><span class="sxs-lookup"><span data-stu-id="f597a-142">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="f597a-143">Market deposu ücret API</span><span class="sxs-lookup"><span data-stu-id="f597a-143">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="f597a-144">Fiyat listesi API'si</span><span class="sxs-lookup"><span data-stu-id="f597a-144">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)