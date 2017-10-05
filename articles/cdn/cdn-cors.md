---
title: CORS'yi Azure CDN kullanarak | Microsoft Docs
description: "Azure içerik teslim ağı (CDN) için çıkış noktaları arası kaynak paylaşımı (CORS) ile kullanmayı öğrenin."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 86740a96-4269-4060-aba3-a69f00e6f14e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 7070397f6e69b21add75bad8220f0b8ebe36d266
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-cdn-with-cors"></a><span data-ttu-id="d8a25-103">CORS'yi Azure CDN kullanma</span><span class="sxs-lookup"><span data-stu-id="d8a25-103">Using Azure CDN with CORS</span></span>
## <a name="what-is-cors"></a><span data-ttu-id="d8a25-104">CORS nedir?</span><span class="sxs-lookup"><span data-stu-id="d8a25-104">What is CORS?</span></span>
<span data-ttu-id="d8a25-105">CORS (arası kaynak kaynak paylaşımı) başka bir etki alanındaki kaynaklara erişmek bir etki alanında çalışan bir web uygulaması sağlayan bir HTTP özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="d8a25-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain to access resources in another domain.</span></span> <span data-ttu-id="d8a25-106">Siteler arası komut dosyası saldırıları olasılığını azaltmak için tüm modern web tarayıcıları olarak bilinen bir güvenlik kısıtlama uygulamak [kaynak aynı ilke](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span><span class="sxs-lookup"><span data-stu-id="d8a25-106">In order to reduce the possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span></span>  <span data-ttu-id="d8a25-107">Bu arama API'ları farklı bir etki alanındaki bir web sayfasından önler.</span><span class="sxs-lookup"><span data-stu-id="d8a25-107">This prevents a web page from calling APIs in a different domain.</span></span>  <span data-ttu-id="d8a25-108">CORS içinde başka bir kaynak API'leri çağırmak bir kaynak (kaynak etki alanı) izin vermek için güvenli bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8a25-108">CORS provides a secure way to allow one origin (the origin domain) to call APIs in another origin.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="d8a25-109">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="d8a25-109">How it works</span></span>
<span data-ttu-id="d8a25-110">CORS isteklerini, iki tür vardır *basit istekleri* ve *karmaşık istekleri.*</span><span class="sxs-lookup"><span data-stu-id="d8a25-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span></span>

### <a name="for-simple-requests"></a><span data-ttu-id="d8a25-111">Basit istekleri için:</span><span class="sxs-lookup"><span data-stu-id="d8a25-111">For simple requests:</span></span>

1. <span data-ttu-id="d8a25-112">CORS istekle ek bir tarayıcı gönderir **kaynak** HTTP isteği üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="d8a25-112">The browser sends the CORS request with an additional **Origin** HTTP request header.</span></span> <span data-ttu-id="d8a25-113">Bu üst bileşimi tanımlanır ana sayfa hizmet başlangıç değeri *protokolü,* *etki alanı,* ve *bağlantı noktası.*</span><span class="sxs-lookup"><span data-stu-id="d8a25-113">The value of this header is the origin that served the parent page, which is defined as the combination of *protocol,* *domain,* and *port.*</span></span>  <span data-ttu-id="d8a25-114">Https://www.contoso.com sayfasından fabrikam.com kaynak kullanıcının verileri erişmeye çalıştığında, aşağıdaki istek üstbilgisi fabrikam.com olarak gönderilir:</span><span class="sxs-lookup"><span data-stu-id="d8a25-114">When a page from https://www.contoso.com attempts to access a user's data in the fabrikam.com origin, the following request header would be sent to fabrikam.com:</span></span>

   `Origin: https://www.contoso.com`

2. <span data-ttu-id="d8a25-115">Sunucusu aşağıdakilerden herhangi biri ile yanıt verebilir:</span><span class="sxs-lookup"><span data-stu-id="d8a25-115">The server may respond with any of the following:</span></span>

   * <span data-ttu-id="d8a25-116">Bir **Access-Control-Allow-Origin** hangi kaynak site izin verilen gösteren yanıt üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="d8a25-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span></span> <span data-ttu-id="d8a25-117">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d8a25-117">For example:</span></span>

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * <span data-ttu-id="d8a25-118">Sunucu çıkış noktaları arası istek kaynak üst bilgisini denetledikten sonra izin vermiyorsa 403 gibi bir HTTP hata kodu</span><span class="sxs-lookup"><span data-stu-id="d8a25-118">An HTTP error code such as 403 if the server does not allow the cross-origin request after checking the Origin header</span></span>

   * <span data-ttu-id="d8a25-119">Bir **Access-Control-Allow-Origin** tüm kaynaklara izin veren bir joker karakter üstbilgiyle:</span><span class="sxs-lookup"><span data-stu-id="d8a25-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span></span>

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a><span data-ttu-id="d8a25-120">Karmaşık istekleri için:</span><span class="sxs-lookup"><span data-stu-id="d8a25-120">For complex requests:</span></span>

<span data-ttu-id="d8a25-121">Karmaşık bir CORS istek göndermek için tarayıcı burada gereken istektir bir *denetim öncesi isteği* (yani ön bir araştırma) fiili CORS isteğini göndermeden önce.</span><span class="sxs-lookup"><span data-stu-id="d8a25-121">A complex request is a CORS request where the browser is required to send a *preflight request* (i.e. a preliminary probe) before sending the actual CORS request.</span></span> <span data-ttu-id="d8a25-122">Denetim öncesi isteği özgün CORS devam edebilirsiniz ve olduğundan isteği sunucu izni soran bir `OPTIONS` aynı URL'ye isteği.</span><span class="sxs-lookup"><span data-stu-id="d8a25-122">The preflight request asks the server permission if the original CORS request can proceed and is an `OPTIONS` request to the same URL.</span></span>

> [!TIP]
> <span data-ttu-id="d8a25-123">CORS akışları ve ortak Tuzaklar hakkında daha fazla ayrıntı için görüntülemek [REST API'leri için CORS kılavuza](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span><span class="sxs-lookup"><span data-stu-id="d8a25-123">For more details on CORS flows and common pitfalls, view the [Guide to CORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span></span>
>
>

## <a name="wildcard-or-single-origin-scenarios"></a><span data-ttu-id="d8a25-124">Joker karakter ya da tek kaynak senaryoları</span><span class="sxs-lookup"><span data-stu-id="d8a25-124">Wildcard or single origin scenarios</span></span>
<span data-ttu-id="d8a25-125">CORS'yi Azure CDN üzerinde ek bir yapılandırma olmadan otomatik olarak çalışır, **Access-Control-Allow-Origin** üstbilgi joker karakter (*) veya tek bir kaynak olarak ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="d8a25-125">CORS on Azure CDN will work automatically with no additional configuration when the **Access-Control-Allow-Origin** header is set to wildcard (*) or a single origin.</span></span>  <span data-ttu-id="d8a25-126">CDN ilk yanıtı önbelleğe alır ve sonraki istekleri aynı başlığını kullanır.</span><span class="sxs-lookup"><span data-stu-id="d8a25-126">The CDN will cache the first response and subsequent requests will use the same header.</span></span>

<span data-ttu-id="d8a25-127">İstek zaten ile CDN üzerinde ayarlanan CORS önce yapılmışsa içerik ile yeniden yüklemek için uç nokta içeriğinizi içeriği temizlenecek gerekir, kaynak **Access-Control-Allow-Origin** üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="d8a25-127">If requests have already been made to the CDN prior to CORS being set on the your origin, you will need to purge content on your endpoint content to reload the content with the **Access-Control-Allow-Origin** header.</span></span>

## <a name="multiple-origin-scenarios"></a><span data-ttu-id="d8a25-128">Birden çok kaynak senaryoları</span><span class="sxs-lookup"><span data-stu-id="d8a25-128">Multiple origin scenarios</span></span>
<span data-ttu-id="d8a25-129">Belirli bir listesi için CORS izin verilecek çıkış noktaları yer izin vermeniz gerekiyorsa, biraz daha karmaşık işlerinizi.</span><span class="sxs-lookup"><span data-stu-id="d8a25-129">If you need to allow a specific list of origins to be allowed for CORS, things get a little more complicated.</span></span> <span data-ttu-id="d8a25-130">CDN önbelleğe sorun oluşur **Access-Control-Allow-Origin** ilk CORS çıkış üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="d8a25-130">The problem occurs when the CDN caches the **Access-Control-Allow-Origin** header for the first CORS origin.</span></span>  <span data-ttu-id="d8a25-131">Farklı bir CORS kaynaktan bir sonraki istekte bulunduğunda CDN önbelleğe alınan hizmet **Access-Control-Allow-Origin** eşleşmeyecektir üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="d8a25-131">When a different CORS origin makes a subsequent request, the CDN will serve the cached **Access-Control-Allow-Origin** header, which won't match.</span></span>  <span data-ttu-id="d8a25-132">Bu sorunu gidermek için birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="d8a25-132">There are several ways to correct this.</span></span>

### <a name="azure-cdn-premium-from-verizon"></a><span data-ttu-id="d8a25-133">Verizon’dan Azure CDN Premium</span><span class="sxs-lookup"><span data-stu-id="d8a25-133">Azure CDN Premium from Verizon</span></span>
<span data-ttu-id="d8a25-134">Bu ayarı etkinleştirmek için en iyi yolu kullanmaktır **verizon'dan Azure CDN Premium**, gelişmiş işlevselliği, bazı kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="d8a25-134">The best way to enable this is to use **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span></span> 

<span data-ttu-id="d8a25-135">Gerekir [bir kural oluşturmak](cdn-rules-engine.md) denetlemek için **kaynak** isteği üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="d8a25-135">You'll need to [create a rule](cdn-rules-engine.md) to check the **Origin** header on the request.</span></span>  <span data-ttu-id="d8a25-136">Geçerli bir kaynak varsa, kural ayarlar **Access-Control-Allow-Origin** üstbilgi isteğinde sağlanan kaynağına sahip.</span><span class="sxs-lookup"><span data-stu-id="d8a25-136">If it's a valid origin, your rule will set the **Access-Control-Allow-Origin** header with the origin provided in the request.</span></span>  <span data-ttu-id="d8a25-137">Kaynak olarak belirtilmişse **kaynak** üstbilgi izin verilmez, kuralınız atlayın **Access-Control-Allow-Origin** isteğini reddetmek tarayıcı neden olacak üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="d8a25-137">If the origin specified in the **Origin** header is not allowed, your rule should omit the **Access-Control-Allow-Origin** header which will cause the browser to reject the request.</span></span> 

<span data-ttu-id="d8a25-138">Bu kurallar altyapısı ile yapmak için iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="d8a25-138">There are two ways to do this with the rules engine.</span></span>  <span data-ttu-id="d8a25-139">Her iki durumda da **Access-Control-Allow-Origin** dosyanın kaynak sunucu başlığından tamamen göz ardı, CDN'ın kurallar altyapısı tamamen izin verilen CORS çıkış noktası yönetir.</span><span class="sxs-lookup"><span data-stu-id="d8a25-139">In both cases, the **Access-Control-Allow-Origin** header from the file's origin server is completely ignored, the CDN's rules engine completely manages the allowed CORS origins.</span></span>

#### <a name="one-regular-expression-with-all-valid-origins"></a><span data-ttu-id="d8a25-140">Tüm geçerli kaynaklara sahip bir normal ifade</span><span class="sxs-lookup"><span data-stu-id="d8a25-140">One regular expression with all valid origins</span></span>
<span data-ttu-id="d8a25-141">Bu durumda, tüm izin vermek istediğiniz kaynakları içerir normal bir ifade oluşturmanız:</span><span class="sxs-lookup"><span data-stu-id="d8a25-141">In this case, you'll create a regular expression that includes all of the origins you want to allow:</span></span> 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> <span data-ttu-id="d8a25-142">**Verizon'dan Azure CDN** kullanan [Perl uyumlu normal ifadeler](http://pcre.org/) normal ifadeler için kendi altyapısı olarak bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="d8a25-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span></span>  <span data-ttu-id="d8a25-143">Gibi bir araç kullanabilirsiniz [normal ifadeler 101](https://regex101.com/) normal ifade doğrulanacak.</span><span class="sxs-lookup"><span data-stu-id="d8a25-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) to validate your regular expression.</span></span>  <span data-ttu-id="d8a25-144">"/" Karakterini normal ifadelerde geçerli olduğundan ve kaçış gerekmez, ancak bu karakteri kaçış en iyi yöntem olarak kabul edilir ve bazı regex doğrulayıcıları tarafından beklenen olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d8a25-144">Note that the "/" character is valid in regular expressions and doesn't need to be escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span></span>
> 
> 

<span data-ttu-id="d8a25-145">Normal ifadeyle eşleşen, kuralınız değiştirir **Access-Control-Allow-Origin** başlığından (varsa) kaynağa isteği gönderen kaynağına sahip.</span><span class="sxs-lookup"><span data-stu-id="d8a25-145">If the regular expression matches, your rule will replace the **Access-Control-Allow-Origin** header (if any) from the origin with the origin that sent the request.</span></span>  <span data-ttu-id="d8a25-146">Ek CORS üstbilgilerini gibi ekleyebilirsiniz **erişim-denetim-Allow-Methods**.</span><span class="sxs-lookup"><span data-stu-id="d8a25-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span></span>

![Normal ifade ile kurallar örneği](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a><span data-ttu-id="d8a25-148">Her kaynak için istek üstbilgisi kuralı.</span><span class="sxs-lookup"><span data-stu-id="d8a25-148">Request header rule for each origin.</span></span>
<span data-ttu-id="d8a25-149">Normal ifadeler yerine, bunun yerine kullanarak izin vermek istediğiniz her kaynak için ayrı bir kural oluşturabileceğiniz **istek üstbilgisi joker** [eşleşen koşulu](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="d8a25-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish to allow using the **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span></span> <span data-ttu-id="d8a25-150">Normal ifade yöntemiyle olduğu gibi tek başına kurallar altyapısı CORS üstbilgilerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d8a25-150">As with the regular expression method, the rules engine alone sets the CORS headers.</span></span> 

![Normal ifade olmadan kuralları örneği](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> <span data-ttu-id="d8a25-152">Joker karakter kullanımı yukarıdaki örnekte * hem HTTP hem de HTTPS eşleştirmek için kurallar altyapısı söyler.</span><span class="sxs-lookup"><span data-stu-id="d8a25-152">In the example above, the use of the wildcard character * tells the rules engine to match both HTTP and HTTPS.</span></span>
> 
> 

### <a name="azure-cdn-standard"></a><span data-ttu-id="d8a25-153">Azure CDN standart</span><span class="sxs-lookup"><span data-stu-id="d8a25-153">Azure CDN Standard</span></span>
<span data-ttu-id="d8a25-154">Azure CDN standart profilleri, birden çok çıkış joker kaynak kullanımı için izin vermek için tek mekanizması kullanmaktır [sorgu dizesi önbelleğe alma](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="d8a25-154">On Azure CDN Standard profiles, the only mechanism to allow for multiple origins without the use of the wildcard origin is to use [query string caching](cdn-query-string.md).</span></span>  <span data-ttu-id="d8a25-155">CDN uç noktası için sorgu dizesi ayarı etkinleştirmek ve izin verilen her etki alanı gelen istekleri için bir benzersiz sorgu dizesi kullanmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8a25-155">You need to enable query string setting for the CDN endpoint and then use a unique query string for requests from each allowed domain.</span></span> <span data-ttu-id="d8a25-156">Bunun yapılması her benzersiz sorgu dizesi için ayrı bir nesne önbelleği CDN neden olur.</span><span class="sxs-lookup"><span data-stu-id="d8a25-156">Doing this will result in the CDN caching a separate object for each unique query string.</span></span> <span data-ttu-id="d8a25-157">Bu yaklaşım ancak ideal, değil gibi birden çok kopyası üzerinde CDN önbelleğe aynı dosya sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="d8a25-157">This approach is not ideal, however, as it will result in multiple copies of the same file cached on the CDN.</span></span>  

