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
# <a name="get-started-with-transparent-data-encryption-tde"></a><span data-ttu-id="7d1ac-103">Saydam veri şifreleme (TDE) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="7d1ac-103">Get started with Transparent Data Encryption (TDE)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7d1ac-104">Güvenlik genel bakış</span><span class="sxs-lookup"><span data-stu-id="7d1ac-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="7d1ac-105">Kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="7d1ac-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="7d1ac-106">Şifreleme (Portal)</span><span class="sxs-lookup"><span data-stu-id="7d1ac-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="7d1ac-107">Şifreleme (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="7d1ac-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="7d1ac-108">Gerekli izinleri</span><span class="sxs-lookup"><span data-stu-id="7d1ac-108">Required Permssions</span></span>
<span data-ttu-id="7d1ac-109">tooenable saydam veri şifreleme (TDE), bir yönetici veya hello dbmanager rolünün bir üyesi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d1ac-109">tooenable Transparent Data Encryption (TDE), you must be an administrator or a member of hello dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="7d1ac-110">Şifrelemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="7d1ac-110">Enabling Encryption</span></span>
<span data-ttu-id="7d1ac-111">Bir SQL Data Warehouse için bu adımları tooenable TDE izleyin:</span><span class="sxs-lookup"><span data-stu-id="7d1ac-111">Follow these steps tooenable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="7d1ac-112">Toohello bağlanmak *ana* hello sunucusundaki bir yönetici veya hello üyesi olan bir oturum açma kullanarak hello veritabanı barındırma veritabanı **dbmanager** hello ana veritabanı rolü</span><span class="sxs-lookup"><span data-stu-id="7d1ac-112">Connect toohello *master* database on hello server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="7d1ac-113">Deyimi tooencrypt hello veritabanı aşağıdaki hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="7d1ac-113">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="7d1ac-114">Şifreleme devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="7d1ac-114">Disabling Encryption</span></span>
<span data-ttu-id="7d1ac-115">Bir SQL Data Warehouse için bu adımları toodisable TDE izleyin:</span><span class="sxs-lookup"><span data-stu-id="7d1ac-115">Follow these steps toodisable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="7d1ac-116">Toohello bağlanmak *ana* bir yönetici veya hello üyesi olan bir oturum açma kullanılarak veritabanı **dbmanager** hello ana veritabanı rolü</span><span class="sxs-lookup"><span data-stu-id="7d1ac-116">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="7d1ac-117">Deyimi tooencrypt hello veritabanı aşağıdaki hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="7d1ac-117">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> <span data-ttu-id="7d1ac-118">Duraklatılmış SQL Data Warehouse toohello TDE ayarları değişiklik yapmadan önce sürdürüldü gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d1ac-118">A paused SQL Data Warehouse must be resumed before making changes toohello TDE settings.</span></span>
> 
> 

## <a name="verifying-encryption"></a><span data-ttu-id="7d1ac-119">Şifreleme doğrulama</span><span class="sxs-lookup"><span data-stu-id="7d1ac-119">Verifying Encryption</span></span>
<span data-ttu-id="7d1ac-120">bir SQL Data Warehouse için tooverify şifreleme durumu hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7d1ac-120">tooverify encryption status for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="7d1ac-121">Toohello bağlanmak *ana* ya da bir yönetici veya hello üyesi olan bir oturum açma kullanarak örnek veritabanı **dbmanager** hello ana veritabanı rolü</span><span class="sxs-lookup"><span data-stu-id="7d1ac-121">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="7d1ac-122">Deyimi tooencrypt hello veritabanı aşağıdaki hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="7d1ac-122">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="7d1ac-123">Sonucunu ```1``` şifrelenmiş bir veritabanı gösterir ```0``` şifrelenmemiş bir veritabanını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7d1ac-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

## <a name="encryption-dmvs"></a><span data-ttu-id="7d1ac-124">Şifreleme Dmv'leri</span><span class="sxs-lookup"><span data-stu-id="7d1ac-124">Encryption DMVs</span></span>
* <span data-ttu-id="7d1ac-125">[sys.Databases][sys.databases]</span><span class="sxs-lookup"><span data-stu-id="7d1ac-125">[sys.databases][sys.databases]</span></span> 
* <span data-ttu-id="7d1ac-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="7d1ac-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
