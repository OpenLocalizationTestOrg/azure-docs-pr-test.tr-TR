---
title: "aaaAzure SQL Data Warehouse yedeklemeleri - anlık görüntüler, coğrafi olarak yedekli | Microsoft Docs"
description: "Bir Azure SQL Data Warehouse tooa geri yükleme noktası veya farklı coğrafi bölge toorestore etkinleştirmek SQL Data Warehouse yerleşik veritabanı yedeklemeleri hakkında bilgi edinin."
services: sql-data-warehouse
documentationcenter: 
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: b5aff094-05b2-4578-acf3-ec456656febd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 34659480485246f54a1490e185fc1b903fb2520d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-backups"></a><span data-ttu-id="e8324-103">SQL veri ambarı yedekleri</span><span class="sxs-lookup"><span data-stu-id="e8324-103">SQL Data Warehouse backups</span></span>
<span data-ttu-id="e8324-104">SQL veri ambarı veri ambarı yedekleme yeteneklerini bir parçası olarak hem yerel hem de coğrafi yedeklemeler sunar.</span><span class="sxs-lookup"><span data-stu-id="e8324-104">SQL Data Warehouse offers both local and geographical backups as part of its data warehouse backup capabilities.</span></span> <span data-ttu-id="e8324-105">Bunlar, Azure Storage Blobuna anlık görüntüler ve coğrafi olarak yedekli depolama içerir.</span><span class="sxs-lookup"><span data-stu-id="e8324-105">These include Azure Storage Blob snapshots and geo-redundant storage.</span></span> <span data-ttu-id="e8324-106">Veri ambarı tooa geri yüklemenizin hello birincil bölgede noktası veya tooa farklı coğrafi geri yükleme, veri ambarı yedeklemeleri toorestore kullanın.</span><span class="sxs-lookup"><span data-stu-id="e8324-106">Use data warehouse backups toorestore your data warehouse tooa restore point in hello primary region, or restore tooa different geographical region.</span></span> <span data-ttu-id="e8324-107">Bu makalede SQL Data Warehouse yedeklemelerin hello özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e8324-107">This article explains hello specifics of backups in SQL Data Warehouse.</span></span>

## <a name="what-is-a-data-warehouse-backup"></a><span data-ttu-id="e8324-108">Veri ambarı yedekleme nedir?</span><span class="sxs-lookup"><span data-stu-id="e8324-108">What is a data warehouse backup?</span></span>
<span data-ttu-id="e8324-109">Veri ambarı yedekleme, veri ambarı tooa belirli bir süre toorestore kullanabileceğiniz hello verilerdir.</span><span class="sxs-lookup"><span data-stu-id="e8324-109">A data warehouse backup is hello data that you can use toorestore a data warehouse tooa specific time.</span></span>  <span data-ttu-id="e8324-110">SQL veri ambarı dağıtılmış bir sistemde olduğundan, bir veri ambarı yedekleme Azure blob'larda depolanan çok sayıda dosya oluşur.</span><span class="sxs-lookup"><span data-stu-id="e8324-110">Since SQL Data Warehouse is a distributed system, a data warehouse backup consists of many files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="e8324-111">Verilerinizin yanlışlıkla Bozulması veya silme korumak için veritabanı yedeklemeleri tüm iş sürekliliği ve olağanüstü durum kurtarma stratejisi, önemli bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="e8324-111">Database backups are an essential part of any business continuity and disaster recovery strategy because they protect your data from accidental corruption or deletion.</span></span> <span data-ttu-id="e8324-112">Daha fazla bilgi için bkz: [iş sürekliliğine genel bakış](../sql-database/sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="e8324-112">For more information, see [Business continuity overview](../sql-database/sql-database-business-continuity.md).</span></span>

## <a name="data-redundancy"></a><span data-ttu-id="e8324-113">Veri yedekliği</span><span class="sxs-lookup"><span data-stu-id="e8324-113">Data redundancy</span></span>
<span data-ttu-id="e8324-114">SQL Data Warehouse, yerel olarak yedekli (LRS) Azure Premium Storage'da veri depolayarak verilerinizi korur.</span><span class="sxs-lookup"><span data-stu-id="e8324-114">SQL Data Warehouse protects your data by storing your data in locally redundant (LRS) Azure Premium Storage.</span></span> <span data-ttu-id="e8324-115">Yerelleştirilmiş hata varsa bu Azure depolama özellik hello verileri birden çok zaman uyumlu kopyası'nde hello yerel veri merkezi tooguarantee saydam veri koruma depolar.</span><span class="sxs-lookup"><span data-stu-id="e8324-115">This Azure Storage feature stores multiple synchronous copies of hello data in hello local data center tooguarantee transparent data protection if there are localized failures.</span></span> <span data-ttu-id="e8324-116">Verilerinizi disk hataları gibi altyapı sorunları varlığını sürdürmesi veri artıklık sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8324-116">Data redundancy ensures that your data can survive infrastructure issues such as disk failures.</span></span> <span data-ttu-id="e8324-117">Veri artıklığı bir hataya dayanıklı ile iş devamlılığı ve yüksek oranda kullanılabilir bir altyapı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8324-117">Data redundancy ensures business continuity with a fault tolerant and highly available infrastructure.</span></span>

<span data-ttu-id="e8324-118">toolearn hakkında daha fazla bilgi:</span><span class="sxs-lookup"><span data-stu-id="e8324-118">toolearn more about:</span></span>

* <span data-ttu-id="e8324-119">Azure Premium depolama bkz [giriş tooAzure Premium depolama](../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="e8324-119">Azure Premium storage, see [Introduction tooAzure Premium Storage](../storage/common/storage-premium-storage.md).</span></span>
* <span data-ttu-id="e8324-120">Yerel olarak yedekli depolama bkz [Azure Storage çoğaltma](../storage/common/storage-redundancy.md#locally-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="e8324-120">Locally Redundant storage, see [Azure Storage replication](../storage/common/storage-redundancy.md#locally-redundant-storage).</span></span>

## <a name="azure-storage-blob-snapshots"></a><span data-ttu-id="e8324-121">Azure depolama blobu anlık görüntüler</span><span class="sxs-lookup"><span data-stu-id="e8324-121">Azure Storage Blob snapshots</span></span>
<span data-ttu-id="e8324-122">Azure Premium Storage kullanmanın avantajı SQL Data Warehouse yerel olarak Azure Storage Blobuna anlık görüntüleri toobackup hello veri ambarı kullanır.</span><span class="sxs-lookup"><span data-stu-id="e8324-122">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots toobackup hello data warehouse locally.</span></span> <span data-ttu-id="e8324-123">Bir veri ambarı tooa anlık görüntü geri yükleme noktası geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8324-123">You can restore a data warehouse tooa snapshot restore point.</span></span> <span data-ttu-id="e8324-124">Anlık görüntüler her sekiz saatte en az başlatmak ve yedi gün için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e8324-124">Snapshots start a minimum of every eight hours and are available for seven days.</span></span>  

<span data-ttu-id="e8324-125">toolearn hakkında daha fazla bilgi:</span><span class="sxs-lookup"><span data-stu-id="e8324-125">toolearn more about:</span></span>

* <span data-ttu-id="e8324-126">Azure blob anlık görüntülerini görmek [blob anlık görüntü](../storage/blobs/storage-blob-snapshots.md).</span><span class="sxs-lookup"><span data-stu-id="e8324-126">Azure blob snapshots, see [Create a blob snapshot](../storage/blobs/storage-blob-snapshots.md).</span></span>

## <a name="geo-redundant-backups"></a><span data-ttu-id="e8324-127">Coğrafi olarak yedekli yedekleri</span><span class="sxs-lookup"><span data-stu-id="e8324-127">Geo-redundant backups</span></span>
<span data-ttu-id="e8324-128">24 saatte SQL Data Warehouse hello tam veri ambarı standart depolama alanında depolar.</span><span class="sxs-lookup"><span data-stu-id="e8324-128">Every 24 hours, SQL Data Warehouse stores hello full data warehouse in Standard storage.</span></span> <span data-ttu-id="e8324-129">Merhaba tam veri ambarı toomatch oluşturulan hello hello son anlık görüntü saati.</span><span class="sxs-lookup"><span data-stu-id="e8324-129">hello full data warehouse is created toomatch hello time of hello last snapshot.</span></span> <span data-ttu-id="e8324-130">Merhaba standart depolama tooa coğrafi olarak yedekli depolama okuma erişimi (RA-GRS) hesabıyla aittir.</span><span class="sxs-lookup"><span data-stu-id="e8324-130">hello standard storage belongs tooa geo-redundant storage account with read access (RA-GRS).</span></span> <span data-ttu-id="e8324-131">Hello Azure depolama RA-GRS özelliği çoğaltır hello yedekleme dosyalarını tooa [eşleştirilmiş veri merkezi](../best-practices-availability-paired-regions.md).</span><span class="sxs-lookup"><span data-stu-id="e8324-131">hello Azure Storage RA-GRS feature replicates hello backup files tooa [paired data center](../best-practices-availability-paired-regions.md).</span></span> <span data-ttu-id="e8324-132">Bu coğrafi çoğaltma, birincil bölgenizde hello anlık görüntüleri erişemiyor durumunda, veri ambarı geri yükleyebilirsiniz sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8324-132">This geo-replication ensures you can restore data warehouse in case you cannot access hello snapshots in your primary region.</span></span> 

<span data-ttu-id="e8324-133">Bu özellik varsayılan olarak açıktır.</span><span class="sxs-lookup"><span data-stu-id="e8324-133">This feature is on by default.</span></span> <span data-ttu-id="e8324-134">Toouse coğrafi olarak yedekli yedeklemeler, sizin [çıkma] istemiyorsanız (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn).</span><span class="sxs-lookup"><span data-stu-id="e8324-134">If you don't want toouse geo-redundant backups, you can [opt out] (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn).</span></span> 

> [!NOTE]
> <span data-ttu-id="e8324-135">Azure depolama alanında hello terim *çoğaltma* toocopying dosyaları tek bir konumda tooanother başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="e8324-135">In Azure storage, hello term *replication* refers toocopying files from one location tooanother.</span></span> <span data-ttu-id="e8324-136">SQL'in *veritabanı çoğaltması* tookeeping toomultiple ikincil veritabanları birincil veritabanı ile eşitlenen başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="e8324-136">SQL's *database replication* refers tookeeping toomultiple secondary databases synchronized with a primary database.</span></span> 
> 
> 

> [!NOTE]
> <span data-ttu-id="e8324-137">Coğrafi olarak yedekli yedeklemelerde DWU 9000 ve DWU 18000 dışında kabul edemez.</span><span class="sxs-lookup"><span data-stu-id="e8324-137">You cannot opt out of geo-redundant backups with DWU 9000 and DWU 18000.</span></span> 
>
> 

<span data-ttu-id="e8324-138">toolearn hakkında daha fazla bilgi:</span><span class="sxs-lookup"><span data-stu-id="e8324-138">toolearn more about:</span></span>

* <span data-ttu-id="e8324-139">Coğrafi olarak yedekli depolama bkz [Azure Storage çoğaltma](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="e8324-139">Geo-redundant storage, see [Azure Storage replication](../storage/common/storage-redundancy.md).</span></span>
* <span data-ttu-id="e8324-140">RA-GRS depolama bkz [okuma erişimli coğrafi olarak yedekli depolama](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="e8324-140">RA-GRS storage, see [Read-access geo-redundant storage](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage).</span></span>

## <a name="data-warehouse-backup-schedule-and-retention-period"></a><span data-ttu-id="e8324-141">Veri ambarı yedekleme zamanlamasını ve saklama süresi</span><span class="sxs-lookup"><span data-stu-id="e8324-141">Data warehouse backup schedule and retention period</span></span>
<span data-ttu-id="e8324-142">SQL veri ambarı çevrimiçi veri ambarınız her dört tooeight saatlerini ve her yedi gün için anlık görüntü tutar anlık görüntüleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e8324-142">SQL Data Warehouse creates snapshots on your online data warehouses every four tooeight hours and keeps each snapshot for seven days.</span></span> <span data-ttu-id="e8324-143">Son yedi gün, çevrimiçi veritabanı tooone hello geri yükleme noktaları hello içinde geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8324-143">You can restore your online database tooone of hello restore points in hello past seven days.</span></span> 

<span data-ttu-id="e8324-144">Merhaba son anlık görüntü başlatıldığında toosee çevrimiçi SQL veri ambarı üzerinde bu sorguyu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e8324-144">toosee when hello last snapshot started, run this query on your online SQL Data Warehouse.</span></span> 

```sql
select top 1 *
from sys.pdw_loader_backup_runs 
order by run_id desc;
```

<span data-ttu-id="e8324-145">Yedi günden daha uzun süre tooretain bir anlık görüntü gerekiyorsa, bir geri yükleme noktası tooa yeni veri ambarı geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8324-145">If you need tooretain a snapshot for longer than seven days, you can restore a restore point tooa new data warehouse.</span></span> <span data-ttu-id="e8324-146">Merhaba geri yüklemeyi tamamladıktan sonra SQL Data Warehouse anlık hello yeni veri ambarı oluşturmayı başlatır.</span><span class="sxs-lookup"><span data-stu-id="e8324-146">After hello restore is finished, SQL Data Warehouse starts creating snapshots on hello new data warehouse.</span></span> <span data-ttu-id="e8324-147">Değişiklikleri toohello yeni veri ambarı yapmazsanız, hello anlık görüntüleri boş kalır ve bu nedenle hello anlık görüntü maliyeti en az.</span><span class="sxs-lookup"><span data-stu-id="e8324-147">If you don't make changes toohello new data warehouse, hello snapshots stay empty and therefore hello snapshot cost is minimal.</span></span> <span data-ttu-id="e8324-148">Merhaba veritabanı tookeep SQL Data Warehouse duraklatın anlık görüntüleri oluşturma.</span><span class="sxs-lookup"><span data-stu-id="e8324-148">You could also pause hello database tookeep SQL Data Warehouse from creating snapshots.</span></span>

### <a name="what-happens-toomy-backup-retention-while-my-data-warehouse-is-paused"></a><span data-ttu-id="e8324-149">My veri ambarı duraklatıldığında toomy yedekleme bekletme ne olur?</span><span class="sxs-lookup"><span data-stu-id="e8324-149">What happens toomy backup retention while my data warehouse is paused?</span></span>
<span data-ttu-id="e8324-150">SQL Data Warehouse anlık görüntülerini oluşturma değil ve bir veri ambarı duraklatıldığında anlık görüntüleri dolmaz.</span><span class="sxs-lookup"><span data-stu-id="e8324-150">SQL Data Warehouse does not create snapshots and does not expire snapshots while a data warehouse is paused.</span></span> <span data-ttu-id="e8324-151">Merhaba veri ambarı duraklatıldığında hello anlık görüntü yaş değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="e8324-151">hello snapshot age does not change while hello data warehouse is paused.</span></span> <span data-ttu-id="e8324-152">Anlık görüntü saklama hello Takvim günleri hello veri ambarı çevrimiçi olduğu gün sayısına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="e8324-152">Snapshot retention is based on hello number of days hello data warehouse is online, not calendar days.</span></span>

<span data-ttu-id="e8324-153">Örneğin, bir anlık görüntü 4'e 1 Ekim başlatır ve 4'e hello veri ambarı Ekim 3 olarak duraklatıldı hello anlık görüntü iki gün olur.</span><span class="sxs-lookup"><span data-stu-id="e8324-153">For example, if a snapshot starts October 1 at 4 pm and hello data warehouse is paused October 3 at 4 pm, hello snapshot is two days old.</span></span> <span data-ttu-id="e8324-154">Merhaba veri ambarını yeniden çevrimiçi duruma dönerse her iki gün hello anlık görüntüsüdür.</span><span class="sxs-lookup"><span data-stu-id="e8324-154">Whenever hello data warehouse comes back online hello snapshot is two days old.</span></span> <span data-ttu-id="e8324-155">Merhaba veri ambarı Ekim 5 4'e çevrimiçi olursa, hello anlık görüntü iki gün önce yapılmışsa ve daha fazla beş gün boyunca devam eder.</span><span class="sxs-lookup"><span data-stu-id="e8324-155">If hello data warehouse comes online October 5 at 4 pm, hello snapshot is two days old and remains for five more days.</span></span>

<span data-ttu-id="e8324-156">Merhaba veri ambarı tekrar çevrimiçi olduğunda, SQL Data Warehouse Yeni Anlık görüntülerin sürdürür ve yedi günden fazla veri olduğunda anlık görüntüleri süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="e8324-156">When hello data warehouse comes back online, SQL Data Warehouse resumes new snapshots and expires snapshots when they have more than seven days of data.</span></span>

### <a name="how-long-is-hello-retention-period-for-a-dropped-data-warehouse"></a><span data-ttu-id="e8324-157">Bırakılan veri ambarı Hello saklama süresi uzunluğu nedir?</span><span class="sxs-lookup"><span data-stu-id="e8324-157">How long is hello retention period for a dropped data warehouse?</span></span>
<span data-ttu-id="e8324-158">Veri ambarı bırakıldığında hello veri ambarı ve hello anlık görüntüleri yedi gün için kaydedilir ve sonra kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="e8324-158">When a data warehouse is dropped, hello data warehouse and hello snapshots are saved for seven days and then removed.</span></span> <span data-ttu-id="e8324-159">Merhaba veri ambarı tooany kaydedilmiş hello geri yükleme noktaları geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8324-159">You can restore hello data warehouse tooany of hello saved restore points.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8324-160">Mantıksal bir SQL server örneği silerseniz, toohello örneği ait tüm veritabanlarının da silinir ve kurtarılamaz.</span><span class="sxs-lookup"><span data-stu-id="e8324-160">If you delete a logical SQL server instance, all databases that belong toohello instance are also deleted and cannot be recovered.</span></span> <span data-ttu-id="e8324-161">Silinen bir sunucuya geri yükleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8324-161">You cannot restore a deleted server.</span></span>
> 
> 

## <a name="data-warehouse-backup-costs"></a><span data-ttu-id="e8324-162">Veri ambarı yedekleme maliyetleri</span><span class="sxs-lookup"><span data-stu-id="e8324-162">Data warehouse backup costs</span></span>
<span data-ttu-id="e8324-163">Maliyet birincil veri ambarı ve Azure Blob anlık görüntü yedi gün için toplam hello TB en yakın yuvarlak toohello ' dir.</span><span class="sxs-lookup"><span data-stu-id="e8324-163">hello total cost for your primary data warehouse and seven days of Azure Blob snapshots is rounded toohello nearest TB.</span></span> <span data-ttu-id="e8324-164">Örneğin, veri Ambarınızı 1,5 TB ise ve 100 GB hello anlık görüntüleri kullanmak, 2 TB veri Azure Premium Storage hızlarında için faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="e8324-164">For example, if your data warehouse is 1.5 TB and hello snapshots use 100 GB, you are billed for 2 TB of data at Azure Premium Storage rates.</span></span> 

> [!NOTE]
> <span data-ttu-id="e8324-165">Her anlık görüntü başlangıçta boş ve değişiklikleri toohello birincil veri ambarı yaptığınız gibi büyür.</span><span class="sxs-lookup"><span data-stu-id="e8324-165">Each snapshot is empty initially and grows as you make changes toohello primary data warehouse.</span></span> <span data-ttu-id="e8324-166">Tüm anlık görüntüleri hello veri ambarı değiştikçe boyutunu artırın.</span><span class="sxs-lookup"><span data-stu-id="e8324-166">All snapshots increase in size as hello data warehouse changes.</span></span> <span data-ttu-id="e8324-167">Bu nedenle, anlık görüntüler için hello depolama maliyetleri değişiklik according toohello oranını artar.</span><span class="sxs-lookup"><span data-stu-id="e8324-167">Therefore, hello storage costs for snapshots grow according toohello rate of change.</span></span>
> 
> 

<span data-ttu-id="e8324-168">Coğrafi olarak yedekli depolama birimi kullanıyorsanız, ayrı depolama ücret alırsınız.</span><span class="sxs-lookup"><span data-stu-id="e8324-168">If you are using geo-redundant storage, you receive a separate storage charge.</span></span> <span data-ttu-id="e8324-169">Merhaba coğrafi olarak yedekli depolama hello standart okuma erişimli coğrafi olarak yedekli depolama (RA-GRS) oranı faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="e8324-169">hello geo-redundant storage is billed at hello standard Read-Access Geographically Redundant Storage (RA-GRS) rate.</span></span>

<span data-ttu-id="e8324-170">SQL Data Warehouse fiyatlandırması hakkında daha fazla bilgi için bkz: [SQL Data Warehouse fiyatlandırması](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="e8324-170">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="using-database-backups"></a><span data-ttu-id="e8324-171">Veritabanı Yedeklemeleri kullanma</span><span class="sxs-lookup"><span data-stu-id="e8324-171">Using database backups</span></span>
<span data-ttu-id="e8324-172">Merhaba birincil için SQL veri ambarı yedekleri toorestore hello veri ambarı tooone hello geri yükleme noktaları hello saklama dönemi içinde kullanılmasıdır.</span><span class="sxs-lookup"><span data-stu-id="e8324-172">hello primary use for SQL data warehouse backups is toorestore hello data warehouse tooone of hello restore points within hello retention period.</span></span>  

* <span data-ttu-id="e8324-173">toorestore SQL data warehouse, bkz: [SQL data warehouse geri](sql-data-warehouse-restore-database-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e8324-173">toorestore a SQL data warehouse, see [Restore a SQL data warehouse](sql-data-warehouse-restore-database-overview.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="e8324-174">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="e8324-174">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="e8324-175">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="e8324-175">Scenarios</span></span>
* <span data-ttu-id="e8324-176">İş sürekliliğine genel bakış için bkz: [iş sürekliliğine genel bakış](../sql-database/sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="e8324-176">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

* <span data-ttu-id="e8324-177">toorestore bir veri ambarı bkz [SQL data warehouse geri yükleme](sql-data-warehouse-restore-database-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e8324-177">toorestore a data warehouse, see [Restore a SQL data warehouse](sql-data-warehouse-restore-database-overview.md)</span></span>

<!-- ### Tutorials -->

