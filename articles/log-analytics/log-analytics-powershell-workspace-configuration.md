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
# <a name="manage-log-analytics-using-powershell"></a><span data-ttu-id="dd4b4-104">PowerShell kullanarak Log Analytics’i yönetme</span><span class="sxs-lookup"><span data-stu-id="dd4b4-104">Manage Log Analytics using PowerShell</span></span>
<span data-ttu-id="dd4b4-105">Merhaba kullanabilirsiniz [günlük analizi PowerShell cmdlet'leri](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform çeşitli işlevler günlük analizi için bir komut satırından veya bir komut dosyasının parçası olarak.</span><span class="sxs-lookup"><span data-stu-id="dd4b4-105">You can use hello [Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform various functions in Log Analytics from a command line or as part of a script.</span></span>  <span data-ttu-id="dd4b4-106">PowerShell ile gerçekleştirebileceğiniz hello görevler örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="dd4b4-106">Examples of hello tasks you can perform with PowerShell include:</span></span>

* <span data-ttu-id="dd4b4-107">Çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd4b4-107">Create a workspace</span></span>
* <span data-ttu-id="dd4b4-108">Bir çözüm Ekle Kaldır</span><span class="sxs-lookup"><span data-stu-id="dd4b4-108">Add or remove a solution</span></span>
* <span data-ttu-id="dd4b4-109">İçeri ve dışarı aktarma Kaydedilmiş aramaları</span><span class="sxs-lookup"><span data-stu-id="dd4b4-109">Import and export saved searches</span></span>
* <span data-ttu-id="dd4b4-110">Bir bilgisayar grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="dd4b4-110">Create a computer group</span></span>
* <span data-ttu-id="dd4b4-111">Merhaba Windows aracısının yüklü olduğu IIS günlüklerinin bilgisayarlardan toplamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="dd4b4-111">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
* <span data-ttu-id="dd4b4-112">Linux ve Windows bilgisayarlarından performans sayaçlarını Topla</span><span class="sxs-lookup"><span data-stu-id="dd4b4-112">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="dd4b4-113">Linux bilgisayarlarda syslog olaylarını Topla</span><span class="sxs-lookup"><span data-stu-id="dd4b4-113">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="dd4b4-114">Windows olay günlüklerini olaylarını Topla</span><span class="sxs-lookup"><span data-stu-id="dd4b4-114">Collect events from Windows event logs</span></span>
* <span data-ttu-id="dd4b4-115">Özel olay günlüklerini toplayın</span><span class="sxs-lookup"><span data-stu-id="dd4b4-115">Collect custom event logs</span></span>
* <span data-ttu-id="dd4b4-116">Merhaba günlük analizi aracı tooan Azure sanal makine ekleyin</span><span class="sxs-lookup"><span data-stu-id="dd4b4-116">Add hello log analytics agent tooan Azure virtual machine</span></span>
* <span data-ttu-id="dd4b4-117">Günlük analizi tooindex verileri Azure Tanılama'yı kullanarak toplanan yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dd4b4-117">Configure log analytics tooindex data collected using Azure diagnostics</span></span>

<span data-ttu-id="dd4b4-118">Bu makale, bazı Powershell'den gerçekleştirebilirsiniz hello işlevleri gösteren iki kod örnekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="dd4b4-118">This article provides two code samples that illustrate some of hello functions that you can perform from PowerShell.</span></span>  <span data-ttu-id="dd4b4-119">Toohello başvurabilir [günlük analizi PowerShell cmdlet başvurusunun](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) diğer işlevleri için.</span><span class="sxs-lookup"><span data-stu-id="dd4b4-119">You can refer toohello [Log Analytics PowerShell cmdlet reference](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for other functions.</span></span>

> [!NOTE]
> <span data-ttu-id="dd4b4-120">Günlük analizi önceden hello cmdlet'leri kullanılan hello adı olmasının olan Operational Insights çağrıldı.</span><span class="sxs-lookup"><span data-stu-id="dd4b4-120">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello cmdlets.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="dd4b4-121">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="dd4b4-121">Prerequisites</span></span>
<span data-ttu-id="dd4b4-122">Bu örnekler 2.3.0 sürümüyle veya hello AzureRm.OperationalInsights modülün daha sonra çalışır.</span><span class="sxs-lookup"><span data-stu-id="dd4b4-122">These examples work with version 2.3.0 or later of hello AzureRm.OperationalInsights module.</span></span>


## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="dd4b4-123">Oluşturma ve yapılandırma günlük analizi çalışma alanı</span><span class="sxs-lookup"><span data-stu-id="dd4b4-123">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="dd4b4-124">Merhaba aşağıdaki komut dosyası örneği gösterilmektedir nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="dd4b4-124">hello following script sample illustrates how to:</span></span>

1. <span data-ttu-id="dd4b4-125">Çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd4b4-125">Create a workspace</span></span>
2. <span data-ttu-id="dd4b4-126">Liste hello kullanılabilir çözümler</span><span class="sxs-lookup"><span data-stu-id="dd4b4-126">List hello available solutions</span></span>
3. <span data-ttu-id="dd4b4-127">Çözümleri toohello çalışma Ekle</span><span class="sxs-lookup"><span data-stu-id="dd4b4-127">Add solutions toohello workspace</span></span>
4. <span data-ttu-id="dd4b4-128">İçeri aktarma Kaydedilmiş aramaları</span><span class="sxs-lookup"><span data-stu-id="dd4b4-128">Import saved searches</span></span>
5. <span data-ttu-id="dd4b4-129">Dışarı aktarma Kaydedilmiş aramaları</span><span class="sxs-lookup"><span data-stu-id="dd4b4-129">Export saved searches</span></span>
6. <span data-ttu-id="dd4b4-130">Bir bilgisayar grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="dd4b4-130">Create a computer group</span></span>
7. <span data-ttu-id="dd4b4-131">Merhaba Windows aracısının yüklü olduğu IIS günlüklerinin bilgisayarlardan toplamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="dd4b4-131">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
8. <span data-ttu-id="dd4b4-132">Mantıksal Disk performans sayaçlarını Linux bilgisayarından toplar (% kullanılan Inode; Boş megabayt; % Kullanılan alan; Disk aktarımı/sn; Disk Okuma/sn; Disk Yazma/sn)</span><span class="sxs-lookup"><span data-stu-id="dd4b4-132">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
9. <span data-ttu-id="dd4b4-133">Linux bilgisayarlardan Syslog olaylarını Topla</span><span class="sxs-lookup"><span data-stu-id="dd4b4-133">Collect syslog events from Linux computers</span></span>
10. <span data-ttu-id="dd4b4-134">Merhaba uygulama olay günlüğüne Windows bilgisayarlardan hata ve uyarı olayları toplar</span><span class="sxs-lookup"><span data-stu-id="dd4b4-134">Collect Error and Warning events from hello Application Event Log from Windows computers</span></span>
11. <span data-ttu-id="dd4b4-135">Windows bilgisayarlardan bellek kullanılabilir MBayt performans sayacı Topla</span><span class="sxs-lookup"><span data-stu-id="dd4b4-135">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
12. <span data-ttu-id="dd4b4-136">Özel günlük Topla</span><span class="sxs-lookup"><span data-stu-id="dd4b4-136">Collect a custom log</span></span> 

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

## <a name="configuring-log-analytics-tooindex-azure-diagnostics"></a><span data-ttu-id="dd4b4-137">Günlük analizi tooindex Azure Tanılama'yı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dd4b4-137">Configuring Log Analytics tooindex Azure diagnostics</span></span>
<span data-ttu-id="dd4b4-138">Azure kaynaklarını aracısız izleme için hello kaynakları toohave Azure tanılama etkinleştirilmiş ve yapılandırılmış toowrite tooa günlük analizi çalışma alanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd4b4-138">For agentless monitoring of Azure resources, hello resources need toohave Azure diagnostics enabled and configured toowrite tooa Log Analytics workspace.</span></span> <span data-ttu-id="dd4b4-139">Bu yaklaşım verileri gönderir doğrudan tooLog analizi ve tooa depolama hesabına yazılan veri toobe gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="dd4b4-139">This approach sends data directly tooLog Analytics and does not require data toobe written tooa storage account.</span></span> <span data-ttu-id="dd4b4-140">Desteklenen kaynaklar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="dd4b4-140">Supported resources include:</span></span>

| <span data-ttu-id="dd4b4-141">Kaynak Türü</span><span class="sxs-lookup"><span data-stu-id="dd4b4-141">Resource Type</span></span> | <span data-ttu-id="dd4b4-142">Günlükler</span><span class="sxs-lookup"><span data-stu-id="dd4b4-142">Logs</span></span> | <span data-ttu-id="dd4b4-143">Ölçümler</span><span class="sxs-lookup"><span data-stu-id="dd4b4-143">Metrics</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd4b4-144">Application Gatewayler</span><span class="sxs-lookup"><span data-stu-id="dd4b4-144">Application Gateways</span></span>    | <span data-ttu-id="dd4b4-145">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-145">Yes</span></span> | <span data-ttu-id="dd4b4-146">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-146">Yes</span></span> |
| <span data-ttu-id="dd4b4-147">Automation hesapları</span><span class="sxs-lookup"><span data-stu-id="dd4b4-147">Automation accounts</span></span>     | <span data-ttu-id="dd4b4-148">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-148">Yes</span></span> | |
| <span data-ttu-id="dd4b4-149">Toplu hesaplar</span><span class="sxs-lookup"><span data-stu-id="dd4b4-149">Batch accounts</span></span>          | <span data-ttu-id="dd4b4-150">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-150">Yes</span></span> | <span data-ttu-id="dd4b4-151">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-151">Yes</span></span> |
| <span data-ttu-id="dd4b4-152">Data Lake analizi</span><span class="sxs-lookup"><span data-stu-id="dd4b4-152">Data Lake analytics</span></span>     | <span data-ttu-id="dd4b4-153">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-153">Yes</span></span> | | 
| <span data-ttu-id="dd4b4-154">Veri Gölü deposu</span><span class="sxs-lookup"><span data-stu-id="dd4b4-154">Data Lake store</span></span>         | <span data-ttu-id="dd4b4-155">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-155">Yes</span></span> | |
| <span data-ttu-id="dd4b4-156">SQL esnek havuzu</span><span class="sxs-lookup"><span data-stu-id="dd4b4-156">Elastic SQL Pool</span></span>        |     | <span data-ttu-id="dd4b4-157">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-157">Yes</span></span> |
| <span data-ttu-id="dd4b4-158">Olay Hub'ad alanı</span><span class="sxs-lookup"><span data-stu-id="dd4b4-158">Event Hub namespace</span></span>     |     | <span data-ttu-id="dd4b4-159">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-159">Yes</span></span> |
| <span data-ttu-id="dd4b4-160">IOT hub'ları</span><span class="sxs-lookup"><span data-stu-id="dd4b4-160">IoT Hubs</span></span>                |     | <span data-ttu-id="dd4b4-161">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-161">Yes</span></span> |
| <span data-ttu-id="dd4b4-162">Anahtar Kasası</span><span class="sxs-lookup"><span data-stu-id="dd4b4-162">Key Vault</span></span>               | <span data-ttu-id="dd4b4-163">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-163">Yes</span></span> | |
| <span data-ttu-id="dd4b4-164">Yük Dengeleyici</span><span class="sxs-lookup"><span data-stu-id="dd4b4-164">Load Balancers</span></span>          | <span data-ttu-id="dd4b4-165">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-165">Yes</span></span> | |
| <span data-ttu-id="dd4b4-166">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="dd4b4-166">Logic Apps</span></span>              | <span data-ttu-id="dd4b4-167">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-167">Yes</span></span> | <span data-ttu-id="dd4b4-168">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-168">Yes</span></span> |
| <span data-ttu-id="dd4b4-169">Ağ Güvenlik Grupları</span><span class="sxs-lookup"><span data-stu-id="dd4b4-169">Network Security Groups</span></span> | <span data-ttu-id="dd4b4-170">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-170">Yes</span></span> | |
| <span data-ttu-id="dd4b4-171">Redis Önbelleği</span><span class="sxs-lookup"><span data-stu-id="dd4b4-171">Redis Cache</span></span>             |     | <span data-ttu-id="dd4b4-172">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-172">Yes</span></span> |
| <span data-ttu-id="dd4b4-173">Hizmet ara</span><span class="sxs-lookup"><span data-stu-id="dd4b4-173">Search services</span></span>         | <span data-ttu-id="dd4b4-174">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-174">Yes</span></span> | <span data-ttu-id="dd4b4-175">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-175">Yes</span></span> |
| <span data-ttu-id="dd4b4-176">Hizmet veri yolu ad alanı</span><span class="sxs-lookup"><span data-stu-id="dd4b4-176">Service Bus namespace</span></span>   |     | <span data-ttu-id="dd4b4-177">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-177">Yes</span></span> |
| <span data-ttu-id="dd4b4-178">SQL (v12)</span><span class="sxs-lookup"><span data-stu-id="dd4b4-178">SQL (v12)</span></span>               |     | <span data-ttu-id="dd4b4-179">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-179">Yes</span></span> |
| <span data-ttu-id="dd4b4-180">Web Siteleri</span><span class="sxs-lookup"><span data-stu-id="dd4b4-180">Web Sites</span></span>               |     | <span data-ttu-id="dd4b4-181">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-181">Yes</span></span> |
| <span data-ttu-id="dd4b4-182">Web sunucu grupları</span><span class="sxs-lookup"><span data-stu-id="dd4b4-182">Web Server farms</span></span>        |     | <span data-ttu-id="dd4b4-183">Evet</span><span class="sxs-lookup"><span data-stu-id="dd4b4-183">Yes</span></span> |

<span data-ttu-id="dd4b4-184">Merhaba kullanılabilir ölçümler Hello ayrıntılarını çok başvuran[ölçümleri Azure İzleyicisi ile desteklenen](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="dd4b4-184">For hello details of hello available metrics, refer too[supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="dd4b4-185">Merhaba kullanılabilir günlüklerini Hello ayrıntılarını çok başvuran[desteklenen Hizmetleri ve şema için tanılama günlüklerini](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span><span class="sxs-lookup"><span data-stu-id="dd4b4-185">For hello details of hello available logs, refer too[supported services and schema for diagnostic logs](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span></span>

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

<span data-ttu-id="dd4b4-186">Cmdlet toocollect farklı Aboneliklerde bulunan kaynaklar günlüklerinden önceki hello de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd4b4-186">You can also use hello preceding cmdlet toocollect logs from resources that are in different subscriptions.</span></span> <span data-ttu-id="dd4b4-187">Merhaba cmdlet günlükleri oluşturma hem hello kaynağın hello kimliği sağlanmaktadır ve hello çalışma hello günlükleri gönderilen abonelikler arasında mümkün toowork taşımaktadır.</span><span class="sxs-lookup"><span data-stu-id="dd4b4-187">hello cmdlet is able toowork across subscriptions since you are providing hello id of both hello resource creating logs and hello workspace hello logs are sent to.</span></span>


## <a name="configuring-log-analytics-tooindex-azure-diagnostics-from-storage"></a><span data-ttu-id="dd4b4-188">Günlük analizi tooindex Azure tanılama depolama biriminden yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dd4b4-188">Configuring Log Analytics tooindex Azure diagnostics from storage</span></span>
<span data-ttu-id="dd4b4-189">toocollect günlük içindeki verileri Klasik bulut hizmeti ya da bir service fabric kümesi, çalışan bir örneği, toofirst yazma hello veri tooAzure depolama gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd4b4-189">toocollect log data from within a running instance of a classic cloud service or a service fabric cluster, you need toofirst write hello data tooAzure storage.</span></span> <span data-ttu-id="dd4b4-190">Günlük analizi durumda toocollect hello günlükleri hello depolama hesabından yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="dd4b4-190">Log Analytics is then configured toocollect hello logs from hello storage account.</span></span> <span data-ttu-id="dd4b4-191">Desteklenen kaynaklar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="dd4b4-191">Supported resources include:</span></span>

* <span data-ttu-id="dd4b4-192">Klasik bulut Hizmetleri (web ve çalışan rolleri)</span><span class="sxs-lookup"><span data-stu-id="dd4b4-192">Classic cloud services (web and worker roles)</span></span>
* <span data-ttu-id="dd4b4-193">Service fabric kümeleri</span><span class="sxs-lookup"><span data-stu-id="dd4b4-193">Service fabric clusters</span></span>

<span data-ttu-id="dd4b4-194">örnekte gösterildiği nasıl aşağıdaki hello için:</span><span class="sxs-lookup"><span data-stu-id="dd4b4-194">hello following example shows how to:</span></span>

1. <span data-ttu-id="dd4b4-195">Liste hello var olan depolama hesapları ve günlük analizi veri dizinini oluşturacak konumları</span><span class="sxs-lookup"><span data-stu-id="dd4b4-195">List hello existing storage accounts and locations that Log Analytics will index data from</span></span>
2. <span data-ttu-id="dd4b4-196">Bir depolama hesabından bir yapılandırma tooread oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd4b4-196">Create a configuration tooread from a storage account</span></span>
3. <span data-ttu-id="dd4b4-197">Yeni yapılandırma tooindex verileri ek konumlardan oluşturulan hello güncelleştir</span><span class="sxs-lookup"><span data-stu-id="dd4b4-197">Update hello newly created configuration tooindex data from additional locations</span></span>
4. <span data-ttu-id="dd4b4-198">Yeni oluşturulan hello yapılandırmasını silme</span><span class="sxs-lookup"><span data-stu-id="dd4b4-198">Delete hello newly created configuration</span></span>

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

<span data-ttu-id="dd4b4-199">Komut dosyası toocollect günlükleri depolama hesaplarından farklı Aboneliklerde önceki hello de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd4b4-199">You can also use hello preceding script toocollect logs from storage accounts in different subscriptions.</span></span> <span data-ttu-id="dd4b4-200">Merhaba betik mümkün toowork abonelikler arasında olduğu hello depolama hesabı kaynak kimliği ve karşılık gelen bir erişim anahtarı sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="dd4b4-200">hello script is able toowork across subscriptions since you are providing hello storage account resource id and a corresponding access key.</span></span> <span data-ttu-id="dd4b4-201">Merhaba erişim tuşu değiştirdiğinizde, tooupdate hello depolama Insight toohave hello yeni anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd4b4-201">When you change hello access key, you need tooupdate hello storage insight toohave hello new key.</span></span>


## <a name="next-steps"></a><span data-ttu-id="dd4b4-202">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dd4b4-202">Next steps</span></span>
* <span data-ttu-id="dd4b4-203">[Günlük analizi PowerShell cmdlet'leri gözden](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) günlük analizi yapılandırması için PowerShell kullanma hakkında ek bilgi için.</span><span class="sxs-lookup"><span data-stu-id="dd4b4-203">[Review Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for additional information on using PowerShell for configuration of Log Analytics.</span></span>

