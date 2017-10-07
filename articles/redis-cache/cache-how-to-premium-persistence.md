---
title: "Premium Azure Redis önbelleği için aaaHow tooconfigure veri kalıcılığını"
description: "Bilgi nasıl tooconfigure ve Premium katmanı Azure Redis önbelleği örnekleri veri kalıcılığını yönetme"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: b01cf279-60a0-4711-8c5f-af22d9540d38
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: sdanie
ms.openlocfilehash: 62feb6f5522e0270487f045eb303bf852434143d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-persistence-for-a-premium-azure-redis-cache"></a>Nasıl tooconfigure veri kalıcılığını Premium Azure Redis önbelleği
Azure Redis önbelleği önbellek boyutu ve özelliklerin Premium katmanı özellikleri kümeleme, sürdürme ve sanal ağ desteği gibi hello seçimi esneklik sağlayan farklı önbellek teklifleri vardır. Nasıl tooconfigure kalıcılığı bir premium, Azure Redis önbelleği bu makalede örneği.

Diğer premium önbellek özellikleri hakkında daha fazla bilgi için bkz: [giriş toohello Azure Redis önbelleği Premium katmanına](cache-premium-tier-intro.md).

## <a name="what-is-data-persistence"></a>Veri kalıcılığını nedir?
[Redis kalıcılığı](https://redis.io/topics/persistence) Redis içinde depolanan toopersist verileri sağlar. Ayrıca, anlık görüntülerini almak ve bir donanım hatası durumunda yükleyebilir hello verileri yedekleyin. Bu temel üzerinde büyük bir avantaj veya burada tüm veri hello standart katmanı bellekte depolanır ve ön bellek düğümleri aşağı nerede arıza durumunda olası veri kaybı olabilir. 

Azure Redis önbelleği Redis kalıcılığı modelleri aşağıdaki hello kullanarak sunar:

* **RDB kalıcılığı** -zaman RDB (Redis veritabanı) Kalıcılık yapılandırılır, Azure Redis önbelleği devam ediyorsa, bir anlık görüntüsünü hello Redis Önbelleği'nde ikili biçimi toodisk yapılandırılabilir bir yedekleme sıklığı dayalı bir Redis. Merhaba birincil ve çoğaltma önbelleği devre dışı bırakan geri dönülemez bir olay meydana gelirse, hello önbellek hello en son anlık görüntü kullanılarak düzenlenir. Merhaba hakkında daha fazla bilgi [avantajları](https://redis.io/topics/persistence#rdb-advantages) ve [dezavantajları](https://redis.io/topics/persistence#rdb-disadvantages) RDB Kalıcılık biri.
* **AOF kalıcılığı** -zaman AOF (yalnızca dosya ekleme) Kalıcılık yapılandırılır, Azure Redis önbelleği en az bir kez bir Azure depolama hesabıyla saniyede kaydedilen her yazma işlemi tooa günlüğüne kaydeder. Merhaba birincil ve çoğaltma önbelleği devre dışı bırakan geri dönülemez bir olay meydana gelirse, hello önbellek depolanan hello yazma işlemleri kullanarak yeniden düzenlenir. Merhaba hakkında daha fazla bilgi [avantajları](https://redis.io/topics/persistence#aof-advantages) ve [dezavantajları](https://redis.io/topics/persistence#aof-disadvantages) AOF Kalıcılık biri.

Kalıcılık hello yapılandırılmış **yeni Redis önbelleği** dikey önbellek oluşturma sırasında ve hello **kaynak menü** için varolan premium önbelleğe alır.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Premium fiyatlandırma katmanına seçildikten sonra tıklatın **Redis kalıcılığı**.

![Redis kalıcılığı][redis-cache-persistence]

Merhaba hello sonraki bölümdeki adımları açıklayan nasıl tooconfigure Redis kalıcılığı yeni premium önbelleğiniz üzerinde. Redis kalıcılığı yapılandırıldıktan sonra tıklatın **oluşturma** yeni premium ile Redis kalıcılığı önbellek toocreate.

## <a name="enable-redis-persistence"></a>Redis kalıcılığı etkinleştir

Redis kalıcılığı hello üzerinde etkin **Redis veri kalıcılığını** ya da seçerek dikey **RDB** veya **AOF** Kalıcılık. Yeni önbellekler için bu dikey penceresinde hello önceki bölümde açıklandığı gibi hello önbelleği oluşturma işlemi sırasında erişilir. Varolan önbellekler için hello **Redis veri kalıcılığını** dikey penceresinde hello erişilen **kaynak menü** önbelleğiniz için.

![Ayarları redis][redis-cache-settings]


## <a name="configure-rdb-persistence"></a>RDB kalıcılığı yapılandırma

tooenable RDB Kalıcılık tıklatın **RDB**. daha önce etkinleştirilmiş premium önbellekteki toodisable RDB Kalıcılık tıklatın **devre dışı**.

![Redis RDB kalıcılığı][redis-cache-rdb-persistence]

tooconfigure hello yedekleme aralığını, select bir **yedekleme sıklığı** hello aşağı açılan listeden. Seçenekleri **15 dakika**, **30 dakika**, **60 dakika**, **6 saat**, **12 saat**ve **24 saat**. Bu aralık hello önceki yedekleme işlemi başarıyla tamamlandıktan sonra sona erdiğinde yeni bir yedekleme başlatılır sayım başlatır.

Tıklatın **depolama hesabı** tooselect depolama hesabı toouse hello ve her iki hello seçin **birincil anahtar** veya **ikincil anahtar** toouse hello gelen **depolama Anahtar** açılır. Hello bir depolama hesabı seçmeniz gerekir hello önbellek, aynı bölgede ve **Premium depolama** hesabı, premium depolama daha yüksek verimlilik olduğundan önerilir. 

> [!IMPORTANT]
> Merhaba depolama anahtarı Kalıcılık hesabınız için yeniden oluşturulursa hello hello istediğiniz anahtarı yeniden yapılandırmanız gerekir **depolama anahtarı** açılır.
> 
> 

Tıklatın **Tamam** toosave hello kalıcılığı yapılandırma.

Merhaba yedekleme sıklığı aralığı geçtikten sonra hello sonraki yedekleme (veya ilk yedek yeni önbellekler için) başlatılır.

## <a name="configure-aof-persistence"></a>AOF kalıcılığı yapılandırma

tooenable AOF Kalıcılık tıklatın **AOF**. daha önce etkinleştirilmiş premium önbellekteki toodisable AOF Kalıcılık tıklatın **devre dışı**.

![Redis AOF kalıcılığı][redis-cache-aof-persistence]

tooconfigure AOF kalıcılığı belirtin bir **ilk depolama hesabı**. Bu depolama hesabını hello olmalıdır hello önbellek, aynı bölgede ve **Premium depolama** hesabı, premium depolama daha yüksek verimlilik olduğundan önerilir. Adlı bir ek depolama alanı hesabı isteğe bağlı olarak yapılandırabilirsiniz **ikinci depolama hesabı**. İkinci bir depolama hesabı yapılandırdıysanız, hello yazma toohello çoğaltma önbelleği yazılır toothis ikinci depolama hesabı. Her yapılandırılan depolama hesabı için her iki hello seçin **birincil anahtar** veya **ikincil anahtar** hello gelen toouse **depolama anahtarı** açılır. 

> [!IMPORTANT]
> Merhaba depolama anahtarı Kalıcılık hesabınız için yeniden oluşturulursa hello hello istediğiniz anahtarı yeniden yapılandırmanız gerekir **depolama anahtarı** açılır.
> 
> 

AOF Kalıcılık etkinleştirildiğinde, işlemleri toohello önbelleği, depolama hesabı (veya ikinci bir depolama hesabı yapılandırdıysanız hesapları) tasarlanmış toohello kaydedilir yazma. Yıkıcı bir hatadan Hello olayında hem aşağı alır birincil hello ve çoğaltma önbelleği hello saklı AOF günlüktür toorebuild hello önbellek kullanılır.

## <a name="persistence-faq"></a>Kalıcılık SSS
Merhaba aşağıdaki listede Azure Redis önbelleği Kalıcılık hakkında sorular yanıtlar toocommonly içerir.

* [Önceden oluşturulmuş önbellekteki Kalıcılık etkinleştirebilirim?](#can-i-enable-persistence-on-a-previously-created-cache)
* [Merhaba adresindeki AOF ve RDB Kalıcılık etkinleştirebilmeniz için aynı anda?](#can-i-enable-aof-and-rdb-persistence-at-the-same-time)
* [Hangi Kalıcılık modeli seçmem gerekir?](#which-persistence-model-should-i-choose)
* [Tooa farklı boyutu ölçeği ve bir yedekleme işlemi ölçeklendirme hello önce yaptığınız geri ne olur?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)


### <a name="rdb-persistence"></a>RDB kalıcılığı
* [Merhaba RDB yedekleme sıklığı, hello önbellek oluşturduktan sonra değiştirebilir miyim?](#can-i-change-the-rdb-backup-frequency-after-i-create-the-cache)
* [Neden 60 dakikada bir RDB yedekleme sıklığını varsa var 60 dakikadan uzun yedeklemeler arasında?](#why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups)
* [Yeni bir yedekleme yapılan toohello eski RDB yedeklemelerin ne olur?](#what-happens-to-the-old-rdb-backups-when-a-new-backup-is-made)

### <a name="aof-persistence"></a>AOF kalıcılığı
* [İkinci bir depolama hesabı ne zaman kullanmalıyım?](#when-should-i-use-a-second-storage-account)
* [AOF Kalıcılık etkileyen boyunca, gecikme veya my önbelleğinin performansını mu?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)
* [Merhaba ikinci depolama hesabı nasıl kaldırabilir miyim?](#how-can-i-remove-the-second-storage-account)
* [Bir yeniden yazma nedir ve my önbellek nasıl etkiler?](#what-is-a-rewrite-and-how-does-it-affect-my-cache)
* [Ne ı etkin AOF bir önbellek ölçeklendirme beklemeniz gerekir?](#what-should-i-expect-when-scaling-a-cache-with-aof-enabled)
* [AOF verilerimi depolama nasıl düzenlenir?](#how-is-my-aof-data-organized-in-storage)


### <a name="can-i-enable-persistence-on-a-previously-created-cache"></a>Önceden oluşturulmuş önbellekteki Kalıcılık etkinleştirebilirim?
Evet, Redis kalıcılığı önbellek oluşturmada ve varolan premium önbelleklere yapılandırılabilir.

### <a name="can-i-enable-aof-and-rdb-persistence-at-hello-same-time"></a>Merhaba adresindeki AOF ve RDB Kalıcılık etkinleştirebilmeniz için aynı anda?

Hayır, yalnızca RDB veya AOF, ancak ikisini hello adresindeki etkinleştirebilirsiniz aynı anda.

### <a name="which-persistence-model-should-i-choose"></a>Hangi Kalıcılık modeli seçmem gerekir?

Üzerinde üretilen işi bazı etkisi her yazma tooa günlük AOF Kalıcılık kaydeder, RDB ile karşılaştırıldığında üzerinde hello bağlı olarak yedeklemeler kaydedileceği Kalıcılık yedekleme aralığını performansı üzerinde en az etkiyle yapılandırılmış. Birincil amacınız toominimize veri kaybı ve önbelleğiniz için işleme düşüş işleyebilir AOF Kalıcılık belirleyin. RDB Kalıcılık önbelleğiniz üzerinde toomaintain en iyi verimlilik istiyor ancak hala veri kurtarma için bir mekanizma istiyorsanız seçin.

* Merhaba hakkında daha fazla bilgi [avantajları](https://redis.io/topics/persistence#rdb-advantages) ve [dezavantajları](https://redis.io/topics/persistence#rdb-disadvantages) RDB Kalıcılık biri.
* Merhaba hakkında daha fazla bilgi [avantajları](https://redis.io/topics/persistence#aof-advantages) ve [dezavantajları](https://redis.io/topics/persistence#aof-disadvantages) AOF Kalıcılık biri.

AOF Kalıcılık kullanırken performans hakkında daha fazla bilgi için bkz: [mu AOF Kalıcılık etkileyen boyunca, gecikme veya my önbelleğinin performansını?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)

### <a name="what-happens-if-i-have-scaled-tooa-different-size-and-a-backup-is-restored-that-was-made-before-hello-scaling-operation"></a>Tooa farklı boyutu ölçeği ve bir yedekleme işlemi ölçeklendirme hello önce yaptığınız geri ne olur?

RDB ve AOF kalıcılığını:

* Tooa daha büyük boyutu ölçeği, üzerinde etkisi yoktur.
* Tooa daha küçük boyutu ölçeği ve özel bir sahip [veritabanları](cache-configure.md#databases) ayarı hello büyük [veritabanları sınırı](cache-configure.md#databases) yeni boyutunuz için bu veritabanlarını verileri geri değil. Daha fazla bilgi için bkz: [olan ölçeklendirme sırasında etkilenen ayarı my özel veritabanlarını?](cache-how-to-scale.md#is-my-custom-databases-setting-affected-during-scaling)
* Tooa daha küçük boyutu ölçeği ve hello hello son yedekleme, anahtarlardan hello verilerin tümü çıkarılacak hello geri yükleme işlemi sırasında daha küçük boyutu toohold içinde yeterli alan yok, genellikle hello kullanarak [allkeys lru](http://redis.io/topics/lru-cache) çıkarma ilke.

### <a name="can-i-change-hello-rdb-backup-frequency-after-i-create-hello-cache"></a>Merhaba RDB yedekleme sıklığı, hello önbellek oluşturduktan sonra değiştirebilir miyim?
Evet, hello yedekleme sıklığı hello üzerinde RDB kalıcılığı için değiştirebileceğiniz **Redis veri kalıcılığını** dikey. Yönergeler için bkz: [yapılandırma Redis kalıcılığı](#configure-redis-persistence).

### <a name="why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups"></a>Neden 60 dakikada bir RDB yedekleme sıklığını varsa var 60 dakikadan uzun yedeklemeler arasında?
Merhaba RDB Kalıcılık yedekleme sıklığı aralığını Hello önceki yedekleme işlemi başarıyla tamamlanana kadar başlatılmaz. Merhaba sonra 75 dakika hello önceki yedekleme çalıştırmadıkça hello yedekleme sıklığı 60 dakikadır ve tam bir yedekleme işlemi 15 dakika toosuccessfully alır, hello sonraki yedekleme başlatılamıyor.

### <a name="what-happens-toohello-old-rdb-backups-when-a-new-backup-is-made"></a>Yeni bir yedekleme yapılan toohello eski RDB yedeklemelerin ne olur?
Merhaba en son biri hariç tüm RDB Kalıcılık yedeklemeleri otomatik olarak silinir. Bu silme işleminin hemen olmayabilir ancak eski yedeklemeler süresiz olarak kalıcı değildir.


### <a name="when-should-i-use-a-second-storage-account"></a>İkinci bir depolama hesabı ne zaman kullanmalıyım?

Merhaba önbellekteki beklenen ayarlama işlemleri daha yüksek olan düşünüyorsanız olduğunda AOF kalıcılığını ikinci bir depolama hesabı kullanmanız gerekir.  Merhaba ikincil depolama hesabı ayarlama önbelleğiniz depolama bant genişliği sınırlarına ulaşma değil sağlamaya yardımcı olur.

### <a name="does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache"></a>AOF Kalıcılık etkileyen boyunca, gecikme veya my önbelleğinin performansını mu?

AOF Kalıcılık hello önbellek en yüksek yük altında olduğunda bu verimliliği yaklaşık % 15-20 oranında etkiler (CPU ve sunucu yükü hem % 90'altında). Olmamalıdır gecikmesi sorunları hello önbellek bu sınırlar içinde olduğunda. Ancak, hello önbellek bu sınırlamaları daha erken etkin AOF ile tamamlayacaktır.

### <a name="how-can-i-remove-hello-second-storage-account"></a>Merhaba ikinci depolama hesabı nasıl kaldırabilir miyim?

Merhaba toobe hello aynı hello ilk depolama hesabı olarak ikinci depolama hesabı ayarlayarak hello AOF Kalıcılık ikincil depolama hesabı kaldırabilirsiniz. Yönergeler için bkz: [yapılandırma AOF kalıcılığı](#configure-aof-persistence).

### <a name="what-is-a-rewrite-and-how-does-it-affect-my-cache"></a>Bir yeniden yazma nedir ve my önbellek nasıl etkiler?

Merhaba AOF dosya yeterince büyük hale geldiğinde yeniden hello önbelleği sıraya alındı otomatik olarak. Merhaba yeniden yazma işlemlerini en az sayıda hello hello AOF dosyasıyla toocreate geçerli veri kümesi hello yeniden boyutlandırır. Yeniden yazdırmaya sırasında tooreach performans sınırlarını er özellikle büyük veri kümeleriyle ilgilenirken bekler. Genellikle hello AOF dosya büyük hale gelir, ancak önemli miktarda zaman zaman gerçekleşeceğini olacak şekilde yeniden yazdırmaya daha az oluşur.

### <a name="what-should-i-expect-when-scaling-a-cache-with-aof-enabled"></a>Ne ı etkin AOF bir önbellek ölçeklendirme beklemeniz gerekir?

Merhaba AOF dosya hello sırasındaki ölçeklendirme önemli ölçüde büyükse hello ölçek işlemi tootake ölçeklendirme tamamlandıktan sonra onu hello dosya yeniden beri beklenenden daha uzun bekler.

Ölçeklendirme ile ilgili daha fazla bilgi için bkz: [tooa farklı boyutu ölçeği ve bir yedekleme işlemi ölçeklendirme hello önce yaptığınız geri ne olur?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)

### <a name="how-is-my-aof-data-organized-in-storage"></a>AOF verilerimi depolama nasıl düzenlenir?

AOF dosyalarında depolanan verileri hello veri toostorage kaydetme düğüm tooincrease performansı başına birden çok sayfa bloblarını ayrılmıştır. Merhaba aşağıdaki tabloda her fiyatlandırma katmanının için kaç tane sayfa bloblarını kullanılan görüntüler:

| Premium katman | Bloblar |
|--------------|-------|
| P1           | parça başına 4    |
| P2           | parça başına 8    |
| P3           | parça başına 16   |
| P4           | parça başına 20   |

Kümeleme etkinleştirildiğinde, her parça hello önbelleğinde hello önceki tabloda belirtildiği gibi sayfa BLOB'ları, kendi kümesi vardır. Örneğin, üç parça P2 önbellekle AOF dosya 24 sayfa blobları (8 BLOB'lar ile 3 parça parça başına) dağıtır.

Bir yeniden yazma sonra depoda AOF dosyaları iki kümesi yok. Yeniden yazdırmaya hello arka planda oluşur ve toohello ikinci kümesi ekleme toohello önbellek hello yeniden yazma sırasında gönderilen ayarlama işlemleri sırasında toohello ilk dosyaları kümesini ekleyin. Bir yedekleme hatası durumunda yeniden yazdırmaya sırasında geçici olarak depolanır, ancak bir yeniden yazma tamamlandıktan sonra hemen silinir.


## <a name="next-steps"></a>Sonraki adımlar
Toouse daha premium özellikleri nasıl önbelleğe alma hakkında bilgi edinin.

* [Giriş toohello Azure Redis önbelleği Premium katmanına](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-premium-pricing-tier]: ./media/cache-how-to-premium-persistence/redis-cache-premium-pricing-tier.png

[redis-cache-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-persistence.png

[redis-cache-rdb-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-rdb-persistence.png

[redis-cache-aof-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-aof-persistence.png

[redis-cache-settings]: ./media/cache-how-to-premium-persistence/redis-cache-settings.png
