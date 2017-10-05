---
title: "Azure SQL Database Transact-SQL ile için coğrafi çoğaltma yapılandırma | Microsoft Docs"
description: "Coğrafi çoğaltma Transact-SQL kullanarak Azure SQL veritabanı için yapılandırma"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d94d89a6-3234-46c5-8279-5eb8daad10ac
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: carlrab
ms.openlocfilehash: e5011c1c67e051616d53621b72e46ba894ca3c02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-with-transact-sql"></a>Aktif coğrafi çoğaltma Transact-SQL ile Azure SQL veritabanı için yapılandırma

Bu makalede Transact-SQL ile bir Azure SQL veritabanı için etkin coğrafi çoğaltma yapılandırma gösterilmektedir.

Transact-SQL kullanarak yük devretme başlatmak için bkz: [Transact-SQL ile Azure SQL veritabanı için planlanmış veya planlanmamış bir yük devretme başlatın](sql-database-geo-replication-failover-transact-sql.md).

> [!NOTE]
> Olağanüstü durum kurtarma için etkin coğrafi çoğaltma (okunabilir ikinciller) kullandığınızda, otomatik ve şeffaf yük devretme etkinleştirmek için bir uygulamadaki tüm veritabanları için bir yük devretme grubu yapılandırmanız gerekir. Bu özelliğin önizlemede değil. Daha fazla bilgi için bkz: [otomatik yük devretme grupları ve coğrafi çoğaltma](sql-database-geo-replication-overview.md).
> 
> 

Aktif coğrafi çoğaltma yapılandırmak için Transact-SQL kullanarak, aşağıdakiler gerekir:

* Bir Azure aboneliği
* Mantıksal bir Azure SQL veritabanı sunucusu <MyLocalServer> ve bir SQL veritabanı <MyDB> -çoğaltmak istediğiniz birincil veritabanı
* Bir veya daha fazla mantıksal Azure SQL veritabanı sunucularının < MySecondaryServer(n) > - ikincil veritabanları oluşturacağınız partner sunucuları olacaktır mantıksal sunucu
* Birincil DBManager olan bir oturum açma
* Coğrafi replicate olacak yerel veritabanı db_ownership sahip
* Coğrafi çoğaltma yapılandıracak partner sunucuları üzerinde DBManager olabilir
* SQL Server Management Studio (SSMS) en yeni sürümü

> [!IMPORTANT]
> Microsoft Azure ve SQL Veritabanı güncelleştirmeleriyle aynı sürümde olmak için her zaman en güncel Management Studio sürümünü kullanmanız önerilir. [SQL Server Management Studio’yu güncelleyin](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

## <a name="add-secondary-database"></a>İkincil veritabanı Ekle
Kullanabileceğiniz **ALTER DATABASE** deyimi bir iş ortağı sunucusunda coğrafi olarak çoğaltılmış ikincil bir veritabanı oluşturun. Çoğaltılacak veritabanını içeren sunucunun ana veritabanı üzerinde bu deyimini yürütün. Coğrafi olarak çoğaltılmış veritabanı ("birincil veritabanı") çoğaltılmasını veritabanı ile aynı ada sahip olur ve varsayılan olarak, birincil veritabanı olarak aynı hizmet düzeyine sahip olacaktır. İkincil veritabanını okunabilir veya okunabilir olmayan olabilir ve tek veritabanı olabilir veya esnek havuzdaki. Daha fazla bilgi için bkz: [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) ve [hizmet katmanları](sql-database-service-tiers.md).
İkincil veritabanını oluşturulan ve dağıtılan sonra verileri zaman uyumsuz olarak birincil veritabanından çoğaltmaya başlar. Aşağıdaki adımlar coğrafi çoğaltma yapılandırılması anlatılmaktadır Management Studio'yu kullanarak. Okunabilir olmayan ve okunabilir ikincil kopya, tek bir veritabanı olarak veya bir esnek havuz oluşturmak için adımlar verilmiştir.

> [!NOTE]
> Belirtilen iş ortağı sunucusunda birincil veritabanı ile aynı adda bir veritabanı zaten varsa komut başarısız olur.
> 

### <a name="add-readable-secondary-single-database"></a>Okunabilir ikincil (tek veritabanı) Ekle
Tek bir veritabanı olarak okunabilir ikincil kopya oluşturmak için aşağıdaki adımları kullanın.

1. Management Studio'da Azure SQL Database mantıksal sunucunuza bağlanın.
2. Veritabanları klasörünü açın, **sistem veritabanları** klasörünü sağ tıklatın **ana**ve ardından **yeni sorgu**.
3. Aşağıdaki **ALTER DATABASE** deyimi yerel bir veritabanı bir coğrafi çoğaltma birincil ikincil bir sunucu üzerinde okunabilir ikincil veritabanına sahip olun.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer2> WITH (ALLOW_CONNECTIONS = ALL);
4. Sorguyu çalıştırmak için **Yürüt**'e tıklayın.

### <a name="add-readable-secondary-elastic-pool"></a>Okunabilir ikincil (esnek havuz) Ekle
Okunabilir ikincil bir esnek havuz oluşturmak için aşağıdaki adımları kullanın.

1. Management Studio'da Azure SQL Database mantıksal sunucunuza bağlanın.
2. Veritabanları klasörünü açın, **sistem veritabanları** klasörünü sağ tıklatın **ana**ve ardından **yeni sorgu**.
3. Aşağıdaki **ALTER DATABASE** deyimi yerel bir veritabanı bir coğrafi çoğaltma birincil ikincil sunucuda esnek havuzdaki okunabilir ikincil veritabanına sahip olun.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer4> WITH (ALLOW_CONNECTIONS = ALL
           , SERVICE_OBJECTIVE = ELASTIC_POOL (name = MyElasticPool2));
4. Sorguyu çalıştırmak için **Yürüt**'e tıklayın.

## <a name="remove-secondary-database"></a>İkincil veritabanını Kaldır
Kullanabileceğiniz **ALTER DATABASE** kalıcı olarak ikincil bir veritabanı ve birincil arasındaki çoğaltma ortaklığı sonlandırmak için deyimi. Bu bildirimi birincil veritabanının bulunduğu ana veritabanı üzerinde yürütülür. İlişki sonlandırma sonra ikincil veritabanını normal okuma-yazma veritabanı haline gelir. İkincil veritabanına bağlantı bozuk ise, komut başarılı olur, ancak bağlantı geri yüklendikten sonra ikincil okuma-yazma olacaktır. Daha fazla bilgi için bkz: [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) ve [hizmet katmanları](sql-database-service-tiers.md).

Coğrafi olarak çoğaltılmış ikincil bir coğrafi çoğaltma ortaklığı kaldırmak için aşağıdaki adımları kullanın.

1. Management Studio'da Azure SQL Database mantıksal sunucunuza bağlanın.
2. Veritabanları klasörünü açın, **sistem veritabanları** klasörünü sağ tıklatın **ana**ve ardından **yeni sorgu**.
3. Aşağıdaki **ALTER DATABASE** coğrafi olarak çoğaltılmış ikincil kaldırmak için deyimi.
   
        ALTER DATABASE <MyDB>
           REMOVE SECONDARY ON SERVER <MySecondaryServer1>;
4. Sorguyu çalıştırmak için **Yürüt**'e tıklayın.

## <a name="monitor-active-geo-replication-configuration-and-health"></a>Aktif coğrafi çoğaltma yapılandırma ve sistem durumu izleme

Coğrafi çoğaltma yapılandırmasını izleme ve veri çoğaltma durumunu izleme izleme görevlerini içerir.  Kullanabileceğiniz **sys.dm_geo_replication_links** dinamik yönetim görünümünü Azure SQL Database mantıksal sunucusunda her veritabanı için mevcut tüm yineleme bağlantıları hakkında bilgi döndürmek için ana veritabanında. Bu görünüm, her birincil ve ikincil veritabanları arasındaki çoğaltma bağlantısı için bir satır içerir. Kullanabileceğiniz **sys.dm_replication_link_status** dinamik yönetim görünümünü şu anda bir çoğaltma yinelemesi ilgilendiğini her Azure SQL veritabanı için bir satırı döndürür. Bu, hem birincil hem de ikincil veritabanlarını içerir. Birden fazla sürekli çoğaltma bağlantısı için belirli bir birincil veritabanı varsa, bu tablo her ilişki için bir satır içerir. Görünüm mantıksal asıl dahil olmak üzere tüm veritabanlarında oluşturulur. Ancak, bu görünümde mantıksal asıl sorgulama boş döndürür. Kullanabileceğiniz **sys.dm_operation_status** dinamik yönetim görünümünü tüm çoğaltma bağlantılarının durumunu da dahil olmak üzere operations veritabanı ilişkin durumunu gösterir. Daha fazla bilgi için bkz: [sys.geo_replication_links (Azure SQL veritabanı)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (Azure SQL veritabanı)](https://msdn.microsoft.com/library/mt575504.aspx), ve [sys.dm_operation_status (Azure SQL veritabanı)](https://msdn.microsoft.com/library/dn270022.aspx).

Aktif coğrafi çoğaltma ortaklığı izlemek için aşağıdaki adımları kullanın.

1. Management Studio'da Azure SQL Database mantıksal sunucunuza bağlanın.
2. Veritabanları klasörünü açın, **sistem veritabanları** klasörünü sağ tıklatın **ana**ve ardından **yeni sorgu**.
3. Coğrafi çoğaltma bağlantıları olan tüm veritabanları göstermek için şu deyimi kullanın.
   
        SELECT database_id, start_date, modify_date, partner_server, partner_database, replication_state_desc, role, secondary_allow_connections_desc FROM sys.geo_replication_links;
4. Sorguyu çalıştırmak için **Yürüt**'e tıklayın.
5. Veritabanları klasörünü açın, **sistem veritabanları** klasörünü sağ tıklatın **MyDB**ve ardından **yeni sorgu**.
6. Çoğaltma gecikmelere ve son çoğaltma göstermek için şu deyimi kullanın MyDB my ikincil veritabanları süresi.
   
        SELECT link_guid, partner_server, last_replication, replication_lag_sec FROM sys.dm_geo_replication_link_status
7. Sorguyu çalıştırmak için **Yürüt**'e tıklayın.
8. MyDB veritabanıyla ilişkili en son coğrafi çoğaltma işlemlerini göstermek için şu deyimi kullanın.
   
        SELECT * FROM sys.dm_operation_status where major_resource_id = 'MyDB'
        ORDER BY start_time DESC
9. Sorguyu çalıştırmak için **Yürüt**'e tıklayın.

## <a name="next-steps"></a>Sonraki adımlar
* Yük devretme grupları ve etkin coğrafi çoğaltma hakkında daha fazla bilgi için bkz: - [yük devretme grupları](sql-database-geo-replication-overview.md)
* İş sürekliliğine genel bakış ve senaryolar için bkz: [iş sürekliliğine genel bakış](sql-database-business-continuity.md)

