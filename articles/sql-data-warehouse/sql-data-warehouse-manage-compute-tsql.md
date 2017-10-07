---
title: "aaaPause, Sürdür, ölçeği T-SQL Azure SQL veri ambarı ile | Microsoft Docs"
description: "Dwu ayarlayarak görevleri tooscale kullanıma performans transact-SQL (T-SQL). Yoğun olmayan saatlerde ölçeklendirme tarafından maliyet tasarrufu."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: a970d939-2adf-4856-8a78-d4fe8ab2cceb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/30/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 84c6868acb673221d8853319ac9a05bb98b2b7c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a>Azure SQL Data warehouse'da (T-SQL) işlem güç yönetimi
> [!div class="op_single_selector"]
> * [Genel Bakış](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a>Geçerli DWU ayarlarını görüntüle
tooview hello geçerli DWU ayarlarına veritabanlarınız için:

1. SQL Server Nesne Gezgini Visual Studio'da açın.
2. Merhaba mantıksal SQL veritabanı sunucusu ile ilişkili toohello ana veritabanına bağlanın.
3. Merhaba sys.database_service_objectives dinamik yönetim görünümünden seçin. Örnek aşağıda verilmiştir: 

```sql
SELECT
    db.name [Database]
,   ds.edition [Edition]
,   ds.service_objective [Service Objective]
FROM
    sys.database_service_objectives ds
JOIN
    sys.databases db ON ds.database_id = db.database_id
```

<a name="scale-dwu-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a>Bilgi işlem
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

toochange hello Dwu:

1. Mantıksal SQL veritabanı sunucunuzla ilişkili toohello ana veritabanına bağlanın.
2. Kullanım hello [ALTER DATABASE] [ ALTER DATABASE] TSQL deyimi. Merhaba aşağıdaki örnek hello hizmet düzeyi hedefi tooDW1000 hello veritabanı MySQLDW için ayarlar. 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a>Veritabanı durumunda ve işlem ilerleme durumunu denetleme

1. Mantıksal SQL veritabanı sunucunuzla ilişkili toohello ana veritabanına bağlanın.
2. Sorgu toocheck veritabanı durumu Gönder

```sql
SELECT *
FROM
sys.databases
```

3. Sorgu toocheck işlemin durumunu Gönder

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

Bu DMV SQL veri ambarı tamamlandı veya IN_PROGRESS olacaktır hello işlemi hello işlemi ve hello durumu gibi çeşitli yönetim işlemlerini hakkında bilgi döndürür.



<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Sonraki adımlar
Diğer yönetim görevleri için bkz: [yönetimine genel bakış][Management overview].

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
