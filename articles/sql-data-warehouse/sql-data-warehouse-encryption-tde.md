---
title: "aaaTransparent veri şifrelemesi SQL Data warehouse'da (Portal) | Microsoft Docs"
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
ms.openlocfilehash: 8233886ecf170844104e0d1459e2a829cafa9b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a><span data-ttu-id="999fe-103">İle saydam veri şifreleme (TDE) SQL veri ambarı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="999fe-103">Get started with Transparent Data Encryption (TDE) in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="999fe-104">Güvenlik genel bakış</span><span class="sxs-lookup"><span data-stu-id="999fe-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="999fe-105">Kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="999fe-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="999fe-106">Şifreleme (Portal)</span><span class="sxs-lookup"><span data-stu-id="999fe-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="999fe-107">Şifreleme (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="999fe-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="999fe-108">Gerekli izinleri</span><span class="sxs-lookup"><span data-stu-id="999fe-108">Required Permssions</span></span>
<span data-ttu-id="999fe-109">tooenable saydam veri şifreleme (TDE), bir yönetici veya hello dbmanager rolünün bir üyesi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="999fe-109">tooenable Transparent Data Encryption (TDE), you must be an administrator or a member of hello dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="999fe-110">Şifrelemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="999fe-110">Enabling Encryption</span></span>
<span data-ttu-id="999fe-111">tooenable TDE bir SQL Data Warehouse için hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="999fe-111">tooenable TDE for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="999fe-112">Merhaba açık hello veritabanında [Azure portalı](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="999fe-112">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="999fe-113">Merhaba veritabanı dikey penceresinde hello tıklayın **ayarları** düğmesi</span><span class="sxs-lookup"><span data-stu-id="999fe-113">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="999fe-114">Select hello **saydam veri şifreleme** seçeneği![][1]</span><span class="sxs-lookup"><span data-stu-id="999fe-114">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="999fe-115">Select hello **üzerinde** ayarı![][2]</span><span class="sxs-lookup"><span data-stu-id="999fe-115">Select hello **On** setting ![][2]</span></span>
5. <span data-ttu-id="999fe-116">Seçin **Kaydet**
   ![][3]</span><span class="sxs-lookup"><span data-stu-id="999fe-116">Select **Save**
![][3]</span></span>  

## <a name="disabling-encryption"></a><span data-ttu-id="999fe-117">Şifreleme devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="999fe-117">Disabling Encryption</span></span>
<span data-ttu-id="999fe-118">toodisable TDE bir SQL Data Warehouse için hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="999fe-118">toodisable TDE for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="999fe-119">Merhaba açık hello veritabanında [Azure portalı](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="999fe-119">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="999fe-120">Merhaba veritabanı dikey penceresinde hello tıklayın **ayarları** düğmesi</span><span class="sxs-lookup"><span data-stu-id="999fe-120">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="999fe-121">Select hello **saydam veri şifreleme** seçeneği![][1]</span><span class="sxs-lookup"><span data-stu-id="999fe-121">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="999fe-122">Select hello **kapalı** ayarı![][4]</span><span class="sxs-lookup"><span data-stu-id="999fe-122">Select hello **Off** setting ![][4]</span></span>
5. <span data-ttu-id="999fe-123">Seçin **Kaydet**
   ![][5]</span><span class="sxs-lookup"><span data-stu-id="999fe-123">Select **Save**
![][5]</span></span>  

## <a name="encryption-dmvs"></a><span data-ttu-id="999fe-124">Şifreleme Dmv'leri</span><span class="sxs-lookup"><span data-stu-id="999fe-124">Encryption DMVs</span></span>
<span data-ttu-id="999fe-125">Şifreleme ile Dmv'leri aşağıdaki hello onaylanabilir:</span><span class="sxs-lookup"><span data-stu-id="999fe-125">Encryption can be confirmed with hello following DMVs:</span></span>

* <span data-ttu-id="999fe-126">[sys.Databases]</span><span class="sxs-lookup"><span data-stu-id="999fe-126">[sys.databases]</span></span>
* <span data-ttu-id="999fe-127">[sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="999fe-127">[sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.Databases]: http://msdn.microsoft.com/library/ms178534.aspx
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
