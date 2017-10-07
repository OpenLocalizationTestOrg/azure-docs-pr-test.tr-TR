---
title: "Azure SQL veritabanı kullanarak dinamik yönetim görünümlerini aaaMonitoring | Microsoft Docs"
description: "Bilgi nasıl toodetect dinamik yönetim görünümlerini toomonitor Microsoft Azure SQL veritabanı kullanarak genel performans sorunlarını tanılamak ve."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: d08f505f-3c62-47d4-bab7-35c9a834b79b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 43d5fe2dd9a38d031e9334f6ad49fce5866e3bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a>Dinamik yönetim görünümlerini kullanarak Azure SQL Database’i izleme
Microsoft Azure SQL veritabanı sağlar, engellenen veya uzun süre çalışan sorgular, kaynak darboğazları, zayıf sorgu planları ve benzeri tarafından kaynaklanabilir toodiagnose performans sorunlarını dinamik yönetim kümesini görüntüler. Bu konu hakkında bilgi sağlar dinamik yönetim görünümlerini kullanarak toodetect ortak performans sorunları.

SQL veritabanı, kısmen dinamik yönetim görünümlerini üç kategoride destekler:

* Veritabanı ile ilgili dinamik yönetim görünümlerini.
* Yürütme ilgili dinamik yönetim görünümlerini.
* İşlem ilgili dinamik yönetim görünümlerini.

Dinamik Yönetim görünümlerini hakkında ayrıntılı bilgi için bkz: [dinamik yönetim görünümlerini ve işlevleri (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) SQL Server Books Online.

## <a name="permissions"></a>İzinler
SQL veritabanı'nda dinamik yönetim görünümünü sorgulanmasını gerektirir **görünüm veritabanı durumu** izinleri. Merhaba **görünüm veritabanı durumu** izin hello geçerli veritabanının içindeki tüm nesneler hakkında bilgi döndürür.
toogrant hello **görünüm veritabanı durumu** izin tooa belirli veritabanı kullanıcısı, sorgu aşağıdaki hello çalıştırın:

```GRANT VIEW DATABASE STATE toodatabase_user; ```

Bir şirket içi SQL Server örneğinde dinamik yönetim görünümlerini sunucu durumu bilgilerini döndürür. SQL veritabanı'nda, bunlar yalnızca geçerli, mantıksal veritabanı ile ilgili bilgiler döndürür.

## <a name="calculating-database-size"></a>Veritabanı boyutu hesaplama
Merhaba aşağıdaki sorguyu veritabanınızın (megabayt cinsinden) hello boyutunu döndürür:

```
-- Calculates hello size of hello database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

Merhaba aşağıdaki sorguyu hello boyutu (megabayt cinsinden) tek tek nesnelerin veritabanınızda döndürür:

```
-- Calculates hello size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a>İzleme bağlantıları
Merhaba kullanabilirsiniz [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) tooretrieve hello kurulan bağlantılar tooa belirli Azure SQL veritabanı sunucusu ve her bağlantının hello ayrıntıları hakkındaki bilgileri görüntüleyin. Ayrıca, hello [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) görünümü, tüm etkin kullanıcı bağlantıları ve iç görevler hakkında bilgi alırken yararlıdır.
Merhaba aşağıdaki sorgu hello geçerli bağlantı üzerine bilgi alır:

```
SELECT
    c.session_id, c.net_transport, c.encrypt_option,
    c.auth_scheme, s.host_name, s.program_name,
    s.client_interface_name, s.login_name, s.nt_domain,
    s.nt_user_name, s.original_login_name, c.connect_time,
    s.login_time
FROM sys.dm_exec_connections AS c
JOIN sys.dm_exec_sessions AS s
    ON c.session_id = s.session_id
WHERE c.session_id = @@SPID;
```

> [!NOTE]
> Merhaba yürütülürken **sys.dm_exec_requests** ve **sys.dm_exec_sessions görünümleri**, varsa **görünüm veritabanı durumu** izin hello veritabanı üzerinde tüm yürütme görürsünüz. Merhaba veritabanı oturumlarını; Aksi takdirde, geçerli oturum yalnızca hello bakın.
> 
> 

## <a name="monitoring-query-performance"></a>Sorgu performansını izleme
Yavaş ya da uzun çalışan sorgu önemli sistem kaynaklarını tüketebilir. Bu bölüm, nasıl toouse dinamik yönetim toodetect birkaç ortak sorgu performans sorunlarına görünümleri gösterir. Sorun giderme, eski ancak hala yararlı bir başvuru: Merhaba [SQL Server 2008'de performans sorunlarını giderme](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) Microsoft TechNet makalesi.

### <a name="finding-top-n-queries"></a>İlk N sorguları bulma
Merhaba aşağıdaki örnek hello üst beş sorgular tarafından ortalama CPU süresi derece hakkında bilgi verir. Mantıksal olarak eşdeğer sorguları kendi toplu kaynak tüketimi gruplanması Bu örnek sorgu karma tootheir göre hello sorguları toplar.

```
SELECT TOP 5 query_stats.query_hash AS "Query Hash",
    SUM(query_stats.total_worker_time) / SUM(query_stats.execution_count) AS "Avg CPU Time",
    MIN(query_stats.statement_text) AS "Statement Text"
FROM
    (SELECT QS.*,
    SUBSTRING(ST.text, (QS.statement_start_offset/2) + 1,
    ((CASE statement_end_offset
        WHEN -1 THEN DATALENGTH(ST.text)
        ELSE QS.statement_end_offset END
            - QS.statement_start_offset)/2) + 1) AS statement_text
     FROM sys.dm_exec_query_stats AS QS
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) as ST) as query_stats
GROUP BY query_stats.query_hash
ORDER BY 2 DESC;
```

### <a name="monitoring-blocked-queries"></a>Engellenen sorguları izleme
Yavaş veya uzun süre çalışan sorgular tooexcessive kaynak tüketimini katkıda ve engellenen sorguları hello sonucu olabilir. Merhaba engelleme nedeni hello sorgu planlarını kullanışlı dizinler eksikliği hello ve benzeri zayıf uygulama tasarımı, bozuk olabilir. Azure SQL veritabanınızda hello sys.dm_tran_locks tooget hakkındaki bilgileri görüntüleyin hello geçerli kilitleme etkinliğini kullanabilirsiniz. Örnek kod, bkz: [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) SQL Server Books Online.

### <a name="monitoring-query-plans"></a>Sorgu planları izleme
Verimsiz sorgu planı da CPU tüketimi artırabilir. Merhaba aşağıdaki örnek kullanır hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) hangi sorgusu hello en toplam CPU kullanan toodetermine görüntüleyin.

```
SELECT
    highest_cpu_queries.plan_handle,
    highest_cpu_queries.total_worker_time,
    q.dbid,
    q.objectid,
    q.number,
    q.encrypted,
    q.[text]
FROM
    (SELECT TOP 50
        qs.plan_handle,
        qs.total_worker_time
    FROM
        sys.dm_exec_query_stats qs
    ORDER BY qs.total_worker_time desc) AS highest_cpu_queries
    CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS q
ORDER BY highest_cpu_queries.total_worker_time DESC;
```

## <a name="see-also"></a>Ayrıca bkz.
[Giriş tooSQL veritabanı](sql-database-technical-overview.md)

