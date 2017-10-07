---
title: "Azure Redis önbelleği aaaHow toomonitor | Microsoft Docs"
description: "Nasıl toomonitor hello sağlık ve performans, Azure Redis önbelleği örnekleri öğrenin"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 7e70b153-9c87-4290-85af-2228f31df118
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: c474d485dfcbb109d5bb634a980f6db080598e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-azure-redis-cache"></a>Nasıl toomonitor Azure Redis önbelleği
Azure Redis önbelleği kullanan [Azure İzleyici](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) tooprovide önbellek örneklerinizi izleme için çeşitli seçenekler. Ölçümleri görüntülemek, ölçümler grafiklerde toohello Sabitle PIN, grafikler izleme hello tarih ve saat aralığı özelleştirme, eklemek ve ölçümleri hello grafikten kaldırabileceğiniz ve belirli koşullar karşılandığında Uyarıları ayarlayın. Bu araçlar, toomonitor hello sistem durumu, Azure Redis önbelleği örnekleri etkinleştirin ve önbelleğe alma uygulamaları yönetmenize yardımcı olur.

Ölçümleri kullanarak Azure Redis önbelleği örnekleri toplanan Redis hello [bilgisi](http://redis.io/commands/info) 30 gün boyunca dakika ve otomatik olarak depolanan başına yaklaşık iki kez komutu (bkz [verme önbellek ölçümleri](#export-cache-metrics) tooconfigure bir farklı bekletme ilkesi) bunlar kullanılabilir hello ölçümler grafiklerde görüntülenir ve uyarı kuralları tarafından değerlendirilen şekilde. Her önbellek ölçümü için kullanılan hello farklı bilgi değerleri hakkında daha fazla bilgi için bkz: [kullanılabilir Ölçümler ve aralıklarını raporlama](#available-metrics-and-reporting-intervals).

<a name="view-cache-metrics"></a>

tooview önbellek ölçümleri [Gözat](cache-configure.md#configure-redis-cache-settings) tooyour önbelleği örneğine hello [Azure portal](https://portal.azure.com).  Azure Redis önbelleği hello üzerinde bazı yerleşik grafiklerde sağlar **genel bakış** dikey penceresinde ve hello **Redis ölçümleri** dikey. Her bir grafik ekleme veya kaldırma ölçümleri ve aralığı raporlama hello değiştirme özelleştirilebilir.

![Ölçümleri redis](./media/cache-how-to-monitor/redis-cache-redis-metrics-blade.png)

## <a name="view-pre-configured-metrics-charts"></a>Önceden yapılandırılmış ölçümleri grafikleri görüntüleme

Merhaba **genel bakış** dikey önceden yapılandırılmış izleme grafikleri aşağıdaki hello sahiptir.

* [İzleme grafikleri](#monitoring-charts)
* [Kullanım grafikleri](#usage-charts)

### <a name="monitoring-charts"></a>İzleme grafikleri
Merhaba **izleme** hello bölümünde **genel bakış** dikey sahip **İsabetli ve isabetsiz okuma**, **alır ve ayarlar**, **bağlantıları**, ve **toplam komutları** grafik.

![İzleme grafikleri](./media/cache-how-to-monitor/redis-cache-monitoring-part.png)

### <a name="usage-charts"></a>Kullanım grafikleri
Merhaba **kullanım** hello bölümünde **genel bakış** dikey sahip **Redis sunucu iş yükü**, **bellek kullanımı**, **ağ bant genişliği** , ve **CPU kullanımı** grafikleri ve aynı zamanda, hello görüntüler **fiyatlandırma katmanı** hello önbellek örneği için.

![Kullanım grafikleri](./media/cache-how-to-monitor/redis-cache-usage-part.png)

Merhaba **fiyatlandırma katmanı** görüntüler hello önbellek fiyatlandırma katmanı ve çok kullanılabilir[ölçek](cache-how-to-scale.md) önbellek tooa fiyatlandırma katmanı farklı hello.

## <a name="view-metrics-with-azure-monitor"></a>Azure İzleyicisi ile metrikleri görüntüleyin
tooview Redis ölçümleri ve Azure İzleyicisi'ni kullanarak özel grafikler oluşturma tıklatın **ölçümleri** hello gelen **kaynak menü**ve istenen hello ölçümleri kullanarak, grafik türü, aralık raporlama grafiğinizi özelleştirmek ve Daha fazla.

![Ölçümleri redis](./media/cache-how-to-monitor/redis-cache-monitor.png)

Azure İzleyicisi'ni kullanarak ölçümleri ile çalışma hakkında daha fazla bilgi için bkz: [Microsoft Azure ölçümlerini genel bakış](../monitoring-and-diagnostics/monitoring-overview-metrics.md).

<a name="how-to-view-metrics-and-customize-chart"></a>
<a name="enable-cache-diagnostics"></a>
## <a name="export-cache-metrics"></a>Önbellek ölçümleri dışarı aktarma
Önbellek ölçümleridir Azure İzleyicisi'nde varsayılan olarak, [30 gün boyunca depolanan](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) ve ardından silinir. toopersist önbellek ölçümlerinizi 30 günden uzun, şunları yapabilirsiniz [bir depolama hesabı atamak](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md) ve belirtin bir **bekletme (gün)** önbellek ölçümlerinizi için ilke. 

tooconfigure önbellek ölçümlerinizi için bir depolama hesabı:

1. Tıklatın **tanılama** hello gelen **kaynak menü** hello içinde **Redis önbelleği** dikey.
2. Tıklatın **üzerinde**.
3. Denetleme **arşiv tooa depolama hesabı**.
4. Hangi toostore hello önbellek ölçümlerini Hello depolama hesabı seçin.
5. Merhaba denetleyin **1 dakika** onay kutusunu ve belirtin bir **bekletme (gün)** ilkesi. Değil tooapply herhangi bir bekletme ilkesi ve veri sonsuza kadar korumak istiyorsanız, Ayarla **bekletme (gün)** çok**0**.
6. **Kaydet** düğmesine tıklayın.

![Tanılama redis](./media/cache-how-to-monitor/redis-cache-diagnostics.png)

>[!NOTE]
>Toplama tooarchiving, önbellek ölçümleri toostorage kullanabileceğiniz [tooan olay hub'ı akış veya tooLog Analytics Gönder](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).
>
>

tooaccess, ölçümlerinizi hello daha önce bu makalesinde açıklandığı gibi Azure portal'ın görüntüleyebilir ve ayrıca erişmesine hello kullanarak [Azure İzleyici ölçümleri REST API](../monitoring-and-diagnostics/monitoring-overview-metrics.md#access-metrics-via-the-rest-api).

> [!NOTE]
> Depolama hesaplarını değiştirirseniz, önceden yapılandırılmış hello depolama hesabındaki hello veri indirme için kullanılabilir kalır, ancak hello Azure portalında görüntülenmez.  
> 
> 

## <a name="available-metrics-and-reporting-intervals"></a>Kullanılabilir Ölçümler ve aralıklarını raporlama
Önbellek ölçümleri de dahil olmak üzere çeşitli raporlama aralıkları kullanarak raporlanır **saati aşan**, **Bugün**, **geçen hafta**, ve **özel**. Merhaba **ölçüm** her ölçümleri grafiği için dikey hello grafikte her ölçümü için hello ortalama, minimum ve maksimum değerleri görüntüler ve bir toplama aralığı raporlama hello için bazı ölçümleri görüntüler. 

Her ölçüm iki sürümlerini içerir. Bir ölçüm ölçer kullanmak önbellekleri ve hello tüm önbelleği için performans [Kümeleme](cache-how-to-premium-clustering.md), içeren hello ölçüm ikinci sürümü `(Shard 0-9)` hello adı ölçümleri performans bir önbellekte tek parça. Örneğin bir önbellek 4 parça varsa `Cache Hits` hello hello tüm önbelleği isabetli okuma sayısının toplam tutar ve `Cache Hits (Shard 3)` yalnızca hello İsabeti bu parça hello önbelleği için.

> [!NOTE]
> Merhaba önbellek hiçbir bağlı etkin istemci uygulamalarıyla boş olsa bile, bağlanan istemciler, bellek kullanımı ve gerçekleştirilen işlemler gibi bazı önbellek etkinliği görebilirsiniz. Bu etkinlik bir Azure Redis önbelleği örneği hello işlemi sırasında normaldir.
> 
> 

| Ölçüm | Açıklama |
| --- | --- |
| İsabetli Önbellek okuma sayısı |Hello hello belirtilen raporlama aralığı sırasında anahtar başarılı arama sayısı. Bu çok eşler`keyspace_hits` hello Redis gelen [bilgisi](http://redis.io/commands/info) komutu. |
| İsabetsiz önbellek okuma sayısı |Merhaba hello belirtilen raporlama aralığı sırasında başarısız anahtar arama sayısı. Bu çok eşler`keyspace_misses` gelen hello Redis bilgileri komutu. Önbellek isabetsizliği hello önbellek ile ilgili bir sorun var. mutlaka anlamına gelmez. Örneğin, edilgen önbellek düzeni programlama hello kullanırken, bir uygulama hello önbelleğinde bir öğe için ilk arar. Merhaba öğesi (önbellek isabetsizliği) yoksa, hello öğe hello veritabanından alınır ve gelecek sefer için toohello önbelleğine eklenmiş. Önbellek isabetsizliği edilgen önbellek düzeni programlama hello normal davranışını ' dir. İsabetsiz önbellek okuma sayısı Hello sayısı beklenenden daha yüksek ise ve hello önbellekten okur doldurur hello uygulama mantığı inceleyin. Öğeleri çıkarılacak toomemory baskısı nedeniyle hello önbelleğinden sonra bazı önbellek isabetsizlik olabilir, ancak daha iyi bir ölçüm toomonitor bellek baskısı için olacaktır `Used Memory` veya `Evicted Keys`. |
| Bağlanan istemciler |istemci bağlantıları toohello önbellek hello belirtilen raporlama aralığı sırasında Hello sayısı. Bu çok eşler`connected_clients` gelen hello Redis bilgileri komutu. Bir kez hello [bağlantı sınırı](cache-configure.md#default-redis-server-configuration) toohello önbellek başarısız olur sonraki bağlantı denemelerinde ulaştı. Hiçbir etkin istemci uygulaması olsa bile var. hala bağlı istemci toointernal işlemleri ve bağlantıları son birkaç örnekleri unutmayın. |
| Çıkarılan anahtarları |Merhaba sırasında hello hello önbellekten çıkarılmasına öğe sayısı belirtilen raporlama aralığı son toohello `maxmemory` sınırı. Bu çok eşler`evicted_keys` gelen hello Redis bilgileri komutu. |
| Süresi dolan anahtarları |öğe sayısı Hello hello önbellekten hello belirtilen Raporlama zaman aralığı boyunca süresi. Bu değeri çok eşler`expired_keys` gelen hello Redis bilgileri komutu. |
| Toplam anahtarları  | Merhaba maksimum süre raporlama geçmiş hello sırasında hello önbelleğindeki anahtar sayısı. Bu çok eşler`keyspace` gelen hello Redis bilgileri komutu. Etkin, kümeleme ile önbellekler için ölçümleri sistem temel hello tooa sınırlaması nedeniyle hello maksimum anahtar sayısı aralığı raporlama hello sırasında vardı hello parça anahtarları hello sayısının toplam anahtarlarını döndürür.  |
| Alır |Merhaba önbelleğinden get işlemleri hello belirtilen raporlama aralığı sırasında Hello sayısı. Hello aşağıdaki hello toplamı değerleri Redis bilgisi hello tüm komutu bu değerdir: `cmdstat_get`, `cmdstat_hget`, `cmdstat_hgetall`, `cmdstat_hmget`, `cmdstat_mget`, `cmdstat_getbit`, ve `cmdstat_getrange`, ve eşdeğer toohello İsabetli Önbellek okuma sayısının toplam ve isabetsiz aralığı raporlama hello sırasında. |
| Redis sunucu iş yükü |hangi hello Redis işlemekle meşgul ve iletiler için boşta beklenmiyor sunucusudur döngüleri Hello yüzdesi. Bu sayaç hello Redis sunucu performans tavan erişti ve hello CPU işleyemiyor gelir 100 ulaşırsa herhangi daha hızlı çalışır. Yüksek Redis sunucusu yükü görüyorsanız, zaman aşımı özel durumlarında hello istemci görürsünüz. Bu durumda ölçeklendirmeyi veya birden çok önbelleklerine verilerinizi bölümleme düşünmelisiniz. |
| Ayarlar |ayarlama işlemleri toohello önbellek hello sırasında Hello sayısı raporlama aralık belirtildi. Hello aşağıdaki hello toplamı değerleri Redis bilgisi hello tüm komutu bu değerdir: `cmdstat_set`, `cmdstat_hset`, `cmdstat_hmset`, `cmdstat_hsetnx`, `cmdstat_lset`, `cmdstat_mset`, `cmdstat_msetnx`, `cmdstat_setbit`, `cmdstat_setex`, `cmdstat_setrange` , ve `cmdstat_setnx`. |
| Toplam işlemler |komutları sırasında hello hello önbellek sunucusu tarafından işlenen toplam sayısı Hello raporlama aralık belirtildi. Bu değeri çok eşler`total_commands_processed` gelen hello Redis bilgileri komutu. Azure Redis önbelleği tamamen pub/alt için kullanıldığında olacağı için hiçbir ölçümleri Not `Cache Hits`, `Cache Misses`, `Gets`, veya `Sets`, olacaktır, ancak `Total Operations` hello önbelleği kullanımını pub/alt işlemleri yansıtacak ölçümleri. |
| Kullanılan bellek |MB cinsinden hello önbelleğindeki anahtar/değer çiftleri için hello sırasında kullanılan önbellek Hello miktarını raporlama aralık belirtildi. Bu değeri çok eşler`used_memory` gelen hello Redis bilgileri komutu. Bu, meta veriler veya parçalanma içermez. |
| Kullanılan bellek RSS |Merhaba önbellek parçalanma ve meta verileri de dahil olmak üzere hello belirtilen Raporlama zaman aralığı boyunca, MB olarak kullanılan bellek miktarı. Bu değeri çok eşler`used_memory_rss` gelen hello Redis bilgileri komutu. |
| CPU |Merhaba CPU kullanımını hello Azure Redis önbelleği sunucu yüzdesi hello sırasında raporlama aralık belirtildi. Bu değer toohello işletim sistemi eşlemeleri `\Processor(_Total)\% Processor Time` performans sayacı. |
| Önbellek Okuma |Merhaba önbelleğinden hello megabayt (MB/sn) hello sırasında saniye başına okunan veri miktarını raporlama aralık belirtildi. Bu değer hello önbellek barındıran ve belirli Redis değil hello sanal makine destekleyen hello ağ arabirim kartları türetilir. **Bu değer bu önbelleği tarafından kullanılan toohello ağ bant genişliği karşılık gelir. Sunucu tarafı ağ bant genişliği sınırlarını uyarıları tooset istiyorsanız, bunu kullanarak oluşturun `Cache Read` sayacı. Bkz: [Bu tablo](cache-faq.md#cache-performance) çeşitli önbellek fiyatlandırma katmanlarına ve boyutları için bant genişliği sınırlarını gözlenen hello için.** |
| Önbellek yazma |toohello önbellek (MB/sn) hello belirtilen raporlama aralığı sırasında saniye başına megabayt cinsinden yazılan veri miktarını hello. Bu değer hello önbellek barındıran ve belirli Redis değil hello sanal makine destekleyen hello ağ arabirim kartları türetilir. Bu değer toohello ağ bant genişliği toohello önbellek hello istemciden gönderilen verileri karşılık gelir. |

<a name="operations-and-alerts"></a>
## <a name="alerts"></a>Uyarılar
Ölçümleri ve etkinlik açtığında temelinde tooreceive uyarılar yapılandırabilirsiniz. Azure İzleyici tetikler olduğunda bir uyarı toodo hello aşağıdaki tooconfigure sağlar:

* Bir e-posta bildirimi gönder
* bir Web kancası çağırın
* Bir Azure mantıksal uygulamayı çağırmak

Önbellek hesabınız için uyarı kuralları tooconfigure tıklatın **uyarı kuralları** hello gelen **kaynak menü**.

![İzleme](./media/cache-how-to-monitor/redis-cache-monitoring.png)

Yapılandırma ve Uyarıları kullanma hakkında daha fazla bilgi için bkz: [genel bakış, uyarıları](../monitoring-and-diagnostics/insights-alerts-portal.md).

## <a name="activity-logs"></a>Etkinlik Günlükleri
Etkinlik günlükleri, Azure Redis önbelleği örnekleri üzerinde gerçekleştirilen hello işlemlerinin bir anlayış sağlar. Daha önce "denetim günlüklerini" veya "işletimsel logs" olarak bilinirdi. Etkinlik Günlükleri'ni kullanarak hello belirleyebilirsiniz "ne, kimin, ne zaman ve" herhangi bir Azure Redis önbelleği örnekleri üzerinde gerçekleştirilen işlemleri (PUT, POST, silme) yazmak için. 

> [!NOTE]
> Etkinlik günlükleri okuma (GET) işlemleri dahil etmeyin.
>
>

Önbellek hesabınız için tooview etkinlik günlükleri'ni tıklatın **etkinlik günlükleri** hello gelen **kaynak menü**.

Etkinlik günlükleri hakkında daha fazla bilgi için bkz: [hello Azure etkinlik günlüğü'ne genel bakış](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).











