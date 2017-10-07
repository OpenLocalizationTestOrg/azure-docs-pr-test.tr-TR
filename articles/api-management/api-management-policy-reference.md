---
title: "aaaAzure API Management ilke başvurusu"
description: "Merhaba ilkeleri kullanılabilir tooconfigure hakkında API Management hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 9d4ac609-b221-4032-93ae-e27a1254d43d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7ee194f4d6f172bf836c789cbe8ab732e18a7e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-policy-reference"></a>Azure API Management ilke başvurusu
Bu bölümde hello hello ilkelerinde dizin sağlayan [API Management ilke başvurusu][API Management policy reference]. Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri][Policies in API Management].

Merhaba ilke aksini belirtmedikçe ilke ifadelerini öznitelik değerleri ya da metin değerleri hello API Management ilkeleri olarak kullanılabilir. Hello gibi bazı ilkeler [kontrol akışı] [ Control flow] ve [değişken Ayarla] [ Set variable] ilkeler ilke ifadelerini temel alarak. Daha fazla bilgi için bkz: [ilkeleri Gelişmiş] [ Advanced policies] ve [ilke ifadeleri][Policy expressions]

## <a name="policy-reference-index"></a>İlke başvuru dizini
* [Erişimi kısıtlama ilkeleri][Access restriction policies]
  * [Onay HTTP üstbilgisi] [ Check HTTP header] -varlığı ve/veya bir HTTP üstbilgisi değerini zorlar.
  * [Abonelik tarafından çağrı hızını sınırla] [ Limit call rate by subscription] -engeller API kullanımı ani başına abonelik başına çağrı hızını sınırlayarak.
  * [Anahtara göre çağrı hızını sınırla](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) -engeller API kullanımı ani başına anahtar başına çağrı hızını sınırlayarak.
  * [Arayan IP'leri kısıtlamak] [ Restrict caller IPs] -filtreleri (verir/engellediği) çağrılarından belirli IP adreslerini ve/veya adres aralığı.
  * [Abonelik tarafından kullanım kotası ayarla] [ Set usage quota by subscription] -bir abonelik başına temelinde tooenforce yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kotaya izin verir.
  * [Anahtara göre kullanım kotası ayarla](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) -bir anahtar başına temelinde tooenforce yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kotaya izin verir.
  * [JWT doğrulama] [ Validate JWT] -varlığı ve belirtilen bir HTTP üstbilgisi veya belirtilen sorgu parametresi ayıklanan JWT geçerliliğini zorlar.
* [Gelişmiş ilkeleri][Advanced policies]
  * [Denetim akışı] [ Control flow] - koşullu ilke deyimleri hello hello değerlendirme Boole sonuçlarına dayalı uygular [ifadeleri][expressions].
  * [İstek] [ Forward request] -hello isteği toohello arka uç hizmeti iletir.
  * [TooEvent Hub oturum] [ Log tooEvent Hub] -hello belirtilen biçim tooa ileti hedefinde tarafından tanımlanan iletileri gönderen bir [Günlükçü](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) varlık.
  * [Yeniden deneme](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) -hello yürütülmesi yeniden deneme içine ilke deyimleri varsa ve hello koşul yerine getirilene kadar. Yürütme yineleyin belirtilen zaman aralığı hello ve belirtilen toohello yeniden deneme sayısı.
  * [Yanıt](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) -iptalleri ardışık düzen yürütmesi ve döndürür hello belirtilen yanıt doğrudan toohello çağıran.
  * [Tek yönlü İsteği Gönder](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) -bir istek toohello belirtilen URL için bir yanıt beklemeden gönderir.
  * [İsteği Gönder](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) -bir istek toohello belirtilen URL gönderir.
  * [İstek yöntemini ayarla](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) -bir istek için toochange hello HTTP yöntemi sağlar.
  * [Durum Ayarla](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) -değişiklikleri hello HTTP durum kodu toohello belirtilen değeri.
  * [Değişken Ayarla] [ Set variable] -adlandırılmış bir değer kalıcı [bağlamı] [ context] sonraki erişim için değişken.
  * [İzleme](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) -hello bir dize ekler [API denetçisi](api-management-howto-api-inspector.md) çıktı.
  * [Bekleyin](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - kapalı gönderme bekler isteği, önbelleğe alınan değer almak veya denetim akışı ilkeleri toocomplete devam etmeden önce.
* [Kimlik doğrulama ilkeleri][Authentication policies]
  * [Basic ile kimlik doğrulaması] [ Authenticate with Basic] -temel kimlik doğrulaması kullanarak arka uç hizmeti ile kimlik doğrulaması.
  * [İstemci sertifikası ile kimlik doğrulaması] [ Authenticate with client certificate] -istemci sertifikalarını kullanan bir arka uç hizmeti ile kimlik doğrulaması.
* [Önbelleğe alma ilkeleri][Caching policies] 
  * [Önbellekten alma] [ Get from cache] -önbellek gerçekleştirmek aramak ve geçerli bir önbelleğe alınan yanıt kullanılabilir olduğunda döndürür.
  * [Depolama toocache] [ Store toocache] -toohello göre önbellekleri yanıt belirtilen önbellek denetimi yapılandırma.
  * [Önbelleğe alınan değer alma](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) -anahtar tarafından önbelleğe alınmış bir öğeyi geri almak.
  * [Değer önbellekte depolamak](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -bir öğe anahtarı tarafından hello önbelleğine depolayabilirsiniz.
  * [Önbelleğe alınan değer Kaldır](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) -öğeyi hello önbelleğinde anahtarının kaldırmak.
* [Etki alanı ilkelerini arası][Cross domain policies] 
  * [Etki alanları arası çağrılar izin] [ Allow cross-domain calls] -yapar hello API erişilebilir Microsoft Silverlight Adobe Flash ve tarayıcı tabanlı istemcilerden.
  * [CORS] [ CORS] -çıkış noktaları arası kaynak paylaşımını (CORS) tooan işlemi destekler veya bir API tooallow etki alanları arası tarayıcı tabanlı istemcilerden çağıran ekler.
  * [JSONP] [ JSONP] - JSON ile destek tooan işlemi (JSONP) doldurma ekler veya bir API tooallow etki alanları arası JavaScript tarayıcı tabanlı istemcilerden çağırır.
* [Dönüştürme ilkelerini][Transformation policies] 
  * [JSON tooXML Dönüştür] [ Convert JSON tooXML] - dönüştürür istek veya yanıt gövdesi JSON tooXML.
  * [XML tooJSON Dönüştür] [ Convert XML tooJSON] - dönüştürür istek veya yanıt gövdesi XML tooJSON.
  * [Bulma ve değiştirme dizesi gövdesi içinde] [ Find and replace string in body] - bir istek veya yanıt alt dizeyi bulur ve farklı bir dizeyle değiştirir.
  * [İçeriği URL'leri maske] [ Mask URLs in content] -(maskeleri)'yeniden yazar bağlantılar hello yanıt gövdesi böylece hello ağ geçidi aracılığıyla toohello eşdeğer bağlantı noktası.
  * [Arka uç hizmetini ayarlamak] [ Set backend service] -değişiklikleri hello arka uç hizmetine gelen bir istek için.
  * [Gövde ayarlamak] [ Set body] -hello ileti gövdesi gelen ve giden istekleri için ayarlar.
  * [HTTP üstbilgisi kümesi] [ Set HTTP header] - değer tooan varolan yanıt ve/veya istek üstbilgisi atar veya yeni bir yanıt ve/veya istek üstbilgisi ekler.
  * [Sorgu dizesi parametresi kümesi] [ Set query string parameter] - ekler, değiştirir değerini veya istek sorgu dizesi parametresi siler.
  * [URL yeniden yazma] [ Rewrite URL] -hello web hizmeti tarafından beklenen genel form toohello formundan bir istek URL'sini dönüştürür.

## <a name="next-steps"></a>Sonraki adımlar
İlke ifadeleri hakkında daha fazla bilgi için aşağıdaki videoyu hello bakın.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Access restriction policies]: https://msdn.microsoft.com/library/azure/dn894078.aspx
[Check HTTP header]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#CheckHTTPHeader
[Limit call rate by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#LimitCallRate
[Restrict caller IPs]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#RestrictCallerIPs
[Set usage quota by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#SetUsageQuota
[Validate JWT]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx
[context]: https://msdn.microsoft.com/library/azure/ea160028-fc04-4782-aa26-4b8329df3448#ContextVariables
[Forward request]: https://msdn.microsoft.com/library/azure/dn894085.aspx#ForwardRequest
[Log tooEvent Hub]: https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub

[Authentication policies]: https://msdn.microsoft.com/library/azure/dn894079.aspx
[Authenticate with Basic]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#Basic
[Authenticate with client certificate]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#ClientCertificate
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx
[Get from cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#GetFromCache
[Store toocache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#StoreToCache

[Cross domain policies]: https://msdn.microsoft.com/library/azure/dn894084.aspx
[Allow cross-domain calls]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#AllowCrossDomainCalls
[CORS]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#CORS
[JSONP]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#JSONP

[Transformation policies]: https://msdn.microsoft.com/library/azure/dn894083.aspx
[Convert JSON tooXML]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertJSONtoXML
[Convert XML tooJSON]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertXMLtoJSON
[Find and replace string in body]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#Findandreplacestringinbody
[Mask URLs in content]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#MaskURLSContent
[Set backend service]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetBackendService
[Set body]: https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBody
[Set HTTP header]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetHTTPheader
[Set query string parameter]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetQueryStringParameter
[Rewrite URL]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#RewriteURL



[Policies in API Management]: api-management-howto-policies.md
[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx

[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx


