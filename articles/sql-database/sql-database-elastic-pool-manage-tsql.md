---
title: "T-SQL: bir Azure SQL Database esnek havuzunu yönetme | Microsoft Docs"
description: "T-SQL toomanage bir Azure SQL Database esnek havuzunu kullanın."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 4e288e17-bc3e-4255-9fbe-0a2ac0dbd7dd
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 05/27/2016
ms.author: srinia
ms.openlocfilehash: 666f131b2c88849a1a9ea83381bbc27548e93599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a>İzleme ve Transact-SQL sahip bir esnek havuz yönetme
Bu konu, nasıl gösterir toomanage ölçeklenebilir [esnek havuzlar](sql-database-elastic-pool.md) Transact-SQL ile.  Ayrıca oluşturmak ve bir Azure esnek havuz hello yönetmek [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), REST API hello veya [C#](sql-database-elastic-pool-manage-csharp.md). Ayrıca oluşturun ve içine ve dışına esnek havuzlar kullanarak veritabanlarını taşıma [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).


Kullanım hello [Create Database (Azure SQL veritabanı)](https://msdn.microsoft.com/library/dn268335.aspx) ve [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) toocreate ve taşıma veritabanları içine ve dışına esnek havuzlar komutları. Bu komutlar kullanmadan önce hello esnek havuz mevcut olması gerekir. Bu komutlar, yalnızca veritabanları etkiler. Yeni havuzları oluşturulmasını ve hello ayarı (örneğin, minimum ve maksimum Edtu) havuzu özelliklerinin T-SQL komutlarıyla değiştirilemez.

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Havuza alınmış bir veritabanı bir esnek havuz oluşturma
Merhaba servıce_objectıve seçeneği ile Merhaba CREATE DATABASE komutunu kullanın.   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

Esnek havuzdaki tüm veritabanları hello hizmet katmanı hello esnek havuzun (temel, standart, Premium) devralır. 

## <a name="move-a-database-between-elastic-pools"></a>Bir veritabanını esnek havuzları arasında taşıma
Merhaba Değiştir ile Merhaba ALTER DATABASE komutunu kullanın ve hizmet kümesi\_HEDEFİ seçeneği esnek olarak\_HAVUZU. Merhaba adı toohello hello hedef havuzu adını ayarlayın.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move hello database named db1 tooan elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a>Bir veritabanını bir esnek havuza taşıma
Merhaba Değiştir ile Merhaba ALTER DATABASE komutunu kullanın ve hizmet kümesi\_HEDEFİ seçeneği ELASTIC_POOL olarak. Merhaba adı toohello hello hedef havuzu adını ayarlayın.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move hello database named db1 tooan elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a>Bir veritabanını bir esnek havuz dışına taşıma
Merhaba ALTER DATABASE komutunu kullanın ve hello servıce_objectıve tooone hello performans düzeyleri (örneğin, S0 veya S1) olarak ayarlayın.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes hello database into a stand-alone database with hello service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a>Esnek havuzdaki veritabanlarını Listele
Kullanım hello [sys.database\_hizmet \_hedefleri Görünüm](https://msdn.microsoft.com/library/mt712619) toolist tüm esnek havuzdaki veritabanları hello. Toohello asıl veritabanı tooquery hello görünümü oturum açın.

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Esnek havuz için kaynak kullanım verilerini alma
Kullanım hello [sys.elastic\_havuzu \_kaynak \_istatistikleri Görünüm](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine hello kaynak kullanım istatistiklerini bir esnek havuz bir mantıksal sunucu üzerinde. Toohello asıl veritabanı tooquery hello görünümü oturum açın.

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a>Havuza alınmış bir veritabanı için kaynak kullanımını Al
Kullanım hello [sys.dm\_ db\_ kaynak\_istatistikleri Görünüm](https://msdn.microsoft.com/library/dn800981.aspx) veya [sys.resource \_istatistikleri Görünüm](https://msdn.microsoft.com/library/dn269979.aspx) tooexamine hello kaynak kullanım istatistiklerini bir Esnek havuzdaki veritabanı. Tek veritabanı için benzer tooquerying kaynak kullanımı işlemidir.

## <a name="next-steps"></a>Sonraki adımlar
Bir esnek havuz oluşturduktan sonra esnek iş oluşturarak hello havuzdaki esnek veritabanları yönetebilirsiniz. Esnek iş hello havuzdaki veritabanları herhangi bir sayıda karşı çalışan T-SQL betiklerini kolaylaştırır. Daha fazla bilgi için bkz: [esnek veritabanı işleri genel bakış](sql-database-elastic-jobs-overview.md). 

Bkz: [Azure SQL veritabanı ile ölçeğini](sql-database-elastic-scale-introduction.md): esnek veritabanı araçlarını tooscale çıkışı kullanın, veri taşıma sorgulamak ya da hareketleri oluşturun.

