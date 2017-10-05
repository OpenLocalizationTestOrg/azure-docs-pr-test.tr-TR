---
title: "Saydam veri şifreleme SQL Data warehouse'da (Portal) | Microsoft Docs"
description: "SQL Data warehouse'da saydam veri şifreleme (TDE)"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: fabf75d3-9bbf-4e0d-9b31-8b5a8713f08d
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: b1db3bdfdfb54bda325c9b971cfcb4dd5efa333a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a><span data-ttu-id="cf1c6-103">İle saydam veri şifreleme (TDE) SQL veri ambarı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="cf1c6-103">Get started with Transparent Data Encryption (TDE) in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cf1c6-104">Güvenlik genel bakış</span><span class="sxs-lookup"><span data-stu-id="cf1c6-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="cf1c6-105">Kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="cf1c6-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="cf1c6-106">Şifreleme (Portal)</span><span class="sxs-lookup"><span data-stu-id="cf1c6-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="cf1c6-107">Şifreleme (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="cf1c6-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="cf1c6-108">Gerekli izinleri</span><span class="sxs-lookup"><span data-stu-id="cf1c6-108">Required Permssions</span></span>
<span data-ttu-id="cf1c6-109">Saydam veri şifreleme (TDE) etkinleştirmek için bir yönetici veya dbmanager rolünün bir üyesi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cf1c6-109">To enable Transparent Data Encryption (TDE), you must be an administrator or a member of the dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="cf1c6-110">Şifrelemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="cf1c6-110">Enabling Encryption</span></span>
<span data-ttu-id="cf1c6-111">Bir SQL Data Warehouse için TDE etkinleştirmek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="cf1c6-111">To enable TDE for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="cf1c6-112">Veritabanında açmak [Azure portalı](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="cf1c6-112">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="cf1c6-113">Veritabanı dikey penceresinde tıklayın **ayarları** düğmesi</span><span class="sxs-lookup"><span data-stu-id="cf1c6-113">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="cf1c6-114">Seçin **saydam veri şifreleme** seçeneği![][1]</span><span class="sxs-lookup"><span data-stu-id="cf1c6-114">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="cf1c6-115">Seçin **üzerinde** ayarı![][2]</span><span class="sxs-lookup"><span data-stu-id="cf1c6-115">Select the **On** setting ![][2]</span></span>
5. <span data-ttu-id="cf1c6-116">Seçin **Kaydet**
   ![][3]</span><span class="sxs-lookup"><span data-stu-id="cf1c6-116">Select **Save**
![][3]</span></span>  

## <a name="disabling-encryption"></a><span data-ttu-id="cf1c6-117">Şifreleme devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="cf1c6-117">Disabling Encryption</span></span>
<span data-ttu-id="cf1c6-118">Bir SQL Data Warehouse için TDE devre dışı bırakmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="cf1c6-118">To disable TDE for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="cf1c6-119">Veritabanında açmak [Azure portalı](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="cf1c6-119">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="cf1c6-120">Veritabanı dikey penceresinde tıklayın **ayarları** düğmesi</span><span class="sxs-lookup"><span data-stu-id="cf1c6-120">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="cf1c6-121">Seçin **saydam veri şifreleme** seçeneği![][1]</span><span class="sxs-lookup"><span data-stu-id="cf1c6-121">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="cf1c6-122">Seçin **kapalı** ayarı![][4]</span><span class="sxs-lookup"><span data-stu-id="cf1c6-122">Select the **Off** setting ![][4]</span></span>
5. <span data-ttu-id="cf1c6-123">Seçin **Kaydet**
   ![][5]</span><span class="sxs-lookup"><span data-stu-id="cf1c6-123">Select **Save**
![][5]</span></span>  

## <a name="encryption-dmvs"></a><span data-ttu-id="cf1c6-124">Şifreleme Dmv'leri</span><span class="sxs-lookup"><span data-stu-id="cf1c6-124">Encryption DMVs</span></span>
<span data-ttu-id="cf1c6-125">Şifreleme ile aşağıdaki Dmv'leri onaylanabilir:</span><span class="sxs-lookup"><span data-stu-id="cf1c6-125">Encryption can be confirmed with the following DMVs:</span></span>

* <span data-ttu-id="cf1c6-126">[sys.Databases]</span><span class="sxs-lookup"><span data-stu-id="cf1c6-126">[sys.databases]</span></span>
* <span data-ttu-id="cf1c6-127">[sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="cf1c6-127">[sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
<span data-ttu-id="cf1c6-128">[sys.Databases]: http://msdn.microsoft.com/library/ms178534.aspx</span><span class="sxs-lookup"><span data-stu-id="cf1c6-128">[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx</span></span>
<span data-ttu-id="cf1c6-129">[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx</span><span class="sxs-lookup"><span data-stu-id="cf1c6-129">[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
