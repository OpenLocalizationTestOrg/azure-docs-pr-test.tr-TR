---
title: "aaaAzure Kurumsal API'leri - faturalama kullanım ayrıntılarını | Microsoft Docs"
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
ms.openlocfilehash: def0805008261df5872f015db3d2b26e47d25569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---usage-details"></a>Kurumsal müşteriler - kullanım ayrıntıları için raporlama API'leri

Merhaba kullanım ayrıntı API'si tüketilen miktarları ve bir kayıt tarafından tahmini ücretleri günlük bir dökümü sunar. Merhaba sonuç ayrıca örnekleri, Ölçümler ve Departmanlar hakkında bilgi içerir. Merhaba API, faturalama dönemi veya belirtilen başlangıç ve bitiş tarihi tarafından sorgulanabilir. 
## <a name="consumption-apis"></a>Tüketim API'leri


##<a name="request"></a>İstek 
Eklenen toobe gereken ortak üstbilgi özelliklerini belirtilen [burada](billing-enterprise-api.md). Fatura döneminde belirtilmezse, veriler hello geçerli faturalama dönemi döndürülür. Özel zaman aralıkları ile Merhaba başlangıç belirtilebilir ve hello yyyy-aa-gg biçiminde içinde olan tarih parametrelerine bitiş Merhaba desteklenen en fazla süre 36 ay aralıktır.  

|Yöntem | İstek URI'si|
|-|-|
|AL|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / usagedetails 
|AL|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / usagedetails|
|AL|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / usagedetailsbycustomdate? startTime 2017-01-01 = & endTime 2017-01-10 =|

> [!Note]
> API, toouse hello önizleme sürümünü v2 URL yukarıdaki hello v1 ile değiştirin.
>

## <a name="response"></a>Yanıt

> Toohello olası büyük miktarda veri hello sonuç kümesi havuzda. Merhaba nextLink özelliği, veri hello sonraki sayfaya hello bağlantı varsa, belirtir. Merhaba bağlantı boşsa, hello son sayfasına olan gösterir. 
<br/>

    {
        "id": "string",
        "data": [
            {                       
            "accountId": 0,
            "productId": 0,
            "resourceLocationId": 0,
            "consumedServiceId": 0,
            "departmentId": 0,
            "accountOwnerEmail": "string",
            "accountName": "string",
            "serviceAdministratorId": "string",
            "subscriptionId": 0,
            "subscriptionGuid": "string",
            "subscriptionName": "string",
            "date": "2017-04-27T23:01:43.799Z",
            "product": "string",
            "meterId": "string",
            "meterCategory": "string",
            "meterSubCategory": "string",
            "meterRegion": "string",
            "meterName": "string",
            "consumedQuantity": 0,
            "resourceRate": 0,
            "Cost": 0,
            "resourceLocation": "string",
            "consumedService": "string",
            "instanceId": "string",
            "serviceInfo1": "string",
            "serviceInfo2": "string",
            "additionalInfo": "string",
            "tags": "string",
            "storeServiceIdentifier": "string",
            "departmentName": "string",
            "costCenter": "string",
            "unitOfMeasure": "string",
            "resourceGroup": "string"
            }
        ],
        "nextLink": "string"
    }

<br/>
**Yanıt özellik tanımları**

|Özellik adı| Tür| Açıklama
|-|-|-|
|id| Dize| Merhaba hello API çağrısı için benzersiz kimlik. |
|Veri| JSON dizisi| Merhaba her instance\meter günlük kullanım ayrıntılarını dizisi.|
|nextLink| Dize| Veri sayfasının hello nextLink noktaları toohello URL tooreturn hello sonraki verilerin daha fazla sayfa olduğunda. |
|Hesap Kimliği| Int| Kullanılmayan alan. Geriye dönük uyumluluk için mevcut. |
|ProductID| Int| Kullanılmayan alan. Geriye dönük uyumluluk için mevcut. |
|resourceLocationId| Int| Kullanılmayan alan. Geriye dönük uyumluluk için mevcut. |
|consumedServiceID| Int| Kullanılmayan alan. Geriye dönük uyumluluk için mevcut. |
|departmentId| Int| Kullanılmayan alan. Geriye dönük uyumluluk için mevcut. |
|accountOwnerEmail| Dize| Merhaba hesabı sahibinin e-posta hesabı. |
|accountName| Dize| Merhaba hesabının girilen müşteri adı. |
|serviceAdministratorId| Dize| E-posta adresi, Hizmet Yöneticisi. |
|subscriptionId| Int| Kullanılmayan alan. Geriye dönük uyumluluk için mevcut. |
|subscriptionGuid| Dize| Merhaba abonelik için genel benzersiz tanımlayıcı. |
|varlığıyla subscriptionName| Dize| Merhaba abonelik adı. |
|Tarih| Dize| Tüketim gerçekleştiği başlangıç tarihi. |
|Ürün| Dize| Merhaba ölçer hakkında daha fazla ayrıntı. Örnek: A1 (VM) Windows - AP Doğu|
|meterId| Dize| Kullanım yayılan hello ölçer Hello tanımlayıcısı. |
|meterCategory| Dize| Merhaba kullanılan Azure platformu hizmeti. |
|meterSubCategory| Dize| Merhaba hızını etkileyebilir hello Azure hizmet türünü tanımlar. Örnek: A1 VM (Windows dışı|
|meterRegion| Dize| Veri merkezi konum temelinde fiyatlandırılır belirli hizmetleri için hello datacenter Hello konumunu tanımlar. |
|meterName| Dize| Merhaba ölçüm adı. |
|consumedQuantity| Çift| Merhaba kullanılmış hello ölçer miktarı. |
|resourceRate| Çift| Merhaba oranı Faturalanabilir birim başına uygulanabilir. |
|Maliyet| Çift| Merhaba ölçer ücrete hello gider. |
|resourceLocation| Dize| Merhaba ölçer çalıştığı hello datacenter tanımlar. |
|consumedService| Dize| Merhaba kullanılan Azure platformu hizmeti. |
|örnek kimliği| Dize| Bu tanımlayıcı hello hello kaynak adıdır veya hello tam kaynak kimliği Daha fazla bilgi için bkz: [Azure Kaynak Yöneticisi API'si](https://docs.microsoft.com/rest/api/resources/resources) |
|serviceInfo1| Dize| İç Azure hizmeti meta verileri. |
|serviceInfo2| Dize| Örneğin, bir görüntü türü için bir sanal makine ve ExpressRoute ISS adı. |
|additionalınfo alanına| Dize| Hizmete özgü meta veriler. Örneğin, bir görüntü türü için bir sanal makine. |
|etiketler| Dize| Müşteri etiketleri eklendi. Daha fazla bilgi için bkz: [etiketlerle Azure kaynaklarınızı düzenleme](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags). |
|storeServiceIdentifier| Dize| Bu sütunlar kullanılmaz. Geriye dönük uyumluluk için mevcut. |
|departmentName| Dize| Merhaba bölüm adı. |
|costCenter| Dize| Merhaba kullanımı ile ilişkili hello maliyet merkezi. |
|unitOfMeasure| Dize| Merhaba hizmet içinde doludur hello birimi tanımlar. Örnek: GB, saat, 10.000 s. |
|kaynak grubu| Dize| Merhaba kaynak grubu hangi hello dağıtılan ölçer çalışıyor. Daha fazla bilgi için bkz. [Azure Resource Manager’a genel bakış](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview). |
<br/>
## <a name="see-also"></a>Ayrıca bkz.

* [Faturalama nokta API](billing-enterprise-api-billing-periods.md)

* [Bakiye ve özeti API](billing-enterprise-api-balance-summary.md)

* [Market deposu ücret API](billing-enterprise-api-marketplace-storecharge.md) 

* [Fiyat listesi API'si](billing-enterprise-api-pricesheet.md)
