---
title: aaaUsing CORS ile Azure CDN | Microsoft Docs
description: "Nasıl toouse hello Azure içerik teslim ağı (CDN) toowith çıkış noktaları arası kaynak paylaşımı (CORS) hakkında bilgi edinin."
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
ms.openlocfilehash: 6c743b56c32a2d3aacc9a77094cb87d61b95d2f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-cdn-with-cors"></a><span data-ttu-id="75c80-103">CORS'yi Azure CDN kullanma</span><span class="sxs-lookup"><span data-stu-id="75c80-103">Using Azure CDN with CORS</span></span>
## <a name="what-is-cors"></a><span data-ttu-id="75c80-104">CORS nedir?</span><span class="sxs-lookup"><span data-stu-id="75c80-104">What is CORS?</span></span>
<span data-ttu-id="75c80-105">CORS (arası kaynak kaynak paylaşımı) altında bir etki alanı tooaccess kaynakları başka bir etki alanında çalışan bir web uygulaması sağlayan bir HTTP özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="75c80-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain tooaccess resources in another domain.</span></span> <span data-ttu-id="75c80-106">Sipariş tooreduce hello olasılığını siteler arası komut dosyası saldırıları içinde tüm modern web tarayıcıları olarak bilinen bir güvenlik kısıtlama uygulamak [kaynak aynı ilke](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span><span class="sxs-lookup"><span data-stu-id="75c80-106">In order tooreduce hello possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span></span>  <span data-ttu-id="75c80-107">Bu arama API'ları farklı bir etki alanındaki bir web sayfasından önler.</span><span class="sxs-lookup"><span data-stu-id="75c80-107">This prevents a web page from calling APIs in a different domain.</span></span>  <span data-ttu-id="75c80-108">CORS bir güvenli şekilde tooallow bir kaynağı (Merhaba kaynak etki alanı) toocall API'leri başka bir kaynak olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="75c80-108">CORS provides a secure way tooallow one origin (hello origin domain) toocall APIs in another origin.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="75c80-109">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="75c80-109">How it works</span></span>
<span data-ttu-id="75c80-110">CORS isteklerini, iki tür vardır *basit istekleri* ve *karmaşık istekleri.*</span><span class="sxs-lookup"><span data-stu-id="75c80-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span></span>

### <a name="for-simple-requests"></a><span data-ttu-id="75c80-111">Basit istekleri için:</span><span class="sxs-lookup"><span data-stu-id="75c80-111">For simple requests:</span></span>

1. <span data-ttu-id="75c80-112">Merhaba tarayıcı gönderir hello CORS istekle ek bir **kaynak** HTTP isteği üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="75c80-112">hello browser sends hello CORS request with an additional **Origin** HTTP request header.</span></span> <span data-ttu-id="75c80-113">Merhaba Bu üstbilgi değeri hello birleşimi tanımlanan hello üst sayfa sunulan hello kaynak *protokolü,* *etki alanı,* ve *bağlantı noktası.*</span><span class="sxs-lookup"><span data-stu-id="75c80-113">hello value of this header is hello origin that served hello parent page, which is defined as hello combination of *protocol,* *domain,* and *port.*</span></span>  <span data-ttu-id="75c80-114">Https://www.contoso.com sayfasından hello fabrikam.com kaynak kullanıcının verileri tooaccess çalıştığında, istek üstbilgisi aşağıdaki hello toofabrikam.com gönderilir:</span><span class="sxs-lookup"><span data-stu-id="75c80-114">When a page from https://www.contoso.com attempts tooaccess a user's data in hello fabrikam.com origin, hello following request header would be sent toofabrikam.com:</span></span>

   `Origin: https://www.contoso.com`

2. <span data-ttu-id="75c80-115">Merhaba sunucusu aşağıdakilerden herhangi birini hello ile yanıt verebilir:</span><span class="sxs-lookup"><span data-stu-id="75c80-115">hello server may respond with any of hello following:</span></span>

   * <span data-ttu-id="75c80-116">Bir **Access-Control-Allow-Origin** hangi kaynak site izin verilen gösteren yanıt üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="75c80-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span></span> <span data-ttu-id="75c80-117">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="75c80-117">For example:</span></span>

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * <span data-ttu-id="75c80-118">Bir HTTP hata kodu 403 gibi hello sunucu hello çıkış noktaları arası istek hello kaynak üstbilgisi denetledikten sonra izin vermiyorsa</span><span class="sxs-lookup"><span data-stu-id="75c80-118">An HTTP error code such as 403 if hello server does not allow hello cross-origin request after checking hello Origin header</span></span>

   * <span data-ttu-id="75c80-119">Bir **Access-Control-Allow-Origin** tüm kaynaklara izin veren bir joker karakter üstbilgiyle:</span><span class="sxs-lookup"><span data-stu-id="75c80-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span></span>

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a><span data-ttu-id="75c80-120">Karmaşık istekleri için:</span><span class="sxs-lookup"><span data-stu-id="75c80-120">For complex requests:</span></span>

<span data-ttu-id="75c80-121">Karmaşık bir istek CORS istek hello tarayıcı gerekli toosend olduğu bir *denetim öncesi isteği* (yani ön bir araştırma) hello fiili CORS isteğini göndermeden önce.</span><span class="sxs-lookup"><span data-stu-id="75c80-121">A complex request is a CORS request where hello browser is required toosend a *preflight request* (i.e. a preliminary probe) before sending hello actual CORS request.</span></span> <span data-ttu-id="75c80-122">Merhaba denetim öncesi isteği hello sunucu izni hello özgün CORS isteğini devam edebilirsiniz ve olup olmadığını soran bir `OPTIONS` toohello isteği aynı URL.</span><span class="sxs-lookup"><span data-stu-id="75c80-122">hello preflight request asks hello server permission if hello original CORS request can proceed and is an `OPTIONS` request toohello same URL.</span></span>

> [!TIP]
> <span data-ttu-id="75c80-123">CORS akışları ve ortak Tuzaklar hakkında daha fazla ayrıntı için hello görüntülemek [tooCORS için REST API'leri Kılavuzu](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span><span class="sxs-lookup"><span data-stu-id="75c80-123">For more details on CORS flows and common pitfalls, view hello [Guide tooCORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span></span>
>
>

## <a name="wildcard-or-single-origin-scenarios"></a><span data-ttu-id="75c80-124">Joker karakter ya da tek kaynak senaryoları</span><span class="sxs-lookup"><span data-stu-id="75c80-124">Wildcard or single origin scenarios</span></span>
<span data-ttu-id="75c80-125">CORS'yi Azure CDN üzerinde ek bir yapılandırma olmadan hello olduğunda otomatik olarak çalışır **Access-Control-Allow-Origin** toowildcard (*) veya tek bir kaynak üstbilgisi ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="75c80-125">CORS on Azure CDN will work automatically with no additional configuration when hello **Access-Control-Allow-Origin** header is set toowildcard (*) or a single origin.</span></span>  <span data-ttu-id="75c80-126">Merhaba CDN önbelleğe alınması hello ilk yanıt ve sonraki istekleri hello kullanacağınız aynı üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="75c80-126">hello CDN will cache hello first response and subsequent requests will use hello same header.</span></span>

<span data-ttu-id="75c80-127">İstekleri toohello CDN önceki tooCORS üzerinde hello kaynağınıza ayarlanan yapılmışsa, toopurge içerik, uç nokta içerik tooreload hello hello ile içerik ihtiyacınız olacak **Access-Control-Allow-Origin** üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="75c80-127">If requests have already been made toohello CDN prior tooCORS being set on hello your origin, you will need toopurge content on your endpoint content tooreload hello content with hello **Access-Control-Allow-Origin** header.</span></span>

## <a name="multiple-origin-scenarios"></a><span data-ttu-id="75c80-128">Birden çok kaynak senaryoları</span><span class="sxs-lookup"><span data-stu-id="75c80-128">Multiple origin scenarios</span></span>
<span data-ttu-id="75c80-129">Tooallow belirli CORS için izin verilen çıkış noktası toobe listesini gerekiyorsa, biraz daha karmaşık işlerinizi.</span><span class="sxs-lookup"><span data-stu-id="75c80-129">If you need tooallow a specific list of origins toobe allowed for CORS, things get a little more complicated.</span></span> <span data-ttu-id="75c80-130">Merhaba sorun oluşuyor hello CDN hello önbelleğe **Access-Control-Allow-Origin** hello ilk CORS çıkış üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="75c80-130">hello problem occurs when hello CDN caches hello **Access-Control-Allow-Origin** header for hello first CORS origin.</span></span>  <span data-ttu-id="75c80-131">Farklı bir CORS kaynaktan bir sonraki istekte bulunduğunda hello CDN önbelleğe hello görecek **Access-Control-Allow-Origin** eşleşmeyecektir üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="75c80-131">When a different CORS origin makes a subsequent request, hello CDN will serve hello cached **Access-Control-Allow-Origin** header, which won't match.</span></span>  <span data-ttu-id="75c80-132">Vardır birkaç yolu toocorrect bu.</span><span class="sxs-lookup"><span data-stu-id="75c80-132">There are several ways toocorrect this.</span></span>

### <a name="azure-cdn-premium-from-verizon"></a><span data-ttu-id="75c80-133">Verizon’dan Azure CDN Premium</span><span class="sxs-lookup"><span data-stu-id="75c80-133">Azure CDN Premium from Verizon</span></span>
<span data-ttu-id="75c80-134">en iyi şekilde tooenable hello toouse budur **verizon'dan Azure CDN Premium**, gelişmiş işlevselliği, bazı kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="75c80-134">hello best way tooenable this is toouse **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span></span> 

<span data-ttu-id="75c80-135">Çok gerekir[bir kural oluşturmak](cdn-rules-engine.md) toocheck hello **kaynak** hello isteği üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="75c80-135">You'll need too[create a rule](cdn-rules-engine.md) toocheck hello **Origin** header on hello request.</span></span>  <span data-ttu-id="75c80-136">Geçerli bir kaynak varsa, kural hello ayarlar **Access-Control-Allow-Origin** üstbilgi hello isteğinde sağlanan hello kaynağına sahip.</span><span class="sxs-lookup"><span data-stu-id="75c80-136">If it's a valid origin, your rule will set hello **Access-Control-Allow-Origin** header with hello origin provided in hello request.</span></span>  <span data-ttu-id="75c80-137">Merhaba kaynak hello belirtilmişse **kaynak** üstbilgi izin verilmez, kuralınız hello atlayın **Access-Control-Allow-Origin** hello tarayıcı tooreject hello isteğini neden olacak üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="75c80-137">If hello origin specified in hello **Origin** header is not allowed, your rule should omit hello **Access-Control-Allow-Origin** header which will cause hello browser tooreject hello request.</span></span> 

<span data-ttu-id="75c80-138">Vardır iki yolu toodo bu hello kurallar altyapısı ile.</span><span class="sxs-lookup"><span data-stu-id="75c80-138">There are two ways toodo this with hello rules engine.</span></span>  <span data-ttu-id="75c80-139">Her iki durumda da hello **Access-Control-Allow-Origin** hello dosyanın kaynak sunucu başlığından tamamen göz ardı, hello CDN'ın kurallar altyapısı tamamen CORS çıkış noktası izin verilen hello yönetir.</span><span class="sxs-lookup"><span data-stu-id="75c80-139">In both cases, hello **Access-Control-Allow-Origin** header from hello file's origin server is completely ignored, hello CDN's rules engine completely manages hello allowed CORS origins.</span></span>

#### <a name="one-regular-expression-with-all-valid-origins"></a><span data-ttu-id="75c80-140">Tüm geçerli kaynaklara sahip bir normal ifade</span><span class="sxs-lookup"><span data-stu-id="75c80-140">One regular expression with all valid origins</span></span>
<span data-ttu-id="75c80-141">Bu durumda, tüm hello kaynakları içeren bir normal ifade oluşturacaksınız tooallow istiyor:</span><span class="sxs-lookup"><span data-stu-id="75c80-141">In this case, you'll create a regular expression that includes all of hello origins you want tooallow:</span></span> 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> <span data-ttu-id="75c80-142">**Verizon'dan Azure CDN** kullanan [Perl uyumlu normal ifadeler](http://pcre.org/) normal ifadeler için kendi altyapısı olarak bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="75c80-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span></span>  <span data-ttu-id="75c80-143">Gibi bir araç kullanabilirsiniz [normal ifadeler 101](https://regex101.com/) toovalidate, normal ifade.</span><span class="sxs-lookup"><span data-stu-id="75c80-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) toovalidate your regular expression.</span></span>  <span data-ttu-id="75c80-144">Merhaba "/" karakterini unutmayın normal ifadelerde geçerli değil ve kaçışlı toobe gerek yoktur, ancak bu karakteri kaçış ve en iyi yöntem olarak kabul edilir bazı regex doğrulayıcıları tarafından beklenen.</span><span class="sxs-lookup"><span data-stu-id="75c80-144">Note that hello "/" character is valid in regular expressions and doesn't need toobe escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span></span>
> 
> 

<span data-ttu-id="75c80-145">Merhaba normal ifadeyle eşleşen, kuralınız hello değiştirir **Access-Control-Allow-Origin** hello isteği gönderen hello kaynağına sahip hello kaynaktan üstbilgi (varsa).</span><span class="sxs-lookup"><span data-stu-id="75c80-145">If hello regular expression matches, your rule will replace hello **Access-Control-Allow-Origin** header (if any) from hello origin with hello origin that sent hello request.</span></span>  <span data-ttu-id="75c80-146">Ek CORS üstbilgilerini gibi ekleyebilirsiniz **erişim-denetim-Allow-Methods**.</span><span class="sxs-lookup"><span data-stu-id="75c80-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span></span>

![Normal ifade ile kurallar örneği](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a><span data-ttu-id="75c80-148">Her kaynak için istek üstbilgisi kuralı.</span><span class="sxs-lookup"><span data-stu-id="75c80-148">Request header rule for each origin.</span></span>
<span data-ttu-id="75c80-149">Normal ifadeler yerine, bunun yerine ayrı bir oluşturabileceğiniz hello kullanarak tooallow istediğiniz her kaynak için kural **istek üstbilgisi joker** [eşleşen koşulu](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="75c80-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish tooallow using hello **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span></span> <span data-ttu-id="75c80-150">Hello normal ifade yöntemiyle olarak tek başına kümeleri hello CORS üstbilgilerini hello kurallar altyapısı.</span><span class="sxs-lookup"><span data-stu-id="75c80-150">As with hello regular expression method, hello rules engine alone sets hello CORS headers.</span></span> 

![Normal ifade olmadan kuralları örneği](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> <span data-ttu-id="75c80-152">Merhaba yukarıdaki örnekte, hello joker karakter kullanımı hello * hello kurallar altyapısı toomatch söyler hem HTTP hem de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="75c80-152">In hello example above, hello use of hello wildcard character * tells hello rules engine toomatch both HTTP and HTTPS.</span></span>
> 
> 

### <a name="azure-cdn-standard"></a><span data-ttu-id="75c80-153">Azure CDN standart</span><span class="sxs-lookup"><span data-stu-id="75c80-153">Azure CDN Standard</span></span>
<span data-ttu-id="75c80-154">Toouse mekanizması tooallow hello joker kaynak hello kullanmadan birden çok kaynaklar için yalnızca Azure CDN standart profilleri hello [sorgu dizesi önbelleğe alma](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="75c80-154">On Azure CDN Standard profiles, hello only mechanism tooallow for multiple origins without hello use of hello wildcard origin is toouse [query string caching](cdn-query-string.md).</span></span>  <span data-ttu-id="75c80-155">İzin verilen her etki alanı gelen istekleri için bir benzersiz sorgu dizesi kullanın ve tooenable sorgu dizesi ayarı hello CDN uç noktası için gerekir.</span><span class="sxs-lookup"><span data-stu-id="75c80-155">You need tooenable query string setting for hello CDN endpoint and then use a unique query string for requests from each allowed domain.</span></span> <span data-ttu-id="75c80-156">Bunun yapılması hello her benzersiz sorgu dizesi için ayrı bir nesne önbelleği CDN neden olur.</span><span class="sxs-lookup"><span data-stu-id="75c80-156">Doing this will result in hello CDN caching a separate object for each unique query string.</span></span> <span data-ttu-id="75c80-157">Bu yaklaşım uygun değildir, ancak aynı dosyayı önbelleğe alınmış hello CDN hello birden çok kopyasını neden.</span><span class="sxs-lookup"><span data-stu-id="75c80-157">This approach is not ideal, however, as it will result in multiple copies of hello same file cached on hello CDN.</span></span>  

