---
title: "aaaAzure Kurumsal API'leri - faturalama bakiye ve özeti | Microsoft Docs"
description: "Azure kaynak tüketimini ve eğilimleri kullanılan tooprovide Öngörüler olan Azure faturalama kullanımını ve RateCard API'ları hakkında bilgi edinin."
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
ms.openlocfilehash: b031de2c347e5abeacd11743cc96024434518918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a><span data-ttu-id="8f9d8-103">Kurumsal müşteriler - bakiye ve özeti için raporlama API'leri</span><span class="sxs-lookup"><span data-stu-id="8f9d8-103">Reporting APIs for Enterprise customers - Balance and Summary</span></span>

<span data-ttu-id="8f9d8-104">Merhaba bakiye ve Özet API aylık bakiyelerini, yeni satın alma işlemleri, Azure Marketi servis ücretleri, ayarlamalar ve fazla kullanım ücretleri bilgilerin özetini sunar.</span><span class="sxs-lookup"><span data-stu-id="8f9d8-104">hello Balance and Summary API offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments, and overage charges.</span></span>


##<a name="request"></a><span data-ttu-id="8f9d8-105">İstek</span><span class="sxs-lookup"><span data-stu-id="8f9d8-105">Request</span></span> 
<span data-ttu-id="8f9d8-106">Eklenen toobe gereken ortak üstbilgi özelliklerini belirtilen [burada](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="8f9d8-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="8f9d8-107">Fatura döneminde belirtilmezse, veriler hello geçerli faturalama dönemi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8f9d8-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span>

|<span data-ttu-id="8f9d8-108">Yöntem</span><span class="sxs-lookup"><span data-stu-id="8f9d8-108">Method</span></span> | <span data-ttu-id="8f9d8-109">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="8f9d8-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="8f9d8-110">AL</span><span class="sxs-lookup"><span data-stu-id="8f9d8-110">GET</span></span>| <span data-ttu-id="8f9d8-111">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / balancesummary</span><span class="sxs-lookup"><span data-stu-id="8f9d8-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span></span>|
|<span data-ttu-id="8f9d8-112">AL</span><span class="sxs-lookup"><span data-stu-id="8f9d8-112">GET</span></span>| <span data-ttu-id="8f9d8-113">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / balancesummary</span><span class="sxs-lookup"><span data-stu-id="8f9d8-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span></span>|

> [!Note]
> <span data-ttu-id="8f9d8-114">API, toouse hello önizleme sürümünü v2 URL yukarıdaki hello v1 ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8f9d8-114">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="8f9d8-115">Yanıt</span><span class="sxs-lookup"><span data-stu-id="8f9d8-115">Response</span></span>

        {
            "id": "enrollments/100/billingperiods/201507/balancesummaries",
            "billingPeriodId": 201507,
            "currencyCode": "USD",
            "beginningBalance": 0,
            "endingBalance": 1.1,
            "newPurchases": 1,
            "adjustments": 1.1,
            "utilized": 1.1,
            "serviceOverage": 1,
            "chargesBilledSeparately": 1,
            "totalOverage": 1,
            "totalUsage": 1.1,
            "azureMarketplaceServiceCharges": 1,
            "newPurchasesDetails": [
                {
                "name": "",
                "value": 1
                }
            ],
            "adjustmentDetails": [
                {
                "name": "Promo Credit",
                "value": 1.1
                },
                {
                "name": "SIE Credit",
                "value": 1.0
                }
            ]
        }


<span data-ttu-id="8f9d8-116">**Yanıt özellik tanımları**</span><span class="sxs-lookup"><span data-stu-id="8f9d8-116">**Response property definitions**</span></span>

|<span data-ttu-id="8f9d8-117">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="8f9d8-117">Property Name</span></span>| <span data-ttu-id="8f9d8-118">Tür</span><span class="sxs-lookup"><span data-stu-id="8f9d8-118">Type</span></span>| <span data-ttu-id="8f9d8-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8f9d8-119">Description</span></span>
|-|-|-|
|<span data-ttu-id="8f9d8-120">id</span><span class="sxs-lookup"><span data-stu-id="8f9d8-120">id</span></span>|<span data-ttu-id="8f9d8-121">Dize</span><span class="sxs-lookup"><span data-stu-id="8f9d8-121">string</span></span>|<span data-ttu-id="8f9d8-122">Merhaba belirli fatura döneminin ve kaydı için benzersiz kimlik</span><span class="sxs-lookup"><span data-stu-id="8f9d8-122">hello unique Id for a specific billing period and enrollment</span></span>|
|<span data-ttu-id="8f9d8-123">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="8f9d8-123">billingPeriodId</span></span>|<span data-ttu-id="8f9d8-124">Dize</span><span class="sxs-lookup"><span data-stu-id="8f9d8-124">string</span></span> |<span data-ttu-id="8f9d8-125">Dönem kodu faturalama hello</span><span class="sxs-lookup"><span data-stu-id="8f9d8-125">hello billing period Id</span></span>|
|<span data-ttu-id="8f9d8-126">currencyCode</span><span class="sxs-lookup"><span data-stu-id="8f9d8-126">currencyCode</span></span>|<span data-ttu-id="8f9d8-127">Dize</span><span class="sxs-lookup"><span data-stu-id="8f9d8-127">string</span></span> |<span data-ttu-id="8f9d8-128">Merhaba para birimi kodu</span><span class="sxs-lookup"><span data-stu-id="8f9d8-128">hello currency code</span></span>|
|<span data-ttu-id="8f9d8-129">beginningBalance</span><span class="sxs-lookup"><span data-stu-id="8f9d8-129">beginningBalance</span></span>|<span data-ttu-id="8f9d8-130">Ondalık</span><span class="sxs-lookup"><span data-stu-id="8f9d8-130">decimal</span></span>| <span data-ttu-id="8f9d8-131">Merhaba Başlangıç bakiyesi hello fatura dönemi için</span><span class="sxs-lookup"><span data-stu-id="8f9d8-131">hello beginning balance for hello billing period</span></span>|
|<span data-ttu-id="8f9d8-132">endingBalance</span><span class="sxs-lookup"><span data-stu-id="8f9d8-132">endingBalance</span></span>|<span data-ttu-id="8f9d8-133">Ondalık</span><span class="sxs-lookup"><span data-stu-id="8f9d8-133">decimal</span></span>| <span data-ttu-id="8f9d8-134">Bakiye (için Açık dönemler bu her gün güncelleştirilir) hello fatura dönemi için bitiş hello</span><span class="sxs-lookup"><span data-stu-id="8f9d8-134">hello ending balance for hello billing period (for open periods this will be updated daily)</span></span>|
|<span data-ttu-id="8f9d8-135">newPurchases</span><span class="sxs-lookup"><span data-stu-id="8f9d8-135">newPurchases</span></span>|<span data-ttu-id="8f9d8-136">Ondalık</span><span class="sxs-lookup"><span data-stu-id="8f9d8-136">decimal</span></span>| <span data-ttu-id="8f9d8-137">Toplam yeni satın alma tutar</span><span class="sxs-lookup"><span data-stu-id="8f9d8-137">Total new purchase amount</span></span>|
|<span data-ttu-id="8f9d8-138">ayarlamaları</span><span class="sxs-lookup"><span data-stu-id="8f9d8-138">adjustments</span></span>|<span data-ttu-id="8f9d8-139">Ondalık</span><span class="sxs-lookup"><span data-stu-id="8f9d8-139">decimal</span></span>| <span data-ttu-id="8f9d8-140">Toplam ayarlama tutar</span><span class="sxs-lookup"><span data-stu-id="8f9d8-140">Total adjustment amount</span></span>|
|<span data-ttu-id="8f9d8-141">kullanılan</span><span class="sxs-lookup"><span data-stu-id="8f9d8-141">utilized</span></span>|<span data-ttu-id="8f9d8-142">Ondalık</span><span class="sxs-lookup"><span data-stu-id="8f9d8-142">decimal</span></span>| <span data-ttu-id="8f9d8-143">Toplam taahhüt kullanım</span><span class="sxs-lookup"><span data-stu-id="8f9d8-143">Total Commitment usage</span></span>|
|<span data-ttu-id="8f9d8-144">serviceOverage</span><span class="sxs-lookup"><span data-stu-id="8f9d8-144">serviceOverage</span></span>|<span data-ttu-id="8f9d8-145">Ondalık</span><span class="sxs-lookup"><span data-stu-id="8f9d8-145">decimal</span></span>| <span data-ttu-id="8f9d8-146">Azure Hizmetleri için fazla kullanım</span><span class="sxs-lookup"><span data-stu-id="8f9d8-146">Overage for Azure services</span></span>|
|<span data-ttu-id="8f9d8-147">chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="8f9d8-147">chargesBilledSeparately</span></span>|<span data-ttu-id="8f9d8-148">Ondalık</span><span class="sxs-lookup"><span data-stu-id="8f9d8-148">decimal</span></span>| <span data-ttu-id="8f9d8-149">Ücretler ayrı olarak faturalandırılır</span><span class="sxs-lookup"><span data-stu-id="8f9d8-149">Charges Billed separately</span></span>|
|<span data-ttu-id="8f9d8-150">totalOverage</span><span class="sxs-lookup"><span data-stu-id="8f9d8-150">totalOverage</span></span>|<span data-ttu-id="8f9d8-151">Ondalık</span><span class="sxs-lookup"><span data-stu-id="8f9d8-151">decimal</span></span>| <span data-ttu-id="8f9d8-152">serviceOverage + chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="8f9d8-152">serviceOverage + chargesBilledSeparately</span></span>|
|<span data-ttu-id="8f9d8-153">totalUsage</span><span class="sxs-lookup"><span data-stu-id="8f9d8-153">totalUsage</span></span>|<span data-ttu-id="8f9d8-154">Ondalık</span><span class="sxs-lookup"><span data-stu-id="8f9d8-154">decimal</span></span>| <span data-ttu-id="8f9d8-155">Azure hizmet taahhüt + toplam fazla kullanım</span><span class="sxs-lookup"><span data-stu-id="8f9d8-155">Azure service commitment + total Overage</span></span>|
|<span data-ttu-id="8f9d8-156">azureMarketplaceServiceCharges</span><span class="sxs-lookup"><span data-stu-id="8f9d8-156">azureMarketplaceServiceCharges</span></span>|<span data-ttu-id="8f9d8-157">Ondalık</span><span class="sxs-lookup"><span data-stu-id="8f9d8-157">decimal</span></span>| <span data-ttu-id="8f9d8-158">Azure Market için toplam ücretleri</span><span class="sxs-lookup"><span data-stu-id="8f9d8-158">Total charges for Azure Marketplace</span></span>|
|<span data-ttu-id="8f9d8-159">newPurchasesDetails</span><span class="sxs-lookup"><span data-stu-id="8f9d8-159">newPurchasesDetails</span></span>|<span data-ttu-id="8f9d8-160">Ad değer çifti JSON dize dizisi</span><span class="sxs-lookup"><span data-stu-id="8f9d8-160">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="8f9d8-161">Yeni satın alma işlemleri listesi</span><span class="sxs-lookup"><span data-stu-id="8f9d8-161">List of new purchases</span></span>|
|<span data-ttu-id="8f9d8-162">adjustmentDetails</span><span class="sxs-lookup"><span data-stu-id="8f9d8-162">adjustmentDetails</span></span>|<span data-ttu-id="8f9d8-163">Ad değer çifti JSON dize dizisi</span><span class="sxs-lookup"><span data-stu-id="8f9d8-163">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="8f9d8-164">Ayarlamaları (promosyon kredi, SIE kredi vb.) listesi</span><span class="sxs-lookup"><span data-stu-id="8f9d8-164">List of Adjustments (Promo credit, SIE credit etc.)</span></span> |


<br/>
## <a name="see-also"></a><span data-ttu-id="8f9d8-165">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8f9d8-165">See also</span></span>

* [<span data-ttu-id="8f9d8-166">Faturalama nokta API</span><span class="sxs-lookup"><span data-stu-id="8f9d8-166">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="8f9d8-167">Kullanım ayrıntılarını API</span><span class="sxs-lookup"><span data-stu-id="8f9d8-167">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="8f9d8-168">Market deposu ücret API</span><span class="sxs-lookup"><span data-stu-id="8f9d8-168">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="8f9d8-169">Fiyat listesi API'si</span><span class="sxs-lookup"><span data-stu-id="8f9d8-169">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)