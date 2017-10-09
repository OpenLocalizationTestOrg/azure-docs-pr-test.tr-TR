---
title: "aaaIntroduction toohello Azure Redis önbelleği Premium katmanına | Microsoft Docs"
description: "Bilgi nasıl toocreate Redis kalıcılığı, Redis Kümeleme ve Premium katmanı Azure Redis önbelleği örnekleri VNET desteği ve yönetme"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 30f46f9f-e6ec-4c38-a8cc-f9d4444856e5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 5b58a03647fbf1198509ac6f1acd04f1b682ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-redis-cache-premium-tier"></a>Giriş toohello Azure Redis önbelleği Premium katmanına
Azure Redis önbelleği Süper hızlı erişim tooyour veri sağlayarak yüksek oranda ölçeklenebilir ve esnek uygulamalar oluşturmanıza yardımcı olan dağıtılmış, yönetilen bir önbelleğidir. 

Tüm hello standart katman özellikleri ve daha iyi performans, daha büyük iş yükleri, olağanüstü durum kurtarma, içeri/dışarı aktarma gibi daha fazlasını içerir ve Gelişmiş güvenlik bir kurumsal hazır katmanı, yeni Premium katmanı olan hello. Okuma toolearn hello Premium önbellek katmanının hello ek özellikler hakkında daha fazla devam edin.

## <a name="better-performance-compared-toostandard-or-basic-tier"></a>Daha iyi performans tooStandard veya temel katmana karşılaştırma
**Performans katmanı standart üzerinden veya temel daha iyi.** Merhaba Premium katmanındaki önbellekleri daha hızlı bir işlemciye sahip ve daha iyi karşılaştırıldığında performansı toohello temel veya standart katman sunan donanımda dağıtılır. Premium katmanı önbellekleri daha yüksek verimlilik ve düşük gecikme vardır. 

**Üretim hello için aynı boyutta önbelleği karşılaştırılan tooStandard katman olarak Premium'da daha yüksektir.** Örneğin, hello verimini 53 GB'a P4 (Premium) önbelleğidir C6 için karşılaştırılan too150K olarak saniyede 250K istekler (standart).

Boyut, işleme ve premium önbelleklere sahip bant genişliği hakkında daha fazla bilgi için bkz: [Azure Redis önbelleği SSS](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)

## <a name="redis-data-persistence"></a>Redis veri kalıcılığını
Hello Premium katman bir Azure depolama hesabında toopersist hello önbellek verileri sağlar. Basic/standart önbelleğinde tüm hello verileri yalnızca bellekte depolanır. Altyapının durumunda sorunlar var. olası veri kaybı olabilir. Veri kaybına karşı hello Premium katmanı tooincrease dayanıklılık içinde hello Redis veri kalıcılığını özelliğini kullanmanızı öneririz. Azure Redis önbelleği seçeneklerinde RDB ve (yakında) AOF sunar [Redis kalıcılığı](http://redis.io/topics/persistence). 

Kalıcılığı yapılandırma ile ilgili yönergeler için bkz: [nasıl Premium Azure Redis önbelleği için kalıcılığı tooconfigure](cache-how-to-premium-persistence.md).

## <a name="redis-cluster"></a>Redis kümesi
Toocreate önbellekleri 53 GB'den büyük istediğiniz veya birden çok Redis düğümünde tooshard veri istiyorsanız hello Premium katmanında kullanılabilir olduğu kümeleme Redis kullanabilirsiniz. Her düğüm, yüksek kullanılabilirlik için Azure tarafından yönetilen bir birincil/çoğaltma önbelleği çifti oluşur. 

**Redis kümeleme en fazla ölçek ve verimlilik sağlar.** Parça (düğümler) hello kümedeki hello sayısını artırmak üretilen işi doğrusal olarak artar. Ör. 10 parça P4 kümesi oluşturun ardından hello kullanılabilir verimlilik olduğu 250 K * 10 saniye başına 2,5 milyon istek =. Lütfen hello bakın [Azure Redis önbelleği SSS](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) boyut, işleme ve premium önbelleklere sahip bant genişliği hakkında daha fazla ayrıntı için.

Kümeleme ile başlatılan tooget bkz [nasıl bir Premium Azure Redis önbelleği için kümeleri tooconfigure](cache-how-to-premium-clustering.md).

## <a name="enhanced-security-and-isolation"></a>Geliştirilmiş güvenlik ve yalıtım
Merhaba temel veya standart katmanında oluşturduğunuzu önbellekleri üzerinde erişilebilir genel internet hello. Erişim toohello önbellek kısıtlı göre hello erişim anahtardır. Merhaba Premium katmanı ile ilgili daha fazla, yalnızca belirtilen ağ istemcileri hello önbellek erişebildiğinden emin olun. Redis Önbelleği'nde dağıtabileceğiniz bir [Azure sanal ağ (VNet)](https://azure.microsoft.com/services/virtual-network/). Alt ağlar, erişim denetimi ilkeleri ve diğer özellikleri toofurther erişim tooRedis kısıtlamak gibi vnet'in tüm hello özelliklerini kullanabilirsiniz.

Daha fazla bilgi için bkz: [tooconfigure sanal ağ Premium Azure Redis önbelleği için nasıl destek](cache-how-to-premium-vnet.md).

## <a name="importexport"></a>İçeri/Dışarı Aktarma
İçeri/dışarı aktarma tooimport veri Azure Redis önbelleği veya Azure Redis önbelleği verileri dışa aktarma ve Redis önbelleği veritabanı'nı (RDB) anlık bir Azure premium önbellek tooa sayfa blobu dışarı aktarma sağlayan bir Azure Redis önbelleği veri yönetimi işlemdir Depolama hesabı. Bu, farklı Azure Redis önbelleği örnekleri arasında toomigrate etkinleştirir veya hello önbellek kullanmadan önce verilerle doldurma.

İçeri aktarma kullanılan toobring Redis uyumlu RDB dosyaları herhangi bir bulut veya ortamını Linux, Windows ya da herhangi bir bulut sağlayıcısına Amazon Web Hizmetleri ve diğerleri gibi çalışan Redis çalıştıran herhangi bir Redis sunucudan olabilir. Veri alma kolay bir yolu toocreate önceden doldurulmuş haldedir verilerle bir önbellek olur. Merhaba içeri aktarma işlemi sırasında Azure Redis önbelleği hello RDB dosyaları Azure Storage'dan belleğe yükler ve sonra hello anahtarları hello önbelleğine ekler.

Dışarı aktarma Azure Redis önbelleği tooRedis uyumlu RDB dosyasında depolanan tooexport hello verileri sağlar. Bu özellik toomove verilerden bir Azure Redis önbelleği örneği tooanother veya tooanother Redis sunucusu kullanabilirsiniz. Hello dışa aktarma işlemi sırasında Azure Redis önbelleği sunucu örneği konakları hello ve depolama hesabı belirlenmiş karşıya yüklenen toohello hello dosyadır VM hello üzerinde geçici bir dosya oluşturulur. Merhaba dışa aktarma işlemi ya da durumunu başarı veya hata ile tamamlandığında hello geçici dosya silindi.

Daha fazla bilgi için bkz: [nasıl tooimport verisine ve Azure Redis Önbelleği'nden veri dışarı aktarma](cache-how-to-import-export-data.md).

## <a name="reboot"></a>Yeniden başlatma
Merhaba premium katmanı tooreboot sağlar, önbellek isteğe bağlı bir veya daha fazla düğümlerinin. Tootest bu sayede uygulamanız hello olay dayanıklılık için bir hata. Düğümleri aşağıdaki hello yeniden başlatabilirsiniz.

* Önbelleğinizi ana düğümünün
* Önbelleğinizi ikincil düğümü
* Önbelleğinizi hem ana hem de ikincil düğümlerinin
* Premium önbelleği Kümeleme ile kullanırken, hello ana, ikincil veya tek tek parça hello önbelleğinde için her iki düğüm yeniden başlatılabilir

Daha fazla bilgi için bkz: [yeniden](cache-administration.md#reboot) ve [yeniden SSS](cache-administration.md#reboot-faq).

>[!NOTE]
>Yeniden başlatma işlevselliği için tüm Azure Redis önbelleği katmanları şimdi etkinleştirildi.
>
>

## <a name="schedule-updates"></a>Güncelleştirmeleri zamanlama
Merhaba zamanlanmış güncelleştirmeler özelliği toodesignate önbelleğiniz için bir bakım penceresi sağlar. Merhaba bakım penceresi belirtildiğinde, herhangi bir Redis sunucu güncelleştirme sırasında bu pencereyi yapılır. toodesignate bir bakım penceresi istenen hello günleri seçin ve her gün için hello bakım penceresi başlangıç saati belirtin. Merhaba bakım penceresi saati UTC biçiminde olduğunu unutmayın. 

Daha fazla bilgi için bkz: [zamanlama güncelleştirmeleri](cache-administration.md#schedule-updates) ve [SSS güncelleştirmeleri zamanla](cache-administration.md#schedule-updates-faq).

> [!NOTE]
> Yalnızca sunucu güncelleştirmeleri hello zamanlanmış bakım penceresi sırasında yapılan Redis. Merhaba bakım penceresi tooAzure güncelleştirmeleri uygulanmaz veya toohello VM işletim sistemi güncelleştirir.
> 
> 

## <a name="geo-replication"></a>Coğrafi çoğaltma

**Coğrafi çoğaltma** iki Premium katmanı Azure Redis önbelleği örnekleri bağlama için bir mekanizma sağlar. Bir önbellek hello birincil bağlantılı önbellek ve hello hello ikincil bağlantılı önbelleği gibi diğer olarak atanır. Merhaba ikincil bağlantılı önbellek salt okunur olur ve yazılı toohello birincil önbelleği veri toohello ikincil bağlantılı önbellek çoğaltılır. Bu işlev Azure bölgeler arasında kullanılan tooreplicate bir önbellek olabilir.

Daha fazla bilgi için bkz: [nasıl Azure Redis önbelleği için coğrafi çoğaltma tooconfigure](cache-how-to-geo-replication.md).


## <a name="tooscale-toohello-premium-tier"></a>tooscale toohello premium katmanı
tooscale toohello premium katmanı, bir hello premium katmanı hello seçmeniz yeterlidir **fiyatlandırma katmanı değişikliği** dikey. Ayrıca PowerShell ve CLI kullanarak önbellek toohello premium katman ölçeklendirebilirsiniz. Adım adım yönergeler için bkz: [nasıl tooScale Azure Redis önbelleği](cache-how-to-scale.md) ve [nasıl tooautomate bir ölçeklendirme işlemi](cache-how-to-scale.md#how-to-automate-a-scaling-operation).

## <a name="next-steps"></a>Sonraki adımlar
Önbellek oluşturmak ve hello yeni premium katmanı özellikleri keşfedin.

* [Nasıl tooconfigure kalıcılığını Premium Azure Redis önbelleği](cache-how-to-premium-persistence.md)
* [Sanal ağ tooconfigure Premium Azure Redis önbelleği için nasıl destekler](cache-how-to-premium-vnet.md)
* [Nasıl bir Premium Azure Redis önbelleği için kümeleri tooconfigure](cache-how-to-premium-clustering.md)
* [Nasıl tooimport verisine ve Azure Redis Önbelleği'nden veri dışarı aktarma](cache-how-to-import-export-data.md)
* [Nasıl tooadminister Azure Redis önbelleği](cache-administration.md)

