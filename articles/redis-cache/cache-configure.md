---
title: "Azure Redis önbelleği aaaHow tooconfigure | Microsoft Docs"
description: "Azure Redis önbelleği için Hello varsayılan Redis yapılandırma anlamak ve nasıl tooconfigure Azure Redis öğrenin önbellek örneklerinde"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/22/2017
ms.author: sdanie
ms.openlocfilehash: 46bffb74cdf40e0e0a99c3a83dbe06d6fe1ea65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-azure-redis-cache"></a>Nasıl tooconfigure Azure Redis önbelleği
Bu konuda, Azure Redis önbelleği örnekleri için yapılandırma ve Azure Redis önbelleği örnekleri için kapsar hello varsayılan Redis sunucu yapılandırması nasıl tooreview ve güncelleştirme hello açıklanmaktadır.

> [!NOTE]
> Yapılandırma ve premium önbellek özellikleri kullanma hakkında daha fazla bilgi için bkz: [nasıl tooconfigure kalıcılığı](cache-how-to-premium-persistence.md), [nasıl kümeleme tooconfigure](cache-how-to-premium-clustering.md), ve [tooconfigure sanal ağ'ı nasıl destekler ](cache-how-to-premium-vnet.md).
> 
> 

## <a name="configure-redis-cache-settings"></a>Redis önbelleği ayarları
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

Azure Redis önbelleği ayarları görüntülenebilir ve hello üzerinde yapılandırılmış **Redis önbelleği** hello kullanarak dikey **kaynak menü**.

![Redis önbelleği ayarları](./media/cache-configure/redis-cache-settings.png)

Görüntüleyebilir ve ayarlarını hello kullanarak aşağıdaki hello yapılandırabilirsiniz **kaynak menü**.

* [Genel Bakış](#overview)
* [Etkinlik Günlüğü](#activity-log)
* [Erişim denetimi (IAM)](#access-control-iam)
* [Etiketler](#tags)
* [Sorunları tanılama ve çözme](#diagnose-and-solve-problems)
* [Ayarlar](#settings)
    * [Erişim tuşları](#access-keys)
    * [Gelişmiş ayarlar](#advanced-settings)
    * [Redis önbelleği Danışmanı](#redis-cache-advisor)
    * [Ölçeklendirme](#scale)
    * [Küme boyutu redis](#cluster-size)
    * [Redis veri kalıcılığını](#redis-data-persistence)
    * [Güncelleştirmeleri zamanlama](#schedule-updates)
    * [Coğrafi çoğaltma](#geo-replication)
    * [Sanal Ağ](#virtual-network)
    * [Güvenlik duvarı](#firewall)
    * [Özellikleri](#properties)
    * [Kilitler](#locks)
    * [Otomasyon komut dosyası](#automation-script)
* [Yönetim](#administration)
    * [Veri alma](#importexport)
    * [Verileri dışarı aktarma](#importexport)
    * [Yeniden başlatma](#reboot)
* [İzleme](#monitoring)
    * [Ölçümleri redis](#redis-metrics)
    * [Uyarı kuralları](#alert-rules)
    * [Tanılama](#diagnostics)
* [Destek ve sorun giderme ayarları](#support-amp-troubleshooting-settings)
    * [Kaynak durumu](#resource-health)
    * [Yeni destek isteği](#new-support-request)


## <a name="overview"></a>Genel Bakış

**Genel Bakış** , fiyatlandırma katmanı ve seçilen önbellek ölçümleri adı gibi önbelleğiniz hakkında temel bilgileri sizinle bağlantı noktaları sağlar.

### <a name="activity-log"></a>Etkinlik günlüğü

Tıklatın **etkinlik günlüğü** tooview eylemleri önbelleğiniz üzerinde. Bu görünüm tooinclude filtreleme tooexpand de kullanabilirsiniz diğer kaynakları. Denetim günlükleri ile çalışma hakkında daha fazla bilgi için bkz: [denetim işlemleri Resource Manager ile](../azure-resource-manager/resource-group-audit.md). Azure Redis önbelleği olaylar izleme hakkında daha fazla bilgi için bkz: [işlemleri ve Uyarıları](cache-how-to-monitor.md#operations-and-alerts).

### <a name="access-control-iam"></a>Erişim denetimi (IAM)

Merhaba **erişim denetimi (IAM)** bölüm desteği sağlar. rol tabanlı erişim denetimi (RBAC) hello Azure portal toohelp kuruluşlar karşılamak erişim yönetimi gereksinimlerine sadece ve tam olarak. Daha fazla bilgi için bkz: [hello Azure portalında rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).

### <a name="tags"></a>Etiketler

Merhaba **etiketleri** bölüm kaynaklarınızı düzenlemenize yardımcı olur. Daha fazla bilgi için bkz: [kullanarak Azure kaynaklarınızı tooorganize etiketler](../azure-resource-manager/resource-group-using-tags.md).


### <a name="diagnose-and-solve-problems"></a>Sorunları tanılama ve çözme

Tıklatın **Tanıla ve sorunları** ortak sorunlar ve stratejileri çözümlemek için sağlanan toobe.



## <a name="settings"></a>Ayarlar
Merhaba **ayarları** bölüm tooaccess sağlar ve önbelleğiniz için ayarları aşağıdaki hello yapılandırın.

* [Erişim tuşları](#access-keys)
* [Gelişmiş ayarlar](#advanced-settings)
* [Redis önbelleği Danışmanı](#redis-cache-advisor)
* [Ölçeklendirme](#scale)
* [Küme boyutu redis](#cluster-size)
* [Redis veri kalıcılığını](#redis-data-persistence)
* [Güncelleştirmeleri zamanlama](#schedule-updates)
* [Coğrafi çoğaltma](#geo-replication)
* [Sanal Ağ](#virtual-network)
* [Güvenlik duvarı](#firewall)
* [Özellikleri](#properties)
* [Kilitler](#locks)
* [Otomasyon komut dosyası](#automation-script)



### <a name="access-keys"></a>Erişim tuşları
Tıklatın **erişim anahtarları** tooview veya yeniden hello erişim tuşları önbelleğiniz için. Bu anahtarlar tooyour önbellek bağlanan hello istemcileri tarafından kullanılır.

![Redis önbelleği erişim tuşları](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a>Gelişmiş ayarlar
Merhaba aşağıdaki ayarları hello üzerinde yapılandırılmış **Gelişmiş ayarları** dikey.

* [Erişim bağlantı noktaları](#access-ports)
* [Bellek ilkeleri](#memory-policies)
* [Keyspace bildirimleri (Gelişmiş ayarları)](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a>Erişim bağlantı noktaları
SSL olmayan erişim yeni önbellekler için varsayılan olarak devre dışı bırakılmıştır. tooenable hello SSL olmayan bağlantı noktası, tıklatın **Hayır** için **yalnızca SSL aracılığıyla erişime izin ver** hello üzerinde **Gelişmiş ayarları** dikey ve ardından **kaydetmek**.

![Redis önbelleği erişim bağlantı noktaları](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a>Bellek ilkeleri
Merhaba **Maxmemory İlkesi**, **maxmemory ayrılmış**, ve **maxfragmentationmemory ayrılmış** hello ayarlarını **Gelişmiş ayarları**dikey penceresinde hello bellek ilkeleri hello önbelleği için yapılandırın.

![Redis önbelleği Maxmemory İlkesi](./media/cache-configure/redis-cache-maxmemory-policy.png)

**Maxmemory İlkesi** hello çıkarma İlkesi hello önbelleği için yapılandırır ve çıkarma ilkelere hello gelen toochoose sağlar:

* `volatile-lru`-Bu hello varsayılandır.
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

Hakkında daha fazla bilgi için `maxmemory` ilkeleri Bkz [çıkarma ilkeleri](http://redis.io/topics/lru-cache#eviction-policies).

Merhaba **maxmemory ayrılmış** ayarı, MB olarak çoğaltma yük devretme sırasında gibi önbellek olmayan işlemleri için ayrılmış bellek miktarı hello yapılandırır. Bu değer ayarlandığında yük değişiklik gösterdiğinde toohave daha tutarlı bir Redis sunucu deneyim da sağlar. Bu değer ağır yazma iş yükleri için yüksek ayarlamanız gerekir. Bu tür işlemler için ayrılmış bellek, önbelleğe alınan veri depolama için kullanılabilir değil.

Merhaba **maxfragmentationmemory ayrılmış** ayarı, MB olarak bellek parçalanması için ayrılmış tooaccommodate olan hello bellek miktarını yapılandırır. Bu değer ayarlandığında toohave daha tutarlı bir Redis sunucu deneyim hello önbellek dolu veya kapat toofull ve hello parçalanma oranı de yüksek olduğunda izin verir. Bu tür işlemler için ayrılmış bellek, önbelleğe alınan veri depolama için kullanılabilir değil.

Yeni bir bellek ayırma değeri seçerken tek şey tooconsider (**maxmemory ayrılmış** veya **maxfragmentationmemory ayrılmış**) ile çalışan bir önbellek bu değişiklik nasıl etkileyebileceğini olduğu büyük miktarlarda veri da. 49 GB veri 53 GB'a önbellekle sahip ardından hello ayırma değeri too8 GB değiştirin, örneğin, bu too45 GB aşağı hello sistemi için en fazla kullanılabilir bellek hello bırakılmasına neden olacak. Her iki geçerli `used_memory` veya `used_memory_rss` değerlerdir hello yeni 45 GB sınırından daha sonra hello sistem tooevict veri sahip olacak kadar her ikisi de `used_memory` ve `used_memory_rss` 45 GB olan. Çıkarma sunucu yükü ve bellek parçalanması artırabilir. Önbellek ölçümleri gibi hakkında daha fazla bilgi için `used_memory` ve `used_memory_rss`, bkz: [kullanılabilir Ölçümler ve aralıklarını raporlama](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).

> [!IMPORTANT]
> Merhaba **maxmemory ayrılmış** ve **maxfragmentationmemory ayrılmış** ayarlarını bulunan ve yalnızca için standart ve Premium önbelleğe alır.
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a>Keyspace bildirimleri (Gelişmiş ayarları)
Keyspace bildirimleri hello üzerinde yapılandırılmış olan redis **Gelişmiş ayarları** dikey. Belirli olaylar oluştuğunda Keyspace bildirimleri istemcileri tooreceive bildirimlerine izin verin.

![Redis önbelleği Gelişmiş ayarlar](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> Keyspace bildirimleri ve hello **bildir-keyspace-olayları** ayarı bulunan ve yalnızca standart ve Premium önbellekler için.
> 
> 

Daha fazla bilgi için bkz: [Redis Keyspace bildirimleri](http://redis.io/topics/notifications). Örnek kod için bkz: Merhaba [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) hello dosyasında [Merhaba Dünya](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) örnek.


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a>Redis önbelleği Danışmanı
Merhaba **Redis önbelleği Danışmanı** dikey önbelleğiniz için öneriler görüntüler. Normal işlemler sırasında öneri yok görüntülenir. 

![Öneriler](./media/cache-configure/redis-cache-no-recommendations.png)

Önbelleğinizin yüksek bellek kullanımı, ağ bant genişliği veya sunucu iş yükü gibi hello işlemleri sırasında tüm koşullar meydana gelirse, bir uyarı hello üzerinde görüntülenir **Redis önbelleği** dikey.

![Öneriler](./media/cache-configure/redis-cache-recommendations-alert.png)

Merhaba hakkında daha fazla bilgi bulunabilir **önerileri** dikey.

![Öneriler](./media/cache-configure/redis-cache-recommendations.png)

Bu ölçümleri hello izleyebilirsiniz [izleme grafikleri](cache-how-to-monitor.md#monitoring-charts) ve [kullanım grafiklerini](cache-how-to-monitor.md#usage-charts) hello bölümlerini **Redis önbelleği** dikey.

Her fiyatlandırma katmanının istemci bağlantıları, bellek ve bant genişliği için farklı sınırları vardır. Bir öneri, önbelleğiniz aralıksız bir süre boyunca Bu ölçümler için maksimum kapasite yaklaşıyor değilse oluşturulur. Merhaba ölçümleri ve hello tarafından gözden sınırları hakkında daha fazla bilgi için **önerileri** aracı, aşağıdaki tablonun hello bakın:

| Redis önbelleği ölçüm | Daha fazla bilgi |
| --- | --- |
| Ağ bant genişliği kullanımı |[Önbellek performansı - kullanılabilir bant genişliği](cache-faq.md#cache-performance) |
| Bağlanan istemciler |[Redis sunucu yapılandırması - maxclients varsayılan](#maxclients) |
| Sunucu iş yükü |[Kullanım grafikler - Redis sunucu iş yükü](cache-how-to-monitor.md#usage-charts) |
| Bellek kullanımı |[Önbellek performansı - boyutu](cache-faq.md#cache-performance) |

tooupgrade, önbellek tıklatın **Şimdi Yükselt** toochange hello fiyatlandırma katmanı ve [ölçek](#scale) önbelleğiniz. Bir fiyatlandırma katmanı seçme hakkında daha fazla bilgi için bkz: [hangi Redis önbelleği teklifini ve boyutunu kullanmalıyım?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)


### <a name="scale"></a>Ölçek
Tıklatın **ölçek** fiyatlandırma katmanı önbelleğiniz için tooview ya da değişiklik hello. Ölçeklendirme ile ilgili daha fazla bilgi için bkz: [nasıl tooScale Azure Redis önbelleği](cache-how-to-scale.md).

![Redis önbelleği fiyatlandırma katmanı](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a>Küme boyutu redis
Tıklatın **(Önizleme) Redis küme boyutu** önbellek toochange hello küme boyutu çalışan premium için kümeleme özelliği etkinleştirilmiş.

> [!NOTE]
> Merhaba katmanı bırakıldı Azure Redis önbelleği Premium sırasında tooGeneral kullanılabilirlik, hello Redis küme boyutu özelliği yayımlanan şu anda önizlemede olduğunu unutmayın.
> 
> 

![Küme boyutu redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

toochange hello küme boyutu, hello kaydırıcıyı kullanın veya hello 1 ile 10 arasında bir sayı yazın **parça sayısı** metin kutusu ve tıklatın **Tamam** toosave.

> [!IMPORTANT]
> Redis kümeleme yalnızca Premium önbellekler için kullanılabilir. Daha fazla bilgi için bkz: [nasıl bir Premium Azure Redis önbelleği için kümeleri tooconfigure](cache-how-to-premium-clustering.md).
> 
> 


### <a name="redis-data-persistence"></a>Redis veri kalıcılığını
Tıklatın **Redis veri kalıcılığını** tooenable, devre dışı bırakın ya da premium önbelleğiniz veri kalıcılığını yapılandırma. Azure Redis önbelleği Redis kalıcılığı kullanarak sunar [RDB kalıcılığı](cache-how-to-premium-persistence.md#configure-rdb-persistence) veya [AOF kalıcılığı](cache-how-to-premium-persistence.md#configure-aof-persistence).

Daha fazla bilgi için bkz: [nasıl Premium Azure Redis önbelleği için kalıcılığı tooconfigure](cache-how-to-premium-persistence.md).


> [!IMPORTANT]
> Redis veri kalıcılığını yalnızca Premium önbellekler için kullanılabilir. 
> 
> 

### <a name="schedule-updates"></a>Güncelleştirmeleri zamanlama
Merhaba **zamanlama güncelleştirmeleri** dikey toodesignate önbelleğiniz için Redis server güncelleştirmeleri için bir bakım penceresi sağlar. 

> [!IMPORTANT]
> Merhaba bakım penceresi yalnızca tooRedis server güncelleştirmeleri ve değil Azure güncelleştirir veya hello önbelleği barındırmak hello VM'lerin toohello işletim sistemi güncelleştirmelerini tooany geçerlidir.
> 
> 

![Güncelleştirmeleri zamanlama](./media/cache-configure/redis-schedule-updates.png)

toospecify bir bakım penceresi istenen hello gün kontrol edin ve her gün için hello bakım penceresi başlangıç saati belirtin ve tıklatın **Tamam**. Merhaba bakım penceresi saati UTC biçiminde olduğunu unutmayın. 

> [!IMPORTANT]
> Merhaba **zamanlama güncelleştirmeleri** işlevdir yalnızca Premium katmanı önbellekler için kullanılabilir. Daha fazla bilgi ve yönergeler için bkz: [Azure Redis önbelleği yönetim - güncelleştirmeleri zamanla](cache-administration.md#schedule-updates).
> 
> 

### <a name="geo-replication"></a>Coğrafi çoğaltma

Merhaba **coğrafi çoğaltma** dikey iki Premium katmanı Azure Redis önbelleği örnekleri bağlama için bir mekanizma sağlar. Bir önbellek hello birincil bağlantılı önbellek ve hello hello ikincil bağlantılı önbelleği gibi diğer olarak atanır. Merhaba ikincil bağlantılı önbellek salt okunur olur ve yazılı toohello birincil önbelleği veri toohello ikincil bağlantılı önbellek çoğaltılır. Bu işlev Azure bölgeler arasında kullanılan tooreplicate bir önbellek olabilir.

> [!IMPORTANT]
> **Coğrafi çoğaltma** yalnızca Premium katmanı önbellekler için kullanılabilir. Daha fazla bilgi ve yönergeler için bkz: [nasıl Azure Redis önbelleği için coğrafi çoğaltma tooconfigure](cache-how-to-geo-replication.md).
> 
> 

### <a name="virtual-network"></a>Sanal Ağ
Merhaba **sanal ağ** bölümü önbelleğiniz için tooconfigure hello sanal ağ ayarlarını sağlar. VNET ile birlikte premium önbelleği oluşturma hakkında bilgi için destek ve ayarlarını güncelleştirmek, bkz: [tooconfigure sanal ağ desteği nasıl Premium Azure Redis önbelleği için](cache-how-to-premium-vnet.md).

> [!IMPORTANT]
> Sanal ağ ayarları yapılandırıldı premium önbelleklere kullanılabilir yalnızca önbellek oluşturma sırasında VNET desteğiyle. 
> 
> 

### <a name="firewall"></a>Güvenlik duvarı

Tıklatın **Güvenlik Duvarı** tooview, Premium Azure Redis önbelleği için güvenlik duvarı kuralları yapılandırın.

![Güvenlik duvarı](./media/cache-configure/redis-firewall-rules.png)

Güvenlik duvarı kuralları ile bir başlangıç ve bitiş IP adresi aralığı belirtebilirsiniz. Güvenlik duvarı kuralları yapılandırıldığında, IP adres aralıklarını toohello önbellek bağlanabilir yalnızca hello'ten istemci bağlantılarını belirtildi. Bir güvenlik duvarı kuralı kaydedildiğinde vardır kısa bir gecikme hello kural etkilidir önce. Bu gecikme, normal bir dakikadan az olur.

> [!IMPORTANT]
> Güvenlik duvarı kuralları yapılandırılmış olsa bile Azure Redis önbelleği sistemleri izleme bağlantılarından her zaman, izin verilir.
> 
> Güvenlik duvarı kuralları yalnızca Premium katmanı önbellekler için kullanılabilir.
> 
> 

### <a name="properties"></a>Özellikler
Tıklatın **özellikleri** hello önbellek uç noktası ve bağlantı noktaları da dahil olmak üzere önbelleğiniz hakkında tooview bilgi.

![Redis önbelleği özellikleri](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a>Kilitler
Merhaba **kilitler** bölümü sağlar, size, toolock bir abonelik, kaynak grubu veya kaynak tooprevent yanlışlıkla silinmesi ya da kritik kaynaklara değiştirme kuruluşunuzdaki diğer kullanıcılar. Daha fazla bilgi için bkz. [Azure Resource Manager ile kaynakları kilitleme](../azure-resource-manager/resource-group-lock-resources.md).

### <a name="automation-script"></a>Otomasyon komut dosyası

Tıklatın **Otomasyon betiğini** toobuild ve dağıtılmış kaynaklarınızın gelecekteki dağıtımlar için şablonu dışarı aktarma. Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [kaynakları Azure Resource Manager şablonları ile dağıtma](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="administration-settings"></a>Yönetim ayarları
Merhaba hello ayarlarında **Yönetim** bölüm önbelleğiniz için yönetim görevleri aşağıdaki tooperform hello izin. 

![Yönetim](./media/cache-configure/redis-cache-administration.png)

* [Veri alma](#importexport)
* [Verileri dışarı aktarma](#importexport)
* [Yeniden başlatma](#reboot)


### <a name="importexport"></a>İçeri/Dışarı Aktarma
İçeri/dışarı aktarma alma ve Redis önbelleği veritabanı'nı (RDB) anlık bir Azure depolama hesabındaki premium önbellek tooa sayfa blobu dışarı aktarma tarafından hello önbelleğinde tooimport ve dışarı aktarma veri sağlayan bir Azure Redis önbelleği veri yönetimi, bir işlemdir. İçeri/dışarı aktarma farklı Azure Redis önbelleği örnekleri arasında toomigrate etkinleştirir veya hello önbellek kullanmadan önce verilerle doldurma.

İçeri aktarma kullanılan toobring Redis uyumlu RDB dosyalarından herhangi bir bulut veya ortamını Linux, Windows ya da herhangi bir bulut sağlayıcısına Amazon Web Hizmetleri ve diğerleri gibi çalışan Redis çalıştıran herhangi bir Redis sunucu olabilir. Veri alma kolay bir yolu toocreate önceden doldurulmuş haldedir verilerle bir önbellek olur. Merhaba içeri aktarma işlemi sırasında Azure Redis önbelleği hello RDB dosyaları Azure Storage'dan belleğe yükler ve sonra hello anahtarları hello önbelleğine ekler.

Dışarı aktarma Azure Redis önbelleği tooRedis uyumlu RDB dosyalarında depolanan tooexport hello verileri sağlar. Bu özellik toomove verilerden bir Azure Redis önbelleği örneği tooanother veya tooanother Redis sunucusu kullanabilirsiniz. Hello dışa aktarma işlemi sırasında Azure Redis önbelleği sunucu örneği konakları hello ve depolama hesabı belirlenmiş karşıya yüklenen toohello hello dosyadır VM hello üzerinde geçici bir dosya oluşturulur. Merhaba dışa aktarma işlemi ya da durumunu başarı veya hata ile tamamlandığında hello geçici dosya silindi.

> [!IMPORTANT]
> İçeri/dışarı aktarma yalnızca Premium katmanı önbellekler için kullanılabilir. Daha fazla bilgi ve yönergeler için bkz: [içeri ve dışarı aktarma Azure Redis önbelleği verilerde](cache-how-to-import-export-data.md).
> 
> 

### <a name="reboot"></a>Yeniden başlatma
Merhaba **yeniden** dikey tooreboot hello önbelleğiniz düğümlerinin sağlar. Bir önbellek düğümü ise bu yeniden başlatma yeteneği, tootest, uygulamanız için esneklik sağlar.

![Yeniden başlatma](./media/cache-configure/redis-cache-reboot.png)

Kümeleme özelliği etkinleştirilmiş bir premium önbelleği varsa, hangi parça hello önbellek tooreboot birini seçebilirsiniz.

![Yeniden başlatma](./media/cache-configure/redis-cache-reboot-cluster.png)

tooreboot, önbellek, bir veya daha fazla düğümlerinin istenen hello düğümleri tıklatıp **yeniden**. Kümeleme özelliği etkinleştirilmiş bir premium önbelleği varsa hello shard(s) tooreboot seçin ve ardından **yeniden**. Birkaç dakika sonra seçili düğümü yeniden başlatma hello ve birkaç dakika sonra yeniden çevrimiçi.

> [!IMPORTANT]
> Yeniden başlatma için tüm fiyatlandırma katmanlarına kullanıma sunulmuştur. Daha fazla bilgi ve yönergeler için bkz: [Azure Redis önbelleği yönetim - yeniden başlatma](cache-administration.md#reboot).
> 
> 


## <a name="monitoring"></a>İzleme

Merhaba **izleme** bölümü sağlar, size, tooconfigure tanılama ve Redis önbelleği için izleme. Azure Redis önbelleği izleme ve Tanılama hakkında daha fazla bilgi için bkz: [nasıl toomonitor Azure Redis önbelleği](cache-how-to-monitor.md).

![Tanılama](./media/cache-configure/redis-cache-diagnostics.png)

* [Ölçümleri redis](#redis-metrics)
* [Uyarı kuralları](#alert-rules)
* [Tanılama](#diagnostics)

### <a name="redis-metrics"></a>Ölçümleri redis
Tıklatın **Redis ölçümleri** çok[görüntülemek ölçümleri](cache-how-to-monitor.md#view-cache-metrics) önbelleğiniz için.

### <a name="alert-rules"></a>Uyarı kuralları

Tıklatın **uyarı kuralları** tooconfigure uyarıları temel Redis önbelleği ölçümleri. Daha fazla bilgi için bkz: [uyarıları](cache-how-to-monitor.md#alerts).

### <a name="diagnostics"></a>Tanılama

Önbellek ölçümleridir Azure İzleyicisi'nde varsayılan olarak, [30 gün boyunca depolanan](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) ve ardından silinir. 30 günden uzun, önbellek ölçümlerinizi toopersist tıklatın **tanılama** çok[hello depolama hesabı yapılandırma](cache-how-to-monitor.md#export-cache-metrics) toostore önbellek tanılamayı kullanılır.

>[!NOTE]
>Toplama tooarchiving, önbellek ölçümleri toostorage kullanabileceğiniz [tooan olay hub'ı akış veya tooLog Analytics Gönder](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).
>
>

## <a name="support--troubleshooting-settings"></a>Destek ve sorun giderme ayarları
Merhaba hello ayarlarında **destek + sorun giderme** bölüm sağlar, önbellek ile ilgili sorunları çözmek için Seçenekler.

![Destek + sorunlarını giderme](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [Kaynak durumu](#resource-health)
* [Yeni destek isteği](#new-support-request)

### <a name="resource-health"></a>Kaynak durumu
**Kaynak durumu** kaynağınız izler ve beklendiği gibi çalışıp çalışmadığını belirtir. Hello Azure kaynak sistem durumu hizmeti hakkında daha fazla bilgi için bkz: [Azure kaynak sistem durumu genel bakış](../resource-health/resource-health-overview.md).

> [!NOTE]
> Kaynak durumu hello durumu sanal ağında barındırılan Azure Redis önbelleği örnekleri üzerinde şu anda işleyemiyor tooreport ' dir. Daha fazla bilgi için bkz: [tüm önbellek özellikleri VNET önbelleğinde barındırdığında çalışır?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)
> 
> 

### <a name="new-support-request"></a>Yeni destek isteği
Tıklatın **yeni destek isteği** tooopen önbellek hesabınız için bir destek isteği.





## <a name="default-redis-server-configuration"></a>Varsayılan Redis sunucu yapılandırması
Yeni Azure Redis önbelleği örnekleri varsayılan Redis yapılandırma değerlerini aşağıdaki hello ile yapılandırılır.

> [!NOTE]
> Bu bölümdeki Hello ayarları değiştirilemiyor hello kullanarak `StackExchange.Redis.IServer.ConfigSet` yöntemi. Bu yöntem, bu bölümdeki hello komutlar biriyle çağrılırsa, bir özel durum benzer toohello aşağıdaki oluşturulur:  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> Yapılandırılabilir gibi herhangi bir değeri **en fazla bellek İlkesi**, hello Azure portalında veya Azure CLI veya PowerShell gibi komut satırı yönetim araçları aracılığıyla yapılandırılabilir.
> 
> 

| Ayar | Varsayılan değer | Açıklama |
| --- | --- | --- |
| `databases` |16 |Merhaba varsayılan veritabanı sayısı 16'dır, ancak fiyatlandırma katmanı bir farklı sayı göre hello yapılandırabilirsiniz. <sup>1</sup> hello varsayılan veritabanı DB 0, farklı bir bağlantı başına kullanma temel seçebileceğiniz `connection.GetDatabase(dbid)` nerede `dbid` arasında bir sayı `0` ve `databases - 1`. |
| `maxclients` |Fiyatlandırma katmanı hello üzerinde bağlıdır<sup>2</sup> |En fazla bağlı istemciyi aynı hello izin hello budur zaman. Merhaba sınırına ulaşıldığında Redis tüm hello yeni bağlantıları, 'max sayısı sınırına istemcileri' hata dönülür. |
| `maxmemory-policy` |`volatile-lru` |Maxmemory İlkesi Redis hangi tooremove nasıl seçtiği için hello ayarı olduğu zaman `maxmemory` (Merhaba önbellek oluşturduğunuzda seçtiğiniz sunumu hello önbellek boyutunu hello) ulaşıldığında. Azure Redis önbelleği hello varsayılan ayardır `volatile-lru`, LRU algoritması kullanılarak ayarlanan bir sona erme ile Merhaba anahtarlarını kaldırır. Bu ayar hello Azure portal yapılandırılabilir. Daha fazla bilgi için bkz: [bellek ilkeleri](#memory-policies). |
| `maxmemory-samples` |3 |toosave bellek, LRU ve TTL algoritmaları en az hassas algoritmaları yerine yaklaşık algoritmaları şunlardır. Varsayılan olarak, daha az kısa bir süre önce kullanılan denetimleri üç anahtarları ve çekmeleri hello bir Redis. |
| `lua-time-limit` |5,000 |Milisaniye cinsinden Lua komut dosyası yürütme zaman sınırı. Merhaba maksimum yürütme süresi ulaştıysanız, Redis bir komut dosyası izin verilen süresi hala yürütme içinde hello maksimum sonra ve bir hata ile tooreply tooqueries başlatır günlüğe kaydeder. |
| `lua-event-limit` |500 |Komut dosyası olay sırasının en büyük boyutu. |
| `client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub` |0 0 032mb 8mb 60 |Merhaba istemci çıkış arabelleği sınırları olabilir veri hello sunucudan yeterince hızlı (ortak bir nedeni Pub/alt istemci iletileri hello yayımcı oluşturmak üzere kadar hızlı kullanamayacaklarını) herhangi bir nedenden dolayı okuyorsanız olmayan istemciler tooforce bağlantısının kesilmesi kullanılır. Daha fazla bilgi için bkz: [http://redis.io/topics/clients](http://redis.io/topics/clients). |

<a name="databases"></a>
<sup>1</sup>hello sınırı `databases` her Azure Redis fiyatlandırma katmanı önbelleği için farklıdır ve önbellek oluşturma sırasında ayarlanabilir. Öyle değilse `databases` ayarı belirtilen önbellek oluşturma sırasında hello varsayılandır 16.

* Temel ve standart önbellekler
  * C0 - too16 veritabanlarını (250 MB) önbelleği
  * C1 - too16 veritabanlarını (1 GB) önbelleği
  * C2 - too16 veritabanlarını (2,5 GB) önbelleği
  * C3 (6 GB) önbelleği - too16 veritabanları
  * C4 (13 GB) önbelleği - too32 veritabanları
  * C5 (26 GB) önbelleği - too48 veritabanları
  * C6 (53 GB'a) önbelleği - too64 veritabanları
* Premium önbelleklere
  * P1 (6 GB - 60 GB) - too16 veritabanlarını
  * P2 (13 GB - 130 GB) - too32 veritabanlarını
  * P3 (26 GB - 260 GB) - too48 veritabanlarını
  * P4 (53 GB'a - 530 GB) - too64 veritabanlarını
  * Etkin - Redis kümesi ile tüm premium önbelleklere Redis küme veritabanı 0 kullanımını şekilde hello destekler `databases` herhangi premium önbelleği etkin Redis kümesi ile etkili bir şekilde 1 ve hello için sınırlamak [seçin](http://redis.io/commands/select) komutu izin verilmez. Daha fazla bilgi için bkz: [toomake kümeleme tüm değişiklikleri toomy istemci uygulaması toouse ihtiyacım var?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)

Veritabanları hakkında daha fazla bilgi için bkz: [Redis veritabanları nelerdir?](cache-faq.md#what-are-redis-databases)

> [!NOTE]
> Merhaba `databases` ayarını önbelleği oluşturma sırasında yalnızca yapılandırılmış ve yalnızca PowerShell, CLI veya diğer yönetim istemcileri kullanarak olabilir. Yapılandırma örneği için `databases` PowerShell kullanarak önbellek oluşturma sırasında bkz [yeni AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).
> 
> 

<a name="maxclients"></a>
<sup>2</sup> `maxclients` her Azure Redis fiyatlandırma katmanı önbelleği için farklıdır.

* Temel ve standart önbellekler
  * C0 (250 MB) önbelleği - too256 bağlantıları
  * C1 (1 GB) önbelleği - too1, 000 bağlantıları
  * C2 (2,5 GB) önbelleği - too2, 000 bağlantıları
  * C3 (6 GB) önbelleği - too5, 000 bağlantıları
  * C4 (13 GB) önbelleği - too10, 000 bağlantıları
  * C5 (26 GB) önbelleği - too15, 000 bağlantıları
  * C6 (53 GB'a) önbelleği - too20, 000 bağlantıları
* Premium önbelleklere
  * P1 (6 GB - 60 GB) - too7, 500 bağlantılar kurma
  * P2 (13 GB - 130 GB) - too15, 000 bağlantıları kurma
  * P3 (26 GB - 260 GB) - too30, 000 bağlantıları kurma
  * P4 (53 GB'a - 530 GB) - too40, 000 bağlantıları kurma

> [!NOTE]
> Her önbellek boyutunu sağlar, ancak *kadar* belirli bir sayıda bağlantıları, her bağlantı tooRedis ek yükü ile ilişkili. TLS/SSL şifreleme sonucunda CPU ve bellek kullanımı gibi ek yükü örneği olacaktır. Belirtilen önbellek boyutu Hello en fazla bağlantı sınırı hafifçe yüklü bir önbellek varsayar. Varsa yük bağlantı yükünü *artı* istemci işlemleri yükü hello sistem kapasitesini aşıyor, hello geçerli önbellek boyutu hello bağlantı sınırını aştınız değil olsa bile, hello önbellek kapasite sorunları deneyimi.
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a>Azure Redis Önbelleği'nde desteklenmeyen komutlar redis
> [!IMPORTANT]
> Microsoft tarafından yapılandırma ve Azure Redis önbelleği örnekleri yönetimini yönetilir çünkü hello aşağıdaki komutları devre dışı bırakılır. Tooinvoke denerseniz, bunları, çok benzer bir hata iletisi alıyorsunuz`"(error) ERR unknown command"`.
> 
> * BGREWRITEAOF
> * BGSAVE
> * YAPILANDIRMA
> * HATA AYIKLAMA
> * GEÇİRME
> * KAYDET
> * KAPATMA
> * SLAVEOF
> * Küme - komutları devre dışı bırakılır yazma ancak salt okunur Küme komutları izin verilir.
> 
> 

Redis komutları hakkında daha fazla bilgi için bkz: [http://redis.io/commands](http://redis.io/commands).

## <a name="redis-console"></a>Konsol redis
Komutları tooyour Azure Redis önbelleği örnekleri hello kullanarak güvenli bir şekilde verebilir **Redis konsol**, hello tüm ön bellek katmanlarını için Azure portalı içinde kullanılabilir olduğu.

> [!IMPORTANT]
> - Merhaba Redis konsolu ile çalışmıyor [VNET](cache-how-to-premium-vnet.md). Önbelleğinizi VNET parçası olduğunda, yalnızca hello VNET istemcilerinde hello önbelleğe erişebilir. Redis konsol VNET hello dışında olan yerel tarayıcınızda çalıştığından tooyour önbellek bağlanamıyor.
> - Azure Redis Önbelleği'nde desteklenen tüm Redis komutları. Önceki hello Azure Redis önbelleği için devre dışı Redis komutların listesi için bkz: [Redis Azure Redis Önbelleği'nde desteklenmeyen komutlar](#redis-commands-not-supported-in-azure-redis-cache) bölümü. Redis komutları hakkında daha fazla bilgi için bkz: [http://redis.io/commands](http://redis.io/commands).
> 
> 

tooaccess hello Redis konsol tıklatın **konsol** hello gelen **Redis önbelleği** dikey.

![Konsol redis](./media/cache-configure/redis-console-menu.png)

Önbellek örneğinizin karşı tooissue komutları, yalnızca türü hello komutu hello konsoluna istenen.

![Konsol redis](./media/cache-configure/redis-console.png)


### <a name="using-hello-redis-console-with-a-premium-clustered-cache"></a>Hello kullanarak bir premium konsoluyla Redis önbelleği kümelenmiş

Önbellek kümelenmiş bir premium ile Merhaba Redis konsolunu kullanarak, komutları tooa tek parça hello önbelleğin verebilir. bir komut tooa belirli parça tooissue bağlanmanız toohello istenen parça hello parça seçici üzerinde tıklayarak.

![Konsol redis](./media/cache-configure/redis-console-premium-cluster.png)

Tooaccess bağlı parça hello daha farklı bir parça içinde depolanan bir anahtarı çalışırsanız iletiden bir hata iletisi benzer bir toohello alıyorsunuz.

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

Merhaba önceki örnekte hello Seçili parça parça 1 olan ancak `myKey` parça 0, hello tarafından belirtildiği şekilde bulunur `(shard 0)` hello hata iletisi kısmı. Bu örnekte, tooaccess `myKey`seçin parça 0 kullanarak hello parça Seçici ve sorunu istenen hello komutu.


## <a name="move-your-cache-tooa-new-subscription"></a>Önbellek tooa yeni abonelik taşıma
Tıklayarak önbellek tooa yeni abonelik taşıyabilirsiniz **taşıma**.

![Redis önbelleği taşıma](./media/cache-configure/redis-cache-move.png)

Bir kaynak grubu tooanother ve bir abonelik tooanother kaynakları taşıma hakkında daha fazla bilgi için bkz: [kaynakları toonew kaynak grubuna veya aboneliğe taşıma](../azure-resource-manager/resource-group-move-resources.md).

## <a name="next-steps"></a>Sonraki adımlar
* Redis komutları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl ı çalıştırabilirsiniz Redis komutları?](cache-faq.md#how-can-i-run-redis-commands)

