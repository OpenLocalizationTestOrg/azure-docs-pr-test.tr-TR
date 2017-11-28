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
# <a name="azure-api-management-policy-reference"></a><span data-ttu-id="c9052-103">Azure API Management ilke başvurusu</span><span class="sxs-lookup"><span data-stu-id="c9052-103">Azure API Management Policy Reference</span></span>
<span data-ttu-id="c9052-104">Bu bölümde hello hello ilkelerinde dizin sağlayan [API Management ilke başvurusu][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="c9052-104">This section provides an index for hello policies in hello [API Management policy reference][API Management policy reference].</span></span> <span data-ttu-id="c9052-105">Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri][Policies in API Management].</span><span class="sxs-lookup"><span data-stu-id="c9052-105">For information on adding and configuring policies, see [Policies in API Management][Policies in API Management].</span></span>

<span data-ttu-id="c9052-106">Merhaba ilke aksini belirtmedikçe ilke ifadelerini öznitelik değerleri ya da metin değerleri hello API Management ilkeleri olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c9052-106">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="c9052-107">Hello gibi bazı ilkeler [kontrol akışı] [ Control flow] ve [değişken Ayarla] [ Set variable] ilkeler ilke ifadelerini temel alarak.</span><span class="sxs-lookup"><span data-stu-id="c9052-107">Some policies such as hello [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="c9052-108">Daha fazla bilgi için bkz: [ilkeleri Gelişmiş] [ Advanced policies] ve [ilke ifadeleri][Policy expressions]</span><span class="sxs-lookup"><span data-stu-id="c9052-108">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions]</span></span>

## <a name="policy-reference-index"></a><span data-ttu-id="c9052-109">İlke başvuru dizini</span><span class="sxs-lookup"><span data-stu-id="c9052-109">Policy reference index</span></span>
* <span data-ttu-id="c9052-110">[Erişimi kısıtlama ilkeleri][Access restriction policies]</span><span class="sxs-lookup"><span data-stu-id="c9052-110">[Access restriction policies][Access restriction policies]</span></span>
  * <span data-ttu-id="c9052-111">[Onay HTTP üstbilgisi] [ Check HTTP header] -varlığı ve/veya bir HTTP üstbilgisi değerini zorlar.</span><span class="sxs-lookup"><span data-stu-id="c9052-111">[Check HTTP header][Check HTTP header] - Enforces existence and/or value of a HTTP Header.</span></span>
  * <span data-ttu-id="c9052-112">[Abonelik tarafından çağrı hızını sınırla] [ Limit call rate by subscription] -engeller API kullanımı ani başına abonelik başına çağrı hızını sınırlayarak.</span><span class="sxs-lookup"><span data-stu-id="c9052-112">[Limit call rate by subscription][Limit call rate by subscription] - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>
  * <span data-ttu-id="c9052-113">[Anahtara göre çağrı hızını sınırla](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) -engeller API kullanımı ani başına anahtar başına çağrı hızını sınırlayarak.</span><span class="sxs-lookup"><span data-stu-id="c9052-113">[Limit call rate by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>
  * <span data-ttu-id="c9052-114">[Arayan IP'leri kısıtlamak] [ Restrict caller IPs] -filtreleri (verir/engellediği) çağrılarından belirli IP adreslerini ve/veya adres aralığı.</span><span class="sxs-lookup"><span data-stu-id="c9052-114">[Restrict caller IPs][Restrict caller IPs] - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>
  * <span data-ttu-id="c9052-115">[Abonelik tarafından kullanım kotası ayarla] [ Set usage quota by subscription] -bir abonelik başına temelinde tooenforce yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kotaya izin verir.</span><span class="sxs-lookup"><span data-stu-id="c9052-115">[Set usage quota by subscription][Set usage quota by subscription] - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>
  * <span data-ttu-id="c9052-116">[Anahtara göre kullanım kotası ayarla](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) -bir anahtar başına temelinde tooenforce yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kotaya izin verir.</span><span class="sxs-lookup"><span data-stu-id="c9052-116">[Set usage quota by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>
  * <span data-ttu-id="c9052-117">[JWT doğrulama] [ Validate JWT] -varlığı ve belirtilen bir HTTP üstbilgisi veya belirtilen sorgu parametresi ayıklanan JWT geçerliliğini zorlar.</span><span class="sxs-lookup"><span data-stu-id="c9052-117">[Validate JWT][Validate JWT] - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>
* <span data-ttu-id="c9052-118">[Gelişmiş ilkeleri][Advanced policies]</span><span class="sxs-lookup"><span data-stu-id="c9052-118">[Advanced policies][Advanced policies]</span></span>
  * <span data-ttu-id="c9052-119">[Denetim akışı] [ Control flow] - koşullu ilke deyimleri hello hello değerlendirme Boole sonuçlarına dayalı uygular [ifadeleri][expressions].</span><span class="sxs-lookup"><span data-stu-id="c9052-119">[Control flow][Control flow] - Conditionally applies policy statements based on hello results of hello evaluation of Boolean [expressions][expressions].</span></span>
  * <span data-ttu-id="c9052-120">[İstek] [ Forward request] -hello isteği toohello arka uç hizmeti iletir.</span><span class="sxs-lookup"><span data-stu-id="c9052-120">[Forward request][Forward request] - Forwards hello request toohello backend service.</span></span>
  * <span data-ttu-id="c9052-121">[TooEvent Hub oturum] [ Log tooEvent Hub] -hello belirtilen biçim tooa ileti hedefinde tarafından tanımlanan iletileri gönderen bir [Günlükçü](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) varlık.</span><span class="sxs-lookup"><span data-stu-id="c9052-121">[Log tooEvent Hub][Log tooEvent Hub] - Sends messages in hello specified format tooa message target defined by a [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entity.</span></span>
  * <span data-ttu-id="c9052-122">[Yeniden deneme](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) -hello yürütülmesi yeniden deneme içine ilke deyimleri varsa ve hello koşul yerine getirilene kadar.</span><span class="sxs-lookup"><span data-stu-id="c9052-122">[Retry](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="c9052-123">Yürütme yineleyin belirtilen zaman aralığı hello ve belirtilen toohello yeniden deneme sayısı.</span><span class="sxs-lookup"><span data-stu-id="c9052-123">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>
  * <span data-ttu-id="c9052-124">[Yanıt](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) -iptalleri ardışık düzen yürütmesi ve döndürür hello belirtilen yanıt doğrudan toohello çağıran.</span><span class="sxs-lookup"><span data-stu-id="c9052-124">[Return response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span>
  * <span data-ttu-id="c9052-125">[Tek yönlü İsteği Gönder](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) -bir istek toohello belirtilen URL için bir yanıt beklemeden gönderir.</span><span class="sxs-lookup"><span data-stu-id="c9052-125">[Send one way request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>
  * <span data-ttu-id="c9052-126">[İsteği Gönder](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) -bir istek toohello belirtilen URL gönderir.</span><span class="sxs-lookup"><span data-stu-id="c9052-126">[Send request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) - Sends a request toohello specified URL.</span></span>
  * <span data-ttu-id="c9052-127">[İstek yöntemini ayarla](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) -bir istek için toochange hello HTTP yöntemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="c9052-127">[Set request method](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>
  * <span data-ttu-id="c9052-128">[Durum Ayarla](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) -değişiklikleri hello HTTP durum kodu toohello belirtilen değeri.</span><span class="sxs-lookup"><span data-stu-id="c9052-128">[Set status](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>
  * <span data-ttu-id="c9052-129">[Değişken Ayarla] [ Set variable] -adlandırılmış bir değer kalıcı [bağlamı] [ context] sonraki erişim için değişken.</span><span class="sxs-lookup"><span data-stu-id="c9052-129">[Set variable][Set variable] - Persist a value in a named [context][context] variable for later access.</span></span>
  * <span data-ttu-id="c9052-130">[İzleme](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) -hello bir dize ekler [API denetçisi](api-management-howto-api-inspector.md) çıktı.</span><span class="sxs-lookup"><span data-stu-id="c9052-130">[Trace](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) - Adds a string into hello [API Inspector](api-management-howto-api-inspector.md) output.</span></span>
  * <span data-ttu-id="c9052-131">[Bekleyin](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - kapalı gönderme bekler isteği, önbelleğe alınan değer almak veya denetim akışı ilkeleri toocomplete devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="c9052-131">[Wait](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - Waits for enclosed Send request, Get value from cache, or Control flow policies toocomplete before proceeding.</span></span>
* <span data-ttu-id="c9052-132">[Kimlik doğrulama ilkeleri][Authentication policies]</span><span class="sxs-lookup"><span data-stu-id="c9052-132">[Authentication policies][Authentication policies]</span></span>
  * <span data-ttu-id="c9052-133">[Basic ile kimlik doğrulaması] [ Authenticate with Basic] -temel kimlik doğrulaması kullanarak arka uç hizmeti ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="c9052-133">[Authenticate with Basic][Authenticate with Basic] - Authenticate with a backend service using Basic authentication.</span></span>
  * <span data-ttu-id="c9052-134">[İstemci sertifikası ile kimlik doğrulaması] [ Authenticate with client certificate] -istemci sertifikalarını kullanan bir arka uç hizmeti ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="c9052-134">[Authenticate with client certificate][Authenticate with client certificate] - Authenticate with a backend service using client certificates.</span></span>
* <span data-ttu-id="c9052-135">[Önbelleğe alma ilkeleri][Caching policies]</span><span class="sxs-lookup"><span data-stu-id="c9052-135">[Caching policies][Caching policies]</span></span> 
  * <span data-ttu-id="c9052-136">[Önbellekten alma] [ Get from cache] -önbellek gerçekleştirmek aramak ve geçerli bir önbelleğe alınan yanıt kullanılabilir olduğunda döndürür.</span><span class="sxs-lookup"><span data-stu-id="c9052-136">[Get from cache][Get from cache] - Perform cache look up and return a valid cached response when available.</span></span>
  * <span data-ttu-id="c9052-137">[Depolama toocache] [ Store toocache] -toohello göre önbellekleri yanıt belirtilen önbellek denetimi yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="c9052-137">[Store toocache][Store toocache] - Caches response according toohello specified cache control configuration.</span></span>
  * <span data-ttu-id="c9052-138">[Önbelleğe alınan değer alma](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) -anahtar tarafından önbelleğe alınmış bir öğeyi geri almak.</span><span class="sxs-lookup"><span data-stu-id="c9052-138">[Get value from cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>
  * <span data-ttu-id="c9052-139">[Değer önbellekte depolamak](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -bir öğe anahtarı tarafından hello önbelleğine depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9052-139">[Store value in cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>
  * <span data-ttu-id="c9052-140">[Önbelleğe alınan değer Kaldır](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) -öğeyi hello önbelleğinde anahtarının kaldırmak.</span><span class="sxs-lookup"><span data-stu-id="c9052-140">[Remove value from cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>
* <span data-ttu-id="c9052-141">[Etki alanı ilkelerini arası][Cross domain policies]</span><span class="sxs-lookup"><span data-stu-id="c9052-141">[Cross domain policies][Cross domain policies]</span></span> 
  * <span data-ttu-id="c9052-142">[Etki alanları arası çağrılar izin] [ Allow cross-domain calls] -yapar hello API erişilebilir Microsoft Silverlight Adobe Flash ve tarayıcı tabanlı istemcilerden.</span><span class="sxs-lookup"><span data-stu-id="c9052-142">[Allow cross-domain calls][Allow cross-domain calls] - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>
  * <span data-ttu-id="c9052-143">[CORS] [ CORS] -çıkış noktaları arası kaynak paylaşımını (CORS) tooan işlemi destekler veya bir API tooallow etki alanları arası tarayıcı tabanlı istemcilerden çağıran ekler.</span><span class="sxs-lookup"><span data-stu-id="c9052-143">[CORS][CORS] - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>
  * <span data-ttu-id="c9052-144">[JSONP] [ JSONP] - JSON ile destek tooan işlemi (JSONP) doldurma ekler veya bir API tooallow etki alanları arası JavaScript tarayıcı tabanlı istemcilerden çağırır.</span><span class="sxs-lookup"><span data-stu-id="c9052-144">[JSONP][JSONP] - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>
* <span data-ttu-id="c9052-145">[Dönüştürme ilkelerini][Transformation policies]</span><span class="sxs-lookup"><span data-stu-id="c9052-145">[Transformation policies][Transformation policies]</span></span> 
  * <span data-ttu-id="c9052-146">[JSON tooXML Dönüştür] [ Convert JSON tooXML] - dönüştürür istek veya yanıt gövdesi JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="c9052-146">[Convert JSON tooXML][Convert JSON tooXML] - Converts request or response body from JSON tooXML.</span></span>
  * <span data-ttu-id="c9052-147">[XML tooJSON Dönüştür] [ Convert XML tooJSON] - dönüştürür istek veya yanıt gövdesi XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="c9052-147">[Convert XML tooJSON][Convert XML tooJSON] - Converts request or response body from XML tooJSON.</span></span>
  * <span data-ttu-id="c9052-148">[Bulma ve değiştirme dizesi gövdesi içinde] [ Find and replace string in body] - bir istek veya yanıt alt dizeyi bulur ve farklı bir dizeyle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="c9052-148">[Find and replace string in body][Find and replace string in body] - Finds a request or response substring and replaces it with a different substring.</span></span>
  * <span data-ttu-id="c9052-149">[İçeriği URL'leri maske] [ Mask URLs in content] -(maskeleri)'yeniden yazar bağlantılar hello yanıt gövdesi böylece hello ağ geçidi aracılığıyla toohello eşdeğer bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c9052-149">[Mask URLs in content][Mask URLs in content] - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>
  * <span data-ttu-id="c9052-150">[Arka uç hizmetini ayarlamak] [ Set backend service] -değişiklikleri hello arka uç hizmetine gelen bir istek için.</span><span class="sxs-lookup"><span data-stu-id="c9052-150">[Set backend service][Set backend service] - Changes hello backend service for an incoming request.</span></span>
  * <span data-ttu-id="c9052-151">[Gövde ayarlamak] [ Set body] -hello ileti gövdesi gelen ve giden istekleri için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c9052-151">[Set body][Set body] - Sets hello message body for incoming and outgoing requests.</span></span>
  * <span data-ttu-id="c9052-152">[HTTP üstbilgisi kümesi] [ Set HTTP header] - değer tooan varolan yanıt ve/veya istek üstbilgisi atar veya yeni bir yanıt ve/veya istek üstbilgisi ekler.</span><span class="sxs-lookup"><span data-stu-id="c9052-152">[Set HTTP header][Set HTTP header] - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>
  * <span data-ttu-id="c9052-153">[Sorgu dizesi parametresi kümesi] [ Set query string parameter] - ekler, değiştirir değerini veya istek sorgu dizesi parametresi siler.</span><span class="sxs-lookup"><span data-stu-id="c9052-153">[Set query string parameter][Set query string parameter] - Adds, replaces value of, or deletes request query string parameter.</span></span>
  * <span data-ttu-id="c9052-154">[URL yeniden yazma] [ Rewrite URL] -hello web hizmeti tarafından beklenen genel form toohello formundan bir istek URL'sini dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="c9052-154">[Rewrite URL][Rewrite URL] - Converts a request URL from its public form toohello form expected by hello web service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9052-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c9052-155">Next steps</span></span>
<span data-ttu-id="c9052-156">İlke ifadeleri hakkında daha fazla bilgi için aşağıdaki videoyu hello bakın.</span><span class="sxs-lookup"><span data-stu-id="c9052-156">For more information on policy expressions, see hello following video.</span></span>

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


