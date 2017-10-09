---
title: "Azure Redis önbelleği aaaHow tooScale | Microsoft Docs"
description: "Nasıl tooscale Azure Redis öğrenin önbellek örneklerinde"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 350db214-3b7c-4877-bd43-fef6df2db96c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: sdanie
ms.openlocfilehash: 8d7c015a539f872913056392aa080bf3f445bd03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-azure-redis-cache"></a>Nasıl tooScale Azure Redis önbelleği
Azure Redis önbelleği, önbellek boyutunu ve özelliklerini hello seçimi esneklik sağlayan farklı önbellek teklifleri vardır. Bir önbellek oluşturulduktan sonra hello boyutu ve uygulamanızın hello gereksinimleri değiştirirseniz, fiyatlandırma katmanı hello önbelleğin hello ölçeklendirebilirsiniz. Bu makalede, Azure PowerShell ve Azure CLI gibi tooscale önbelleğiniz hem hello Azure portal, hem de kullanarak nasıl araçları gösterir.

## <a name="when-tooscale"></a>Zaman tooscale
Merhaba kullanabilirsiniz [izleme](cache-how-to-monitor.md) Azure Redis önbelleği toomonitor özelliklerini hello sistem durumunu ve performansını önbelleğiniz ve ne zaman tooscale hello önbellek belirlemenize yardımcı olması. 

Merhaba aşağıdaki izleyebilirsiniz ölçümleri toohelp tooscale gerekip gerekmediğini belirleyin.

* Redis sunucu iş yükü
* Bellek kullanımı
* Ağ bant genişliği
* CPU kullanımı

Önbelleğinizi artık uygulamanızın gereksinimlerini karşılıyor mu karar verirseniz, fiyatlandırma katmanı, uygulamanız için doğru tooa daha büyük veya küçük önbellek ölçeklendirebilirsiniz. Hangi fiyatlandırma katmanı toouse önbelleğe belirleme hakkında daha fazla bilgi için bkz: [hangi Redis önbelleği teklifini ve boyutunu kullanmalıyım](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).

## <a name="scale-a-cache"></a>Ölçek bir önbellek
tooscale, önbellek [toohello önbelleği Gözat](cache-configure.md#configure-redis-cache-settings) hello içinde [Azure portal](https://portal.azure.com) tıklatıp **ölçek** hello gelen **kaynak menü**.

![Ölçek](./media/cache-how-to-scale/redis-cache-scale-menu.png)

Select hello istenen fiyatlandırma Katmanı'ndan hello **fiyatlandırma katmanı seçme** tıklayın ve dikey **seçin**.

![Fiyatlandırma katmanı][redis-cache-pricing-tier-blade]


Tooa kısıtlamaları aşağıdaki hello ile fiyatlandırma katmanı farklı ölçeklendirebilirsiniz:

* Bir daha yüksek fiyatlandırma katmanı tooa fiyatlandırma katmanı alt ölçeklendirme olamaz.
  * Ölçeklendirme olamaz bir **Premium** tooa aşağı önbellek **standart** veya **temel** önbelleği.
  * Ölçeklendirme olamaz bir **standart** tooa aşağı önbellek **temel** önbelleği.
* Ölçeklendirme yapılabilir bir **temel** tooa önbelleğe **standart** önbellek ancak hello hello boyutta değiştiremiyor aynı anda. Farklı bir boyut gerekiyorsa, bir sonraki ölçeklendirme işlemi istenen toohello boyutu yapabilirsiniz.
* Ölçeklendirme olamaz bir **temel** doğrudan tooa önbelleğe **Premium** önbelleği. Ölçeklendirme gerekir **temel** çok**standart** bir ölçeklendirme işlemi ve ardından gelen **standart** çok**Premium** , sonraki ölçeklendirme işlem.
* Büyük bir değerden toohello aşağı ölçeklendirme olamaz **C0 (250 MB)** boyutu.
 
Merhaba önbellek toohello yeni fiyatlandırma katmanı, ölçekleme sırasında bir **ölçeklendirme** durum hello görüntülenen **Redis önbelleği** dikey.

![Ölçeklendirme][redis-cache-scaling]

Ölçeklendirme tamamlandığında hello durum değişiklikleri **ölçeklendirme** çok**çalıştıran**.

## <a name="how-tooautomate-a-scaling-operation"></a>Nasıl tooautomate bir ölçeklendirme işlemi
Toplama tooscaling önbellek örneklerinizi Azure portal Merhaba, PowerShell cmdlet'leri, Azure CLI kullanarak ölçeklendirme ve Microsoft Azure yönetim kitaplıkları (MAML) hello kullanarak. 

* [PowerShell kullanarak ölçek](#scale-using-powershell)
* [Azure CLI kullanarak ölçek](#scale-using-azure-cli)
* [Ölçek MAML kullanma](#scale-using-maml)

### <a name="scale-using-powershell"></a>PowerShell kullanarak ölçek
Hello kullanarak PowerShell ile Azure Redis önbelleği örneklerinizi ölçeklendirebilirsiniz [kümesi AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet hello zaman `Size`, `Sku`, veya `ShardCount` özellikleri değiştirilemez. Merhaba aşağıdaki örnekte nasıl tooscale bir önbellek adlı gösterir `myCache` tooa 2,5 GB önbellek. 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

PowerShell ile ölçeklendirme ile ilgili daha fazla bilgi için bkz: [tooscale bir Redis önbelleğe Powershell kullanarak](cache-howto-manage-redis-cache-powershell.md#scale).

### <a name="scale-using-azure-cli"></a>Azure CLI kullanarak ölçek
Azure CLI kullanarak Azure Redis önbelleği örneklerinizi tooscale çağrısı hello `azure rediscache set` komut ve yeni boyutu, sku veya hello bağlı olarak küme boyutu dahil istenen hello yapılandırma değişikliklerini geçişinde istenen ölçekleme işlemi.

Azure CLI ile ölçeklendirme ile ilgili daha fazla bilgi için bkz: [var olan bir Redis Önbelleği Ayarları Değiştir](cache-manage-cli.md#scale).

### <a name="scale-using-maml"></a>Ölçek MAML kullanma
tooscale hello kullanarak, Azure Redis önbelleği örnekleri [Microsoft Azure yönetim kitaplıkları (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), çağrı hello `IRedisOperations.CreateOrUpdate` yöntemi ve yeni boyutu hello hello geçişinde `RedisProperties.SKU.Capacity`.

    static void Main(string[] args)
    {
        // For instructions on getting hello access token, see
        // https://azure.microsoft.com/documentation/articles/cache-configure/#access-keys
        string token = GetAuthorizationHeader();

        TokenCloudCredentials creds = new TokenCloudCredentials(subscriptionId,token);

        RedisManagementClient client = new RedisManagementClient(creds);
        var redisProperties = new RedisProperties();

        // tooscale, set a new size for hello redisSKUCapacity parameter.
        redisProperties.Sku = new Sku(redisSKUName,redisSKUFamily,redisSKUCapacity);
        redisProperties.RedisVersion = redisVersion;
        var redisParams = new RedisCreateOrUpdateParameters(redisProperties, redisCacheRegion);
        client.Redis.CreateOrUpdate(resourceGroupName,cacheName, redisParams);
    }

Daha fazla bilgi için bkz: Merhaba [yönetmek MAML kullanarak Redis önbelleği](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) örnek.

## <a name="scaling-faq"></a>Ölçeklendirme ile ilgili SSS
Merhaba aşağıdaki listede Azure Redis önbelleği ölçeklendirme hakkında sorular yanıtlar toocommonly içerir.

* [İçin ya da Premium önbelleği içinde ölçekleme?](#can-i-scale-to-from-or-within-a-premium-cache)
* [Ölçeklendirme sonra ı toochange my önbellek adını veya erişim anahtarları var mı?](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [Ölçeklendirme nasıl çalışır?](#how-does-scaling-work)
* [Ölçeklendirme sırasında ı my önbellekten veri kaybedersiniz?](#will-i-lose-data-from-my-cache-during-scaling)
* [My özel veritabanlarını ölçeklendirme sırasında etkilenen ayarlıyor?](#is-my-custom-databases-setting-affected-during-scaling)
* [My önbellek ölçeklendirme sırasında kullanılabilir olacak?](#will-my-cache-be-available-during-scaling)
* [Desteklenmeyen işlemleri](#operations-that-are-not-supported)
* [Ne kadar ölçeklendirme sürer?](#how-long-does-scaling-take)
* [Ölçeklendirme tamamlandığında nasıl anlayabilirim?](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a>İçin ya da Premium önbelleği içinde ölçekleme?
* Ölçeklendirme olamaz bir **Premium** tooa aşağı önbellek **temel** veya **standart** fiyatlandırma katmanı.
* Birinden ölçeklendirebilirsiniz **Premium** önbellek fiyatlandırma katmanı tooanother.
* Ölçeklendirme olamaz bir **temel** doğrudan tooa önbelleğe **Premium** önbelleği. Öğesinden önce Ölçeklendirmesi gerekir **temel** çok**standart** bir ölçeklendirme işlemi ve ardından gelen **standart** çok**Premium** sonraki ölçeklendirme işlemi.
* Kümeleme etkinleştirilirse oluşturduğunuzda, **Premium** önbellek, şunları yapabilirsiniz [hello küme boyutunu değiştirme](cache-how-to-premium-clustering.md#cluster-size). Önbelleğinizi etkin Kümeleme olmadan oluşturulduysa, daha sonraki bir zamanda kümeleme yapılandıramazsınız.
  
  Daha fazla bilgi için bkz: [nasıl bir Premium Azure Redis önbelleği için kümeleri tooconfigure](cache-how-to-premium-clustering.md).

### <a name="after-scaling-do-i-have-toochange-my-cache-name-or-access-keys"></a>Ölçeklendirme sonra ı toochange my önbellek adını veya erişim anahtarları var mı?
Hayır, önbellek adı ve anahtarları bir ölçeklendirme işlemi sırasında değiştirilmez.

### <a name="how-does-scaling-work"></a>Ölçeklendirme nasıl çalışır?
* Zaman bir **temel** önbellek ölçeklendirilmiş tooa farklı boyutu, onu kapatılır ve yeni bir önbellek hello yeni boyut kullanılarak sağlanır. Bu süre boyunca hello önbellek kullanılamıyor ve hello önbelleğindeki verilerin tümü kaybolur.
* Zaman bir **temel** önbelleğidir ölçeklendirilmiş tooa **standart** önbellek, çoğaltma önbelleği hazırlanmıştır ve hello veri hello birincil önbellek toohello çoğaltma önbellekten kopyalanır. Merhaba önbellek işlem ölçeklendirme hello sırasında kullanılabilir olarak kalır.
* Zaman bir **standart** önbelleğidir ölçeklendirilmiş tooa farklı boyutu veya tooa **Premium** önbellek, biri hello çoğaltmaları kapatılması ve yeniden sağlanan üzerinden aktarılan toohello yeni boyutunu ve hello verileri ve hello diğer Çoğaltma, yeniden sağlanmadan önce yük devretme, başarısızlığın hello önbellek düğümlerinden biri sırasında oluşan benzer toohello işlem gerçekleştirir.

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a>Ölçeklendirme sırasında ı my önbellekten veri kaybedersiniz?
* Zaman bir **temel** ölçeklendirilmiş tooa yeni boyutu, tüm veriler kaybolur ve hello önbellek işlemi ölçeklendirme hello sırasında kullanılamıyorsa önbelleği.
* Zaman bir **temel** önbelleğidir ölçeklendirilmiş tooa **standart** önbelleğe, hello hello önbellekteki veri genellikle korunur.
* Zaman bir **standart** önbelleğidir ölçeklendirilmiş tooa büyük ya da katmanı, veya bir **Premium** önbellek ölçeklendirilmiş tooa büyük boyut, tüm verileri genellikle korunur. Ölçekleme sırasında bir **standart** veya **Premium** tooa daha küçük boyutu, veri aşağı önbellek kaybolabilir ne kadar veri hello önbelleğinde olan bağlı olarak ilgili toohello yeni boyutu, ölçeklendirilir olduğunda. Veri ölçeklendirdiğinizde kaybolursa, anahtarları hello kullanarak çıkarılacak [allkeys lru](http://redis.io/topics/lru-cache) çıkarma ilkesi. 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a>My özel veritabanlarını ölçeklendirme sırasında etkilenen ayarlıyor?
Bazı fiyatlandırma katmanları farklı sahip [veritabanları sınırları](cache-configure.md#databases), böylece bazı noktalar IF ölçekleme hello için özel bir değer yapılandırıldığında `databases` önbellek oluşturma sırasında ayarlama.

* Fiyatlandırma katmanı ile bir alt tooa'ne zaman ölçeklendirme `databases` hello geçerli katmanı sınırından:
  * Merhaba varsayılan sayısı kullanıyorsanız `databases` tüm fiyatlandırma katmanlarına 16 olduğu, veri kaybı olmamasına.
  * Özel bir dizi kullanıyorsanız `databases` ölçeklendirme, hello katmanı toowhich için hello sınırları içinde kalan bu `databases` ayarı tutulur ve veri kaybı olmamasına.
  * Özel bir dizi kullanıyorsanız `databases` , hello sınırlarını hello yeni katmanının hello aşıyor `databases` ayarı hello yeni katmanı alçaltılmış toohello sınırları ve kaldırılmış hello veritabanlarındaki verilerin tümü kaybolur.
* Aynı veya daha yüksek fiyatlandırma katmanı hello ile tooa'ne zaman ölçeklendirme `databases` hello geçerli katmanı sınırından, `databases` ayarı tutulur ve veri kaybı olmamasına.

% 99,9 SLA kullanılabilirlik için standart ve Premium önbellekleri sahip olsa da, veri kaybı için hiçbir SLA yoktur.

### <a name="will-my-cache-be-available-during-scaling"></a>My önbellek ölçeklendirme sırasında kullanılabilir olacak?
* **Standart** ve **Premium** önbellekleri kullanılabilir olmaya devam eder işlemi ölçeklendirme hello sırasında.
* **Temel** önbellekleri işlemleri tooa farklı boyutu ölçeklendirme sırasında çevrimdışı, ancak gelen ölçekleme sırasında kullanılabilir olmaya devam etmesi **temel** çok**standart**.

### <a name="operations-that-are-not-supported"></a>Desteklenmeyen işlemleri
* Bir daha yüksek fiyatlandırma katmanı tooa fiyatlandırma katmanı alt ölçeklendirme olamaz.
  * Ölçeklendirme olamaz bir **Premium** tooa aşağı önbellek **standart** veya **temel** önbelleği.
  * Ölçeklendirme olamaz bir **standart** tooa aşağı önbellek **temel** önbelleği.
* Ölçeklendirme yapılabilir bir **temel** tooa önbelleğe **standart** önbellek ancak hello hello boyutta değiştiremiyor aynı anda. Farklı bir boyut gerekiyorsa, bir sonraki ölçeklendirme işlemi istenen toohello boyutu yapabilirsiniz.
* Ölçeklendirme olamaz bir **temel** doğrudan tooa önbelleğe **Premium** önbelleği. Öğesinden önce Ölçeklendirmesi gerekir **temel** çok**standart** bir ölçeklendirme işlemi ve ardından gelen **standart** çok**Premium** sonraki ölçeklendirme işlemi.
* Büyük bir değerden toohello aşağı ölçeklendirme olamaz **C0 (250 MB)** boyutu.

Bir ölçeklendirme işlemi başarısız olursa, hello hizmet toorevert hello işlemi deneyecek ve hello önbellek toohello özgün boyutunu döner.

### <a name="how-long-does-scaling-take"></a>Ne kadar ölçeklendirme sürer?
Yaklaşık 20 hello önbellekte ne kadar veri bağlı olarak dakika sürer ölçeklendirme.

### <a name="how-can-i-tell-when-scaling-is-complete"></a>Ölçeklendirme tamamlandığında nasıl anlayabilirim?
Hello Azure portal, devam eden işlemi ölçeklendirme hello görebilirsiniz. Ölçeklendirme tamamlandığında hello önbelleği değişiklikleri durumunu çok hello**çalıştıran**.

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



