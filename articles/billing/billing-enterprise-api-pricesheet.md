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
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a>Kurumsal müşteriler - fiyat listesi için raporlama API'leri

Merhaba fiyat listesi API verilen kayıt ve faturalama dönemi hello her ölçer hello geçerli hızı sunar.

##<a name="request"></a>İstek
Eklenen toobe gereken ortak üstbilgi özelliklerini belirtilen [burada](billing-enterprise-api.md). Fatura döneminde belirtilmezse, veriler hello geçerli faturalama dönemi döndürülür.

|Yöntem | İstek URI'si|
|-|-|
|AL|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / fiyat listesi|
|AL|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / fiyat listesi|

> [!Note]
> API, toouse hello önizleme sürümünü v2 URL yukarıdaki hello v1 ile değiştirin.
>

## <a name="response"></a>Yanıt

    
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
>Merhaba Önizleme API kullanıyorsanız, meterId alan kullanılamaz.
>

**Yanıt özellik tanımları**

|Özellik adı| Tür| Açıklama
|-|-|-|
|id| Dize| Merhaba belirli bir fiyat listesi öğesini (faturalama dönemi tarafından ölçer) temsil eden benzersiz kimliği|
|billingPeriodId| Dize| Merhaba belirli bir fatura dönemi temsil eden benzersiz kimliği|
|meterId| Dize| Merhaba ölçer Hello tanımlayıcısı. Eşlenen toohello kullanım meterId olabilir.|
|meterName| Dize| Merhaba ölçüm adı|
|unitOfMeasure| Dize| Merhaba hizmet ölçmek için ölçü hello|
|includedQuantity| Ondalık| Dahil edilen miktar |
|partNumber| Dize| Ölçer Hello ile ilişkili hello parça numarası|
|unitPrice| Ondalık| Merhaba birim fiyat hello ölçmek için|
|currencyCode| Dize| Merhaba unitPrice Hello para birimi kodu|
<br/>
## <a name="see-also"></a>Ayrıca bkz.

* [Faturalama nokta API](billing-enterprise-api-billing-periods.md)

* [Kullanım ayrıntılarını API](billing-enterprise-api-usage-detail.md)

* [Bakiye ve özeti API](billing-enterprise-api-balance-summary.md)

* [Market deposu ücret API](billing-enterprise-api-marketplace-storecharge.md)
