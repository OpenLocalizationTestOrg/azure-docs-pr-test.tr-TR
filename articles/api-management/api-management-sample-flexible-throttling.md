---
title: "Azure API Management ile azaltma aaaAdvanced isteği"
description: "Bilgi nasıl toocreate ve esnek kota ve ilkeleri Azure API Management ile hız sınırı uygulayın."
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: ac87f83118a37bd587fddf044e5c2d6fc2af9031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a><span data-ttu-id="40949-103">Gelişmiş istek azaltma ile Azure API Yönetimi</span><span class="sxs-lookup"><span data-stu-id="40949-103">Advanced request throttling with Azure API Management</span></span>
<span data-ttu-id="40949-104">Mümkün toothrottle gelen istekleri olan Azure API Management önemli bir rol var.</span><span class="sxs-lookup"><span data-stu-id="40949-104">Being able toothrottle incoming requests is a key role of Azure API Management.</span></span> <span data-ttu-id="40949-105">API Management sağlar ya da kontrol eden hello oranı istekler veya hello toplam istekleri/veri transfer, API sağlayıcıları tooprotect kötüye kendi API'lerden ve farklı API ürün katmanları için değeri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="40949-105">Either by controlling hello rate of requests or hello total requests/data transferred, API Management allows API providers tooprotect their APIs from abuse and create value for different API product tiers.</span></span>

## <a name="product-based-throttling"></a><span data-ttu-id="40949-106">Ürün tabanlı azaltma</span><span class="sxs-lookup"><span data-stu-id="40949-106">Product based throttling</span></span>
<span data-ttu-id="40949-107">toodate, kısıtlama yetenekleri hello oranı sınırlı toobeing kapsamlı tooa belirli ürün abonelik (aslında bir anahtarı), API Management yayımcı portalına hello tanımlanan.</span><span class="sxs-lookup"><span data-stu-id="40949-107">toodate, hello rate throttling capabilities have been limited toobeing scoped tooa particular Product subscription (essentially a key), defined in hello API Management publisher portal.</span></span> <span data-ttu-id="40949-108">Merhaba API sağlayıcısı tooapply sınırları toouse kendi API açmış hello geliştiriciler için faydalıdır, ancak bu, örneğin, tek tek son kullanıcılar hello API için azaltma korumaz.</span><span class="sxs-lookup"><span data-stu-id="40949-108">This is useful for hello API provider tooapply limits on hello developers who have signed up toouse their API, however, it does not help, for example, in throttling individual end-users of hello API.</span></span> <span data-ttu-id="40949-109">Bu, hello geliştiricinin uygulama tooconsume tek bir kullanıcı için tüm kota hello ve ardından diğer müşteriler hello Developer mümkün toouse Merhaba uygulaması engelleyen mümkün olur.</span><span class="sxs-lookup"><span data-stu-id="40949-109">It is possible that for single user of hello developer's application tooconsume hello entire quota and then prevent other customers of hello developer from being able toouse hello application.</span></span> <span data-ttu-id="40949-110">Ayrıca, bir istek hacmi yüksek oluşturabilir çeşitli müşteriler erişim toooccasional kullanıcıları sınırlayabilir.</span><span class="sxs-lookup"><span data-stu-id="40949-110">Also, several customers who might generate a high volume of requests may limit access toooccasional users.</span></span>

## <a name="custom-key-based-throttling"></a><span data-ttu-id="40949-111">Özel anahtar tabanlı azaltma</span><span class="sxs-lookup"><span data-stu-id="40949-111">Custom key based throttling</span></span>
<span data-ttu-id="40949-112">Merhaba yeni [anahtar tarafından hızı sınırı](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) ve [kota anahtarı](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) önemli ölçüde daha esnek bir çözüm tootraffic denetim ilkeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="40949-112">hello new [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies provide a significantly more flexible solution tootraffic control.</span></span> <span data-ttu-id="40949-113">Bu yeni ilkeleri kullanılan tootrack trafiği kullanım olacaktır toodefine ifadeleri tooidentify hello anahtarlarının izin verir.</span><span class="sxs-lookup"><span data-stu-id="40949-113">These new policies allow you toodefine expressions tooidentify hello keys that will be used tootrack traffic usage.</span></span> <span data-ttu-id="40949-114">Bu çalışır hello şekilde kolay bir örnekle gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="40949-114">hello way this works is easiest illustrated with an example.</span></span> 

## <a name="ip-address-throttling"></a><span data-ttu-id="40949-115">IP adresi azaltma</span><span class="sxs-lookup"><span data-stu-id="40949-115">IP Address throttling</span></span>
<span data-ttu-id="40949-116">Merhaba aşağıdaki ilkeleri kısıtlamak tek bir istemci IP adresi tooonly 10 dakikada 1.000.000 çağrıları ve bant genişliği aylık 10.000 kilobayt toplam çağırır.</span><span class="sxs-lookup"><span data-stu-id="40949-116">hello following policies restrict a single client IP address tooonly 10 calls every minute, with a total of 1,000,000 calls and 10,000 kilobytes of bandwidth per month.</span></span> 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

<span data-ttu-id="40949-117">Merhaba Internet üzerindeki tüm istemcilere benzersiz bir IP adresi kullandıysanız, bu kullanıcı tarafından kullanımı sınırlama, etkili bir yol olabilir.</span><span class="sxs-lookup"><span data-stu-id="40949-117">If all clients on hello Internet used a unique IP address, this might be an effective way of limiting usage by user.</span></span> <span data-ttu-id="40949-118">Ancak, birden çok kullanıcı bir NAT cihazı üzerinden toothem erişilirken hello Internet nedeniyle tek bir ortak IP adresi paylaşımı olacak oldukça olasıdır.</span><span class="sxs-lookup"><span data-stu-id="40949-118">However, it is quite likely that multiple users will sharing a single public IP address due toothem accessing hello Internet via a NAT device.</span></span> <span data-ttu-id="40949-119">Buna karşın, kimliği doğrulanmamış erişim hello izin API'leri için `IpAddress` hello en iyi seçenek olabilir.</span><span class="sxs-lookup"><span data-stu-id="40949-119">Despite this, for APIs that allow unauthenticated access hello `IpAddress` might be hello best option.</span></span>

## <a name="user-identity-throttling"></a><span data-ttu-id="40949-120">Kullanıcı Kimliği azaltma</span><span class="sxs-lookup"><span data-stu-id="40949-120">User identity throttling</span></span>
<span data-ttu-id="40949-121">Son kullanıcının kimliği doğrulandıktan sonra azaltma anahtarı tanıtan bir, bilgilere dayalı olarak oluşturulabilen kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="40949-121">If an end user is authenticated then a throttling key can be generated based on information that uniquely identifies an that user.</span></span>

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

<span data-ttu-id="40949-122">Bu örnekte biz hello Authorization Üstbilgisi ayıklama ve çok Dönüştür`JWT` nesne ve hello belirteci tooidentify hello kullanıcının hello konu ve anahtar sınırlama hello hızı olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="40949-122">In this example we extract hello Authorization header, convert it too`JWT` object and use hello subject of hello token tooidentify hello user and use that as hello rate limiting key.</span></span> <span data-ttu-id="40949-123">Merhaba kullanıcı kimliği hello depolanıyorsa `JWT` hello başka birini sonra değer onun yerine kullanılabilir talep gibi.</span><span class="sxs-lookup"><span data-stu-id="40949-123">If hello user identity is stored in hello `JWT` as one of hello other claims then that value could be used in its place.</span></span>

## <a name="combined-policies"></a><span data-ttu-id="40949-124">Birleşik ilkeleri</span><span class="sxs-lookup"><span data-stu-id="40949-124">Combined policies</span></span>
<span data-ttu-id="40949-125">Yeni ilkeler azaltma hello kısıtlama ilkeleri varolan hello daha fazla denetim sağlar ancak da hala her iki özelliği birleştirme değer vardır.</span><span class="sxs-lookup"><span data-stu-id="40949-125">Although hello new throttling policies provide more control than hello existing throttling policies, there is still value combining both capabilities.</span></span> <span data-ttu-id="40949-126">Ürün abonelik anahtarı tarafından azaltma ([abonelik tarafından çağrı hızını sınırla](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) ve [abonelik tarafından kullanım kotası ayarla](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) temel kullanım düzeyleri şarj tarafından bir API tooenable monetizing harika bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="40949-126">Throttling by product subscription key ([Limit call rate by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is a great way tooenable monetizing of an API by charging based on usage levels.</span></span> <span data-ttu-id="40949-127">Merhaba kullanıcı tarafından mümkün toothrottle olma daha hassas denetim tamamlayıcı ve bir kullanıcının davranışına başka bir hello deneyimi düşürmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="40949-127">hello finer grained control of being able toothrottle by user is complementary and prevents one user's behavior from degrading hello experience of another.</span></span> 

## <a name="client-driven-throttling"></a><span data-ttu-id="40949-128">Azaltma yönetilen istemci</span><span class="sxs-lookup"><span data-stu-id="40949-128">Client driven throttling</span></span>
<span data-ttu-id="40949-129">Anahtar azaltma hello kullanarak tanımlandığında bir [ilke ifadesi](https://msdn.microsoft.com/library/azure/dn910913.aspx), hello azaltma nasıl kapsamlıdır seçme hello API sağlayıcı ise.</span><span class="sxs-lookup"><span data-stu-id="40949-129">When hello throttling key is defined using a [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx), then it is hello API provider that is choosing how hello throttling is scoped.</span></span> <span data-ttu-id="40949-130">Bununla birlikte, bir geliştirici isteyebilirsiniz nasıl oranı toocontrol sınırlamak kendi müşteriler.</span><span class="sxs-lookup"><span data-stu-id="40949-130">However, a developer might want toocontrol how they rate limit their own customers.</span></span> <span data-ttu-id="40949-131">Bu hello API sağlayıcısı tarafından bir özel üstbilgi tooallow hello Geliştirici istemci uygulaması toocommunicate hello anahtar toohello API sunarak etkinleştirilmesi.</span><span class="sxs-lookup"><span data-stu-id="40949-131">This could be enabled by hello API provider by introducing a custom header tooallow hello developer's client application toocommunicate hello key toohello API.</span></span>

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

<span data-ttu-id="40949-132">Bu hello geliştiricinin istemci uygulaması toochoose sağlar anahtar sınırlama toocreate hello oranı nasıl istedikleri.</span><span class="sxs-lookup"><span data-stu-id="40949-132">This enables hello developer's client application toochoose how they want toocreate hello rate limiting key.</span></span> <span data-ttu-id="40949-133">Biraz resimleri ile bir istemci Geliştirici anahtarları toousers kümelerini ayırma ve hello anahtar kullanımı döndürme kendi oranı katmanları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40949-133">With a little bit of ingenuity a client developer could create their own rate tiers by allocating sets of keys toousers and rotating hello key usage.</span></span>

## <a name="summary"></a><span data-ttu-id="40949-134">Özet</span><span class="sxs-lookup"><span data-stu-id="40949-134">Summary</span></span>
<span data-ttu-id="40949-135">Azure API Management oranı tooboth azaltma teklif korumak ve değer tooyour API hizmeti eklemek sağlar.</span><span class="sxs-lookup"><span data-stu-id="40949-135">Azure API Management provides rate and quote throttling tooboth protect and add value tooyour API service.</span></span> <span data-ttu-id="40949-136">Yeni özel ölçüm kuralları ilkeleriyle azaltma hello yüksekse, bu ilkeleri tooenable üzerinde denetim müşteriler toobuild daha da iyi uygulamalarınızı düzey izin verir.</span><span class="sxs-lookup"><span data-stu-id="40949-136">hello new throttling policies with custom scoping rules allow you finer grained control over those policies tooenable your customers toobuild even better applications.</span></span> <span data-ttu-id="40949-137">Bu makalede Hello örnekler, istemci IP adresleri, kullanıcı kimliği ve istemci oluşturulan değerleri anahtarlarla sınırlama üretim hızına göre bu yeni ilkeleri hello kullanımını göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="40949-137">hello examples in this article demonstrate hello use of these new policies by manufacturing rate limiting keys with client IP addresses, user identity, and client generated values.</span></span> <span data-ttu-id="40949-138">Ancak, diğer birçok kullanılabilecek kullanıcı aracısı, URL yolu parçaları, ileti boyutu gibi selamlama iletisine bölümleri vardır.</span><span class="sxs-lookup"><span data-stu-id="40949-138">However, there are many other parts of hello message that could be used such as user agent, URL path fragments, message size.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40949-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="40949-139">Next steps</span></span>
<span data-ttu-id="40949-140">Lütfen bize Geri bildiriminizi hello Disqus iş parçacığı için bu konunun verin.</span><span class="sxs-lookup"><span data-stu-id="40949-140">Please give us your feedback in hello Disqus thread for this topic.</span></span> <span data-ttu-id="40949-141">Senaryolarınız mantıksal bir seçenek olan diğer olası anahtar değerleri hakkında harika toohear olacaktır.</span><span class="sxs-lookup"><span data-stu-id="40949-141">It would be great toohear about other potential key values that have been a logical choice in your scenarios.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="40949-142">Bu ilkelerin video genel izleyin</span><span class="sxs-lookup"><span data-stu-id="40949-142">Watch a video overview of these policies</span></span>
<span data-ttu-id="40949-143">Merhaba hakkında daha fazla bilgi için [anahtar tarafından hızı sınırı](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) ve [kota anahtarı](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) bu makalede ele alınan ilkeleri Lütfen video aşağıdaki hello izleyin.</span><span class="sxs-lookup"><span data-stu-id="40949-143">For more information on hello [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies covered in this article, please watch hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

