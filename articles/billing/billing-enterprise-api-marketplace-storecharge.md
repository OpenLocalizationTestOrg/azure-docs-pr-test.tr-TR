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
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a>Kurumsal müşteriler - Market deposu Ücret için raporlama API'leri

Merhaba Market deposu ücret API döndürür hello kullanım tabanlı Market ücretleri dökümü hello için günlük belirtilen fatura dönemi veya başlangıç ve bitiş tarihleri (bir kez ücretler dahil değildir).

##<a name="request"></a>İstek 
Eklenen toobe gereken ortak üstbilgi özelliklerini belirtilen [burada](billing-enterprise-api.md). Fatura döneminde belirtilmezse, veriler hello geçerli faturalama dönemi döndürülür. Özel zaman aralıkları ile Merhaba başlangıç belirtilebilir ve hello biçimi yyyy-aa-gg, desteklenen maksimum hello zamanında 36 ay aralığı olduğu tarih parametrelerine bitmelidir.  

|Yöntem | İstek URI'si|
|-|-|
|AL|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / marketplacecharges|
|AL|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / marketplacecharges|
|AL|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / marketplacechargesbycustomdate? startTime 2017-01-01 = & endTime 2017-01-10 =|

> [!Note]
> API, toouse hello önizleme sürümünü v2 URL yukarıdaki hello v1 ile değiştirin.
>

## <a name="response"></a>Yanıt
 
    
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
    

**Yanıt özellik tanımları**

|Özellik adı| Tür| Açıklama
|-|-|-|
|id|Dize|Merhaba Market ücret öğesi için benzersiz kimliği|
|subscriptionGuid|GUID|Merhaba abonelik GUID|
|varlığıyla subscriptionName|Dize|Merhaba abonelik adı|
|meterId|Dize|Ölçer hello kimliği yayılan|
|usageStartDate|Tarih saat|Merhaba kullanım kaydı için başlangıç zamanı|
|usageEndDate|Tarih saat|Merhaba kullanım kaydı için bitiş zamanı|
|offerName|Dize|Merhaba teklif adı|
|kaynak grubu|Dize|Merhaba kaynak grubu|
|örnek kimliği|Dize|Örnek kimliği|
|additionalınfo alanına|Dize|Ek bilgi JSON dizesi|
|etiketler|Dize|Etiket JSON dizesi|
|orderNumber|Dize|Merhaba sipariş numarası|
|unitOfMeasure|Dize|Ölçü hello ölçer|
|costCenter|Dize|Merhaba maliyet merkezi|
|Hesap Kimliği|Int|Merhaba hesap kimliği|
|accountName|Dize |Merhaba hesap adı|
|accountOwnerId|Dize|Merhaba hesap sahibinin kimliği|
|departmentId|Int|Merhaba bölüm kimliği|
|departmentName|Dize|Merhaba bölüm adı|
|publisherName|Dize|Merhaba Yayımcı adı|
|planName|Dize|Merhaba planı adı|
|consumedQuantity|Ondalık|Bu süre boyunca Tüketilen Miktar|
|resourceRate|Ondalık|Birim Fiyat hello ölçmek için|
|extendedCost|Ondalık|Tüketilen Miktar ve genişletilmiş maliyet göre ücret tahmini|
<br/>
## <a name="see-also"></a>Ayrıca bkz.

* [Faturalama nokta API](billing-enterprise-api-billing-periods.md)

* [Kullanım ayrıntılarını API](billing-enterprise-api-usage-detail.md) 

* [Bakiye ve özeti API](billing-enterprise-api-balance-summary.md)

* [Fiyat listesi API'si](billing-enterprise-api-pricesheet.md)