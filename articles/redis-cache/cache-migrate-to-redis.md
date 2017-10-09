---
title: "aaaMigrate yönetilen önbellek hizmeti uygulamaları tooRedis - Azure | Microsoft Docs"
description: "Bilgi nasıl toomigrate yönetilen önbellek hizmeti ve rol içi önbelleği uygulamaları tooAzure Redis önbelleği"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 041f077b-8c8e-4d7c-a3fc-89d334ed70d6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/30/2017
ms.author: sdanie
ms.openlocfilehash: bd81722820acf0d2637828fbb6100c723aafeba5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-managed-cache-service-tooazure-redis-cache"></a>Yönetilen önbellek hizmeti tooAzure Redis Önbelleği ' geçiş
Azure yönetilen önbellek hizmeti tooAzure Redis önbelleği kullanan, uygulamaları geçirmeye önbelleğe alma, uygulamanız tarafından kullanılan hello yönetilen önbellek hizmeti özelliklere bağlı olarak küçük değişiklikler tooyour uygulama ile gerçekleştirilebilir. Merhaba API'leri tam hello çalışırken aynı benzer oldukları ve küçük değişiklikler ile yönetilen önbellek hizmeti tooaccess bir önbellek kullanan mevcut kodunuzu çoğunu yeniden kullanılabilir. Bu konu nasıl toomake hello gerekli yapılandırma ve uygulama değişiklikleri toomigrate yönetilen önbellek hizmeti uygulamaları toouse Azure Redis önbelleği gösterir ve bazı Azure Redis önbelleği hello özelliklerini kullanılan tooimplement hello işlev nasıl olabilir gösterir Yönetilen önbellek hizmeti önbelleği.

>[!NOTE]
>Yönetilen önbellek hizmeti ve rol içi önbelleği [Çekildi](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/) 30 Kasım 2016. Toomigrate tooAzure Redis önbelleği istediğiniz tüm rol içi önbelleği dağıtımları varsa, bu makaledeki hello adımları izleyebilirsiniz.

## <a name="migration-steps"></a>Geçiş adımları
Aşağıdaki adımları hello gerekli toomigrate yönetilen önbellek hizmeti uygulama toouse Azure Redis Önbelleği ' dir.

* Yönetilen önbellek hizmeti özellikleri tooAzure Redis önbelleği eşleme
* Önbelleği teklifini seçin
* Bir önbellek oluşturma
* Merhaba önbellek istemcilerini yapılandırın
  * Merhaba yönetilen önbellek hizmet yapılandırmasını Kaldır
  * Merhaba StackExchange.Redis NuGet paketi kullanarak bir önbellek istemcisini yapılandırma
* Yönetilen önbellek hizmeti kodunu taşıma
  * Merhaba ConnectionMultiplexer sınıfını kullanarak toohello Önbelleği'ne bağlama
  * Merhaba önbelleğinde erişim temel veri türleri
  * Merhaba önbelleğinde .NET nesneleriyle çalışma
* ASP.NET oturum durumu ve çıktı tooAzure Redis önbelleği önbelleği geçirme 

## <a name="map-managed-cache-service-features-tooazure-redis-cache"></a>Yönetilen önbellek hizmeti özellikleri tooAzure Redis önbelleği eşleme
Azure yönetilen önbellek hizmeti ve Azure Redis önbelleği benzer, ancak bazı özelliklerine farklı şekillerde uygulamak. Bu bölümde bazı hello farklar açıklanmaktadır ve Azure Redis Önbelleği'nde hello yönetilen önbellek hizmeti özelliklerini uygulanmasına yönelik rehberlik sağlar.

| Yönetilen önbellek hizmeti özelliği | Yönetilen önbellek hizmeti desteği | Azure Redis önbelleği desteği |
| --- | --- | --- |
| Adlandırılmış önbellekler |Varsayılan önbellek yapılandırılır ve hello adlandırılan önbellekler standart ve Premium önbellek teklifleri toonine ek yedeklemek isterseniz yapılandırılabilir. |Azure Redis önbellekleri yapılandırılabilir benzer bir işlevsellik toonamed önbelleğe kullanılan tooimplement olabilir (varsayılan 16) veritabanlarının sahiptir. Daha fazla bilgi için bkz. [Redis veritabanı nedir?](cache-faq.md#what-are-redis-databases) ve [Varsayılan Redis sunucu yapılandırması](cache-configure.md#default-redis-server-configuration). |
| Yüksek kullanılabilirlik |Merhaba standart ve Premium önbellek teklifleri hello önbelleğindeki öğeler için yüksek kullanılabilirlik sağlar. Öğeleri tooa hatası kaybolursa hello öğeleri hello önbelleğinde yedek kopyalarını yine kullanılabilir durumdadır. Toohello ikincil önbellek zaman uyumlu olarak yapılan yazar. |Yüksek kullanılabilirlik (her parça Premium önbelleğinde birincil/çoğaltma çifti sahiptir) bir iki düğümlü birincil/çoğaltma yapılandırması olan hello standart ve Premium önbellek tekliflerini, kullanılabilir. Zaman uyumsuz olarak yazar toohello çoğaltma yapılır. Daha fazla bilgi için bkz: [Azure Redis önbelleği fiyatlandırma](https://azure.microsoft.com/pricing/details/cache/). |
| Bildirimler |Bir adlandırılmış önbelleği istemcileri tooreceive zaman uyumsuz bildirimleri önbellek işlemleri çeşitli olduğunda ortaya sağlar. |İstemci uygulamaları, Redis pub/alt kullanabilir veya [Keyspace bildirimleri](cache-configure.md#keyspace-notifications-advanced-settings) tooachieve benzer bir işlevsellik toonotifications. |
| Yerel önbellek |Önbelleğe alınan nesnelerin bir kopyasını çok hızlı erişim için hello istemcisinde yerel olarak depolar. |İstemci uygulamaları tooimplement bir sözlük veya benzer veri yapısı kullanarak bu işlevselliği gerekir. |
| Çıkarma İlkesi |None veya LRU. Merhaba varsayılan ilke LRU olur. |Azure Redis önbelleği çıkarma ilkelere hello destekler: geçici lru allkeys lru, geçici rastgele, allkeys rastgele, geçici ttl, noeviction. Merhaba varsayılan ilke geçici lru olur. Daha fazla bilgi için bkz: [varsayılan Redis sunucu yapılandırması](cache-configure.md#default-redis-server-configuration). |
| Süre sonu ilkesi |Merhaba varsayılan süre sonu ilkesi mutlak ve hello varsayılan sona erme aralığını on dakika. Kayan ve hiçbir zaman ilkeler de kullanılabilir. |Varsayılan olarak hello önbelleğindeki öğeler son kullanma tarihi, ancak bir sona erme önbellek kümesi aşırı kullanarak bir yazma başına temelinde yapılandırılabilir. Daha fazla bilgi için bkz: [ekleme ve alma nesneleri hello önbelleğinden](cache-dotnet-how-to-use-azure-redis-cache.md#add-and-retrieve-objects-from-the-cache). |
| Bölgeler ve etiketleme |Bölgeler önbelleğe alınmış öğeleri için alt grupları var. Bölgeler, önbelleğe alınmış öğelerin hello ek açıklama etiketleri adlı ek açıklama dizelerle de destekler. Bölgeler bu bölgede herhangi etiketli öğelerinde hello özelliği tooperform arama işlemleri destekler. Bir bölge içindeki tüm öğeler tek bir düğüm hello önbellek küme içinde yer alır. |(Redis kümesi etkinleştirilmediği sürece) yönetilen önbellek hizmeti bölgeler hello kavramı uygulanamaz Redis önbelleği tek bir düğüm oluşur. Aramayı destekler ve joker işlemleri açıklayıcı etiketler hello anahtar adları içinde katıştırılmış ve daha sonra kullanılan tooretrieve hello öğeleri için anahtarlar alınırken redis. Redis kullanarak etiketleme bir çözüm uygulama örneği için bkz: [Redis ile etiketleme önbellek uygulama](http://stackify.com/implementing-cache-tagging-redis/). |
| Seri hale getirme |Yönetilen önbellek NetDataContractSerializer, BinaryFormatter ve özel serileştiricileri hello kullanımını destekler. Merhaba, NetDataContractSerializer varsayılandır. |Bunu hello hello istemci uygulama tooserialize .NET nesneleri bunları hello seçiminde toohello istemci uygulama geliştiricisi yukarı hello seri hale getirici, hello önbelleğine yerleştirmeden önce sorumluluğundadır. Daha fazla bilgi ve örnek kod için bkz: [hello önbelleğinde .NET nesneleriyle çalışma](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache). |
| Önbellek öykünücüsü |Yönetilen önbellek yerel önbelleği öykünücü sağlar. |Azure Redis önbelleği bir öykünücü sahip değildir, ancak yapabilecekleriniz [redis server.exe hello MSOpenTech derlemesinde yerel olarak çalıştırma](cache-faq.md#cache-emulator) tooprovide bir öykünücü deneyimi. |

## <a name="choose-a-cache-offering"></a>Önbelleği teklifini seçin
Microsoft Azure Redis önbelleği Katmanlar izleyerek hello kullanılabilir:

* **Temel** – Tek düğümlü. Birden çok too53 GB boyutları.
* **Standart** – İki düğümlü Birincil/Çoğaltma. Birden çok too53 GB boyutları. %99,9 SLA.
* **Premium** – iki düğümlü birincil/çoğaltma ile too10 parça ayarlama. 6 GB too530 GB birden çok boyut. [Redis kümesi](cache-how-to-premium-clustering.md), [Redis kalıcılığı](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md) dahil tüm Standart katman özellikleri ve fazlası. %99,9 SLA.

Her katman özellikler ve fiyatlandırma açısından farklıdır. Merhaba özellikleri daha sonra bu kılavuzdaki ve fiyatlandırma hakkında daha fazla bilgi için kapsanan bkz [önbellek fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/cache/).

Geçiş için bir başlangıç noktası, önceki yönetilen önbellek hizmeti önbelleği hello boyutunu eşleşen toopick hello boyutu ve yukarı veya Aşağı'i, uygulamanızın hello gereksinimlerine bağlı olarak ölçeklendirin. Merhaba sağ Azure Redis önbelleği teklifini seçme konusunda daha fazla yönergeler için bkz: [hangi Redis önbelleği teklifini ve boyutunu kullanmalıyım?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).

## <a name="create-a-cache"></a>Bir önbellek oluşturma
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="configure-hello-cache-clients"></a>Merhaba önbellek istemcilerini yapılandırın
Merhaba önbellek oluşturulan ve yapılandırıldıktan sonra hello sonraki adım tooremove hello yönetilen önbellek hizmeti yapılandırması ve hello ekleme önbellek istemcilerinin hello önbellek erişebilmesi için hello Azure Redis önbelleği yapılandırması ve başvurular ekleyin.

* Merhaba yönetilen önbellek hizmet yapılandırmasını Kaldır
* Merhaba StackExchange.Redis NuGet paketi kullanarak bir önbellek istemcisini yapılandırma

### <a name="remove-hello-managed-cache-service-configuration"></a>Merhaba yönetilen önbellek hizmet yapılandırmasını Kaldır
Hello önce istemci uygulamalar Azure Redis önbelleği için hello var olan yönetilen önbellek hizmeti yapılandırmasını yapılandırılabilir ve derleme başvurularını hello yönetilen önbellek hizmeti NuGet paketi kaldırarak kaldırılması gerekir.

toouninstall hello yönetilen önbellek hizmeti NuGet paketini sağ tıklatın, hello istemci projesinde **Çözüm Gezgini** ve **NuGet paketlerini Yönet**. Select hello **yüklü paketleri** düğümü ve türü W**indowsAzure.Caching** hello paketler kutusunu araması yaparak yüklü. Seçin **Windows** **Azure önbelleği** (veya **Windows** **Azure önbelleğe alma** hello NuGet paketi hello sürümüne bağlı olarak), tıklatın **Kaldırma**ve ardından **Kapat**.

![Azure yönetilen önbellek hizmeti NuGet Paketi'ni Kaldır](./media/cache-migrate-to-redis/IC757666.jpg)

Kaldırma hello yönetilen önbellek hizmeti NuGet paketi hello yönetilen önbellek hizmeti derlemeler ve hello yönetilen önbellek hizmeti girişleri hello app.config veya web.config hello istemci uygulamasının kaldırır. Bazı özelleştirilmiş ayarları hello NuGet paketi kaldırırken kaldırılmamış olabilir çünkü web.config veya app.config açın ve öğeleri aşağıdaki o hello tamamen kaldırılabileceği emin olun.

Bu hello olun `dataCacheClients` girdisi hello kaldırıldı `configSections` öğesi. Merhaba tüm kaldırmayın `configSections` öğesi; yalnızca Kaldır hello `dataCacheClients` varsa, girdi.

```xml
<configSections>
  <!-- Existing sections omitted for clarity. -->
  <section name="dataCacheClients"type="Microsoft.ApplicationServer.Caching.DataCacheClientsSection, Microsoft.ApplicationServer.Caching.Core" allowLocation="true" allowDefinition="Everywhere"/>
</configSections>
```

Bu hello olun `dataCacheClients` bölüm kaldırılır. Merhaba `dataCacheClients` bölümü aşağıdaki örneğine benzer toohello olacaktır.

```xml
<dataCacheClients>
  <dataCacheClientname="default">
    <!--toouse hello in-role flavor of Azure Cache, set identifier toobe hello cache cluster role name -->
    <!--toouse hello Azure Managed Cache Service, set identifier toobe hello endpoint of hello cache cluster -->
    <autoDiscoverisEnabled="true"identifier="[Cache role name or Service Endpoint]"/>

    <!--<localCache isEnabled="true" sync="TimeoutBased" objectCount="100000" ttlValue="300" />-->
    <!--Use this section toospecify security settings for connecting tooyour cache. This section is not required if your cache is hosted on a role that is a part of your cloud service. -->
    <!--<securityProperties mode="Message" sslEnabled="true">
      <messageSecurity authorizationInfo="[Authentication Key]" />
    </securityProperties>-->
  </dataCacheClient>
</dataCacheClients>
```

Merhaba yönetilen önbellek hizmeti yapılandırma kaldırıldıktan sonra hello önbellek istemcisi bölümden hello açıklandığı şekilde yapılandırabilirsiniz.

### <a name="configure-a-cache-client-using-hello-stackexchangeredis-nuget-package"></a>Merhaba StackExchange.Redis NuGet paketi kullanarak bir önbellek istemcisini yapılandırma
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

## <a name="migrate-managed-cache-service-code"></a>Yönetilen önbellek hizmeti kodunu taşıma
Merhaba hello StackExchange.Redis önbellek istemcisi için benzer toohello yönetilen önbellek hizmeti API'dir. Bu bölümde hello farklar genel bir bakış sağlar.

### <a name="connect-toohello-cache-using-hello-connectionmultiplexer-class"></a>Merhaba ConnectionMultiplexer sınıfını kullanarak toohello Önbelleği'ne bağlama
Yönetilen önbellek hizmeti bağlantıları toohello önbellek hello tarafından işlendi `DataCacheFactory` ve `DataCache` sınıfları. Azure Redis Önbelleği'nde bu bağlantılar hello tarafından yönetilen `ConnectionMultiplexer` sınıfı.

Merhaba aşağıdaki eklemek istediğiniz tooaccess hello önbellek dosyasının deyimi toohello üst kullanarak.

```c#
using StackExchange.Redis
```

Bu ad alanı sorunu çözmezse, açıklandığı gibi hello StackExchange.Redis NuGet paketi eklediğinizden emin olun [hello önbellek istemcilerini yapılandırın](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).

> [!NOTE]
> Not Bu hello StackExchange.Redis istemcisi .NET Framework 4 veya üstünü gerektirir.
> 
> 

tooconnect tooan Azure Redis önbelleği örneği, çağrı hello statik `ConnectionMultiplexer.Connect` yöntemi ve hello uç noktasını ve anahtarı geçirin. Bir yaklaşım toosharing bir `ConnectionMultiplexer` örneğidir uygulamanızda toohave aşağıdaki örneğine benzer toohello bir bağlı örnek döndüren statik özelliğe. Bu, yalnızca tek bir bağlı olan bir iş parçacığı açısından güvenli şekilde tooinitialize sağlar `ConnectionMultiplexer` örneği. Bu örnekte `abortConnect` bağlantı toohello önbellek bile kurulamazsa hello çağrının başarılı olacağıdır anlamına gelir kümesi toofalse değil. Temel özelliklerinden biri `ConnectionMultiplexer` hello ağ sorunu ya da diğer nedenler çözüldükten sonra otomatik olarak bağlantı toohello önbellek geri yükleme.

```c#
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
```

Merhaba önbellek uç noktasını, anahtarlar ve bağlantı noktaları hello elde edilebilir **Redis önbelleği** dikey penceresinde, önbellek örneğinizin. Daha fazla bilgi için bkz: [Redis önbelleği özellikleri](cache-configure.md#properties).

Merhaba bağlantı kurulduktan sonra bir başvuru toohello Redis önbelleği veritabanına göre arama hello dönmek `ConnectionMultiplexer.GetDatabase` yöntemi. Merhaba hello döndürülen `GetDatabase` yöntemi basit bir geçiş nesnesi ve depolanan toobe gerekli değildir.

```c#
IDatabase cache = Connection.GetDatabase();

// Perform cache operations using hello cache object...
// Simple put of integral data types into hello cache
cache.StringSet("key1", "value");
cache.StringSet("key2", 25);

// Simple get of data types from hello cache
string key1 = cache.StringGet("key1");
int key2 = (int)cache.StringGet("key2");
```

Merhaba StackExchange.Redis istemcisi kullanır hello `RedisKey` ve `RedisValue` erişme ve öğeleri hello önbellekte depolamak için türleri. Bu tür dizesi dahil olmak üzere en basit dil türler harita ve genellikle doğrudan kullanılmaz. Redis dizeleri Redis değeri en temel tür hello ve pek çok seri hale getirilmiş ikili akışlar dahil olmak üzere veri türünü içerebilir ve hello türü doğrudan kullanamazsınız sırada içeren yöntemleri kullanacaksınız `String` hello adı. En basit veri türleri için depolamak ve öğeleri hello kullanarak hello önbellekten `StringSet` ve `StringGet` yöntemleri, koleksiyonları veya diğer Redis veri türlerine hello önbellekte depolamak sürece. 

`StringSet`ve `StringGet` çok benzer toohello yönetilen önbellek hizmeti olan `Put` ve `Get` yöntemleriyle, önemli bir fark olmasına, ayarlama ve .NET nesnesi hello önbelleğe alma önce onu önce seri gerekir. 

Çağrılırken `StringGet`hello nesne varsa, döndürülür ve mevcut değilse null değeri döndürülür. Bu durumda hello değeri hello istenen veri kaynağından almak ve daha sonra kullanılmak hello önbelleğindeki saklayın. Bu hello edilgen önbellek düzeni bilinir.

bir öğenin hello önbelleğindeki kullanım hello toospecify hello sona erme `TimeSpan` parametresinin `StringSet`.

```c#
cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));
```

Azure Redis önbelleği temel veri türlerinin yanı sıra .NET nesnelerini ile çalışabilir, ancak bir .NET nesnesini önbelleğe alabilmek için seri hale getirilmesi gerekir. Bu hello hello uygulama geliştiricisinin sorumluluğundadır. Bu, hello seri hale getirici hello tercihini hello Geliştirici esnekliği sağlar. Daha fazla bilgi ve örnek kod için bkz: [hello önbelleğinde .NET nesneleriyle çalışma](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).

## <a name="migrate-aspnet-session-state-and-output-caching-tooazure-redis-cache"></a>ASP.NET oturum durumu ve çıktı tooAzure Redis önbelleği önbelleği geçirme
Azure Redis önbelleği ASP.NET oturum durumu ve sayfa çıktı önbelleği sağlayıcıları vardır. toomigrate hello yönetilen önbellek hizmeti sürümleri bu sağlayıcıların kullandığı uygulamanızı kaldırın web.config varolan bölümlerinden hello ve hello Azure Redis önbelleği hello sağlayıcıları sürümleri yapılandırın. Azure Redis önbelleği ASP.NET sağlayıcıları kullanma yönergeleri hello için bkz: [Azure Redis önbelleği için ASP.NET oturum durumu sağlayıcısı](cache-aspnet-session-state-provider.md) ve [Azure Redis önbelleği için ASP.NET çıktı önbelleği sağlayıcısı](cache-aspnet-output-cache-provider.md).

## <a name="next-steps"></a>Sonraki adımlar
Merhaba keşfedin [Azure Redis önbelleği belgelerine](https://azure.microsoft.com/documentation/services/cache/) öğreticiler, örnekler, videolar ve daha fazla bilgi için.

