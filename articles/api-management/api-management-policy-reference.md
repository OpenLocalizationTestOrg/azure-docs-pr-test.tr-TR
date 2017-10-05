---
title: "Azure API Management ilke başvurusu"
description: "API Management yapılandırmak amacıyla kullanılabilir ilkeleri hakkında bilgi edinin."
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
ms.openlocfilehash: adc0c4415e10ddd0b4994cecef17f026546e91a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-policy-reference"></a><span data-ttu-id="9715a-103">Azure API Management ilke başvurusu</span><span class="sxs-lookup"><span data-stu-id="9715a-103">Azure API Management Policy Reference</span></span>
<span data-ttu-id="9715a-104">Bu bölümde ilkelerinde dizin sağlayan [API Management ilke başvurusu][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="9715a-104">This section provides an index for the policies in the [API Management policy reference][API Management policy reference].</span></span> <span data-ttu-id="9715a-105">Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri][Policies in API Management].</span><span class="sxs-lookup"><span data-stu-id="9715a-105">For information on adding and configuring policies, see [Policies in API Management][Policies in API Management].</span></span>

<span data-ttu-id="9715a-106">İlke ifadeleri herhangi bir API Management ilkesinde, ilke aksini belirtmedikçe, öznitelik değerleri ya da metin değerleri olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9715a-106">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="9715a-107">Gibi bazı ilkeler [kontrol akışı] [ Control flow] ve [değişken Ayarla] [ Set variable] ilkeler ilke ifadelerini temel alarak.</span><span class="sxs-lookup"><span data-stu-id="9715a-107">Some policies such as the [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="9715a-108">Daha fazla bilgi için bkz: [ilkeleri Gelişmiş] [ Advanced policies] ve [ilke ifadeleri][Policy expressions]</span><span class="sxs-lookup"><span data-stu-id="9715a-108">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions]</span></span>

## <a name="policy-reference-index"></a><span data-ttu-id="9715a-109">İlke başvuru dizini</span><span class="sxs-lookup"><span data-stu-id="9715a-109">Policy reference index</span></span>
* <span data-ttu-id="9715a-110">[Erişimi kısıtlama ilkeleri][Access restriction policies]</span><span class="sxs-lookup"><span data-stu-id="9715a-110">[Access restriction policies][Access restriction policies]</span></span>
  * <span data-ttu-id="9715a-111">[Onay HTTP üstbilgisi] [ Check HTTP header] -varlığı ve/veya bir HTTP üstbilgisi değerini zorlar.</span><span class="sxs-lookup"><span data-stu-id="9715a-111">[Check HTTP header][Check HTTP header] - Enforces existence and/or value of a HTTP Header.</span></span>
  * <span data-ttu-id="9715a-112">[Abonelik tarafından çağrı hızını sınırla] [ Limit call rate by subscription] -engeller API kullanımı ani başına abonelik başına çağrı hızını sınırlayarak.</span><span class="sxs-lookup"><span data-stu-id="9715a-112">[Limit call rate by subscription][Limit call rate by subscription] - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>
  * <span data-ttu-id="9715a-113">[Anahtara göre çağrı hızını sınırla](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) -engeller API kullanımı ani başına anahtar başına çağrı hızını sınırlayarak.</span><span class="sxs-lookup"><span data-stu-id="9715a-113">[Limit call rate by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>
  * <span data-ttu-id="9715a-114">[Arayan IP'leri kısıtlamak] [ Restrict caller IPs] -filtreleri (verir/engellediği) çağrılarından belirli IP adreslerini ve/veya adres aralığı.</span><span class="sxs-lookup"><span data-stu-id="9715a-114">[Restrict caller IPs][Restrict caller IPs] - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>
  * <span data-ttu-id="9715a-115">[Abonelik tarafından kullanım kotası ayarla] [ Set usage quota by subscription] -yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kota, abonelik başına temelinde zorunlu tutmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="9715a-115">[Set usage quota by subscription][Set usage quota by subscription] - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>
  * <span data-ttu-id="9715a-116">[Anahtara göre kullanım kotası ayarla](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) -yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kota anahtarı başına temelinde zorunlu tutmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="9715a-116">[Set usage quota by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>
  * <span data-ttu-id="9715a-117">[JWT doğrulama] [ Validate JWT] -varlığı ve belirtilen bir HTTP üstbilgisi veya belirtilen sorgu parametresi ayıklanan JWT geçerliliğini zorlar.</span><span class="sxs-lookup"><span data-stu-id="9715a-117">[Validate JWT][Validate JWT] - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>
* <span data-ttu-id="9715a-118">[Gelişmiş ilkeleri][Advanced policies]</span><span class="sxs-lookup"><span data-stu-id="9715a-118">[Advanced policies][Advanced policies]</span></span>
  * <span data-ttu-id="9715a-119">[Denetim akışı] [ Control flow] - koşullu ilke deyimleri Boole değerlendirmesi sonuçlarına dayalı uygular [ifadeleri][expressions].</span><span class="sxs-lookup"><span data-stu-id="9715a-119">[Control flow][Control flow] - Conditionally applies policy statements based on the results of the evaluation of Boolean [expressions][expressions].</span></span>
  * <span data-ttu-id="9715a-120">[İstek] [ Forward request] -arka uç hizmetine isteği iletir.</span><span class="sxs-lookup"><span data-stu-id="9715a-120">[Forward request][Forward request] - Forwards the request to the backend service.</span></span>
  * <span data-ttu-id="9715a-121">[Olay Hub'ına günlük] [ Log to Event Hub] -gönderdiği iletileri belirtilen biçimde tarafından tanımlanan bir ileti hedef bir [Günlükçü](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) varlık.</span><span class="sxs-lookup"><span data-stu-id="9715a-121">[Log to Event Hub][Log to Event Hub] - Sends messages in the specified format to a message target defined by a [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entity.</span></span>
  * <span data-ttu-id="9715a-122">[Yeniden deneme](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) -değilse ve koşul yerine getirilene kadar iliştirilmiş ilke deyimleri yürütülmesi yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="9715a-122">[Retry](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="9715a-123">Yürütme belirtilen zaman aralıklarında yineleyin ve belirtilen en fazla yeniden deneme sayısı.</span><span class="sxs-lookup"><span data-stu-id="9715a-123">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>
  * <span data-ttu-id="9715a-124">[Yanıt](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) -iptalleri potansiyel satış, yürütme ve doğrudan çağırana belirtilen yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="9715a-124">[Return response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span>
  * <span data-ttu-id="9715a-125">[Tek yönlü İsteği Gönder](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) -bir istek için yanıt beklemeden belirtilen URL'ye gönderir.</span><span class="sxs-lookup"><span data-stu-id="9715a-125">[Send one way request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>
  * <span data-ttu-id="9715a-126">[İsteği Gönder](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) -belirtilen URL'ye bir isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="9715a-126">[Send request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) - Sends a request to the specified URL.</span></span>
  * <span data-ttu-id="9715a-127">[İstek yöntemini ayarla](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) -bir istek için HTTP yöntemini değiştirmenize izin verir.</span><span class="sxs-lookup"><span data-stu-id="9715a-127">[Set request method](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>
  * <span data-ttu-id="9715a-128">[Durum Ayarla](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) -HTTP durum kodu için belirtilen değer değiştirir.</span><span class="sxs-lookup"><span data-stu-id="9715a-128">[Set status](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) - Changes the HTTP status code to the specified value.</span></span>
  * <span data-ttu-id="9715a-129">[Değişken Ayarla] [ Set variable] -adlandırılmış bir değer kalıcı [bağlamı] [ context] sonraki erişim için değişken.</span><span class="sxs-lookup"><span data-stu-id="9715a-129">[Set variable][Set variable] - Persist a value in a named [context][context] variable for later access.</span></span>
  * <span data-ttu-id="9715a-130">[İzleme](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) -bir dizeye ekler [API denetçisi](api-management-howto-api-inspector.md) çıktı.</span><span class="sxs-lookup"><span data-stu-id="9715a-130">[Trace](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) - Adds a string into the [API Inspector](api-management-howto-api-inspector.md) output.</span></span>
  * <span data-ttu-id="9715a-131">[Bekleyin](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) -kapalı gönderme bekler, önbellek, Get değerinden istek veya denetim devam etmeden önce tamamlanmasını akış ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="9715a-131">[Wait](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - Waits for enclosed Send request, Get value from cache, or Control flow policies to complete before proceeding.</span></span>
* <span data-ttu-id="9715a-132">[Kimlik doğrulama ilkeleri][Authentication policies]</span><span class="sxs-lookup"><span data-stu-id="9715a-132">[Authentication policies][Authentication policies]</span></span>
  * <span data-ttu-id="9715a-133">[Basic ile kimlik doğrulaması] [ Authenticate with Basic] -temel kimlik doğrulaması kullanarak arka uç hizmeti ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="9715a-133">[Authenticate with Basic][Authenticate with Basic] - Authenticate with a backend service using Basic authentication.</span></span>
  * <span data-ttu-id="9715a-134">[İstemci sertifikası ile kimlik doğrulaması] [ Authenticate with client certificate] -istemci sertifikalarını kullanan bir arka uç hizmeti ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="9715a-134">[Authenticate with client certificate][Authenticate with client certificate] - Authenticate with a backend service using client certificates.</span></span>
* <span data-ttu-id="9715a-135">[Önbelleğe alma ilkeleri][Caching policies]</span><span class="sxs-lookup"><span data-stu-id="9715a-135">[Caching policies][Caching policies]</span></span> 
  * <span data-ttu-id="9715a-136">[Önbellekten alma] [ Get from cache] -önbellek gerçekleştirmek aramak ve geçerli bir önbelleğe alınan yanıt kullanılabilir olduğunda döndürür.</span><span class="sxs-lookup"><span data-stu-id="9715a-136">[Get from cache][Get from cache] - Perform cache look up and return a valid cached response when available.</span></span>
  * <span data-ttu-id="9715a-137">[Önbellek deposuna] [ Store to cache] -belirtilen önbellek denetim yapılandırmasında göre yanıtı önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="9715a-137">[Store to cache][Store to cache] - Caches response according to the specified cache control configuration.</span></span>
  * <span data-ttu-id="9715a-138">[Önbelleğe alınan değer alma](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) -anahtar tarafından önbelleğe alınmış bir öğeyi geri almak.</span><span class="sxs-lookup"><span data-stu-id="9715a-138">[Get value from cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>
  * <span data-ttu-id="9715a-139">[Değer önbellekte depolamak](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -bir öğe anahtarı tarafından önbellekte depolamak.</span><span class="sxs-lookup"><span data-stu-id="9715a-139">[Store value in cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) - Store an item in the cache by key.</span></span>
  * <span data-ttu-id="9715a-140">[Önbelleğe alınan değer kaldırmak](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) -öğenin önbellekte anahtarının kaldırın.</span><span class="sxs-lookup"><span data-stu-id="9715a-140">[Remove value from cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>
* <span data-ttu-id="9715a-141">[Etki alanı ilkelerini arası][Cross domain policies]</span><span class="sxs-lookup"><span data-stu-id="9715a-141">[Cross domain policies][Cross domain policies]</span></span> 
  * <span data-ttu-id="9715a-142">[Etki alanları arası çağrılar izin] [ Allow cross-domain calls] -API Adobe Flash ve Microsoft Silverlight tarayıcı tabanlı istemcilerden erişilebilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="9715a-142">[Allow cross-domain calls][Allow cross-domain calls] - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>
  * <span data-ttu-id="9715a-143">[CORS] [ CORS] -çıkış noktaları arası kaynak paylaşımı (CORS) desteklemek için bir işlem veya tarayıcı tabanlı istemcilerden etki alanları arası çağrılarına izin vermek için bir API ekler.</span><span class="sxs-lookup"><span data-stu-id="9715a-143">[CORS][CORS] - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>
  * <span data-ttu-id="9715a-144">[JSONP] [ JSONP] -bir işlem veya tarayıcı tabanlı JavaScript istemcilerden etki alanları arası çağrılarına izin vermek için bir API (JSONP) doldurma desteğiyle JSON ekler.</span><span class="sxs-lookup"><span data-stu-id="9715a-144">[JSONP][JSONP] - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>
* <span data-ttu-id="9715a-145">[Dönüştürme ilkelerini][Transformation policies]</span><span class="sxs-lookup"><span data-stu-id="9715a-145">[Transformation policies][Transformation policies]</span></span> 
  * <span data-ttu-id="9715a-146">[XML ve JSON Dönüştür] [ Convert JSON to XML] - dönüştürür isteği veya yanıtı XML ve JSON öğesinden gövde.</span><span class="sxs-lookup"><span data-stu-id="9715a-146">[Convert JSON to XML][Convert JSON to XML] - Converts request or response body from JSON to XML.</span></span>
  * <span data-ttu-id="9715a-147">[XML JSON biçimine Dönüştür] [ Convert XML to JSON] - dönüştürür isteği veya yanıtı için JSON XML'den gövde.</span><span class="sxs-lookup"><span data-stu-id="9715a-147">[Convert XML to JSON][Convert XML to JSON] - Converts request or response body from XML to JSON.</span></span>
  * <span data-ttu-id="9715a-148">[Bulma ve değiştirme dizesi gövdesi içinde] [ Find and replace string in body] - bir istek veya yanıt alt dizeyi bulur ve farklı bir dizeyle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="9715a-148">[Find and replace string in body][Find and replace string in body] - Finds a request or response substring and replaces it with a different substring.</span></span>
  * <span data-ttu-id="9715a-149">[İçeriği URL'leri maske] [ Mask URLs in content] -yanıta bağlantı (maskeleri)'yeniden yazar gövde böylece bunlar ağ geçidi aracılığıyla eşdeğer bağlantı üzerine gelin.</span><span class="sxs-lookup"><span data-stu-id="9715a-149">[Mask URLs in content][Mask URLs in content] - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>
  * <span data-ttu-id="9715a-150">[Arka uç hizmetini ayarlamak] [ Set backend service] -gelen bir istek için arka uç hizmeti değiştirir.</span><span class="sxs-lookup"><span data-stu-id="9715a-150">[Set backend service][Set backend service] - Changes the backend service for an incoming request.</span></span>
  * <span data-ttu-id="9715a-151">[Gövde ayarlamak] [ Set body] -ileti gövdesi gelen ve giden istekleri için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="9715a-151">[Set body][Set body] - Sets the message body for incoming and outgoing requests.</span></span>
  * <span data-ttu-id="9715a-152">[HTTP üstbilgisi kümesi] [ Set HTTP header] - değer atayan bir varolan yanıt ve/veya istek üstbilgisi veya yeni bir yanıt ve/veya istek üstbilgisi ekler.</span><span class="sxs-lookup"><span data-stu-id="9715a-152">[Set HTTP header][Set HTTP header] - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>
  * <span data-ttu-id="9715a-153">[Sorgu dizesi parametresi kümesi] [ Set query string parameter] - ekler, değiştirir değerini veya istek sorgu dizesi parametresi siler.</span><span class="sxs-lookup"><span data-stu-id="9715a-153">[Set query string parameter][Set query string parameter] - Adds, replaces value of, or deletes request query string parameter.</span></span>
  * <span data-ttu-id="9715a-154">[URL yeniden yazma] [ Rewrite URL] -bir istek URL'sini ortak formundan web hizmeti tarafından beklenen biçime dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="9715a-154">[Rewrite URL][Rewrite URL] - Converts a request URL from its public form to the form expected by the web service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9715a-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9715a-155">Next steps</span></span>
<span data-ttu-id="9715a-156">Aşağıdaki videoda İlkesi ifadeleri hakkında daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="9715a-156">For more information on policy expressions, see the following video.</span></span>

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
[Log to Event Hub]: https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub

[Authentication policies]: https://msdn.microsoft.com/library/azure/dn894079.aspx
[Authenticate with Basic]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#Basic
[Authenticate with client certificate]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#ClientCertificate
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx
[Get from cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#GetFromCache
[Store to cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#StoreToCache

[Cross domain policies]: https://msdn.microsoft.com/library/azure/dn894084.aspx
[Allow cross-domain calls]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#AllowCrossDomainCalls
[CORS]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#CORS
[JSONP]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#JSONP

[Transformation policies]: https://msdn.microsoft.com/library/azure/dn894083.aspx
[Convert JSON to XML]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertJSONtoXML
[Convert XML to JSON]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertXMLtoJSON
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


