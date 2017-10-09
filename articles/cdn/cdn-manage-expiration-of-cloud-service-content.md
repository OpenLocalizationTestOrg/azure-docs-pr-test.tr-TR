---
title: "web içeriğinin Azure CDN aaaManage sona erme | Microsoft Docs"
description: "Bilgi nasıl Azure CDN Azure Web Apps/bulut Hizmetleri, ASP.NET ve IIS içeriğinde toomanage sona erme tarihi."
services: cdn
documentationcenter: .NET
author: zhangmanling
manager: erikre
editor: 
ms.assetid: bef53fcc-bb13-4002-9324-9edee9da8288
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a0154236c3893b627f4480e0688f555964862556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a><span data-ttu-id="abba0-103">Azure CDN Azure Web Apps/bulut Hizmetleri, ASP.NET ve IIS içeriğinin kullanım süresini yönetme</span><span class="sxs-lookup"><span data-stu-id="abba0-103">Manage expiration of Azure Web Apps/Cloud Services, ASP.NET, or IIS content in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="abba0-104">Azure Web Apps/bulut Hizmetleri, ASP.NET ve IIS</span><span class="sxs-lookup"><span data-stu-id="abba0-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="abba0-105">Azure depolama blob hizmeti</span><span class="sxs-lookup"><span data-stu-id="abba0-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="abba0-106">Kendi yaşam süresi (TTL) geçen kadar herhangi bir genel olarak erişilebilir kaynak web sunucusuna dosyalarından Azure CDN'de önbelleğe alınabilir.</span><span class="sxs-lookup"><span data-stu-id="abba0-106">Files from any publicly accessible origin web server can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="abba0-107">Merhaba TTL hello tarafından belirlenir [ *Cache-Control* üstbilgi](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) hello kaynak sunucudan hello HTTP yanıt.</span><span class="sxs-lookup"><span data-stu-id="abba0-107">hello TTL is determined by hello [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in hello HTTP response from hello origin server.</span></span>  <span data-ttu-id="abba0-108">Bu makalede nasıl tooset `Cache-Control` Azure Web uygulamaları, Azure bulut Hizmetleri, ASP.NET uygulamaları ve bunların tümü benzer şekilde yapılandırılmış, Internet Information Services siteleri için üstbilgiler.</span><span class="sxs-lookup"><span data-stu-id="abba0-108">This article describes how tooset `Cache-Control` headers for Azure Web Apps, Azure Cloud Services, ASP.NET applications, and Internet Information Services sites, all of which are configured similarly.</span></span>

> [!TIP]
> <span data-ttu-id="abba0-109">Bir dosya üzerinde hiçbir TTL tooset seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="abba0-109">You may choose tooset no TTL on a file.</span></span>  <span data-ttu-id="abba0-110">Bu durumda, Azure CDN varsayılan TTL yedi gün otomatik olarak uygular.</span><span class="sxs-lookup"><span data-stu-id="abba0-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="abba0-111">Hello Azure CDN toospeed erişim toofiles ve diğer kaynakların nasıl çalıştığı hakkında daha fazla bilgi için bkz: [Azure CDN'ye genel bakış](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="abba0-111">For more information about how Azure CDN works toospeed up access toofiles and other resources, see hello [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a><span data-ttu-id="abba0-112">Cache-Control üstbilgileri yapılandırmasında ayarlama</span><span class="sxs-lookup"><span data-stu-id="abba0-112">Setting Cache-Control Headers in configuration</span></span>
<span data-ttu-id="abba0-113">Görüntüleri ve stil sayfalarını gibi statik içerik hello güncelleştirme sıklığı hello değiştirerek denetleyebilirsiniz **applicationHost.config** veya **web.config** web uygulamanız için dosyaları.</span><span class="sxs-lookup"><span data-stu-id="abba0-113">For static content, such as images and style sheets, you can control hello update frequency by modifying hello **applicationHost.config** or **web.config** files for your web application.</span></span>  <span data-ttu-id="abba0-114">Merhaba **system.webServer\staticContent\clientCache** hello yapılandırma dosyası öğesi hello ayarlayacak `Cache-Control` içeriğiniz için üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="abba0-114">hello **system.webServer\staticContent\clientCache** element in hello configuration file will set hello `Cache-Control` header for your content.</span></span> <span data-ttu-id="abba0-115">İçin **web.config**, hello yapılandırma ayarlarını etkiler her şeyi hello klasör ve tüm alt klasörlerde hello alt düzeyinde geçersiz kılınmadığı sürece.</span><span class="sxs-lookup"><span data-stu-id="abba0-115">For **web.config**, hello configuration settings will affect everything in hello folder and all subfolders, unless overridden at hello subfolder level.</span></span>  <span data-ttu-id="abba0-116">Örneğin, bir varsayılan yaşam süresi sırasında tüm statik içeriği 3 gün boyunca önbelleğe alınmış, ancak daha fazla değişken 6 saat ile bir önbellek ayarı içerik sahip bir alt klasörünüz hello kök toohave ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="abba0-116">For example, you can set a default time-to-live at hello root toohave all static content cached for 3 days, but have a subfolder that has more variable content with a cache setting of 6 hours.</span></span>  <span data-ttu-id="abba0-117">İçin **applicationHost.config**, hello sitedeki tüm uygulamaları etkiler ancak geçersiz kılınabilir **web.config** hello uygulamalarında dosyaları.</span><span class="sxs-lookup"><span data-stu-id="abba0-117">For **applicationHost.config**, all applications on hello site will be affected, but can be overridden in **web.config** files in hello applications.</span></span>

<span data-ttu-id="abba0-118">Merhaba aşağıdaki XML örneği ayarı gösterilmektedir **clientCache** en uzun geçerlilik süresi 3 günlük bir toospecify:</span><span class="sxs-lookup"><span data-stu-id="abba0-118">hello following XML shows an example of setting **clientCache** toospecify a maximum age of 3 days:</span></span>  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

<span data-ttu-id="abba0-119">Belirtme **UseMaxAge** ekler bir `Cache-Control: max-age=<nnn>` hello belirtilen hello değere dayanarak üstbilgi toohello yanıt **CacheControlMaxAge** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="abba0-119">Specifying **UseMaxAge** adds a `Cache-Control: max-age=<nnn>` header toohello response based on hello value specified in hello **CacheControlMaxAge** attribute.</span></span> <span data-ttu-id="abba0-120">Merhaba hello timespan biçimidir Merhaba **cacheControlMaxAge** özniteliği <days>.<hours>:<min>:<sec>.</span><span class="sxs-lookup"><span data-stu-id="abba0-120">hello format of hello timespan is for hello **cacheControlMaxAge** attribute is <days>.<hours>:<min>:<sec>.</span></span> <span data-ttu-id="abba0-121">Merhaba hakkında daha fazla bilgi için **clientCache** düğümü, bkz: [istemci önbelleği <clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span><span class="sxs-lookup"><span data-stu-id="abba0-121">For more information on hello **clientCache** node, see [Client Cache <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span></span>  

## <a name="setting-cache-control-headers-in-code"></a><span data-ttu-id="abba0-122">Cache-Control üstbilgileri kodda ayarlama</span><span class="sxs-lookup"><span data-stu-id="abba0-122">Setting Cache-Control Headers in Code</span></span>
<span data-ttu-id="abba0-123">ASP.NET uygulamaları için hello CDN önbelleğe alma davranışını programlı olarak ayarlama hello tarafından ayarlayabileceğiniz **HttpResponse.Cache** özelliği.</span><span class="sxs-lookup"><span data-stu-id="abba0-123">For ASP.NET applications, you can set hello CDN caching behavior programmatically by setting hello **HttpResponse.Cache** property.</span></span> <span data-ttu-id="abba0-124">Merhaba hakkında daha fazla bilgi için **HttpResponse.Cache** özelliği, bkz: [HttpResponse.Cache özelliği](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) ve [HttpCachePolicy sınıfı](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="abba0-124">For more information on hello **HttpResponse.Cache** property, see [HttpResponse.Cache Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) and [HttpCachePolicy Class](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

<span data-ttu-id="abba0-125">ASP.NET tooprogrammatically önbellek uygulama içeriği istiyorsanız hello içerik HttpCacheability çok ayarlayarak olarak alınabilir işaretli olduğundan emin olun*ortak*.</span><span class="sxs-lookup"><span data-stu-id="abba0-125">If you want tooprogrammatically cache application content in ASP.NET, make sure that hello content is marked as cacheable by setting HttpCacheability too*Public*.</span></span> <span data-ttu-id="abba0-126">Ayrıca, bir önbellek Doğrulayıcı ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="abba0-126">Also, ensure that a cache validator is set.</span></span> <span data-ttu-id="abba0-127">Merhaba önbellek Doğrulayıcı son değişiklik olabilir SetLastModified ya da bir etag değeri aranarak zaman damgası ayarlamak SetETag çağırarak.</span><span class="sxs-lookup"><span data-stu-id="abba0-127">hello cache validator can be a Last Modified timestamp set by calling SetLastModified, or an etag value set by calling SetETag.</span></span> <span data-ttu-id="abba0-128">İsteğe bağlı olarak, SetExpires çağırarak bir önbellek süre sonu zamanı belirtebilirsiniz veya hello varsayılan önbellek buluşsal yöntemler bu belgenin önceki bölümlerinde açıklanan bağlı.</span><span class="sxs-lookup"><span data-stu-id="abba0-128">Optionally, you can also specify a cache expiration time by calling SetExpires, or you can rely on hello default cache heuristics described earlier in this document.</span></span>  

<span data-ttu-id="abba0-129">Örneğin, bir saat toocache içerik hello aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="abba0-129">For example, toocache content for one hour, add hello following:</span></span>  

```csharp
// Set hello caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a><span data-ttu-id="abba0-130">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="abba0-130">Next Steps</span></span>
* [<span data-ttu-id="abba0-131">Merhaba ayrıntılarını okumak **clientCache** öğesi</span><span class="sxs-lookup"><span data-stu-id="abba0-131">Read details about hello **clientCache** element</span></span>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [<span data-ttu-id="abba0-132">Merhaba Hello belgelerini okuyun **HttpResponse.Cache** özelliği</span><span class="sxs-lookup"><span data-stu-id="abba0-132">Read hello documentation for hello **HttpResponse.Cache** Property</span></span>](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* <span data-ttu-id="abba0-133">[Merhaba Hello belgelerini okuyun **HttpCachePolicy sınıfı**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="abba0-133">[Read hello documentation for hello **HttpCachePolicy Class**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

