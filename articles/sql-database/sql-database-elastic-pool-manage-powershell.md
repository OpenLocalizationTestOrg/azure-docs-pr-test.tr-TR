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
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a>Oluşturma ve bir esnek havuz PowerShell ile yönetme
Bu konu, nasıl gösterir toocreate ve ölçeklenebilir yönetmek [esnek havuzlar](sql-database-elastic-pool.md) PowerShell ile.  Ayrıca oluşturabilir ve hello kullanarak bir Azure esnek havuzunu yönetme [Azure portal](https://portal.azure.com/), REST API veya [C#](sql-database-elastic-pool-manage-csharp.md). Ayrıca oluşturun ve içine ve dışına esnek havuzlar kullanarak veritabanlarını taşıma [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a>Esnek havuz oluşturma
Merhaba [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet'i bir esnek havuz oluşturur. eDTU havuzu, en az ve maksimum Dtu başına Hello değerlerini hello hizmet katmanı değerine (temel, standart, Premium veya Premium RS) kısıtlanmıştır. Bkz: [esnek havuzlar ve havuza alınmış veritabanları için eDTU ve depolama sınırları](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Havuza alınmış bir veritabanı bir esnek havuz oluşturma
Kullanım hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet'i ve kümesi hello **ElasticPoolName** parametresi toohello hedef havuzu. Varolan bir veritabanını bir esnek havuz toomove bkz [bir veritabanını bir esnek havuza taşıma](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a>Betiğin tamamı
Bir Azure kaynak grubu ve sunucu bu komut dosyasını oluşturur. İstendiğinde, bir yönetici kullanıcı adı ve parolası hello yeni sunucu (Azure kimlik bilgilerinizi değil) sağlayın.

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
Esnek havuzdaki birçok veritabanı oluşturulmasını hello portalı veya aynı anda yalnızca tek bir veritabanı oluşturabilirsiniz PowerShell cmdlet'lerini kullanarak tamamlanınca zaman alabilir. bir esnek havuz tooautomate oluşturma bkz [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).

## <a name="move-a-database-into-an-elastic-pool"></a>Bir veritabanını bir esnek havuza taşıma
Bir veritabanı içine veya dışına hello sahip bir esnek havuz taşıyabilirsiniz [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a>Bir esnek havuz performans ayarlarını değiştir
Performans düşebilir hello havuzu tooaccommodate büyüme hello ayarlarını değiştirebilirler. Kullanım hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet'i. Merhaba - Dtu parametresi toohello Edtu havuzu başına ayarlayın. Bkz: [eDTU ve depolama sınırları](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) olası değerler için.

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a>Bir esnek havuz depolama sınırı Hello değiştirme

Kullanım hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _- StorageMB_ parametresi. Merhaba depolama sınırı MB (örneğin, 2097152 kümeleri hello depolama sınırı too2 TB) sağlayın. Bkz: [eDTU ve depolama sınırları](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) olası değerler için.

> [!IMPORTANT]
> Premium havuzlarıyla 1500 Edtu havuzu başına Hello varsayılan en büyük veri depolama veya daha fazla 750 GB'dir. daha yüksek tooobtain hello _en büyük havuz başına veri depolama boyut_, hello depolama sınırını açıkça ayarlanmalıdır. Premium 750 GB'den fazla depolama havuzlarıyla şu anda bölgeleri aşağıdaki hello genel önizleme: Doğu ABD 2, Batı ABD, BİZE kamu Virginia, Batı Avrupa, Orta Almanya, Güneydoğu Asya, Japonya Doğu, Avustralya Doğu, Kanada merkezi ve Doğu Kanada.

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a>Merhaba durumunu havuzunun işlemlerinin Al
Bir esnek havuz oluşturma zaman alabilir. oluşturma ve güncelleştirmeler, kullanım hello dahil olmak üzere havuzu işlemlerinin tootrack hello durumu [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet'i.

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a>Bir veritabanı içine ve dışına esnek havuz taşıma hello durumunu Al
Bir veritabanını taşıma zaman alabilir. Hello kullanarak bir taşıma durumunu izlemek [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet'i.

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Esnek havuz için kaynak kullanım verilerini alma
Merhaba kaynak havuzu sınırı yüzdesi olarak alınabilir ölçümleri:

| Ölçüm adı | Açıklama |
|:--- |:--- |
| CPU\_yüzde |Merhaba havuzunun hello sınırı yüzdesi cinsinden ortalama işlem kullanımı. |
| fiziksel\_veri\_okuma\_yüzde |Merhaba havuzu hello sınırının temel yüzde cinsinden ortalama g/ç kullanımı. |
| Günlük\_yazma\_yüzde |Ortalama hello sınırı hello havuzunun yüzde olarak kaynak kullanımı yazma. |
| DTU\_tüketim\_yüzde |Merhaba havuzu için eDTU sınırı yüzdesi cinsinden ortalama eDTU kullanımı |
| Depolama\_yüzde |Merhaba havuzunun hello depolama sınırı yüzdesi cinsinden ortalama depolama kullanımı. |
| Çalışanlar\_yüzde |Maksimum eşzamanlı çalışan (istek) hello havuzu hello sınırının temel yüzdesi. |
| oturumları\_yüzde |En fazla eşzamanlı oturum hello havuzu hello sınırının temel yüzdesi. |
| eDTU_limit |Geçerli en büyük esnek havuz DTU ayarı bu esnek havuz için bu aralığında. |
| Depolama\_sınırı |Geçerli en fazla esnek havuz depolama sınırı bu megabayt cinsinden esnek havuz için bu zaman aralığında ayarlama. |
| eDTU\_kullanılan |Bu aralık hello havuzunda tarafından kullanılan ortalama Edtu. |
| Depolama\_kullanılan |Bu aralık bayt hello havuzunda tarafından kullanılan ortalama depolama |

**Ölçümleri ayrıntı düzeyi/bekletme süreleri:**

* 5 dakikalık bazda veriler döndürülür.  
* Veri saklama 35 gün olur.  

Bu cmdlet ve API hello bir çağrı too1000 satırı (yaklaşık 3 gün 5 dakikalık ayrıntı düzeyi, verilerin) alınan satır sayısını sınırlar. Ancak daha fazla veri bu komut birden çok kez farklı başlangıç/bitiş zaman aralıkları tooretrieve ile çağrılamaz

tooretrieve hello ölçümleri:

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a>Kaynak kullanım verilerini bir esnek havuz için bir veritabanı Al
Bu API'leri anlamsal fark aşağıdaki hello dışında tek bir veritabanının hello kaynak kullanımını izlemek için kullanılan API'leri hello aynı hello şunlardır: alınan ölçümleri başına maksimum veritabanı edtu'ları (veya eşdeğer cap hello için hello yüzdesi olarak ifade edilir Ölçüm CPU veya g/ç gibi temel), havuz için ayarlayın. Örneğin, % 50 kullanımını bu ölçümleri hello belirli kaynak tüketimini hello hello üst havuzunda bu kaynak için veritabanı sınırı her % 50 olduğunu gösterir.

tooretrieve hello ölçümleri:

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a>Bir uyarı tooan esnek havuz kaynak ekleyin
Tooan esnek havuz toosend e-posta bildirimleri veya uyarıyı dizeleri çok uyarı kuralları ekleyebilirsiniz[URL uç noktaları](https://msdn.microsoft.com/library/mt718036.aspx) zaman hello esnek havuz isabetler sizin ayarladığınız bir kullanım eşiği. Merhaba Ekle-AzureRmMetricAlertRule cmdlet'ini kullanın.

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

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a>Bir esnek havuz uyarıları tooall veritabanları ekleme
Esnek havuz toosend tooall veritabanında e-posta bildirimleri veya uyarıyı dizeleri çok uyarı kuralları ekleyebilirsiniz[URL uç noktaları](https://msdn.microsoft.com/library/mt718036.aspx) ne zaman bir kaynak isabetler hello uyarı tarafından ayarlanan kullanım eşiği.

> [!IMPORTANT]
> Esnek havuzlar için izleme kaynak kullanımı en az 5 dakikalık bir gecikme vardır. 10 dakikadan daha kısa bir süre esnek havuzlar için uyarıları ayarlama şu anda desteklenmiyor. Nokta esnek havuzlar için herhangi bir uyarı ayarlayın (adlı parametre "-pencereboyutu" PowerShell API'sindeki) 10 dakikadan daha kısa bir süre değil tetiklenebilir. 10 dakikalık bir süre (pencereboyutu) veya daha fazla esnek havuzlarını kullanmak için herhangi bir uyarı tanımladığınız olduğundan emin olun.
>

Bu örnek bir uyarı tooeach hello veritabanlarının bu veritabanının DTU tüketimi belirli eşiğin üzerinde olduğunda bildirim için esnek havuzdaki ekler.

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

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a>Toplamak ve bir abonelikte birden çok havuz arasında kaynak kullanım verilerini izlemek
Bir abonelikte birçok veritabanı varsa, her esnek havuz ayrı olarak sıkıcı toomonitor var. Bunun yerine, SQL veritabanı PowerShell cmdlet'leri ve T-SQL sorgularını birleşik toocollect kaynak kullanım verilerini birden çok havuz ve izleme ve kaynak kullanımını analiz için kendi veritabanlarını olabilir. A [örnek uygulama](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) gibi birtakım PowerShell betikleri hello GitHub SQL Server örnekleri deposu ne yaptığını üzerinde belgelerle birlikte bulunabilir ve nasıl toouse onu.

toouse Bu örnek uygulama aşağıdaki adımları izleyin.

1. Merhaba karşıdan [betikleri ve belgeleri](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):
2. Ortamınız için başlangıç betiklerini değiştirin. Esnek havuzlar üzerinde barındırılan bir veya daha fazla sunucuları belirtin.
3. Merhaba toplanan ölçümleri depolanan toobe nerede telemetri veritabanını belirtin.
4. Merhaba betik toospecify hello hello komut yürütme süresini özelleştirin.

Yüksek bir düzeyde, aşağıdaki hello betikleri hello:

* Belirli bir Azure aboneliği (veya belirtilen sunucularının listesini) tüm sunucular numaralandırır.
* Her sunucu için bir arka plan işi çalıştırır. Merhaba iş düzenli aralıklarla bir döngüde çalışır ve tüm hello havuzları hello Server'daki telemetri verileri toplar. Ardından hello toplanan verileri hello belirtilen telemetri veritabanına yükler.
* Her havuzu toocollect hello veritabanı kaynak kullanım verilerini veritabanlarında listesini numaralandırır. Ardından hello toplanan verileri hello telemetri veritabanına yükler.

Merhaba hello telemetri veritabanında toplanan ölçümleri çözümlenen toomonitor hello durumunu esnek havuzlar ve hello veritabanlarında olabilir. Merhaba betik hello telemetri veritabanı toohelp toplama hello ölçümleri belirtilen zaman penceresi için önceden tanımlanmış Tablo Değerli Fonksiyon (TVF) de yükler. Örneğin, hello TVF sonuçlarını olabilir kullanılan tooshow "ilk N esnek havuzları, belirli bir zaman penceresinde hello maksimum eDTU kullanımı ile." İsteğe bağlı olarak, Excel veya Power BI tooquery gibi analitik araçlarını kullanın ve hello toplanan verileri analiz edin.

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a>Örnek: bir esnek havuz ve veritabanlarını için kaynak tüketimi ölçümlerini alın
Bu örnek, belirli bir esnek havuz ve tüm veritabanları için hello tüketimi ölçümlerini alır. Toplanan veri biçimlendirilmiş ve tooa .csv biçimlendirilmiş dosyasına yazılır. Merhaba dosya Excel ile göz atılacak.

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

## <a name="latency-of-elastic-pool-operations"></a>Esnek havuz işlemlerinin gecikme süresi
* Veritabanı veya en büyük veritabanı başına Edtu başına Hello min Edtu'lar genellikle değiştirme 5 dakika veya daha az tamamlar.
* Merhaba Edtu havuzu başına değiştirme hello toplam hello havuzdaki tüm veritabanları tarafından kullanılan alanı miktarına bağlıdır. Değişiklikler 100 GB için ortalama 90 dakika veya daha az sürer. Örneğin, tarafından kullanılan hello toplam alanı hello havuzdaki tüm veritabanları ise 200 GB hello havuz eDTU havuzu başına değiştirmek için gecikme süresi 3 saattir hello beklenen sonra veya daha az.



## <a name="next-steps"></a>Sonraki adımlar
* [Esnek iş oluşturma](sql-database-elastic-jobs-overview.md) esnek işler hello havuzdaki veritabanları herhangi bir sayıda karşı T-SQL betiklerini çalıştırmanızı sağlar.
* Bkz: [Azure SQL veritabanı ile ölçeğini](sql-database-elastic-scale-introduction.md): esnek araçlar tooscale çıkışı kullanın, veri taşıma işlemleri oluşturmak veya sorguyu.
