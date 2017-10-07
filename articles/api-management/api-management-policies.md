---
title: aaaAzure API Management ilkeleri | Microsoft Docs
description: "Azure API Management'te kullanıma hello ilkeleri hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 1cc460cb-8e67-41aa-bc76-bbafc1892798
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1c468ff37d73359f1dd694b91e20c2ca04f8934e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-policies"></a>API Management ilkeleri
Bu bölümde API Management ilkelere hello için bir başvuru sağlar. Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).  
  
 Güçlü bir özellik toochange hello davranışını yapılandırma yoluyla hello API hello publisher izin hello sisteminin ilkelerdir. Merhaba istek üzerinde sırayla yürütülen deyimlerin bir koleksiyon veya bir API yanıtını ilkelerdir. Sık kullanılan deyimler XML tooJSON biçimi dönüştürme içerir ve bir geliştiriciden gelen çağrıların toorestrict hello miktarını sınırlamak oranı çağırın. Çok daha fazla ilke hello kutu dışı kullanılabilir.  
  
 Merhaba ilke aksini belirtmedikçe ilke ifadelerini öznitelik değerleri ya da metin değerleri hello API Management ilkeleri olarak kullanılabilir. Hello gibi bazı ilkeler [kontrol akışı](api-management-advanced-policies.md#choose) ve [değişken Ayarla](api-management-advanced-policies.md#set-variable) ilkeler ilke ifadelerini temel alarak. Daha fazla bilgi için bkz: [ilkeleri Gelişmiş](api-management-advanced-policies.md#AdvancedPolicies) ve [ilke ifadelerini](api-management-policy-expressions.md).  
  
##  <a name="ProxyPolicies"></a>İlkeleri  
  
-   [Erişimi kısıtlama ilkeleri](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   [Onay HTTP üstbilgisi](api-management-access-restriction-policies.md#CheckHTTPHeader) -varlığı ve/veya bir HTTP üstbilgisi değerini zorlar.  
  
    -   [Abonelik tarafından çağrı hızını sınırla](api-management-access-restriction-policies.md#LimitCallRate) -engeller API kullanımı ani başına abonelik başına çağrı hızını sınırlayarak.  
  
    -   [Anahtara göre çağrı hızını sınırla](api-management-access-restriction-policies.md#LimitCallRateByKey) -engeller API kullanımı ani başına anahtar başına çağrı hızını sınırlayarak.  
  
    -   [Arayan IP'leri kısıtlamak](api-management-access-restriction-policies.md#RestrictCallerIPs) -filtreleri (verir/engellediği) çağrılarından belirli IP adreslerini ve/veya adres aralığı.  
  
    -   [Abonelik tarafından kullanım kotası ayarla](api-management-access-restriction-policies.md#SetUsageQuota) -bir abonelik başına temelinde tooenforce yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kotaya izin verir.  
  
    -   [Anahtara göre kullanım kotası ayarla](api-management-access-restriction-policies.md#SetUsageQuotaByKey) -bir anahtar başına temelinde tooenforce yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kotaya izin verir.  
  
    -   [JWT doğrulama](api-management-access-restriction-policies.md#ValidateJWT) -varlığı ve belirtilen bir HTTP üstbilgisi veya belirtilen sorgu parametresi ayıklanan JWT geçerliliğini zorlar.  
  
-   [Gelişmiş ilkeler](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   [Denetim akışı](api-management-advanced-policies.md#choose) - koşullu ilke deyimleri Boole ifadeleri hello değerlendirmesine göre uygulanır.  
  
    -   [İstek](api-management-advanced-policies.md#ForwardRequest) -hello isteği toohello arka uç hizmeti iletir.  
  
    -   [TooEvent Hub oturum](api-management-advanced-policies.md#log-to-eventhub) -hello belirtilen biçim tooa ileti hedefinde Günlükçü varlık tarafından tanımlanan iletileri gönderir.  
  
    -   [Yeniden deneme](api-management-advanced-policies.md#Retry) -hello yürütülmesi yeniden deneme içine ilke deyimleri varsa ve hello koşul yerine getirilene kadar. Yürütme yineleyin belirtilen zaman aralığı hello ve belirtilen toohello yeniden deneme sayısı.  
  
    -   [Yanıt](api-management-advanced-policies.md#ReturnResponse) -iptalleri ardışık düzen yürütmesi ve döndürür hello belirtilen yanıt doğrudan toohello çağıran.  
  
    -   [Tek yönlü İsteği Gönder](api-management-advanced-policies.md#SendOneWayRequest) -bir istek toohello belirtilen URL için bir yanıt beklemeden gönderir.  
  
    -   [İsteği Gönder](api-management-advanced-policies.md#SendRequest) -bir istek toohello belirtilen URL gönderir.  
  
    -   [Değişken Ayarla](api-management-advanced-policies.md#set-variable) -adlandırılmış bağlamının sonraki erişim için bir değer kalır.  
  
    -   [İstek yöntemini ayarla](api-management-advanced-policies.md#SetRequestMethod) -bir istek için toochange hello HTTP yöntemi sağlar.  
  
    -   [Durum kodu ayarlamak](api-management-advanced-policies.md#SetStatus) -değişiklikleri hello HTTP durum kodu toohello belirtilen değeri.  
  
    -   [İzleme](api-management-advanced-policies.md#Trace) -hello bir dize ekler [API denetçisi](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) çıktı.  
  
    -   [Bekleyin](api-management-advanced-policies.md#Wait) -içine için bekleyeceği [gönderme isteği](api-management-advanced-policies.md#SendRequest), [değeri önbellekten alma](api-management-caching-policies.md#GetFromCacheByKey), veya [kontrol akışı](api-management-advanced-policies.md#choose) ilkeleri toocomplete devam etmeden önce.  
  
-   [Kimlik doğrulama ilkeleri](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   [Basic ile kimlik doğrulaması](api-management-authentication-policies.md#Basic) -temel kimlik doğrulaması kullanarak arka uç hizmeti ile kimlik doğrulaması.  
  
    -   [İstemci sertifikası ile kimlik doğrulaması](api-management-authentication-policies.md#ClientCertificate) -istemci sertifikalarını kullanan bir arka uç hizmeti ile kimlik doğrulaması.  
  
-   [Önbelleğe alma ilkeleri](api-management-caching-policies.md#CachingPolicies)  
  
    -   [Önbellekten alma](api-management-caching-policies.md#GetFromCache) -önbellek gerçekleştirmek aramak ve geçerli bir önbelleğe alınan yanıt kullanılabilir olduğunda döndürür.  
  
    -   [Depolama toocache](api-management-caching-policies.md#StoreToCache) -toohello göre önbellekleri yanıt belirtilen önbellek denetimi yapılandırma.  
  
    -   [Önbelleğe alınan değer alma](api-management-caching-policies.md#GetFromCacheByKey) -anahtar tarafından önbelleğe alınmış bir öğeyi geri almak.  
  
    -   [Değer önbellekte depolamak](api-management-caching-policies.md#StoreToCacheByKey) -bir öğe anahtarı tarafından hello önbelleğine depolayabilirsiniz.  
  
    -   [Önbelleğe alınan değer Kaldır](api-management-caching-policies.md#RemoveCacheByKey) -öğeyi hello önbelleğinde anahtarının kaldırmak.  
  
-   [Çapraz etki alanı ilkeleri](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   [Etki alanları arası çağrılar izin](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -yapar hello API erişilebilir Microsoft Silverlight Adobe Flash ve tarayıcı tabanlı istemcilerden.  
  
    -   [CORS](api-management-cross-domain-policies.md#CORS) -çıkış noktaları arası kaynak paylaşımını (CORS) tooan işlemi destekler veya bir API tooallow etki alanları arası tarayıcı tabanlı istemcilerden çağıran ekler.  
  
    -   [JSONP](api-management-cross-domain-policies.md#JSONP) - JSON ile destek tooan işlemi (JSONP) doldurma ekler veya bir API tooallow etki alanları arası JavaScript tarayıcı tabanlı istemcilerden çağırır.  
  
-   [Dönüştürme ilkeleri](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   [JSON tooXML Dönüştür](api-management-transformation-policies.md#ConvertJSONtoXML) - dönüştürür istek veya yanıt gövdesi JSON tooXML.  
  
    -   [XML tooJSON Dönüştür](api-management-transformation-policies.md#ConvertXMLtoJSON) - dönüştürür istek veya yanıt gövdesi XML tooJSON.  
  
    -   [Bulma ve değiştirme dizesi gövdesi içinde](api-management-transformation-policies.md#Findandreplacestringinbody) - bir istek veya yanıt alt dizeyi bulur ve farklı bir dizeyle değiştirir.  
  
    -   [İçeriği URL'leri maske](api-management-transformation-policies.md#MaskURLSContent) -(maskeleri)'yeniden yazar bağlantılar hello yanıt gövdesi böylece hello ağ geçidi aracılığıyla toohello eşdeğer bağlantı noktası.  
  
    -   [Arka uç hizmetini ayarlamak](api-management-transformation-policies.md#SetBackendService) -değişiklikleri hello arka uç hizmetine gelen bir istek için.  
  
    -   [Gövde ayarlamak](api-management-transformation-policies.md#SetBody) -hello ileti gövdesi gelen ve giden istekleri için ayarlar.  
  
    -   [HTTP üstbilgisi kümesi](api-management-transformation-policies.md#SetHTTPheader) - değer tooan varolan yanıt ve/veya istek üstbilgisi atar veya yeni bir yanıt ve/veya istek üstbilgisi ekler.  
  
    -   [Sorgu dizesi parametresi kümesi](api-management-transformation-policies.md#SetQueryStringParameter) - ekler, değiştirir değerini veya istek sorgu dizesi parametresi siler.  
  
    -   [URL yeniden yazma](api-management-transformation-policies.md#RewriteURL) -hello web hizmeti tarafından beklenen genel form toohello formundan bir istek URL'sini dönüştürür.  
  
    -   [XSLT kullanarak XML dönüştürme](api-management-transformation-policies.md#XSLTransform) -bir XSL Dönüştürme tooXML hello istek veya yanıt gövdesi içinde geçerlidir.  
  
## <a name="next-steps"></a>Sonraki adımlar
İlkeleriyle çalışma daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).  
