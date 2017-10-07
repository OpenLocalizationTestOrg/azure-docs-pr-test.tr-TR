---
title: "SQL veritabanı kaynak sınırları aaaAzure | Microsoft Docs"
description: "Bu sayfa, Azure SQL veritabanı için bazı ortak kaynak sınırları açıklar."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 884e519f-23bb-4b73-a718-00658629646a
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2017
ms.author: carlrab
ms.openlocfilehash: 3e7be4fdc74e802d37274690531caaf138bcedb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-resource-limits"></a>Azure SQL veritabanı kaynak sınırları
## <a name="overview"></a>Genel Bakış
Azure SQL veritabanı iki farklı mekanizmalarını kullanarak hello kaynakları kullanılabilir tooa veritabanı yönetir: **kaynakları idare** ve **zorlama, sınırları**. Bu konuda, bu iki temel konu kaynak yönetimi açıklanmaktadır.

## <a name="resource-governance"></a>Kaynak İdaresi
Merhaba tasarım hedefleri hello temel, standart, Premium ve Premium RS hizmet katmanı için Azure SQL veritabanı toobehave hello veritabanı diğer veritabanlarından yalıtılmış kendi makinede çalışıyor gibi biridir. Kaynak İdaresi Bu davranış öykünür. Hello toplanan kaynak kullanımı hello en fazla kullanılabilir CPU, bellek, günlük g/ç ve veri g/ç kaynakları atanan toohello veritabanına kaynak İdaresi yürütme sıraları sorgularda ulaşana ve toohello sorguları olarak boşaltın sıraya alınmış kaynaklar atayın.

Olarak daha uzun bir yürütme sorguları, şu anda yürütülmekte olan tüm kullanılabilir kaynakları sonuçlarında kullanılarak adanmış bir makinede hangi komutu zaman aşımı hello istemcide neden olabilir. Agresif yeniden deneme mantığı ile uygulamaları ve yüksek yoğunlukta hello veritabanıyla sorgu yürütebilir uygulamaları hata iletileri hello eş zamanlı istek sınırına ulaşıldı zaman tooexecute yeni sorgular çalışırken karşılaşırsınız.

### <a name="recommendations"></a>Öneriler:
Merhaba kaynak kullanımı ve sorguları hello ortalama yanıt sürelerini hello en iyi veritabanı dolmak üzere olduğunda izleyin. Daha yüksek sorgu gecikmeleri karşılaşıldığında, genellikle üç seçeneğiniz vardır:

1. Gelen istekleri toohello veritabanı tooprevent zaman aşımı ve hello yığını istekleri Hello sayısını azaltın.
2. Daha yüksek performans düzeyi toohello veritabanı atayın.
3. Her sorgu sorguları tooreduce hello kaynak kullanımı en iyi duruma getirme. Daha fazla bilgi için bkz: hello hello Azure SQL Database performans rehberi makaledeki sorgu ayarlama/Hinting bölümü.

## <a name="enforcement-of-limits"></a>Sınırlarının zorlama
Kaynaklar CPU, bellek, günlük g/ç ve veri g/ç dışında sınırlara ulaşıldığında, yeni istekleri vermeyerek uygulanır. Bir veritabanı hello yapılandırılmış en büyük boyut sınırı, ekler ve artırmak güncelleştirmeleri ulaştığında veri boyutu başarısız seçer ve silme toowork devam ederken. İstemcileri alır bir [hata iletisi](sql-database-develop-error-messages.md) ulaşıldı hello sınırı bağlı olarak.

Örneğin, bağlantıları tooa SQL veritabanı hello sayısı ve hello işlenebilir eşzamanlı istek sayısı sınırlıdır. SQL veritabanı bağlantılarını toohello veritabanı toobe hello sayıda eşzamanlı istek toosupport bağlantı havuzu sayısı hello büyük izin verir. Kullanılabilir bağlantı Hello sayısı hello uygulama tarafından kolayca denetlenebilir, ancak hello paralel istekler genellikle kez daha zor tooestimate ve toocontrol sayısıdır. Merhaba uygulaması ya da çok fazla istek gönderir veya kaynak sınırlarına hello veritabanı ulaştığında ve çalışan iş parçacığı toolonger çalışan sorguları son piling başlar, hatalarla karşılaştı özellikle yükleri dağıtmakta sırasında.

## <a name="service-tiers-and-performance-levels"></a>Hizmet katmanları ve performans düzeyleri
Hizmet katmanları ve performans düzeyleri tek veritabanı ve esnek havuzlar için vardır.

### <a name="single-databases"></a>Tek veritabanları
Tek bir veritabanı için bir veritabanı hello sınırları hello veritabanının Hizmet katmanını ve performans düzeyine göre tanımlanır. Aşağıdaki tablonun hello performans düzeyleri değişen en temel, standart, Premium ve Premium RS veritabanları hello özelliklerini açıklar.

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

> [!IMPORTANT]
> P11 ve P15 performans düzeyleri kullanan müşteriler, ek ücret ödemeden dahil depolama too4 TB yukarı kullanabilirsiniz. Bu 4 TB seçeneği bölgeleri aşağıdaki hello şu anda kullanılabilir değil: BİZE East2, Batı ABD, BİZE kamu Virginia, Batı Avrupa, Orta Almanya, Güney Doğu Asya, Japonya Doğu, Avustralya Doğu, Kanada merkezi ve Doğu Kanada.
>

### <a name="elastic-pools"></a>Esnek havuzlar
[Esnek havuzlar](sql-database-elastic-pool.md) kaynakları hello havuzdaki veritabanları arasında paylaşın. Aşağıdaki tablonun hello temel, standart, Premium ve Premium RS esnek havuzlar hello özelliklerini açıklar.

[!INCLUDE [SQL DB service tiers table for elastic databases](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

Merhaba önceki tablolarda listelenen her bir kaynak için bir genişletilmiş tanımı Merhaba açıklamalarına bakın [hizmet katmanı özellikleri ve sınırları](sql-database-performance-guidance.md#service-tier-capabilities-and-limits). Hizmet katmanları genel bakış için bkz: [Azure SQL Database hizmet katmanları ve performans düzeyleri](sql-database-service-tiers.md).

## <a name="other-sql-database-limits"></a>Diğer SQL veritabanı sınırları
| Alan | Sınır | Açıklama |
| --- | --- | --- |
| Abonelik başına otomatik verme kullanılarak veritabanları |10 |Otomatik dışarı aktarma, SQL veritabanlarını yedekleme için özel bir zamanlama toocreate sağlar. Bu özelliğin Hello preview 1 Mart 2017 sona erer.  |
| Sunucu başına veritabanları |Too5000 |Too5000 veritabanları sunucu başına izin verilir. |
| Sunucu başına Dtu'lar |45000 |45000 Dtu'lar, bağımsız veritabanları ve esnek havuzlar sağlamak için sunucu başına izin verilir. tek başına veritabanı ve sunucu başına izin verilen havuzları toplam sayısı Hello sunucu Dtu'lar yalnızca hello sayısına göre sınırlıdır.  

> [!IMPORTANT]
> Azure SQL veritabanı otomatik dışarı aktarma Önizleme'de sunulmuştur ve 1 Mart 2017 üzerinde kullanımdan kaldırılacaktır. 1. aralık 2016'dan başlayarak artık mümkün tooconfigure otomatik dışarı aktarma herhangi bir SQL veritabanı üzerinde olacaktır. Tüm mevcut otomatik dışarı aktarma işleri toowork 1 Mart 2017 kadar devam eder. 1. aralık 2016'dan sonra kullanabileceğiniz [uzun vadeli yedekleme bekletme](sql-database-long-term-retention.md) veya [Azure Otomasyonu](../automation/automation-intro.md) tooarchive SQL veritabanları düzenli olarak düzenli aralıklarla tercih ettiğiniz tooa zamanlamaya göre PowerShell kullanarak. Bir örnek komut dosyası için hello indirebilirsiniz [örnek komut dosyası github'dan](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export).
>


## <a name="resources"></a>Kaynaklar
[Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md)

[Azure SQL Database hizmet katmanları ve performans düzeyleri](sql-database-service-tiers.md)

[SQL Veritabanı istemci programları için hata iletileri](sql-database-develop-error-messages.md)
