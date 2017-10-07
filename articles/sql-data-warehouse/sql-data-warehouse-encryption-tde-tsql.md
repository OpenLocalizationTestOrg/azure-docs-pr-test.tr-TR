---
title: "SQL veri ambarı (T-SQL) verileri şifreleme aaaTransparent | Microsoft Docs"
description: "Saydam veri şifreleme (TDE) SQL veri ambarı (T-SQL)"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: barbkess
editor: 
ms.assetid: 8ccefef3-1308-41ee-b336-5e491d1098ae
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 3894431c76f14b217f3a6b9a42dbf2f4d216bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a>Saydam veri şifreleme (TDE) ile çalışmaya başlama
> [!div class="op_single_selector"]
> * [Güvenlik genel bakış](sql-data-warehouse-overview-manage-security.md)
> * [Kimlik doğrulaması](sql-data-warehouse-authentication.md)
> * [Şifreleme (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Şifreleme (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a>Gerekli izinleri
tooenable saydam veri şifreleme (TDE), bir yönetici veya hello dbmanager rolünün bir üyesi olmanız gerekir.

## <a name="enabling-encryption"></a>Şifrelemeyi etkinleştirme
Bir SQL Data Warehouse için bu adımları tooenable TDE izleyin:

1. Toohello bağlanmak *ana* hello sunucusundaki bir yönetici veya hello üyesi olan bir oturum açma kullanarak hello veritabanı barındırma veritabanı **dbmanager** hello ana veritabanı rolü
2. Deyimi tooencrypt hello veritabanı aşağıdaki hello yürütün.

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>Şifreleme devre dışı bırakma
Bir SQL Data Warehouse için bu adımları toodisable TDE izleyin:

1. Toohello bağlanmak *ana* bir yönetici veya hello üyesi olan bir oturum açma kullanılarak veritabanı **dbmanager** hello ana veritabanı rolü
2. Deyimi tooencrypt hello veritabanı aşağıdaki hello yürütün.

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> Duraklatılmış SQL Data Warehouse toohello TDE ayarları değişiklik yapmadan önce sürdürüldü gerekir.
> 
> 

## <a name="verifying-encryption"></a>Şifreleme doğrulama
bir SQL Data Warehouse için tooverify şifreleme durumu hello adımları izleyin:

1. Toohello bağlanmak *ana* ya da bir yönetici veya hello üyesi olan bir oturum açma kullanarak örnek veritabanı **dbmanager** hello ana veritabanı rolü
2. Deyimi tooencrypt hello veritabanı aşağıdaki hello yürütün.

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

Sonucunu ```1``` şifrelenmiş bir veritabanı gösterir ```0``` şifrelenmemiş bir veritabanını gösterir.

## <a name="encryption-dmvs"></a>Şifreleme Dmv'leri
* [sys.Databases][sys.databases] 
* [sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
