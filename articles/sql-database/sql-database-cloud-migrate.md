---
title: "aaaSQL sunucu veritabanı geçiş tooAzure SQL veritabanı | Microsoft Docs"
description: "Ne dersiniz SQL Server veritabanı geçiş tooAzure hello bulut SQL veritabanında öğrenin. Veritabanı Geçiş Araçları tootest uyumluluk önceki toodatabase geçişi kullanın."
keywords: "veritabanı geçişi,sql server veritabanı geçişi,veritabanı taşıma araçları,veritabanı taşıma,sql veritabanı geçişi"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 9cf09000-87fc-4589-8543-a89175151bc2
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sqldb-migrate
ms.date: 02/08/2017
ms.author: carlrab
ms.openlocfilehash: 3a5e879404dd2da1dd5254a6134e3ee1517648db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-database-migration-toosql-database-in-hello-cloud"></a>SQL Server veritabanı geçiş tooSQL hello bulut veritabanında
Bu makalede, SQL Server 2005 veya üzeri veritabanı tooAzure SQL veritabanı geçiş başlıca iki yöntem hakkında hello öğrenin. Merhaba ilk yöntem basittir ancak bazıları gerektirir hello geçiş sırasında büyük olasılıkla önemli kapalı kalma süresi. Merhaba ikinci yöntem daha karmaşıktır, ancak önemli ölçüde hello geçiş sırasında kapalı kalma süresini ortadan kaldırır.

Her iki durumda da ihtiyacınız tooensure hello kaynak veritabanının hello kullanarak Azure SQL veritabanı ile uyumlu olan [veri geçiş Yardımcısı (DMA)](https://www.microsoft.com/download/details.aspx?id=53595). SQL Database V12 yaklaşan [özellik eşliği](sql-database-features.md) sorunları ilgili tooserver düzeyi ve veritabanları arası işlemleri dışında SQL Server ile. Veritabanları ve kullanan uygulamalar [kısmen desteklenen veya desteklenmeyen işlevler](sql-database-transact-sql-information.md) bazı gereksinim [toofix yeniden mühendislik Bu uyumsuzluklar](sql-database-cloud-migrate.md#resolving-database-migration-compatibility-issues) hello önce SQL Server veritabanı geçirilebilir.

> [!NOTE]
> toomigrate bkz: Microsoft Access, Sybase, MySQL Oracle ve DB2 tooAzure SQL veritabanı dahil olmak üzere bir SQL Server veritabanı [SQL Server Geçiş Yardımcısı](https://blogs.msdn.microsoft.com/datamigration/2016/12/22/released-sql-server-migration-assistant-ssma-v7-2/).
> 

## <a name="method-1-migration-with-downtime-during-hello-migration"></a>Yöntem 1: Geçiş kapalı kalma süresi ile Merhaba geçiş sırasında

 Veritabanının kapalı kalması kabul edilebilir bir durumsa veya ileride geçiş yapmak üzere bir üretim veritabanının test geçişini gerçekleştiriyorsanız bu yöntemi kullanın. Bir öğretici için bkz: [bir SQL Server veritabanını geçirme](sql-database-migrate-your-sql-server-database.md).

Merhaba aşağıdaki listede hello bu yöntemi kullanarak SQL Server veritabanı geçiş için genel iş akışını içerir.

  ![VSSSDT geçiş şeması](./media/sql-database-cloud-migrate/azure-sql-migration-sql-db.png)

1. Merhaba veritabanı hello en son sürümünü kullanarak uyumluluk için değerlendirecek [veri geçiş Yardımcısı (DMA)](https://www.microsoft.com/download/details.aspx?id=53595).
2. Transact-SQL betikleri halinde tüm gerekli düzeltmeleri hazırlayın.
3. Merhaba kaynak veritabanı işlemsel olarak tutarlı bir kopyasını geçirilmekte - ve olun toohello kaynak veritabanının daha fazla değişiklik yapılan (veya hello geçiş tamamlandıktan sonra bu değişiklikleri el ile uygulayabilirsiniz). İstemci bağlantısı toocreating devre dışı bırakma bir veritabanından, birçok yöntemleri tooquiesce olan bir [veritabanı anlık görüntüsü](https://msdn.microsoft.com/library/ms175876.aspx).
4. Merhaba Transact-SQL betikleri tooapply hello düzeltmeleri toohello veritabanı kopyası dağıtın.
5. [Dışarı aktarma](sql-database-export.md) veritabanı kopyası tooa hello. Bir yerel sürücüde BACPAC dosyası.
6. [İçeri aktarma](sql-database-import.md) hello. Birkaç BACPAC birini kullanarak yeni bir Azure SQL veritabanı olarak BACPAC dosyasını araçları, aracı en iyi performans için önerilen hello olan SQLPackage.exe ile aktarın.

### <a name="optimizing-data-transfer-performance-during-migration"></a>Geçiş sırasında veri aktarımı performansını en iyi duruma getirme 

liste aşağıdaki hello hello içeri aktarma işlemi sırasında en iyi performans için öneriler içerir.

* Merhaba yüksek hizmet düzeyi ve performans katmanı bütçenizi toomaximize hello aktarımı performans sağlayan seçin. Toosave para Hello geçiş tamamlandıktan sonra ölçeklendirebilirsiniz. 
* Merhaba arasındaki uzaklığı en aza indirmek için. BACPAC dosya ve hello hedef veri merkezi.
* Geçiş sırasında otomatik istatistikleri devre dışı bırakma
* Tabloları ve dizinleri bölümleme
* Dizini oluşturulmuş görünümleri bırakma ve tamamlandıktan sonra yeniden oluşturma
* Nadiren sorgulanan geçmiş verileri tooanother veritabanını kaldırın ve bu geçmiş verileri tooa ayrı Azure SQL veritabanını geçirme. Daha sonra bu geçmiş verileri [esnek sorgular](sql-database-elastic-query-overview.md) kullanarak sorgulayabilirsiniz.

### <a name="optimize-performance-after-hello-migration-completes"></a>Merhaba geçiş tamamlandıktan sonra performansı en iyi duruma getirme

[İstatistikleri güncelleştirme](https://msdn.microsoft.com/library/ms187348.aspx) hello geçiş tamamlandıktan sonra tam tarama ile.

## <a name="method-2-use-transactional-replication"></a>Yöntem 2: İşlem Çoğaltma Kullanma

Merhaba geçiş yapılırken, tooremove, SQL Server veritabanınızın üretimden göze alamıyorsanız, SQL Server işlem çoğaltma geçiş çözümü olarak kullanabilirsiniz. Bu yöntem, hello kaynak veritabanı gerekir toouse karşılayan hello [işlemsel çoğaltma gereksinimlerini](https://msdn.microsoft.com/library/mt589530.aspx) ve Azure SQL veritabanı için uyumlu. AlwaysOn SQL çoğaltma hakkında daha fazla bilgi için bkz: [Always On kullanılabilirlik grupları (SQL Server) için çoğaltma yapılandırma](/sql/database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server).

toouse Bu çözüm toomigrate istediğiniz bir abone toohello SQL Server örneği olarak Azure SQL veritabanınıza yapılandırın. Merhaba işlemsel çoğaltma dağıtıcı eşitler eşitlenen hello veritabanı toobe (Merhaba yayımcı) verilerden oluşan yeni bir işlem devam ederken. 

İşlemsel tüm değişiklikleri tooyour veri veya şema görünmesini Azure SQL veritabanı'nda. Merhaba eşitleme tamamlandıktan sonra hazır toomigrate olan, uygulamaları toopoint hello bağlantı dizesini değiştirmek bunları tooyour Azure SQL veritabanı. Sol herhangi bir değişiklik işlemsel çoğaltma boşaltır sonra kaynak veritabanını ve tüm uygulamalarınızı tooAzure DB noktası, işlemsel çoğaltma kaldırabilirsiniz. Azure SQL Veritabanınız artık üretim sisteminizdir.

 ![SeedCloudTR diyagramı](./media/sql-database-cloud-migrate/SeedCloudTR.png)

> [!TIP]
> İşlemsel çoğaltma toomigrate Kaynak veritabanınıza kümesini de kullanabilirsiniz. Merhaba yayın tooAzure SQL veritabanı çoğaltma sınırlı tooa alt çoğaltılmasını hello veritabanındaki hello tabloların olabilir. Çoğaltılmasını her tablo için hello veri tooa satırların alt kümesini hello ve/veya hello bir sütun alt kümesini sınırlayabilirsiniz.
>

### <a name="migration-toosql-database-using-transaction-replication-workflow"></a>Geçiş tooSQL işlem çoğaltma iş akışını kullanarak veritabanı

> [!IMPORTANT]
> Merhaba en son sürümünü kullanın SQL Server Management Studio tooremain Azure ve SQL veritabanı güncelleştirmeleri tooMicrosoft ile eşitlenmiş. SQL Server Management Studio’nun eski sürümleri, SQL Veritabanını abone olarak ayarlayamaz. [SQL Server Management Studio’yu güncelleyin](https://msdn.microsoft.com/library/mt238290.aspx).
> 

1. Dağıtımı Ayarlama
   -  [SQL Server Management Studio (SSMS) kullanma](https://msdn.microsoft.com/library/ms151192.aspx#Anchor_1)
   -  [Transact-SQL kullanma](https://msdn.microsoft.com/library/ms151192.aspx#Anchor_2)
2. Yayın Oluşturma
   -  [SQL Server Management Studio (SSMS) kullanma](https://msdn.microsoft.com/library/ms151160.aspx#Anchor_1)
   -  [Transact-SQL kullanma](https://msdn.microsoft.com/library/ms151160.aspx#Anchor_2)
3. Abonelik Oluşturma
   -  [SQL Server Management Studio (SSMS) kullanma](https://msdn.microsoft.com/library/ms152566.aspx#Anchor_0)
   -  [Transact-SQL kullanma](https://msdn.microsoft.com/library/ms152566.aspx#Anchor_1)

### <a name="some-tips-and-differences-for-migrating-toosql-database"></a>Bazı ipuçları ve geçiş farklar tooSQL veritabanı

1. Yerel dağıtıcı kullanma 
   - Bu, hello sunucuda performans düşüşüne neden olur. 
   - Merhaba performans etkisi kabul edilebilir değilse, başka bir sunucu kullanabilirsiniz ancak yönetimi ve yönetim karmaşıklığını ekler.
2. Anlık görüntü klasörü, seçtiğiniz yapma emin hello klasör seçerek büyüklükte toohold BCP her tablonun olduğunda tooreplicate istiyor. 
3. Anlık görüntü oluşturma kilit işlemi tamamlanana kadar ilişkili tabloları Merhaba, bu nedenle, anlık görüntü zamanlamasının. 
4. Azure SQL Veritabanında yalnızca iletme abonelikleri desteklenir. Yalnızca hello kaynak veritabanından aboneler ekleyebilirsiniz.

## <a name="resolving-database-migration-compatibility-issues"></a>Veritabanı geçişi uyumluluk sorunlarını çözme
Çok çeşitli, hem de SQL Server sürümü hello hello kaynak veritabanı ve hello karmaşıklığı geçirdiğiniz hello veritabanının bağlı olarak, karşılaşabileceğiniz uyumluluk sorunları vardır. Eski SQL Server sürümlerinde daha fazla uyumluluk sorunları algılanabilir. Kaynakları aşağıdaki hello kullanın, ayrıca, arama motoru seçenekleri kullanarak Internet arama tooa hedeflenen:

* [Azure SQL Veritabanında desteklenmeyen SQL Server veritabanı özellikleri](sql-database-transact-sql-information.md)
* [SQL Server 2016'da Artık Sağlanmayan Veritabanı Altyapısı İşlevleri](https://msdn.microsoft.com/library/ms144262%28v=sql.130%29)
* [SQL Server 2014'te Artık Sağlanmayan Veritabanı Altyapısı İşlevleri](https://msdn.microsoft.com/library/ms144262%28v=sql.120%29)
* [SQL Server 2012'de Artık Sağlanmayan Veritabanı Altyapısı İşlevleri](https://msdn.microsoft.com/library/ms144262%28v=sql.110%29)
* [SQL Server 2008 R2'de Artık Sağlanmayan Veritabanı Altyapısı İşlevleri](https://msdn.microsoft.com/library/ms144262%28v=sql.105%29)
* [SQL Server 2005'te Artık Sağlanmayan Veritabanı Altyapısı İşlevleri](https://msdn.microsoft.com/library/ms144262%28v=sql.90%29)

Ayrıca toosearching Internet hello ve bu kaynakları kullanarak hello [MSDN SQL Server topluluk forumları](https://social.msdn.microsoft.com/Forums/sqlserver/home?category=sqlserver) veya [StackOverflow](http://stackoverflow.com/).

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba betiği hello Azure SQL EMEA mühendisleri blogunda çok kullan[geçiş sırasında tempdb kullanımı izlemek](https://blogs.msdn.microsoft.com/azuresqlemea/2016/12/28/lesson-learned-10-monitoring-tempdb-usage/).
* Merhaba betiği hello Azure SQL EMEA mühendisleri blogunda çok kullan[geçiş yapılırken hello işlem günlüğü alanı veritabanınızın izlemek](https://blogs.msdn.microsoft.com/azuresqlemea/2016/10/31/lesson-learned-7-monitoring-the-transaction-log-space-of-my-database/0).
* BACPAC dosyalarını kullanarak bir SQL Server Müşteri danışma ekibi blogu geçirme hakkında bkz [SQL BACPAC dosyalarını kullanarak veritabanını SQL Server tooAzure geçiş](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* Geçişten sonra UTC saati ile çalışma hakkında daha fazla bilgi için bkz: [için yerel saat dilimini değiştirme hello varsayılan saat dilimini](https://blogs.msdn.microsoft.com/azuresqlemea/2016/07/27/lesson-learned-4-modifying-the-default-time-zone-for-your-local-time-zone/).
* Geçişten sonra bir veritabanı hello varsayılan dilini değiştirme hakkında daha fazla bilgi için bkz: [nasıl toochange hello Azure SQL veritabanı'nın varsayılan dil](https://blogs.msdn.microsoft.com/azuresqlemea/2017/01/13/lesson-learned-16-how-to-change-the-default-language-of-azure-sql-database/).


