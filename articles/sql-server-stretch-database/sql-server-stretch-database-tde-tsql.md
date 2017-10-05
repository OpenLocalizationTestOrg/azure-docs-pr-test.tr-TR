---
title: "Saydam veri şifreleme Esnetme veritabanı TSQL - Azure için etkinleştirme | Microsoft Docs"
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
ms.openlocfilehash: ed26c2b386e08b76f78b4a05e12c46d2b97c20f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a><span data-ttu-id="a70f2-103">Saydam veri şifreleme (TDE) Azure (Transact-SQL) üzerinde Esnetme veritabanı için etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="a70f2-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure (Transact-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a70f2-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="a70f2-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="a70f2-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="a70f2-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="a70f2-106">Saydam veri şifreleme (TDE) gerçek zamanlı şifreleme ve şifre çözme veritabanının, ilişkili yedeklemelerinizi ve geri kalan işlem günlüğü dosyalarını uygulamasında yapılacak değişiklikler gerek kalmadan gerçekleştirerek kötü amaçlı etkinliği tehdide karşı korunmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a70f2-106">Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span></span>

<span data-ttu-id="a70f2-107">TDE, veritabanının tamamını Depolama veritabanı şifreleme anahtarını adlı bir simetrik anahtar kullanarak şifreler.</span><span class="sxs-lookup"><span data-stu-id="a70f2-107">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="a70f2-108">Veritabanı şifreleme anahtarını bir yerleşik bir sunucu sertifikası tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="a70f2-108">The database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="a70f2-109">Yerleşik bir sunucu sertifikası Azure her sunucu için benzersizdir.</span><span class="sxs-lookup"><span data-stu-id="a70f2-109">The built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="a70f2-110">Microsoft, bu sertifikalar otomatik olarak en az 90 günde döndürür.</span><span class="sxs-lookup"><span data-stu-id="a70f2-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="a70f2-111">TDE genel bir açıklaması için bkz [saydam veri şifreleme (TDE)].</span><span class="sxs-lookup"><span data-stu-id="a70f2-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="a70f2-112">Şifrelemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="a70f2-112">Enabling Encryption</span></span>
<span data-ttu-id="a70f2-113">TDE Azure etkinleştirmek için bir SQL Server Esnetme etkinleştirilmiş veritabanından veri depolama veritabanı geçişi, şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="a70f2-113">To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="a70f2-114">Bağlanmak *ana* veritabanından bir yönetici veya bir üyesi olan bir oturum açma kullanarak veritabanını barındıran Azure sunucusuna **dbmanager** ana veritabanı rolü</span><span class="sxs-lookup"><span data-stu-id="a70f2-114">Connect to the *master* database on the Azure server hosting the database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="a70f2-115">Veritabanı şifrelemek için şu deyimi yürütün.</span><span class="sxs-lookup"><span data-stu-id="a70f2-115">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="a70f2-116">Şifreleme devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="a70f2-116">Disabling Encryption</span></span>
<span data-ttu-id="a70f2-117">Azure TDE devre dışı bırakmak için bir SQL Server Esnetme etkinleştirilmiş veritabanından veri depolama veritabanı geçişi, şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="a70f2-117">To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="a70f2-118">Bağlanmak *ana* bir yönetici veya bir üyesi olan bir oturum açma kullanılarak veritabanı **dbmanager** ana veritabanı rolü</span><span class="sxs-lookup"><span data-stu-id="a70f2-118">Connect to the *master* database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="a70f2-119">Veritabanı şifrelemek için şu deyimi yürütün.</span><span class="sxs-lookup"><span data-stu-id="a70f2-119">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a><span data-ttu-id="a70f2-120">Şifreleme doğrulama</span><span class="sxs-lookup"><span data-stu-id="a70f2-120">Verifying Encryption</span></span>
<span data-ttu-id="a70f2-121">Bir SQL Server Esnetme etkinleştirilmiş veritabanından verileri depolarken bir Azure veritabanı için şifreleme durum geçişi doğrulamak için şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="a70f2-121">To verify encryption status for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="a70f2-122">Bağlanmak *ana* ya da bir yönetici veya bir üyesi olan bir oturum açma kullanarak örnek veritabanı **dbmanager** ana veritabanı rolü</span><span class="sxs-lookup"><span data-stu-id="a70f2-122">Connect to the *master* or instance database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="a70f2-123">Veritabanı şifrelemek için şu deyimi yürütün.</span><span class="sxs-lookup"><span data-stu-id="a70f2-123">Execute the following statement to encrypt the database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="a70f2-124">Sonucunu ```1``` şifrelenmiş bir veritabanı gösterir ```0``` şifrelenmemiş bir veritabanını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a70f2-124">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

<!--Anchors-->
<span data-ttu-id="a70f2-125">[saydam veri şifreleme (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span><span class="sxs-lookup"><span data-stu-id="a70f2-125">[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span></span>


<!--Image references-->

<!--Link references-->
