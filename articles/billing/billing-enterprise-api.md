---
title: aaaAzure faturalama Kurumsal API'leri | Microsoft Docs
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
ms.openlocfilehash: 017cecc57ad6bdeb402b5d9d57fc95df9b033a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a>Kurumsal müşteriler için raporlama API'leri genel bakış
Merhaba raporlama API'leri kuruluş Azure müşterilerin tooprogrammatically çekme kullanım ve fatura veri tercih edilen veri çözümleme araçları etkinleştirin. 

## <a name="enabling-data-access-toohello-api"></a>Veri erişim toohello API etkinleştirme
* **Oluşturmak veya hello API anahtarı alıp** - günlük - Yardım altında toohello Enterprise portal ve izleme hello öğreticide raporlama API'leri. Bu Yardım makalenin ilk bölümünde Hello nasıl toogenerate veya alma hello API anahtarı hello için kayıt belirtilen açıklanmaktadır.
* **Merhaba API anahtarları geçirme** -hello API anahtarı kimlik doğrulaması ve yetkilendirme her çağrı için geçirilen toobe gerekir. Merhaba aşağıdaki özellik toobe toohello HTTP üstbilgileri olması gerekiyor

|Üstbilgi anahtarı iste | Değer|
|-|-|
|Yetkilendirme| Merhaba değer şu biçimde belirtin: **taşıyıcı {apı_key}** <br/> Örnek: taşıyıcı eyr... 09|

## <a name="consumption-apis"></a>Tüketim API'leri
Swagger uç nokta kullanılabilir [burada](https://consumption.azure.com/swagger/ui/index) Merhaba API'leri altında etkinleştir kolay introspection hello API ve hello özelliği toogenerate istemci SDK'ları kullanma konusunda açıklandığı [AutoRest](https://github.com/Azure/AutoRest) veya [ CodeGen swagger](http://swagger.io/swagger-codegen/). 1 Mayıs 2014 başlayan veriler bu API aracılığıyla kullanılabilir. 

* **Yük Dengeleme ve Özet** - hello [dengelemek ve Özet API](billing-enterprise-api-balance-summary.md) aylık bakiyelerini, yeni satın alma işlemleri, Azure Marketi servis ücretleri, ayarlamalar ve fazla kullanım ücretleri bilgilerin özetini sunar.

* **Kullanım ayrıntılarını** - hello [kullanım ayrıntı API'si](billing-enterprise-api-usage-detail.md) tüketilen miktarları ve bir kayıt tarafından tahmini ücretleri günlük bir dökümü sunar. Merhaba sonuç ayrıca örnekleri, Ölçümler ve Departmanlar hakkında bilgi içerir. Merhaba API, faturalama dönemi veya belirtilen başlangıç ve bitiş tarihi tarafından sorgulanabilir. 

* **Market deposu ücret** - hello [Market deposu ücret API](billing-enterprise-api-marketplace-storecharge.md) hello Faturalama dönem veya (bir kez ücretleri olmayan dahil) başlangıç ve bitiş tarihleri belirtilen için hello kullanım tabanlı Market ücretleri dökümü güne göre döndürür. .

* **Fiyat listesi** - hello [fiyat listesi API](billing-enterprise-api-pricesheet.md) verilen kayıt ve faturalama dönemi hello her ölçer hello geçerli hızı sunar. 

## <a name="helper-apis"></a>Yardımcısı API'ları
 **Liste faturalama nokta** - hello [faturalama nokta API](billing-enterprise-api-billing-periods.md) Tüketim verileri hello kayıt ters kronolojik sırada belirtilen için olan nokta faturalama bir liste döndürür. Her dönem toohello API rota verilerini - BalanceSummary, UsageDetails, Market ücretleri ve fiyat listesi hello dört kümeleri için işaret eden bir özellik içerir.


## <a name="api-response-codes"></a>API yanıt kodları  
|Yanıt durum kodu|İleti|Açıklama|
|-|-|-|
|200| TAMAM|Hiçbir hata|
|401| Yetkilendirilmemiş| API anahtarı bulunamadı, geçersiz, vb. süresi doldu.|
|404| Kullanılamıyor| Rapor uç noktası bulunamadı|
|400| Hatalı istek| Geçersiz params – tarih aralıkları EA numaralarını vb..|
|500| Sunucu hatası| İstek işleme Unexoected hatası| 









