---
title: "Azure SQL veritabanı kaynak sınırları | Microsoft Docs"
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
ms.openlocfilehash: e75458db79e6c15f8d5155b71f04a20fa21818ff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-sql-database-resource-limits"></a>Azure SQL veritabanı kaynak sınırları
## <a name="overview"></a>Genel Bakış
Azure SQL veritabanı iki farklı mekanizmalarını kullanarak bir veritabanı için kullanılabilir kaynakları yönetir: **kaynakları idare** ve **zorlama, sınırları**. Bu konuda, bu iki temel konu kaynak yönetimi açıklanmaktadır.

## <a name="resource-governance"></a>Kaynak İdaresi
Temel, standart, Premium ve Premium RS hizmet katmanları, Tasarım hedeflerini veritabanı diğer veritabanlarından yalıtılmış kendi makinede çalışıyor gibi davranmasını Azure SQL veritabanı için biridir. Kaynak İdaresi Bu davranış öykünür. Toplanan kaynak kullanımı en fazla kullanılabilir CPU ulaşırsa, bellek, günlük g/ç ve veri g/ç kaynakları kaynak İdaresi sıraları yürütme sorgularda veritabanı atanan ve bunlar boşaltmak gibi kaynakları sıraya alınan sorguları atayın.

Olarak daha uzun bir yürütme sorguları, şu anda yürütülmekte olan tüm kullanılabilir kaynakları sonuçlarında kullanılarak adanmış bir makinede, istemci üzerinde komut zaman aşımı neden olabilir. Agresif yeniden deneme mantığı ile uygulamaları ve yüksek yoğunlukta veritabanıyla sorgu yürütebilir uygulamaları hata iletileri eş zamanlı istek sınırına ulaşıldığında, yeni sorgular yürütmeye çalışırken karşılaşırsınız.

### <a name="recommendations"></a>Öneriler:
Kaynak kullanımı ve sorguların ortalama yanıt süreleri en iyi veritabanı dolmak üzere olduğunda izleyin. Daha yüksek sorgu gecikmeleri karşılaşıldığında, genellikle üç seçeneğiniz vardır:

1. Zaman aşımı ve yukarı yığın istekleri önlemek için veritabanına gelen isteklerin sayısını azaltın.
2. Yüksek bir performans düzeyine veritabanına atayın.
3. Her sorgu kaynak kullanımını azaltmak için sorguları iyileştirin. Daha fazla bilgi için Azure SQL Database performans rehberi makaledeki sorgu ayarlama/Hinting bölümüne bakın.

## <a name="enforcement-of-limits"></a>Sınırlarının zorlama
Kaynaklar CPU, bellek, günlük g/ç ve veri g/ç dışında sınırlara ulaşıldığında, yeni istekleri vermeyerek uygulanır. Bir veritabanı yapılandırılan boyut sınırına ulaştığında seçer ve silme çalışmaya devam ederken ekler ve veri boyutunu artırın güncelleştirmeler başarısız olur. İstemcileri alır bir [hata iletisi](sql-database-develop-error-messages.md) ulaşıldı sınırı bağlı olarak.

Örneğin, bir SQL veritabanına bağlantı sayısı ve işlenebilir eşzamanlı istek sayısı sınırlıdır. SQL veritabanı bağlantı havuzunu desteklemek için eşzamanlı istek sayısından büyük olması için veritabanı bağlantı sayısını sağlar. Kullanılabilir bağlantı sayısı uygulama tarafından kolayca denetlenebilir olsa da, paralel istekler genellikle sürelerini tahmin etmek için ve denetlemek için daha zor sayısıdır. Ya da gönderir, kaynak çok fazla istek ya da veritabanı ulaştığında uygulama sınırlar ve uzun çalışan sorguları nedeniyle çalışan iş parçacığı piling başladığında özellikle yoğun yükleri sırasında hatalarla karşılaştı.

## <a name="service-tiers-and-performance-levels"></a>Hizmet katmanları ve performans düzeyleri
Hizmet katmanları ve performans düzeyleri tek veritabanı ve esnek havuzlar için vardır.

### <a name="single-databases"></a>Tek veritabanları
Tek bir veritabanı için bir veritabanı sınırları veritabanının Hizmet katmanını ve performans düzeyine göre tanımlanır. Aşağıdaki tabloda, performans düzeyleri değişen en temel, standart, Premium ve Premium RS veritabanları özelliklerini açıklar.

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

> [!IMPORTANT]
> P11 ve P15 performans düzeyleri kullanan müşteriler, ek ücret ödemeden en fazla 4 TB dahil depolama kullanabilirsiniz. Bu 4 TB seçenek aşağıdaki bölgelerde şu anda kullanılabilir: BİZE East2, Batı ABD, BİZE kamu Virginia, Batı Avrupa, Orta Almanya, Güney Doğu Asya, Japonya Doğu, Avustralya Doğu, Kanada merkezi ve Doğu Kanada.
>

### <a name="elastic-pools"></a>Esnek havuzlar
[Esnek havuzlar](sql-database-elastic-pool.md) kaynakları havuzdaki veritabanları arasında paylaşın. Aşağıdaki tabloda temel, standart, Premium ve Premium RS esnek havuzlar özelliklerini açıklar.

[!INCLUDE [SQL DB service tiers table for elastic databases](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

İçin bir genişletilmiş tanımı önceki tablolarda listelenen her bir kaynağın açıklamalarına bakın [hizmet katmanı özellikleri ve sınırları](sql-database-performance-guidance.md#service-tier-capabilities-and-limits). Hizmet katmanları genel bakış için bkz: [Azure SQL Database hizmet katmanları ve performans düzeyleri](sql-database-service-tiers.md).

## <a name="other-sql-database-limits"></a>Diğer SQL veritabanı sınırları
| Alan | Sınır | Açıklama |
| --- | --- | --- |
| Abonelik başına otomatik verme kullanılarak veritabanları |10 |Otomatik dışarı aktarma, SQL veritabanlarını yedekleme için özel bir zamanlama oluşturmanıza olanak sağlar. Bu özellik Önizleme 1 Mart 2017 sona erer.  |
| Sunucu başına veritabanları |En fazla 5000 |Sunucu başına en fazla 5000 veritabanları izin verilir. |
| Sunucu başına Dtu'lar |45000 |45000 Dtu'lar, bağımsız veritabanları ve esnek havuzlar sağlamak için sunucu başına izin verilir. Tek başına veritabanı ve sunucu başına izin verilen havuzları toplam sayısı yalnızca sunucu Dtu'lar sayısıyla sınırlıdır.  

> [!IMPORTANT]
> Azure SQL veritabanı otomatik dışarı aktarma Önizleme'de sunulmuştur ve 1 Mart 2017 üzerinde kullanımdan kaldırılacaktır. 1. aralık 2016'dan başlayarak, artık otomatik dışarı aktarma üzerinde herhangi bir SQL veritabanına yapılandırmanız mümkün olmayacaktır. Tüm var olan işleri 1 Mart 2017 kadar çalışmaya devam edecek verme otomatik. 1. aralık 2016'dan sonra kullanabileceğiniz [uzun vadeli yedekleme bekletme](sql-database-long-term-retention.md) veya [Azure Otomasyonu](../automation/automation-intro.md) SQL arşivlemek için veritabanları düzenli aralıklarla PowerShell tercih ettiğiniz bir zamanlamaya göre düzenli aralıklarla kullanarak. Bir örnek komut dosyası için indirdiğiniz [örnek komut dosyası github'dan](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export).
>


## <a name="resources"></a>Kaynaklar
[Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md)

[Azure SQL Database hizmet katmanları ve performans düzeyleri](sql-database-service-tiers.md)

[SQL Veritabanı istemci programları için hata iletileri](sql-database-develop-error-messages.md)
