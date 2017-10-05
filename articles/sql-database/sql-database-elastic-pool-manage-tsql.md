---
title: "T-SQL: bir Azure SQL Database esnek havuzunu yönetme | Microsoft Docs"
description: "T-SQL Azure SQL Database esnek havuzunu yönetmek için kullanın."
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
ms.openlocfilehash: c6b64e4a7fd91283a37a792b294965064d653003
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a>İzleme ve Transact-SQL sahip bir esnek havuz yönetme
Bu konuda nasıl yönetileceğini ölçeklenebilir gösterilmektedir [esnek havuzlar](sql-database-elastic-pool.md) Transact-SQL ile.  Ayrıca oluşturabilir ve bir Azure esnek havuzunu yönetme [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), REST API veya [C#](sql-database-elastic-pool-manage-csharp.md). Ayrıca oluşturun ve içine ve dışına esnek havuzlar kullanarak veritabanlarını taşıma [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).


Kullanım [Create Database (Azure SQL veritabanı)](https://msdn.microsoft.com/library/dn268335.aspx) ve [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) oluşturun ve içine ve dışına esnek havuzlar veritabanlarını taşımak için komutları. Esnek havuz bu komutları kullanmadan önce mevcut olması gerekir. Bu komutlar, yalnızca veritabanları etkiler. T-SQL komutlarıyla yeni havuzları oluşturulmasını ve havuzu özelliklerini (örneğin, minimum ve maksimum Edtu) ayarı değiştirilemez.

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Havuza alınmış bir veritabanı bir esnek havuz oluşturma
CREATE DATABASE komutunu servıce_objectıve seçeneğiyle kullanın.   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

Esnek havuzdaki tüm veritabanları esnek havuzun (temel, standart, Premium) hizmet katmanı devralır. 

## <a name="move-a-database-between-elastic-pools"></a>Bir veritabanını esnek havuzları arasında taşıma
ALTER DATABASE komutu ile değiştir kullanın ve hizmet kümesi\_HEDEFİ seçeneği esnek olarak\_HAVUZU. Adı, hedef havuzunun adına ayarlayın.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move the database named db1 to an elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a>Bir veritabanını bir esnek havuza taşıma
ALTER DATABASE komutu ile değiştir kullanın ve hizmet kümesi\_HEDEFİ seçeneği ELASTIC_POOL olarak. Adı, hedef havuzunun adına ayarlayın.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move the database named db1 to an elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a>Bir veritabanını bir esnek havuz dışına taşıma
ALTER DATABASE komutunu kullanın ve servıce_objectıve birisi performans düzeyleri (örneğin, S0 veya S1) olarak ayarlayın.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes the database into a stand-alone database with the service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a>Esnek havuzdaki veritabanlarını Listele
Kullanım [sys.database\_hizmet \_hedefleri Görünüm](https://msdn.microsoft.com/library/mt712619) esnek havuzdaki tüm veritabanları listelemek için. Asıl veritabanı görünümü sorgulamak için oturum açın.

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Esnek havuz için kaynak kullanım verilerini alma
Kullanım [sys.elastic\_havuzu \_kaynak \_istatistikleri Görünüm](https://msdn.microsoft.com/library/mt280062.aspx) bir esnek havuz bir mantıksal sunucu üzerinde kaynak kullanım istatistiklerini incelemek için. Asıl veritabanı görünümü sorgulamak için oturum açın.

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a>Havuza alınmış bir veritabanı için kaynak kullanımını Al
Kullanım [sys.dm\_ db\_ kaynak\_istatistikleri Görünüm](https://msdn.microsoft.com/library/dn800981.aspx) veya [sys.resource \_istatistikleri Görünüm](https://msdn.microsoft.com/library/dn269979.aspx) bir veritabanında kaynak kullanım istatistiklerini incelemek için bir Esnek havuz. Bu işlem, kaynak kullanımı için tek bir veritabanını sorgulamak için benzer.

## <a name="next-steps"></a>Sonraki adımlar
Bir esnek havuz oluşturduktan sonra havuzdaki esnek veritabanları esnek iş oluşturarak yönetebilirsiniz. Esnek iş havuzdaki veritabanlarına herhangi bir sayıda karşı çalışan T-SQL betiklerini kolaylaştırır. Daha fazla bilgi için bkz: [esnek veritabanı işleri genel bakış](sql-database-elastic-jobs-overview.md). 

Bkz: [Azure SQL veritabanı ile ölçeğini](sql-database-elastic-scale-introduction.md): ölçeğini, verileri taşımak için esnek veritabanı araçlarını kullanın sorgulamak ya da hareketleri oluşturun.

