---
title: Azure API Management ilkeleri | Microsoft Docs
description: "Azure API Management'te kullanıma ilkeleri hakkında bilgi edinin."
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
ms.openlocfilehash: 485dc3a87a81dc67f5144596a30d498293d6b76a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-policies"></a><span data-ttu-id="b6ecd-103">API Management ilkeleri</span><span class="sxs-lookup"><span data-stu-id="b6ecd-103">API Management policies</span></span>
<span data-ttu-id="b6ecd-104">Bu bölümde aşağıdaki API Management ilkeleri bir başvuru sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-104">This section provides a reference for the following API Management policies.</span></span> <span data-ttu-id="b6ecd-105">Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="b6ecd-105">For information on adding and configuring policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
  
 <span data-ttu-id="b6ecd-106">Yapılandırma yoluyla API'nin davranışını değiştirmek yayımcının sisteminin güçlü bir özellik ilkelerdir.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-106">Policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="b6ecd-107">İstek üzerinde sırayla yürütülen deyimlerin bir koleksiyon veya bir API yanıtını ilkelerdir.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-107">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="b6ecd-108">Sık kullanılan deyimler, XML'den JSON biçimi dönüştürme içerir ve bir geliştiriciden gelen çağrıların miktarını sınırlamak için hız sınırı çağırın.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-108">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="b6ecd-109">Kutudan çıktığında çok daha fazla ilke kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-109">Many more policies are available out of the box.</span></span>  
  
 <span data-ttu-id="b6ecd-110">İlke ifadeleri herhangi bir API Management ilkesinde, ilke aksini belirtmedikçe, öznitelik değerleri ya da metin değerleri olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-110">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="b6ecd-111">[Akışı denetle](api-management-advanced-policies.md#choose) ve [Değişken ayarla](api-management-advanced-policies.md#set-variable) gibi bazı ilkeler ilke ifadelerini temel alır.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-111">Some policies such as the [Control flow](api-management-advanced-policies.md#choose) and [Set variable](api-management-advanced-policies.md#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="b6ecd-112">Daha fazla bilgi için bkz: [ilkeleri Gelişmiş](api-management-advanced-policies.md#AdvancedPolicies) ve [ilke ifadelerini](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="b6ecd-112">For more information, see [Advanced policies](api-management-advanced-policies.md#AdvancedPolicies) and [Policy expressions](api-management-policy-expressions.md).</span></span>  
  
##  <span data-ttu-id="b6ecd-113"><a name="ProxyPolicies"></a>İlkeleri</span><span class="sxs-lookup"><span data-stu-id="b6ecd-113"><a name="ProxyPolicies"></a> Policies</span></span>  
  
-   [<span data-ttu-id="b6ecd-114">Erişimi kısıtlama ilkeleri</span><span class="sxs-lookup"><span data-stu-id="b6ecd-114">Access restriction policies</span></span>](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   <span data-ttu-id="b6ecd-115">[Onay HTTP üstbilgisi](api-management-access-restriction-policies.md#CheckHTTPHeader) -varlığı ve/veya bir HTTP üstbilgisi değerini zorlar.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-115">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
    -   <span data-ttu-id="b6ecd-116">[Abonelik tarafından çağrı hızını sınırla](api-management-access-restriction-policies.md#LimitCallRate) -engeller API kullanımı ani başına abonelik başına çağrı hızını sınırlayarak.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-116">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="b6ecd-117">[Anahtara göre çağrı hızını sınırla](api-management-access-restriction-policies.md#LimitCallRateByKey) -engeller API kullanımı ani başına anahtar başına çağrı hızını sınırlayarak.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-117">[Limit call rate by key](api-management-access-restriction-policies.md#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="b6ecd-118">[Arayan IP'leri kısıtlamak](api-management-access-restriction-policies.md#RestrictCallerIPs) -filtreleri (verir/engellediği) çağrılarından belirli IP adreslerini ve/veya adres aralığı.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-118">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
    -   <span data-ttu-id="b6ecd-119">[Abonelik tarafından kullanım kotası ayarla](api-management-access-restriction-policies.md#SetUsageQuota) -yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kota, abonelik başına temelinde zorunlu tutmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-119">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="b6ecd-120">[Anahtara göre kullanım kotası ayarla](api-management-access-restriction-policies.md#SetUsageQuotaByKey) -yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kota anahtarı başına temelinde zorunlu tutmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-120">[Set usage quota by key](api-management-access-restriction-policies.md#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="b6ecd-121">[JWT doğrulama](api-management-access-restriction-policies.md#ValidateJWT) -varlığı ve belirtilen bir HTTP üstbilgisi veya belirtilen sorgu parametresi ayıklanan JWT geçerliliğini zorlar.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-121">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
-   [<span data-ttu-id="b6ecd-122">Gelişmiş ilkeler</span><span class="sxs-lookup"><span data-stu-id="b6ecd-122">Advanced policies</span></span>](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   <span data-ttu-id="b6ecd-123">[Denetim akışı](api-management-advanced-policies.md#choose) - koşullu ilke deyimleri Boole ifadeleri değerlendirmeye dayanarak uygular.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-123">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on the evaluation of Boolean expressions.</span></span>  
  
    -   <span data-ttu-id="b6ecd-124">[İstek](api-management-advanced-policies.md#ForwardRequest) -arka uç hizmetine isteği iletir.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-124">[Forward request](api-management-advanced-policies.md#ForwardRequest) - Forwards the request to the backend service.</span></span>  
  
    -   <span data-ttu-id="b6ecd-125">[Olay Hub'ına günlük](api-management-advanced-policies.md#log-to-eventhub) -gönderdiği iletileri belirtilen biçimde Günlükçü varlık tarafından tanımlanan bir ileti hedef.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-125">[Log to Event Hub](api-management-advanced-policies.md#log-to-eventhub) - Sends messages in the specified format to a message target defined by a Logger entity.</span></span>  
  
    -   <span data-ttu-id="b6ecd-126">[Yeniden deneme](api-management-advanced-policies.md#Retry) -değilse ve koşul yerine getirilene kadar iliştirilmiş ilke deyimleri yürütülmesi yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-126">[Retry](api-management-advanced-policies.md#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="b6ecd-127">Yürütme belirtilen zaman aralıklarında yineleyin ve belirtilen en fazla yeniden deneme sayısı.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-127">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>  
  
    -   <span data-ttu-id="b6ecd-128">[Yanıt](api-management-advanced-policies.md#ReturnResponse) -iptalleri potansiyel satış, yürütme ve doğrudan çağırana belirtilen yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-128">[Return response](api-management-advanced-policies.md#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span>  
  
    -   <span data-ttu-id="b6ecd-129">[Tek yönlü İsteği Gönder](api-management-advanced-policies.md#SendOneWayRequest) -bir istek için yanıt beklemeden belirtilen URL'ye gönderir.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-129">[Send one way request](api-management-advanced-policies.md#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>  
  
    -   <span data-ttu-id="b6ecd-130">[İsteği Gönder](api-management-advanced-policies.md#SendRequest) -belirtilen URL'ye bir isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-130">[Send request](api-management-advanced-policies.md#SendRequest) - Sends a request to the specified URL.</span></span>  
  
    -   <span data-ttu-id="b6ecd-131">[Değişken Ayarla](api-management-advanced-policies.md#set-variable) -adlandırılmış bağlamının sonraki erişim için bir değer kalır.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-131">[Set variable](api-management-advanced-policies.md#set-variable) - Persist a value in a named context variable for later access.</span></span>  
  
    -   <span data-ttu-id="b6ecd-132">[İstek yöntemini ayarla](api-management-advanced-policies.md#SetRequestMethod) -bir istek için HTTP yöntemini değiştirmenize izin verir.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-132">[Set request method](api-management-advanced-policies.md#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>  
  
    -   <span data-ttu-id="b6ecd-133">[Durum kodu ayarlamak](api-management-advanced-policies.md#SetStatus) -HTTP durum kodu için belirtilen değer değiştirir.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-133">[Set status code](api-management-advanced-policies.md#SetStatus) - Changes the HTTP status code to the specified value.</span></span>  
  
    -   <span data-ttu-id="b6ecd-134">[İzleme](api-management-advanced-policies.md#Trace) -bir dizeye ekler [API denetçisi](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) çıktı.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-134">[Trace](api-management-advanced-policies.md#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
    -   <span data-ttu-id="b6ecd-135">[Bekleyin](api-management-advanced-policies.md#Wait) -içine için bekleyeceği [gönderme isteği](api-management-advanced-policies.md#SendRequest), [değeri önbellekten alma](api-management-caching-policies.md#GetFromCacheByKey), veya [kontrol akışı](api-management-advanced-policies.md#choose) devam etmeden önce tamamlanmasını ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-135">[Wait](api-management-advanced-policies.md#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies to complete before proceeding.</span></span>  
  
-   [<span data-ttu-id="b6ecd-136">Kimlik doğrulama ilkeleri</span><span class="sxs-lookup"><span data-stu-id="b6ecd-136">Authentication policies</span></span>](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   <span data-ttu-id="b6ecd-137">[Basic ile kimlik doğrulaması](api-management-authentication-policies.md#Basic) -temel kimlik doğrulaması kullanarak arka uç hizmeti ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-137">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
    -   <span data-ttu-id="b6ecd-138">[İstemci sertifikası ile kimlik doğrulaması](api-management-authentication-policies.md#ClientCertificate) -istemci sertifikalarını kullanan bir arka uç hizmeti ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-138">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
-   [<span data-ttu-id="b6ecd-139">Önbelleğe alma ilkeleri</span><span class="sxs-lookup"><span data-stu-id="b6ecd-139">Caching policies</span></span>](api-management-caching-policies.md#CachingPolicies)  
  
    -   <span data-ttu-id="b6ecd-140">[Önbellekten alma](api-management-caching-policies.md#GetFromCache) -önbellek gerçekleştirmek aramak ve geçerli bir önbelleğe alınan yanıt kullanılabilir olduğunda döndürür.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-140">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached response when available.</span></span>  
  
    -   <span data-ttu-id="b6ecd-141">[Önbellek deposuna](api-management-caching-policies.md#StoreToCache) -belirtilen önbellek denetim yapılandırmasında göre yanıtı önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-141">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches response according to the specified cache control configuration.</span></span>  
  
    -   <span data-ttu-id="b6ecd-142">[Önbelleğe alınan değer alma](api-management-caching-policies.md#GetFromCacheByKey) -anahtar tarafından önbelleğe alınmış bir öğeyi geri almak.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-142">[Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="b6ecd-143">[Değer önbellekte depolamak](api-management-caching-policies.md#StoreToCacheByKey) -bir öğe anahtarı tarafından önbellekte depolamak.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-143">[Store value in cache](api-management-caching-policies.md#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="b6ecd-144">[Önbelleğe alınan değer kaldırmak](api-management-caching-policies.md#RemoveCacheByKey) -öğenin önbellekte anahtarının kaldırın.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-144">[Remove value from cache](api-management-caching-policies.md#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
-   [<span data-ttu-id="b6ecd-145">Çapraz etki alanı ilkeleri</span><span class="sxs-lookup"><span data-stu-id="b6ecd-145">Cross domain policies</span></span>](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   <span data-ttu-id="b6ecd-146">[Etki alanları arası çağrılar izin](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -API Adobe Flash ve Microsoft Silverlight tarayıcı tabanlı istemcilerden erişilebilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-146">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
    -   <span data-ttu-id="b6ecd-147">[CORS](api-management-cross-domain-policies.md#CORS) -çıkış noktaları arası kaynak paylaşımı (CORS) desteklemek için bir işlem veya tarayıcı tabanlı istemcilerden etki alanları arası çağrılarına izin vermek için bir API ekler.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-147">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
    -   <span data-ttu-id="b6ecd-148">[JSONP](api-management-cross-domain-policies.md#JSONP) -bir işlem veya tarayıcı tabanlı JavaScript istemcilerden etki alanları arası çağrılarına izin vermek için bir API (JSONP) doldurma desteğiyle JSON ekler.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
-   [<span data-ttu-id="b6ecd-149">Dönüştürme ilkeleri</span><span class="sxs-lookup"><span data-stu-id="b6ecd-149">Transformation policies</span></span>](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   <span data-ttu-id="b6ecd-150">[XML ve JSON Dönüştür](api-management-transformation-policies.md#ConvertJSONtoXML) - dönüştürür isteği veya yanıtı XML ve JSON öğesinden gövde.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-150">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span></span>  
  
    -   <span data-ttu-id="b6ecd-151">[XML JSON biçimine Dönüştür](api-management-transformation-policies.md#ConvertXMLtoJSON) - dönüştürür isteği veya yanıtı için JSON XML'den gövde.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-151">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span></span>  
  
    -   <span data-ttu-id="b6ecd-152">[Bulma ve değiştirme dizesi gövdesi içinde](api-management-transformation-policies.md#Findandreplacestringinbody) - bir istek veya yanıt alt dizeyi bulur ve farklı bir dizeyle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-152">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
    -   <span data-ttu-id="b6ecd-153">[İçeriği URL'leri maske](api-management-transformation-policies.md#MaskURLSContent) -yanıta bağlantı (maskeleri)'yeniden yazar gövde böylece bunlar ağ geçidi aracılığıyla eşdeğer bağlantı üzerine gelin.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-153">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>  
  
    -   <span data-ttu-id="b6ecd-154">[Arka uç hizmetini ayarlamak](api-management-transformation-policies.md#SetBackendService) -gelen bir istek için arka uç hizmeti değiştirir.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-154">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span></span>  
  
    -   <span data-ttu-id="b6ecd-155">[Gövde ayarlamak](api-management-transformation-policies.md#SetBody) -ileti gövdesi gelen ve giden istekleri için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-155">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span></span>  
  
    -   <span data-ttu-id="b6ecd-156">[HTTP üstbilgisi kümesi](api-management-transformation-policies.md#SetHTTPheader) - değer atayan bir varolan yanıt ve/veya istek üstbilgisi veya yeni bir yanıt ve/veya istek üstbilgisi ekler.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-156">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
    -   <span data-ttu-id="b6ecd-157">[Sorgu dizesi parametresi kümesi](api-management-transformation-policies.md#SetQueryStringParameter) - ekler, değiştirir değerini veya istek sorgu dizesi parametresi siler.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-157">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
    -   <span data-ttu-id="b6ecd-158">[URL yeniden yazma](api-management-transformation-policies.md#RewriteURL) -bir istek URL'sini ortak formundan web hizmeti tarafından beklenen biçime dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-158">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span></span>  
  
    -   <span data-ttu-id="b6ecd-159">[XSLT kullanarak XML dönüştürme](api-management-transformation-policies.md#XSLTransform) -XSL dönüşümü istek veya yanıt gövdesinde XML için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b6ecd-159">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="b6ecd-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b6ecd-160">Next steps</span></span>
<span data-ttu-id="b6ecd-161">İlkeleriyle çalışma daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="b6ecd-161">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
