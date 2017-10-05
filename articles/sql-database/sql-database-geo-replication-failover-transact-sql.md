---
title: "Azure SQL veritabanı için TSQL:Initiate yük devretme | Microsoft Docs"
description: "Transact-SQL kullanarak Azure SQL veritabanı için planlanmış veya planlanmamış bir yük devretme başlatın"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5eb2d256-025d-4f5a-99d4-17f702b37f14
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 459941d2c82e5d4ef62beab4ccf775ab8f5efce4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="initiate-a-planned-or-unplanned-failover-for-azure-sql-database-with-transact-sql"></a>Azure SQL Database Transact-SQL ile için planlanmış veya planlanmamış bir yük devretme başlatın

Bu makalede Transact-SQL kullanarak bir ikincil SQL veritabanı yük devretme başlatın kullanmayı gösterir. Coğrafi çoğaltma yapılandırmak için bkz: [Azure SQL veritabanı için coğrafi çoğaltma yapılandırma](sql-database-geo-replication-transact-sql.md).

Yük devretme başlatmak için aşağıdakiler gerekir:

* Birincil DBManager olan bir oturum açma
* Coğrafi replicate olacak yerel veritabanı db_ownership sahip
* Coğrafi çoğaltma yapılandıracak partner sunucuları üzerinde DBManager olabilir
* En yeni sürümü SQL Server Management Studio (SSMS)

> [!IMPORTANT]
> Microsoft Azure ve SQL Veritabanı güncelleştirmeleriyle aynı sürümde olmak için her zaman en güncel Management Studio sürümünü kullanmanız önerilir. [SQL Server Management Studio’yu güncelleyin](https://msdn.microsoft.com/library/mt238290.aspx).
>  

## <a name="initiate-a-planned-failover-promoting-a-secondary-database-to-become-the-new-primary"></a>Yeni birincil olmasını ikincil bir veritabanı yükseltme planlı bir yük devretme başlatın
Kullanabileceğiniz **ALTER DATABASE** ikincil olmak için var olan birincil indirgeme planlı bir şekilde yeni birincil veritabanı olmak için ikincil bir veritabanını yükseltmek için deyimi. Bu ifade, yükseltilmekte coğrafi olarak çoğaltılmış ikincil veritabanının bulunduğu Azure SQL Database mantıksal sunucusu üzerindeki ana veritabanı üzerinde yürütülür. Bu işlev için planlanan yük devretme, DR ayrıntısına sırasında gibi tasarlanmıştır ve birincil veritabanının kullanılabilir olması gerekir.

Komutu aşağıdaki iş akışını gerçekleştirir:

1. Geçici olarak çoğaltma ikincil kopyalanması tüm bekleyen işlemleri neden ve tüm yeni işlemleri engelleme zaman uyumlu moduna geçer;
2. İki veritabanı rolleri coğrafi çoğaltma ortaklığı geçer.  

Bu sıra iki veritabanı rolleri geçin ve bu nedenle veri kaybı olmayacaktır önce eşitlenir güvence altına alır. Rolleri geçiş sırasında hangi sırasında her iki veritabanı (0-25 saniye terabayt) kullanılamaz kısa bir süre yoktur. Birincil veritabanında birden fazla ikincil veritabanı varsa, yeni birincil bağlanmak için diğer ikincil kopya komutu otomatik olarak yeniden yapılandırır.  Tüm işlemi normal koşullarda tamamlanması bir dakikadan az zamanınızı. Daha fazla bilgi için bkz: [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) ve [hizmet katmanları](sql-database-service-tiers.md).

Planlanmış bir yük devretme başlatmak için aşağıdaki adımları kullanın.

1. Management Studio'da coğrafi olarak çoğaltılmış ikincil veritabanının bulunduğu Azure SQL Database mantıksal sunucusuna bağlanın.
2. Veritabanları klasörünü açın, **sistem veritabanları** klasörünü sağ tıklatın **ana**ve ardından **yeni sorgu**.
3. Aşağıdaki **ALTER DATABASE** ikincil veritabanının birincil role geçiş yapmak için deyimi.
   
        ALTER DATABASE <MyDB> FAILOVER;
4. Sorguyu çalıştırmak için **Yürüt**'e tıklayın.

> [!NOTE]
> Nadir durumlarda işlemi tamamlayamıyor ve takılan görünebilir mümkündür. Bu durumda, kullanıcı zorla yük devri komutunu yürütün ve veri kaybı kabul edin.
> 
> 

## <a name="initiate-an-unplanned-failover-from-the-primary-database-to-the-secondary-database"></a>Planlanmamış yük devretme birincil veritabanından ikincil veritabanını başlatmak
Kullanabileceğiniz **ALTER DATABASE** birincil veritabanı artık kullanılabilir olmadığında bir kerede bir ikincil olmak için var olan birincil indirgeme zorlama planlanmamış bir şekilde yeni birincil veritabanı olmak için ikincil bir veritabanını yükseltmek için deyimi. Bu ifade, yükseltilmekte coğrafi olarak çoğaltılmış ikincil veritabanının bulunduğu Azure SQL Database mantıksal sunucusu üzerindeki ana veritabanı üzerinde yürütülür.

Bu işlevsellik, kullanılabilirlik veritabanının geri yüklenmesi önemli ve bazı veri kaybı kabul edilebilir olduğunda, olağanüstü durum kurtarma için tasarlanmıştır. Zorla yük devretme çağrıldığında, belirtilen ikincil veritabanı hemen birincil veritabanı haline gelir ve yazma işlemleri kabul başlar. Özgün birincil veritabanı bu yeni birincil veritabanı ile bağlanana hemen artımlı yedekleme özgün birincil veritabanında alınır ve yeni birincil veritabanı için ikincil bir veritabanı içine eski birincil veritabanında yapılan; Sonuç olarak, yalnızca eşitleme çoğaltmasının yeni birincil değil.

Ancak, zorla yük devretme oluşmadan önce yeni birincil veritabanına çoğaltılmamış olmayan eski birincil veritabanına gönderilen verileri kurtarmak kullanıcı isterse, zaman içinde nokta geri ikincil veritabanlarında desteklenmediğinden, bu veri kaybı kurtarmak için destek bulunmaya kullanıcı gerekir.

Birincil veritabanında birden fazla ikincil veritabanı varsa, yeni birincil bağlanmak için diğer ikincil kopya komutu otomatik olarak yeniden yapılandırır.

Planlanmamış bir yük devretme başlatmak için aşağıdaki adımları kullanın.

1. Management Studio'da coğrafi olarak çoğaltılmış ikincil veritabanının bulunduğu Azure SQL Database mantıksal sunucusuna bağlanın.
2. Veritabanları klasörünü açın, **sistem veritabanları** klasörünü sağ tıklatın **ana**ve ardından **yeni sorgu**.
3. Aşağıdaki **ALTER DATABASE** ikincil veritabanının birincil role geçiş yapmak için deyimi.
   
        ALTER DATABASE <MyDB>   FORCE_FAILOVER_ALLOW_DATA_LOSS;
4. Sorguyu çalıştırmak için **Yürüt**'e tıklayın.

> [!NOTE]
> Birincil ve ikincil çevrimiçi olduğunda komutu verildikten eski birincil veri eşitleme olmadan hemen yeni ikincil olur. Bazı veri kaybı komutu verildiğinde uygulanıyor işlemleri birincil ortaya çıkabilir.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* Yük devretme işleminden sonra yeni birincil sunucu ve veritabanı için kimlik doğrulama gereksinimlerini yapılandırılmış emin olun. Ayrıntılar için bkz [olağanüstü durum kurtarma işleminden sonra SQL veritabanı güvenlik](sql-database-geo-replication-security-config.md).
* Aktif coğrafi bir olağanüstü durum kurtarma ayrıntıya gerçekleştirme ve öncesi kurtarma ve kurtarma sonrası adımları dahil olmak üzere çoğaltma, kullanarak sonra bir olağanüstü durum kurtarma öğrenmek için bkz: [olağanüstü durum kurtarma](sql-database-disaster-recovery.md)
* Aktif coğrafi çoğaltma hakkında bir Sasha Nosov blog gönderisi için bkz: [Spotlight yeni coğrafi çoğaltma özellikleri hakkında](https://azure.microsoft.com/blog/spotlight-on-new-capabilities-of-azure-sql-database-geo-replication/)
* Aktif coğrafi çoğaltma kullanmak üzere bulut uygulamaları tasarlama hakkında daha fazla bilgi için bkz: [coğrafi çoğaltma'yı kullanarak iş sürekliliği için bulut uygulama tasarlama](sql-database-designing-cloud-solutions-for-disaster-recovery.md)
* Aktif coğrafi çoğaltma ile esnek havuzları kullanma hakkında daha fazla bilgi için bkz: [esnek havuz olağanüstü durum kurtarma stratejilerini](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
* İş sürekliliği genel bakış için bkz: [iş Sürekliliğine genel bakış](sql-database-business-continuity.md)

