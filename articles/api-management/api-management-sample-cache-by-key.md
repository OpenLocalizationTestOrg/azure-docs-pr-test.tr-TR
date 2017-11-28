---
title: "Azure API Management'te özel önbelleğe alma"
description: "Azure API Management'te anahtarı tarafından öğeleri önbelleğe öğrenin"
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
ms.openlocfilehash: f5d5f44e34fbcd122a10be0ca5b3001760c4c64d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="ca1e3-103">Azure API Management'te özel önbelleğe alma</span><span class="sxs-lookup"><span data-stu-id="ca1e3-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="ca1e3-104">Azure API Management hizmeti için yerleşik destek sahip [HTTP yanıt önbelleğe alma](api-management-howto-cache.md) kaynak URL anahtar olarak kullanma.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using the resource URL as the key.</span></span> <span data-ttu-id="ca1e3-105">Anahtar kullanarak istek üstbilgileri tarafından değiştirilebilir `vary-by` özellikleri.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-105">The key can be modified by request headers using the `vary-by` properties.</span></span> <span data-ttu-id="ca1e3-106">Tüm HTTP yanıtlarını (diğer adıyla Beyanları) önbelleğe alma işlemi için yararlıdır, ancak bazen yalnızca önbellek temsili bir kısmı için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful to just cache a portion of a representation.</span></span> <span data-ttu-id="ca1e3-107">Yeni [önbellek arama değeri](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) ve [önbellek deposu değeri](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) ilkeleri, depolama ve ilke tanımları içindeki verileri rasgele parçalarını alma olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-107">The new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide the ability to store and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="ca1e3-108">Bu özellik ayrıca değeri önceden sunulan ekler [gönderme isteği](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) İlkesi çünkü dış hizmetler yanıtlarının şimdi önbelleğe alabilir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-108">This ability also adds value to the previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="ca1e3-109">Mimari</span><span class="sxs-lookup"><span data-stu-id="ca1e3-109">Architecture</span></span>
<span data-ttu-id="ca1e3-110">En fazla ölçek gibi birden çok birimi hala aynı erişimi alırsınız verileri önbelleğe böylece API Management hizmeti Kiracı başına paylaşılan veri önbelleği kullanır.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-110">API Management service uses a shared per-tenant data cache so that, as you scale up to multiple units you will still get access to the same cached data.</span></span> <span data-ttu-id="ca1e3-111">Ancak, bölgeli dağıtımı ile çalışırken, her bölge içinde bağımsız önbellekleri vardır.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-111">However, when working with a multi-region deployment there are independent caches within each of the regions.</span></span> <span data-ttu-id="ca1e3-112">Bunun nedeni, önbelleğe yalnızca kaynak bilgileri parçasının olduğu bir veri deposu olarak davranmanız değil önemlidir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-112">Due to this, it is important to not treat the cache as a data store, where it is the only source of some piece of information.</span></span> <span data-ttu-id="ca1e3-113">Vermedi ve daha sonra bölgeli dağıtım yararlanmak karar, seyahat kullanıcılarla müşteriler bu önbelleğe alınmış verileri erişimlerini kaybedebilir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-113">If you did, and later decided to take advantage of the multi-region deployment, then customers with users that travel may lose access to that cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="ca1e3-114">Parça önbelleğe alma</span><span class="sxs-lookup"><span data-stu-id="ca1e3-114">Fragment caching</span></span>
<span data-ttu-id="ca1e3-115">Burada verilen yanıtları belirlemek pahalıdır ve makul bir süre için henüz yeni kalan verileri kısmı içeren bazı durumlar vardır.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-115">There are certain cases where responses being returned contain some portion of data that is expensive to determine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="ca1e3-116">Örnek olarak, Uçuş Rezervasyonları, uçuş durumu ile ilgili bilgi sağlayan bir uçak tarafından oluşturulmuş bir hizmeti kullanmayı düşünün. Kullanıcı airlines noktaları program üyesi ise, ayrıca bunların geçerli durumu ve toplanan mesafe ilgili bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If the user is a member of the airlines points program, they would also have information relating to their current status and mileage accumulated.</span></span> <span data-ttu-id="ca1e3-117">Bu kullanıcı ile ilgili bilgiler farklı depolanabilir, ancak uçuş durumu ve ayırmaları hakkında döndürülen yanıtlar dahil istenebilir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-117">This user-related information might be stored in a different system, but it may be desirable to include it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="ca1e3-118">Bu yapılabilir parça önbelleğe alma adlı bir işlem kullanılarak.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="ca1e3-119">Birincil gösterimi kullanıcı ile ilgili bilgiler eklenecek nerede belirtmek için bir tür belirteci kullanarak kaynak sunucudan döndürülebilir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-119">The primary representation can be returned from the origin server using some kind of token to indicate where the user-related information is to be inserted.</span></span> 

<span data-ttu-id="ca1e3-120">Arka uç API'si aşağıdaki JSON yanıtı göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-120">Consider the following JSON response from a backend API.</span></span>

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

<span data-ttu-id="ca1e3-121">Ve ikincil kaynakta `/userprofile/{userid}` olduğunu gibi görünüyor,</span><span class="sxs-lookup"><span data-stu-id="ca1e3-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="ca1e3-122">Uygun kullanıcı bilgileri içerecek şekilde belirlemek için biz son kullanıcının kim olduğunu tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-122">In order to determine the appropriate user information to include, we need to identify who the end user is.</span></span> <span data-ttu-id="ca1e3-123">Bu mekanizma bağımlı uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-123">This mechanism is implementation dependent.</span></span> <span data-ttu-id="ca1e3-124">Örnek olarak, kullanıyorum `Subject` , talep bir `JWT` belirteci.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-124">As an example, I am using the `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="ca1e3-125">Bu depolarız `enduserid` daha sonra kullanmak için bir bağlam değişken değeri.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-125">We store this `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="ca1e3-126">Sonraki adım, önceki bir istek daha önce kullanıcı bilgileri alınır ve önbellekte depolanan varsa belirlemektir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-126">The next step is to determine if a previous request has already retrieved the user information and stored it in the cache.</span></span> <span data-ttu-id="ca1e3-127">Bunun için kullandığımız `cache-lookup-value` ilkesi.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-127">For this we use the `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="ca1e3-128">Anahtar değeri sonra Hayır karşılık gelen önbellek girişi yoksa `userprofile` bağlamının oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-128">If there is no entry in the cache that corresponds to the key value, then no `userprofile` context variable will be created.</span></span> <span data-ttu-id="ca1e3-129">Biz arama kullanma başarısını denetleyin `choose` kontrol akışı ilkesi.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-129">We check the success of the lookup using the `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If the userprofile context variable doesn’t exist, make an HTTP request to retrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="ca1e3-130">Varsa `userprofile` bağlamının yoksa, ardından bunu almak için bir HTTP isteği yapmak zorunda kalacaklarını.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-130">If the `userprofile` context variable doesn’t exist, then we are going to have to make an HTTP request to retrieve it.</span></span>

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points to the profile for the current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="ca1e3-131">Kullanırız `enduserid` kullanıcı profili kaynağı URL'si oluşturulamadı.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-131">We use the `enduserid` to construct the URL to the user profile resource.</span></span> <span data-ttu-id="ca1e3-132">Yanıt sahibiz sonra biz yanıt dışında gövde metni çekmek ve bir bağlam değişkende saklayın.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-132">Once we have the response, we can pull the body text out of the response and store it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="ca1e3-133">Bize aynı kullanıcı başka bir istekte bulunduğunda bu HTTP isteği yeniden sağlamak zorunda önlemek için biz kullanıcı profili önbellekte saklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-133">To avoid us having to make this HTTP request again, when the same user makes another request, we can store the user profile in the cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="ca1e3-134">Biz başlangıçta ile almayı denedi tam aynı anahtarı kullanarak önbelleğinde değeri depolarız.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-134">We store the value in the cache using the exact same key that we originally attempted to retrieve it with.</span></span> <span data-ttu-id="ca1e3-135">Biz değeri depolamak üzere seçtiğiniz süre hakkında temel gereken genellikle bilgi değişikliklerini ve nasıl dayanıklı kullanıcılar için güncel bilgilerdir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-135">The duration that we choose to store the value should be based on how often the information changes and how tolerant users are to out of date information.</span></span> 

<span data-ttu-id="ca1e3-136">Önbellekten hala olduğundan bir işlem dışı, ağ isteği ve potansiyel olarak milisaniye onlarca isteği eklemeye devam edebilirsiniz, hayata geçirmek önemlidir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-136">It is important to realize that retrieving from the cache is still an out-of-process, network request and potentially can still add tens of milliseconds to the request.</span></span> <span data-ttu-id="ca1e3-137">Kullanıcı profili bilgilerini sorgular veya toplama bilgilerinden birden fazla arka uç veritabanı gerek nedeniyle daha önemli ölçüde daha uzun sürer belirlerken avantajları gelir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-137">The benefits come when determining the user profile information takes significantly longer than that due to needing to do database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="ca1e3-138">Son işlem döndürülen yanıt bizim kullanıcı profili bilgilerle güncelleştirmek için adımdır.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-138">The final step in the process is to update the returned response with our user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="ca1e3-139">Tırnak işaretleri belirtecinin bir parçası içermesi Değiştir bile gerçekleşmezse, yanıt hala geçerli JSON zamanki seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-139">I chose to include the quotation marks as part of the token so that even when the replace doesn’t occur, the response was still valid JSON.</span></span> <span data-ttu-id="ca1e3-140">Öncelikle daha kolay hata ayıklama yapmak için bu.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-140">This was primarily to make debugging easier.</span></span>

<span data-ttu-id="ca1e3-141">Tüm adımları birleştirmek sonra sonuç aşağıdaki biri gibi görünen bir ilkedir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-141">Once you combine all these steps together, the end result is a policy that looks like the following one.</span></span>

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in the cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in the cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request to get user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points to the profile for the current end-user -->
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

<span data-ttu-id="ca1e3-142">Önbelleğe alma bu yaklaşım, tek bir sayfa olarak işlenebilecek böylece burada HTML sunucu tarafında oluşur web siteleri, öncelikle kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-142">This caching approach is primarily used in web sites where HTML is composed on the server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="ca1e3-143">Ancak, bu da yararlı olabilir burada istemcileri bulunulamaz istemci API'ları yan HTTP önbelleğe alma veya bu sorumluluğu istemcide değil yerleştirilecek istenen bir durumdur.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-143">However, it can also be useful in APIs where clients cannot do client side HTTP caching or it is desirable not to put that responsibility on the client.</span></span>

<span data-ttu-id="ca1e3-144">Parça önbelleğe alma bu aynı tür, arka uç web sunucularında sunucu önbelleği Redis kullanılarak yapılabilir, önbelleğe alınan parçaları birincil daha farklı arka uçları'ten gelen ancak API Management hizmeti kullanarak bu çalışmayı gerçekleştirmek için faydalıdır yanıtlar.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-144">This same kind of fragment caching can also be done on the backend web servers using a Redis caching server, however, using the API Management service to perform this work is useful when the cached fragments are coming from different back-ends than the primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="ca1e3-145">Saydam sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="ca1e3-145">Transparent versioning</span></span>
<span data-ttu-id="ca1e3-146">Herhangi bir zamanda desteklenmesi için bir API birden çok farklı uygulama sürümlerini yaygın bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-146">It is common practice for multiple different implementation versions of an API to be supported at any one time.</span></span> <span data-ttu-id="ca1e3-147">Bu belki de geliştirme, test, üretim, vb., gibi farklı ortamları desteklemek için veya daha yeni sürümüne geçirmek API Tüketiciler için zaman vermek için API eski sürümleri desteklemek için olabilir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-147">This is perhaps to support different environments, like dev, test, production, etc, or it may be to support older versions of the API to give time for API consumers to migrate to newer versions.</span></span> 

<span data-ttu-id="ca1e3-148">Bu URL'lerden değiştirmek istemci geliştiriciler istemek yerine işleme bir yaklaşım `/v1/customers` için `/v2/customers` şu anda istedikleri kullanın ve uygun arka uç URL'si çağırmak için API'ın hangi sürümü tüketicinin profil verileri depolamak için.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-148">One approach to handling this instead of requiring client developers to change the URLs from `/v1/customers` to `/v2/customers` is to store in the consumer’s profile data which version of the API they currently wish to use and call the appropriate backend URL.</span></span> <span data-ttu-id="ca1e3-149">Belirli bir istemci için çağırmak için doğru arka uç URL'si belirlemek için bazı yapılandırma verileri sorgulamak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-149">In order to determine the correct backend URL to call for a particular client, it is necessary to query some configuration data.</span></span> <span data-ttu-id="ca1e3-150">Bu yapılandırma verileri önbelleğe alarak biz yaşanan bu Arama yapmanın performans sorunları en aza indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-150">By caching this configuration data, we can minimize the performance penalty of doing this lookup.</span></span>

<span data-ttu-id="ca1e3-151">İlk adım, istenen sürüm yapılandırmak için kullanılan tanımlayıcı belirlemektir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-151">The first step is to determine the identifier used to configure the desired version.</span></span> <span data-ttu-id="ca1e3-152">Bu örnekte, ürün abonelik anahtarı sürüme ilişkilendirilecek seçtiğim.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-152">In this example, I chose to associate the version to the product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="ca1e3-153">Biz sonra biz zaten istenen istemci sürümü aldıktan olmadığını görmek için önbellek araması yapın.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-153">We then do a cache lookup to see if we already have retrieved the desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="ca1e3-154">Ardından biz biz bunu önbellekte bulamadı olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-154">Then we check to see if we did not find it in the cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="ca1e3-155">Git ve bunu alma sonra biz almadıysanız.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-155">If we didn’t then we go and retrieve it.</span></span>

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

<span data-ttu-id="ca1e3-156">Yanıt gövdesi metni yanıttan ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-156">Extract the response body text from the response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="ca1e3-157">Gelecekte kullanım için önbelleğindeki depolar.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-157">Store it back in the cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="ca1e3-158">Ve son olarak istemci tarafından istenen hizmetin sürümünü seçmek için arka uç URL'si güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-158">And finally update the back-end URL to select the version of the service desired by the client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="ca1e3-159">Tamamen ilke aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-159">The completely policy is as follows.</span></span>

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in the cache, make a request for it and store it -->
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

<span data-ttu-id="ca1e3-160">Saydam güncelleştirin ve istemcilerin yeniden dağıtmak zorunda kalmadan, hangi arka uç sürümü istemciler tarafından erişiliyor denetlemek API tüketicileri etkinleştirme birçok API sürüm oluşturma sorunları ele zarif bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-160">Enabling API consumers to transparently control which backend version is being accessed by clients without having to update and redeploy clients is a elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="ca1e3-161">Kiracı yalıtımı</span><span class="sxs-lookup"><span data-stu-id="ca1e3-161">Tenant Isolation</span></span>
<span data-ttu-id="ca1e3-162">Daha büyük, çok kiracılı dağıtımlarda bazı şirketler, arka uç donanım ayrı dağıtımlarına kiracılar ayrı grupları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-162">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="ca1e3-163">Bu arka uç üzerinde donanım sorundan etkilenen müşteriler sayısını en aza indirir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-163">This minimizes the number of customers who are impacted by a hardware issue on the backend.</span></span> <span data-ttu-id="ca1e3-164">Ayrıca, yeni yazılım sürümleri aşamada alınması sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-164">It also enables new software versions to be rolled out in stages.</span></span> <span data-ttu-id="ca1e3-165">İdeal olarak bu arka uç mimarisi API tüketicilere saydam olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-165">Ideally this backend architecture should be transparent to API consumers.</span></span> <span data-ttu-id="ca1e3-166">API anahtarı başına yapılandırma durumu kullanarak arka uç URL'si düzenleme aynı tekniği bağlı olduğu bu saydam sürüm benzer bir şekilde sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-166">This can be achieved in a similar way to transparent versioning because it is based on the same technique of manipulating the backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="ca1e3-167">API her abonelik anahtarı için tercih edilen bir sürümünü döndürme yerine atanan donanım grubu için bir kiracı ilişkili tanımlayıcı döndürecektir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-167">Instead of returning a preferred version of the API for each subscription key, you would return an identifier that relates a tenant to the assigned hardware group.</span></span> <span data-ttu-id="ca1e3-168">Bu tanımlayıcı, uygun arka uç URL'si oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-168">That identifier can be used to construct the appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="ca1e3-169">Özet</span><span class="sxs-lookup"><span data-stu-id="ca1e3-169">Summary</span></span>
<span data-ttu-id="ca1e3-170">Her türlü veri depolamak için Azure API management önbellek kullanma özgürlüğü verimli bir gelen talep işlenen biçimini etkileyebilir yapılandırma verilerine erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-170">The freedom to use the Azure API management cache for storing any kind of data enables efficient access to configuration data that can affect the way an inbound request is processed.</span></span> <span data-ttu-id="ca1e3-171">Ayrıca, bir arka API döndürülen yanıt genişletebilirsiniz veri parçaları depolamak için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-171">It can also be used to store data fragments that can augment responses, returned from a backend API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca1e3-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ca1e3-172">Next steps</span></span>
<span data-ttu-id="ca1e3-173">Lütfen bize geri bildirim Disqus iş parçacığı için bu konuda bu ilkeler için etkinleştirdiğiniz diğer senaryolar varsa veya senaryoları varsa elde etmek ister misiniz verin ancak şu anda mümkün olan eşitleyerek değil.</span><span class="sxs-lookup"><span data-stu-id="ca1e3-173">Please give us your feedback in the Disqus thread for this topic if there are other scenarios that these policies have enabled for you, or if there are scenarios you would like to achieve but do not feel are currently possible.</span></span>

