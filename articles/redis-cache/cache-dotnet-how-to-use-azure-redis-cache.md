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
# <a name="how-toouse-azure-redis-cache"></a>Nasıl tooUse Azure Redis önbelleği
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Bu kılavuz size nasıl tooget kullanmaya gösterir **Azure Redis önbelleği**. Microsoft Azure Redis önbelleği hello popüler açık kaynak Redis önbelleğini temel alır. Size verir Microsoft tarafından yönetilen tooa güvenli, ayrılmış bir Redis önbelleğine erişmek. Azure Redis Cache kullanılarak oluşturulan bir önbelleğe Microsoft Azure’daki her uygulamadan erişilebilir.

Microsoft Azure Redis önbelleği Katmanlar izleyerek hello kullanılabilir:

* **Temel** – Tek düğümlü. Birden çok too53 GB boyutları.
* **Standart** – İki düğümlü Birincil/Çoğaltma. Birden çok too53 GB boyutları. %99,9 SLA.
* **Premium** – iki düğümlü birincil/çoğaltma ile too10 parça ayarlama. 6 GB too530 GB birden çok boyut. [Redis kümesi](cache-how-to-premium-clustering.md), [Redis kalıcılığı](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md) dahil tüm Standart katman özellikleri ve fazlası. %99,9 SLA.

Her katman özellikler ve fiyatlandırma açısından farklıdır. Fiyatlandırma hakkında daha fazla bilgi için bkz. [Önbellek Fiyatlandırma Ayrıntıları][Cache Pricing Details].

Bu kılavuz size nasıl gösterir toouse hello [StackExchange.Redis] [ StackExchange.Redis] C kullanarak istemci\# kodu. Merhaba kapsanan senaryolar dahil **oluşturma ve bir önbellek yapılandırma**, **önbellek istemcilerini yapılandırma**, ve **ekleme ve nesneleri hello önbellekten kaldırma**. Azure Redis Cache’i kullanma hakkında daha fazla bilgi için bkz. [Sonraki Adımlar][Next Steps]. Bir ASP.NET MVC Redis önbelleği ile web uygulaması oluşturmanın adım adım öğretici için bkz [nasıl toocreate bir Web uygulamasını Redis önbelleği ile](cache-web-app-howto.md).

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a>Azure Redis Cache’i kullanmaya başlama
Azure Redis Cache’i kullanmaya başlamak kolaydır. tooget başlatıldı, sağlamak ve bir önbellek yapılandırın. Ardından, hello önbelleğe erişebilmeleri hello önbellek istemcilerini yapılandırın. Merhaba önbellek istemcileri yapılandırıldıktan sonra bunlarla çalışmaya başlayabilirsiniz.

* [Merhaba önbelleği oluşturma][Create hello cache]
* [Merhaba önbellek istemcilerini yapılandırın][Configure hello cache clients]

<a name="create-cache"></a>

## <a name="create-a-cache"></a>Bir önbellek oluşturma
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a>tooaccess önbelleğiniz sonraki oluşturulur
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

Önbelleğinizi yapılandırma hakkında daha fazla bilgi için bkz: [nasıl tooconfigure Azure Redis önbelleği](cache-configure.md).

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a>Merhaba önbellek istemcilerini yapılandırın
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

İstemci projeniz önbelleğe almak için yapılandırıldıktan sonra önbelleğinizle çalışmak için bölümleri aşağıdaki hello açıklanan hello teknikleri kullanabilirsiniz.

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a>Önbelleklerle Çalışma
Bu bölümdeki Hello adımları nasıl önbellekle tooperform ortak görevler açıklanmaktadır.

* [Toohello Önbelleği'ne bağlama][Connect toohello cache]
* [Ekleme ve nesneleri hello önbellekten alma][Add and retrieve objects from hello cache]
* [Merhaba önbelleğinde .NET nesneleriyle çalışma](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a>Toohello Önbelleği'ne bağlama
tooprogrammatically iş sahip bir önbellek, bir başvuru toohello önbellek gerekir. Toohello üst toouse hello StackExchange.Redis istemcisi tooaccess bir Azure Redis önbelleği istediğiniz herhangi bir dosyasının içinden aşağıdaki hello ekleyin.

    using StackExchange.Redis;

> [!NOTE]
> Merhaba StackExchange.Redis istemcisi .NET Framework 4 veya üstünü gerektirir.
> 
> 

Azure Redis önbelleği hello tarafından yönetilen bağlantı toohello hello `ConnectionMultiplexer` sınıfı. Bu sınıf, paylaşılan ve istemci uygulamanız genelinde yeniden ve işlem bazında oluşturulan toobe gerekli değildir. 

Azure Redis önbelleği tooconnect tooan ve bağlı bir örneği döndürülmesi `ConnectionMultiplexer`, çağrı hello statik `Connect` yöntemi ve hello geçişinde önbellek uç noktasını ve anahtarı. Merhaba hello parola parametresi olarak Azure portalında üretilen hello anahtarı kullanın.

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> Uyarı: Kimlik bilgilerini asla kaynak kodunda depolamayın. tookeep Bu örneği basit ı bunları hello kaynak kodunda gösteren. Bkz: [nasıl uygulama dizeleri ve bağlantı dizeleri çalışma] [ How Application Strings and Connection Strings Work] hakkında bilgi için toostore kimlik bilgileri.
> 
> 

Toouse SSL istemiyorsanız ya da ayarlayın `ssl=false` veya hello çıkarın `ssl` parametresi.

> [!NOTE]
> Merhaba SSL olmayan bağlantı noktasının yeni önbellekler için varsayılan olarak devre dışıdır. Merhaba SSL olmayan bağlantı noktasının etkinleştirilmesi ile ilgili yönergeler için bkz: [erişim bağlantı noktaları](cache-configure.md#access-ports).
> 
> 

Bir yaklaşım toosharing bir `ConnectionMultiplexer` örneğidir uygulamanızda toohave aşağıdaki örneğine benzer toohello bir bağlı örnek döndüren statik özelliğe. Bu yaklaşım, bağlı tek bir iş parçacığı açısından güvenli şekilde tooinitialize sağlar `ConnectionMultiplexer` örneği. Bu örneklerde `abortConnect` bağlantı toohello Azure Redis önbelleği bile kurulamazsa hello çağrı başarılı anlamına gelir kümesi toofalse değil. Temel özelliklerinden biri `ConnectionMultiplexer` hello ağ sorunu ya da diğer nedenler çözüldükten sonra otomatik olarak bağlantı toohello önbellek yükler emin olan.

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

Gelişmiş bağlantı yapılandırma seçenekleri hakkında daha fazla bilgi için bkz:.[StackExchange.Redis yapılandırma modeli][StackExchange.Redis configuration model].

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

Merhaba bağlantı kurulduktan sonra bir başvuru toohello redis önbelleği veritabanına göre arama hello dönmek `ConnectionMultiplexer.GetDatabase` yöntemi. Merhaba hello döndürülen `GetDatabase` yöntemi basit bir geçiş nesnesi ve depolanan toobe gerekli değildir.

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

Azure Redis önbellekleri yapılandırılabilir Redis önbelleği içinde kullanılan toologically ayrı hello veri olabilir (varsayılan 16) veritabanlarının sahiptir. Daha fazla bilgi için bkz. [Redis veritabanı nedir?](cache-faq.md#what-are-redis-databases) ve [Varsayılan Redis sunucu yapılandırması](cache-configure.md#default-redis-server-configuration).

Veritabanı tooconnect tooan Azure Redis önbelleği örneği ve return başvuru toohello nasıl önbelleğe bildiğinize göre hello önbellekle çalışmaya konumundaki bakalım.

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a>Ekleme ve nesneleri hello önbellekten alma
Öğeleri depolanır ve hello kullanarak önbellekten `StringSet` ve `StringGet` yöntemleri.

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

Çoğu veri Redis dizeleri, ancak bu dizeler olarak pek çok .NET nesneleri depolarken kullanılabilecek hello önbelleğinde seri hale getirilmiş ikili veriler dahil olmak üzere veri türünü içerebilir depoları redis.

Çağrılırken `StringGet`, hello nesne varsa, döndürülür ve onu yoksa `null` döndürülür. Varsa `null` döndürülür, hello değeri hello istenen veri kaynağından almak ve daha sonra kullanılmak hello önbelleğindeki saklayın. Bu kullanım deseni hello edilgen önbellek düzeni bilinir.

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

Aynı zamanda `RedisValue`hello aşağıdaki örnekte gösterildiği gibi. `RedisValue`, tam sayı veri türleriyle çalışmaya yönelik örtük işleçlere sahiptir ve önbelleğe alınan öğe için `null` beklenen bir değerse yararlı olabilir.


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


bir öğenin hello önbelleğindeki kullanım hello toospecify hello sona erme `TimeSpan` parametresinin `StringSet`.

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a>Merhaba önbelleğinde .NET nesneleriyle çalışma
Azure Redis Cache temel veri türlerinin yanı sıra .NET nesnelerini de önbelleğe alabilir, ancak bir .NET nesnesini önbelleğe alabilmek için seri hale getirilmesi gerekir. Bu .NET nesne seri hale getirme hello uygulama geliştiricisi hello sorumluluğundadır ve hello seri hale getirici hello tercihini hello Geliştirici esnekliği sağlar.

Bir basit yol tooserialize nesneleri olan toouse hello `JsonConvert` seri hale getirme yöntemleri [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) ve tooand JSON öğesinden seri. Merhaba aşağıdaki örnek bir kullanılarak Al ve Ayarla gösterir bir `Employee` nesne örneği.

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

## <a name="next-steps"></a>Sonraki Adımlar
Merhaba öğrendiğinize göre Azure Redis önbelleği hakkında daha fazla bu bağlantılar toolearn izleyin.

* Out Hello Azure Redis önbelleği için ASP.NET sağlayıcılarına denetleyin.
  * [Azure Redis Oturum Durumu Sağlayıcısı](cache-aspnet-session-state-provider.md)
  * [Azure Redis Cache ASP.NET Çıktı Önbelleği Sağlayıcısı](cache-aspnet-output-cache-provider.md)
* [Önbellek tanılamayı etkinleştirin](cache-how-to-monitor.md#enable-cache-diagnostics) , böylece [İzleyici](cache-how-to-monitor.md) hello önbelleğinizin sistem durumunu. Hello Azure portal ve ölçümler için de hello görüntüleyebilirsiniz [indirebilir ve gözden](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) bunları tercih ettiğiniz hello araçlarını kullanma.
* Merhaba denetleyin [StackExchange.Redis önbellek istemcisi belgeleri][StackExchange.Redis cache client documentation].
  * Azure Redis Cache birçok Redis istemcisinden ve geliştirme dilinden erişilebilir. Daha fazla bilgi için bkz. [http://redis.io/clients][http://redis.io/clients].
* Azure Redis Cache ayrıca Redsmin ve Redis Desktop Manager gibi üçüncü taraf hizmetler ve araçlarla birlikte kullanılabilir.
  * Redsmin birlikte hakkında daha fazla bilgi için bkz: [nasıl tooretrieve bir Azure Redis bağlantı dizesi ve redsmin ile birlikte][How tooretrieve an Azure Redis connection string and use it with Redsmin].
  * Azure Redis Cache’teki verilerinize erişin ve bunları [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager) kullanan bir GUI ile inceleyin.
* Merhaba bkz [redis] [ redis] belgeleri ve hakkında bilgi [redis veri türleri] [ redis data types] ve [on beş dakikalık bir giriş tooRedis veri türleri][a fifteen minute introduction tooRedis data types].

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


