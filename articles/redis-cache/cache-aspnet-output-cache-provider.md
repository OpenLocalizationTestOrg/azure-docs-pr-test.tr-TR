---
title: "aaaCache ASP.NET çıktı önbelleği sağlayıcısı"
description: "Bilgi Azure Redis önbelleği kullanılarak toocache ASP.NET sayfa çıktısı nasıl"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 78469a66-0829-484f-8660-b2598ec60fbf
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/14/2017
ms.author: sdanie
ms.openlocfilehash: fc38cc657604b351f55ad8febac383783ac29700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a><span data-ttu-id="dc22f-103">ASP.NET çıktı önbelleği sağlayıcısı Azure Redis önbelleği</span><span class="sxs-lookup"><span data-stu-id="dc22f-103">ASP.NET Output Cache Provider for Azure Redis Cache</span></span>
<span data-ttu-id="dc22f-104">Merhaba Redis çıkış önbelleği sağlayıcısı, çıktı önbelleği veriler için bir işlem dışı depolama mekanizmasıdır.</span><span class="sxs-lookup"><span data-stu-id="dc22f-104">hello Redis Output Cache Provider is an out-of-process storage mechanism for output cache data.</span></span> <span data-ttu-id="dc22f-105">Bu veriler için özellikle tam HTTP yanıtları edinilebilir (sayfa çıkış önbelleğe alma).</span><span class="sxs-lookup"><span data-stu-id="dc22f-105">This data is specifically for full HTTP responses (page output caching).</span></span> <span data-ttu-id="dc22f-106">noktasına ASP.NET 4'te tanıtılan hello yeni çıkış önbelleği sağlayıcısı genişletilebilirlik Hello sağlayıcısı takılan.</span><span class="sxs-lookup"><span data-stu-id="dc22f-106">hello provider plugs into hello new output cache provider extensibility point that was introduced in ASP.NET 4.</span></span>

<span data-ttu-id="dc22f-107">toouse hello Redis çıkış önbelleği sağlayıcısı önbelleğinizi önce yapılandırın ve hello Redis çıkış önbelleği sağlayıcısı NuGet paketi kullanarak ASP.NET uygulamanızı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="dc22f-107">toouse hello Redis Output Cache Provider, first configure your cache, and then configure your ASP.NET application using hello Redis Output Cache Provider NuGet package.</span></span> <span data-ttu-id="dc22f-108">Bu konu, uygulama toouse hello Redis çıktı önbelleği sağlayıcısını yapılandırma hakkında yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="dc22f-108">This topic provides guidance on configuring your application toouse hello Redis Output Cache Provider.</span></span> <span data-ttu-id="dc22f-109">Oluşturma ve bir Azure Redis önbelleği örneği yapılandırma hakkında daha fazla bilgi için bkz: [bir önbellek oluşturma](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="dc22f-109">For more information about creating and configuring an Azure Redis Cache instance, see [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

## <a name="store-aspnet-page-output-in-hello-cache"></a><span data-ttu-id="dc22f-110">ASP.NET sayfa çıktısının hello önbelleğine depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dc22f-110">Store ASP.NET page output in hello cache</span></span>
<span data-ttu-id="dc22f-111">tooconfigure hello Redis önbelleği oturum durumu NuGet paketini kullanarak Visual Studio'da bir istemci uygulaması tıklatın **NuGet Paket Yöneticisi**, **Paket Yöneticisi Konsolu** hello gelen **Araçları** menüsü.</span><span class="sxs-lookup"><span data-stu-id="dc22f-111">tooconfigure a client application in Visual Studio using hello Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>

<span data-ttu-id="dc22f-112">Çalışma hello hello komuttan aşağıdaki `Package Manager Console` penceresi.</span><span class="sxs-lookup"><span data-stu-id="dc22f-112">Run hello following command from hello `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

<span data-ttu-id="dc22f-113">Merhaba Redis çıkış önbelleği sağlayıcısı NuGet paketi hello StackExchange.Redis.StrongName paketi bir bağımlılığa sahiptir.</span><span class="sxs-lookup"><span data-stu-id="dc22f-113">hello Redis Output Cache Provider NuGet package has a dependency on hello StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="dc22f-114">Merhaba StackExchange.Redis.StrongName paket projenizde mevcut değilse, yüklenir.</span><span class="sxs-lookup"><span data-stu-id="dc22f-114">If hello StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span> <span data-ttu-id="dc22f-115">Merhaba hello Redis çıkış önbelleği sağlayıcısı NuGet paketi hakkında daha fazla bilgi için bkz: [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet sayfası.</span><span class="sxs-lookup"><span data-stu-id="dc22f-115">For more information about hello Redis Output Cache Provider NuGet package, see hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet page.</span></span>

>[!NOTE]
><span data-ttu-id="dc22f-116">Toplama toohello tanımlayıcı adlı StackExchange.Redis.StrongName paketinde ayrıca hello StackExchange.Redis olmayan-tanımlayıcı adlı sürümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="dc22f-116">In addition toohello strong-named StackExchange.Redis.StrongName package, there is also hello StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="dc22f-117">Projenizi hello olmayan-tanımlayıcı adlı StackExchange.Redis sürümü kaldırmanız gerekir kullanıyorsanız, aksi takdirde, projenizde adlandırma çakışmaları alın.</span><span class="sxs-lookup"><span data-stu-id="dc22f-117">If your project is using hello non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="dc22f-118">Bu paketleri hakkında daha fazla bilgi için bkz: [yapılandırma .NET önbellek istemcilerinin](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span><span class="sxs-lookup"><span data-stu-id="dc22f-118">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="dc22f-119">Hello paketi indirir ve hello ekler NuGet gerekli derleme başvuruyor ve bölümü web.config dosyanıza aşağıdaki hello ekler.</span><span class="sxs-lookup"><span data-stu-id="dc22f-119">hello NuGet package downloads and adds hello required assembly references and adds hello following section into your web.config file.</span></span> <span data-ttu-id="dc22f-120">Bu bölümde, ASP.NET uygulama toouse hello Redis çıkış önbelleği sağlayıcısı için hello gerekli yapılandırmayı içerir.</span><span class="sxs-lookup"><span data-stu-id="dc22f-120">This section contains hello required configuration for your ASP.NET application toouse hello Redis Output Cache Provider.</span></span>

```xml
<caching>
  <outputCachedefault Provider="MyRedisOutputCache">
    <providers>
      <!--
      <add name="MyRedisOutputCache"
        host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
      />
      -->
      <add name="MyRedisOutputCache" type="Microsoft.Web.Redis.RedisOutputCacheProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
  </outputCache>
</caching>
```

<span data-ttu-id="dc22f-121">Merhaba geçersiz kılınan bölüm hello özniteliklerinin ve örnek ayarlarını her özniteliği için bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="dc22f-121">hello commented section provides an example of hello attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="dc22f-122">Merhaba Microsoft Azure Portalı'nda önbellek dikey pencerenizin hello değerlerle Hello öznitelikleri yapılandırmak ve yapılandırmak istediğiniz gibi diğer değerleri hello.</span><span class="sxs-lookup"><span data-stu-id="dc22f-122">Configure hello attributes with hello values from your cache blade in hello Microsoft Azure portal, and configure hello other values as desired.</span></span> <span data-ttu-id="dc22f-123">Önbellek özelliklerine erişme ile ilgili yönergeler için bkz: [Redis önbelleği ayarlarını yapılandırma](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="dc22f-123">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="dc22f-124">**ana bilgisayar** – önbellek uç noktasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="dc22f-124">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="dc22f-125">**bağlantı noktası** – SSL olmayan bağlantı noktası veya hello ssl ayarlarına bağlı olarak, SSL bağlantı noktası kullanın.</span><span class="sxs-lookup"><span data-stu-id="dc22f-125">**port** – use either your non-SSL port or your SSL port, depending on hello ssl settings.</span></span>
* <span data-ttu-id="dc22f-126">**accessKey** – önbelleğiniz için ya da hello birincil veya ikincil anahtarı kullanın.</span><span class="sxs-lookup"><span data-stu-id="dc22f-126">**accessKey** – use either hello primary or secondary key for your cache.</span></span>
* <span data-ttu-id="dc22f-127">**SSL** – toosecure önbellek/istemci iletişimleri ile ssl istiyorsanız True, aksi takdirde false.</span><span class="sxs-lookup"><span data-stu-id="dc22f-127">**ssl** – true if you want toosecure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="dc22f-128">Emin toospecify hello doğru bağlantı noktası olabilir.</span><span class="sxs-lookup"><span data-stu-id="dc22f-128">Be sure toospecify hello correct port.</span></span>
  * <span data-ttu-id="dc22f-129">Merhaba SSL olmayan bağlantı noktasının yeni önbellekler için varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="dc22f-129">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="dc22f-130">Bu ayar toouse hello SSL bağlantı noktası için true belirtin.</span><span class="sxs-lookup"><span data-stu-id="dc22f-130">Specify true for this setting toouse hello SSL port.</span></span> <span data-ttu-id="dc22f-131">Merhaba hello SSL olmayan bağlantı noktası etkinleştirme hakkında daha fazla bilgi için bkz: [erişim bağlantı noktaları](cache-configure.md#access-ports) hello bölümünde [bir önbellek yapılandırma](cache-configure.md) konu.</span><span class="sxs-lookup"><span data-stu-id="dc22f-131">For more information about enabling hello non-SSL port, see hello [Access Ports](cache-configure.md#access-ports) section in hello [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="dc22f-132">**Databaseıd** – hangi veritabanı toouse önbelleği için çıktı verilerini belirtilen.</span><span class="sxs-lookup"><span data-stu-id="dc22f-132">**databaseId** – Specified which database toouse for cache output data.</span></span> <span data-ttu-id="dc22f-133">Belirtilmezse, 0 hello varsayılan değeri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dc22f-133">If not specified, hello default value of 0 is used.</span></span>
* <span data-ttu-id="dc22f-134">**applicationName** – anahtarları redis depolanır `<AppName>_<SessionId>_Data`.</span><span class="sxs-lookup"><span data-stu-id="dc22f-134">**applicationName** – Keys are stored in redis as `<AppName>_<SessionId>_Data`.</span></span> <span data-ttu-id="dc22f-135">Bu adlandırma şeması birden çok uygulamaları tooshare hello etkinleştirir aynı anahtarı.</span><span class="sxs-lookup"><span data-stu-id="dc22f-135">This naming scheme enables multiple applications tooshare hello same key.</span></span> <span data-ttu-id="dc22f-136">Bu parametre isteğe bağlıdır ve onu belirtmezseniz, varsayılan değer kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dc22f-136">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="dc22f-137">**connectionTimeoutInMilliseconds** – Bu ayar, hello StackExchange.Redis istemci ayarı toooverride hello connectTimeout sağlar.</span><span class="sxs-lookup"><span data-stu-id="dc22f-137">**connectionTimeoutInMilliseconds** – This setting allows you toooverride hello connectTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="dc22f-138">Belirtilmezse, 5000 hello varsayılan connectTimeout ayarı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dc22f-138">If not specified, hello default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="dc22f-139">Daha fazla bilgi için bkz: [StackExchange.Redis yapılandırma modeli](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="dc22f-139">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="dc22f-140">**operationTimeoutInMilliseconds** – Bu ayar, hello StackExchange.Redis istemci ayarı toooverride hello syncTimeout sağlar.</span><span class="sxs-lookup"><span data-stu-id="dc22f-140">**operationTimeoutInMilliseconds** – This setting allows you toooverride hello syncTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="dc22f-141">Belirtilmezse, 1000 hello varsayılan syncTimeout ayar kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dc22f-141">If not specified, hello default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="dc22f-142">Daha fazla bilgi için bkz: [StackExchange.Redis yapılandırma modeli](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="dc22f-142">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="dc22f-143">Toocache hello çıkış istediğiniz bir OutputCache yönergesi tooeach sayfası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="dc22f-143">Add an OutputCache directive tooeach page for which you wish toocache hello output.</span></span>

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

<span data-ttu-id="dc22f-144">Merhaba önceki örnekte hello sayfası veri kalır hello önbelleğinde 60 saniye boyunca önbelleğe ve hello sayfanın farklı bir sürümünü her parametre birleşimi için önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="dc22f-144">In hello previous example, hello cached page data remains in hello cache for 60 seconds, and a different version of hello page is cached for each parameter combination.</span></span> <span data-ttu-id="dc22f-145">Merhaba OutputCache yönergesi hakkında daha fazla bilgi için bkz: [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837).</span><span class="sxs-lookup"><span data-stu-id="dc22f-145">For more information about hello OutputCache directive, see [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span></span>

<span data-ttu-id="dc22f-146">Bu adımları gerçekleştirdikten sonra yapılandırılmış toouse hello Redis çıkış önbelleği sağlayıcısı uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="dc22f-146">Once these steps are performed, your application is configured toouse hello Redis Output Cache Provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc22f-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dc22f-147">Next steps</span></span>
<span data-ttu-id="dc22f-148">Merhaba denetleyin [Azure Redis önbelleği için ASP.NET oturum durumu sağlayıcısı](cache-aspnet-session-state-provider.md).</span><span class="sxs-lookup"><span data-stu-id="dc22f-148">Check out hello [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md).</span></span>

