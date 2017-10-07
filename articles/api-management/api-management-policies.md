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
# <a name="api-management-policies"></a><span data-ttu-id="c3798-103">API Management ilkeleri</span><span class="sxs-lookup"><span data-stu-id="c3798-103">API Management policies</span></span>
<span data-ttu-id="c3798-104">Bu bölümde API Management ilkelere hello için bir başvuru sağlar.</span><span class="sxs-lookup"><span data-stu-id="c3798-104">This section provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="c3798-105">Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="c3798-105">For information on adding and configuring policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
  
 <span data-ttu-id="c3798-106">Güçlü bir özellik toochange hello davranışını yapılandırma yoluyla hello API hello publisher izin hello sisteminin ilkelerdir.</span><span class="sxs-lookup"><span data-stu-id="c3798-106">Policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="c3798-107">Merhaba istek üzerinde sırayla yürütülen deyimlerin bir koleksiyon veya bir API yanıtını ilkelerdir.</span><span class="sxs-lookup"><span data-stu-id="c3798-107">Policies are a collection of Statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="c3798-108">Sık kullanılan deyimler XML tooJSON biçimi dönüştürme içerir ve bir geliştiriciden gelen çağrıların toorestrict hello miktarını sınırlamak oranı çağırın.</span><span class="sxs-lookup"><span data-stu-id="c3798-108">Popular Statements include format conversion from XML tooJSON and call rate limiting toorestrict hello amount of incoming calls from a developer.</span></span> <span data-ttu-id="c3798-109">Çok daha fazla ilke hello kutu dışı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c3798-109">Many more policies are available out of hello box.</span></span>  
  
 <span data-ttu-id="c3798-110">Merhaba ilke aksini belirtmedikçe ilke ifadelerini öznitelik değerleri ya da metin değerleri hello API Management ilkeleri olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c3798-110">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="c3798-111">Hello gibi bazı ilkeler [kontrol akışı](api-management-advanced-policies.md#choose) ve [değişken Ayarla](api-management-advanced-policies.md#set-variable) ilkeler ilke ifadelerini temel alarak.</span><span class="sxs-lookup"><span data-stu-id="c3798-111">Some policies such as hello [Control flow](api-management-advanced-policies.md#choose) and [Set variable](api-management-advanced-policies.md#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="c3798-112">Daha fazla bilgi için bkz: [ilkeleri Gelişmiş](api-management-advanced-policies.md#AdvancedPolicies) ve [ilke ifadelerini](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="c3798-112">For more information, see [Advanced policies](api-management-advanced-policies.md#AdvancedPolicies) and [Policy expressions](api-management-policy-expressions.md).</span></span>  
  
##  <span data-ttu-id="c3798-113"><a name="ProxyPolicies"></a>İlkeleri</span><span class="sxs-lookup"><span data-stu-id="c3798-113"><a name="ProxyPolicies"></a> Policies</span></span>  
  
-   [<span data-ttu-id="c3798-114">Erişimi kısıtlama ilkeleri</span><span class="sxs-lookup"><span data-stu-id="c3798-114">Access restriction policies</span></span>](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   <span data-ttu-id="c3798-115">[Onay HTTP üstbilgisi](api-management-access-restriction-policies.md#CheckHTTPHeader) -varlığı ve/veya bir HTTP üstbilgisi değerini zorlar.</span><span class="sxs-lookup"><span data-stu-id="c3798-115">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
    -   <span data-ttu-id="c3798-116">[Abonelik tarafından çağrı hızını sınırla](api-management-access-restriction-policies.md#LimitCallRate) -engeller API kullanımı ani başına abonelik başına çağrı hızını sınırlayarak.</span><span class="sxs-lookup"><span data-stu-id="c3798-116">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="c3798-117">[Anahtara göre çağrı hızını sınırla](api-management-access-restriction-policies.md#LimitCallRateByKey) -engeller API kullanımı ani başına anahtar başına çağrı hızını sınırlayarak.</span><span class="sxs-lookup"><span data-stu-id="c3798-117">[Limit call rate by key](api-management-access-restriction-policies.md#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="c3798-118">[Arayan IP'leri kısıtlamak](api-management-access-restriction-policies.md#RestrictCallerIPs) -filtreleri (verir/engellediği) çağrılarından belirli IP adreslerini ve/veya adres aralığı.</span><span class="sxs-lookup"><span data-stu-id="c3798-118">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
    -   <span data-ttu-id="c3798-119">[Abonelik tarafından kullanım kotası ayarla](api-management-access-restriction-policies.md#SetUsageQuota) -bir abonelik başına temelinde tooenforce yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kotaya izin verir.</span><span class="sxs-lookup"><span data-stu-id="c3798-119">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="c3798-120">[Anahtara göre kullanım kotası ayarla](api-management-access-restriction-policies.md#SetUsageQuotaByKey) -bir anahtar başına temelinde tooenforce yenilenebilir veya ömrü çağrısı birim ve/veya bant genişliği kotaya izin verir.</span><span class="sxs-lookup"><span data-stu-id="c3798-120">[Set usage quota by key](api-management-access-restriction-policies.md#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="c3798-121">[JWT doğrulama](api-management-access-restriction-policies.md#ValidateJWT) -varlığı ve belirtilen bir HTTP üstbilgisi veya belirtilen sorgu parametresi ayıklanan JWT geçerliliğini zorlar.</span><span class="sxs-lookup"><span data-stu-id="c3798-121">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
-   [<span data-ttu-id="c3798-122">Gelişmiş ilkeler</span><span class="sxs-lookup"><span data-stu-id="c3798-122">Advanced policies</span></span>](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   <span data-ttu-id="c3798-123">[Denetim akışı](api-management-advanced-policies.md#choose) - koşullu ilke deyimleri Boole ifadeleri hello değerlendirmesine göre uygulanır.</span><span class="sxs-lookup"><span data-stu-id="c3798-123">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on hello evaluation of Boolean expressions.</span></span>  
  
    -   <span data-ttu-id="c3798-124">[İstek](api-management-advanced-policies.md#ForwardRequest) -hello isteği toohello arka uç hizmeti iletir.</span><span class="sxs-lookup"><span data-stu-id="c3798-124">[Forward request](api-management-advanced-policies.md#ForwardRequest) - Forwards hello request toohello backend service.</span></span>  
  
    -   <span data-ttu-id="c3798-125">[TooEvent Hub oturum](api-management-advanced-policies.md#log-to-eventhub) -hello belirtilen biçim tooa ileti hedefinde Günlükçü varlık tarafından tanımlanan iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="c3798-125">[Log tooEvent Hub](api-management-advanced-policies.md#log-to-eventhub) - Sends messages in hello specified format tooa message target defined by a Logger entity.</span></span>  
  
    -   <span data-ttu-id="c3798-126">[Yeniden deneme](api-management-advanced-policies.md#Retry) -hello yürütülmesi yeniden deneme içine ilke deyimleri varsa ve hello koşul yerine getirilene kadar.</span><span class="sxs-lookup"><span data-stu-id="c3798-126">[Retry](api-management-advanced-policies.md#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="c3798-127">Yürütme yineleyin belirtilen zaman aralığı hello ve belirtilen toohello yeniden deneme sayısı.</span><span class="sxs-lookup"><span data-stu-id="c3798-127">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>  
  
    -   <span data-ttu-id="c3798-128">[Yanıt](api-management-advanced-policies.md#ReturnResponse) -iptalleri ardışık düzen yürütmesi ve döndürür hello belirtilen yanıt doğrudan toohello çağıran.</span><span class="sxs-lookup"><span data-stu-id="c3798-128">[Return response](api-management-advanced-policies.md#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span>  
  
    -   <span data-ttu-id="c3798-129">[Tek yönlü İsteği Gönder](api-management-advanced-policies.md#SendOneWayRequest) -bir istek toohello belirtilen URL için bir yanıt beklemeden gönderir.</span><span class="sxs-lookup"><span data-stu-id="c3798-129">[Send one way request](api-management-advanced-policies.md#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>  
  
    -   <span data-ttu-id="c3798-130">[İsteği Gönder](api-management-advanced-policies.md#SendRequest) -bir istek toohello belirtilen URL gönderir.</span><span class="sxs-lookup"><span data-stu-id="c3798-130">[Send request](api-management-advanced-policies.md#SendRequest) - Sends a request toohello specified URL.</span></span>  
  
    -   <span data-ttu-id="c3798-131">[Değişken Ayarla](api-management-advanced-policies.md#set-variable) -adlandırılmış bağlamının sonraki erişim için bir değer kalır.</span><span class="sxs-lookup"><span data-stu-id="c3798-131">[Set variable](api-management-advanced-policies.md#set-variable) - Persist a value in a named context variable for later access.</span></span>  
  
    -   <span data-ttu-id="c3798-132">[İstek yöntemini ayarla](api-management-advanced-policies.md#SetRequestMethod) -bir istek için toochange hello HTTP yöntemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="c3798-132">[Set request method](api-management-advanced-policies.md#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>  
  
    -   <span data-ttu-id="c3798-133">[Durum kodu ayarlamak](api-management-advanced-policies.md#SetStatus) -değişiklikleri hello HTTP durum kodu toohello belirtilen değeri.</span><span class="sxs-lookup"><span data-stu-id="c3798-133">[Set status code](api-management-advanced-policies.md#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>  
  
    -   <span data-ttu-id="c3798-134">[İzleme](api-management-advanced-policies.md#Trace) -hello bir dize ekler [API denetçisi](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) çıktı.</span><span class="sxs-lookup"><span data-stu-id="c3798-134">[Trace](api-management-advanced-policies.md#Trace) - Adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
    -   <span data-ttu-id="c3798-135">[Bekleyin](api-management-advanced-policies.md#Wait) -içine için bekleyeceği [gönderme isteği](api-management-advanced-policies.md#SendRequest), [değeri önbellekten alma](api-management-caching-policies.md#GetFromCacheByKey), veya [kontrol akışı](api-management-advanced-policies.md#choose) ilkeleri toocomplete devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="c3798-135">[Wait](api-management-advanced-policies.md#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies toocomplete before proceeding.</span></span>  
  
-   [<span data-ttu-id="c3798-136">Kimlik doğrulama ilkeleri</span><span class="sxs-lookup"><span data-stu-id="c3798-136">Authentication policies</span></span>](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   <span data-ttu-id="c3798-137">[Basic ile kimlik doğrulaması](api-management-authentication-policies.md#Basic) -temel kimlik doğrulaması kullanarak arka uç hizmeti ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="c3798-137">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
    -   <span data-ttu-id="c3798-138">[İstemci sertifikası ile kimlik doğrulaması](api-management-authentication-policies.md#ClientCertificate) -istemci sertifikalarını kullanan bir arka uç hizmeti ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="c3798-138">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
-   [<span data-ttu-id="c3798-139">Önbelleğe alma ilkeleri</span><span class="sxs-lookup"><span data-stu-id="c3798-139">Caching policies</span></span>](api-management-caching-policies.md#CachingPolicies)  
  
    -   <span data-ttu-id="c3798-140">[Önbellekten alma](api-management-caching-policies.md#GetFromCache) -önbellek gerçekleştirmek aramak ve geçerli bir önbelleğe alınan yanıt kullanılabilir olduğunda döndürür.</span><span class="sxs-lookup"><span data-stu-id="c3798-140">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached response when available.</span></span>  
  
    -   <span data-ttu-id="c3798-141">[Depolama toocache](api-management-caching-policies.md#StoreToCache) -toohello göre önbellekleri yanıt belirtilen önbellek denetimi yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="c3798-141">[Store toocache](api-management-caching-policies.md#StoreToCache) - Caches response according toohello specified cache control configuration.</span></span>  
  
    -   <span data-ttu-id="c3798-142">[Önbelleğe alınan değer alma](api-management-caching-policies.md#GetFromCacheByKey) -anahtar tarafından önbelleğe alınmış bir öğeyi geri almak.</span><span class="sxs-lookup"><span data-stu-id="c3798-142">[Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="c3798-143">[Değer önbellekte depolamak](api-management-caching-policies.md#StoreToCacheByKey) -bir öğe anahtarı tarafından hello önbelleğine depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3798-143">[Store value in cache](api-management-caching-policies.md#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>  
  
    -   <span data-ttu-id="c3798-144">[Önbelleğe alınan değer Kaldır](api-management-caching-policies.md#RemoveCacheByKey) -öğeyi hello önbelleğinde anahtarının kaldırmak.</span><span class="sxs-lookup"><span data-stu-id="c3798-144">[Remove value from cache](api-management-caching-policies.md#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>  
  
-   [<span data-ttu-id="c3798-145">Çapraz etki alanı ilkeleri</span><span class="sxs-lookup"><span data-stu-id="c3798-145">Cross domain policies</span></span>](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   <span data-ttu-id="c3798-146">[Etki alanları arası çağrılar izin](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -yapar hello API erişilebilir Microsoft Silverlight Adobe Flash ve tarayıcı tabanlı istemcilerden.</span><span class="sxs-lookup"><span data-stu-id="c3798-146">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
    -   <span data-ttu-id="c3798-147">[CORS](api-management-cross-domain-policies.md#CORS) -çıkış noktaları arası kaynak paylaşımını (CORS) tooan işlemi destekler veya bir API tooallow etki alanları arası tarayıcı tabanlı istemcilerden çağıran ekler.</span><span class="sxs-lookup"><span data-stu-id="c3798-147">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
    -   <span data-ttu-id="c3798-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - JSON ile destek tooan işlemi (JSONP) doldurma ekler veya bir API tooallow etki alanları arası JavaScript tarayıcı tabanlı istemcilerden çağırır.</span><span class="sxs-lookup"><span data-stu-id="c3798-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
-   [<span data-ttu-id="c3798-149">Dönüştürme ilkeleri</span><span class="sxs-lookup"><span data-stu-id="c3798-149">Transformation policies</span></span>](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   <span data-ttu-id="c3798-150">[JSON tooXML Dönüştür](api-management-transformation-policies.md#ConvertJSONtoXML) - dönüştürür istek veya yanıt gövdesi JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="c3798-150">[Convert JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON tooXML.</span></span>  
  
    -   <span data-ttu-id="c3798-151">[XML tooJSON Dönüştür](api-management-transformation-policies.md#ConvertXMLtoJSON) - dönüştürür istek veya yanıt gövdesi XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="c3798-151">[Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML tooJSON.</span></span>  
  
    -   <span data-ttu-id="c3798-152">[Bulma ve değiştirme dizesi gövdesi içinde](api-management-transformation-policies.md#Findandreplacestringinbody) - bir istek veya yanıt alt dizeyi bulur ve farklı bir dizeyle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="c3798-152">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
    -   <span data-ttu-id="c3798-153">[İçeriği URL'leri maske](api-management-transformation-policies.md#MaskURLSContent) -(maskeleri)'yeniden yazar bağlantılar hello yanıt gövdesi böylece hello ağ geçidi aracılığıyla toohello eşdeğer bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c3798-153">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>  
  
    -   <span data-ttu-id="c3798-154">[Arka uç hizmetini ayarlamak](api-management-transformation-policies.md#SetBackendService) -değişiklikleri hello arka uç hizmetine gelen bir istek için.</span><span class="sxs-lookup"><span data-stu-id="c3798-154">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes hello backend service for an incoming request.</span></span>  
  
    -   <span data-ttu-id="c3798-155">[Gövde ayarlamak](api-management-transformation-policies.md#SetBody) -hello ileti gövdesi gelen ve giden istekleri için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c3798-155">[Set body](api-management-transformation-policies.md#SetBody) - Sets hello message body for incoming and outgoing requests.</span></span>  
  
    -   <span data-ttu-id="c3798-156">[HTTP üstbilgisi kümesi](api-management-transformation-policies.md#SetHTTPheader) - değer tooan varolan yanıt ve/veya istek üstbilgisi atar veya yeni bir yanıt ve/veya istek üstbilgisi ekler.</span><span class="sxs-lookup"><span data-stu-id="c3798-156">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
    -   <span data-ttu-id="c3798-157">[Sorgu dizesi parametresi kümesi](api-management-transformation-policies.md#SetQueryStringParameter) - ekler, değiştirir değerini veya istek sorgu dizesi parametresi siler.</span><span class="sxs-lookup"><span data-stu-id="c3798-157">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
    -   <span data-ttu-id="c3798-158">[URL yeniden yazma](api-management-transformation-policies.md#RewriteURL) -hello web hizmeti tarafından beklenen genel form toohello formundan bir istek URL'sini dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="c3798-158">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form toohello form expected by hello web service.</span></span>  
  
    -   <span data-ttu-id="c3798-159">[XSLT kullanarak XML dönüştürme](api-management-transformation-policies.md#XSLTransform) -bir XSL Dönüştürme tooXML hello istek veya yanıt gövdesi içinde geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="c3798-159">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="c3798-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c3798-160">Next steps</span></span>
<span data-ttu-id="c3798-161">İlkeleriyle çalışma daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="c3798-161">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
