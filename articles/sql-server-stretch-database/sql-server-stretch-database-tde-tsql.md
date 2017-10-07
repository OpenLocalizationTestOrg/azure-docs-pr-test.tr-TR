---
title: "Saydam veri şifreleme için Esnetme veritabanı TSQL - Azure aaaEnable | Microsoft Docs"
description: "Saydam veri şifreleme (TDE) Azure TSQL üzerinde SQL Server Esnetme veritabanı için etkinleştirin"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: jhubbard
editor: 
ms.assetid: 27753d91-9ca2-4d47-b34d-b5e2c2f029bb
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: anvang
ms.openlocfilehash: a9ba23649656fb344480d79438a1115f0eb353bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a>Saydam veri şifreleme (TDE) Azure (Transact-SQL) üzerinde Esnetme veritabanı için etkinleştirin
> [!div class="op_single_selector"]
> * [Azure portal](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Saydam veri şifreleme (TDE) gerçek zamanlı şifreleme ve şifre çözme hello veritabanının, ilişkili yedeklemelerinizi ve geri kalan işlem günlüğü dosyalarını değişiklikleri toohello gerek kalmadan gerçekleştirerek kötü amaçlı etkinliği hello tehdide karşı korunmasına yardımcı olur. uygulama.

TDE, bir simetrik anahtar adlı hello veritabanı şifreleme anahtarı kullanarak veritabanının tamamını hello depolanmasını şifreler. Merhaba veritabanı şifreleme anahtarı, bir yerleşik bir sunucu sertifikası tarafından korunur. Merhaba yerleşik bir sunucu sertifikası Azure her sunucu için benzersizdir. Microsoft, bu sertifikalar otomatik olarak en az 90 günde döndürür. TDE genel bir açıklaması için bkz [saydam veri şifreleme (TDE)].

## <a name="enabling-encryption"></a>Şifrelemeyi etkinleştirme
bir SQL Server Esnetme etkinleştirilmiş veritabanından veri geçişi hello depolama Azure bir veritabanı için tooenable TDE hello şeyler aşağıdaki:

1. Toohello bağlanmak *ana* bir yönetici veya hello üyesi olan bir oturum açma kullanılarak hello Azure sunucusu barındırma hello veritabanı üzerinde veritabanı **dbmanager** hello ana veritabanı rolü
2. Deyimi tooencrypt hello veritabanı aşağıdaki hello yürütün.

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>Şifreleme devre dışı bırakma
bir SQL Server Esnetme etkinleştirilmiş veritabanından veri geçişi hello depolama Azure bir veritabanı için toodisable TDE hello şeyler aşağıdaki:

1. Toohello bağlanmak *ana* bir yönetici veya hello üyesi olan bir oturum açma kullanılarak veritabanı **dbmanager** hello ana veritabanı rolü
2. Deyimi tooencrypt hello veritabanı aşağıdaki hello yürütün.

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a>Şifreleme doğrulama
bir SQL Server Esnetme etkinleştirilmiş veritabanından veri geçişi hello depolama Azure bir veritabanı için tooverify şifreleme durum hello şeyler aşağıdaki:

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

<!--Anchors-->
[saydam veri şifreleme (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
