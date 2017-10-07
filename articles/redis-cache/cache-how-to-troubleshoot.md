---
title: "Azure Redis önbelleği aaaHow tootroubleshoot | Microsoft Docs"
description: "Azure Redis önbelleği ile nasıl tooresolve ortak sorunlar hakkında bilgi edinin."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 928b9b9c-d64f-4252-884f-af7ba8309af6
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: sdanie
ms.openlocfilehash: 4e736fce2b6d5200a2a8d802f3f1384b63458cab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-azure-redis-cache"></a>Nasıl tootroubleshoot Azure Redis önbelleği
Bu makalede Azure Redis önbelleği sorunları kategorilerini aşağıdaki hello gidermeye yönelik yönergeler sağlar.

* [İstemci tarafı sorun giderme](#client-side-troubleshooting) - Bu bölüm, tanımlamaya yönergeleri sağlar ve sorunları gidererek neden tooAzure Redis önbelleği bağlanma hello uygulama tarafından.
* [Sunucu tarafı sorun giderme](#server-side-troubleshooting) - Bu bölüm, tanımlamaya yönergeleri sağlar ve Azure Redis önbelleği sunucu tarafı neden üzerinde hello sorunlarını çözme.
* [StackExchange.Redis zaman aşımı özel](#stackexchangeredis-timeout-exceptions) -Bu bölüm, hello StackExchange.Redis istemcisi kullanılırken sorunlarını giderme hakkında bilgi sağlar.

> [!NOTE]
> Sorun giderme adımları bu kılavuzun hello çeşitli toorun çeşitli performans ölçümleri izleyin ve komutları Redis yönergeler içerir. Daha fazla bilgi ve yönergeler için hello hello makalelerinde bkz [ek bilgi](#additional-information) bölümü.
> 
> 

## <a name="client-side-troubleshooting"></a>İstemci tarafı sorunlarını giderme
Bu bölümde Merhaba istemci uygulaması bir koşul nedeniyle oluşan sorun giderme sorunlar açıklanmaktadır.

* [Bellek baskısı hello istemcide](#memory-pressure-on-the-client)
* [Trafik veri bloğu](#burst-of-traffic)
* [Yüksek istemci CPU kullanımı](#high-client-cpu-usage)
* [İstemci tarafı bant genişliği aşıldı](#client-side-bandwidth-exceeded)
* [Büyük istek/yanıt boyutu](#large-requestresponse-size)
* [Hangi Redis oldu toomy verilerde?](#what-happened-to-my-data-in-redis)

### <a name="memory-pressure-on-hello-client"></a>Bellek baskısı hello istemcide
#### <a name="problem"></a>Sorun
Bellek baskısı hello istemci makine üzerinde herhangi bir gecikme olmadan hello Redis örneği tarafından gönderilen verilerin işlenmesini geciktirebilir performans sorunlarını tooall tür yol açar. Bellek baskısı geldiğinde hello sistem diskte olan fiziksel bellek toovirtual bellek toopage verileri genellikle vardır. Bu *sayfa hatalı* nedenler hello sistem tooslow aşağı önemli ölçüde.

#### <a name="measurement"></a>Ölçüm
1. Makine toomake kullanılabilir bellek aşmadığından emin bellek kullanımı izleyin. 
2. İzleyici hello `Page Faults/Sec` performans sayacı. Çoğu sistemi bazı sayfa hataları bile normal işlem sırasında vardır, bu nedenle bu sayfa hataları performans sayacı zaman aşımlarını karşılık gelen ani izleyin.

#### <a name="resolution"></a>Çözüm
İstemci tooa büyük istemci daha fazla belleğe sahip VM boyutunu yükseltebilir veya, bellek kullanım desenlerini tooreduce bellek tüketim derinliklerine.

### <a name="burst-of-traffic"></a>Trafik veri bloğu
#### <a name="problem"></a>Sorun
WINS'e trafiği düşük ile birlikte `ThreadPool` ayarları zaten hello Redis sunucu tarafından gönderilen ancak henüz hello istemci tarafında tüketilen veri işliyor gecikmelere neden olur.

#### <a name="measurement"></a>Ölçüm
İzleyici nasıl, `ThreadPool` istatistikleri değiştirme kodu kullanarak zamanla [şöyle](https://github.com/JonCole/SampleCode/blob/master/ThreadPoolMonitor/ThreadPoolLogger.cs). Hello de bakabilirsiniz `TimeoutException` StackExchange.Redis ileti. Örnek aşağıda verilmiştir:

    System.TimeoutException: Timeout performing EVAL, inst: 8, mgr: Inactive, queue: 0, qu: 0, qs: 0, qc: 0, wr: 0, wq: 0, in: 64221, ar: 0, 
    IOCP: (Busy=6,Free=999,Min=2,Max=1000), WORKER: (Busy=7,Free=8184,Min=2,Max=8191)

İleti yukarıda Hello ilginç bazı sorunlar vardır:

1. Söz konusu hello fark `IOCP` bölümü ve hello `WORKER` bölümüne sahip bir `Busy` hello büyük olan değeri `Min` değeri. Bunun anlamı, `ThreadPool` ayarlarına gereksinim ayarlama.
2. Ayrıca bkz `in: 64221`. Bu, 64211 bayt hello çekirdek yuva katmanında alınan ancak henüz hello uygulama (örneğin StackExchange.Redis) tarafından henüz okunmamış gösterir. Bu, genellikle uygulamanız verileri hello ağdan hello sunucu tooyou gönderiyor olabildiğince çabuk okuma değil, anlamına gelir.

#### <a name="resolution"></a>Çözüm
Yapılandırma, [iş parçacığı havuzu ayarlarını](https://gist.github.com/JonCole/e65411214030f0d823cb) toomake, iş parçacığı havuzu hızlı bir şekilde altında ölçeklendirilmesini emin senaryoları veri bloğu.

### <a name="high-client-cpu-usage"></a>Yüksek istemci CPU kullanımı
#### <a name="problem"></a>Sorun
Yüksek CPU kullanımı hello istemcide hello sistem tooperform istendi hello çalışmak yetişemiyor göstergesidir. Başka bir deyişle, Redis gönderilen hello yanıtı çok hızlı bir şekilde olsa bile hello istemci tooprocess Redis yanıt zamanında başarısız olabilir.

#### <a name="measurement"></a>Ölçüm
Performans sayacı İzleyicisi Merhaba sistem geniş CPU kullanımı hello veya hello Azure Portal aracılığıyla ilişkili. Dikkatli olun değil toomonitor *işlem* CPU tek bir işlem en düşük CPU kullanımı olabilir çünkü hello aynı zaman genel sistem CPU yüksek olabilir. Zaman aşımlarını karşılık ani CPU kullanımını izleyin. Yüksek CPU sonucu olarak, aynı zamanda yüksek görebileceğiniz `in: XXX` değerler `TimeoutException` hata iletileri hello açıklandığı gibi [veri bloğu trafik](#burst-of-traffic) bölümü.

> [!NOTE]
> StackExchange.Redis 1.1.603 ve daha sonra hello içerir `local-cpu` içinde ölçüm `TimeoutException` hata iletileri. Merhaba hello en son sürümünü kullandığından emin olun [StackExchange.Redis NuGet paketi](https://www.nuget.org/packages/StackExchange.Redis/). Sürekli olarak hataları vardır hello en son sürümünü olması önemlidir hello kod toomake, daha sağlam tootimeouts sabit.
> 
> 

#### <a name="resolution"></a>Çözüm
Daha fazla CPU kapasiteli daha büyük VM boyutu tooa yükseltin veya CPU ani neden olan araştırın. 

### <a name="client-side-bandwidth-exceeded"></a>İstemci tarafı bant genişliği aşıldı
#### <a name="problem"></a>Sorun
Farklı boyutlarda istemci makineler sahip sınırlamalar kullanılabilir olan ne kadar üzerindeki ağ bant genişliği. Merhaba istemci aşarsa, kullanılabilir bant genişliğini hello sonra veri hello istemci tarafında hello sunucusuna gönderme olabildiğince çabuk işlenmeyecek. Bu tootimeouts yol açabilir.

#### <a name="measurement"></a>Ölçüm
Bant genişliği kullanımını kod kullanarak zamanla nasıl değiştiğini izlemek [şöyle](https://github.com/JonCole/SampleCode/blob/master/BandWidthMonitor/BandwidthLogger.cs). Bu kod (örneğin, Azure web siteleri) kısıtlı izinleri olan bazı ortamlarda başarılı bir şekilde çalışmayabilir unutmayın.

#### <a name="resolution"></a>Çözüm
İstemci VM boyutunu artırın veya ağ bant genişliği tüketimini azaltabilir.

### <a name="large-requestresponse-size"></a>Büyük istek/yanıt boyutu
#### <a name="problem"></a>Sorun
Büyük bir istek/yanıt zaman aşımlarına neden olabilir. Örnek olarak, istemcide yapılandırılan, zaman aşımı değeri 1 saniyedir varsayalım. Uygulamanız (örneğin, iki anahtar istekleri 'A' ve 'B') Merhaba, aynı zamanda (aynı fiziksel ağ bağlantısını hello kullanarak). Hem 'A' ve 'B' hello kablo toohello sunucuda bir hello sonra hello yanıtlar için beklemeden diğer gönderdiği istekleri, çoğu istemci isteklerinin "Pipelining" destekler. Merhaba sunucu hello yanıtları geri hello aynı gönderecek sırası. Yanıt 'A' büyükse yetecek kadar sonraki istekleri için hello zaman aşımı çoğunu yemek. 

Bu senaryo aşağıdaki örneğine hello gösterir. Bu senaryoda, 'Bir ''i ve 'B' hello sunucu yanıtları 'A' ve 'B' hızlı gönderme başlar, ancak veri aktarım süreleri nedeniyle 'B' arkasında takılı hızlı bir şekilde, gönderilen istek hello diğer istek ve zaman aşımına rağmen hello sunucu hızlı bir şekilde yanıt verdi.

    |-------- 1 Second Timeout (A)----------|
    |-Request A-|
         |-------- 1 Second Timeout (B) ----------|
         |-Request B-|
                |- Read Response A --------|
                                           |- Read Response B-| (**TIMEOUT**)



#### <a name="measurement"></a>Ölçüm
Zor bir toomeasure budur. İstemci kodu tootrack büyük istekleri ve yanıtları temelde tooinstrument vardır. 

#### <a name="resolution"></a>Çözüm
1. Redis çok sayıda birkaç büyük değerler yerine küçük değerler için optimize edilmiştir. Merhaba tercih edilen toobreak verilerinizi ilgili küçük değerler çözümüdür. Merhaba bkz [redis için hello ideal değer boyutu aralığı nedir? 100 KB çok büyük? ](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ) sonrası küçük değerler neden önerilen geçici Ayrıntılar için.
2. Merhaba boyutunu artırın (için istemci ve Redis önbelleği sunucu), VM veriyi azaltma tooget daha yüksek bant genişliği özellikleri, daha büyük yanıt süreleri aktarım. Yalnızca hello sunucuda alma daha fazla bant genişliği Not veya yalnızca üzerinde hello istemci yeterli olmayabilir. Bant genişliği kullanımı ölçmek ve şu anda VM hello boyutunu toohello özelliklerini karşılaştırın.
3. Merhaba sayısını artırmak `ConnectionMultiplexer` farklı bağlantıları üzerinden kullanın ve hepsini istekleri nesneleri.

### <a name="what-happened-toomy-data-in-redis"></a>Hangi Redis oldu toomy verilerde?
#### <a name="problem"></a>Sorun
T belirli veri toobe my Azure Redis önbelleği örneğine bekleniyordu ancak toobe yok gibi görünüyor alamadık.

#### <a name="resolution"></a>Çözüm
Bkz: [Redis ne oldu toomy verileri?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md) olası nedenleri ve çözümlemeleri için.

## <a name="server-side-troubleshooting"></a>Sunucu tarafı sorunlarını giderme
Bu bölümde hello önbellek sunucusu bir koşul nedeniyle oluşan sorun giderme sorunlar açıklanmaktadır.

* [Bellek baskısı hello sunucuda](#memory-pressure-on-the-server)
* [Yüksek CPU kullanımı / sunucu iş yükü](#high-cpu-usage-server-load)
* [Sunucu tarafı bant genişliği aşıldı](#server-side-bandwidth-exceeded)

### <a name="memory-pressure-on-hello-server"></a>Bellek baskısı hello sunucuda
#### <a name="problem"></a>Sorun
Bellek baskısı hello sunucu tarafında tooall tür isteklerinin işlenmesini geciktirebilir performans sorunlarına yol açar. Bellek baskısı geldiğinde hello sistem diskte olan fiziksel bellek toovirtual bellek toopage verileri genellikle vardır. Bu *sayfa hatalı* nedenler hello sistem tooslow aşağı önemli ölçüde. Bu bellek baskısı birkaç olası nedenleri şunlardır: 

1. Merhaba önbellek toofull kapasite verilerle doldurduktan. 
2. Redis yüksek bellek parçalanması - çoğunlukla büyük nesneler depolayarak neden görmesini (Redis - bkz: hello gibi küçük bir nesneler için iyileştirilmiş [hello ideal değer boyutu redis için aralık nedir? 100 KB çok büyük? ](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ) sonrası ayrıntılarını). 

#### <a name="measurement"></a>Ölçüm
Redis bu sorunu belirlemenize yardımcı olabilecek iki ölçümleri kullanıma sunar. Merhaba ilk olan `used_memory` ve hello diğer `used_memory_rss`. [Bu ölçümler](cache-how-to-monitor.md#available-metrics-and-reporting-intervals) hello Azure Portal veya hello aracılığıyla kullanılabilir [Redis bilgisi](http://redis.io/commands/info) komutu.

#### <a name="resolution"></a>Çözüm
Toohelp Koru bellek kullanımı sağlıklı hale getirebilir birkaç olası değişiklikleri şunlardır:

1. [Bellek ilkesini yapılandırma](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) ve anahtarlarınızı üzerinde zaman aşımı değeri ayarlayın. Bu parçalanma varsa yeterli olmayabilir olduğunu unutmayın.
2. [Maxmemory ayrılmış bir değer](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) diğer bir deyişle büyüklükte toocompensate bellek parçalanması için.
3. Büyük önbelleğe alınmış nesnelerinizi küçük ilgili nesneleri içine bölün.
4. [Ölçek](cache-how-to-scale.md) tooa daha büyük önbellek boyutu.
5. Kullanıyorsanız bir [premium önbelleği etkin Redis kümesi ile](cache-how-to-premium-clustering.md) yapabilecekleriniz [parça hello sayısını artırmak](cache-how-to-premium-clustering.md#change-the-cluster-size-on-a-running-premium-cache).

### <a name="high-cpu-usage--server-load"></a>Yüksek CPU kullanımı / sunucu iş yükü
#### <a name="problem"></a>Sorun
Yüksek CPU kullanımı, Redis gönderilen hello yanıtı çok hızlı bir şekilde olsa bile hello istemci tarafı tooprocess Redis yanıt zamanında yük devredebildiğini anlamına gelebilir.

#### <a name="measurement"></a>Ölçüm
Performans sayacı İzleyicisi Merhaba sistem geniş CPU kullanımı hello veya hello Azure Portal aracılığıyla ilişkili. Dikkatli olun değil toomonitor *işlem* CPU tek bir işlem en düşük CPU kullanımı olabilir çünkü hello aynı zaman genel sistem CPU yüksek olabilir. Zaman aşımlarını karşılık ani CPU kullanımını izleyin.

#### <a name="resolution"></a>Çözüm
[Ölçek](cache-how-to-scale.md) tooa daha büyük önbellek katmanı ile daha fazla CPU kapasitesini veya CPU ani neden olan araştırın. 

### <a name="server-side-bandwidth-exceeded"></a>Sunucu tarafı bant genişliği aşıldı
#### <a name="problem"></a>Sorun
Farklı boyutlarda önbellek örneğe sahip sınırlamalar kullanılabilir olan ne kadar üzerindeki ağ bant genişliği. Merhaba sunucu hello kullanılabilir bant genişliğini aşarsa, ardından veri toohello istemci hızlı bir şekilde gönderilmez. Bu tootimeouts yol açabilir.

#### <a name="measurement"></a>Ölçüm
Merhaba izleyebilirsiniz `Cache Read` hello belirtilen Raporlama zaman aralığı boyunca önbelleğinden hello megabayt (MB/sn) saniye başına okunan veriler hello miktarıdır ölçüm. Bu değer bu önbelleği tarafından kullanılan toohello ağ bant genişliği karşılık gelir. Sunucu tarafı ağ bant genişliği sınırlarını uyarıları tooset istiyorsanız, bunu kullanarak bunları oluşturabilirsiniz `Cache Read` sayacı. Merhaba değerleriyle, okumalar karşılaştırmak [Bu tablo](cache-faq.md#cache-performance) çeşitli önbellek fiyatlandırma katmanlarına ve boyutları için bant genişliği sınırlarını gözlenen hello için.

#### <a name="resolution"></a>Çözüm
Fiyatlandırma katmanı ve önbellek boyutu için en yüksek bant genişliği gözlenen hello yakın tutarlı olup olmadığını düşünün [ölçeklendirme](cache-how-to-scale.md) fiyatlandırma katmanı ya da daha fazla ağ bant genişliği olan boyutu, hello değerleri kullanarak tooa [Bu tablo](cache-faq.md#cache-performance) bir kılavuz olarak.

## <a name="stackexchangeredis-timeout-exceptions"></a>StackExchange.Redis zaman aşımı özel durumlar
StackExchange.Redis adlı bir yapılandırma ayarı kullanır `synctimeout` varsayılan değer 1000 MS olduğu zaman uyumlu işlemler için. Zaman uyumlu çağrıyı içinde tamamlanmazsa hello aşağıdaki örneğine zaman aşımı hatası benzer bir toohello zaman, hello StackExchange.Redis istemcisi atar belirlenen.

    System.TimeoutException: Timeout performing MGET 2728cc84-58ae-406b-8ec8-3f962419f641, inst: 1,mgr: Inactive, queue: 73, qu=6, qs=67, qc=0, wr=1/1, in=0/0 IOCP: (Busy=6, Free=999, Min=2,Max=1000), WORKER (Busy=7,Free=8184,Min=2,Max=8191)


Bu hata iletisini toohello nedeni ve olası çözüm hello sorunun noktası yardımcı olabilecek ölçümleri içerir. Merhaba aşağıdaki tabloda hello hata iletisi ölçümleri ayrıntılarını içerir.

| Hata iletisi ölçümü | Ayrıntılar |
| --- | --- |
| INST |Merhaba son zaman dilimi içinde: 0 komutları verilen |
| Mgr |Merhaba yuva Yöneticisi gerçekleştirip `socket.select` yani hello OS tooindicate bir şey var olan bir yuvayı istemesi toodo; temelde: hello okuyucu değil etkin olarak okuma hello ağdan herhangi bir şey yok düşündüğünüz değil çünkü toodo |
| Sırası |73 toplam devam eden işlemler vardır |
| Pro |Merhaba devam eden işlemlerin 6 hello gönderilmemiş sıradaki ve toohello giden ağ yazılmadı |
| qs |he devam eden işlemlerin 67 toohello sunucu gönderildi ancak yanıt henüz kullanılabilir değil. Merhaba yanıt olabilir `Not yet sent by hello server` veya`sent by hello server but not yet processed by hello client.` |
| QC |Merhaba devam eden işlemlerin 0 yanıtları gördünüz ancak henüz son tamamlandı olarak işaretlenmedi hello tamamlama döngüde toowaiting |
| wr |Etkin bir yazıcı yoktur (6 gönderilmemiş istekleri hello anlamı değil yoksayılır) bayt/activewriters |
| İçinde |Hiçbir etkin okuyucular vardır ve NIC bayt/activereaders hello üzerinde okuma kullanılabilir toobe sıfır bayt olan |

### <a name="steps-tooinvestigate"></a>Adımları tooinvestigate
1. En iyi uygulama emin yaptıkça düzeni tooconnect hello StackExchange.Redis istemcisi kullanılırken aşağıdaki hello kullanıyor.

    ```c#
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("cachename.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ````

    Daha fazla bilgi için bkz: [toohello önbelleği StackExchange.Redis kullanarak bağlanmak](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache).

1. Azure Redis önbelleği ve Merhaba istemci uygulaması hello olduğundan emin olun azure'da aynı bölgede. Örneğin, zaman aşımı önbelleğiniz Doğu ABD olduğunu ancak hello istemci olduğunda Batı ABD ve hello isteği içinde hello tamamlamak değil elde `synctimeout` aralığı veya alınırken zaman aşımı yerel geliştirme makinenizden ayıklarken. 
   
    Toohave hello önbellek tavsiye ve'de hello istemcisi aynı hello Azure bölgesi. Çapraz bölge çağrıları içeren bir senaryo varsa hello ayarlamalısınız `synctimeout` aralığı tooa değeri ekleyerek hello varsayılan 1000 ms aralığından daha yüksek bir `synctimeout` hello bağlantı dizesindeki özelliği. Merhaba aşağıdaki örnekte gösterilir StackExchange.Redis önbelleği bağlantı dizesi parçacığıyla bir `synctimeout` 2000 MS.
   
        synctimeout=2000,cachename.redis.cache.windows.net,abortConnect=false,ssl=true,password=...
2. Merhaba hello en son sürümünü kullandığından emin olun [StackExchange.Redis NuGet paketi](https://www.nuget.org/packages/StackExchange.Redis/). Sürekli olarak hataları vardır hello en son sürümünü olması önemlidir hello kod toomake, daha sağlam tootimeouts sabit.
3. Bant genişliği sınırlamaları hello sunucu veya istemci tarafından bağlı isteği varsa, bunlar için daha uzun sürer toocomplete ve böylece zaman aşımlarına neden olabilir. toosee toonetwork bant genişliği hello sunucuda nedeniyle, zaman aşımı olup olmadığını görmek [sunucu tarafı bant genişliği aşıldı](#server-side-bandwidth-exceeded). zaman aşımı tooclient ağ bant genişliği ise toosee bkz [istemci tarafı bant genişliği aşıldı](#client-side-bandwidth-exceeded).
4. CPU alma hello sunucusunda veya hello istemci bağlı?
   
   * CPU ile Merhaba isteği toonot neden olabilecek, istemcide bağlıysa onay içinde hello işlenmesi `synctimeout` aralığı, böylece bir zaman aşımı neden. Tooa büyük istemci taşıma veya hello yükü dağıtma toocontrol bu yardımcı olabilir. 
   * CPU alıyorsanız onay hello izleyerek hello sunucuda bağlı `CPU` [performans ölçüm önbelleğe](cache-how-to-monitor.md#available-metrics-and-reporting-intervals). Redis CPU bağımlı olanlar neden olabilir durumdayken gelen tootimeout istekleri. tooaddress bu hello dağıtabilirsiniz premium önbelleğinde birden fazla parça genelinde yüklemek veya tooa büyük veya fiyatlandırma katmanına yükseltin. Daha fazla bilgi için bkz: [sunucu tarafı bant genişliği aşıldı](#server-side-bandwidth-exceeded).
5. Uzun süre tooprocess hello sunucuda alma komutları var mı? Uzun süre tooprocess hello redis-sunucuda sürüyor komutları uzun süre çalışan zaman aşımlarına neden olabilir. Uzun süre çalışan komutlar bazı örnekleri şunlardır `mget` anahtarları, çok sayıda ile `keys *` veya lua betikleri'kötü yazılmış. Merhaba redis CLI istemcisini kullanarak tooyour Azure Redis önbelleği örneğine bağlanın veya hello kullan [Redis konsol](cache-configure.md#redis-console) ve çalışma hello [SlowLog](http://redis.io/commands/slowlog) beklenenden uzun sürüyor isteği yoksa komutu toosee. Redis sunucu ve StackExchange.Redis daha az büyük istekleri yerine çok sayıda küçük istekleri için iyileştirilir. Verilerinizi daha küçük parçalara bölme şeyleri burada artırabilir. 
   
    Merhaba redis CLI ve stunnel kullanarak toohello Azure Redis önbelleği SSL uç noktasını bağlanma hakkında daha fazla bilgi için bkz [Redis Önizleme sürümü için ASP.NET oturum durumu sağlayıcısı Duyurusu](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) blog postası. Daha fazla bilgi için bkz: [SlowLog](http://redis.io/commands/slowlog).
6. Yüksek Redis sunucusu yükü zaman aşımlarına neden olabilir. Merhaba izleyerek hello sunucu iş yükü izleyebilirsiniz `Redis Server Load` [performans ölçüm önbelleğe](cache-how-to-monitor.md#available-metrics-and-reporting-intervals). Merhaba redis sunucu isteklerini işleme hiçbir boşta kalma süresi ile meşgul bir sunucu yükü 100 (en fazla değer) belirtir. toosee belirli isteklerini hello sunucu özelliği, tüm alıyorsanız hello SlowLog komutunu çalıştırın, hello önceki paragrafta açıklanan. Daha fazla bilgi için bkz: [yüksek CPU kullanımı / sunucu iş yükü](#high-cpu-usage-server-load).
7. Bir ağ blip neden olan hello istemci tarafında başka bir olay oluştu? Merhaba istemcide (web, çalışan rolü veya bir Iaas VM) istemci sayısının hello yukarı veya aşağı Ölçeklendirmesi veya hello istemci yeni bir sürümü dağıtma gibi bir olay olup olmadığını denetleyin veya Otomatik ölçek etkin mi? Bizim otomatik ölçeklendirme veya yukarı/aşağı Ölçeklendirmesi neden olabilir. bulduk testinde giden ağ bağlantısı için birkaç saniye kaybolabilir. StackExchange.Redis kod dayanıklı toosuch olayları ve yeniden bağlanır. Yeniden bağlantı bu süre boyunca hello sırasındaki tüm isteklerin zaman aşımı olabilir.
8. Çeşitli küçük istekleri toohello zaman aşımına uğradı Redis önbelleği önceki büyük bir istek oluştu? parametre hello `qs` hello hata iletisi, kaç istek hello istemci toohello sunucudan gönderildi ancak yanıt henüz işlenmedi bildirir. StackExchange.Redis tek bir TCP bağlantı kullanır ve bir yanıt aynı anda yalnızca okuyabilir çünkü bu değer büyüyor. Merhaba ilk işlemi zaman aşımına uğradı olsa bile, hello sunucu denetleyicisinden gönderilen hello veri durdurmaz ve bu, zaman aşımı neden tamamlanana kadar diğer istekleri engellenir. Bir zaman aşımı toominimize hello olasılığı, önbellek, iş yükü için yeterince büyük olduğundan emin olmanın ve büyük değerler daha küçük parçalara bölme çözümüdür. Başka bir olası toouse havuzu çözümdür `ConnectionMultiplexer` nesneleri, istemci ve az yüklenen hello seçin `ConnectionMultiplexer` yeni bir istek gönderirken. Bu tek bir zaman aşımı diğer istekleri tooalso zaman aşımı neden olmasını engellemeye.
9. Kullanıyorsanız `RedisSessionStateprovider`, hello yeniden deneme zaman aşımı doğru ayarladığınızdan emin olun. `retrytimeoutInMilliseconds`daha yüksek olmalıdır `operationTimeoutinMilliseonds`, aksi takdirde hiçbir yeniden denemeler meydana gelir. Aşağıdaki örneğine hello içinde `retrytimeoutInMilliseconds` too3000 ayarlanır. Daha fazla bilgi için bkz: [Azure Redis önbelleği için ASP.NET oturum durumu sağlayıcısı](cache-aspnet-session-state-provider.md) ve [nasıl toouse hello yapılandırma parametrelerinin oturum durumu sağlayıcısı ve çıkış önbelleği sağlayıcısı](https://github.com/Azure/aspnet-redis-providers/wiki/Configuration).

    <add
      name="AFRedisCacheSessionStateProvider"
      type="Microsoft.Web.Redis.RedisSessionStateProvider"
      host="enbwcache.redis.cache.windows.net"
      port="6380"
      accessKey="…"
      ssl="true"
      databaseId="0"
      applicationName="AFRedisCacheSessionState"
      connectionTimeoutInMilliseconds = "5000"
      operationTimeoutInMilliseconds = "1000"
      retryTimeoutInMilliseconds="3000" />


1. Tarafından hello Azure Redis önbelleği sunucusunda bellek kullanımı denetleyin [izleme](cache-how-to-monitor.md#available-metrics-and-reporting-intervals) `Used Memory RSS` ve `Used Memory`. Bir çıkarma İlkesi yerinde ise, Redis başlatır çıkarma, anahtarları ne zaman `Used_Memory` ulaştığında hello önbellek boyutu. İdeal olarak, `Used Memory RSS` yalnızca biraz daha yüksek olmalıdır `Used memory`. Büyük bir fark (iç veya dış. bellek parçalanması olduğu anlamına gelir. Zaman `Used Memory RSS` olan değerinden `Used Memory`, hello önbellek parçası, hello işletim sistemi tarafından takas anlamına gelir. Bu durumda, bazı önemli gecikmeleri bekleyebilirsiniz. Redis üzerinden denetim olmadığından nasıl kendi ayırmaları toomemory sayfaları, yüksek eşlendi `Used Memory RSS` genellikle hello bellek kullanımında ani sonucudur. Redis bellek boşaltır, hello bellek geri toohello ayırıcısı verilir ve hello ayırıcısı olabilir veya hello bellek geri toohello sistem vermeyebilir. Merhaba arasında bir farklılık olabilir `Used Memory` hello işletim sistemi tarafından bildirilen değeri ve bellek tüketimi. Son olabilir bellek kullanılan ve Redis, ancak geri toohello sistem verilen değil serbest toohello olgu. toohelp etkisini bellek sorunları hello aşağıdaki adımları gerçekleştirebilirsiniz.
   
   * Böylece hello sistemde bellek sınırlamaları sunmayı çalışmayan hello önbellek tooa büyük boyutu yükseltin.
   * Zaman aşımı değeri hello anahtarları eski değerleri proaktif olarak çıkarılacak şekilde ayarlayın.
   * İzleyici hello hello `used_memory_rss` ölçüm önbelleğe. Bu değer, önbellek boyutunu hello yaklaştığında, performans sorunlarını görmesini büyük olasılıkla toostart demektir. Premium önbelleği kullanıyorsanız veya tooa daha büyük önbellek boyutu yükseltme hello veri birden fazla parça dağıtır.
   
   Daha fazla bilgi için bkz: [hello sunucuda bellek baskısı](#memory-pressure-on-the-server).

## <a name="additional-information"></a>Ek bilgiler
* [Hangi Redis Önbelleği teklifini ve boyutunu kullanmalıyım?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)
* [Nasıl ı Kıyaslama test ve hello my önbelleğinin performansını?](cache-faq.md#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* [Redis komutları nasıl çalıştırabilir miyim?](cache-faq.md#how-can-i-run-redis-commands)
* [Nasıl toomonitor Azure Redis önbelleği](cache-how-to-monitor.md)

