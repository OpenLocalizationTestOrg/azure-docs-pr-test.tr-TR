---
title: "Saydam veri şifreleme SQL Data warehouse'da (T-SQL) | Microsoft Docs"
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
ms.openlocfilehash: 74c9032aababdce91ed617cd7a4c628915b42504
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a><span data-ttu-id="65dc9-103">Saydam veri şifreleme (TDE) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="65dc9-103">Get started with Transparent Data Encryption (TDE)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="65dc9-104">Güvenlik genel bakış</span><span class="sxs-lookup"><span data-stu-id="65dc9-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="65dc9-105">Kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="65dc9-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="65dc9-106">Şifreleme (Portal)</span><span class="sxs-lookup"><span data-stu-id="65dc9-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="65dc9-107">Şifreleme (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="65dc9-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="65dc9-108">Gerekli izinleri</span><span class="sxs-lookup"><span data-stu-id="65dc9-108">Required Permssions</span></span>
<span data-ttu-id="65dc9-109">Saydam veri şifreleme (TDE) etkinleştirmek için bir yönetici veya dbmanager rolünün bir üyesi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="65dc9-109">To enable Transparent Data Encryption (TDE), you must be an administrator or a member of the dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="65dc9-110">Şifrelemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="65dc9-110">Enabling Encryption</span></span>
<span data-ttu-id="65dc9-111">Bir SQL Data Warehouse için TDE etkinleştirmek için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="65dc9-111">Follow these steps to enable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="65dc9-112">Bağlanmak *ana* bir yönetici veya bir üyesi olan bir oturum açma kullanarak veritabanını barındıran sunucuda veritabanı **dbmanager** ana veritabanı rolü</span><span class="sxs-lookup"><span data-stu-id="65dc9-112">Connect to the *master* database on the server hosting the database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="65dc9-113">Veritabanı şifrelemek için şu deyimi yürütün.</span><span class="sxs-lookup"><span data-stu-id="65dc9-113">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="65dc9-114">Şifreleme devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="65dc9-114">Disabling Encryption</span></span>
<span data-ttu-id="65dc9-115">Bir SQL Data Warehouse için TDE devre dışı bırakmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="65dc9-115">Follow these steps to disable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="65dc9-116">Bağlanmak *ana* bir yönetici veya bir üyesi olan bir oturum açma kullanılarak veritabanı **dbmanager** ana veritabanı rolü</span><span class="sxs-lookup"><span data-stu-id="65dc9-116">Connect to the *master* database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="65dc9-117">Veritabanı şifrelemek için şu deyimi yürütün.</span><span class="sxs-lookup"><span data-stu-id="65dc9-117">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> <span data-ttu-id="65dc9-118">Duraklatılmış SQL Data Warehouse TDE ayarlarına değişiklik yapmadan önce sürdürüldü gerekir.</span><span class="sxs-lookup"><span data-stu-id="65dc9-118">A paused SQL Data Warehouse must be resumed before making changes to the TDE settings.</span></span>
> 
> 

## <a name="verifying-encryption"></a><span data-ttu-id="65dc9-119">Şifreleme doğrulama</span><span class="sxs-lookup"><span data-stu-id="65dc9-119">Verifying Encryption</span></span>
<span data-ttu-id="65dc9-120">Bir SQL Data Warehouse için şifreleme durumunu doğrulamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="65dc9-120">To verify encryption status for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="65dc9-121">Bağlanmak *ana* ya da bir yönetici veya bir üyesi olan bir oturum açma kullanarak örnek veritabanı **dbmanager** ana veritabanı rolü</span><span class="sxs-lookup"><span data-stu-id="65dc9-121">Connect to the *master* or instance database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="65dc9-122">Veritabanı şifrelemek için şu deyimi yürütün.</span><span class="sxs-lookup"><span data-stu-id="65dc9-122">Execute the following statement to encrypt the database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="65dc9-123">Sonucunu ```1``` şifrelenmiş bir veritabanı gösterir ```0``` şifrelenmemiş bir veritabanını gösterir.</span><span class="sxs-lookup"><span data-stu-id="65dc9-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

## <a name="encryption-dmvs"></a><span data-ttu-id="65dc9-124">Şifreleme Dmv'leri</span><span class="sxs-lookup"><span data-stu-id="65dc9-124">Encryption DMVs</span></span>
* <span data-ttu-id="65dc9-125">[sys.Databases][sys.databases]</span><span class="sxs-lookup"><span data-stu-id="65dc9-125">[sys.databases][sys.databases]</span></span> 
* <span data-ttu-id="65dc9-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="65dc9-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
