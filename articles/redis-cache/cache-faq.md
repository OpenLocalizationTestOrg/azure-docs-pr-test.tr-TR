---
title: "aaaAzure Redis önbelleği SSS | Microsoft Docs"
description: "Merhaba toocommon sorular, desenleri ve en iyi uygulamalar Azure Redis önbelleği için yanıtlar öğrenin"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c2c52b7d-b2d1-433a-b635-c20180e5cab2
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 2c6ed2f65f755bd08f04857b7af31f520cf4f158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-faq"></a>Azure Redis Cache SSS
Merhaba toocommon sorular, desenleri ve en iyi uygulamalar Azure Redis önbelleği için yanıtlar hakkında bilgi edinin.

## <a name="what-if-my-question-isnt-answered-here"></a>Ne sorumun cevabı burada cevaplanıp değil mi?
Sorunuzun yanıtını burada listelenmiyorsa, bize bildirin ve yanıt bulmanıza yardımcı olacağız.

* Bu SSS hello sonunda hello açıklamalarında bir soru gönderin ve hello Azure önbelleği ekip ve diğer topluluk üyeleri bu makale hakkında göster.
* daha geniş bir kitleye tooreach gönderdiğiniz bir soru hello üzerinde [Azure önbelleği MSDN Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=azurecache) ve hello Azure önbelleği ekibi ve hello Topluluğu'nun diğer üyeleri göster.
* Özellik isteği toomake istiyorsanız, istekleri ve fikirleri çok gönderebilmek için[Azure Redis önbelleği kullanıcı sesi](https://feedback.azure.com/forums/169382-cache).
* Ayrıca bir e-posta adresindeki toous gönderebilirsiniz [Azure önbelleği dış geri bildirim](mailto:azurecache@microsoft.com).

## <a name="azure-redis-cache-basics"></a>Azure Redis önbelleği temel kavramları
Merhaba SSS Bu bölümde bazı Azure Redis önbelleği hello temelleri kapsar.

* [Azure Redis Önbelleği nedir?](#what-is-azure-redis-cache)
* [Azure Redis önbelleği ile çalışmaya nasıl?](#how-can-i-get-started-with-azure-redis-cache)

Aşağıdaki sık sorulan sorular temel kavramları ve Azure Redis önbelleği hakkında sorular kapsar ve birinde yanıtlanır hello diğer SSS bölümleri hello.

* [Hangi Redis Önbelleği teklifini ve boyutunu kullanmalıyım?](#what-redis-cache-offering-and-size-should-i-use)
* [Hangi Redis önbelleği istemcileri kullanabilir miyim?](#what-redis-cache-clients-can-i-use)
* [Azure Redis önbelleği için yerel bir öykünücü var mı?](#is-there-a-local-emulator-for-azure-redis-cache)
* [Merhaba sağlık ve performans my önbelleğinin nasıl izlerim?](#how-do-i-monitor-the-health-and-performance-of-my-cache)

## <a name="planning-faqs"></a>Sık sorulan sorular planlama
* [Hangi Redis Önbelleği teklifini ve boyutunu kullanmalıyım?](#what-redis-cache-offering-and-size-should-i-use)
* [Azure Redis önbelleği performansı](#azure-redis-cache-performance)
* [Hangi bölgede ı my önbellek bulun?](#in-what-region-should-i-locate-my-cache)
* [Azure Redis önbelleği için nasıl faturalandırılır?](#how-am-i-billed-for-azure-redis-cache)
* [Azure Redis önbelleği Azure Bulutu, Azure Çin Bulut veya Microsoft Azure Almanya kullanabilir miyim?](#can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany)

## <a name="development-faqs"></a>Geliştirme ile ilgili SSS
* [Merhaba StackExchange.Redis yapılandırma seçeneklerini ne yapacaksınız?](#what-do-the-stackexchangeredis-configuration-options-do)
* [Hangi Redis önbelleği istemcileri kullanabilir miyim?](#what-redis-cache-clients-can-i-use)
* [Azure Redis önbelleği için yerel bir öykünücü var mı?](#is-there-a-local-emulator-for-azure-redis-cache)
* [Redis komutları nasıl çalıştırabilir miyim?](#how-can-i-run-redis-commands)
* [Azure Redis önbelleği diğer Azure hizmetleriyle hello bir MSDN sınıf kitaplığı başvurusu gibi bazı neden yok?](#why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-the-other-azure-services)
* [Azure Redis önbelleği PHP oturum önbelleği olarak kullanabilir miyim?](#can-i-use-azure-redis-cache-as-a-php-session-cache)
* [Redis veritabanları nelerdir?](#what-are-redis-databases)

## <a name="security-faqs"></a>Güvenlik ile ilgili SSS
* [TooRedis bağlanmak için SSL olmayan bağlantı noktası hello etkinleştirdiğinizde?](#when-should-i-enable-the-non-ssl-port-for-connecting-to-redis)

## <a name="production-faqs"></a>Üretim SSS
* [Bazı üretim en iyi uygulamalar nelerdir?](#what-are-some-production-best-practices)
* [Merhaba konuları bazı yaygın Redis komutları kullanırken nelerdir?](#what-are-some-of-the-considerations-when-using-common-redis-commands)
* [Nasıl ı Kıyaslama test ve hello my önbelleğinin performansını?](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* [İş parçacığı havuzu büyüme hakkında önemli ayrıntıları](#important-details-about-threadpool-growth)
* [StackExchange.Redis kullanırken hello istemci üzerinde daha fazla üretilen işi sunucusu GC tooget etkinleştir](#enable-server-gc-to-get-more-throughput-on-the-client-when-using-stackexchangeredis)
* [Bağlantıları geçici performans etkenleri](#performance-considerations-around-connections)

## <a name="monitoring-and-troubleshooting-faqs"></a>İzleme ve sık sorulan sorular sorun giderme
Bu bölümde kapak ortak izleme ve sorun giderme soruları Hello SSS. İzleme ve Azure Redis önbelleği örnekleri sorun giderme hakkında daha fazla bilgi için bkz: [nasıl toomonitor Azure Redis önbelleği](cache-how-to-monitor.md) ve [nasıl tootroubleshoot Azure Redis önbelleği](cache-how-to-troubleshoot.md).

* [Merhaba sağlık ve performans my önbelleğinin nasıl izlerim?](#how-do-i-monitor-the-health-and-performance-of-my-cache)
* [Zaman aşımları neden görüyorum?](#why-am-i-seeing-timeouts)
* [Neden my istemci hello önbellekten kesildi?](#why-was-my-client-disconnected-from-the-cache)

## <a name="prior-cache-offering-faqs"></a>Önceki önbelleği teklifini SSS
* [Hangi Azure önbelleği teklifini benim için en uygun mi?](#which-azure-cache-offering-is-right-for-me)

### <a name="what-is-azure-redis-cache"></a>Azure Redis Önbelleği nedir?
Azure Redis önbelleği hello popüler açık kaynak üzerinde temel [Redis önbelleği](http://redis.io). Size verir Azure içinde herhangi bir uygulamadan tooa güvenli, ayrılmış bir Redis önbelleğine Microsoft tarafından yönetilen ve erişilebilir erişim. Daha ayrıntılı bir genel bakış için bkz: Merhaba [Azure Redis önbelleği](https://azure.microsoft.com/services/cache/) Azure.com üzerindeki ürün sayfası.

### <a name="how-can-i-get-started-with-azure-redis-cache"></a>Azure Redis önbelleği ile çalışmaya nasıl?
Azure Redis önbelleği kullanmaya başlamak birkaç yolu vardır.

* Kullanılabilir öğreticilerimizden birini çıkışı denetleyebilirsiniz [.NET](cache-dotnet-how-to-use-azure-redis-cache.md), [ASP.NET](cache-web-app-howto.md), [Java](cache-java-get-started.md), [Node.js](cache-nodejs-get-started.md), ve [Python](cache-python-get-started.md).
* İzleyebilir [nasıl tooBuild yüksek performanslı uygulamalar kullanarak Microsoft Azure Redis önbelleği](https://azure.microsoft.com/documentation/videos/how-to-build-high-performance-apps-using-microsoft-azure-cache/).
* Merhaba istemcisi belgeleri nasıl toouse Redis, proje toosee hello geliştirme dilini eşleşen hello istemciler için kullanıma alabilirsiniz. Azure Redis önbelleği ile kullanılan birçok Redis istemcileri vardır. Redis istemcileri listesi için bkz: [http://redis.io/clients](http://redis.io/clients).

Zaten bir Azure hesabınız yoksa, şunları yapabilirsiniz:

* [Ücretsiz bir Azure hesabı açın](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero). Out kullanılan tootry Ücretli Azure hizmetlerini olabilir krediler alırsınız. Hatta hello krediler bitmiş olsa, hello hesabı sürdürebilir ve ücretsiz Azure hizmetlerini ve özellikleri kullanın.
* [Visual Studio abone avantajları etkinleştirin](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero). MSDN aboneliğiniz, ücretli Azure hizmetlerinizi kullanabildiğiniz her ay size kredi verir.

<a name="cache-size"></a>

### <a name="what-redis-cache-offering-and-size-should-i-use"></a>Hangi Redis Önbelleği teklifini ve boyutunu kullanmalıyım?
Her Azure Redis önbelleği teklifini farklı düzeylerde sağlar **boyutu**, **bant genişliği**, **yüksek kullanılabilirlik**, ve **SLA** seçenekleri.

Merhaba, önbelleği teklifini seçme hakkında önemli noktalar şunlardır.

* **Bellek**: hello temel ve standart katmanları, 250 MB – 53 GB'a sunar. Merhaba Premium katmanı too530 GB sunar. Daha fazla bilgi için bkz: [Azure Redis önbelleği fiyatlandırma](https://azure.microsoft.com/pricing/details/cache/).
* **Ağ performansı**: yüksek işleme gerektiren bir iş yükü varsa, daha fazla bant genişliği karşılaştırılan tooStandard veya Basic hello Premium katmanı sunar. Ayrıca her katman içinde hello önbellek barındıran VM temel hello nedeniyle daha fazla bant genişliği daha büyük boyutu önbellekleri vardır. Merhaba bkz [tablo aşağıdaki](#cache-performance) daha fazla bilgi için.
* **Üretilen iş**: hello Premium katmanı hello en fazla kullanılabilir üretilen sunar. Merhaba önbellek sunucu veya istemci hello bant genişliği sınırlarını ulaşırsa, hello istemci tarafındaki zaman aşımı alabilirsiniz. Daha fazla bilgi için aşağıdaki tablonun hello bakın.
* **Yüksek kullanılabilirlik SLA**: Azure Redis önbelleği standart/Premium önbelleği en az başlangıç saati % 99,9 kullanılabilir olduğunu güvence altına alır. Bizim SLA hakkında daha fazla toolearn bkz [Azure Redis önbelleği fiyatlandırma](https://azure.microsoft.com/support/legal/sla/cache/v1_0/). Merhaba SLA bağlantı toohello önbellek uç noktalar yalnızca kapsar. Merhaba SLA veri kaybına karşı koruma kapsamaz. Veri kaybına karşı hello Premium katmanı tooincrease dayanıklılık içinde hello Redis veri kalıcılığını özelliğini kullanmanızı öneririz.
* **Redis veri kalıcılığını**: hello Premium katmanı sağlar toopersist hello önbellek verilerini Azure depolama hesabı. Basic/standart önbelleğinde tüm hello verileri yalnızca bellekte depolanır. Temel alınan altyapı sorunları varsa olası veri kaybı olabilir. Veri kaybına karşı hello Premium katmanı tooincrease dayanıklılık içinde hello Redis veri kalıcılığını özelliğini kullanmanızı öneririz. Azure Redis önbelleği RDB ve (yakında) AOF Redis kalıcılığı seçenekleri sunar. Daha fazla bilgi için bkz: [nasıl Premium Azure Redis önbelleği için kalıcılığı tooconfigure](cache-how-to-premium-persistence.md).
* **Redis kümesi**: toocreate önbelleğe 53 GB'a veya tooshard veri büyük birden çok Redis düğümünde, Redis kümeleme, hello Premium katmanında kullanılabilir olduğu kullanabilirsiniz. Her düğüm, yüksek kullanılabilirlik için birincil/çoğaltma önbelleği çiftinin oluşur. Daha fazla bilgi için bkz: [nasıl bir Premium Azure Redis önbelleği için kümeleri tooconfigure](cache-how-to-premium-clustering.md).
* **Gelişmiş Güvenlik ve ağ yalıtımı**: Gelişmiş Güvenlik ve yalıtım, Azure Redis önbelleği yanı sıra alt ağlar, erişim denetimi ilkeleri için Azure sanal ağ (VNET) dağıtım sağlar ve diğer özellikleri toofurther erişimi kısıtlayın. Daha fazla bilgi için bkz: [tooconfigure sanal ağ Premium Azure Redis önbelleği için nasıl destek](cache-how-to-premium-vnet.md).
* **Redis yapılandırma**: hello standart ve Premium Katmanlar Redis için Keyspace bildirimleri yapılandırabilirsiniz.
* **İstemci bağlantısı sayısı**: hello Premium katmanı tooRedis, büyük ölçekli önbellekler için bağlantılarının daha yüksek bir sayı ile bağlanan istemciler hello sayısının sunar. Daha fazla bilgi için bkz: [Azure Redis önbelleği fiyatlandırma](https://azure.microsoft.com/pricing/details/cache/).
* **Redis sunucu için çekirdek ayrılmış**: hello Premium katmanındaki tüm önbellek boyutlarını adanmış bir çekirdek için Redis sahip. Merhaba Basic/standart katmanları C1 boyutu hello ve yukarıdaki Redis sunucusu için ayrılmış bir çekirdek vardır.
* **Redis tek iş parçacıklı** ikiden fazla çekirdeğe sahip sağlamaz ek avantajı yalnızca iki çekirdeğe sahip üzerinden ancak büyük VM boyutları genellikle daha fazla bant genişliği daha küçük boyutlara sahiptir. Merhaba önbellek sunucu veya istemci hello bant genişliği sınırlarını ulaşırsa, hello istemci tarafındaki zaman aşımı alırsınız.
* **Performans iyileştirmeleri**: hello Premium katmanındaki önbellekleri, daha hızlı bir işlemciye sahip donanım üzerinde daha iyi performans karşılaştırılan toohello temel veya standart katmanı vermiş dağıtılır. Premium katmanı önbellekleri daha yüksek verimlilik ve düşük gecikme vardır.

<a name="cache-performance"></a>

### <a name="azure-redis-cache-performance"></a>Azure Redis önbelleği performansı
Merhaba aşağıdaki tablo standart çeşitli boyutlarda test ederken gözlenen hello en yüksek bant genişliği değerleri gösterir ve Premium önbellekleri kullanarak `redis-benchmark.exe` hello Azure Redis önbelleği endpoint karşı bir Iaas VM'den. 

>[!NOTE] 
>Bu değerleri yıkıcıları ve bunlar için hiçbir SLA numaraları ancak tipik olması gerekir. Yüklemesi gerektiğini kendi uygulama toodetermine hello sağ önbellek boyutu, uygulamanız için test edin.
>
>

Bu tablodan şu sonuçları aşağıdaki hello çizebilirsiniz:

* Karşılaştırılan toohello standart katmanı hello aynı boyutta daha yüksek olan hello önbellekler için işleme hello Premium katmanı. Örneğin, 6 GB önbellek ile karşılaştırılan too49, C3 000 olarak 180.000 RPS P1 verimini olur.
* Parça (düğümler) hello kümedeki hello sayısı arttıkça kümeleme Redis ile üretilen işi doğrusal olarak artırır. 10 parça P4 kümesi oluşturursanız, örneğin, hello kullanılabilir verimlilik 400.000 ise * 10 = 4 milyon RPS.
* Daha büyük anahtar boyutları için işleme karşılaştırılan toohello standart katmanı hello Premium katmanındaki yüksektir.

| Fiyatlandırma katmanı | Boyut | CPU çekirdekleri | Kullanılabilir bant genişliği | 1 KB değer boyutu |
| --- | --- | --- | --- | --- |
| **Standart önbellek boyutu** | | |**Megabit / sn (Mb/sn) / megabayt sayısı / sn (MB/sn)** |**(RPS) saniye başına istek sayısı** |
| C0 |250 MB |Paylaşılan |5 / 0.625 |600 |
| C1 |1 GB |1 |100 / 12.5 |12,200 |
| C2 |2.5 GB |2 |200 / 25 |24,000 |
| C3 |6 GB |4 |400 / 50 |49,000 |
| C4 |13 GB |2 |500 / 62.5 |61,000 |
| C5 |26 GB |4 |1,000 / 125 |115,000 |
| C6 |53 GB |8 |2,000 / 250 |150,000 |
| **Premium önbellek boyutu** | |**Parça başına CPU çekirdekleri** | **Megabit / sn (Mb/sn) / megabayt sayısı / sn (MB/sn)** |**Parça (RPS) saniyede istekleri** |
| P1 |6 GB |2 |1,500 / 187.5 |180,000 |
| P2 |13 GB |4 |3,000 / 375 |360,000 |
| P3 |26 GB |4 |3,000 / 375 |360,000 |
| P4 |53 GB |8 |6,000 / 750 |400,000 |

Merhaba indirme yönergeleri araçları gibi Redis için `redis-benchmark.exe`, hello bkz [nasıl ı çalıştırabilirsiniz Redis komutları?](#cache-commands) bölümü.

<a name="cache-region"></a>

### <a name="in-what-region-should-i-locate-my-cache"></a>Hangi bölgede ı my önbellek bulun?
Azure Redis önbelleği hello bulun ve en iyi performans ve düşük gecikme, önbellek istemci uygulamanız aynı bölgede.

<a name="cache-billing"></a>

### <a name="how-am-i-billed-for-azure-redis-cache"></a>Azure Redis önbelleği için nasıl faturalandırılır?
Azure Redis önbelleği fiyatlandırma olan [burada](https://azure.microsoft.com/pricing/details/cache/). Fiyatlandırma sayfası hello saat ücretine fiyatlandırma listeler. Önbellekleri hello önbelleği önbellek silinmiş hello zamana kadar oluşturulan hello zamandan dakika başına temelinde faturalandırılır. Durdurma veya duraklatma hello faturalama bir önbelleği için bir seçenek yoktur.

### <a name="can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany"></a>Azure Redis önbelleği Azure Bulutu, Azure Çin Bulut veya Microsoft Azure Almanya kullanabilir miyim?
Evet, Azure Redis önbelleği Azure Bulutu, Azure Çin Bulut ve Microsoft Azure Almanya kullanılabilir. Merhaba URL'leri erişme ve Azure Redis önbelleği yönetmek için Azure genel bulut ile karşılaştırıldığında bu bulutların farklıdır. 

| Bulut   | Redis için DNS son eki            |
|---------|---------------------------------|
| Genel  | *. redis.cache.windows.net       |
| ABD Devleti  | *. redis.cache.usgovcloudapi.net |
| Almanya | *. redis.cache.cloudapi.de       |
| Çin   | *. redis.cache.chinacloudapi.cn  |

Azure Redis önbelleği ile diğer Bulutları kullanmayla ilgili konular hakkında daha fazla bilgi için bağlantılar aşağıdaki hello bakın.

- [Azure kamu veritabanları - Azure Redis önbelleği](../azure-government/documentation-government-services-database.md#azure-redis-cache)
- [Azure Çin bulut - Azure Redis önbelleği](https://www.azure.cn/documentation/services/redis-cache/)
- [Microsoft Azure Almanya](https://azure.microsoft.com/overview/clouds/germany/)

Azure Bulutu, Azure Çin Bulut ve Microsoft Azure Almanya de PowerShell ile Azure Redis önbelleği kullanma hakkında daha fazla bilgi için bkz: [nasıl tooconnect tooother Bulutlar - Azure Redis önbelleği PowerShell](cache-howto-manage-redis-cache-powershell.md#how-to-connect-to-other-clouds).

<a name="cache-configuration"></a>

### <a name="what-do-hello-stackexchangeredis-configuration-options-do"></a>Merhaba StackExchange.Redis yapılandırma seçeneklerini ne yapacaksınız?
StackExchange.Redis pek çok seçenek vardır. Bu bölümde bazı hello ortak ayarları hakkında alınmaktadır. StackExchange.Redis seçenekleri hakkında daha ayrıntılı bilgi için bkz: [StackExchange.Redis yapılandırma](https://stackexchange.github.io/StackExchange.Redis/Configuration).

| ConfigurationOptions | Açıklama | Öneri |
| --- | --- | --- |
| AbortOnConnectFail |Tootrue, ayarlandığında hello bağlantısı olmayan bir ağ hatasından sonra yeniden. |Toofalse ayarlamak ve otomatik olarak yeniden StackExchange.Redis izin verin. |
| ConnectRetry |Merhaba kaç kez sırasında ilk toorepeat bağlanma denemelerinin bağlayın. |Kılavuzu notları aşağıdaki hello bakın. |
| ConnectTimeout |Bağlantı işlemleri için ms cinsinden zaman aşımı. |Kılavuzu notları aşağıdaki hello bakın. |

Genellikle hello istemcisinin hello varsayılan değerler yeterlidir. Başlangıç seçenekleri, iş yüküne göre ince ayar yapabilirsiniz.

* **Yeniden deneme sayısı**
  * ConnectRetry ve ConnectTimeout, hello genel rehberlik toofail hızlı verilir ve yeniden deneyin. Bu kılavuz, iş yükü ve üzerinde ne kadar zaman alır, istemci tooissue bir Redis komutu için ortalama ve yanıt dayanır.
  * Bağlantı durumunu denetleme ve kendiniz yeniden bağlanmayı yerine otomatik olarak yeniden StackExchange.Redis olanak tanır. **Merhaba ConnectionMultiplexer.IsConnected özelliğini kullanmaktan kaçının**.
  * Snowballing - burada yeniden deneniyor ve hello snowball yeniden deneme sayısı ve hiçbir zaman kurtarır sorunu bazen çalışabilir. Snowballing meydana gelirse, açıklandığı gibi bir üstel geri alma yeniden deneme algoritması kullanmayı düşünmelisiniz [yeniden genel rehberlik](../best-practices-retry-general.md) hello Microsoft Patterns & yöntemler grubu tarafından yayımlanan.
* **Zaman aşımı değerleri**
  * İş yükünüzün göz önünde bulundurun ve hello değerlerini uygun şekilde ayarlayın. Büyük değerler depolanıyorsa hello zaman aşımı tooa daha yüksek değere ayarlayın.
  * Ayarlama `AbortOnConnectFail` toofalse ve sizin için yeniden StackExchange.Redis izin verin.
  * Tek bir ConnectionMultiplexer örneği hello uygulama için kullanın. LazyConnection toocreate bağlantı özellik tarafından döndürülen tek bir örneğinde gösterildiği gibi kullanabilirsiniz [toohello önbellek hello ConnectionMultiplexer sınıfını kullanarak bağlanmak](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache).
  * Set hello `ConnectionMultiplexer.ClientName` özelliği tooan uygulama örneği için benzersiz bir ad tanılma.
  * Birden çok kullanmak `ConnectionMultiplexer` özel iş yükleri için örnek.
      * Uygulamanızda değişen yük varsa, bu model izleyebilirsiniz. Örneğin:
      * Çoğaltıcı büyük anahtarların ilgilenmek için bir bulunabilir.
      * Çoğaltıcı küçük anahtarlar ilgilenmek için bir bulunabilir.
      * Bağlantı zaman aşımı için farklı değerler ayarlayın ve kullandığınız her ConnectionMultiplexer için mantığı yeniden deneyin.
      * Set hello `ClientName` Tanılama ile çoğaltıcı her toohelp özelliği.
      * Bu kılavuz hızlandırıldı toomore gecikme başına açabilir `ConnectionMultiplexer`.

### <a name="what-redis-cache-clients-can-i-use"></a>Hangi Redis önbelleği istemcileri kullanabilir miyim?
Redis hakkındaki harika şeylerden hello olan birçok farklı geliştirme dili destekleyen birçok istemciler biridir. İstemcilerin geçerli bir listesi için bkz [Redis istemcileri](http://redis.io/clients). Birkaç farklı diller ve istemcilerin kapak öğreticileri için bkz: [nasıl toouse Azure Redis önbelleği](cache-dotnet-how-to-use-azure-redis-cache.md) ve hello dil değiştirici hello makalenin hello üstünde istenen hello dilden'ı tıklatın.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<a name="cache-emulator"></a>

### <a name="is-there-a-local-emulator-for-azure-redis-cache"></a>Azure Redis önbelleği için yerel bir öykünücü var mı?
Azure Redis önbelleği için hiçbir yerel öykünücüsü yoktur, ancak hello hello MSOpenTech redis server.exe sürümünü çalıştırabilirsiniz [Redis komut satırı araçları](https://github.com/MSOpenTech/redis/releases/) yerel makine ve tooit tooget benzer bir deneyim tooa yerel önbelleğe bağlanma öykünücü, hello aşağıdaki örnekte gösterildiği gibi:

    private static Lazy<ConnectionMultiplexer>
          lazyConnection = new Lazy<ConnectionMultiplexer>
        (() =>
        {
            // Connect tooa locally running instance of Redis toosimulate a local cache emulator experience.
            return ConnectionMultiplexer.Connect("127.0.0.1:6379");
        });

        public static ConnectionMultiplexer Connection
        {
            get
            {
                return lazyConnection.Value;
            }
        }


İsteğe bağlı olarak yapılandırabileceğiniz bir [redis.conf](http://redis.io/topics/config) dosya toomore hello karşılayabilmesi [varsayılan önbellek ayarları](cache-configure.md#default-redis-server-configuration) çevrimiçi Azure Redis isterseniz önbelleğiniz için.

<a name="cache-commands"></a>

### <a name="how-can-i-run-redis-commands"></a>Redis komutları nasıl çalıştırabilir miyim?
Adresinde listelenmiş hello komutlardan herhangi birini kullanabilirsiniz [Redis komutları](http://redis.io/commands#) adresinde listelenmiş hello komutları dışında [Redis Azure Redis Önbelleği'nde desteklenmeyen komutlar](cache-configure.md#redis-commands-not-supported-in-azure-redis-cache). Çeşitli seçenekler toorun Redis komutları var.

* Standart veya Premium önbellek varsa, hello kullanarak Redis komutları çalıştırabilirsiniz [Redis konsol](cache-configure.md#redis-console). Merhaba Redis Konsolu'na hello Azure portal Redis komutlarda güvenli şekilde toorun sağlar.
* Merhaba Redis komut satırı araçları da kullanabilirsiniz. bunları, toouse gerçekleştirmek hello adımları izleyin:
* Merhaba karşıdan [Redis komut satırı araçları](https://github.com/MSOpenTech/redis/releases/).
* Önbellek toohello kullanarak bağlan `redis-cli.exe`. Merhaba önbellek son nokta hello -h anahtar hello aşağıdaki örnekte gösterildiği gibi kullanarak ve başlangıç anahtarı kullanarak geçirin:
* `redis-cli -h <your cache="" name="">
  .redis.cache.windows.net -a <key>
  `

> [!NOTE]
> Merhaba Redis komut satırı araçları hello SSL bağlantı noktası ile çalışmaz, ancak bir yardımcı programı gibi kullanabilir `stunnel` toosecurely hello hello yönergeleri izleyerek hello araçları toohello SSL bağlantı bağlanmayı [için ASP.NET oturum durumu sağlayıcısı Duyurusu Önizleme sürümü redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) blog postası.
>
>

<a name="cache-reference"></a>

### <a name="why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-hello-other-azure-services"></a>Azure Redis önbelleği diğer Azure hizmetleriyle hello bir MSDN sınıf kitaplığı başvurusu gibi bazı neden yok?
Microsoft Azure Redis önbelleği hello popüler açık kaynak Redis önbelleğini temel alır ve çok çeşitli tarafından erişilebilen [Redis istemcileri](http://redis.io/clients) pek çok programlama dili için. Her istemci yapar çağırdığı toohello Redis önbelleği örneği kullanarak kendi API sahip [Redis komutları](http://redis.io/commands).

Her istemci farklı olduğu için MSDN'de olmayan bir merkezi sınıf başvurusu olan ve her bir istemci kendi başvuru belgeleri korur. Ayrıca toohello başvuru belgelerini, tooget Azure Redis önbelleği farklı diller ve önbellek istemcilerinin kullanılarak ile çalışmaya nasıl gösteren birkaç öğreticileri vardır. Bu öğreticiler tooaccess bkz [nasıl toouse Azure Redis önbelleği](cache-dotnet-how-to-use-azure-redis-cache.md) ve hello dil değiştirici hello makalenin hello üstünde istenen hello dilden'ı tıklatın.

### <a name="can-i-use-azure-redis-cache-as-a-php-session-cache"></a>Azure Redis önbelleği PHP oturum önbelleği olarak kullanabilir miyim?
Evet, Azure Redis önbelleği PHP oturumu önbelleği olarak toouse belirtin hello bağlantı dizesi tooyour Azure Redis önbelleği örneğine `session.save_path`.

> [!IMPORTANT]
> Azure Redis önbelleği PHP oturum önbelleği olarak kullanırken, URL gerekir hello aşağıdaki örnekte gösterildiği gibi hello güvenlik anahtar kullanılan tooconnect toohello önbelleği, kodlama:
>
> `session.save_path = "tcp://mycache.redis.cache.windows.net:6379?auth=<url encoded primary or secondary key here>";`
>
> Merhaba anahtar URL kodlanmış değilse, bir özel durumla aşağıdakine benzer bir ileti alabilirsiniz:`Failed tooparse session.save_path`
>
>

Merhaba PhpRedis istemcisi ile PHP oturumu önbelleği olarak Redis önbelleği kullanma hakkında daha fazla bilgi için bkz: [PHP oturum işleyici](https://github.com/phpredis/phpredis#php-session-handler).

### <a name="what-are-redis-databases"></a>Redis veritabanları nelerdir?

Redis veritabanlarıdır yalnızca mantıksal ayırma hello içindeki verilerin aynı Redis örneği. Hello önbellek tüm hello veritabanları arasında paylaşılır ve verilen bir veritabanı gerçek bellek tüketimini başlangıç anahtarları/değerleri bu veritabanında depolanan bağlıdır. Örneğin bir C6 önbellek 53 GB'a kadar bellek sahiptir. Onu birden çok veritabanları arasında bölmek ya da bir veritabanına tüm 53 GB'a tooput seçebilirsiniz. 

> [!NOTE]
> Premium Azure Redis önbelleği kümeleme özelliği etkinleştirilmiş kullanırken, yalnızca veritabanı 0 kullanılabilir. Bu sınırlama bir iç Redis sınırlaması ve belirli tooAzure Redis önbelleği değil. Daha fazla bilgi için bkz: [toomake kümeleme tüm değişiklikleri toomy istemci uygulaması toouse ihtiyacım var?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 


<a name="cache-ssl"></a>

### <a name="when-should-i-enable-hello-non-ssl-port-for-connecting-tooredis"></a>TooRedis bağlanmak için SSL olmayan bağlantı noktası hello etkinleştirdiğinizde?
Redis sunucu SSL yerel olarak desteklemez ancak Azure Redis önbelleği desteklemez. TooAzure Redis önbelleği bağlanan ve istemci StackExchange.Redis gibi SSL destekliyorsa SSL kullanmanız gerekir.

>[!NOTE]
>Merhaba SSL olmayan bağlantı noktası yeni Azure Redis önbelleği örnekleri için varsayılan olarak devre dışıdır. İstemci SSL desteklemeyen sonra hello hello yönergeleri izleyerek hello SSL olmayan bağlantı noktası etkinleştirmelisiniz [erişim bağlantı noktaları](cache-configure.md#access-ports) hello bölümünü [Azure Redis Önbelleği'nde bir önbellek yapılandırma](cache-configure.md) makalesi.
>
>

Araçları gibi redis `redis-cli` hello SSL bağlantı noktası ile çalışmaz, ancak bir yardımcı programı gibi kullanabilir `stunnel` toosecurely hello hello yönergeleri izleyerek hello araçları toohello SSL bağlantı bağlanmayı [tanışın ASP.NET oturum durumu sağlayıcısı Redis Önizleme sürümü için](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) blog postası.

Merhaba hello indirme yönergeleri araçları Redis için bkz: [nasıl ı çalıştırabilirsiniz Redis komutları?](#cache-commands) bölümü.

### <a name="what-are-some-production-best-practices"></a>Bazı üretim en iyi uygulamalar nelerdir?
* [StackExchange.Redis en iyi uygulamalar](#stackexchangeredis-best-practices)
* [Yapılandırma ve kavramları](#configuration-and-concepts)
* [Performansı test etme](#performance-testing)

#### <a name="stackexchangeredis-best-practices"></a>StackExchange.Redis en iyi uygulamalar
* Ayarlama `AbortConnect` toofalse, sonra hello ConnectionMultiplexer yeniden otomatik olarak sağlayabilirsiniz. [Ayrıntılar için burada gördüğünüz](https://gist.github.com/JonCole/36ba6f60c274e89014dd#file-se-redis-setabortconnecttofalse-md).
* Merhaba ConnectionMultiplexer yeniden - her istek için yeni bir tane oluşturmayın. Merhaba `Lazy<ConnectionMultiplexer>` düzeni [burada gösterilen](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache) önerilir.
* Works en küçük değerleri ile redis, böylece birden çok anahtar daha büyük veri chopping göz önünde bulundurun. İçinde [bu Redis tartışma](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ), 100 kb büyük değerlendirilir. Okuma [bu makalede](https://gist.github.com/JonCole/db0e90bedeb3fc4823c2#large-requestresponse-size) büyük değerler neden bir örnek sorun için.
* Yapılandırma, [iş parçacığı havuzu ayarlarını](#important-details-about-threadpool-growth) tooavoid zaman aşımı.
* Kullanımı en az 5 saniyelik varsayılan connectTimeout hello. Bu aralık StackExchange.Redis yeterli zaman toore verirsiniz-ağ blip durumunda hello bağlantı.
* Kullanmakta olduğunuz farklı işlemlerle ilişkili hello performans maliyetleri farkında olun. Örneğin, hello `KEYS` komut bir o(n) ve kaçınılmalıdır. Merhaba [redis.io site](http://redis.io/commands/) hello zaman karmaşıklık desteklediği her bir işlemin ayrıntılarla sahiptir. Her komut toosee hello karmaşıklık her işlem için tıklatın.

#### <a name="configuration-and-concepts"></a>Yapılandırma ve kavramları
* Standart veya Premium katmanı üretim sistemleri için kullanın. Merhaba temel katman, hiçbir veri çoğaltma ve hiçbir SLA ile bir tek düğümlü sistemidir. Ayrıca, en az bir C1 önbellek kullanır. C0 önbellekleri genellikle basit geliştirme ve test senaryoları için kullanılır.
* Redis olduğunu unutmayın bir **bellek içi** veri deposu. Okuma [bu makalede](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md) burada veri kaybının olabileceği senaryoları kullanan; böylece.
* Bağlantı blips işleyebilir gibi sisteminizi geliştirmek [son toopatching ve yük devretme](https://gist.github.com/JonCole/317fe03805d5802e31cfa37e646e419d#file-azureredis-patchingexplained-md).

#### <a name="performance-testing"></a>Performansı test etme
* Başlangıç kullanarak `redis-benchmark.exe` tooget fikir sahibi olmak için performans testleri yazmadan önce olası işleme. Çünkü `redis-benchmark` SSL desteklemiyor gerekir [hello SSL olmayan bağlantı noktası hello Azure portal üzerinden etkinleştirme](cache-configure.md#access-ports) hello testini çalıştırmadan önce. Örnekler için bkz: [nasıl ı Kıyaslama test ve hello my önbelleğinin performansını?](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* Merhaba istemci test etmek için kullanılan VM hello olmalıdır, Redis önbelleği örneği aynı bölgede.
* Daha iyi donanım sahip ve hello en iyi sonuçlar vermelidir Dv2 VM dizisi için istemcinizi kullanmanızı öneririz.
* Seçtiğiniz VM test ettiğiniz hello önbelleği olarak en az kadar bilgi işlem ve bant genişliği yeteneği olan istemci emin olun.
* Windows'da ise VRSS hello istemci makinesinde etkinleştirin. [Ayrıntılar için burada gördüğünüz](https://technet.microsoft.com/library/dn383582.aspx).
* CPU ve ağ için daha iyi donanım üzerinde çalıştırdığınız için daha iyi gecikme süresi ve verimlilik premium katmanı Redis örnekleri ağ.

<a name="cache-redis-commands"></a>

### <a name="what-are-some-of-hello-considerations-when-using-common-redis-commands"></a>Merhaba konuları bazı yaygın Redis komutları kullanırken nelerdir?
* Bu komutlar hello etkisini anlamak olmadan uzun süre toocomplete alması belirli Redis komutları çalıştırmamanız gerekir.
  * Örneğin, hello çalıştırmayın [ANAHTARLARI](http://redis.io/commands/keys) uzun süre tooreturn anahtar hello sayısı bağlı olarak ele geçirebilir gibi üretimde komutu. Redis bir tek iş parçacıklı bir sunucudur ve aynı anda komutları işler. ANAHTARLARI sonra diğer komutlara varsa, Redis hello ANAHTARLARI komutu işleyene kadar bunlar işlenmeyecek. Merhaba [redis.io site](http://redis.io/commands/) hello zaman karmaşıklık desteklediği her bir işlemin ayrıntılarla sahiptir. Her komut toosee hello karmaşıklık her işlem için tıklatın.
* Küçük anahtar/değer veya büyük anahtar/değer anahtar boyutları - kullanmalıyım? Genel olarak, hello senaryoya bağlıdır. Büyük anahtarlar senaryonuz gerektiriyorsa, hello ConnectionTimeout ayarlamak ve değerleri yeniden deneyin ve yeniden deneme mantığı ayarlayın. Redis sunucu açısından bakıldığında, küçük değerler toohave daha iyi performans gözetilir.
* Bu noktalar Redis büyük değerleri depolayamaz anlamına yoktur; Merhaba ilgili önemli noktalar aşağıdaki farkında olmanız gerekir. Gecikme süreleri daha yüksek olur. Bir büyük veri kümesi ve daha küçük olan bir varsa, birden çok ConnectionMultiplexer örnekleri kullanabilirsiniz, her hello önceki açıklandığı gibi farklı bir zaman aşımı ve yeniden deneme değerlerini kümesi ile yapılandırılmış [hello StackExchange.Redis yapılandırma seçenekleri yapmak](#cache-configuration) bölümü.

<a name="cache-benchmarking"></a>

### <a name="how-can-i-benchmark-and-test-hello-performance-of-my-cache"></a>Nasıl ı Kıyaslama test ve hello my önbelleğinin performansını?
* [Önbellek tanılamayı etkinleştirin](cache-how-to-monitor.md#enable-cache-diagnostics) , böylece [İzleyici](cache-how-to-monitor.md) hello önbelleğinizin sistem durumunu. Hello Azure portal ve ölçümler için de hello görüntüleyebilirsiniz [indirebilir ve gözden](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) bunları tercih ettiğiniz hello araçlarını kullanma.
* Redis-benchmark.exe tooload test Redis sunucunuza kullanabilirsiniz.
* Merhaba yük testi istemci ve hello Redis önbelleği hello olduğundan emin olun aynı bölgede.
* Redis-cli.exe kullanın ve hello bilgisi komutunu kullanarak hello önbelleğini izleyebilirsiniz.
* Yük yüksek bellek parçalanması neden olup olmadığını tooa daha büyük önbellek boyutu ölçeklendirmeniz gerekir.
* Merhaba hello indirme yönergeleri araçları Redis için bkz: [nasıl ı çalıştırabilirsiniz Redis komutları?](#cache-commands) bölümü.

Merhaba aşağıdaki komutları redis benchmark.exe kullanmaya ilişkin bir örnek sağlar. Merhaba, bir VM'den doğru sonuçlar için bu komutları çalıştırdıktan önbelleğiniz aynı bölgede.

* 1 k yükü kullanarak test ardışık SET istekleri

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t SET -n 1000000 -d 1024 -P 50`
* Ardışık test alma 1 k yükü kullanarak ister.
  Not: ilk toopopulate önbellek gösterilen hello KÜMESİ testi çalıştırma

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t GET -n 1000000 -d 1024 -P 50`

<a name="threadpool"></a>

### <a name="important-details-about-threadpool-growth"></a>İş parçacığı havuzu büyüme hakkında önemli ayrıntıları
Merhaba CLR iş parçacığı havuzu iş parçacıkları - "Alt" ve "G/ç tamamlama bağlantı noktasını" (diğer adıyla ıocp Açılırken) iki tür vardır iş parçacığı sayısı.

* Çalışan iş parçacığı işleme gibi şeyleri zaman için kullanılan `Task.Run(…)` veya `ThreadPool.QueueUserWorkItem(…)` yöntemleri. İş toohappen arka plan iş parçacığında gerektiğinde bu iş parçacıkları hello CLR içinde çeşitli bileşenler tarafından da kullanılır.
* Zaman uyumsuz g/ç (örneğin hello ağdan okunurken) olduğunda ıocp Açılırken iş parçacığı kullanılır.

g/ç tamamlama (olmadan herhangi azaltma) isteğe bağlı bu kadar iş parçacıklarında ulaştığında hello "Minimum" ayarı iş parçacığı her tür için veya yeni çalışan iş parçacığı Hello iş parçacığı havuzu sağlar. Varsayılan olarak, hello en az iş parçacığı sayısını bir sistemde işlemci sayısını toohello ayarlanır.

Bir kez hello sayısının varolan (meşgul) iş parçacıklarının isabet hello "minimum" iş parçacığı, hello iş parçacığı havuzu azaltma ve bu da en yeni iş parçacıklarının tooone iş parçacığı başına 500 milisaniye yerleştirir hello oranı. Sisteminizin bir veri bloğu ıocp Açılırken iş parçacığı ihtiyaç duyan iş alırsa, genellikle, bu çalışan çok hızlı bir şekilde işler. Ancak, iş hello veri bloğu hello "Minimum" ayarı yapılandırılmış fazlasını ise, olacaktır bazı gecikme hello iş parçacığı havuzu iki şey toohappen biri için bekleyeceği gibi bazı hello iş işleme.

1. Var olan bir iş parçacığı ücretsiz tooprocess hello iş olur.
2. Yeni bir iş parçacığı oluşmasını mevcut hiçbir iş parçacığı 500ms için boş olur.

Temel olarak hello meşgul iş parçacığı sayısını en az iş parçacığı büyük olduğunda, ağ trafiğini hello uygulama tarafından işlenmeden önce büyük olasılıkla bir 500ms gecikme ödeme yapıyorsanız, anlamına gelir. Ayrıca, var olan iş parçacığı (t unutmayın üzerinde göre) 15 saniye daha uzun süre boşta kalır önemli toonote olduğundan, temizlenen ve bu büyüme ve azalması döngüsünü yineleyebilirsiniz.

StackExchange.Redis biz bir örnek hata ileti baktığınızda (1.0.450 yapı veya sonrası), bunu şimdi (bkz. ıocp Açılırken ve çalışan ayrıntılarına bakın) iş parçacığı havuzu istatistikleri yazdırır görürsünüz.

    System.TimeoutException: Timeout performing GET MyKey, inst: 2, mgr: Inactive,
    queue: 6, qu: 0, qs: 6, qc: 0, wr: 0, wq: 0, in: 0, ar: 0,
    IOCP: (Busy=6,Free=994,Min=4,Max=1000),
    WORKER: (Busy=3,Free=997,Min=4,Max=1000)

Merhaba önceki örnekte için ıocp Açılırken iş parçacığı 6 meşgul iş parçacığı vardır ve yapılandırılmış tooallow 4 en az iş parçacığı Merhaba sistemdir görebilirsiniz. Bu durumda, hello istemci büyük olasılıkla iki 500 ms gecikmeler nedeniyle gördünüz 6 > 4.

Büyüme ıocp Açılırken ya da çalışan iş parçacığı kısıtlanan, StackExchange.Redis zaman aşımları isabet olduğunu unutmayın.

### <a name="recommendation"></a>Öneri
Bu bilgiler verildiğinde, müşteriler için ıocp Açılırken ve çalışan iş parçacıkları toosomething hello en düşük yapılandırma değeri hello varsayılan değerinden daha büyük ayarlamak kesinlikle öneririz. Biz, çok yüksek/düşük başka bir uygulama için bir uygulama için hello sağ değer olacağından ne bu değer olmalıdır BT'ye yönergeler veremez. Her müşterinin toofine ayarlama belirli bu ayarı tootheir gereken gereken şekilde bu ayar ayrıca karmaşık uygulamalar, diğer bölümleri hello performansını etkileyebilir. İyi bir başlangıç noktası 200 veya 300, ardından test ve gerektiği gibi ince ayar.

Nasıl tooconfigure bu ayarı:

* ASP.NET, hello kullan ["minIoThreads" yapılandırma ayarı] [ "minIoThreads" configuration setting] hello altında `<processModel>` web.config dosyasındaki yapılandırma öğesi. Azure Web siteleri içinde çalıştırıyorsanız, bu ayar hello yapılandırma seçenekleri gösterilmez. Ancak, hala bu ayarı programlama mümkün tooconfigure olması (aşağıda Application_Start yönteminizi global.asax.cs gelen bakın).

  > [!NOTE] 
  > Merhaba bu yapılandırma öğesinde belirtilen değeri olan bir *çekirdek başına* ayarı. Örneğin, 4 çekirdekli makine olması ve çalışma zamanında, minIOThreads ayarı toobe 200 istiyorsanız kullanacağınız `<processModel minIoThreads="50"/>`.
  >

* ASP.NET dışında hello kullanan [ThreadPool.SetMinThreads(...) ](https://msdn.microsoft.com/library/system.threading.threadpool.setminthreads.aspx) API.

<a name="server-gc"></a>

### <a name="enable-server-gc-tooget-more-throughput-on-hello-client-when-using-stackexchangeredis"></a>StackExchange.Redis kullanırken hello istemci üzerinde daha fazla üretilen işi sunucusu GC tooget etkinleştir
Sunucu GC etkinleştirme hello istemci en iyi duruma getirme ve StackExchange.Redis kullanırken daha iyi performans ve verimlilik sağlar. GC sunucusunda daha fazla bilgi için ve nasıl tooenable, makaleler hello bakın:

* [tooenable sunucusu GC](https://msdn.microsoft.com/library/ms229357.aspx)
* [Çöp toplamanın temelleri](https://msdn.microsoft.com/library/ee787088.aspx)
* [Çöp toplama ve performans](https://msdn.microsoft.com/library/ee851764.aspx)


### <a name="performance-considerations-around-connections"></a>Bağlantıları geçici performans etkenleri

Her fiyatlandırma katmanının istemci bağlantıları, bellek ve bant genişliği için farklı sınırları vardır. Her önbellek boyutunu sağlar, ancak *kadar* belirli bir sayıda bağlantıları, her bağlantı tooRedis ek yükü ile ilişkili. TLS/SSL şifreleme sonucunda CPU ve bellek kullanımı gibi ek yükü örneği olacaktır. Belirtilen önbellek boyutu Hello en fazla bağlantı sınırı hafifçe yüklü bir önbellek varsayar. Varsa yük bağlantı yükünü *artı* istemci işlemleri yükü hello sistem kapasitesini aşıyor, hello geçerli önbellek boyutu hello bağlantı sınırını aştınız değil olsa bile, hello önbellek kapasite sorunları deneyimi.

Her katman için hello farklı bağlantı sınırları hakkında daha fazla bilgi için bkz: [Azure Redis önbelleği fiyatlandırma](https://azure.microsoft.com/pricing/details/cache/). Bağlantıları ve diğer varsayılan yapılandırmaları hakkında daha fazla bilgi için bkz: [varsayılan Redis sunucu yapılandırması](cache-configure.md#default-redis-server-configuration).

<a name="cache-monitor"></a>

### <a name="how-do-i-monitor-hello-health-and-performance-of-my-cache"></a>Merhaba sağlık ve performans my önbelleğinin nasıl izlerim?
Microsoft Azure Redis önbelleği örnekleri hello izlenebilir [Azure portal](https://portal.azure.com). Ölçümleri görüntülemek, ölçümler grafiklerde toohello Sabitle PIN, grafikler izleme hello tarih ve saat aralığı özelleştirme, eklemek ve ölçümleri hello grafikten kaldırabileceğiniz ve belirli koşullar karşılandığında Uyarıları ayarlayın. Daha fazla bilgi için bkz: [İzleyici Azure Redis önbelleği](cache-how-to-monitor.md).

Merhaba Redis önbelleği **kaynak menü** de izleme ve önbellekleri sorun giderme için çeşitli araçlar içerir.

* **Sorunları tanılamak ve** çözümlemek için ortak sorunlar ve stratejileri hakkında bilgi sağlar.
* **Kaynak durumu** kaynağınız izler ve beklendiği gibi çalışıp çalışmadığını belirtir. Hello Azure kaynak sistem durumu hizmeti hakkında daha fazla bilgi için bkz: [Azure kaynak sistem durumu genel bakış](../resource-health/resource-health-overview.md).
* **Yeni destek isteği** seçenekleri tooopen önbelleğiniz için bir destek isteği sağlar.

Bu araçlar, toomonitor hello sistem durumu, Azure Redis önbelleği örnekleri etkinleştirin ve önbelleğe alma uygulamaları yönetmenize yardımcı olur. Daha fazla bilgi için hello "Destek ve sorun giderme ayarları" bölümüne bakın [nasıl tooconfigure Azure Redis önbelleği](cache-configure.md).

<a name="cache-timeouts"></a>

### <a name="why-am-i-seeing-timeouts"></a>Zaman aşımları neden görüyorum?
Zaman aşımları tootalk tooRedis kullandığınız hello istemcisinde gerçekleşir. Bir komut toohello Redis sunucu gönderildiğinde, hello komutu sıraya ve Redis sunucu sonunda hello komutu seçer ve yürütür. Ancak bu işlem sırasında zaman aşımı ve bir özel durum desteklemediğini hello istemci olabilir yan çağırma hello üzerinde oluşturulur. Zaman aşımı sorunlarının giderilmesiyle ilgili daha fazla bilgi için bkz: [istemci-tarafı sorun giderme](cache-how-to-troubleshoot.md#client-side-troubleshooting) ve [StackExchange.Redis zaman aşımı özel](cache-how-to-troubleshoot.md#stackexchangeredis-timeout-exceptions).

<a name="cache-disconnect"></a>

### <a name="why-was-my-client-disconnected-from-hello-cache"></a>Neden my istemci hello önbellekten kesildi?
Merhaba, ortak bir nedenden dolayı bir önbellek bağlantıyı kes verilmiştir.

* İstemci-tarafı neden olur.
  * Merhaba istemci uygulaması yeniden dağıtıldı.
  * Merhaba istemci uygulaması bir ölçeklendirme işlemi gerçekleştirilir.
    * Bulut Hizmetleri ya da Web Apps Hello durumda bu son olabilir tooauto ölçeklendirme.
  * Merhaba ağ katmanı hello istemci tarafında değiştirildi.
  * Merhaba istemci veya hello ağ düğümleri hello istemci hello sunucusu arasındaki geçici hataları oluştu.
  * Merhaba bant genişliği eşik sınırını ulaşılan.
  * CPU bağımlı işlemleri toocomplete çok uzun sürdü.
* Sunucu tarafı neden olur.
  * Teklifi hello standart önbelleğinde hello birincil düğüm toohello ikincil düğümden yük devretme hello Azure Redis önbelleği hizmeti başlatıldı.
  * Azure hello önbellek dağıtıldığı hello örneği düzeltme
    * Bu, Redis sunucu güncelleştirmeleri veya genel VM bakım için olabilir.

### <a name="which-azure-cache-offering-is-right-for-me"></a>Hangi Azure Önbellek teklifi bana uygundur?
> [!IMPORTANT]
> Geçen yıla göre [duyuru](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/), Azure yönetilen önbellek hizmeti ve Azure rol içi önbelleği hizmeti **devre dışı bırakılmış** 30 Kasım 2016. Bizim önerimiz toouse olan [Azure Redis önbelleği](https://azure.microsoft.com/services/cache/). Geçiş hakkında daha fazla bilgi için bkz: [geçirme yönetilen önbellek hizmeti tooAzure Redis Önbelleği'nden](cache-migrate-to-redis.md).
>
>

### <a name="azure-redis-cache"></a>Azure Redis Cache
Azure Redis önbelleği too53 GB yukarı boyutlarda genellikle kullanılabilir olduğunu ve % 99,9 SLA kullanılabilirlik sahip. Merhaba yeni [premium katmanı](cache-premium-tier-intro.md) boyutları too530 GB ve kümeleme, sanal ağ ve % 99,9 SLA ile kalıcılığı için destek sunar.

Microsoft tarafından yönetilen azure Redis önbelleği verir müşteriler hello özelliği toouse bir güvenli, ayrılmış bir Redis önbelleğine. Bu teklif ile tooleverage hello zengin özellik kümesi ve Redis, güvenilir barındırma ve izleme Microsoft tarafından sağlanan ekosistemi alın.

Yalnızca anahtar-değer çiftleri ile ilgilenir geleneksel önbellekleri Redis, yüksek oranda kullanıcı veri türleri için yaygın olarak kullanılır. Ayrıca tooa dize ekleme gibi bu türlerinde atomik işlemleri çalışmayı destekliyor redis; artan bir karma Hello değeri; tooa listesi Ftp'den; bilgi işlem kümesi, union ve kesişimi fark; veya bir sıralanmış küme olarak en yüksek derecelendirme alma hello üyesiyle. Yapılandırma ayarları toomake Redis davranır daha geleneksel bir önbellek ister ve diğer özellikleri işlemleri, pub/alt, Lua komut dosyası, sınırlı bir yaşam süresi anahtarlarla için destek içerir.

Başka bir önemli nokta tooRedis başarı hello sağlıklı, Canlı açık kaynak ekosistemi çevresinde oluşturulmuş olur. Bu hello farklı Redis istemcileri kullanılabilir kümesinde birden çok dil arasında yansıtılır. Bu ekosistem ve çeşitli istemciler Azure içinde oluşturmayı tercih neredeyse tüm iş yükü tarafından kullanılan Azure Redis önbelleği toobe izin verir.

Azure Redis önbelleği kullanmaya başlama hakkında daha fazla bilgi için bkz: [nasıl tooUse Azure Redis önbelleği](cache-dotnet-how-to-use-azure-redis-cache.md) ve [Azure Redis önbelleği belgelerine](index.md).

### <a name="managed-cache-service"></a>Yönetilen önbellek hizmeti
[Önbellek hizmeti 30 Kasım 2016 devre dışı bırakılan yönetilen.](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)

tooview arşivlenmiş belgelerine bakın [arşivlenmiş yönetilen önbellek hizmeti belgeleri](https://msdn.microsoft.com/library/azure/dn386094.aspx).

### <a name="in-role-cache"></a>Rol İçi Önbellek
[Rol içi önbelleği 30 Kasım 2016 devre dışı bırakılan.](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)

tooview arşivlenmiş belgelerine bakın [arşivlenmiş rol içi önbellek belgeleri](https://msdn.microsoft.com/library/azure/dn386103.aspx).

["minIoThreads" configuration setting]: https://msdn.microsoft.com/library/vstudio/7w2sway1(v=vs.100).aspx
