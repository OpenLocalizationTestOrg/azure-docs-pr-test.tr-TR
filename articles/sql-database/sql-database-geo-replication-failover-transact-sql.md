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
ms.openlocfilehash: 418953e044ba84ce758063d56a371af45d5cdfe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="initiate-a-planned-or-unplanned-failover-for-azure-sql-database-with-transact-sql"></a>Azure SQL Database Transact-SQL ile için planlanmış veya planlanmamış bir yük devretme başlatın

Bu makale size nasıl gösterir tooinitiate yük devretme tooa ikincil SQL veritabanı Transact-SQL kullanarak. tooconfigure coğrafi çoğaltma, bkz: [Azure SQL veritabanı için coğrafi çoğaltma yapılandırma](sql-database-geo-replication-transact-sql.md).

tooinitiate yük devretme hello aşağıdaki gerekir:

* Birincil hello DBManager olan bir oturum açma
* Coğrafi replicate olacak hello yerel veritabanı db_ownership sahip
* DBManager hello partner sunucuları toowhich üzerinde olmanız coğrafi çoğaltma yapılandırır
* En yeni sürümü SQL Server Management Studio (SSMS)

> [!IMPORTANT]
> Her zaman hello kullanmanız önerilir Management Studio tooremain en son sürümünü Azure ve SQL veritabanı güncelleştirmeleri tooMicrosoft ile eşitlenir. [SQL Server Management Studio’yu güncelleyin](https://msdn.microsoft.com/library/mt238290.aspx).
>  

## <a name="initiate-a-planned-failover-promoting-a-secondary-database-toobecome-hello-new-primary"></a>İkincil veritabanı toobecome hello yeni birincil yükseltme planlı bir yük devretme başlatın
Merhaba kullanabilirsiniz **ALTER DATABASE** deyimi toopromote ikincil veritabanı toobecome hello yeni birincil, ikincil bir hello varolan birincil toobecome indirgeme planlı bir biçimde veritabanı. Bu bildirimi hello Azure SQL Database mantıksal sunucusunda hangi hello yükseltilmekte coğrafi olarak çoğaltılmış ikincil veritabanının bulunduğu hello ana veritabanı üzerinde yürütülür. Bu işlev için planlanan yük devretme, gibi hello DR ayrıntısına sırasında tasarlanmıştır ve bu hello birincil veritabanı kullanılabilir olmasını gerektirir.

Merhaba komutu iş akışının izlenmesi hello gerçekleştirir:

1. Geçici olarak anahtarları çoğaltma toosynchronous modu, tüm bekleyen işlemleri toobe neden toohello ikincil ve tüm yeni işlemleri engelleme Temizlenen;
2. Anahtarları hello iki hello coğrafi çoğaltma ortaklığı veritabanlarında rolleri hello.  

Bu sıra iki veritabanı hello rolleri geçin ve bu nedenle veri kaybı olmayacaktır önce eşitlenir bu hello güvence altına alır. Merhaba rolleri geçiş sırasında hangi sırasında her iki veritabanı (Merhaba 0 too25 saniye üzerinde sırasını) kullanılamaz kısa bir süre yoktur. Otomatik olarak Hello birincil veritabanı varsa, birden fazla ikincil veritabanları, hello komutu RECONFIGURE diğer ikincil tooconnect toohello yeni birincil hello.  Merhaba tüm işlemi normal koşullarda dakika toocomplete değerinden almanız gerekir. Daha fazla bilgi için bkz: [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) ve [hizmet katmanları](sql-database-service-tiers.md).

Aşağıdaki adımları tooinitiate planlanmış bir yük devretme hello kullanın.

1. Management Studio'da coğrafi olarak çoğaltılmış ikincil veritabanının bulunduğu toohello Azure SQL Database mantıksal sunucusuna bağlanın.
2. Merhaba Hello veritabanları klasörünü açın, **sistem veritabanları** klasörünü sağ tıklatın **ana**ve ardından **yeni sorgu**.
3. Merhaba aşağıdaki kullanın **ALTER DATABASE** deyimi tooswitch hello ikincil veritabanı toohello birincil rolü.
   
        ALTER DATABASE <MyDB> FAILOVER;
4. Tıklatın **yürütme** toorun hello sorgu.

> [!NOTE]
> Nadir durumlarda hello işlemi tamamlayamıyor ve takılan görünebilir mümkündür. Bu durumda, hello kullanıcı hello zorla yük devri komutunu yürütün ve veri kaybı kabul edin.
> 
> 

## <a name="initiate-an-unplanned-failover-from-hello-primary-database-toohello-secondary-database"></a>Merhaba birincil veritabanı toohello ikincil veritabanını planlanmamış bir yük devretmeyi başlatın
Merhaba kullanabilirsiniz **ALTER DATABASE** deyimi toopromote ikincil veritabanı toobecome hello yeni birincil veritabanı hello varolan birincil toobecome hello indirgeme zorlama bir planlanmamış şekilde, bir ikincil aynı anda zaman hello birincil veritabanı artık kullanılamıyor. Bu bildirimi hello Azure SQL Database mantıksal sunucusunda hangi hello yükseltilmekte coğrafi olarak çoğaltılmış ikincil veritabanının bulunduğu hello ana veritabanı üzerinde yürütülür.

Bu işlevsellik, hello veritabanı geri yükleme kullanılabilirliğini kritik ve bazı veri kaybı kabul edilebilir olduğunda, olağanüstü durum kurtarma için tasarlanmıştır. Merhaba zorla yük devretme çağrıldığında, belirtilen ikincil veritabanı hemen hello birincil veritabanı haline gelir ve yazma işlemleri kabul başlar. Bu yeni birincil veritabanı ile mümkün tooreconnect Hello özgün birincil veritabanı olduğunda hemen artımlı yedekleme hello özgün birincil veritabanı alınır ve hello yeni birincil veritabanı için ikincil bir veritabanı içine hello eski birincil veritabanına yapılan; Sonuç olarak, yalnızca eşitleme çoğaltmasının hello yeni birincil değil.

Ancak, kaydedilen toorecover veri Hello kullanıcı isterse, zaman içinde nokta geri hello ikincil veritabanlarında, desteklenmediğinden hello zorla yük devretme oluşmadan önce değil olsaydı toohello eski birincil veritabanı toohello yeni birincil veritabanı çoğaltılan, Merhaba kullanıcının tooengage destek toorecover gerekir bu verileri kaybolur.

Otomatik olarak Hello birincil veritabanı varsa, birden fazla ikincil veritabanları, hello komutu RECONFIGURE diğer ikincil tooconnect toohello yeni birincil hello.

Aşağıdaki adımları tooinitiate planlanmamış bir yük devretme hello kullanın.

1. Management Studio'da coğrafi olarak çoğaltılmış ikincil veritabanının bulunduğu toohello Azure SQL Database mantıksal sunucusuna bağlanın.
2. Merhaba Hello veritabanları klasörünü açın, **sistem veritabanları** klasörünü sağ tıklatın **ana**ve ardından **yeni sorgu**.
3. Merhaba aşağıdaki kullanın **ALTER DATABASE** deyimi tooswitch hello ikincil veritabanı toohello birincil rolü.
   
        ALTER DATABASE <MyDB>   FORCE_FAILOVER_ALLOW_DATA_LOSS;
4. Tıklatın **yürütme** toorun hello sorgu.

> [!NOTE]
> Birincil ve ikincil çevrimiçi olduğunda hello komutu verilirse hello eski birincil olacak yeni ikincil veri eşitleme olmadan hemen hello. Bazı veri kaybı hello komut verildiğinde uygulanıyor işlemleri Hello birincil olduğunda oluşabilir.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* Yük devretme sonrasında hello yeni birincil sunucu ve veritabanı hello kimlik doğrulama gereksinimleri yapılandırılmış emin olun. Ayrıntılar için bkz [olağanüstü durum kurtarma işleminden sonra SQL veritabanı güvenlik](sql-database-geo-replication-security-config.md).
* Aktif coğrafi bir olağanüstü durum kurtarma ayrıntıya gerçekleştirme ve öncesi kurtarma ve kurtarma sonrası adımları dahil olmak üzere çoğaltma, kullanarak sonra bir olağanüstü durum kurtarma toolearn bakın [olağanüstü durum kurtarma](sql-database-disaster-recovery.md)
* Aktif coğrafi çoğaltma hakkında bir Sasha Nosov blog gönderisi için bkz: [Spotlight yeni coğrafi çoğaltma özellikleri hakkında](https://azure.microsoft.com/blog/spotlight-on-new-capabilities-of-azure-sql-database-geo-replication/)
* Bulut uygulamaları toouse aktif coğrafi çoğaltma tasarlama hakkında daha fazla bilgi için bkz: [coğrafi çoğaltma'yı kullanarak iş sürekliliği için bulut uygulama tasarlama](sql-database-designing-cloud-solutions-for-disaster-recovery.md)
* Aktif coğrafi çoğaltma ile esnek havuzları kullanma hakkında daha fazla bilgi için bkz: [esnek havuz olağanüstü durum kurtarma stratejilerini](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
* İş sürekliliği genel bakış için bkz: [iş Sürekliliğine genel bakış](sql-database-business-continuity.md)

