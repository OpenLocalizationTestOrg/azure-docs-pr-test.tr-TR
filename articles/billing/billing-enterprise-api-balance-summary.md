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
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a>Kurumsal müşteriler - bakiye ve özeti için raporlama API'leri

Merhaba bakiye ve Özet API aylık bakiyelerini, yeni satın alma işlemleri, Azure Marketi servis ücretleri, ayarlamalar ve fazla kullanım ücretleri bilgilerin özetini sunar.


##<a name="request"></a>İstek 
Eklenen toobe gereken ortak üstbilgi özelliklerini belirtilen [burada](billing-enterprise-api.md). Fatura döneminde belirtilmezse, veriler hello geçerli faturalama dönemi döndürülür.

|Yöntem | İstek URI'si|
|-|-|
|AL| https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / balancesummary|
|AL| https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / balancesummary|

> [!Note]
> API, toouse hello önizleme sürümünü v2 URL yukarıdaki hello v1 ile değiştirin.
>

## <a name="response"></a>Yanıt

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


**Yanıt özellik tanımları**

|Özellik adı| Tür| Açıklama
|-|-|-|
|id|Dize|Merhaba belirli fatura döneminin ve kaydı için benzersiz kimlik|
|billingPeriodId|Dize |Dönem kodu faturalama hello|
|currencyCode|Dize |Merhaba para birimi kodu|
|beginningBalance|Ondalık| Merhaba Başlangıç bakiyesi hello fatura dönemi için|
|endingBalance|Ondalık| Bakiye (için Açık dönemler bu her gün güncelleştirilir) hello fatura dönemi için bitiş hello|
|newPurchases|Ondalık| Toplam yeni satın alma tutar|
|ayarlamaları|Ondalık| Toplam ayarlama tutar|
|kullanılan|Ondalık| Toplam taahhüt kullanım|
|serviceOverage|Ondalık| Azure Hizmetleri için fazla kullanım|
|chargesBilledSeparately|Ondalık| Ücretler ayrı olarak faturalandırılır|
|totalOverage|Ondalık| serviceOverage + chargesBilledSeparately|
|totalUsage|Ondalık| Azure hizmet taahhüt + toplam fazla kullanım|
|azureMarketplaceServiceCharges|Ondalık| Azure Market için toplam ücretleri|
|newPurchasesDetails|Ad değer çifti JSON dize dizisi|Yeni satın alma işlemleri listesi|
|adjustmentDetails|Ad değer çifti JSON dize dizisi|Ayarlamaları (promosyon kredi, SIE kredi vb.) listesi |


<br/>
## <a name="see-also"></a>Ayrıca bkz.

* [Faturalama nokta API](billing-enterprise-api-billing-periods.md)

* [Kullanım ayrıntılarını API](billing-enterprise-api-usage-detail.md) 

* [Market deposu ücret API](billing-enterprise-api-marketplace-storecharge.md) 

* [Fiyat listesi API'si](billing-enterprise-api-pricesheet.md)