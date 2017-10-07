---
title: "SQL Veritabanı: DTU nedir? | Microsoft Belgeleri"
description: "Azure SQL Veritabanı işlem biriminin ne olduğunu anlama."
keywords: "veritabanı seçenekleri,veritabanı performansı"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: CarlRabeler
ms.assetid: 89e3e9ce-2eeb-4949-b40f-6fc3bf520538
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 04/13/2017
ms.author: carlrab
ms.openlocfilehash: ba1fe580b32826259edaf6c8dc124faaf5b3d234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="explaining-database-transaction-units-dtus-and-elastic-database-transaction-units-edtus"></a>Veritabanı İşlem Birimlerini (DTU'lar) ve esnek Veritabanı İşlem Birimlerini (eDTU'lar) açıklama
Bu makalede, veritabanı işlem birimleri (Dtu'lar) ve esnek veritabanı işlem birimleri (Edtu'lar) ve, isabet ne olur maksimum Dtu veya Edtu'lar hello açıklanmaktadır.  

## <a name="what-are-database-transaction-units-dtus"></a>Veritabanı İşlem Birimleri (DTU'lar) nedir?
Belirli bir performans düzeyinde içinde tek bir Azure SQL veritabanı için bir [hizmet katmanı](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels), Microsoft Kaynak veritabanı için belirli bir düzeyde (başka bir veritabanında bulunan hello Azure bulut bağımsız) garanti ve sağlayarak bir tahmin edilebilir performans düzeyi. Bu miktarda kaynak veritabanı işlem birimleri veya Dtu'lar sayısı olarak hesaplanır ve CPU, bellek, g/ç (veri ve işlem günlüğü g/ç) karışık ölçüsüdür. Bu kaynaklar arasında Hello oranı tarafından ilk olarak belirlendi bir [OLTP Kıyaslama iş yükü](sql-database-benchmark-overview.md) toobe gerçek OLTP iş yükü tipik tasarlanmıştır. İş yükünüzün hello miktarını bu kaynakları aştığında, üretilen iş daraltılmış - yavaş performans ve zaman aşımları sonuç. İş yükünüzün kullandığı hello kaynakları hello kaynakları kullanılabilir tooother SQL veritabanlarında hello Azure bulut etkilemeyen ve diğer iş yükleri tarafından kullanılan hello kaynak hello kaynakları kullanılabilir tooyour SQL veritabanını etkileyen değil.

![sınırlama kutusu](./media/sql-database-what-is-a-dtu/bounding-box.png)

Dtu'lar anlama hello göreli miktarını Azure SQL veritabanları farklı performans düzeyleri ve hizmet katmanları arasında kaynakları için en kullanışlıdır. Örneğin, bir veritabanı hello performans düzeyini artırarak hello Dtu'lar Katlama toodoubling hello kaynak kullanılabilir toothat veritabanı kümesi karşılık gelir. Örneğin, 1750 DTU’ya sahip Premium P11 veritabanı 5 DTU’ya sahip Temel veritabanına göre 350 kat daha fazla DTU işlem gücü sağlıyor.  

iş yükü, kullanım hello (DTU) kaynak tüketimini daha derin anlayış toogain [Azure SQL veritabanı sorgu performansı öngörüleri](sql-database-query-performance.md) için:

- Potansiyel olarak performansı için ayarlanan süre/CPU/yürütme sayısı tarafından Hello en sık kullanılan sorguların tanımlayın. Örneğin, bir g/ç yoğun sorgusu hello kullanımından yararlanabilir [bellek içi iyileştirme tekniklerini](sql-database-in-memory.md) toomake daha iyi kullanımı hello kullanılabilir belleğin düzeyde belirli hizmet katmanını ve performans.
- Bir sorgu hello ayrıntılarını detaya, metin ve kaynak kullanımı geçmişini görüntüleyin.
- Erişim performans tarafından gerçekleştirilen eylemler Göster önerileri ayarlama [SQL veritabanı Danışmanı'nı](sql-database-advisor.md).

Yapabilecekleriniz [hizmet katmanları değiştirmek](sql-database-service-tiers.md) (genellikle altında dört saniye ortalaması) en düşük kapalı kalma tooyour uygulamayla herhangi bir zamanda. Birçok işletme ve uygulama için mümkün toocreate veritabanları olmasına ve özellikle kullanım desenlerini nispeten tahmin edilebilir yeterince ise performans yukarı veya aşağı isteğe bağlı arama. Ancak tahmin edilemeyen kullanım biçimlerine sahipseniz, bunu sabit toomanage maliyetleri ve iş modelinizin yapabilirsiniz. Bu senaryoda, belirli bir hello havuzdaki birden fazla veritabanı arasında paylaşılan Edtu sayısı ile bir esnek havuz kullanın.

![Giriş tooSQL veritabanı: tek veritabanı Dtu'lar katmanı ve düzeyi](./media/sql-database-what-is-a-dtu/single_db_dtus.png)

## <a name="what-are-elastic-database-transaction-units-edtus"></a>Esnek Veritabanı İşlem Birimleri (eDTU'lar) nedir?
Bunun yerine kaynakları (Dtu'lar) tooa her zaman gerekmeyen olup olmadığını bağımsız olarak, kullanılabilir SQL veritabanı ayrılmış bir dizi sağlamak daha veritabanlarına yerleştireceğiniz bir [esnek havuz](sql-database-elastic-pool.md) bir SQL veritabanı sunucusunda kaynak havuzu paylaşır Bu veritabanı arasında. Merhaba paylaşılan kaynakları bir esnek havuzdaki esnek veritabanı işlem birimleri veya Edtu ölçülür. Esnek havuzlar toomanage hello performans hedeflerini birden çok yaygın olarak değişen sahip veritabanları ve tahmin edilemeyen kullanım biçimlerine için basit ve uygun maliyetli bir çözüm sağlar. Bir esnek havuz tek veritabanı hello kaynakların tümünü kullanan garanti edebilir hello havuzda olduğunu ve ayrıca en az miktarda kaynak her zaman kullanılabilir tooa esnek havuzdaki veritabanıdır. Bkz: [esnek havuzlar](sql-database-elastic-pool.md) daha fazla bilgi için.

![Giriş tooSQL veritabanı: katmanı ve düzeyi tarafından Edtu](./media/sql-database-what-is-a-dtu/sqldb_elastic_pools.png)

Havuza belirli bir fiyat karşılığında, belirli bir sayıda eDTU verilir. Merhaba esnek havuz tek veritabanlarını hello esneklik tooauto ölçekli yapılandırılmış hello sınırları içinde verilir. Hafif yükleri altındaki veritabanları daha az veritabanları hiçbir yük altında hiçbir Edtu'lar tüketen toohello noktası yukarı tüketmesine sırada ağır yük altında daha fazla Edtu'lar toomeet isteğe bağlı bir veritabanı kullanabilir. Merhaba tüm havuz için kaynak sağlama tarafından yerine veritabanı başına yönetim görevleri basitleştirilmiştir ve hello havuzu için tahmin edilebilir bir bütçe vardır.

Ek Edtu'lar tooan varolan havuzu hiçbir etkisi olmadan hiçbir veritabanı kapalı kalma süresi ile Merhaba veritabanlarında hello havuzunda eklenebilir. Benzer şekilde, ek eDTU’lara artık ihtiyaç yoksa bunlar mevcut bir havuzdan ne zaman isterseniz kaldırılabilir. Eklemek veya veritabanlarını toohello havuzu çıkarmak veya sınırı hello Edtu'lar bir veritabanı miktarını ağır yük tooreserve Edtu'lar altında diğer veritabanları için kullanabilirsiniz. Bir veritabanı beklendiği altında-kullanılarak durumdaysa kaynakları hello havuzu dışında taşıyın ve tahmin edilebilir miktarda kaynak gerektirdiği tek bir veritabanı olarak yapılandırın.

## <a name="how-can-i-determine-hello-number-of-dtus-needed-by-my-workload"></a>My iş yükü tarafından gerekli Dtu'lar hello sayısını nasıl belirleyebilirim?
Toomigrate mevcut şirket içi veya SQL Server sanal makine iş yükü tooAzure SQL veritabanı arıyorsanız, hello kullanabilirsiniz [DTU Hesaplayıcıyı](http://dtucalculator.azurewebsites.net/) tooapproximate hello gerekli Dtu'lar sayısı. Bir mevcut Azure SQL veritabanı iş yükü için kullandığınız [SQL veritabanı sorgu performansı öngörüleri](sql-database-query-performance.md) toounderstand, veritabanı kaynak tüketimi (Dtu'lar) tooget daha derin bir anlayış nasıl toooptimize, iş yükü. Merhaba de kullanabilirsiniz [sys.dm_db_ resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) DMV tooget hello kaynak tüketimi bilgileri hello için son bir saat. Alternatif olarak, katalog görünümünü hello [sys.resource_stats](http://msdn.microsoft.com/library/dn269979.aspx) ayrıca olması sorgulanan tooget hello aynı veri hello son 14 gün için bir alt doğruluğu beş dakikalık ortalamalar, ancak en.

## <a name="how-do-i-know-if-i-could-benefit-from-an-elastic-pool-of-resources"></a>Esnek bir kaynak havuzundan fayda sağlayıp sağlayamayacağımı nasıl öğrenebilirim?
Havuzlar, belirli kullanım düzenlerine sahip çok sayıda veritabanı bulunan durumlar için uygundur. Söz konusu kullanım düzeni, belirli bir veritabanı için ortalama düşük düzeyde kullanım ile nispeten nadir zamanlarda kullanımın ani olarak artması şeklindedir. SQL veritabanı otomatik olarak varolan bir SQL veritabanı sunucusuna veritabanlarında hello geçmiş kaynak kullanımını değerlendirir ve hello Azure portal hello uygun havuzu yapılandırması önerir. Daha fazla bilgi için bkz. [ne zaman elastik bir havuz kullanılması gerekir?](sql-database-elastic-pool.md)

## <a name="what-happens-when-i-hit-my-maximum-dtus"></a>Maksimum DTU sayıma ulaştığımda ne olur?
Performans düzeyleri ayarlandığından ve yönetilen tooprovide hello kaynakları toorun veritabanının yükünüzü toohello max sınırları, seçili hizmet katmanı/performans düzeyini izin yukarı gerekli. İş yükünüzün CPU/Data GÇ/günlük GÇ sınırları hello sınırları basarsa, hello izin verilen en yüksek düzeyde tooreceive hello kaynakları devam, ancak sorgularınızı artan büyük olasılıkla toosee gecikmeleri olduğunuz. Merhaba yavaşlama sorguları zamanlama başlar, bu nedenle önemli hale sürece bu sınırları hataları, ancak yerine yavaşlama hello iş yükü içinde neden değil. İzin verilen en yüksek eş zamanlı kullanıcı oturumu/isteği (çalışan iş parçacıkları) sayısı sınırına ulaşırsanız açık hatalar görürsünüz. CPU, bellek, veri G/Ç ve işlem günlüğü G/Ç kaynakları dışındaki kaynaklara yönelik sınırlar hakkında bilgi edinmek için bkz. [Azure SQL Database resource limits](sql-database-resource-limits.md) (Azure SQL Veritabanı kaynak sınırları).

## <a name="next-steps"></a>Sonraki adımlar
* Bkz: [hizmet katmanı](sql-database-service-tiers.md) hello Dtu ve Edtu tek veritabanları ve esnek havuzlar için kullanılabilir hakkında bilgi için.
* CPU, bellek, veri G/Ç ve işlem günlüğü G/Ç kaynakları dışındaki kaynaklara yönelik sınırlar hakkında bilgi edinmek için bkz. [Azure SQL Database resource limits](sql-database-resource-limits.md) (Azure SQL Veritabanı kaynak sınırları).
* Bkz: [SQL veritabanı sorgu performansı öngörüleri](sql-database-query-performance.md) toounderstand (Dtu'lar) tüketim.
* Bkz: [SQL veritabanı Kıyaslama genel bakış](sql-database-benchmark-overview.md) toounderstand hello Metodoloji hello OLTP Kıyaslama iş yükü arkasında kullanılan DTU blend toodetermine hello.
