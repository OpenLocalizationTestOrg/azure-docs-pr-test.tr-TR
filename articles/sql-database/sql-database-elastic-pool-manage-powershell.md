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
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a>Oluşturma ve bir esnek havuz PowerShell ile yönetme
Bu konuda oluşturmak ve yönetmek nasıl ölçeklenebilir gösterilmektedir [esnek havuzlar](sql-database-elastic-pool.md) PowerShell ile.  Ayrıca oluşturabilir ve bir Azure esnek havuz kullanarak yönetebileceğiniz [Azure portal](https://portal.azure.com/), REST API veya [C#](sql-database-elastic-pool-manage-csharp.md). Ayrıca oluşturun ve içine ve dışına esnek havuzlar kullanarak veritabanlarını taşıma [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a>Esnek havuz oluşturma
[New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet'i bir esnek havuz oluşturur. EDTU havuzu, minimum ve maksimum Dtu değerleri, hizmet katmanı değerine (temel, standart, Premium veya Premium RS) kısıtlanmıştır. Bkz: [esnek havuzlar ve havuza alınmış veritabanları için eDTU ve depolama sınırları](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Havuza alınmış bir veritabanı bir esnek havuz oluşturma
[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet komutunu kullanın ve hedef havuz için **ElasticPoolName** parametresini ayarlayın. Varolan bir veritabanını bir esnek havuza taşımak için bkz: [bir veritabanını bir esnek havuza taşıma](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a>Betiğin tamamı
Bir Azure kaynak grubu ve sunucu bu komut dosyasını oluşturur. İstendiğinde, yeni sunucu için bir yönetici kullanıcı adı ve parola (Azure kimlik bilgilerinizi değil) sağlayın.

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

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a>Bir esnek havuz oluşturma ve birden fazla havuza veritabanı ekleme
Esnek havuzdaki birçok veritabanı oluşturulmasını portalı veya aynı anda yalnızca tek bir veritabanı oluşturabilirsiniz PowerShell cmdlet'lerini kullanarak tamamlanınca zaman alabilir. İçine bir esnek havuz oluşturmayı otomatikleştirmek için bkz: [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).

## <a name="move-a-database-into-an-elastic-pool"></a>Bir veritabanını bir esnek havuza taşıma
Bir veritabanı içine veya dışına sahip bir esnek havuz taşıyabilirsiniz [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a>Bir esnek havuz performans ayarlarını değiştir
Performans düşebilir, büyüme uyum sağlayacak şekilde havuzu ayarlarını değiştirebilirsiniz. Kullanım [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet'i. Havuz başına edtu'larını - Dtu parametreyi ayarlayın. Bkz: [eDTU ve depolama sınırları](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) olası değerler için.

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-the-storage-limit-for-an-elastic-pool"></a>Bir esnek havuz depolama sınırını değiştirme

Kullanım [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) ayarlamak için cmdlet _- StorageMB_ parametresi. (Depolama sınırı 2 TB Örneğin, 2097152 kümeleri) MB cinsinden depolama sınırı sağlar. Bkz: [eDTU ve depolama sınırları](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) olası değerler için.

> [!IMPORTANT]
> Premium havuzlarıyla 1500 Edtu havuzu başına varsayılan en büyük veri depolama veya daha fazla 750 GB'dir. En yüksek elde etmek için _en büyük havuz başına veri depolama boyut_, depolama sınırını açıkça ayarlamanız gerekir. Premium 750 GB'den fazla depolama havuzlarıyla şu anda aşağıdaki bölgelerde genel önizlemede: Doğu ABD 2, Batı ABD, BİZE kamu Virginia, Batı Avrupa, Orta Almanya, Güneydoğu Asya, Japonya Doğu, Avustralya Doğu, Kanada merkezi ve Doğu Kanada.

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-the-status-of-pool-operations"></a>Havuz işlem durumunu Al
Bir esnek havuz oluşturma zaman alabilir. Oluşturma ve güncelleştirmeleri de dahil olmak üzere havuzu işlemleri durumunu izlemek için [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet'i.

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-the-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a>Bir veritabanı içine ve dışına esnek havuz taşıma durumunu Al
Bir veritabanını taşıma zaman alabilir. Kullanarak bir taşıma durumunu izlemek [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet'i.

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Esnek havuz için kaynak kullanım verilerini alma
Kaynak havuzu sınırı yüzdesi olarak alınabilir ölçümleri:

| Ölçüm adı | Açıklama |
|:--- |:--- |
| CPU\_yüzde |Havuz sınırı yüzdesi cinsinden ortalama işlem kullanımı. |
| fiziksel\_veri\_okuma\_yüzde |Yüzde tabanlı havuzunun sınırını ortalama g/ç kullanımı. |
| Günlük\_yazma\_yüzde |Ortalama havuzu sınırının yüzde olarak kaynak kullanımı yazma. |
| DTU\_tüketim\_yüzde |Havuz eDTU sınırı yüzdesi cinsinden ortalama eDTU kullanımı |
| Depolama\_yüzde |Depolama kullanımı havuz depolama sınırı yüzdesi cinsinden ortalama. |
| Çalışanlar\_yüzde |Maksimum eşzamanlı çalışanları (istek) havuzunun sınırını göre yüzdesi. |
| oturumları\_yüzde |Havuzun sınırını göre yüzde cinsinden en fazla eşzamanlı oturum. |
| eDTU_limit |Geçerli en büyük esnek havuz DTU ayarı bu esnek havuz için bu aralığında. |
| Depolama\_sınırı |Geçerli en fazla esnek havuz depolama sınırı bu megabayt cinsinden esnek havuz için bu zaman aralığında ayarlama. |
| eDTU\_kullanılan |Bu aralık havuzunda tarafından kullanılan ortalama Edtu. |
| Depolama\_kullanılan |Bu aralık bayt havuzunda tarafından kullanılan ortalama depolama |

**Ölçümleri ayrıntı düzeyi/bekletme süreleri:**

* 5 dakikalık bazda veriler döndürülür.  
* Veri saklama 35 gün olur.  

Bu cmdlet ve API 1000 satırı (yaklaşık 3 gün 5 dakikalık ayrıntı düzeyi, verilerin) yapılan bir çağrı alınabilir satır sayısını sınırlar. Ancak bu komut, daha fazla veri almak için birden çok kez farklı başlangıç/bitiş zaman aralıkları ile çağrılamaz

Ölçümler alınamadı:

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a>Kaynak kullanım verilerini bir esnek havuz için bir veritabanı Al
Bu API'leri aşağıdaki anlamsal fark dışında tek bir veritabanının kaynak kullanımını izlemek için kullanılan API'leri ile aynıdır: alınan ölçümler bir yüzdesi olarak ifade edilen her veritabanı maksimum Edtu (veya arka plandaki için eşdeğer cap Metrik CPU veya g/ç gibi) için bu havuzu ayarlayın. Örneğin, % 50 kullanımını bu ölçümleri belirli kaynak tüketimini % 50'den gösterir başına veritabanı cap sınırını ana havuzunda bu kaynak için.

Ölçümler alınamadı:

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-to-an-elastic-pool-resource"></a>Bir uyarı için bir esnek havuz kaynak ekleyin
E-posta bildirimleri veya uyarı dizelere göndermek için bir esnek havuz için uyarı kuralı ekleyebilirsiniz [URL uç noktaları](https://msdn.microsoft.com/library/mt718036.aspx) zaman esnek havuz isabetler sizin ayarladığınız bir kullanım eşiği. Add-AzureRmMetricAlertRule cmdlet'ini kullanın.

> [!IMPORTANT]
> Esnek havuzlar için izleme kaynak kullanımı en az 5 dakikalık bir gecikme vardır. 10 dakikadan daha kısa bir süre esnek havuzlar için uyarıları ayarlama şu anda desteklenmiyor. Nokta esnek havuzlar için herhangi bir uyarı ayarlayın (adlı parametre "-pencereboyutu" PowerShell API'sindeki) 10 dakikadan daha kısa bir süre değil tetiklenebilir. 10 dakikalık bir süre (pencereboyutu) veya daha fazla esnek havuzlarını kullanmak için herhangi bir uyarı tanımladığınız olduğundan emin olun.
>
>

Bu örnek, bir esnek havuza ait eDTU tüketim belirli eşiğin gittiğinde bildirim için bir uyarı ekler.

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

Daha fazla bilgi için bkz: [Azure Portalı'nda SQL veritabanı uyarıları oluşturma](sql-database-insights-alerts-portal.md).

## <a name="add-alerts-to-all-databases-in-an-elastic-pool"></a>Esnek havuzdaki tüm veritabanları için uyarıları Ekle
Uyarı kuralları e-posta bildirimleri veya uyarı dizelere göndermek için esnek havuzdaki tüm veritabanı ekleyebileceğiniz [URL uç noktaları](https://msdn.microsoft.com/library/mt718036.aspx) ne zaman bir kaynak isabetler uyarı tarafından ayarlanan kullanım eşiği.

> [!IMPORTANT]
> Esnek havuzlar için izleme kaynak kullanımı en az 5 dakikalık bir gecikme vardır. 10 dakikadan daha kısa bir süre esnek havuzlar için uyarıları ayarlama şu anda desteklenmiyor. Nokta esnek havuzlar için herhangi bir uyarı ayarlayın (adlı parametre "-pencereboyutu" PowerShell API'sindeki) 10 dakikadan daha kısa bir süre değil tetiklenebilir. 10 dakikalık bir süre (pencereboyutu) veya daha fazla esnek havuzlarını kullanmak için herhangi bir uyarı tanımladığınız olduğundan emin olun.
>

Bu örnekte, her bir veritabanının ait DTU tüketimi belirli eşiğin gittiğinde bildirim için esnek havuzdaki veritabanları bir uyarı ekler.

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

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a>Toplamak ve bir abonelikte birden çok havuz arasında kaynak kullanım verilerini izlemek
Bir abonelikte birçok veritabanı varsa, her esnek havuz ayrı ayrı izlemek için sıkıcı. Bunun yerine, SQL veritabanı PowerShell cmdlet'leri ve T-SQL sorgularını birden çok havuz ve kendi veritabanlarını izleme ve kaynak kullanımını analiz için kaynak kullanım verilerini toplamak için birleştirilebilir. A [örnek uygulama](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) gibi birtakım PowerShell komut dosyaları GitHub SQL Server örnekleri depo ne yaptığını ve nasıl kullanılacağını belgelerle birlikte bulunabilir.

Bu örnek uygulama kullanmak için aşağıdaki adımları izleyin.

1. Karşıdan [betikleri ve belgeleri](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):
2. Ortamınız için komut dosyalarını değiştirin. Esnek havuzlar üzerinde barındırılan bir veya daha fazla sunucuları belirtin.
3. Toplanan ölçümleri depolanması nerede telemetri veritabanını belirtin.
4. Komut dosyaları yürütme süresini belirtmek için komut dosyası özelleştirin.

Yüksek düzeyde, komut dosyaları aşağıdakileri yapın:

* Belirli bir Azure aboneliği (veya belirtilen sunucularının listesini) tüm sunucular numaralandırır.
* Her sunucu için bir arka plan işi çalıştırır. İş, düzenli aralıklarla bir döngüde çalışır ve sunucudaki tüm havuzları telemetri verileri toplar. Daha sonra belirtilen telemetri veritabanına toplanan verileri yükler.
* Veritabanı kaynak kullanım verilerini toplamak için her havuzda veritabanlarının listesini numaralandırır. Daha sonra toplanan verileri telemetri veritabanına yükler.

Esnek havuzlar ve veritabanlarında sağlığını izlemek için toplanan ölçümleri telemetri veritabanındaki çözümlenebilir. Komut dosyası, belirtilen zaman penceresi için ölçümleri toplama yardımcı olmak için telemetri veritabanında önceden tanımlanmış Tablo Değerli Fonksiyon (TVF) de yükler. Örneğin, TVF sonuçlarını "üst N esnek havuzları, belirli bir zaman penceresinde maksimum eDTU kullanımı ile." göstermek için kullanılabilir İsteğe bağlı olarak, sorgu ve toplanan verileri çözümlemek için Excel veya Power BI gibi analitik araçlarını kullanın.

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a>Örnek: bir esnek havuz ve veritabanlarını için kaynak tüketimi ölçümlerini alın
Bu örnek, belirli bir esnek havuz ve tüm veritabanları için tüketimi ölçümlerini alır. Toplanan veri biçimlendirilmiş ve biçimlendirilmiş bir .csv dosyasına yazılır. Dosyayı Excel ile göz atılacak.

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

## <a name="latency-of-elastic-pool-operations"></a>Esnek havuz işlemlerinin gecikme süresi
* Veritabanı veya maksimum Edtu başına veritabanı başına minimum edtu'larını genellikle değiştirme 5 dakika veya daha az tamamlar.
* Havuz başına edtu'larını değiştirme havuzdaki tüm veritabanları tarafından kullanılan alanı toplam miktarına bağlıdır. Değişiklikler 100 GB için ortalama 90 dakika veya daha az sürer. Örneğin, toplam alanı tarafından kullanılan havuzdaki tüm veritabanları ise 200 GB havuz eDTU havuzu başına değiştirmek için beklenen gecikme süresi 3 saat sonra veya daha az.



## <a name="next-steps"></a>Sonraki adımlar
* [Esnek iş oluşturma](sql-database-elastic-jobs-overview.md): Esnek işler, havuzda bulunan herhangi bir sayıdaki veritabanı için T-SQL betiklerini çalıştırmanızı sağlar.
* Bkz [Azure SQL veritabanı ile ölçeğini](sql-database-elastic-scale-introduction.md): ölçeğini, verileri taşımak için esnek araçlar kullanın sorgulamak ya da hareketleri oluşturun.
