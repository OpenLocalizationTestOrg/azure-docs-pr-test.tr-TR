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
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a>Kurumsal müşteriler - faturalama nokta için raporlama API'leri

Merhaba nokta API faturalama verileriniz tüketim hello nokta faturalama listesi kayıt ters kronolojik sırada belirtilen döndürür. Her dönem toohello API rota verilerini - BalanceSummary, UsageDetails, Marktplace ücretleri ve fiyat listesi hello dört kümeleri için işaret eden bir özellik içerir. Merhaba dönem veri yoksa hello karşılık gelen özelliği null olur. 


##<a name="request"></a>İstek 
Eklenen toobe gereken ortak üstbilgi özelliklerini belirtilen [burada](billing-enterprise-api.md). 

|Yöntem | İstek URI'si|
|-|-|
|AL| https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / billingperiods|

> [!Note]
> API, toouse hello önizleme sürümünü v2 URL yukarıdaki hello v1 ile değiştirin.
>

## <a name="response"></a>Yanıt
 
    
    
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
    

**Yanıt özellik tanımları**

|Özellik adı| Tür| Açıklama
|-|-|-|
|billingPeriodId| Dize| Merhaba belirli bir fatura dönemi temsil eden benzersiz kimliği|
|billingStart| Tarih saat| Merhaba dönem başlangıç tarihi temsil eden ISO 8601 dize|
|billingEnd| Tarih saat| Merhaba dönem bitiş tarihi temsil eden ISO 8601 dize|
|balanceSummary| Dize| Bu dönem için toohello bakiye özeti verilerini yönlendirir hello URL yolu|
|usageDetails| Dize| Bu dönem için toohello kullanım ayrıntılarını veri yolları hello URL yolu|
|marketplaceCharges| Dize| Bu dönem için toohello Market ücretleri veri yolları hello URL yolu|
|Fiyat listesi| Dize| Bu dönem için toohello fiyat listesi veri yolları hello URL yolu|

<br/>
## <a name="see-also"></a>Ayrıca bkz.

* [Bakiye ve özeti API](billing-enterprise-api-balance-summary.md)

* [Kullanım ayrıntılarını API](billing-enterprise-api-usage-detail.md) 

* [Market deposu ücret API](billing-enterprise-api-marketplace-storecharge.md) 

* [Fiyat listesi API'si](billing-enterprise-api-pricesheet.md)