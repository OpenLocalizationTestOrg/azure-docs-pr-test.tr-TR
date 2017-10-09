---
title: "Azure SQL Database Transact-SQL ile için aaaConfigure coğrafi çoğaltma | Microsoft Docs"
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
ms.openlocfilehash: 295b6b12f257dfb15131d5ee28fbe65c6476352d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-with-transact-sql"></a>Aktif coğrafi çoğaltma Transact-SQL ile Azure SQL veritabanı için yapılandırma

Bu makale size nasıl gösterir tooconfigure etkin coğrafi çoğaltma için bir Azure SQL Database Transact-SQL ile.

Transact-SQL kullanarak tooinitiate yük devretme bkz [Transact-SQL ile Azure SQL veritabanı için planlanmış veya planlanmamış bir yük devretme başlatın](sql-database-geo-replication-failover-transact-sql.md).

> [!NOTE]
> Olağanüstü durum kurtarma için etkin coğrafi çoğaltma (okunabilir ikinciller) kullandığınızda, bir uygulama tooenable otomatik ve şeffaf yük devretme içindeki tüm veritabanları için bir yük devretme grubu yapılandırmanız gerekir. Bu özelliğin önizlemede değil. Daha fazla bilgi için bkz: [otomatik yük devretme grupları ve coğrafi çoğaltma](sql-database-geo-replication-overview.md).
> 
> 

tooconfigure etkin coğrafi çoğaltma Transact-SQL kullanarak hello aşağıdaki gerekir:

* Bir Azure aboneliği
* Mantıksal bir Azure SQL veritabanı sunucusu <MyLocalServer> ve bir SQL veritabanı <MyDB> -tooreplicate istediğiniz hello birincil veritabanı
* Bir veya daha fazla mantıksal Azure SQL veritabanı sunucularının < MySecondaryServer(n) > - ikincil veritabanları oluşturacağınız hello partner sunucuları olacaktır hello mantıksal sunucu
* Birincil hello DBManager olan bir oturum açma
* Coğrafi replicate olacak hello yerel veritabanı db_ownership sahip
* DBManager hello partner sunucuları toowhich üzerinde olmanız coğrafi çoğaltma yapılandırır
* Merhaba en yeni sürümü SQL Server Management Studio (SSMS)

> [!IMPORTANT]
> Her zaman hello kullanmanız önerilir Management Studio tooremain en son sürümünü Azure ve SQL veritabanı güncelleştirmeleri tooMicrosoft ile eşitlenir. [SQL Server Management Studio’yu güncelleyin](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

## <a name="add-secondary-database"></a>İkincil veritabanı Ekle
Merhaba kullanabilirsiniz **ALTER DATABASE** deyimi toocreate coğrafi olarak çoğaltılmış ikincil sunucu bir veritabanı bir iş ortağı. Hello Yöneticisi çoğaltılan hello sunucu içeren hello veritabanı toobe veritabanlarında bu deyimini yürütün. Merhaba coğrafi olarak çoğaltılmış veritabanınız (Merhaba "birincil veritabanı") hello aynı adı çoğaltılmasını hello veritabanı ve varsayılan olarak, hello sahip olacak hello birincil veritabanı olarak aynı hizmet düzeyi. Merhaba ikincil veritabanı okunabilir veya okunabilir olmayan olabilir ve tek veritabanı olabilir veya esnek havuzdaki. Daha fazla bilgi için bkz: [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) ve [hizmet katmanları](sql-database-service-tiers.md).
Hello ikincil veritabanı oluşturulan ve dağıtılan sonra verileri zaman uyumsuz olarak hello birincil veritabanından çoğaltmaya başlar. Merhaba adımları açıklayan nasıl tooconfigure coğrafi çoğaltma Management Studio'yu kullanarak. Adımları toocreate okunabilir olmayan ve okunabilir ikincil kopya, tek bir veritabanı ya da esnek havuzdaki sağlanır.

> [!NOTE]
> Merhaba hello birincil aynı ad ile Merhaba belirtilen iş ortağı sunucusunda bir veritabanı zaten varsa veritabanı hello komutu başarısız olur.
> 

### <a name="add-readable-secondary-single-database"></a>Okunabilir ikincil (tek veritabanı) Ekle
Aşağıdaki adımları toocreate okunabilir ikincil tek bir veritabanı olarak hello kullanın.

1. Management Studio'da tooyour Azure SQL Database mantıksal sunucusuna bağlanın.
2. Merhaba Hello veritabanları klasörünü açın, **sistem veritabanları** klasörünü sağ tıklatın **ana**ve ardından **yeni sorgu**.
3. Merhaba aşağıdaki kullanın **ALTER DATABASE** deyimi toomake yerel bir coğrafi çoğaltma birincil veritabanında bir ikincil sunucudaki okunabilir ikincil veritabanına sahip.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer2> WITH (ALLOW_CONNECTIONS = ALL);
4. Tıklatın **yürütme** toorun hello sorgu.

### <a name="add-readable-secondary-elastic-pool"></a>Okunabilir ikincil (esnek havuz) Ekle
Aşağıdaki adımları toocreate okunabilir ikincil esnek havuzdaki hello kullanın.

1. Management Studio'da tooyour Azure SQL Database mantıksal sunucusuna bağlanın.
2. Merhaba Hello veritabanları klasörünü açın, **sistem veritabanları** klasörünü sağ tıklatın **ana**ve ardından **yeni sorgu**.
3. Merhaba aşağıdaki kullanın **ALTER DATABASE** deyimi toomake yerel bir coğrafi çoğaltma birincil veritabanında bir ikincil sunucuda esnek havuzdaki okunabilir ikincil veritabanına sahip.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer4> WITH (ALLOW_CONNECTIONS = ALL
           , SERVICE_OBJECTIVE = ELASTIC_POOL (name = MyElasticPool2));
4. Tıklatın **yürütme** toorun hello sorgu.

## <a name="remove-secondary-database"></a>İkincil veritabanını Kaldır
Merhaba kullanabilirsiniz **ALTER DATABASE** deyimi toopermanently ikincil bir veritabanı ve birincil arasındaki hello çoğaltma ortaklığı sonlandırılacak. Bu bildirimi hello ana veritabanı üzerinde hangi hello birincil veritabanının bulunduğu üzerinde yürütülür. Merhaba ilişki sonlandırma sonra normal okuma-yazma veritabanı hello ikincil veritabanı haline gelir. Merhaba bağlantı toosecondary veritabanı bozuk ise hello komutu başarılı olur, ancak bağlantı geri yüklendikten sonra hello ikincil salt okunur hale gelir. Daha fazla bilgi için bkz: [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) ve [hizmet katmanları](sql-database-service-tiers.md).

Adımları tooremove coğrafi olarak çoğaltılmış ikincil bir coğrafi çoğaltma ortaklığı aşağıdaki hello kullanın.

1. Management Studio'da tooyour Azure SQL Database mantıksal sunucusuna bağlanın.
2. Merhaba Hello veritabanları klasörünü açın, **sistem veritabanları** klasörünü sağ tıklatın **ana**ve ardından **yeni sorgu**.
3. Merhaba aşağıdaki kullanın **ALTER DATABASE** deyimi tooremove bir coğrafi olarak çoğaltılmış ikincil.
   
        ALTER DATABASE <MyDB>
           REMOVE SECONDARY ON SERVER <MySecondaryServer1>;
4. Tıklatın **yürütme** toorun hello sorgu.

## <a name="monitor-active-geo-replication-configuration-and-health"></a>Aktif coğrafi çoğaltma yapılandırma ve sistem durumu izleme

İzleme görev hello coğrafi çoğaltma yapılandırma izleme ve veri çoğaltma durumunu izleme içerir.  Merhaba kullanabilirsiniz **sys.dm_geo_replication_links** Itanium tabanlı sistemler için hello ana veritabanı tooreturn bilgileri her veritabanı için mevcut tüm yineleme bağlantıları hakkında hello Azure SQL Database mantıksal sunucusu üzerinde dinamik yönetim görünümünü. Bu görünüm, her birincil ve ikincil veritabanları arasında hello çoğaltma bağlantısı için bir satır içerir. Merhaba kullanabilirsiniz **sys.dm_replication_link_status** dinamik yönetim şu anda bir çoğaltma yinelemesi ilgilendiğini her Azure SQL veritabanı için bir satır tooreturn görüntüleyin. Bu, hem birincil hem de ikincil veritabanlarını içerir. Birden fazla sürekli çoğaltma bağlantısı için belirli bir birincil veritabanı varsa, bu tablo her hello ilişkiler için bir satır içerir. Merhaba görünüm hello mantıksal asıl dahil olmak üzere tüm veritabanlarında oluşturulur. Ancak, bu görünümde hello mantıksal asıl sorgulama boş döndürür. Merhaba kullanabilirsiniz **sys.dm_operation_status** tüm hello hello çoğaltma bağlantılarının durumunu da dahil olmak üzere operations veritabanı için dinamik yönetim görünümünü tooshow hello durumu. Daha fazla bilgi için bkz: [sys.geo_replication_links (Azure SQL veritabanı)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (Azure SQL veritabanı)](https://msdn.microsoft.com/library/mt575504.aspx), ve [sys.dm_operation_status (Azure SQL veritabanı)](https://msdn.microsoft.com/library/dn270022.aspx).

Aşağıdaki adımları toomonitor etkin bir coğrafi çoğaltma ortaklığı hello kullanın.

1. Management Studio'da tooyour Azure SQL Database mantıksal sunucusuna bağlanın.
2. Merhaba Hello veritabanları klasörünü açın, **sistem veritabanları** klasörünü sağ tıklatın **ana**ve ardından **yeni sorgu**.
3. Deyimi tooshow aşağıdaki hello tüm veritabanları ile coğrafi Çoğaltma bağlantılarını kullanın.
   
        SELECT database_id, start_date, modify_date, partner_server, partner_database, replication_state_desc, role, secondary_allow_connections_desc FROM sys.geo_replication_links;
4. Tıklatın **yürütme** toorun hello sorgu.
5. Merhaba Hello veritabanları klasörünü açın, **sistem veritabanları** klasörünü sağ tıklatın **MyDB**ve ardından **yeni sorgu**.
6. Deyimi tooshow hello çoğaltma aşağıdaki kullanım hello gecikmelere ve son çoğaltma zamanı MyDB'my ikincil veritabanları.
   
        SELECT link_guid, partner_server, last_replication, replication_lag_sec FROM sys.dm_geo_replication_link_status
7. Tıklatın **yürütme** toorun hello sorgu.
8. MyDB veritabanıyla ilişkili deyimi tooshow hello en son coğrafi çoğaltma işlemleri aşağıdaki hello kullanın.
   
        SELECT * FROM sys.dm_operation_status where major_resource_id = 'MyDB'
        ORDER BY start_time DESC
9. Tıklatın **yürütme** toorun hello sorgu.

## <a name="next-steps"></a>Sonraki adımlar
* Yük devretme grupları ve etkin coğrafi çoğaltma hakkında daha fazla toolearn bakın - [yük devretme grupları](sql-database-geo-replication-overview.md)
* İş sürekliliğine genel bakış ve senaryolar için bkz: [iş sürekliliğine genel bakış](sql-database-business-continuity.md)

