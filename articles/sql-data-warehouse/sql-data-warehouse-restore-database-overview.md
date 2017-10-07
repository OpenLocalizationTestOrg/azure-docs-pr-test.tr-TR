---
title: "Azure veri ambarı - yerel ve coğrafi olarak yedekli aaaRestore | Microsoft Docs"
description: "Azure SQL Data Warehouse bir veritabanına kurtarmak için hello veritabanı geri yükleme seçeneklerine genel bakış."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: a96b898372b29d420e1416ca93a172ff8af47fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-restore"></a><span data-ttu-id="a6493-103">SQL veri ambarı geri yükleme</span><span class="sxs-lookup"><span data-stu-id="a6493-103">SQL Data Warehouse restore</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="a6493-104">[Genel bakış][Overview]</span><span class="sxs-lookup"><span data-stu-id="a6493-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="a6493-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="a6493-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="a6493-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="a6493-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="a6493-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="a6493-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="a6493-108">SQL veri ambarı hem yerel hem de coğrafi geri yükleme, veri ambarı olağanüstü bir parçası olarak kurtarma özellikleri sunar.</span><span class="sxs-lookup"><span data-stu-id="a6493-108">SQL Data Warehouse offers both local and geographical restores as part of its data warehouse disaster recovery capabilities.</span></span> <span data-ttu-id="a6493-109">Veri ambarı tooa geri yüklemenizin hello birincil bölgede noktası veya coğrafi olarak yedekli yedeklemeleri toorestore tooa farklı coğrafi bölge kullanın veri ambarı yedeklemeleri toorestore kullanın.</span><span class="sxs-lookup"><span data-stu-id="a6493-109">Use data warehouse backups toorestore your data warehouse tooa restore point in hello primary region, or use geo-redundant backups toorestore tooa different geographical region.</span></span> <span data-ttu-id="a6493-110">Bu makalede, bir veri ambarı geri yüklenmesi hello özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a6493-110">This article explains hello specifics of restoring a data warehouse.</span></span>

## <a name="what-is-a-data-warehouse-restore"></a><span data-ttu-id="a6493-111">Veri ambarı geri nedir?</span><span class="sxs-lookup"><span data-stu-id="a6493-111">What is a data warehouse restore?</span></span>
<span data-ttu-id="a6493-112">Bir veri ambarı geri yükleme, varolan bir yedek kopyadan oluşturulan yeni veri ambarı veya silinen veri ambarı ' dir.</span><span class="sxs-lookup"><span data-stu-id="a6493-112">A data warehouse restore is a new data warehouse that is created from a backup of an existing or deleted data warehouse.</span></span> <span data-ttu-id="a6493-113">Merhaba geri yüklenen veri ambarı hello yedeklenen veri ambarı belirli bir zamanda yeniden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a6493-113">hello restored data warehouse re-creates hello backed-up data warehouse at a specific time.</span></span> <span data-ttu-id="a6493-114">SQL veri ambarı dağıtılmış bir sistemde olduğundan, bir veri ambarı geri yükleme dosyalarından Azure BLOB'ları depolanan birçok yedekleme oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a6493-114">Since SQL Data Warehouse is a distributed system, a data warehouse restore is created from many backup files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="a6493-115">Veritabanı geri yükleme tüm iş sürekliliği ve olağanüstü durum kurtarma stratejisi önemli bir parçası olduğundan, verilerinizin yanlışlıkla Bozulması veya silme işlemi sonrasında yeniden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a6493-115">Database restore is an essential part of any business continuity and disaster recovery strategy because it re-creates your data after accidental corruption or deletion.</span></span>

<span data-ttu-id="a6493-116">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="a6493-116">For more information, see:</span></span>

* [<span data-ttu-id="a6493-117">SQL veri ambarı yedekleri</span><span class="sxs-lookup"><span data-stu-id="a6493-117">SQL Data Warehouse backups</span></span>](sql-data-warehouse-backups.md)
* [<span data-ttu-id="a6493-118">İş sürekliliğine genel bakış</span><span class="sxs-lookup"><span data-stu-id="a6493-118">Business continuity overview</span></span>](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a><span data-ttu-id="a6493-119">Veri ambarı geri yükleme noktaları</span><span class="sxs-lookup"><span data-stu-id="a6493-119">Data warehouse restore points</span></span>
<span data-ttu-id="a6493-120">Azure Premium Storage kullanmanın avantajı Azure Storage Blobuna anlık görüntüleri toobackup hello birincil veri ambarı SQL Data Warehouse kullanır.</span><span class="sxs-lookup"><span data-stu-id="a6493-120">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots toobackup hello primary data warehouse.</span></span> <span data-ttu-id="a6493-121">Başlangıç zamanı temsil eden bir geri yükleme noktası her anlık görüntü var hello anlık görüntü başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="a6493-121">Each snapshot has a restore point that represents hello time hello snapshot started.</span></span> <span data-ttu-id="a6493-122">bir geri yükleme noktası seçin ve geri yükleme komutu toorestore bir veri ambarı.</span><span class="sxs-lookup"><span data-stu-id="a6493-122">toorestore a data warehouse, you choose a restore point and issue a restore command.</span></span>  

<span data-ttu-id="a6493-123">SQL Data Warehouse, her zaman hello yedekleme tooa yeni veri ambarı geri yükler.</span><span class="sxs-lookup"><span data-stu-id="a6493-123">SQL Data Warehouse always restores hello backup tooa new data warehouse.</span></span> <span data-ttu-id="a6493-124">Merhaba geri yüklenen veri ambarı tutmak geçerli bir hello veya bunlardan birini silin.</span><span class="sxs-lookup"><span data-stu-id="a6493-124">You can either keep hello restored data warehouse and hello current one, or delete one of them.</span></span> <span data-ttu-id="a6493-125">Tooreplace hello geçerli istiyorsanız hello veri ambarına veri ambarını geri, onu yeniden adlandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6493-125">If you want tooreplace hello current data warehouse with hello restored data warehouse, you can rename it.</span></span>

<span data-ttu-id="a6493-126">Toorestore silinmiş ya da duraklatılmış veri ambarı gerekiyorsa, yapabilecekleriniz [destek bileti oluşturma](sql-data-warehouse-get-started-create-support-ticket.md).</span><span class="sxs-lookup"><span data-stu-id="a6493-126">If you need toorestore a deleted or paused data warehouse, you can [create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span></span> 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a><span data-ttu-id="a6493-127">Coğrafi olarak yedekli geri yükleme</span><span class="sxs-lookup"><span data-stu-id="a6493-127">Geo-redundant restore</span></span>
<span data-ttu-id="a6493-128">Azure SQL Data Warehouse, seçilen performans düzeyinde destekleyen, veri ambarı tooany bölgesi geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6493-128">You can restore your data warehouse tooany region supporting Azure SQL Data Warehouse at your chosen performance level.</span></span> <span data-ttu-id="a6493-129">9000 ve 18000 DWU desteklenmez, tüm bölgelerde hello Önizleme sırasında unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a6493-129">Please note that 9000 and 18000 DWU are not supported in all regions during hello preview.</span></span>

> [!NOTE]
> <span data-ttu-id="a6493-130">bir coğrafi olarak yedekli tooperform geri yükleme, bu özellik dışında çevirdiniz gerekir değil.</span><span class="sxs-lookup"><span data-stu-id="a6493-130">tooperform a geo-redundant restore you must not have opted out of this feature.</span></span>
> 
> 

## <a name="restore-timeline"></a><span data-ttu-id="a6493-131">Zaman çizelgesi geri yükleme</span><span class="sxs-lookup"><span data-stu-id="a6493-131">Restore timeline</span></span>
<span data-ttu-id="a6493-132">Son yedi günde bir veritabanı tooany kullanılabilir geri yükleme noktası hello içinde geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6493-132">You can restore a database tooany available restore point within hello last seven days.</span></span> <span data-ttu-id="a6493-133">Anlık görüntüler, dört tooeight saatte başlatmak ve yedi gün için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a6493-133">Snapshots start every four tooeight hours and are available for seven days.</span></span> <span data-ttu-id="a6493-134">Bir anlık görüntü yedi günden daha eski olduğunda süresi dolmadan ve geri yükleme noktası artık kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="a6493-134">When a snapshot is older than seven days, it expires and its restore point is no longer available.</span></span>

## <a name="restore-costs"></a><span data-ttu-id="a6493-135">Maliyetleri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="a6493-135">Restore costs</span></span>
<span data-ttu-id="a6493-136">hello Azure Premium Storage hızında hello geri yüklenen veri ambarı için Hello depolama ücret faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="a6493-136">hello storage charge for hello restored data warehouse is billed at hello Azure Premium Storage rate.</span></span> 

<span data-ttu-id="a6493-137">Geri yüklenen veri ambarı durdurursanız hello Azure Premium Storage hızında depolama için ücretlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6493-137">If you pause a restored data warehouse, you are charged for storage at hello Azure Premium Storage rate.</span></span> <span data-ttu-id="a6493-138">duraklatma hello avantajı hello DWU bilgi işlem kaynakları için sizden ücret istenmese olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="a6493-138">hello advantage of pausing is you are not charged for hello DWU computing resources.</span></span>

<span data-ttu-id="a6493-139">SQL Data Warehouse fiyatlandırması hakkında daha fazla bilgi için bkz: [SQL Data Warehouse fiyatlandırması](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="a6493-139">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="uses-for-restore"></a><span data-ttu-id="a6493-140">Geri yükleme için de kullanır</span><span class="sxs-lookup"><span data-stu-id="a6493-140">Uses for restore</span></span>
<span data-ttu-id="a6493-141">Merhaba birincil veri ambarı geri yüklemek için toorecover veri yanlışlıkla veri kaybı veya bozulması sonra kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a6493-141">hello primary use for data warehouse restore is toorecover data after accidental data loss or corruption.</span></span>

<span data-ttu-id="a6493-142">Veri ambarı geri yükleme tooretain bir yedekleme, yedi günden daha uzun için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6493-142">You can also use data warehouse restore tooretain a backup for longer than seven days.</span></span> <span data-ttu-id="a6493-143">Merhaba yedekleme geri yüklendikten sonra hello veri ambarı çevrimiçi sahip ve duraklatabilir süresiz olarak toosave işlem maliyetleri.</span><span class="sxs-lookup"><span data-stu-id="a6493-143">Once hello backup is restored, you have hello data warehouse online and can pause it indefinitely toosave compute costs.</span></span> <span data-ttu-id="a6493-144">Merhaba duraklatılmış veritabanı depolama ücretleri hello Azure Premium Storage hızında doğurur.</span><span class="sxs-lookup"><span data-stu-id="a6493-144">hello paused database incurs storage charges at hello Azure Premium Storage rate.</span></span> 

## <a name="related-topics"></a><span data-ttu-id="a6493-145">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="a6493-145">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="a6493-146">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="a6493-146">Scenarios</span></span>
* <span data-ttu-id="a6493-147">İş sürekliliğine genel bakış için bkz: [iş sürekliliğine genel bakış](../sql-database/sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="a6493-147">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

<span data-ttu-id="a6493-148">veri ambarı tooperform geri yükleme, kullanarak geri yükleyin:</span><span class="sxs-lookup"><span data-stu-id="a6493-148">tooperform a data warehouse restore, restore using:</span></span>

* <span data-ttu-id="a6493-149">Azure portal, bkz: [hello Azure portal kullanarak bir veri ambarı geri yükle](sql-data-warehouse-restore-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a6493-149">Azure portal, see [Restore a data warehouse using hello Azure portal](sql-data-warehouse-restore-database-portal.md)</span></span>
* <span data-ttu-id="a6493-150">PowerShell cmdlet'leri görmek [PowerShell cmdlet'lerini kullanarak bir veri ambarı geri yükle](sql-data-warehouse-restore-database-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="a6493-150">PowerShell cmdlets, see [Restore a data warehouse using PowerShell cmdlets](sql-data-warehouse-restore-database-powershell.md)</span></span>
* <span data-ttu-id="a6493-151">REST API için bkz: [hello REST API'lerini kullanarak bir veri ambarı geri yükle](sql-data-warehouse-restore-database-rest-api.md)</span><span class="sxs-lookup"><span data-stu-id="a6493-151">REST APIs, see [Restore a data warehouse using hello REST APIs](sql-data-warehouse-restore-database-rest-api.md)</span></span>

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
