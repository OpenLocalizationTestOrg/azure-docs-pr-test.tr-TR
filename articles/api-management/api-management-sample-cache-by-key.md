---
title: "Azure API Management'te aaaCustom önbelleğe alma"
description: "Azure API Management'te anahtarı tarafından nasıl toocache öğelerini öğrenin"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 772bc8dd-5cda-41c4-95bf-b9f6f052bc85
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 681380743c8c96af5d0a8e25948a8c0663e9fd35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="f392d-103">Azure API Management'te özel önbelleğe alma</span><span class="sxs-lookup"><span data-stu-id="f392d-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="f392d-104">Azure API Management hizmeti için yerleşik destek sahip [HTTP yanıt önbelleğe alma](api-management-howto-cache.md) hello kaynak URL hello anahtar olarak kullanma.</span><span class="sxs-lookup"><span data-stu-id="f392d-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using hello resource URL as hello key.</span></span> <span data-ttu-id="f392d-105">Merhaba anahtar hello kullanarak istek üstbilgileri tarafından değiştirilebilir `vary-by` özellikleri.</span><span class="sxs-lookup"><span data-stu-id="f392d-105">hello key can be modified by request headers using hello `vary-by` properties.</span></span> <span data-ttu-id="f392d-106">Tüm HTTP yanıtlarını (diğer adıyla Beyanları) önbelleğe alma işlemi için kullanışlıdır ancak bazen yararlı toojust önbellek temsili bir bölümü olabilir.</span><span class="sxs-lookup"><span data-stu-id="f392d-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful toojust cache a portion of a representation.</span></span> <span data-ttu-id="f392d-107">Merhaba yeni [önbellek arama değeri](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) ve [önbellek deposu değeri](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) ilkeler ilke tanımları içindeki verileri toostore ve alma rasgele parçalarını hello olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="f392d-107">hello new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide hello ability toostore and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="f392d-108">Bu yeteneği de daha önce eklenen değer toohello ekler [gönderme isteği](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) İlkesi çünkü dış hizmetler yanıtlarının şimdi önbelleğe alabilir.</span><span class="sxs-lookup"><span data-stu-id="f392d-108">This ability also adds value toohello previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="f392d-109">Mimari</span><span class="sxs-lookup"><span data-stu-id="f392d-109">Architecture</span></span>
<span data-ttu-id="f392d-110">API Management hizmeti kullanan bir kiracı başına paylaşılan veri önbelleği toomultiple birimler ölçeklendirmenize göre erişim toohello hala alırsınız böylece aynı verileri önbelleğe.</span><span class="sxs-lookup"><span data-stu-id="f392d-110">API Management service uses a shared per-tenant data cache so that, as you scale up toomultiple units you will still get access toohello same cached data.</span></span> <span data-ttu-id="f392d-111">Ancak, bölgeli dağıtımı ile çalışırken, her hello bölgelerinin bağımsız önbellekleri vardır.</span><span class="sxs-lookup"><span data-stu-id="f392d-111">However, when working with a multi-region deployment there are independent caches within each of hello regions.</span></span> <span data-ttu-id="f392d-112">Son toothis, onu önemlidir toonot hello önbellek hello yalnızca kaynak bilgileri parçasının olduğu bir veri deposu olarak ele alın.</span><span class="sxs-lookup"><span data-stu-id="f392d-112">Due toothis, it is important toonot treat hello cache as a data store, where it is hello only source of some piece of information.</span></span> <span data-ttu-id="f392d-113">Vermedi ve daha sonra hello bölgeli dağıtım tootake avantajlarından karar, seyahat kullanıcılar müşterilerle erişim önbelleğe toothat veri kaybedebilir.</span><span class="sxs-lookup"><span data-stu-id="f392d-113">If you did, and later decided tootake advantage of hello multi-region deployment, then customers with users that travel may lose access toothat cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="f392d-114">Parça önbelleğe alma</span><span class="sxs-lookup"><span data-stu-id="f392d-114">Fragment caching</span></span>
<span data-ttu-id="f392d-115">Burada verilen yanıtları pahalı toodetermine ve makul bir süre için henüz yeni kalan verileri kısmı içeren bazı durumlar vardır.</span><span class="sxs-lookup"><span data-stu-id="f392d-115">There are certain cases where responses being returned contain some portion of data that is expensive toodetermine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="f392d-116">Örnek olarak, Uçuş Rezervasyonları, uçuş durumu ile ilgili bilgi sağlayan bir uçak tarafından oluşturulmuş bir hizmeti kullanmayı düşünün. Merhaba kullanıcı hello airlines noktaları program üyesi ise, bunlar tootheir geçerli durumu ve toplanan mesafe ilgili bilgileri de gerekir.</span><span class="sxs-lookup"><span data-stu-id="f392d-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If hello user is a member of hello airlines points program, they would also have information relating tootheir current status and mileage accumulated.</span></span> <span data-ttu-id="f392d-117">Bu kullanıcı ile ilgili bilgiler farklı depolanabilir, ancak uçuş durumu ve ayırmaları hakkında yanıtlarındaki döndürdüğü arzu tooinclude olabilir.</span><span class="sxs-lookup"><span data-stu-id="f392d-117">This user-related information might be stored in a different system, but it may be desirable tooinclude it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="f392d-118">Bu yapılabilir parça önbelleğe alma adlı bir işlem kullanılarak.</span><span class="sxs-lookup"><span data-stu-id="f392d-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="f392d-119">Merhaba birincil gösterimi hello kullanıcıyla ilişkili bilgileri eklenen toobe olduğu belirteci tooindicate çeşit kullanılarak hello kaynak sunucudan döndürülebilir.</span><span class="sxs-lookup"><span data-stu-id="f392d-119">hello primary representation can be returned from hello origin server using some kind of token tooindicate where hello user-related information is toobe inserted.</span></span> 

<span data-ttu-id="f392d-120">Arka uç API yanıtından JSON aşağıdaki hello göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="f392d-120">Consider hello following JSON response from a backend API.</span></span>

```json
{
  "airline" : "Air Canada",
  "flightno" : "871",
  "status" : "ontime",
  "gate" : "B40",
  "terminal" : "2A",
  "userprofile" : "$userprofile$"
}  
```

<span data-ttu-id="f392d-121">Ve ikincil kaynakta `/userprofile/{userid}` olduğunu gibi görünüyor,</span><span class="sxs-lookup"><span data-stu-id="f392d-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="f392d-122">Sipariş toodetermine hello uygun kullanıcı bilgileri tooinclude içinde hello son kullanıcıdan tooidentify gerekir.</span><span class="sxs-lookup"><span data-stu-id="f392d-122">In order toodetermine hello appropriate user information tooinclude, we need tooidentify who hello end user is.</span></span> <span data-ttu-id="f392d-123">Bu mekanizma bağımlı uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="f392d-123">This mechanism is implementation dependent.</span></span> <span data-ttu-id="f392d-124">Örnek olarak, hello kullanıyorum `Subject` , talep bir `JWT` belirteci.</span><span class="sxs-lookup"><span data-stu-id="f392d-124">As an example, I am using hello `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="f392d-125">Bu depolarız `enduserid` daha sonra kullanmak için bir bağlam değişken değeri.</span><span class="sxs-lookup"><span data-stu-id="f392d-125">We store this `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="f392d-126">önceki bir istek varsa zaten hello kullanıcı bilgileri alınır ve hello önbellekte depolanan hello sonraki toodetermine adımdır.</span><span class="sxs-lookup"><span data-stu-id="f392d-126">hello next step is toodetermine if a previous request has already retrieved hello user information and stored it in hello cache.</span></span> <span data-ttu-id="f392d-127">Merhaba bu için kullandığımız `cache-lookup-value` ilkesi.</span><span class="sxs-lookup"><span data-stu-id="f392d-127">For this we use hello `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="f392d-128">Toohello anahtar değeri ve ardından Hayır karşılık gelen hello önbelleğinde girişi yoksa `userprofile` bağlamının oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f392d-128">If there is no entry in hello cache that corresponds toohello key value, then no `userprofile` context variable will be created.</span></span> <span data-ttu-id="f392d-129">Biz hello kullanarak hello araması hello başarısını denetleyin `choose` kontrol akışı ilkesi.</span><span class="sxs-lookup"><span data-stu-id="f392d-129">We check hello success of hello lookup using hello `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If hello userprofile context variable doesn’t exist, make an HTTP request tooretrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="f392d-130">Merhaba, `userprofile` bağlamının yok ve devam eden toohave toomake bir HTTP isteği tooretrieve gerçekleştiriyoruz.</span><span class="sxs-lookup"><span data-stu-id="f392d-130">If hello `userprofile` context variable doesn’t exist, then we are going toohave toomake an HTTP request tooretrieve it.</span></span>

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points toohello profile for hello current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="f392d-131">Merhaba kullanırız `enduserid` tooconstruct hello URL toohello kullanıcı profili kaynağı.</span><span class="sxs-lookup"><span data-stu-id="f392d-131">We use hello `enduserid` tooconstruct hello URL toohello user profile resource.</span></span> <span data-ttu-id="f392d-132">Biz hello yanıt olduktan sonra biz hello gövde metni hello yanıt dışında çekme ve bir bağlam değişkende saklayın.</span><span class="sxs-lookup"><span data-stu-id="f392d-132">Once we have hello response, we can pull hello body text out of hello response and store it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="f392d-133">tooavoid bize hello aynı kullanıcı başka bir istekte bulunduğunda toomake bu HTTP isteği yeniden sahip, biz hello kullanıcı profili hello önbellekte saklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f392d-133">tooavoid us having toomake this HTTP request again, when hello same user makes another request, we can store hello user profile in hello cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="f392d-134">Biz başlangıçta tooretrieve çalıştı hello tam aynı anahtarı kullanarak hello Önbelleği'nde hello değeri depolarız ile.</span><span class="sxs-lookup"><span data-stu-id="f392d-134">We store hello value in hello cache using hello exact same key that we originally attempted tooretrieve it with.</span></span> <span data-ttu-id="f392d-135">Merhaba toostore hello değeri seçeneğini belirledik süresi ne sıklıkta hello bilgi değişikliklerini ve nasıl dayanıklı kullanıcılar tarih bilgisi tooout olduğuna bağlı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f392d-135">hello duration that we choose toostore hello value should be based on how often hello information changes and how tolerant users are tooout of date information.</span></span> 

<span data-ttu-id="f392d-136">Bu önemli toorealize hello önbellekten hala olduğundan bir işlem dışı, ağ isteği ve potansiyel olarak milisaniye toohello isteği onlarca eklemeye devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f392d-136">It is important toorealize that retrieving from hello cache is still an out-of-process, network request and potentially can still add tens of milliseconds toohello request.</span></span> <span data-ttu-id="f392d-137">belirleme hello kullanıcı profili bilgilerini daha önemli ölçüde uzun son tooneeding toodo veritabanı sorguları veya birden fazla arka uç toplama bilgilerinden yönlendirdiğinde hello avantajları gelir.</span><span class="sxs-lookup"><span data-stu-id="f392d-137">hello benefits come when determining hello user profile information takes significantly longer than that due tooneeding toodo database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="f392d-138">Merhaba son hello işleminde bizim kullanıcı profili bilgilerini içeren bir yanıt döndürdü tooupdate hello adımdır.</span><span class="sxs-lookup"><span data-stu-id="f392d-138">hello final step in hello process is tooupdate hello returned response with our user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="f392d-139">Böylece hello Değiştir bile gerçekleşmezse, hello yanıt hala geçerli JSON zamanki tooinclude hello tırnak işaretleri hello belirtecinin bir parçası seçtiğim.</span><span class="sxs-lookup"><span data-stu-id="f392d-139">I chose tooinclude hello quotation marks as part of hello token so that even when hello replace doesn’t occur, hello response was still valid JSON.</span></span> <span data-ttu-id="f392d-140">Öncelikle daha kolay hata ayıklama toomake oluştu.</span><span class="sxs-lookup"><span data-stu-id="f392d-140">This was primarily toomake debugging easier.</span></span>

<span data-ttu-id="f392d-141">Tüm adımları birleştirmek sonra hello sonuç hello bir aşağıdaki gibi görünen bir ilkedir.</span><span class="sxs-lookup"><span data-stu-id="f392d-141">Once you combine all these steps together, hello end result is a policy that looks like hello following one.</span></span>

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in hello cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in hello cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request tooget user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points toohello profile for hello current end-user -->
                    <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),(string)context.Variables["enduserid"]).AbsoluteUri)</set-url>
                    <set-method>GET</set-method>
                </send-request>

                <!-- Store response body in context variable -->
                <set-variable
                  name="userprofile"
                  value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />

                <!-- Store result in cache -->
                <cache-store-value
                  key="@("userprofile-" + context.Variables["enduserid"])"
                  value="@((string)context.Variables["userprofile"])"
                  duration="100000" />
            </when>
        </choose>
        <base />
    </inbound>
    <outbound>
        <!-- Update response body with user profile-->
        <find-and-replace
              from='"$userprofile$"'
              to="@((string)context.Variables["userprofile"])" />
        <base />
    </outbound>
</policies>
```

<span data-ttu-id="f392d-142">Önbelleğe alma bu yaklaşım, tek bir sayfa olarak işlenebilecek böylece burada HTML hello sunucu tarafında oluşur web siteleri, öncelikle kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f392d-142">This caching approach is primarily used in web sites where HTML is composed on hello server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="f392d-143">Ancak, bu da yararlı olabilir burada istemcileri bulunulamaz istemci API'ları yan HTTP önbelleğe alma veya tercih edilir değil tooput bu sorumluluğu hello istemcide.</span><span class="sxs-lookup"><span data-stu-id="f392d-143">However, it can also be useful in APIs where clients cannot do client side HTTP caching or it is desirable not tooput that responsibility on hello client.</span></span>

<span data-ttu-id="f392d-144">Parça önbelleğe alma bu aynı tür, sunucu önbelleği Redis hello arka uç web sunucularında kullanılarak yapılabilir, önbelleğe alınmış hello parçaları hello'den farklı arka uçları'ten gelen ancak hello API Management hizmeti tooperform kullanarak bu iş kullanışlıdır Birincil yanıtlar.</span><span class="sxs-lookup"><span data-stu-id="f392d-144">This same kind of fragment caching can also be done on hello backend web servers using a Redis caching server, however, using hello API Management service tooperform this work is useful when hello cached fragments are coming from different back-ends than hello primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="f392d-145">Saydam sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="f392d-145">Transparent versioning</span></span>
<span data-ttu-id="f392d-146">Desteklenen herhangi bir anda bir API toobe birden çok farklı uygulama sürümlerini yaygın bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="f392d-146">It is common practice for multiple different implementation versions of an API toobe supported at any one time.</span></span> <span data-ttu-id="f392d-147">Bu belki de geliştirme, test, üretim, vb., gibi toosupport farklı ortamlar veya hello API toogive zaman API tüketicileri toomigrate toonewer sürümleri için eski sürümleri toosupport olabilir.</span><span class="sxs-lookup"><span data-stu-id="f392d-147">This is perhaps toosupport different environments, like dev, test, production, etc, or it may be toosupport older versions of hello API toogive time for API consumers toomigrate toonewer versions.</span></span> 

<span data-ttu-id="f392d-148">İstemci geliştiricilerin toochange hello URL'lerden gerektiren bu bunun yerine, bir yaklaşım toohandling `/v1/customers` çok`/v2/customers` toostore hello tüketicinin profil verileri de hello API'ın hangi sürümü bunlar şu anda toouse istiyor ve çağırın hello uygun değil arka uç URL'si.</span><span class="sxs-lookup"><span data-stu-id="f392d-148">One approach toohandling this instead of requiring client developers toochange hello URLs from `/v1/customers` too`/v2/customers` is toostore in hello consumer’s profile data which version of hello API they currently wish toouse and call hello appropriate backend URL.</span></span> <span data-ttu-id="f392d-149">İsteğe bağlı olarak belirli bir istemci için sipariş toodetermine hello doğru arka uç URL'si toocall içinde gerekli tooquery olan bazı yapılandırma verileri.</span><span class="sxs-lookup"><span data-stu-id="f392d-149">In order toodetermine hello correct backend URL toocall for a particular client, it is necessary tooquery some configuration data.</span></span> <span data-ttu-id="f392d-150">Bu yapılandırma verileri önbelleğe alarak Biz bu Arama yapmanın hello performans cezası en aza indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f392d-150">By caching this configuration data, we can minimize hello performance penalty of doing this lookup.</span></span>

<span data-ttu-id="f392d-151">Merhaba ilk adımı toodetermine hello tanımlayıcı tooconfigure hello istediğiniz sürümü kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f392d-151">hello first step is toodetermine hello identifier used tooconfigure hello desired version.</span></span> <span data-ttu-id="f392d-152">Bu örnekte, t tooassociate hello sürüm toohello ürün abonelik anahtarı seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="f392d-152">In this example, I chose tooassociate hello version toohello product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="f392d-153">Biz hello istenen istemci sürümü aldıktan, biz sonra bir önbellek arama toosee yapın.</span><span class="sxs-lookup"><span data-stu-id="f392d-153">We then do a cache lookup toosee if we already have retrieved hello desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="f392d-154">Biz bunu hello önbelleğinde bulamadı olmadığını biz toosee denetleyin.</span><span class="sxs-lookup"><span data-stu-id="f392d-154">Then we check toosee if we did not find it in hello cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="f392d-155">Git ve bunu alma sonra biz almadıysanız.</span><span class="sxs-lookup"><span data-stu-id="f392d-155">If we didn’t then we go and retrieve it.</span></span>

```xml
<send-request
    mode="new"
    response-variable-name="clientconfiguresponse"
    timeout="10"
    ignore-error="true">
            <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
            <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="f392d-156">Merhaba yanıt gövdesi metni hello yanıttan ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="f392d-156">Extract hello response body text from hello response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="f392d-157">Gelecekte kullanım için hello önbelleğindeki geri depolar.</span><span class="sxs-lookup"><span data-stu-id="f392d-157">Store it back in hello cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="f392d-158">Ve son olarak hello arka uç URL'si tooselect hello hello istemci tarafından istenen hello hizmetinin sürümünü güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f392d-158">And finally update hello back-end URL tooselect hello version of hello service desired by hello client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="f392d-159">Merhaba tamamen ilke aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="f392d-159">hello completely policy is as follows.</span></span>

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in hello cache, make a request for it and store it -->
    <choose>
        <when condition="@(!context.Variables.ContainsKey("clientversion"))">
            <send-request mode="new" response-variable-name="clientconfiguresponse" timeout="10" ignore-error="true">
                <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
                <set-method>GET</set-method>
            </send-request>
            <!-- Store response body in context variable -->
            <set-variable name="clientversion" value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
            <!-- Store result in cache -->
            <cache-store-value key="@("clientversion-" + context.Variables["clientid"])" value="@((string)context.Variables["clientversion"])" duration="100000" />
        </when>
    </choose>
    <set-backend-service base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
</inbound>
```

<span data-ttu-id="f392d-160">Hangi arka uç sürümü tooupdate ve yeniden dağıtın istemcileri gerek kalmadan istemciler tarafından erişiliyor API tüketicileri tootransparently denetimini etkinleştirme birçok API sürüm oluşturma sorunları ele zarif bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="f392d-160">Enabling API consumers tootransparently control which backend version is being accessed by clients without having tooupdate and redeploy clients is a elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="f392d-161">Kiracı yalıtımı</span><span class="sxs-lookup"><span data-stu-id="f392d-161">Tenant Isolation</span></span>
<span data-ttu-id="f392d-162">Daha büyük, çok kiracılı dağıtımlarda bazı şirketler, arka uç donanım ayrı dağıtımlarına kiracılar ayrı grupları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f392d-162">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="f392d-163">Bu bir donanım sorunu hello arka uç tarafından etkilenen müşteriler hello sayısını en aza indirir.</span><span class="sxs-lookup"><span data-stu-id="f392d-163">This minimizes hello number of customers who are impacted by a hardware issue on hello backend.</span></span> <span data-ttu-id="f392d-164">Ayrıca, yeni yazılım sürümleri toobe aşamada alındı sağlar.</span><span class="sxs-lookup"><span data-stu-id="f392d-164">It also enables new software versions toobe rolled out in stages.</span></span> <span data-ttu-id="f392d-165">İdeal olarak bu arka uç mimarisi saydam tooAPI tüketicileri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f392d-165">Ideally this backend architecture should be transparent tooAPI consumers.</span></span> <span data-ttu-id="f392d-166">Merhaba üzerinde dayandığından bu benzer bir şekilde tootransparent sürüm oluşturma sağlanabilir API anahtarı başına yapılandırma durumu kullanarak hello arka uç URL'si düzenleme aynı tekniği.</span><span class="sxs-lookup"><span data-stu-id="f392d-166">This can be achieved in a similar way tootransparent versioning because it is based on hello same technique of manipulating hello backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="f392d-167">Merhaba API her abonelik anahtarı için tercih edilen bir sürümünü döndürme yerine bir kiracı atanan toohello donanım grubu ilişkili tanımlayıcı döndürecektir.</span><span class="sxs-lookup"><span data-stu-id="f392d-167">Instead of returning a preferred version of hello API for each subscription key, you would return an identifier that relates a tenant toohello assigned hardware group.</span></span> <span data-ttu-id="f392d-168">Bu tanımlayıcı, kullanılan tooconstruct hello uygun arka uç URL'si olabilir.</span><span class="sxs-lookup"><span data-stu-id="f392d-168">That identifier can be used tooconstruct hello appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="f392d-169">Özet</span><span class="sxs-lookup"><span data-stu-id="f392d-169">Summary</span></span>
<span data-ttu-id="f392d-170">Hello özgürlük toouse hello Azure API management önbellek her türlü veri depolamak için bir gelen talep işlenen hello biçimini etkileyebilir etkili erişim tooconfiguration veri sağlar.</span><span class="sxs-lookup"><span data-stu-id="f392d-170">hello freedom toouse hello Azure API management cache for storing any kind of data enables efficient access tooconfiguration data that can affect hello way an inbound request is processed.</span></span> <span data-ttu-id="f392d-171">Ayrıca, arka ucundan API döndürülen yanıt genişletebilirsiniz kullanılan toostore veri parçaları de olabilir.</span><span class="sxs-lookup"><span data-stu-id="f392d-171">It can also be used toostore data fragments that can augment responses, returned from a backend API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f392d-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f392d-172">Next steps</span></span>
<span data-ttu-id="f392d-173">Bu ilkeler için etkinleştirdiğiniz, veya senaryoları varsa tooachieve istediğiniz ancak değil düşündüğünüz diğer senaryolar şu anda olası varsa lütfen bize Geri bildiriminizi hello Disqus iş parçacığı için bu konunun verin.</span><span class="sxs-lookup"><span data-stu-id="f392d-173">Please give us your feedback in hello Disqus thread for this topic if there are other scenarios that these policies have enabled for you, or if there are scenarios you would like tooachieve but do not feel are currently possible.</span></span>

