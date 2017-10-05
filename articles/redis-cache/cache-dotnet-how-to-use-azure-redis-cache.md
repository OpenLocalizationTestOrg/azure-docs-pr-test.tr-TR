---
title: "Azure Redis Cache’i Kullanma | Microsoft Belgeleri"
description: "Azure Redis Cache ile Azure, uygulamalarınızın performansını artırmayı öğrenin"
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
ms.openlocfilehash: 3dfc026490093523446650c510dbebdd660e8b6b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-redis-cache"></a><span data-ttu-id="30de5-103">Azure Redis Cache’i kullanma</span><span class="sxs-lookup"><span data-stu-id="30de5-103">How to Use Azure Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="30de5-104">.NET</span><span class="sxs-lookup"><span data-stu-id="30de5-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="30de5-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="30de5-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="30de5-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="30de5-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="30de5-107">Java</span><span class="sxs-lookup"><span data-stu-id="30de5-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="30de5-108">Python</span><span class="sxs-lookup"><span data-stu-id="30de5-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="30de5-109">Bu kılavuz **Azure Redis Cache**’i kullanmaya başlamayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="30de5-109">This guide shows you how to get started using **Azure Redis Cache**.</span></span> <span data-ttu-id="30de5-110">Microsoft Azure Redis Cache popüler açık kaynak Redis Cache’i temel alır.</span><span class="sxs-lookup"><span data-stu-id="30de5-110">Microsoft Azure Redis Cache is based on the popular open source Redis Cache.</span></span> <span data-ttu-id="30de5-111">Microsoft tarafından yönetilen güvenli, ayrılmış bir Redis Cache’e erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="30de5-111">It gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="30de5-112">Azure Redis Cache kullanılarak oluşturulan bir önbelleğe Microsoft Azure’daki her uygulamadan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="30de5-112">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="30de5-113">Microsoft Azure Redis Cache aşağıdaki katmanlarda kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="30de5-113">Microsoft Azure Redis Cache is available in the following tiers:</span></span>

* <span data-ttu-id="30de5-114">**Temel** – Tek düğümlü.</span><span class="sxs-lookup"><span data-stu-id="30de5-114">**Basic** – Single node.</span></span> <span data-ttu-id="30de5-115">53 GB'a kadar birden çok boyut.</span><span class="sxs-lookup"><span data-stu-id="30de5-115">Multiple sizes up to 53 GB.</span></span>
* <span data-ttu-id="30de5-116">**Standart** – İki düğümlü Birincil/Çoğaltma.</span><span class="sxs-lookup"><span data-stu-id="30de5-116">**Standard** – Two-node Primary/Replica.</span></span> <span data-ttu-id="30de5-117">53 GB'a kadar birden çok boyut.</span><span class="sxs-lookup"><span data-stu-id="30de5-117">Multiple sizes up to 53 GB.</span></span> <span data-ttu-id="30de5-118">%99,9 SLA.</span><span class="sxs-lookup"><span data-stu-id="30de5-118">99.9% SLA.</span></span>
* <span data-ttu-id="30de5-119">**Premium** – İki düğümlü Birincil/Çoğaltma, En fazla 10 parça.</span><span class="sxs-lookup"><span data-stu-id="30de5-119">**Premium** – Two-node Primary/Replica with up to 10 shards.</span></span> <span data-ttu-id="30de5-120">6 GB'tan 530 GB'a kadar birden çok boyut.</span><span class="sxs-lookup"><span data-stu-id="30de5-120">Multiple sizes from 6 GB to 530 GB.</span></span> <span data-ttu-id="30de5-121">[Redis kümesi](cache-how-to-premium-clustering.md), [Redis kalıcılığı](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md) dahil tüm Standart katman özellikleri ve fazlası.</span><span class="sxs-lookup"><span data-stu-id="30de5-121">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="30de5-122">%99,9 SLA.</span><span class="sxs-lookup"><span data-stu-id="30de5-122">99.9% SLA.</span></span>

<span data-ttu-id="30de5-123">Her katman özellikler ve fiyatlandırma açısından farklıdır.</span><span class="sxs-lookup"><span data-stu-id="30de5-123">Each tier differs in terms of features and pricing.</span></span> <span data-ttu-id="30de5-124">Fiyatlandırma hakkında daha fazla bilgi için bkz. [Önbellek Fiyatlandırma Ayrıntıları][Cache Pricing Details].</span><span class="sxs-lookup"><span data-stu-id="30de5-124">For information on pricing, see [Cache Pricing Details][Cache Pricing Details].</span></span>

<span data-ttu-id="30de5-125">Bu kılavuz C\# kodu kullanarak [StackExchange.Redis][StackExchange.Redis] istemcisi kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="30de5-125">This guide shows you how to use the [StackExchange.Redis][StackExchange.Redis] client using C\# code.</span></span> <span data-ttu-id="30de5-126">Ele alınan senaryolar **bir önbellek oluşturma ve yapılandırma**, **önbellek istemcilerini yapılandırma** ve **önbelleğe nesne ekleme ve nesneleri önbellekten kaldırma** konularını içerir.</span><span class="sxs-lookup"><span data-stu-id="30de5-126">The scenarios covered include **creating and configuring a cache**, **configuring cache clients**, and **adding and removing objects from the cache**.</span></span> <span data-ttu-id="30de5-127">Azure Redis Cache’i kullanma hakkında daha fazla bilgi için bkz. [Sonraki Adımlar][Next Steps].</span><span class="sxs-lookup"><span data-stu-id="30de5-127">For more information on using Azure Redis Cache, see [Next Steps][Next Steps].</span></span> <span data-ttu-id="30de5-128">Redis Cache ile ASP.NET MVC web uygulaması oluşturmaya ilişkin adım bir öğretici için, bkz. [Redis Cache ile Web Uygulaması Oluşturma](cache-web-app-howto.md)</span><span class="sxs-lookup"><span data-stu-id="30de5-128">For a step-by-step tutorial of building an ASP.NET MVC web app with Redis Cache, see [How to create a Web App with Redis Cache](cache-web-app-howto.md).</span></span>

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a><span data-ttu-id="30de5-129">Azure Redis Cache’i kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="30de5-129">Get Started with Azure Redis Cache</span></span>
<span data-ttu-id="30de5-130">Azure Redis Cache’i kullanmaya başlamak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="30de5-130">Getting started with Azure Redis Cache is easy.</span></span> <span data-ttu-id="30de5-131">Başlamak için, bir önbellek hazırlayın ve yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="30de5-131">To get started, you provision and configure a cache.</span></span> <span data-ttu-id="30de5-132">Ardından, önbelleğe erişebilmeleri için önbellek istemcilerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="30de5-132">Next, you configure the cache clients so they can access the cache.</span></span> <span data-ttu-id="30de5-133">Önbellek istemcileri yapılandırıldıktan sonra, bunlarla çalışmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30de5-133">Once the cache clients are configured, you can begin working with them.</span></span>

* <span data-ttu-id="30de5-134">[Önbelleği oluşturma][Create the cache]</span><span class="sxs-lookup"><span data-stu-id="30de5-134">[Create the cache][Create the cache]</span></span>
* <span data-ttu-id="30de5-135">[Önbellek istemcilerini yapılandırma][Configure the cache clients]</span><span class="sxs-lookup"><span data-stu-id="30de5-135">[Configure the cache clients][Configure the cache clients]</span></span>

<a name="create-cache"></a>

## <a name="create-a-cache"></a><span data-ttu-id="30de5-136">Bir önbellek oluşturma</span><span class="sxs-lookup"><span data-stu-id="30de5-136">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="to-access-your-cache-after-its-created"></a><span data-ttu-id="30de5-137">Oluşturulduktan sonra önbelleğinize erişmek için</span><span class="sxs-lookup"><span data-stu-id="30de5-137">To access your cache after it's created</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="30de5-138">Önbelleğinizi yapılandırma hakkında daha fazla bilgi için, bkz. [Azure Redis Cache’i yapılandırma](cache-configure.md).</span><span class="sxs-lookup"><span data-stu-id="30de5-138">For more information about configuring your cache, see [How to configure Azure Redis Cache](cache-configure.md).</span></span>

<a name="NuGet"></a>

## <a name="configure-the-cache-clients"></a><span data-ttu-id="30de5-139">Önbellek istemcilerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="30de5-139">Configure the cache clients</span></span>
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

<span data-ttu-id="30de5-140">İstemci projeniz önbelleğe almak üzere yapılandırıldığında, önbelleğinizle çalışmak için aşağıdaki bölümlerde açıklanan teknikleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30de5-140">Once your client project is configured for caching, you can use the techniques described in the following sections for working with your cache.</span></span>

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a><span data-ttu-id="30de5-141">Önbelleklerle Çalışma</span><span class="sxs-lookup"><span data-stu-id="30de5-141">Working with Caches</span></span>
<span data-ttu-id="30de5-142">Bu bölümdeki adımlar Önbellek ile ortak görevler gerçekleştirmeyi açıklar.</span><span class="sxs-lookup"><span data-stu-id="30de5-142">The steps in this section describe how to perform common tasks with Cache.</span></span>

* <span data-ttu-id="30de5-143">[Önbelleğe bağlanma][Connect to the cache]</span><span class="sxs-lookup"><span data-stu-id="30de5-143">[Connect to the cache][Connect to the cache]</span></span>
* <span data-ttu-id="30de5-144">[Önbelleğe nesneler ekleme ve nesneleri önbellekten alma][Add and retrieve objects from the cache]</span><span class="sxs-lookup"><span data-stu-id="30de5-144">[Add and retrieve objects from the cache][Add and retrieve objects from the cache]</span></span>
* [<span data-ttu-id="30de5-145">Önbellekte .NET nesneleriyle çalışma</span><span class="sxs-lookup"><span data-stu-id="30de5-145">Work with .NET objects in the cache</span></span>](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-to-the-cache"></a><span data-ttu-id="30de5-146">Önbelleğe bağlanma</span><span class="sxs-lookup"><span data-stu-id="30de5-146">Connect to the cache</span></span>
<span data-ttu-id="30de5-147">Program aracılığıyla bir önbellekle çalışmak için önbelleğe başvuru gerekir.</span><span class="sxs-lookup"><span data-stu-id="30de5-147">To programmatically work with a cache, you need a reference to the cache.</span></span> <span data-ttu-id="30de5-148">Azure Redis Cache’e erişmek üzere StackExchange.Redis istemcisini kullanmak istediğiniz bir dosyanın en üstüne aşağıdakileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="30de5-148">Add the following to the top of any file from which you want to use the StackExchange.Redis client to access an Azure Redis Cache.</span></span>

    using StackExchange.Redis;

> [!NOTE]
> <span data-ttu-id="30de5-149">StackExchange.Redis istemcisi .NET Framework 4 veya üst sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="30de5-149">The StackExchange.Redis client requires .NET Framework 4 or higher.</span></span>
> 
> 

<span data-ttu-id="30de5-150">Azure Redis Cache bağlantısı `ConnectionMultiplexer` sınıfı tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="30de5-150">The connection to the Azure Redis Cache is managed by the `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="30de5-151">Bu sınıf istemci uygulamanız genelinde paylaşılmak ve yeniden kullanılmak içindir ve işlem bazında oluşturulmasına gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="30de5-151">This class should be shared and reused throughout your client application, and does not need to be created on a per operation basis.</span></span> 

<span data-ttu-id="30de5-152">Bir Azure Redis Cache’e bağlanmak ve bağlı bir `ConnectionMultiplexer` örneği döndürülmesi için, statik `Connect` yöntemini çağırın ve önbellek uç noktasını ve anahtarı geçirin.</span><span class="sxs-lookup"><span data-stu-id="30de5-152">To connect to an Azure Redis Cache and be returned an instance of a connected `ConnectionMultiplexer`, call the static `Connect` method and pass in the cache endpoint and key.</span></span> <span data-ttu-id="30de5-153">Parola parametresi olarak Azure portalında oluşturulan anahtarı kullanın.</span><span class="sxs-lookup"><span data-stu-id="30de5-153">Use the key generated from the Azure portal as the password parameter.</span></span>

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> <span data-ttu-id="30de5-154">Uyarı: Kimlik bilgilerini asla kaynak kodunda depolamayın.</span><span class="sxs-lookup"><span data-stu-id="30de5-154">Warning: Never store credentials in source code.</span></span> <span data-ttu-id="30de5-155">Bu örneği basit tutmak için bunları kaynak kodunda gösteriyorum.</span><span class="sxs-lookup"><span data-stu-id="30de5-155">To keep this sample simple, I’m showing them in the source code.</span></span> <span data-ttu-id="30de5-156">Kimlik bilgilerini depolamaya hakkında bilgi için, bkz. [Uygulama Dizeleri ve Bağlantı Dizeleri Nasıl Çalışır?][How Application Strings and Connection Strings Work]</span><span class="sxs-lookup"><span data-stu-id="30de5-156">See [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] for information on how to store credentials.</span></span>
> 
> 

<span data-ttu-id="30de5-157">SSL kullanmak istemiyorsanız, `ssl=false` ayarlayın ya da `ssl` parametresini atlayın.</span><span class="sxs-lookup"><span data-stu-id="30de5-157">If you don't want to use SSL, either set `ssl=false` or omit the `ssl` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="30de5-158">SSL olmayan bağlantı noktasın yeni önbellekler için varsayılan olarak devre dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="30de5-158">The non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="30de5-159">SSL olmayan bağlantı noktası etkinleştirme hakkında yönergeler için bkz. [Erişim Bağlantı Noktaları](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="30de5-159">For instructions on enabling the non-SSL port, see [Access Ports](cache-configure.md#access-ports).</span></span>
> 
> 

<span data-ttu-id="30de5-160">Uygulamanızda bir `ConnectionMultiplexer` örneği paylaşmaya ilişkin bir yaklaşım, aşağıdaki örneğe benzer bir bağlı örnek döndüren statik özelliğe sahip olmaktır.</span><span class="sxs-lookup"><span data-stu-id="30de5-160">One approach to sharing a `ConnectionMultiplexer` instance in your application is to have a static property that returns a connected instance, similar to the following example.</span></span> <span data-ttu-id="30de5-161">Bu yaklaşım yalnızca tek bir bağlı `ConnectionMultiplexer` örneği başlatmak için iş parçacığı güvenli bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="30de5-161">This approach provides a thread-safe way to initialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="30de5-162">Bu örneklerde `abortConnect` false olarak ayarlanır; bunun anlamı Azure Redis Cache’e bağlantı kurulmasa bile çağrının başarılı olacağıdır.</span><span class="sxs-lookup"><span data-stu-id="30de5-162">In these examples `abortConnect` is set to false, which means that the call succeeds even if a connection to the Azure Redis Cache is not established.</span></span> <span data-ttu-id="30de5-163">`ConnectionMultiplexer` temel özelliklerinden biri ağ sorunu ya da diğer nedenler çözümlendiğinde önbellek bağlantısını otomatik olarak geri yüklemesidir.</span><span class="sxs-lookup"><span data-stu-id="30de5-163">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity to the cache once the network issue or other causes are resolved.</span></span>

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

<span data-ttu-id="30de5-164">Gelişmiş bağlantı yapılandırma seçenekleri hakkında daha fazla bilgi için bkz:.[StackExchange.Redis yapılandırma modeli][StackExchange.Redis configuration model].</span><span class="sxs-lookup"><span data-stu-id="30de5-164">For more information on advanced connection configuration options, see [StackExchange.Redis configuration model][StackExchange.Redis configuration model].</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="30de5-165">Bağlantı kurulduktan sonra, `ConnectionMultiplexer.GetDatabase` yöntemini çağırarak Redis Cache veritabanına bir başvuru döndürün.</span><span class="sxs-lookup"><span data-stu-id="30de5-165">Once the connection is established, return a reference to the redis cache database by calling the `ConnectionMultiplexer.GetDatabase` method.</span></span> <span data-ttu-id="30de5-166">`GetDatabase` yönteminden döndürülen nesne küçük, geçişli bir nesnedir ve depolanması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="30de5-166">The object returned from the `GetDatabase` method is a lightweight pass-through object and does not need to be stored.</span></span>

    // Connection refers to a property that returns a ConnectionMultiplexer
    // as shown in the previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using the cache object...
    // Simple put of integral data types into the cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from the cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

<span data-ttu-id="30de5-167">Azure Redis Cache’ler, bir Redis Cache’teki verileri mantıksal olarak ayırmak için yapılandırılabilir sayıda veritabanına (varsayılan değer 16) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="30de5-167">Azure Redis caches have a configurable number of databases (default of 16) that can be used to logically separate the data within a Redis cache.</span></span> <span data-ttu-id="30de5-168">Daha fazla bilgi için bkz. [Redis veritabanı nedir?](cache-faq.md#what-are-redis-databases) ve [Varsayılan Redis sunucu yapılandırması](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="30de5-168">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span>

<span data-ttu-id="30de5-169">Artık Azure Redis Cache örneğine bağlanmayı ve önbellek veritabanına bir başvuru döndürmeyi bildiğinize göre, şimdi önbellekle çalışmaya göz atalım.</span><span class="sxs-lookup"><span data-stu-id="30de5-169">Now that you know how to connect to an Azure Redis Cache instance and return a reference to the cache database, let's look at working with the cache.</span></span>

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-the-cache"></a><span data-ttu-id="30de5-170">Önbelleğe nesneler ekleme ve nesneleri önbellekten alma</span><span class="sxs-lookup"><span data-stu-id="30de5-170">Add and retrieve objects from the cache</span></span>
<span data-ttu-id="30de5-171">`StringSet` ve `StringGet` yöntemleri.kullanılarak öğeleri bir önbellekte depolanabilir ve önbellekten alınabilir.</span><span class="sxs-lookup"><span data-stu-id="30de5-171">Items can be stored in and retrieved from a cache by using the `StringSet` and `StringGet` methods.</span></span>

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

<span data-ttu-id="30de5-172">Redis, Redis dizeleri kadar veri depolar, ancak bu dizeler önbellekte .NET nesneleri depolarken kullanılabilecek seri hale getirilmiş ikili veriler dahil, birçok veri türünü içerebilir.</span><span class="sxs-lookup"><span data-stu-id="30de5-172">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in the cache.</span></span>

<span data-ttu-id="30de5-173">`StringGet` çağrılırken, nesne varsa, döndürülür ve nesne yoksa, `null` döndürülür.</span><span class="sxs-lookup"><span data-stu-id="30de5-173">When calling `StringGet`, if the object exists, it is returned, and if it does not, `null` is returned.</span></span> <span data-ttu-id="30de5-174">`null` döndürülürse istenen veri kaynağından değeri alabilir ve sonra kullanmak için önbellekte saklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30de5-174">If `null` is returned, you can retrieve the value from the desired data source and store it in the cache for subsequent use.</span></span> <span data-ttu-id="30de5-175">Bu kullanım şekli edilgen önbellek düzeni olarak bilinir.</span><span class="sxs-lookup"><span data-stu-id="30de5-175">This usage pattern is known as the cache-aside pattern.</span></span>

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // The item keyed by "key1" is not in the cache. Obtain
        // it from the desired data source and add it to the cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

<span data-ttu-id="30de5-176">Aynı zamanda aşağıdaki örnekte gösterildiği gibi `RedisValue` kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30de5-176">You can also use `RedisValue`, as shown in the following example.</span></span> <span data-ttu-id="30de5-177">`RedisValue`, tam sayı veri türleriyle çalışmaya yönelik örtük işleçlere sahiptir ve önbelleğe alınan öğe için `null` beklenen bir değerse yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="30de5-177">`RedisValue` has implicit operators for working with integral data types, and can be useful if `null` is an expected value for a cached item.</span></span>


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


<span data-ttu-id="30de5-178">Bir öğenin önbellekte sona erme tarihini belirtmek için, `StringSet` dizesine ait `TimeSpan` parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="30de5-178">To specify the expiration of an item in the cache, use the `TimeSpan` parameter of `StringSet`.</span></span>

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-the-cache"></a><span data-ttu-id="30de5-179">Önbellekte .NET nesneleriyle çalışma</span><span class="sxs-lookup"><span data-stu-id="30de5-179">Work with .NET objects in the cache</span></span>
<span data-ttu-id="30de5-180">Azure Redis Cache temel veri türlerinin yanı sıra .NET nesnelerini de önbelleğe alabilir, ancak bir .NET nesnesini önbelleğe alabilmek için seri hale getirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="30de5-180">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="30de5-181">Bu .NET nesne serileştirmesi uygulama geliştiricisinin sorumluluğundadır ve geliştiriciye seri hale getirici tercihinde esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="30de5-181">This .NET object serialization is the responsibility of the application developer, and gives the developer flexibility in the choice of the serializer.</span></span>

<span data-ttu-id="30de5-182">Nesneleri seri hale getirmenin basit bir yolu [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1)’te `JsonConvert` seri hale getirme yöntemleri kullanmak ve JSON’a ve JSON’dan seri hale getirmektir.</span><span class="sxs-lookup"><span data-stu-id="30de5-182">One simple way to serialize objects is to use the `JsonConvert` serialization methods in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) and serialize to and from JSON.</span></span> <span data-ttu-id="30de5-183">Aşağıdaki örnekte bir `Employee` nesnesi örneği kullanılarak al ve ayarla seçeneği gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="30de5-183">The following example shows a get and set using an `Employee` object instance.</span></span>

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

    // Store to cache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a><span data-ttu-id="30de5-184">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="30de5-184">Next Steps</span></span>
<span data-ttu-id="30de5-185">Artık temel bilgileri öğrendiğinize göre, Azure Redis Cache hakkında daha fazla bilgi edinmek için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="30de5-185">Now that you've learned the basics, follow these links to learn more about Azure Redis Cache.</span></span>

* <span data-ttu-id="30de5-186">Azure Redis Cache için ASP.NET sağlayıcılarına göz atın.</span><span class="sxs-lookup"><span data-stu-id="30de5-186">Check out the ASP.NET providers for Azure Redis Cache.</span></span>
  * [<span data-ttu-id="30de5-187">Azure Redis Oturum Durumu Sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="30de5-187">Azure Redis Session State Provider</span></span>](cache-aspnet-session-state-provider.md)
  * [<span data-ttu-id="30de5-188">Azure Redis Cache ASP.NET Çıktı Önbelleği Sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="30de5-188">Azure Redis Cache ASP.NET Output Cache Provider</span></span>](cache-aspnet-output-cache-provider.md)
* <span data-ttu-id="30de5-189">Önbelleğinizin sistem durumunu [izleyebilmeniz](cache-how-to-monitor.md) için [önbellek tanılamayı etkinleştirin](cache-how-to-monitor.md#enable-cache-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="30de5-189">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) the health of your cache.</span></span> <span data-ttu-id="30de5-190">Azure portalında ölçümleri görüntüleyebilir ve ayrıca istediğiniz araçları kullanarak bunları [indirebilir ve gözden geçirebilirsiniz](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring).</span><span class="sxs-lookup"><span data-stu-id="30de5-190">You can view the metrics in the Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using the tools of your choice.</span></span>
* <span data-ttu-id="30de5-191">[StackExchange.Redis önbellek istemcisi belgelerine][StackExchange.Redis cache client documentation] bakın.</span><span class="sxs-lookup"><span data-stu-id="30de5-191">Check out the [StackExchange.Redis cache client documentation][StackExchange.Redis cache client documentation].</span></span>
  * <span data-ttu-id="30de5-192">Azure Redis Cache birçok Redis istemcisinden ve geliştirme dilinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="30de5-192">Azure Redis Cache can be accessed from many Redis clients and development languages.</span></span> <span data-ttu-id="30de5-193">Daha fazla bilgi için bkz. [http://redis.io/clients][http://redis.io/clients].</span><span class="sxs-lookup"><span data-stu-id="30de5-193">For more information, see [http://redis.io/clients][http://redis.io/clients].</span></span>
* <span data-ttu-id="30de5-194">Azure Redis Cache ayrıca Redsmin ve Redis Desktop Manager gibi üçüncü taraf hizmetler ve araçlarla birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="30de5-194">Azure Redis Cache can also be used with third-party services and tools such as Redsmin and Redis Desktop Manager.</span></span>
  * <span data-ttu-id="30de5-195">Redsmin hakkında daha fazla bilgi için bkz. [Azure Redis bağlantı dizesi alma ve Redsmin ile birlikte kullanma][How to retrieve an Azure Redis connection string and use it with Redsmin].</span><span class="sxs-lookup"><span data-stu-id="30de5-195">For more information about Redsmin, see [How to retrieve an Azure Redis connection string and use it with Redsmin][How to retrieve an Azure Redis connection string and use it with Redsmin].</span></span>
  * <span data-ttu-id="30de5-196">Azure Redis Cache’teki verilerinize erişin ve bunları [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager) kullanan bir GUI ile inceleyin.</span><span class="sxs-lookup"><span data-stu-id="30de5-196">Access and inspect your data in Azure Redis Cache with a GUI using [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span></span>
* <span data-ttu-id="30de5-197">[redis][redis] belgelerine bakın ve [redis veri türleri][redis data types] hakkında bilgi edinin ve [Redis veri türlerine on beş dakikalık bir giriş][a fifteen minute introduction to Redis data types] sayfasına göz atın.</span><span class="sxs-lookup"><span data-stu-id="30de5-197">See the [redis][redis] documentation and read about [redis data types][redis data types] and [a fifteen minute introduction to Redis data types][a fifteen minute introduction to Redis data types].</span></span>

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction to Azure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project to Use Azure Caching]: #prepare-vs
[Configure Your Application to Use Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create the cache]: #create-cache
[Configure the cache]: #enable-caching
[Configure the cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect to the cache]: #connect-to-cache
[Add and retrieve objects from the cache]: #add-object
[Specify the expiration of an object in the cache]: #specify-expiration
[Store ASP.NET session state in the cache]: #store-session


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
[How to retrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How to Configure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set the Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in the cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate to Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups to manage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction to Redis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/


