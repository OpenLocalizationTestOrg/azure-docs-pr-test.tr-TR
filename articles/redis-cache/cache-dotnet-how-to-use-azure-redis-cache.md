---
title: "Azure Redis önbelleği aaaHow tooUse | Microsoft Docs"
description: "Nasıl tooimprove hello Azure Redis önbelleği ile Azure, uygulamalarınızın performansını öğrenin"
services: redis-cache,app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c502f74c-44de-4087-8303-1b1f43da12d5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 763d70c10972eec9a1885969e8da5bf1c4084727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache"></a><span data-ttu-id="428f8-103">Nasıl tooUse Azure Redis önbelleği</span><span class="sxs-lookup"><span data-stu-id="428f8-103">How tooUse Azure Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="428f8-104">.NET</span><span class="sxs-lookup"><span data-stu-id="428f8-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="428f8-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="428f8-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="428f8-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="428f8-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="428f8-107">Java</span><span class="sxs-lookup"><span data-stu-id="428f8-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="428f8-108">Python</span><span class="sxs-lookup"><span data-stu-id="428f8-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="428f8-109">Bu kılavuz size nasıl tooget kullanmaya gösterir **Azure Redis önbelleği**.</span><span class="sxs-lookup"><span data-stu-id="428f8-109">This guide shows you how tooget started using **Azure Redis Cache**.</span></span> <span data-ttu-id="428f8-110">Microsoft Azure Redis önbelleği hello popüler açık kaynak Redis önbelleğini temel alır.</span><span class="sxs-lookup"><span data-stu-id="428f8-110">Microsoft Azure Redis Cache is based on hello popular open source Redis Cache.</span></span> <span data-ttu-id="428f8-111">Size verir Microsoft tarafından yönetilen tooa güvenli, ayrılmış bir Redis önbelleğine erişmek.</span><span class="sxs-lookup"><span data-stu-id="428f8-111">It gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="428f8-112">Azure Redis Cache kullanılarak oluşturulan bir önbelleğe Microsoft Azure’daki her uygulamadan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="428f8-112">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="428f8-113">Microsoft Azure Redis önbelleği Katmanlar izleyerek hello kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="428f8-113">Microsoft Azure Redis Cache is available in hello following tiers:</span></span>

* <span data-ttu-id="428f8-114">**Temel** – Tek düğümlü.</span><span class="sxs-lookup"><span data-stu-id="428f8-114">**Basic** – Single node.</span></span> <span data-ttu-id="428f8-115">Birden çok too53 GB boyutları.</span><span class="sxs-lookup"><span data-stu-id="428f8-115">Multiple sizes up too53 GB.</span></span>
* <span data-ttu-id="428f8-116">**Standart** – İki düğümlü Birincil/Çoğaltma.</span><span class="sxs-lookup"><span data-stu-id="428f8-116">**Standard** – Two-node Primary/Replica.</span></span> <span data-ttu-id="428f8-117">Birden çok too53 GB boyutları.</span><span class="sxs-lookup"><span data-stu-id="428f8-117">Multiple sizes up too53 GB.</span></span> <span data-ttu-id="428f8-118">%99,9 SLA.</span><span class="sxs-lookup"><span data-stu-id="428f8-118">99.9% SLA.</span></span>
* <span data-ttu-id="428f8-119">**Premium** – iki düğümlü birincil/çoğaltma ile too10 parça ayarlama.</span><span class="sxs-lookup"><span data-stu-id="428f8-119">**Premium** – Two-node Primary/Replica with up too10 shards.</span></span> <span data-ttu-id="428f8-120">6 GB too530 GB birden çok boyut.</span><span class="sxs-lookup"><span data-stu-id="428f8-120">Multiple sizes from 6 GB too530 GB.</span></span> <span data-ttu-id="428f8-121">[Redis kümesi](cache-how-to-premium-clustering.md), [Redis kalıcılığı](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md) dahil tüm Standart katman özellikleri ve fazlası.</span><span class="sxs-lookup"><span data-stu-id="428f8-121">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="428f8-122">%99,9 SLA.</span><span class="sxs-lookup"><span data-stu-id="428f8-122">99.9% SLA.</span></span>

<span data-ttu-id="428f8-123">Her katman özellikler ve fiyatlandırma açısından farklıdır.</span><span class="sxs-lookup"><span data-stu-id="428f8-123">Each tier differs in terms of features and pricing.</span></span> <span data-ttu-id="428f8-124">Fiyatlandırma hakkında daha fazla bilgi için bkz. [Önbellek Fiyatlandırma Ayrıntıları][Cache Pricing Details].</span><span class="sxs-lookup"><span data-stu-id="428f8-124">For information on pricing, see [Cache Pricing Details][Cache Pricing Details].</span></span>

<span data-ttu-id="428f8-125">Bu kılavuz size nasıl gösterir toouse hello [StackExchange.Redis] [ StackExchange.Redis] C kullanarak istemci\# kodu.</span><span class="sxs-lookup"><span data-stu-id="428f8-125">This guide shows you how toouse hello [StackExchange.Redis][StackExchange.Redis] client using C\# code.</span></span> <span data-ttu-id="428f8-126">Merhaba kapsanan senaryolar dahil **oluşturma ve bir önbellek yapılandırma**, **önbellek istemcilerini yapılandırma**, ve **ekleme ve nesneleri hello önbellekten kaldırma**.</span><span class="sxs-lookup"><span data-stu-id="428f8-126">hello scenarios covered include **creating and configuring a cache**, **configuring cache clients**, and **adding and removing objects from hello cache**.</span></span> <span data-ttu-id="428f8-127">Azure Redis Cache’i kullanma hakkında daha fazla bilgi için bkz. [Sonraki Adımlar][Next Steps].</span><span class="sxs-lookup"><span data-stu-id="428f8-127">For more information on using Azure Redis Cache, see [Next Steps][Next Steps].</span></span> <span data-ttu-id="428f8-128">Bir ASP.NET MVC Redis önbelleği ile web uygulaması oluşturmanın adım adım öğretici için bkz [nasıl toocreate bir Web uygulamasını Redis önbelleği ile](cache-web-app-howto.md).</span><span class="sxs-lookup"><span data-stu-id="428f8-128">For a step-by-step tutorial of building an ASP.NET MVC web app with Redis Cache, see [How toocreate a Web App with Redis Cache](cache-web-app-howto.md).</span></span>

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a><span data-ttu-id="428f8-129">Azure Redis Cache’i kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="428f8-129">Get Started with Azure Redis Cache</span></span>
<span data-ttu-id="428f8-130">Azure Redis Cache’i kullanmaya başlamak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="428f8-130">Getting started with Azure Redis Cache is easy.</span></span> <span data-ttu-id="428f8-131">tooget başlatıldı, sağlamak ve bir önbellek yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="428f8-131">tooget started, you provision and configure a cache.</span></span> <span data-ttu-id="428f8-132">Ardından, hello önbelleğe erişebilmeleri hello önbellek istemcilerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="428f8-132">Next, you configure hello cache clients so they can access hello cache.</span></span> <span data-ttu-id="428f8-133">Merhaba önbellek istemcileri yapılandırıldıktan sonra bunlarla çalışmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="428f8-133">Once hello cache clients are configured, you can begin working with them.</span></span>

* <span data-ttu-id="428f8-134">[Merhaba önbelleği oluşturma][Create hello cache]</span><span class="sxs-lookup"><span data-stu-id="428f8-134">[Create hello cache][Create hello cache]</span></span>
* <span data-ttu-id="428f8-135">[Merhaba önbellek istemcilerini yapılandırın][Configure hello cache clients]</span><span class="sxs-lookup"><span data-stu-id="428f8-135">[Configure hello cache clients][Configure hello cache clients]</span></span>

<a name="create-cache"></a>

## <a name="create-a-cache"></a><span data-ttu-id="428f8-136">Bir önbellek oluşturma</span><span class="sxs-lookup"><span data-stu-id="428f8-136">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a><span data-ttu-id="428f8-137">tooaccess önbelleğiniz sonraki oluşturulur</span><span class="sxs-lookup"><span data-stu-id="428f8-137">tooaccess your cache after it's created</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="428f8-138">Önbelleğinizi yapılandırma hakkında daha fazla bilgi için bkz: [nasıl tooconfigure Azure Redis önbelleği](cache-configure.md).</span><span class="sxs-lookup"><span data-stu-id="428f8-138">For more information about configuring your cache, see [How tooconfigure Azure Redis Cache](cache-configure.md).</span></span>

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a><span data-ttu-id="428f8-139">Merhaba önbellek istemcilerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="428f8-139">Configure hello cache clients</span></span>
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

<span data-ttu-id="428f8-140">İstemci projeniz önbelleğe almak için yapılandırıldıktan sonra önbelleğinizle çalışmak için bölümleri aşağıdaki hello açıklanan hello teknikleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="428f8-140">Once your client project is configured for caching, you can use hello techniques described in hello following sections for working with your cache.</span></span>

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a><span data-ttu-id="428f8-141">Önbelleklerle Çalışma</span><span class="sxs-lookup"><span data-stu-id="428f8-141">Working with Caches</span></span>
<span data-ttu-id="428f8-142">Bu bölümdeki Hello adımları nasıl önbellekle tooperform ortak görevler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="428f8-142">hello steps in this section describe how tooperform common tasks with Cache.</span></span>

* <span data-ttu-id="428f8-143">[Toohello Önbelleği'ne bağlama][Connect toohello cache]</span><span class="sxs-lookup"><span data-stu-id="428f8-143">[Connect toohello cache][Connect toohello cache]</span></span>
* <span data-ttu-id="428f8-144">[Ekleme ve nesneleri hello önbellekten alma][Add and retrieve objects from hello cache]</span><span class="sxs-lookup"><span data-stu-id="428f8-144">[Add and retrieve objects from hello cache][Add and retrieve objects from hello cache]</span></span>
* [<span data-ttu-id="428f8-145">Merhaba önbelleğinde .NET nesneleriyle çalışma</span><span class="sxs-lookup"><span data-stu-id="428f8-145">Work with .NET objects in hello cache</span></span>](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a><span data-ttu-id="428f8-146">Toohello Önbelleği'ne bağlama</span><span class="sxs-lookup"><span data-stu-id="428f8-146">Connect toohello cache</span></span>
<span data-ttu-id="428f8-147">tooprogrammatically iş sahip bir önbellek, bir başvuru toohello önbellek gerekir.</span><span class="sxs-lookup"><span data-stu-id="428f8-147">tooprogrammatically work with a cache, you need a reference toohello cache.</span></span> <span data-ttu-id="428f8-148">Toohello üst toouse hello StackExchange.Redis istemcisi tooaccess bir Azure Redis önbelleği istediğiniz herhangi bir dosyasının içinden aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="428f8-148">Add hello following toohello top of any file from which you want toouse hello StackExchange.Redis client tooaccess an Azure Redis Cache.</span></span>

    using StackExchange.Redis;

> [!NOTE]
> <span data-ttu-id="428f8-149">Merhaba StackExchange.Redis istemcisi .NET Framework 4 veya üstünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="428f8-149">hello StackExchange.Redis client requires .NET Framework 4 or higher.</span></span>
> 
> 

<span data-ttu-id="428f8-150">Azure Redis önbelleği hello tarafından yönetilen bağlantı toohello hello `ConnectionMultiplexer` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="428f8-150">hello connection toohello Azure Redis Cache is managed by hello `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="428f8-151">Bu sınıf, paylaşılan ve istemci uygulamanız genelinde yeniden ve işlem bazında oluşturulan toobe gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="428f8-151">This class should be shared and reused throughout your client application, and does not need toobe created on a per operation basis.</span></span> 

<span data-ttu-id="428f8-152">Azure Redis önbelleği tooconnect tooan ve bağlı bir örneği döndürülmesi `ConnectionMultiplexer`, çağrı hello statik `Connect` yöntemi ve hello geçişinde önbellek uç noktasını ve anahtarı.</span><span class="sxs-lookup"><span data-stu-id="428f8-152">tooconnect tooan Azure Redis Cache and be returned an instance of a connected `ConnectionMultiplexer`, call hello static `Connect` method and pass in hello cache endpoint and key.</span></span> <span data-ttu-id="428f8-153">Merhaba hello parola parametresi olarak Azure portalında üretilen hello anahtarı kullanın.</span><span class="sxs-lookup"><span data-stu-id="428f8-153">Use hello key generated from hello Azure portal as hello password parameter.</span></span>

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> <span data-ttu-id="428f8-154">Uyarı: Kimlik bilgilerini asla kaynak kodunda depolamayın.</span><span class="sxs-lookup"><span data-stu-id="428f8-154">Warning: Never store credentials in source code.</span></span> <span data-ttu-id="428f8-155">tookeep Bu örneği basit ı bunları hello kaynak kodunda gösteren.</span><span class="sxs-lookup"><span data-stu-id="428f8-155">tookeep this sample simple, I’m showing them in hello source code.</span></span> <span data-ttu-id="428f8-156">Bkz: [nasıl uygulama dizeleri ve bağlantı dizeleri çalışma] [ How Application Strings and Connection Strings Work] hakkında bilgi için toostore kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="428f8-156">See [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] for information on how toostore credentials.</span></span>
> 
> 

<span data-ttu-id="428f8-157">Toouse SSL istemiyorsanız ya da ayarlayın `ssl=false` veya hello çıkarın `ssl` parametresi.</span><span class="sxs-lookup"><span data-stu-id="428f8-157">If you don't want toouse SSL, either set `ssl=false` or omit hello `ssl` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="428f8-158">Merhaba SSL olmayan bağlantı noktasının yeni önbellekler için varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="428f8-158">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="428f8-159">Merhaba SSL olmayan bağlantı noktasının etkinleştirilmesi ile ilgili yönergeler için bkz: [erişim bağlantı noktaları](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="428f8-159">For instructions on enabling hello non-SSL port, see [Access Ports](cache-configure.md#access-ports).</span></span>
> 
> 

<span data-ttu-id="428f8-160">Bir yaklaşım toosharing bir `ConnectionMultiplexer` örneğidir uygulamanızda toohave aşağıdaki örneğine benzer toohello bir bağlı örnek döndüren statik özelliğe.</span><span class="sxs-lookup"><span data-stu-id="428f8-160">One approach toosharing a `ConnectionMultiplexer` instance in your application is toohave a static property that returns a connected instance, similar toohello following example.</span></span> <span data-ttu-id="428f8-161">Bu yaklaşım, bağlı tek bir iş parçacığı açısından güvenli şekilde tooinitialize sağlar `ConnectionMultiplexer` örneği.</span><span class="sxs-lookup"><span data-stu-id="428f8-161">This approach provides a thread-safe way tooinitialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="428f8-162">Bu örneklerde `abortConnect` bağlantı toohello Azure Redis önbelleği bile kurulamazsa hello çağrı başarılı anlamına gelir kümesi toofalse değil.</span><span class="sxs-lookup"><span data-stu-id="428f8-162">In these examples `abortConnect` is set toofalse, which means that hello call succeeds even if a connection toohello Azure Redis Cache is not established.</span></span> <span data-ttu-id="428f8-163">Temel özelliklerinden biri `ConnectionMultiplexer` hello ağ sorunu ya da diğer nedenler çözüldükten sonra otomatik olarak bağlantı toohello önbellek yükler emin olan.</span><span class="sxs-lookup"><span data-stu-id="428f8-163">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity toohello cache once hello network issue or other causes are resolved.</span></span>

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

<span data-ttu-id="428f8-164">Gelişmiş bağlantı yapılandırma seçenekleri hakkında daha fazla bilgi için bkz:.[StackExchange.Redis yapılandırma modeli][StackExchange.Redis configuration model].</span><span class="sxs-lookup"><span data-stu-id="428f8-164">For more information on advanced connection configuration options, see [StackExchange.Redis configuration model][StackExchange.Redis configuration model].</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="428f8-165">Merhaba bağlantı kurulduktan sonra bir başvuru toohello redis önbelleği veritabanına göre arama hello dönmek `ConnectionMultiplexer.GetDatabase` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="428f8-165">Once hello connection is established, return a reference toohello redis cache database by calling hello `ConnectionMultiplexer.GetDatabase` method.</span></span> <span data-ttu-id="428f8-166">Merhaba hello döndürülen `GetDatabase` yöntemi basit bir geçiş nesnesi ve depolanan toobe gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="428f8-166">hello object returned from hello `GetDatabase` method is a lightweight pass-through object and does not need toobe stored.</span></span>

    // Connection refers tooa property that returns a ConnectionMultiplexer
    // as shown in hello previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using hello cache object...
    // Simple put of integral data types into hello cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from hello cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

<span data-ttu-id="428f8-167">Azure Redis önbellekleri yapılandırılabilir Redis önbelleği içinde kullanılan toologically ayrı hello veri olabilir (varsayılan 16) veritabanlarının sahiptir.</span><span class="sxs-lookup"><span data-stu-id="428f8-167">Azure Redis caches have a configurable number of databases (default of 16) that can be used toologically separate hello data within a Redis cache.</span></span> <span data-ttu-id="428f8-168">Daha fazla bilgi için bkz. [Redis veritabanı nedir?](cache-faq.md#what-are-redis-databases) ve [Varsayılan Redis sunucu yapılandırması](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="428f8-168">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span>

<span data-ttu-id="428f8-169">Veritabanı tooconnect tooan Azure Redis önbelleği örneği ve return başvuru toohello nasıl önbelleğe bildiğinize göre hello önbellekle çalışmaya konumundaki bakalım.</span><span class="sxs-lookup"><span data-stu-id="428f8-169">Now that you know how tooconnect tooan Azure Redis Cache instance and return a reference toohello cache database, let's look at working with hello cache.</span></span>

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a><span data-ttu-id="428f8-170">Ekleme ve nesneleri hello önbellekten alma</span><span class="sxs-lookup"><span data-stu-id="428f8-170">Add and retrieve objects from hello cache</span></span>
<span data-ttu-id="428f8-171">Öğeleri depolanır ve hello kullanarak önbellekten `StringSet` ve `StringGet` yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="428f8-171">Items can be stored in and retrieved from a cache by using hello `StringSet` and `StringGet` methods.</span></span>

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

<span data-ttu-id="428f8-172">Çoğu veri Redis dizeleri, ancak bu dizeler olarak pek çok .NET nesneleri depolarken kullanılabilecek hello önbelleğinde seri hale getirilmiş ikili veriler dahil olmak üzere veri türünü içerebilir depoları redis.</span><span class="sxs-lookup"><span data-stu-id="428f8-172">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in hello cache.</span></span>

<span data-ttu-id="428f8-173">Çağrılırken `StringGet`, hello nesne varsa, döndürülür ve onu yoksa `null` döndürülür.</span><span class="sxs-lookup"><span data-stu-id="428f8-173">When calling `StringGet`, if hello object exists, it is returned, and if it does not, `null` is returned.</span></span> <span data-ttu-id="428f8-174">Varsa `null` döndürülür, hello değeri hello istenen veri kaynağından almak ve daha sonra kullanılmak hello önbelleğindeki saklayın.</span><span class="sxs-lookup"><span data-stu-id="428f8-174">If `null` is returned, you can retrieve hello value from hello desired data source and store it in hello cache for subsequent use.</span></span> <span data-ttu-id="428f8-175">Bu kullanım deseni hello edilgen önbellek düzeni bilinir.</span><span class="sxs-lookup"><span data-stu-id="428f8-175">This usage pattern is known as hello cache-aside pattern.</span></span>

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

<span data-ttu-id="428f8-176">Aynı zamanda `RedisValue`hello aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="428f8-176">You can also use `RedisValue`, as shown in hello following example.</span></span> <span data-ttu-id="428f8-177">`RedisValue`, tam sayı veri türleriyle çalışmaya yönelik örtük işleçlere sahiptir ve önbelleğe alınan öğe için `null` beklenen bir değerse yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="428f8-177">`RedisValue` has implicit operators for working with integral data types, and can be useful if `null` is an expected value for a cached item.</span></span>


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


<span data-ttu-id="428f8-178">bir öğenin hello önbelleğindeki kullanım hello toospecify hello sona erme `TimeSpan` parametresinin `StringSet`.</span><span class="sxs-lookup"><span data-stu-id="428f8-178">toospecify hello expiration of an item in hello cache, use hello `TimeSpan` parameter of `StringSet`.</span></span>

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a><span data-ttu-id="428f8-179">Merhaba önbelleğinde .NET nesneleriyle çalışma</span><span class="sxs-lookup"><span data-stu-id="428f8-179">Work with .NET objects in hello cache</span></span>
<span data-ttu-id="428f8-180">Azure Redis Cache temel veri türlerinin yanı sıra .NET nesnelerini de önbelleğe alabilir, ancak bir .NET nesnesini önbelleğe alabilmek için seri hale getirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="428f8-180">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="428f8-181">Bu .NET nesne seri hale getirme hello uygulama geliştiricisi hello sorumluluğundadır ve hello seri hale getirici hello tercihini hello Geliştirici esnekliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="428f8-181">This .NET object serialization is hello responsibility of hello application developer, and gives hello developer flexibility in hello choice of hello serializer.</span></span>

<span data-ttu-id="428f8-182">Bir basit yol tooserialize nesneleri olan toouse hello `JsonConvert` seri hale getirme yöntemleri [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) ve tooand JSON öğesinden seri.</span><span class="sxs-lookup"><span data-stu-id="428f8-182">One simple way tooserialize objects is toouse hello `JsonConvert` serialization methods in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) and serialize tooand from JSON.</span></span> <span data-ttu-id="428f8-183">Merhaba aşağıdaki örnek bir kullanılarak Al ve Ayarla gösterir bir `Employee` nesne örneği.</span><span class="sxs-lookup"><span data-stu-id="428f8-183">hello following example shows a get and set using an `Employee` object instance.</span></span>

    class Employee
    {
        public int Id { get; set; }
        public string Name { get; set; }

        public Employee(int EmployeeId, string Name)
        {
            this.Id = EmployeeId;
            this.Name = Name;
        }
    }

    // Store toocache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a><span data-ttu-id="428f8-184">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="428f8-184">Next Steps</span></span>
<span data-ttu-id="428f8-185">Merhaba öğrendiğinize göre Azure Redis önbelleği hakkında daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="428f8-185">Now that you've learned hello basics, follow these links toolearn more about Azure Redis Cache.</span></span>

* <span data-ttu-id="428f8-186">Out Hello Azure Redis önbelleği için ASP.NET sağlayıcılarına denetleyin.</span><span class="sxs-lookup"><span data-stu-id="428f8-186">Check out hello ASP.NET providers for Azure Redis Cache.</span></span>
  * [<span data-ttu-id="428f8-187">Azure Redis Oturum Durumu Sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="428f8-187">Azure Redis Session State Provider</span></span>](cache-aspnet-session-state-provider.md)
  * [<span data-ttu-id="428f8-188">Azure Redis Cache ASP.NET Çıktı Önbelleği Sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="428f8-188">Azure Redis Cache ASP.NET Output Cache Provider</span></span>](cache-aspnet-output-cache-provider.md)
* <span data-ttu-id="428f8-189">[Önbellek tanılamayı etkinleştirin](cache-how-to-monitor.md#enable-cache-diagnostics) , böylece [İzleyici](cache-how-to-monitor.md) hello önbelleğinizin sistem durumunu.</span><span class="sxs-lookup"><span data-stu-id="428f8-189">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span> <span data-ttu-id="428f8-190">Hello Azure portal ve ölçümler için de hello görüntüleyebilirsiniz [indirebilir ve gözden](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) bunları tercih ettiğiniz hello araçlarını kullanma.</span><span class="sxs-lookup"><span data-stu-id="428f8-190">You can view hello metrics in hello Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using hello tools of your choice.</span></span>
* <span data-ttu-id="428f8-191">Merhaba denetleyin [StackExchange.Redis önbellek istemcisi belgeleri][StackExchange.Redis cache client documentation].</span><span class="sxs-lookup"><span data-stu-id="428f8-191">Check out hello [StackExchange.Redis cache client documentation][StackExchange.Redis cache client documentation].</span></span>
  * <span data-ttu-id="428f8-192">Azure Redis Cache birçok Redis istemcisinden ve geliştirme dilinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="428f8-192">Azure Redis Cache can be accessed from many Redis clients and development languages.</span></span> <span data-ttu-id="428f8-193">Daha fazla bilgi için bkz. [http://redis.io/clients][http://redis.io/clients].</span><span class="sxs-lookup"><span data-stu-id="428f8-193">For more information, see [http://redis.io/clients][http://redis.io/clients].</span></span>
* <span data-ttu-id="428f8-194">Azure Redis Cache ayrıca Redsmin ve Redis Desktop Manager gibi üçüncü taraf hizmetler ve araçlarla birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="428f8-194">Azure Redis Cache can also be used with third-party services and tools such as Redsmin and Redis Desktop Manager.</span></span>
  * <span data-ttu-id="428f8-195">Redsmin birlikte hakkında daha fazla bilgi için bkz: [nasıl tooretrieve bir Azure Redis bağlantı dizesi ve redsmin ile birlikte][How tooretrieve an Azure Redis connection string and use it with Redsmin].</span><span class="sxs-lookup"><span data-stu-id="428f8-195">For more information about Redsmin, see [How tooretrieve an Azure Redis connection string and use it with Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].</span></span>
  * <span data-ttu-id="428f8-196">Azure Redis Cache’teki verilerinize erişin ve bunları [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager) kullanan bir GUI ile inceleyin.</span><span class="sxs-lookup"><span data-stu-id="428f8-196">Access and inspect your data in Azure Redis Cache with a GUI using [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span></span>
* <span data-ttu-id="428f8-197">Merhaba bkz [redis] [ redis] belgeleri ve hakkında bilgi [redis veri türleri] [ redis data types] ve [on beş dakikalık bir giriş tooRedis veri türleri][a fifteen minute introduction tooRedis data types].</span><span class="sxs-lookup"><span data-stu-id="428f8-197">See hello [redis][redis] documentation and read about [redis data types][redis data types] and [a fifteen minute introduction tooRedis data types][a fifteen minute introduction tooRedis data types].</span></span>

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction tooAzure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project tooUse Azure Caching]: #prepare-vs
[Configure Your Application tooUse Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create hello cache]: #create-cache
[Configure hello cache]: #enable-caching
[Configure hello cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect toohello cache]: #connect-to-cache
[Add and retrieve objects from hello cache]: #add-object
[Specify hello expiration of an object in hello cache]: #specify-expiration
[Store ASP.NET session state in hello cache]: #store-session


<!-- IMAGES -->


[StackExchangeNuget]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-stackexchange-redis.png

[NuGetMenu]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-nuget-menu.png

[CacheProperties]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-properties.png

[ManageKeys]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-keys.png

[SessionStateNuGet]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-session-state-provider.png

[BrowseCaches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-browse-caches.png

[Caches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-caches.png







<!-- LINKS -->
[http://redis.io/clients]: http://redis.io/clients
[Develop in other languages for Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn690470.aspx
[How tooretrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How tooConfigure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set hello Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in hello cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate tooAzure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups toomanage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction tooRedis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/


