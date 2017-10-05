---
title: "PowerShell: Azure SQL esnek havuzunu yönetme & Oluştur | Microsoft Docs"
description: "Bir esnek havuz yönetmek için PowerShell kullanmayı öğrenin."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 61289770-69b9-4ae3-9252-d0e94d709331
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: data-management
ms.date: 06/06/2017
ms.author: srinia
ms.openlocfilehash: 5e76397c62e5a6ff7fb356bd81218c307f3fda31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="2eeb6-103">Oluşturma ve bir esnek havuz PowerShell ile yönetme</span><span class="sxs-lookup"><span data-stu-id="2eeb6-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="2eeb6-104">Bu konuda oluşturmak ve yönetmek nasıl ölçeklenebilir gösterilmektedir [esnek havuzlar](sql-database-elastic-pool.md) PowerShell ile.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-104">This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="2eeb6-105">Ayrıca oluşturabilir ve bir Azure esnek havuz kullanarak yönetebileceğiniz [Azure portal](https://portal.azure.com/), REST API veya [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="2eeb6-105">You can also create and manage an Azure elastic pool using the [Azure portal](https://portal.azure.com/), REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="2eeb6-106">Ayrıca oluşturun ve içine ve dışına esnek havuzlar kullanarak veritabanlarını taşıma [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="2eeb6-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="2eeb6-107">Esnek havuz oluşturma</span><span class="sxs-lookup"><span data-stu-id="2eeb6-107">Create an elastic pool</span></span>
<span data-ttu-id="2eeb6-108">[New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet'i bir esnek havuz oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-108">The [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="2eeb6-109">EDTU havuzu, minimum ve maksimum Dtu değerleri, hizmet katmanı değerine (temel, standart, Premium veya Premium RS) kısıtlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-109">The values for eDTU per pool, min, and max DTUs are constrained by the service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="2eeb6-110">Bkz: [esnek havuzlar ve havuza alınmış veritabanları için eDTU ve depolama sınırları](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="2eeb6-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="2eeb6-111">Havuza alınmış bir veritabanı bir esnek havuz oluşturma</span><span class="sxs-lookup"><span data-stu-id="2eeb6-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="2eeb6-112">[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet komutunu kullanın ve hedef havuz için **ElasticPoolName** parametresini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-112">Use the [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet and set the **ElasticPoolName** parameter to the target pool.</span></span> <span data-ttu-id="2eeb6-113">Varolan bir veritabanını bir esnek havuza taşımak için bkz: [bir veritabanını bir esnek havuza taşıma](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="2eeb6-113">To move an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a><span data-ttu-id="2eeb6-114">Betiğin tamamı</span><span class="sxs-lookup"><span data-stu-id="2eeb6-114">Complete script</span></span>
<span data-ttu-id="2eeb6-115">Bir Azure kaynak grubu ve sunucu bu komut dosyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="2eeb6-116">İstendiğinde, yeni sunucu için bir yönetici kullanıcı adı ve parola (Azure kimlik bilgilerinizi değil) sağlayın.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-116">When prompted, supply an administrator username and password for the new server (not your Azure credentials).</span></span>

```PowerShell
$subscriptionId = '<your Azure subscription id>'
$resourceGroupName = '<resource group name>'
$location = '<datacenter location>'
$serverName = '<server name>'
$poolName = '<pool name>'
$databaseName = '<database name>'

Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $serverName -Location $location -ServerVersion "12.0"
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $serverName -FirewallRuleName "rule1" -StartIpAddress "192.168.0.198" -EndIpAddress "192.168.0.199"

New-AzureRmSqlElasticPool -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

New-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -ElasticPoolName $poolName -MaxSizeBytes 10GB
```

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="2eeb6-117">Bir esnek havuz oluşturma ve birden fazla havuza veritabanı ekleme</span><span class="sxs-lookup"><span data-stu-id="2eeb6-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="2eeb6-118">Esnek havuzdaki birçok veritabanı oluşturulmasını portalı veya aynı anda yalnızca tek bir veritabanı oluşturabilirsiniz PowerShell cmdlet'lerini kullanarak tamamlanınca zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-118">Creation of many databases in an elastic pool can take time when done using the portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="2eeb6-119">İçine bir esnek havuz oluşturmayı otomatikleştirmek için bkz: [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span><span class="sxs-lookup"><span data-stu-id="2eeb6-119">To automate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="2eeb6-120">Bir veritabanını bir esnek havuza taşıma</span><span class="sxs-lookup"><span data-stu-id="2eeb6-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="2eeb6-121">Bir veritabanı içine veya dışına sahip bir esnek havuz taşıyabilirsiniz [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="2eeb6-121">You can move a database into or out of an elastic pool with the [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span></span>

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="2eeb6-122">Bir esnek havuz performans ayarlarını değiştir</span><span class="sxs-lookup"><span data-stu-id="2eeb6-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="2eeb6-123">Performans düşebilir, büyüme uyum sağlayacak şekilde havuzu ayarlarını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-123">When performance suffers, you can change the settings of the pool to accommodate growth.</span></span> <span data-ttu-id="2eeb6-124">Kullanım [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-124">Use the [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span></span> <span data-ttu-id="2eeb6-125">Havuz başına edtu'larını - Dtu parametreyi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-125">Set the -Dtu parameter to the eDTUs per pool.</span></span> <span data-ttu-id="2eeb6-126">Bkz: [eDTU ve depolama sınırları](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) olası değerler için.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-the-storage-limit-for-an-elastic-pool"></a><span data-ttu-id="2eeb6-127">Bir esnek havuz depolama sınırını değiştirme</span><span class="sxs-lookup"><span data-stu-id="2eeb6-127">Change the storage limit for an elastic pool</span></span>

<span data-ttu-id="2eeb6-128">Kullanım [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) ayarlamak için cmdlet _- StorageMB_ parametresi.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-128">Use the [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet to set the _-StorageMB_ parameter.</span></span> <span data-ttu-id="2eeb6-129">(Depolama sınırı 2 TB Örneğin, 2097152 kümeleri) MB cinsinden depolama sınırı sağlar.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-129">Provide the storage limit in MB (for example, 2097152 sets the storage limit to 2 TB).</span></span> <span data-ttu-id="2eeb6-130">Bkz: [eDTU ve depolama sınırları](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) olası değerler için.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-130">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2eeb6-131">Premium havuzlarıyla 1500 Edtu havuzu başına varsayılan en büyük veri depolama veya daha fazla 750 GB'dir.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-131">The default max data storage per pool for Premium pools with 1500 eDTUs or more is 750 GB.</span></span> <span data-ttu-id="2eeb6-132">En yüksek elde etmek için _en büyük havuz başına veri depolama boyut_, depolama sınırını açıkça ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-132">To obtain the higher _max data storage size per pool_, the storage limit must be explicitly set.</span></span> <span data-ttu-id="2eeb6-133">Premium 750 GB'den fazla depolama havuzlarıyla şu anda aşağıdaki bölgelerde genel önizlemede: Doğu ABD 2, Batı ABD, BİZE kamu Virginia, Batı Avrupa, Orta Almanya, Güneydoğu Asya, Japonya Doğu, Avustralya Doğu, Kanada merkezi ve Doğu Kanada.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-133">Premium pools with more than 750 GB of storage is currently in public preview in the following regions: East US 2, West US, US Gov Virginia, West Europe, Germany Central, Southeast Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-the-status-of-pool-operations"></a><span data-ttu-id="2eeb6-134">Havuz işlem durumunu Al</span><span class="sxs-lookup"><span data-stu-id="2eeb6-134">Get the status of pool operations</span></span>
<span data-ttu-id="2eeb6-135">Bir esnek havuz oluşturma zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-135">Creating an elastic pool can take time.</span></span> <span data-ttu-id="2eeb6-136">Oluşturma ve güncelleştirmeleri de dahil olmak üzere havuzu işlemleri durumunu izlemek için [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-136">To track the status of pool operations including creation and updates, use the [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-the-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="2eeb6-137">Bir veritabanı içine ve dışına esnek havuz taşıma durumunu Al</span><span class="sxs-lookup"><span data-stu-id="2eeb6-137">Get the status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="2eeb6-138">Bir veritabanını taşıma zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-138">Moving a database can take time.</span></span> <span data-ttu-id="2eeb6-139">Kullanarak bir taşıma durumunu izlemek [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-139">Track a move status using the [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="2eeb6-140">Esnek havuz için kaynak kullanım verilerini alma</span><span class="sxs-lookup"><span data-stu-id="2eeb6-140">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="2eeb6-141">Kaynak havuzu sınırı yüzdesi olarak alınabilir ölçümleri:</span><span class="sxs-lookup"><span data-stu-id="2eeb6-141">Metrics that can be retrieved as a percentage of the resource pool limit:</span></span>

| <span data-ttu-id="2eeb6-142">Ölçüm adı</span><span class="sxs-lookup"><span data-stu-id="2eeb6-142">Metric name</span></span> | <span data-ttu-id="2eeb6-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2eeb6-143">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2eeb6-144">CPU\_yüzde</span><span class="sxs-lookup"><span data-stu-id="2eeb6-144">cpu\_percent</span></span> |<span data-ttu-id="2eeb6-145">Havuz sınırı yüzdesi cinsinden ortalama işlem kullanımı.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-145">Average compute utilization in percentage of the limit of the pool.</span></span> |
| <span data-ttu-id="2eeb6-146">fiziksel\_veri\_okuma\_yüzde</span><span class="sxs-lookup"><span data-stu-id="2eeb6-146">physical\_data\_read\_percent</span></span> |<span data-ttu-id="2eeb6-147">Yüzde tabanlı havuzunun sınırını ortalama g/ç kullanımı.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-147">Average I/O utilization in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="2eeb6-148">Günlük\_yazma\_yüzde</span><span class="sxs-lookup"><span data-stu-id="2eeb6-148">log\_write\_percent</span></span> |<span data-ttu-id="2eeb6-149">Ortalama havuzu sınırının yüzde olarak kaynak kullanımı yazma.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-149">Average write resource utilization in percentage of the limit of the pool.</span></span> |
| <span data-ttu-id="2eeb6-150">DTU\_tüketim\_yüzde</span><span class="sxs-lookup"><span data-stu-id="2eeb6-150">DTU\_consumption\_percent</span></span> |<span data-ttu-id="2eeb6-151">Havuz eDTU sınırı yüzdesi cinsinden ortalama eDTU kullanımı</span><span class="sxs-lookup"><span data-stu-id="2eeb6-151">Average eDTU utilization in percentage of eDTU limit for the pool</span></span> |
| <span data-ttu-id="2eeb6-152">Depolama\_yüzde</span><span class="sxs-lookup"><span data-stu-id="2eeb6-152">storage\_percent</span></span> |<span data-ttu-id="2eeb6-153">Depolama kullanımı havuz depolama sınırı yüzdesi cinsinden ortalama.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-153">Average storage utilization in percentage of the storage limit of the pool.</span></span> |
| <span data-ttu-id="2eeb6-154">Çalışanlar\_yüzde</span><span class="sxs-lookup"><span data-stu-id="2eeb6-154">workers\_percent</span></span> |<span data-ttu-id="2eeb6-155">Maksimum eşzamanlı çalışanları (istek) havuzunun sınırını göre yüzdesi.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-155">Maximum concurrent workers (requests) in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="2eeb6-156">oturumları\_yüzde</span><span class="sxs-lookup"><span data-stu-id="2eeb6-156">sessions\_percent</span></span> |<span data-ttu-id="2eeb6-157">Havuzun sınırını göre yüzde cinsinden en fazla eşzamanlı oturum.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-157">Maximum concurrent sessions in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="2eeb6-158">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="2eeb6-158">eDTU_limit</span></span> |<span data-ttu-id="2eeb6-159">Geçerli en büyük esnek havuz DTU ayarı bu esnek havuz için bu aralığında.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-159">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="2eeb6-160">Depolama\_sınırı</span><span class="sxs-lookup"><span data-stu-id="2eeb6-160">storage\_limit</span></span> |<span data-ttu-id="2eeb6-161">Geçerli en fazla esnek havuz depolama sınırı bu megabayt cinsinden esnek havuz için bu zaman aralığında ayarlama.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-161">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="2eeb6-162">eDTU\_kullanılan</span><span class="sxs-lookup"><span data-stu-id="2eeb6-162">eDTU\_used</span></span> |<span data-ttu-id="2eeb6-163">Bu aralık havuzunda tarafından kullanılan ortalama Edtu.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-163">Average eDTUs used by the pool in this interval.</span></span> |
| <span data-ttu-id="2eeb6-164">Depolama\_kullanılan</span><span class="sxs-lookup"><span data-stu-id="2eeb6-164">storage\_used</span></span> |<span data-ttu-id="2eeb6-165">Bu aralık bayt havuzunda tarafından kullanılan ortalama depolama</span><span class="sxs-lookup"><span data-stu-id="2eeb6-165">Average storage used by the pool in this interval in bytes</span></span> |

<span data-ttu-id="2eeb6-166">**Ölçümleri ayrıntı düzeyi/bekletme süreleri:**</span><span class="sxs-lookup"><span data-stu-id="2eeb6-166">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="2eeb6-167">5 dakikalık bazda veriler döndürülür.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-167">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="2eeb6-168">Veri saklama 35 gün olur.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-168">Data retention is 35 days.</span></span>  

<span data-ttu-id="2eeb6-169">Bu cmdlet ve API 1000 satırı (yaklaşık 3 gün 5 dakikalık ayrıntı düzeyi, verilerin) yapılan bir çağrı alınabilir satır sayısını sınırlar.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-169">This cmdlet and API limits the number of rows that can be retrieved in one call to 1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="2eeb6-170">Ancak bu komut, daha fazla veri almak için birden çok kez farklı başlangıç/bitiş zaman aralıkları ile çağrılamaz</span><span class="sxs-lookup"><span data-stu-id="2eeb6-170">But this command can be called multiple times with different start/end time intervals to retrieve more data</span></span>

<span data-ttu-id="2eeb6-171">Ölçümler alınamadı:</span><span class="sxs-lookup"><span data-stu-id="2eeb6-171">To retrieve the metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="2eeb6-172">Kaynak kullanım verilerini bir esnek havuz için bir veritabanı Al</span><span class="sxs-lookup"><span data-stu-id="2eeb6-172">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="2eeb6-173">Bu API'leri aşağıdaki anlamsal fark dışında tek bir veritabanının kaynak kullanımını izlemek için kullanılan API'leri ile aynıdır: alınan ölçümler bir yüzdesi olarak ifade edilen her veritabanı maksimum Edtu (veya arka plandaki için eşdeğer cap Metrik CPU veya g/ç gibi) için bu havuzu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-173">These APIs are the same as the APIs used for monitoring the resource utilization of a single database, except for the following semantic difference: metrics retrieved are expressed as a percentage of the per database max eDTUs (or equivalent cap for the underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="2eeb6-174">Örneğin, % 50 kullanımını bu ölçümleri belirli kaynak tüketimini % 50'den gösterir başına veritabanı cap sınırını ana havuzunda bu kaynak için.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-174">For example, 50% utilization of any of these metrics indicates that the specific resource consumption is at 50% of the per database cap limit for that resource in the parent pool.</span></span>

<span data-ttu-id="2eeb6-175">Ölçümler alınamadı:</span><span class="sxs-lookup"><span data-stu-id="2eeb6-175">To retrieve the metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-to-an-elastic-pool-resource"></a><span data-ttu-id="2eeb6-176">Bir uyarı için bir esnek havuz kaynak ekleyin</span><span class="sxs-lookup"><span data-stu-id="2eeb6-176">Add an alert to an elastic pool resource</span></span>
<span data-ttu-id="2eeb6-177">E-posta bildirimleri veya uyarı dizelere göndermek için bir esnek havuz için uyarı kuralı ekleyebilirsiniz [URL uç noktaları](https://msdn.microsoft.com/library/mt718036.aspx) zaman esnek havuz isabetler sizin ayarladığınız bir kullanım eşiği.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-177">You can add alert rules to an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when the elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="2eeb6-178">Add-AzureRmMetricAlertRule cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-178">Use the Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2eeb6-179">Esnek havuzlar için izleme kaynak kullanımı en az 5 dakikalık bir gecikme vardır.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-179">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="2eeb6-180">10 dakikadan daha kısa bir süre esnek havuzlar için uyarıları ayarlama şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-180">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="2eeb6-181">Nokta esnek havuzlar için herhangi bir uyarı ayarlayın (adlı parametre "-pencereboyutu" PowerShell API'sindeki) 10 dakikadan daha kısa bir süre değil tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="2eeb6-182">10 dakikalık bir süre (pencereboyutu) veya daha fazla esnek havuzlarını kullanmak için herhangi bir uyarı tanımladığınız olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>
>

<span data-ttu-id="2eeb6-183">Bu örnek, bir esnek havuza ait eDTU tüketim belirli eşiğin gittiğinde bildirim için bir uyarı ekler.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-183">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location =  '<location'                         # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

#$Target Resource ID
$ResourceID = '/subscriptions/' + $subscriptionId + '/resourceGroups/' +$resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticpools/' + $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# create a unique rule name
$alertName = $poolName + "- DTU consumption rule"

# Create an alert rule for DTU_consumption_percent
Add-AzureRMMetricAlertRule -Name $alertName -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $ResourceID -MetricName "DTU_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail
```

<span data-ttu-id="2eeb6-184">Daha fazla bilgi için bkz: [Azure Portalı'nda SQL veritabanı uyarıları oluşturma](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2eeb6-184">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="add-alerts-to-all-databases-in-an-elastic-pool"></a><span data-ttu-id="2eeb6-185">Esnek havuzdaki tüm veritabanları için uyarıları Ekle</span><span class="sxs-lookup"><span data-stu-id="2eeb6-185">Add alerts to all databases in an elastic pool</span></span>
<span data-ttu-id="2eeb6-186">Uyarı kuralları e-posta bildirimleri veya uyarı dizelere göndermek için esnek havuzdaki tüm veritabanı ekleyebileceğiniz [URL uç noktaları](https://msdn.microsoft.com/library/mt718036.aspx) ne zaman bir kaynak isabetler uyarı tarafından ayarlanan kullanım eşiği.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-186">You can add alert rules to all database in an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by the alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2eeb6-187">Esnek havuzlar için izleme kaynak kullanımı en az 5 dakikalık bir gecikme vardır.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-187">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="2eeb6-188">10 dakikadan daha kısa bir süre esnek havuzlar için uyarıları ayarlama şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-188">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="2eeb6-189">Nokta esnek havuzlar için herhangi bir uyarı ayarlayın (adlı parametre "-pencereboyutu" PowerShell API'sindeki) 10 dakikadan daha kısa bir süre değil tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-189">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="2eeb6-190">10 dakikalık bir süre (pencereboyutu) veya daha fazla esnek havuzlarını kullanmak için herhangi bir uyarı tanımladığınız olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-190">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>

<span data-ttu-id="2eeb6-191">Bu örnekte, her bir veritabanının ait DTU tüketimi belirli eşiğin gittiğinde bildirim için esnek havuzdaki veritabanları bir uyarı ekler.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-191">This example adds an alert to each of the databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get the list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for the specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop the alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="2eeb6-192">Toplamak ve bir abonelikte birden çok havuz arasında kaynak kullanım verilerini izlemek</span><span class="sxs-lookup"><span data-stu-id="2eeb6-192">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="2eeb6-193">Bir abonelikte birçok veritabanı varsa, her esnek havuz ayrı ayrı izlemek için sıkıcı.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-193">When you have many databases in a subscription, it is cumbersome to monitor each elastic pool separately.</span></span> <span data-ttu-id="2eeb6-194">Bunun yerine, SQL veritabanı PowerShell cmdlet'leri ve T-SQL sorgularını birden çok havuz ve kendi veritabanlarını izleme ve kaynak kullanımını analiz için kaynak kullanım verilerini toplamak için birleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-194">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined to collect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="2eeb6-195">A [örnek uygulama](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) gibi birtakım PowerShell komut dosyaları GitHub SQL Server örnekleri depo ne yaptığını ve nasıl kullanılacağını belgelerle birlikte bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-195">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in the GitHub SQL Server samples repository along with documentation on what it does and how to use it.</span></span>

<span data-ttu-id="2eeb6-196">Bu örnek uygulama kullanmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-196">To use this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="2eeb6-197">Karşıdan [betikleri ve belgeleri](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span><span class="sxs-lookup"><span data-stu-id="2eeb6-197">Download the [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="2eeb6-198">Ortamınız için komut dosyalarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-198">Modify the scripts for your environment.</span></span> <span data-ttu-id="2eeb6-199">Esnek havuzlar üzerinde barındırılan bir veya daha fazla sunucuları belirtin.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-199">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="2eeb6-200">Toplanan ölçümleri depolanması nerede telemetri veritabanını belirtin.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-200">Specify a telemetry database where the collected metrics are to be stored.</span></span>
4. <span data-ttu-id="2eeb6-201">Komut dosyaları yürütme süresini belirtmek için komut dosyası özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-201">Customize the script to specify the duration of the scripts' execution.</span></span>

<span data-ttu-id="2eeb6-202">Yüksek düzeyde, komut dosyaları aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="2eeb6-202">At a high level, the scripts do the following:</span></span>

* <span data-ttu-id="2eeb6-203">Belirli bir Azure aboneliği (veya belirtilen sunucularının listesini) tüm sunucular numaralandırır.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-203">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="2eeb6-204">Her sunucu için bir arka plan işi çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-204">Runs a background job for each server.</span></span> <span data-ttu-id="2eeb6-205">İş, düzenli aralıklarla bir döngüde çalışır ve sunucudaki tüm havuzları telemetri verileri toplar.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-205">The job runs in a loop at regular intervals and collects telemetry data for all the pools in the server.</span></span> <span data-ttu-id="2eeb6-206">Daha sonra belirtilen telemetri veritabanına toplanan verileri yükler.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-206">It then loads the collected data into the specified telemetry database.</span></span>
* <span data-ttu-id="2eeb6-207">Veritabanı kaynak kullanım verilerini toplamak için her havuzda veritabanlarının listesini numaralandırır.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-207">Enumerates a list of databases in each pool to collect the database resource usage data.</span></span> <span data-ttu-id="2eeb6-208">Daha sonra toplanan verileri telemetri veritabanına yükler.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-208">It then loads the collected data into the telemetry database.</span></span>

<span data-ttu-id="2eeb6-209">Esnek havuzlar ve veritabanlarında sağlığını izlemek için toplanan ölçümleri telemetri veritabanındaki çözümlenebilir.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-209">The collected metrics in the telemetry database can be analyzed to monitor the health of elastic pools and the databases in it.</span></span> <span data-ttu-id="2eeb6-210">Komut dosyası, belirtilen zaman penceresi için ölçümleri toplama yardımcı olmak için telemetri veritabanında önceden tanımlanmış Tablo Değerli Fonksiyon (TVF) de yükler.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-210">The script also installs a pre-defined Table-Value function (TVF) in the telemetry database to help aggregate the metrics for a specified time window.</span></span> <span data-ttu-id="2eeb6-211">Örneğin, TVF sonuçlarını "üst N esnek havuzları, belirli bir zaman penceresinde maksimum eDTU kullanımı ile." göstermek için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="2eeb6-211">For example, results of the TVF can be used to show “top N elastic pools with the maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="2eeb6-212">İsteğe bağlı olarak, sorgu ve toplanan verileri çözümlemek için Excel veya Power BI gibi analitik araçlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-212">Optionally, use analytic tools like Excel or Power BI to query and analyze the collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="2eeb6-213">Örnek: bir esnek havuz ve veritabanlarını için kaynak tüketimi ölçümlerini alın</span><span class="sxs-lookup"><span data-stu-id="2eeb6-213">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="2eeb6-214">Bu örnek, belirli bir esnek havuz ve tüm veritabanları için tüketimi ölçümlerini alır.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-214">This example retrieves the consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="2eeb6-215">Toplanan veri biçimlendirilmiş ve biçimlendirilmiş bir .csv dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-215">Collected data is formatted and written to a .csv formatted file.</span></span> <span data-ttu-id="2eeb6-216">Dosyayı Excel ile göz atılacak.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-216">The file can be browsed with Excel.</span></span>

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login to Azure account and select the subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for the specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct the pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get the list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for the specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format the metrics and output as .csv file using the following script block.
$command = {
param($metricList, $outputFile)

# Format metrics into a table.
$table = @()
foreach($metric in $metricList) {
   foreach($metricValue in $metric.MetricValues) {
      $sx = New-Object PSObject -Property @{
      Timestamp = $metricValue.Timestamp.ToString()
      MetricName = $metric.Name;
      Average = $metricValue.Average;
      ResourceID = $metric.ResourceId
   }$table = $table += $sx
   }
}

# Output the metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="2eeb6-217">Esnek havuz işlemlerinin gecikme süresi</span><span class="sxs-lookup"><span data-stu-id="2eeb6-217">Latency of elastic pool operations</span></span>
* <span data-ttu-id="2eeb6-218">Veritabanı veya maksimum Edtu başına veritabanı başına minimum edtu'larını genellikle değiştirme 5 dakika veya daha az tamamlar.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-218">Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="2eeb6-219">Havuz başına edtu'larını değiştirme havuzdaki tüm veritabanları tarafından kullanılan alanı toplam miktarına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-219">Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool.</span></span> <span data-ttu-id="2eeb6-220">Değişiklikler 100 GB için ortalama 90 dakika veya daha az sürer.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-220">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="2eeb6-221">Örneğin, toplam alanı tarafından kullanılan havuzdaki tüm veritabanları ise 200 GB havuz eDTU havuzu başına değiştirmek için beklenen gecikme süresi 3 saat sonra veya daha az.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-221">For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.</span></span>



## <a name="next-steps"></a><span data-ttu-id="2eeb6-222">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2eeb6-222">Next steps</span></span>
* <span data-ttu-id="2eeb6-223">[Esnek iş oluşturma](sql-database-elastic-jobs-overview.md): Esnek işler, havuzda bulunan herhangi bir sayıdaki veritabanı için T-SQL betiklerini çalıştırmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-223">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in the pool.</span></span>
* <span data-ttu-id="2eeb6-224">Bkz [Azure SQL veritabanı ile ölçeğini](sql-database-elastic-scale-introduction.md): ölçeğini, verileri taşımak için esnek araçlar kullanın sorgulamak ya da hareketleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2eeb6-224">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools to scale out, move data, query, or create transactions.</span></span>
