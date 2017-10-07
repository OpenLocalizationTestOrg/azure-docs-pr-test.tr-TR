---
title: "PowerShell: Azure SQL esnek havuzunu yönetme & Oluştur | Microsoft Docs"
description: "Bilgi nasıl toouse PowerShell toomanage bir esnek havuz."
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
ms.openlocfilehash: 92de2a4b243dcc74502064e9d2c31682691753d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="a4366-103">Oluşturma ve bir esnek havuz PowerShell ile yönetme</span><span class="sxs-lookup"><span data-stu-id="a4366-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="a4366-104">Bu konu, nasıl gösterir toocreate ve ölçeklenebilir yönetmek [esnek havuzlar](sql-database-elastic-pool.md) PowerShell ile.</span><span class="sxs-lookup"><span data-stu-id="a4366-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="a4366-105">Ayrıca oluşturabilir ve hello kullanarak bir Azure esnek havuzunu yönetme [Azure portal](https://portal.azure.com/), REST API veya [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="a4366-105">You can also create and manage an Azure elastic pool using hello [Azure portal](https://portal.azure.com/), REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="a4366-106">Ayrıca oluşturun ve içine ve dışına esnek havuzlar kullanarak veritabanlarını taşıma [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="a4366-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="a4366-107">Esnek havuz oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4366-107">Create an elastic pool</span></span>
<span data-ttu-id="a4366-108">Merhaba [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet'i bir esnek havuz oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a4366-108">hello [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="a4366-109">eDTU havuzu, en az ve maksimum Dtu başına Hello değerlerini hello hizmet katmanı değerine (temel, standart, Premium veya Premium RS) kısıtlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a4366-109">hello values for eDTU per pool, min, and max DTUs are constrained by hello service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="a4366-110">Bkz: [esnek havuzlar ve havuza alınmış veritabanları için eDTU ve depolama sınırları](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="a4366-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="a4366-111">Havuza alınmış bir veritabanı bir esnek havuz oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4366-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="a4366-112">Kullanım hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet'i ve kümesi hello **ElasticPoolName** parametresi toohello hedef havuzu.</span><span class="sxs-lookup"><span data-stu-id="a4366-112">Use hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet and set hello **ElasticPoolName** parameter toohello target pool.</span></span> <span data-ttu-id="a4366-113">Varolan bir veritabanını bir esnek havuz toomove bkz [bir veritabanını bir esnek havuza taşıma](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="a4366-113">toomove an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a><span data-ttu-id="a4366-114">Betiğin tamamı</span><span class="sxs-lookup"><span data-stu-id="a4366-114">Complete script</span></span>
<span data-ttu-id="a4366-115">Bir Azure kaynak grubu ve sunucu bu komut dosyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a4366-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="a4366-116">İstendiğinde, bir yönetici kullanıcı adı ve parolası hello yeni sunucu (Azure kimlik bilgilerinizi değil) sağlayın.</span><span class="sxs-lookup"><span data-stu-id="a4366-116">When prompted, supply an administrator username and password for hello new server (not your Azure credentials).</span></span>

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

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="a4366-117">Bir esnek havuz oluşturma ve birden fazla havuza veritabanı ekleme</span><span class="sxs-lookup"><span data-stu-id="a4366-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="a4366-118">Esnek havuzdaki birçok veritabanı oluşturulmasını hello portalı veya aynı anda yalnızca tek bir veritabanı oluşturabilirsiniz PowerShell cmdlet'lerini kullanarak tamamlanınca zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="a4366-118">Creation of many databases in an elastic pool can take time when done using hello portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="a4366-119">bir esnek havuz tooautomate oluşturma bkz [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span><span class="sxs-lookup"><span data-stu-id="a4366-119">tooautomate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="a4366-120">Bir veritabanını bir esnek havuza taşıma</span><span class="sxs-lookup"><span data-stu-id="a4366-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="a4366-121">Bir veritabanı içine veya dışına hello sahip bir esnek havuz taşıyabilirsiniz [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="a4366-121">You can move a database into or out of an elastic pool with hello [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span></span>

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="a4366-122">Bir esnek havuz performans ayarlarını değiştir</span><span class="sxs-lookup"><span data-stu-id="a4366-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="a4366-123">Performans düşebilir hello havuzu tooaccommodate büyüme hello ayarlarını değiştirebilirler.</span><span class="sxs-lookup"><span data-stu-id="a4366-123">When performance suffers, you can change hello settings of hello pool tooaccommodate growth.</span></span> <span data-ttu-id="a4366-124">Kullanım hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="a4366-124">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span></span> <span data-ttu-id="a4366-125">Merhaba - Dtu parametresi toohello Edtu havuzu başına ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a4366-125">Set hello -Dtu parameter toohello eDTUs per pool.</span></span> <span data-ttu-id="a4366-126">Bkz: [eDTU ve depolama sınırları](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) olası değerler için.</span><span class="sxs-lookup"><span data-stu-id="a4366-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a><span data-ttu-id="a4366-127">Bir esnek havuz depolama sınırı Hello değiştirme</span><span class="sxs-lookup"><span data-stu-id="a4366-127">Change hello storage limit for an elastic pool</span></span>

<span data-ttu-id="a4366-128">Kullanım hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _- StorageMB_ parametresi.</span><span class="sxs-lookup"><span data-stu-id="a4366-128">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _-StorageMB_ parameter.</span></span> <span data-ttu-id="a4366-129">Merhaba depolama sınırı MB (örneğin, 2097152 kümeleri hello depolama sınırı too2 TB) sağlayın.</span><span class="sxs-lookup"><span data-stu-id="a4366-129">Provide hello storage limit in MB (for example, 2097152 sets hello storage limit too2 TB).</span></span> <span data-ttu-id="a4366-130">Bkz: [eDTU ve depolama sınırları](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) olası değerler için.</span><span class="sxs-lookup"><span data-stu-id="a4366-130">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4366-131">Premium havuzlarıyla 1500 Edtu havuzu başına Hello varsayılan en büyük veri depolama veya daha fazla 750 GB'dir.</span><span class="sxs-lookup"><span data-stu-id="a4366-131">hello default max data storage per pool for Premium pools with 1500 eDTUs or more is 750 GB.</span></span> <span data-ttu-id="a4366-132">daha yüksek tooobtain hello _en büyük havuz başına veri depolama boyut_, hello depolama sınırını açıkça ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a4366-132">tooobtain hello higher _max data storage size per pool_, hello storage limit must be explicitly set.</span></span> <span data-ttu-id="a4366-133">Premium 750 GB'den fazla depolama havuzlarıyla şu anda bölgeleri aşağıdaki hello genel önizleme: Doğu ABD 2, Batı ABD, BİZE kamu Virginia, Batı Avrupa, Orta Almanya, Güneydoğu Asya, Japonya Doğu, Avustralya Doğu, Kanada merkezi ve Doğu Kanada.</span><span class="sxs-lookup"><span data-stu-id="a4366-133">Premium pools with more than 750 GB of storage is currently in public preview in hello following regions: East US 2, West US, US Gov Virginia, West Europe, Germany Central, Southeast Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a><span data-ttu-id="a4366-134">Merhaba durumunu havuzunun işlemlerinin Al</span><span class="sxs-lookup"><span data-stu-id="a4366-134">Get hello status of pool operations</span></span>
<span data-ttu-id="a4366-135">Bir esnek havuz oluşturma zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="a4366-135">Creating an elastic pool can take time.</span></span> <span data-ttu-id="a4366-136">oluşturma ve güncelleştirmeler, kullanım hello dahil olmak üzere havuzu işlemlerinin tootrack hello durumu [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="a4366-136">tootrack hello status of pool operations including creation and updates, use hello [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="a4366-137">Bir veritabanı içine ve dışına esnek havuz taşıma hello durumunu Al</span><span class="sxs-lookup"><span data-stu-id="a4366-137">Get hello status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="a4366-138">Bir veritabanını taşıma zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="a4366-138">Moving a database can take time.</span></span> <span data-ttu-id="a4366-139">Hello kullanarak bir taşıma durumunu izlemek [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="a4366-139">Track a move status using hello [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="a4366-140">Esnek havuz için kaynak kullanım verilerini alma</span><span class="sxs-lookup"><span data-stu-id="a4366-140">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="a4366-141">Merhaba kaynak havuzu sınırı yüzdesi olarak alınabilir ölçümleri:</span><span class="sxs-lookup"><span data-stu-id="a4366-141">Metrics that can be retrieved as a percentage of hello resource pool limit:</span></span>

| <span data-ttu-id="a4366-142">Ölçüm adı</span><span class="sxs-lookup"><span data-stu-id="a4366-142">Metric name</span></span> | <span data-ttu-id="a4366-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a4366-143">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a4366-144">CPU\_yüzde</span><span class="sxs-lookup"><span data-stu-id="a4366-144">cpu\_percent</span></span> |<span data-ttu-id="a4366-145">Merhaba havuzunun hello sınırı yüzdesi cinsinden ortalama işlem kullanımı.</span><span class="sxs-lookup"><span data-stu-id="a4366-145">Average compute utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="a4366-146">fiziksel\_veri\_okuma\_yüzde</span><span class="sxs-lookup"><span data-stu-id="a4366-146">physical\_data\_read\_percent</span></span> |<span data-ttu-id="a4366-147">Merhaba havuzu hello sınırının temel yüzde cinsinden ortalama g/ç kullanımı.</span><span class="sxs-lookup"><span data-stu-id="a4366-147">Average I/O utilization in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="a4366-148">Günlük\_yazma\_yüzde</span><span class="sxs-lookup"><span data-stu-id="a4366-148">log\_write\_percent</span></span> |<span data-ttu-id="a4366-149">Ortalama hello sınırı hello havuzunun yüzde olarak kaynak kullanımı yazma.</span><span class="sxs-lookup"><span data-stu-id="a4366-149">Average write resource utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="a4366-150">DTU\_tüketim\_yüzde</span><span class="sxs-lookup"><span data-stu-id="a4366-150">DTU\_consumption\_percent</span></span> |<span data-ttu-id="a4366-151">Merhaba havuzu için eDTU sınırı yüzdesi cinsinden ortalama eDTU kullanımı</span><span class="sxs-lookup"><span data-stu-id="a4366-151">Average eDTU utilization in percentage of eDTU limit for hello pool</span></span> |
| <span data-ttu-id="a4366-152">Depolama\_yüzde</span><span class="sxs-lookup"><span data-stu-id="a4366-152">storage\_percent</span></span> |<span data-ttu-id="a4366-153">Merhaba havuzunun hello depolama sınırı yüzdesi cinsinden ortalama depolama kullanımı.</span><span class="sxs-lookup"><span data-stu-id="a4366-153">Average storage utilization in percentage of hello storage limit of hello pool.</span></span> |
| <span data-ttu-id="a4366-154">Çalışanlar\_yüzde</span><span class="sxs-lookup"><span data-stu-id="a4366-154">workers\_percent</span></span> |<span data-ttu-id="a4366-155">Maksimum eşzamanlı çalışan (istek) hello havuzu hello sınırının temel yüzdesi.</span><span class="sxs-lookup"><span data-stu-id="a4366-155">Maximum concurrent workers (requests) in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="a4366-156">oturumları\_yüzde</span><span class="sxs-lookup"><span data-stu-id="a4366-156">sessions\_percent</span></span> |<span data-ttu-id="a4366-157">En fazla eşzamanlı oturum hello havuzu hello sınırının temel yüzdesi.</span><span class="sxs-lookup"><span data-stu-id="a4366-157">Maximum concurrent sessions in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="a4366-158">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="a4366-158">eDTU_limit</span></span> |<span data-ttu-id="a4366-159">Geçerli en büyük esnek havuz DTU ayarı bu esnek havuz için bu aralığında.</span><span class="sxs-lookup"><span data-stu-id="a4366-159">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="a4366-160">Depolama\_sınırı</span><span class="sxs-lookup"><span data-stu-id="a4366-160">storage\_limit</span></span> |<span data-ttu-id="a4366-161">Geçerli en fazla esnek havuz depolama sınırı bu megabayt cinsinden esnek havuz için bu zaman aralığında ayarlama.</span><span class="sxs-lookup"><span data-stu-id="a4366-161">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="a4366-162">eDTU\_kullanılan</span><span class="sxs-lookup"><span data-stu-id="a4366-162">eDTU\_used</span></span> |<span data-ttu-id="a4366-163">Bu aralık hello havuzunda tarafından kullanılan ortalama Edtu.</span><span class="sxs-lookup"><span data-stu-id="a4366-163">Average eDTUs used by hello pool in this interval.</span></span> |
| <span data-ttu-id="a4366-164">Depolama\_kullanılan</span><span class="sxs-lookup"><span data-stu-id="a4366-164">storage\_used</span></span> |<span data-ttu-id="a4366-165">Bu aralık bayt hello havuzunda tarafından kullanılan ortalama depolama</span><span class="sxs-lookup"><span data-stu-id="a4366-165">Average storage used by hello pool in this interval in bytes</span></span> |

<span data-ttu-id="a4366-166">**Ölçümleri ayrıntı düzeyi/bekletme süreleri:**</span><span class="sxs-lookup"><span data-stu-id="a4366-166">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="a4366-167">5 dakikalık bazda veriler döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a4366-167">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="a4366-168">Veri saklama 35 gün olur.</span><span class="sxs-lookup"><span data-stu-id="a4366-168">Data retention is 35 days.</span></span>  

<span data-ttu-id="a4366-169">Bu cmdlet ve API hello bir çağrı too1000 satırı (yaklaşık 3 gün 5 dakikalık ayrıntı düzeyi, verilerin) alınan satır sayısını sınırlar.</span><span class="sxs-lookup"><span data-stu-id="a4366-169">This cmdlet and API limits hello number of rows that can be retrieved in one call too1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="a4366-170">Ancak daha fazla veri bu komut birden çok kez farklı başlangıç/bitiş zaman aralıkları tooretrieve ile çağrılamaz</span><span class="sxs-lookup"><span data-stu-id="a4366-170">But this command can be called multiple times with different start/end time intervals tooretrieve more data</span></span>

<span data-ttu-id="a4366-171">tooretrieve hello ölçümleri:</span><span class="sxs-lookup"><span data-stu-id="a4366-171">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="a4366-172">Kaynak kullanım verilerini bir esnek havuz için bir veritabanı Al</span><span class="sxs-lookup"><span data-stu-id="a4366-172">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="a4366-173">Bu API'leri anlamsal fark aşağıdaki hello dışında tek bir veritabanının hello kaynak kullanımını izlemek için kullanılan API'leri hello aynı hello şunlardır: alınan ölçümleri başına maksimum veritabanı edtu'ları (veya eşdeğer cap hello için hello yüzdesi olarak ifade edilir Ölçüm CPU veya g/ç gibi temel), havuz için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a4366-173">These APIs are hello same as hello APIs used for monitoring hello resource utilization of a single database, except for hello following semantic difference: metrics retrieved are expressed as a percentage of hello per database max eDTUs (or equivalent cap for hello underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="a4366-174">Örneğin, % 50 kullanımını bu ölçümleri hello belirli kaynak tüketimini hello hello üst havuzunda bu kaynak için veritabanı sınırı her % 50 olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="a4366-174">For example, 50% utilization of any of these metrics indicates that hello specific resource consumption is at 50% of hello per database cap limit for that resource in hello parent pool.</span></span>

<span data-ttu-id="a4366-175">tooretrieve hello ölçümleri:</span><span class="sxs-lookup"><span data-stu-id="a4366-175">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="a4366-176">Bir uyarı tooan esnek havuz kaynak ekleyin</span><span class="sxs-lookup"><span data-stu-id="a4366-176">Add an alert tooan elastic pool resource</span></span>
<span data-ttu-id="a4366-177">Tooan esnek havuz toosend e-posta bildirimleri veya uyarıyı dizeleri çok uyarı kuralları ekleyebilirsiniz[URL uç noktaları](https://msdn.microsoft.com/library/mt718036.aspx) zaman hello esnek havuz isabetler sizin ayarladığınız bir kullanım eşiği.</span><span class="sxs-lookup"><span data-stu-id="a4366-177">You can add alert rules tooan elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when hello elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="a4366-178">Merhaba Ekle-AzureRmMetricAlertRule cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a4366-178">Use hello Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4366-179">Esnek havuzlar için izleme kaynak kullanımı en az 5 dakikalık bir gecikme vardır.</span><span class="sxs-lookup"><span data-stu-id="a4366-179">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="a4366-180">10 dakikadan daha kısa bir süre esnek havuzlar için uyarıları ayarlama şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="a4366-180">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="a4366-181">Nokta esnek havuzlar için herhangi bir uyarı ayarlayın (adlı parametre "-pencereboyutu" PowerShell API'sindeki) 10 dakikadan daha kısa bir süre değil tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="a4366-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="a4366-182">10 dakikalık bir süre (pencereboyutu) veya daha fazla esnek havuzlarını kullanmak için herhangi bir uyarı tanımladığınız olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a4366-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>
>

<span data-ttu-id="a4366-183">Bu örnek, bir esnek havuza ait eDTU tüketim belirli eşiğin gittiğinde bildirim için bir uyarı ekler.</span><span class="sxs-lookup"><span data-stu-id="a4366-183">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

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

<span data-ttu-id="a4366-184">Daha fazla bilgi için bkz: [Azure Portalı'nda SQL veritabanı uyarıları oluşturma](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a4366-184">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a><span data-ttu-id="a4366-185">Bir esnek havuz uyarıları tooall veritabanları ekleme</span><span class="sxs-lookup"><span data-stu-id="a4366-185">Add alerts tooall databases in an elastic pool</span></span>
<span data-ttu-id="a4366-186">Esnek havuz toosend tooall veritabanında e-posta bildirimleri veya uyarıyı dizeleri çok uyarı kuralları ekleyebilirsiniz[URL uç noktaları](https://msdn.microsoft.com/library/mt718036.aspx) ne zaman bir kaynak isabetler hello uyarı tarafından ayarlanan kullanım eşiği.</span><span class="sxs-lookup"><span data-stu-id="a4366-186">You can add alert rules tooall database in an elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by hello alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4366-187">Esnek havuzlar için izleme kaynak kullanımı en az 5 dakikalık bir gecikme vardır.</span><span class="sxs-lookup"><span data-stu-id="a4366-187">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="a4366-188">10 dakikadan daha kısa bir süre esnek havuzlar için uyarıları ayarlama şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="a4366-188">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="a4366-189">Nokta esnek havuzlar için herhangi bir uyarı ayarlayın (adlı parametre "-pencereboyutu" PowerShell API'sindeki) 10 dakikadan daha kısa bir süre değil tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="a4366-189">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="a4366-190">10 dakikalık bir süre (pencereboyutu) veya daha fazla esnek havuzlarını kullanmak için herhangi bir uyarı tanımladığınız olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a4366-190">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>

<span data-ttu-id="a4366-191">Bu örnek bir uyarı tooeach hello veritabanlarının bu veritabanının DTU tüketimi belirli eşiğin üzerinde olduğunda bildirim için esnek havuzdaki ekler.</span><span class="sxs-lookup"><span data-stu-id="a4366-191">This example adds an alert tooeach of hello databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop hello alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="a4366-192">Toplamak ve bir abonelikte birden çok havuz arasında kaynak kullanım verilerini izlemek</span><span class="sxs-lookup"><span data-stu-id="a4366-192">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="a4366-193">Bir abonelikte birçok veritabanı varsa, her esnek havuz ayrı olarak sıkıcı toomonitor var.</span><span class="sxs-lookup"><span data-stu-id="a4366-193">When you have many databases in a subscription, it is cumbersome toomonitor each elastic pool separately.</span></span> <span data-ttu-id="a4366-194">Bunun yerine, SQL veritabanı PowerShell cmdlet'leri ve T-SQL sorgularını birleşik toocollect kaynak kullanım verilerini birden çok havuz ve izleme ve kaynak kullanımını analiz için kendi veritabanlarını olabilir.</span><span class="sxs-lookup"><span data-stu-id="a4366-194">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined toocollect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="a4366-195">A [örnek uygulama](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) gibi birtakım PowerShell betikleri hello GitHub SQL Server örnekleri deposu ne yaptığını üzerinde belgelerle birlikte bulunabilir ve nasıl toouse onu.</span><span class="sxs-lookup"><span data-stu-id="a4366-195">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in hello GitHub SQL Server samples repository along with documentation on what it does and how toouse it.</span></span>

<span data-ttu-id="a4366-196">toouse Bu örnek uygulama aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="a4366-196">toouse this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="a4366-197">Merhaba karşıdan [betikleri ve belgeleri](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span><span class="sxs-lookup"><span data-stu-id="a4366-197">Download hello [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="a4366-198">Ortamınız için başlangıç betiklerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a4366-198">Modify hello scripts for your environment.</span></span> <span data-ttu-id="a4366-199">Esnek havuzlar üzerinde barındırılan bir veya daha fazla sunucuları belirtin.</span><span class="sxs-lookup"><span data-stu-id="a4366-199">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="a4366-200">Merhaba toplanan ölçümleri depolanan toobe nerede telemetri veritabanını belirtin.</span><span class="sxs-lookup"><span data-stu-id="a4366-200">Specify a telemetry database where hello collected metrics are toobe stored.</span></span>
4. <span data-ttu-id="a4366-201">Merhaba betik toospecify hello hello komut yürütme süresini özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a4366-201">Customize hello script toospecify hello duration of hello scripts' execution.</span></span>

<span data-ttu-id="a4366-202">Yüksek bir düzeyde, aşağıdaki hello betikleri hello:</span><span class="sxs-lookup"><span data-stu-id="a4366-202">At a high level, hello scripts do hello following:</span></span>

* <span data-ttu-id="a4366-203">Belirli bir Azure aboneliği (veya belirtilen sunucularının listesini) tüm sunucular numaralandırır.</span><span class="sxs-lookup"><span data-stu-id="a4366-203">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="a4366-204">Her sunucu için bir arka plan işi çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="a4366-204">Runs a background job for each server.</span></span> <span data-ttu-id="a4366-205">Merhaba iş düzenli aralıklarla bir döngüde çalışır ve tüm hello havuzları hello Server'daki telemetri verileri toplar.</span><span class="sxs-lookup"><span data-stu-id="a4366-205">hello job runs in a loop at regular intervals and collects telemetry data for all hello pools in hello server.</span></span> <span data-ttu-id="a4366-206">Ardından hello toplanan verileri hello belirtilen telemetri veritabanına yükler.</span><span class="sxs-lookup"><span data-stu-id="a4366-206">It then loads hello collected data into hello specified telemetry database.</span></span>
* <span data-ttu-id="a4366-207">Her havuzu toocollect hello veritabanı kaynak kullanım verilerini veritabanlarında listesini numaralandırır.</span><span class="sxs-lookup"><span data-stu-id="a4366-207">Enumerates a list of databases in each pool toocollect hello database resource usage data.</span></span> <span data-ttu-id="a4366-208">Ardından hello toplanan verileri hello telemetri veritabanına yükler.</span><span class="sxs-lookup"><span data-stu-id="a4366-208">It then loads hello collected data into hello telemetry database.</span></span>

<span data-ttu-id="a4366-209">Merhaba hello telemetri veritabanında toplanan ölçümleri çözümlenen toomonitor hello durumunu esnek havuzlar ve hello veritabanlarında olabilir.</span><span class="sxs-lookup"><span data-stu-id="a4366-209">hello collected metrics in hello telemetry database can be analyzed toomonitor hello health of elastic pools and hello databases in it.</span></span> <span data-ttu-id="a4366-210">Merhaba betik hello telemetri veritabanı toohelp toplama hello ölçümleri belirtilen zaman penceresi için önceden tanımlanmış Tablo Değerli Fonksiyon (TVF) de yükler.</span><span class="sxs-lookup"><span data-stu-id="a4366-210">hello script also installs a pre-defined Table-Value function (TVF) in hello telemetry database toohelp aggregate hello metrics for a specified time window.</span></span> <span data-ttu-id="a4366-211">Örneğin, hello TVF sonuçlarını olabilir kullanılan tooshow "ilk N esnek havuzları, belirli bir zaman penceresinde hello maksimum eDTU kullanımı ile."</span><span class="sxs-lookup"><span data-stu-id="a4366-211">For example, results of hello TVF can be used tooshow “top N elastic pools with hello maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="a4366-212">İsteğe bağlı olarak, Excel veya Power BI tooquery gibi analitik araçlarını kullanın ve hello toplanan verileri analiz edin.</span><span class="sxs-lookup"><span data-stu-id="a4366-212">Optionally, use analytic tools like Excel or Power BI tooquery and analyze hello collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="a4366-213">Örnek: bir esnek havuz ve veritabanlarını için kaynak tüketimi ölçümlerini alın</span><span class="sxs-lookup"><span data-stu-id="a4366-213">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="a4366-214">Bu örnek, belirli bir esnek havuz ve tüm veritabanları için hello tüketimi ölçümlerini alır.</span><span class="sxs-lookup"><span data-stu-id="a4366-214">This example retrieves hello consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="a4366-215">Toplanan veri biçimlendirilmiş ve tooa .csv biçimlendirilmiş dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="a4366-215">Collected data is formatted and written tooa .csv formatted file.</span></span> <span data-ttu-id="a4366-216">Merhaba dosya Excel ile göz atılacak.</span><span class="sxs-lookup"><span data-stu-id="a4366-216">hello file can be browsed with Excel.</span></span>

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login tooAzure account and select hello subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for hello specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct hello pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format hello metrics and output as .csv file using hello following script block.
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

# Output hello metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="a4366-217">Esnek havuz işlemlerinin gecikme süresi</span><span class="sxs-lookup"><span data-stu-id="a4366-217">Latency of elastic pool operations</span></span>
* <span data-ttu-id="a4366-218">Veritabanı veya en büyük veritabanı başına Edtu başına Hello min Edtu'lar genellikle değiştirme 5 dakika veya daha az tamamlar.</span><span class="sxs-lookup"><span data-stu-id="a4366-218">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="a4366-219">Merhaba Edtu havuzu başına değiştirme hello toplam hello havuzdaki tüm veritabanları tarafından kullanılan alanı miktarına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="a4366-219">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="a4366-220">Değişiklikler 100 GB için ortalama 90 dakika veya daha az sürer.</span><span class="sxs-lookup"><span data-stu-id="a4366-220">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="a4366-221">Örneğin, tarafından kullanılan hello toplam alanı hello havuzdaki tüm veritabanları ise 200 GB hello havuz eDTU havuzu başına değiştirmek için gecikme süresi 3 saattir hello beklenen sonra veya daha az.</span><span class="sxs-lookup"><span data-stu-id="a4366-221">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>



## <a name="next-steps"></a><span data-ttu-id="a4366-222">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a4366-222">Next steps</span></span>
* <span data-ttu-id="a4366-223">[Esnek iş oluşturma](sql-database-elastic-jobs-overview.md) esnek işler hello havuzdaki veritabanları herhangi bir sayıda karşı T-SQL betiklerini çalıştırmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4366-223">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in hello pool.</span></span>
* <span data-ttu-id="a4366-224">Bkz: [Azure SQL veritabanı ile ölçeğini](sql-database-elastic-scale-introduction.md): esnek araçlar tooscale çıkışı kullanın, veri taşıma işlemleri oluşturmak veya sorguyu.</span><span class="sxs-lookup"><span data-stu-id="a4366-224">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools tooscale out, move data, query, or create transactions.</span></span>
