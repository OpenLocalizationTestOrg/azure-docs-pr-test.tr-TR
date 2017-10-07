---
title: "aaaUse PowerShell tooCreate ve günlük analizi çalışma alanı yapılandırma | Microsoft Docs"
description: "Altyapı Bulut veya şirket içi sunuculardan Analytics kullanım verilerini oturum. Azure tanılama tarafından oluşturulan zaman Azure depolama biriminden makine verilerini toplayabilir."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 3b9b7ade-3374-4596-afb1-51b695f481c2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: powershell
ms.topic: article
ms.date: 11/21/2016
ms.author: richrund
ms.openlocfilehash: a6d66194204cc58de6aafb687a19fe9611e0c58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-log-analytics-using-powershell"></a>PowerShell kullanarak Log Analytics’i yönetme
Merhaba kullanabilirsiniz [günlük analizi PowerShell cmdlet'leri](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform çeşitli işlevler günlük analizi için bir komut satırından veya bir komut dosyasının parçası olarak.  PowerShell ile gerçekleştirebileceğiniz hello görevler örnekleri şunlardır:

* Çalışma alanı oluşturma
* Bir çözüm Ekle Kaldır
* İçeri ve dışarı aktarma Kaydedilmiş aramaları
* Bir bilgisayar grubu oluşturun
* Merhaba Windows aracısının yüklü olduğu IIS günlüklerinin bilgisayarlardan toplamayı etkinleştir
* Linux ve Windows bilgisayarlarından performans sayaçlarını Topla
* Linux bilgisayarlarda syslog olaylarını Topla 
* Windows olay günlüklerini olaylarını Topla
* Özel olay günlüklerini toplayın
* Merhaba günlük analizi aracı tooan Azure sanal makine ekleyin
* Günlük analizi tooindex verileri Azure Tanılama'yı kullanarak toplanan yapılandırma

Bu makale, bazı Powershell'den gerçekleştirebilirsiniz hello işlevleri gösteren iki kod örnekleri sağlar.  Toohello başvurabilir [günlük analizi PowerShell cmdlet başvurusunun](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) diğer işlevleri için.

> [!NOTE]
> Günlük analizi önceden hello cmdlet'leri kullanılan hello adı olmasının olan Operational Insights çağrıldı.
> 
> 

## <a name="prerequisites"></a>Ön koşullar
Bu örnekler 2.3.0 sürümüyle veya hello AzureRm.OperationalInsights modülün daha sonra çalışır.


## <a name="create-and-configure-a-log-analytics-workspace"></a>Oluşturma ve yapılandırma günlük analizi çalışma alanı
Merhaba aşağıdaki komut dosyası örneği gösterilmektedir nasıl yapılır:

1. Çalışma alanı oluşturma
2. Liste hello kullanılabilir çözümler
3. Çözümleri toohello çalışma Ekle
4. İçeri aktarma Kaydedilmiş aramaları
5. Dışarı aktarma Kaydedilmiş aramaları
6. Bir bilgisayar grubu oluşturun
7. Merhaba Windows aracısının yüklü olduğu IIS günlüklerinin bilgisayarlardan toplamayı etkinleştir
8. Mantıksal Disk performans sayaçlarını Linux bilgisayarından toplar (% kullanılan Inode; Boş megabayt; % Kullanılan alan; Disk aktarımı/sn; Disk Okuma/sn; Disk Yazma/sn)
9. Linux bilgisayarlardan Syslog olaylarını Topla
10. Merhaba uygulama olay günlüğüne Windows bilgisayarlardan hata ve uyarı olayları toplar
11. Windows bilgisayarlardan bellek kullanılabilir MBayt performans sayacı Topla
12. Özel günlük Topla 

```

$ResourceGroup = "oms-example"
$WorkspaceName = "log-analytics-" + (Get-Random -Maximum 99999) # workspace names need toobe unique - Get-Random helps with this for hello example code
$Location = "westeurope"

# List of solutions tooenable
$Solutions = "Security", "Updates", "SQLAssessment"

# Saved Searches tooimport
$ExportedSearches = @"
[
    {
        "Category":  "My Saved Searches",
        "DisplayName":  "WAD Events (All)",
        "Query":  "Type=Event SourceSystem:AzureStorage ",
        "Version":  1
    },
    {        
        "Category":  "My Saved Searches",
        "DisplayName":  "Current Disk Queue Length",
        "Query":  "Type=Perf ObjectName=LogicalDisk InstanceName=\"C:\" CounterName=\"Current Disk Queue Length\"",
        "Version":  1
    }
]
"@ | ConvertFrom-Json

# Custom Log toocollect
$CustomLog = @"
{
    "customLogName": "sampleCustomLog1", 
    "description": "Example custom log datasource", 
    "inputs": [
        { 
            "location": { 
            "fileSystemLocations": { 
                "windowsFileTypeLogPaths": [ "e:\\iis5\\*.log" ], 
                "linuxFileTypeLogPaths": [ "/var/logs" ] 
                } 
            }, 
        "recordDelimiter": { 
            "regexDelimiter": { 
                "pattern": "\\n", 
                "matchIndex": 0, 
                "matchIndexSpecified": true, 
                "numberedGroup": null 
                } 
            } 
        }
    ], 
    "extractions": [
        { 
            "extractionName": "TimeGenerated", 
            "extractionType": "DateTime", 
            "extractionProperties": { 
                "dateTimeExtraction": { 
                    "regex": null, 
                    "joinStringRegex": null 
                    } 
                } 
            }
        ] 
    }
"@

# Create hello resource group if needed
try {
    Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop
} catch {
    New-AzureRmResourceGroup -Name $ResourceGroup -Location $Location
}

# Create hello workspace
New-AzureRmOperationalInsightsWorkspace -Location $Location -Name $WorkspaceName -Sku Standard -ResourceGroupName $ResourceGroup

# List all solutions and their installation status
Get-AzureRmOperationalInsightsIntelligencePacks -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Add solutions
foreach ($solution in $Solutions) {
    Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -IntelligencePackName $solution -Enabled $true
}

#List enabled solutions
(Get-AzureRmOperationalInsightsIntelligencePacks -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName).Where({($_.enabled -eq $true)})

# Import Saved Searches
foreach ($search in $ExportedSearches) {
    $id = $search.Category + "|" + $search.DisplayName
    New-AzureRmOperationalInsightsSavedSearch -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId $id -DisplayName $search.DisplayName -Category $search.Category -Query $search.Query -Version $search.Version
}

# Export Saved Searches
(Get-AzureRmOperationalInsightsSavedSearch -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName).Value.Properties | ConvertTo-Json 

# Create Computer Group based on a query
New-AzureRmOperationalInsightsComputerGroup -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId "My Web Servers" -DisplayName "Web Servers" -Category "My Saved Searches" -Query "Computer=""web*"" | distinct Computer" -Version 1

# Create a computer group based on names (up too5000)
$computerGroup = """servername1.contoso.com"",""servername2.contoso.com"",""servername3.contoso.com"",""servername4.contoso.com"""
New-AzureRmOperationalInsightsComputerGroup -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId "My Named Servers" -DisplayName "Named Servers" -Category "My Saved Searches" -Query $computerGroup -Version 1

# Enable IIS Log Collection using agent
Enable-AzureRmOperationalInsightsIISLogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Linux Perf
New-AzureRmOperationalInsightsLinuxPerformanceObjectDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -ObjectName "Logical Disk" -InstanceName "*"  -CounterNames @("% Used Inodes", "Free Megabytes", "% Used Space", "Disk Transfers/sec", "Disk Reads/sec", "Disk Reads/sec", "Disk Writes/sec") -IntervalSeconds 20  -Name "Example Linux Disk Performance Counters"
Enable-AzureRmOperationalInsightsLinuxCustomLogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Linux Syslog
New-AzureRmOperationalInsightsLinuxSyslogDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -Facility "kern" -CollectEmergency -CollectAlert -CollectCritical -CollectError -CollectWarning -Name "Example kernal syslog collection"
Enable-AzureRmOperationalInsightsLinuxSyslogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Windows Event
New-AzureRmOperationalInsightsWindowsEventDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -EventLogName "Application" -CollectErrors -CollectWarnings -Name "Example Application Event Log"

# Windows Perf
New-AzureRmOperationalInsightsWindowsPerformanceCounterDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -ObjectName "Memory" -InstanceName "*" -CounterName "Available MBytes" -IntervalSeconds 20 -Name "Example Windows Performance Counter"

# Custom Logs
New-AzureRmOperationalInsightsCustomLogDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -CustomLogRawJson "$CustomLog" -Name "Example Custom Log Collection"

```

## <a name="configuring-log-analytics-tooindex-azure-diagnostics"></a>Günlük analizi tooindex Azure Tanılama'yı yapılandırma
Azure kaynaklarını aracısız izleme için hello kaynakları toohave Azure tanılama etkinleştirilmiş ve yapılandırılmış toowrite tooa günlük analizi çalışma alanı gerekir. Bu yaklaşım verileri gönderir doğrudan tooLog analizi ve tooa depolama hesabına yazılan veri toobe gerektirmez. Desteklenen kaynaklar şunlardır:

| Kaynak Türü | Günlükler | Ölçümler |
| --- | --- | --- |
| Application Gatewayler    | Evet | Evet |
| Automation hesapları     | Evet | |
| Toplu hesaplar          | Evet | Evet |
| Data Lake analizi     | Evet | | 
| Veri Gölü deposu         | Evet | |
| SQL esnek havuzu        |     | Evet |
| Olay Hub'ad alanı     |     | Evet |
| IOT hub'ları                |     | Evet |
| Anahtar Kasası               | Evet | |
| Yük Dengeleyici          | Evet | |
| Logic Apps              | Evet | Evet |
| Ağ Güvenlik Grupları | Evet | |
| Redis Önbelleği             |     | Evet |
| Hizmet ara         | Evet | Evet |
| Hizmet veri yolu ad alanı   |     | Evet |
| SQL (v12)               |     | Evet |
| Web Siteleri               |     | Evet |
| Web sunucu grupları        |     | Evet |

Merhaba kullanılabilir ölçümler Hello ayrıntılarını çok başvuran[ölçümleri Azure İzleyicisi ile desteklenen](../monitoring-and-diagnostics/monitoring-supported-metrics.md).

Merhaba kullanılabilir günlüklerini Hello ayrıntılarını çok başvuran[desteklenen Hizmetleri ve şema için tanılama günlüklerini](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

Cmdlet toocollect farklı Aboneliklerde bulunan kaynaklar günlüklerinden önceki hello de kullanabilirsiniz. Merhaba cmdlet günlükleri oluşturma hem hello kaynağın hello kimliği sağlanmaktadır ve hello çalışma hello günlükleri gönderilen abonelikler arasında mümkün toowork taşımaktadır.


## <a name="configuring-log-analytics-tooindex-azure-diagnostics-from-storage"></a>Günlük analizi tooindex Azure tanılama depolama biriminden yapılandırma
toocollect günlük içindeki verileri Klasik bulut hizmeti ya da bir service fabric kümesi, çalışan bir örneği, toofirst yazma hello veri tooAzure depolama gerekir. Günlük analizi durumda toocollect hello günlükleri hello depolama hesabından yapılandırılmış. Desteklenen kaynaklar şunlardır:

* Klasik bulut Hizmetleri (web ve çalışan rolleri)
* Service fabric kümeleri

örnekte gösterildiği nasıl aşağıdaki hello için:

1. Liste hello var olan depolama hesapları ve günlük analizi veri dizinini oluşturacak konumları
2. Bir depolama hesabından bir yapılandırma tooread oluşturma
3. Yeni yapılandırma tooindex verileri ek konumlardan oluşturulan hello güncelleştir
4. Yeni oluşturulan hello yapılandırmasını silme

```
# validTables = "WADWindowsEventLogsTable", "LinuxsyslogVer2v0", "WADServiceFabric*EventTable", "WADETWEventTable" 
$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq "your workspace name"})

# Update these two lines with hello storage account resource ID and hello storage account key for hello storage account you want tooLog Analytics too 
$storageId = "/subscriptions/ec11ca60-1234-491e-5678-0ea07feae25c/resourceGroups/demo/providers/Microsoft.Storage/storageAccounts/wadv2storage"
$key = "abcd=="

# List existing insights
Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

# Create a new insight
New-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -StorageAccountResourceId $storageId -StorageAccountKey $key -Tables @("WADWindowsEventLogsTable") -Containers @("wad-iis-logfiles")

# Update existing insight
Set-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -Tables @("WADWindowsEventLogsTable", "WADETWEventTable") -Containers @("wad-iis-logfiles")

# Remove hello insight
Remove-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" 

```

Komut dosyası toocollect günlükleri depolama hesaplarından farklı Aboneliklerde önceki hello de kullanabilirsiniz. Merhaba betik mümkün toowork abonelikler arasında olduğu hello depolama hesabı kaynak kimliği ve karşılık gelen bir erişim anahtarı sağlanmaktadır. Merhaba erişim tuşu değiştirdiğinizde, tooupdate hello depolama Insight toohave hello yeni anahtarı gerekir.


## <a name="next-steps"></a>Sonraki adımlar
* [Günlük analizi PowerShell cmdlet'leri gözden](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) günlük analizi yapılandırması için PowerShell kullanma hakkında ek bilgi için.

