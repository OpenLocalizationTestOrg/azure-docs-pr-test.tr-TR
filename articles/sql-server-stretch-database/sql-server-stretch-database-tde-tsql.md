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
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a><span data-ttu-id="e74c9-103">Saydam veri şifreleme (TDE) Azure (Transact-SQL) üzerinde Esnetme veritabanı için etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="e74c9-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure (Transact-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e74c9-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="e74c9-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="e74c9-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="e74c9-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="e74c9-106">Saydam veri şifreleme (TDE) gerçek zamanlı şifreleme ve şifre çözme hello veritabanının, ilişkili yedeklemelerinizi ve geri kalan işlem günlüğü dosyalarını değişiklikleri toohello gerek kalmadan gerçekleştirerek kötü amaçlı etkinliği hello tehdide karşı korunmasına yardımcı olur. uygulama.</span><span class="sxs-lookup"><span data-stu-id="e74c9-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="e74c9-107">TDE, bir simetrik anahtar adlı hello veritabanı şifreleme anahtarı kullanarak veritabanının tamamını hello depolanmasını şifreler.</span><span class="sxs-lookup"><span data-stu-id="e74c9-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="e74c9-108">Merhaba veritabanı şifreleme anahtarı, bir yerleşik bir sunucu sertifikası tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="e74c9-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="e74c9-109">Merhaba yerleşik bir sunucu sertifikası Azure her sunucu için benzersizdir.</span><span class="sxs-lookup"><span data-stu-id="e74c9-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="e74c9-110">Microsoft, bu sertifikalar otomatik olarak en az 90 günde döndürür.</span><span class="sxs-lookup"><span data-stu-id="e74c9-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="e74c9-111">TDE genel bir açıklaması için bkz [saydam veri şifreleme (TDE)].</span><span class="sxs-lookup"><span data-stu-id="e74c9-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="e74c9-112">Şifrelemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="e74c9-112">Enabling Encryption</span></span>
<span data-ttu-id="e74c9-113">bir SQL Server Esnetme etkinleştirilmiş veritabanından veri geçişi hello depolama Azure bir veritabanı için tooenable TDE hello şeyler aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="e74c9-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="e74c9-114">Toohello bağlanmak *ana* bir yönetici veya hello üyesi olan bir oturum açma kullanılarak hello Azure sunucusu barındırma hello veritabanı üzerinde veritabanı **dbmanager** hello ana veritabanı rolü</span><span class="sxs-lookup"><span data-stu-id="e74c9-114">Connect toohello *master* database on hello Azure server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="e74c9-115">Deyimi tooencrypt hello veritabanı aşağıdaki hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="e74c9-115">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="e74c9-116">Şifreleme devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="e74c9-116">Disabling Encryption</span></span>
<span data-ttu-id="e74c9-117">bir SQL Server Esnetme etkinleştirilmiş veritabanından veri geçişi hello depolama Azure bir veritabanı için toodisable TDE hello şeyler aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="e74c9-117">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="e74c9-118">Toohello bağlanmak *ana* bir yönetici veya hello üyesi olan bir oturum açma kullanılarak veritabanı **dbmanager** hello ana veritabanı rolü</span><span class="sxs-lookup"><span data-stu-id="e74c9-118">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="e74c9-119">Deyimi tooencrypt hello veritabanı aşağıdaki hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="e74c9-119">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a><span data-ttu-id="e74c9-120">Şifreleme doğrulama</span><span class="sxs-lookup"><span data-stu-id="e74c9-120">Verifying Encryption</span></span>
<span data-ttu-id="e74c9-121">bir SQL Server Esnetme etkinleştirilmiş veritabanından veri geçişi hello depolama Azure bir veritabanı için tooverify şifreleme durum hello şeyler aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="e74c9-121">tooverify encryption status for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="e74c9-122">Toohello bağlanmak *ana* ya da bir yönetici veya hello üyesi olan bir oturum açma kullanarak örnek veritabanı **dbmanager** hello ana veritabanı rolü</span><span class="sxs-lookup"><span data-stu-id="e74c9-122">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="e74c9-123">Deyimi tooencrypt hello veritabanı aşağıdaki hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="e74c9-123">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="e74c9-124">Sonucunu ```1``` şifrelenmiş bir veritabanı gösterir ```0``` şifrelenmemiş bir veritabanını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e74c9-124">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

<!--Anchors-->
[saydam veri şifreleme (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
