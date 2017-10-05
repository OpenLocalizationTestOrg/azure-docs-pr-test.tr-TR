---
title: "Oluşturma ve bir günlük analizi çalışma alanı yapılandırmak için PowerShell kullanın | Microsoft Docs"
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
ms.openlocfilehash: 6807ab67e3593da82c147669b29bfdae3b6c967c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-log-analytics-using-powershell"></a><span data-ttu-id="0d46b-104">PowerShell kullanarak Log Analytics’i yönetme</span><span class="sxs-lookup"><span data-stu-id="0d46b-104">Manage Log Analytics using PowerShell</span></span>
<span data-ttu-id="0d46b-105">Kullanabileceğiniz [günlük analizi PowerShell cmdlet'leri](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) bir komut satırından veya bir komut dosyasının parçası olarak günlük analizi çeşitli işlevleri gerçekleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="0d46b-105">You can use the [Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) to perform various functions in Log Analytics from a command line or as part of a script.</span></span>  <span data-ttu-id="0d46b-106">PowerShell ile gerçekleştirebileceğiniz görevler örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0d46b-106">Examples of the tasks you can perform with PowerShell include:</span></span>

* <span data-ttu-id="0d46b-107">Çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0d46b-107">Create a workspace</span></span>
* <span data-ttu-id="0d46b-108">Bir çözüm Ekle Kaldır</span><span class="sxs-lookup"><span data-stu-id="0d46b-108">Add or remove a solution</span></span>
* <span data-ttu-id="0d46b-109">İçeri ve dışarı aktarma Kaydedilmiş aramaları</span><span class="sxs-lookup"><span data-stu-id="0d46b-109">Import and export saved searches</span></span>
* <span data-ttu-id="0d46b-110">Bir bilgisayar grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="0d46b-110">Create a computer group</span></span>
* <span data-ttu-id="0d46b-111">Windows aracısının yüklü olduğu IIS günlüklerinin bilgisayarlardan toplamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="0d46b-111">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
* <span data-ttu-id="0d46b-112">Linux ve Windows bilgisayarlarından performans sayaçlarını Topla</span><span class="sxs-lookup"><span data-stu-id="0d46b-112">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="0d46b-113">Linux bilgisayarlarda syslog olaylarını Topla</span><span class="sxs-lookup"><span data-stu-id="0d46b-113">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="0d46b-114">Windows olay günlüklerini olaylarını Topla</span><span class="sxs-lookup"><span data-stu-id="0d46b-114">Collect events from Windows event logs</span></span>
* <span data-ttu-id="0d46b-115">Özel olay günlüklerini toplayın</span><span class="sxs-lookup"><span data-stu-id="0d46b-115">Collect custom event logs</span></span>
* <span data-ttu-id="0d46b-116">Bir Azure sanal makinesi için günlük analizi Aracısı Ekle</span><span class="sxs-lookup"><span data-stu-id="0d46b-116">Add the log analytics agent to an Azure virtual machine</span></span>
* <span data-ttu-id="0d46b-117">Azure Tanılama'yı kullanarak toplanan dizin verileri için günlük analizi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0d46b-117">Configure log analytics to index data collected using Azure diagnostics</span></span>

<span data-ttu-id="0d46b-118">Bu makale, bazı Powershell'den gerçekleştirebileceğiniz işlevlerin göstermek iki kod örnekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="0d46b-118">This article provides two code samples that illustrate some of the functions that you can perform from PowerShell.</span></span>  <span data-ttu-id="0d46b-119">Başvurabilirsiniz [günlük analizi PowerShell cmdlet başvurusunun](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) diğer işlevleri için.</span><span class="sxs-lookup"><span data-stu-id="0d46b-119">You can refer to the [Log Analytics PowerShell cmdlet reference](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for other functions.</span></span>

> [!NOTE]
> <span data-ttu-id="0d46b-120">Günlük analizi daha önce yer alan cmdlet'ler kullanılan ad olmasının olan Operational Insights çağrıldı.</span><span class="sxs-lookup"><span data-stu-id="0d46b-120">Log Analytics was previously called Operational Insights, which is why it is the name used in the cmdlets.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="0d46b-121">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0d46b-121">Prerequisites</span></span>
<span data-ttu-id="0d46b-122">Bu örnekler 2.3.0 sürümüyle ya da daha sonra AzureRm.OperationalInsights modülün çalışır.</span><span class="sxs-lookup"><span data-stu-id="0d46b-122">These examples work with version 2.3.0 or later of the AzureRm.OperationalInsights module.</span></span>


## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="0d46b-123">Oluşturma ve yapılandırma günlük analizi çalışma alanı</span><span class="sxs-lookup"><span data-stu-id="0d46b-123">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="0d46b-124">Aşağıdaki komut dosyası örneği gösterilmektedir nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="0d46b-124">The following script sample illustrates how to:</span></span>

1. <span data-ttu-id="0d46b-125">Çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0d46b-125">Create a workspace</span></span>
2. <span data-ttu-id="0d46b-126">Var olan çözümlerinin listesi</span><span class="sxs-lookup"><span data-stu-id="0d46b-126">List the available solutions</span></span>
3. <span data-ttu-id="0d46b-127">Çalışma Alanı'na çözümleri Ekle</span><span class="sxs-lookup"><span data-stu-id="0d46b-127">Add solutions to the workspace</span></span>
4. <span data-ttu-id="0d46b-128">İçeri aktarma Kaydedilmiş aramaları</span><span class="sxs-lookup"><span data-stu-id="0d46b-128">Import saved searches</span></span>
5. <span data-ttu-id="0d46b-129">Dışarı aktarma Kaydedilmiş aramaları</span><span class="sxs-lookup"><span data-stu-id="0d46b-129">Export saved searches</span></span>
6. <span data-ttu-id="0d46b-130">Bir bilgisayar grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="0d46b-130">Create a computer group</span></span>
7. <span data-ttu-id="0d46b-131">Windows aracısının yüklü olduğu IIS günlüklerinin bilgisayarlardan toplamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="0d46b-131">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
8. <span data-ttu-id="0d46b-132">Mantıksal Disk performans sayaçlarını Linux bilgisayarından toplar (% kullanılan Inode; Boş megabayt; % Kullanılan alan; Disk aktarımı/sn; Disk Okuma/sn; Disk Yazma/sn)</span><span class="sxs-lookup"><span data-stu-id="0d46b-132">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
9. <span data-ttu-id="0d46b-133">Linux bilgisayarlardan Syslog olaylarını Topla</span><span class="sxs-lookup"><span data-stu-id="0d46b-133">Collect syslog events from Linux computers</span></span>
10. <span data-ttu-id="0d46b-134">Uygulama olay günlüğü'ndeki Windows bilgisayarlardan hata ve uyarı olaylarını Topla</span><span class="sxs-lookup"><span data-stu-id="0d46b-134">Collect Error and Warning events from the Application Event Log from Windows computers</span></span>
11. <span data-ttu-id="0d46b-135">Windows bilgisayarlardan bellek kullanılabilir MBayt performans sayacı Topla</span><span class="sxs-lookup"><span data-stu-id="0d46b-135">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
12. <span data-ttu-id="0d46b-136">Özel günlük Topla</span><span class="sxs-lookup"><span data-stu-id="0d46b-136">Collect a custom log</span></span> 

```

$ResourceGroup = "oms-example"
$WorkspaceName = "log-analytics-" + (Get-Random -Maximum 99999) # workspace names need to be unique - Get-Random helps with this for the example code
$Location = "westeurope"

# List of solutions to enable
$Solutions = "Security", "Updates", "SQLAssessment"

# Saved Searches to import
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

# Custom Log to collect
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

# Create the resource group if needed
try {
    Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop
} catch {
    New-AzureRmResourceGroup -Name $ResourceGroup -Location $Location
}

# Create the workspace
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

# Create a computer group based on names (up to 5000)
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

## <a name="configuring-log-analytics-to-index-azure-diagnostics"></a><span data-ttu-id="0d46b-137">Azure tanılama dizin için yapılandırma günlük analizi</span><span class="sxs-lookup"><span data-stu-id="0d46b-137">Configuring Log Analytics to index Azure diagnostics</span></span>
<span data-ttu-id="0d46b-138">Azure kaynaklarını aracısız izleme için kaynakları Azure tanılama etkin ve günlük analizi çalışma alanına yazmak için yapılandırılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0d46b-138">For agentless monitoring of Azure resources, the resources need to have Azure diagnostics enabled and configured to write to a Log Analytics workspace.</span></span> <span data-ttu-id="0d46b-139">Bu yaklaşım, doğrudan günlük analizi veri gönderir ve bir depolama hesabına yazılması için veri gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="0d46b-139">This approach sends data directly to Log Analytics and does not require data to be written to a storage account.</span></span> <span data-ttu-id="0d46b-140">Desteklenen kaynaklar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0d46b-140">Supported resources include:</span></span>

| <span data-ttu-id="0d46b-141">Kaynak Türü</span><span class="sxs-lookup"><span data-stu-id="0d46b-141">Resource Type</span></span> | <span data-ttu-id="0d46b-142">Günlükler</span><span class="sxs-lookup"><span data-stu-id="0d46b-142">Logs</span></span> | <span data-ttu-id="0d46b-143">Ölçümler</span><span class="sxs-lookup"><span data-stu-id="0d46b-143">Metrics</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0d46b-144">Application Gatewayler</span><span class="sxs-lookup"><span data-stu-id="0d46b-144">Application Gateways</span></span>    | <span data-ttu-id="0d46b-145">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-145">Yes</span></span> | <span data-ttu-id="0d46b-146">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-146">Yes</span></span> |
| <span data-ttu-id="0d46b-147">Automation hesapları</span><span class="sxs-lookup"><span data-stu-id="0d46b-147">Automation accounts</span></span>     | <span data-ttu-id="0d46b-148">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-148">Yes</span></span> | |
| <span data-ttu-id="0d46b-149">Toplu hesaplar</span><span class="sxs-lookup"><span data-stu-id="0d46b-149">Batch accounts</span></span>          | <span data-ttu-id="0d46b-150">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-150">Yes</span></span> | <span data-ttu-id="0d46b-151">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-151">Yes</span></span> |
| <span data-ttu-id="0d46b-152">Data Lake analizi</span><span class="sxs-lookup"><span data-stu-id="0d46b-152">Data Lake analytics</span></span>     | <span data-ttu-id="0d46b-153">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-153">Yes</span></span> | | 
| <span data-ttu-id="0d46b-154">Veri Gölü deposu</span><span class="sxs-lookup"><span data-stu-id="0d46b-154">Data Lake store</span></span>         | <span data-ttu-id="0d46b-155">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-155">Yes</span></span> | |
| <span data-ttu-id="0d46b-156">SQL esnek havuzu</span><span class="sxs-lookup"><span data-stu-id="0d46b-156">Elastic SQL Pool</span></span>        |     | <span data-ttu-id="0d46b-157">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-157">Yes</span></span> |
| <span data-ttu-id="0d46b-158">Olay Hub'ad alanı</span><span class="sxs-lookup"><span data-stu-id="0d46b-158">Event Hub namespace</span></span>     |     | <span data-ttu-id="0d46b-159">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-159">Yes</span></span> |
| <span data-ttu-id="0d46b-160">IOT hub'ları</span><span class="sxs-lookup"><span data-stu-id="0d46b-160">IoT Hubs</span></span>                |     | <span data-ttu-id="0d46b-161">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-161">Yes</span></span> |
| <span data-ttu-id="0d46b-162">Anahtar Kasası</span><span class="sxs-lookup"><span data-stu-id="0d46b-162">Key Vault</span></span>               | <span data-ttu-id="0d46b-163">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-163">Yes</span></span> | |
| <span data-ttu-id="0d46b-164">Yük Dengeleyici</span><span class="sxs-lookup"><span data-stu-id="0d46b-164">Load Balancers</span></span>          | <span data-ttu-id="0d46b-165">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-165">Yes</span></span> | |
| <span data-ttu-id="0d46b-166">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="0d46b-166">Logic Apps</span></span>              | <span data-ttu-id="0d46b-167">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-167">Yes</span></span> | <span data-ttu-id="0d46b-168">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-168">Yes</span></span> |
| <span data-ttu-id="0d46b-169">Ağ Güvenlik Grupları</span><span class="sxs-lookup"><span data-stu-id="0d46b-169">Network Security Groups</span></span> | <span data-ttu-id="0d46b-170">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-170">Yes</span></span> | |
| <span data-ttu-id="0d46b-171">Redis Önbelleği</span><span class="sxs-lookup"><span data-stu-id="0d46b-171">Redis Cache</span></span>             |     | <span data-ttu-id="0d46b-172">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-172">Yes</span></span> |
| <span data-ttu-id="0d46b-173">Hizmet ara</span><span class="sxs-lookup"><span data-stu-id="0d46b-173">Search services</span></span>         | <span data-ttu-id="0d46b-174">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-174">Yes</span></span> | <span data-ttu-id="0d46b-175">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-175">Yes</span></span> |
| <span data-ttu-id="0d46b-176">Hizmet veri yolu ad alanı</span><span class="sxs-lookup"><span data-stu-id="0d46b-176">Service Bus namespace</span></span>   |     | <span data-ttu-id="0d46b-177">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-177">Yes</span></span> |
| <span data-ttu-id="0d46b-178">SQL (v12)</span><span class="sxs-lookup"><span data-stu-id="0d46b-178">SQL (v12)</span></span>               |     | <span data-ttu-id="0d46b-179">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-179">Yes</span></span> |
| <span data-ttu-id="0d46b-180">Web Siteleri</span><span class="sxs-lookup"><span data-stu-id="0d46b-180">Web Sites</span></span>               |     | <span data-ttu-id="0d46b-181">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-181">Yes</span></span> |
| <span data-ttu-id="0d46b-182">Web sunucu grupları</span><span class="sxs-lookup"><span data-stu-id="0d46b-182">Web Server farms</span></span>        |     | <span data-ttu-id="0d46b-183">Evet</span><span class="sxs-lookup"><span data-stu-id="0d46b-183">Yes</span></span> |

<span data-ttu-id="0d46b-184">Kullanılabilir ölçümler ayrıntılarını başvurmak [ölçümleri Azure İzleyicisi ile desteklenen](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="0d46b-184">For the details of the available metrics, refer to [supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="0d46b-185">Kullanılabilir günlüklerini ayrıntılarını başvurmak [desteklenen Hizmetleri ve şema için tanılama günlüklerini](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span><span class="sxs-lookup"><span data-stu-id="0d46b-185">For the details of the available logs, refer to [supported services and schema for diagnostic logs](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span></span>

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

<span data-ttu-id="0d46b-186">Farklı Aboneliklerde bulunan kaynaklar günlükleri toplamak için önceki cmdlet'ini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d46b-186">You can also use the preceding cmdlet to collect logs from resources that are in different subscriptions.</span></span> <span data-ttu-id="0d46b-187">Cmdlet günlükleri ve günlükleri gönderilen çalışma alanı oluşturma her iki kaynağın kimliği sağlama abonelikler arasında çalışmaya yapabiliyor.</span><span class="sxs-lookup"><span data-stu-id="0d46b-187">The cmdlet is able to work across subscriptions since you are providing the id of both the resource creating logs and the workspace the logs are sent to.</span></span>


## <a name="configuring-log-analytics-to-index-azure-diagnostics-from-storage"></a><span data-ttu-id="0d46b-188">Günlük analizi depolama biriminden Azure tanılama dizin için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0d46b-188">Configuring Log Analytics to index Azure diagnostics from storage</span></span>
<span data-ttu-id="0d46b-189">Klasik bulut hizmeti ya da bir service fabric kümesi çalışan bir örneğini günlük verilerini toplamak için önce verileri Azure depolama alanına yazmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="0d46b-189">To collect log data from within a running instance of a classic cloud service or a service fabric cluster, you need to first write the data to Azure storage.</span></span> <span data-ttu-id="0d46b-190">Günlük analizi depolama hesabından günlükleri toplamak için sonra yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="0d46b-190">Log Analytics is then configured to collect the logs from the storage account.</span></span> <span data-ttu-id="0d46b-191">Desteklenen kaynaklar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0d46b-191">Supported resources include:</span></span>

* <span data-ttu-id="0d46b-192">Klasik bulut Hizmetleri (web ve çalışan rolleri)</span><span class="sxs-lookup"><span data-stu-id="0d46b-192">Classic cloud services (web and worker roles)</span></span>
* <span data-ttu-id="0d46b-193">Service fabric kümeleri</span><span class="sxs-lookup"><span data-stu-id="0d46b-193">Service fabric clusters</span></span>

<span data-ttu-id="0d46b-194">Aşağıdaki örnekte gösterildiği nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="0d46b-194">The following example shows how to:</span></span>

1. <span data-ttu-id="0d46b-195">Günlük analizi veri dizinini oluşturacak konumları ve var olan depolama hesaplarını Listele</span><span class="sxs-lookup"><span data-stu-id="0d46b-195">List the existing storage accounts and locations that Log Analytics will index data from</span></span>
2. <span data-ttu-id="0d46b-196">Bir depolama hesabından okumak için bir yapılandırma oluşturmak</span><span class="sxs-lookup"><span data-stu-id="0d46b-196">Create a configuration to read from a storage account</span></span>
3. <span data-ttu-id="0d46b-197">Yeni oluşturulan yapılandırma veri dizini oluşturmak için ek konumlardan güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="0d46b-197">Update the newly created configuration to index data from additional locations</span></span>
4. <span data-ttu-id="0d46b-198">Yeni oluşturulan yapılandırmasını silme</span><span class="sxs-lookup"><span data-stu-id="0d46b-198">Delete the newly created configuration</span></span>

```
# validTables = "WADWindowsEventLogsTable", "LinuxsyslogVer2v0", "WADServiceFabric*EventTable", "WADETWEventTable" 
$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq "your workspace name"})

# Update these two lines with the storage account resource ID and the storage account key for the storage account you want to Log Analytics to  
$storageId = "/subscriptions/ec11ca60-1234-491e-5678-0ea07feae25c/resourceGroups/demo/providers/Microsoft.Storage/storageAccounts/wadv2storage"
$key = "abcd=="

# List existing insights
Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

# Create a new insight
New-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -StorageAccountResourceId $storageId -StorageAccountKey $key -Tables @("WADWindowsEventLogsTable") -Containers @("wad-iis-logfiles")

# Update existing insight
Set-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -Tables @("WADWindowsEventLogsTable", "WADETWEventTable") -Containers @("wad-iis-logfiles")

# Remove the insight
Remove-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" 

```

<span data-ttu-id="0d46b-199">Yukarıdaki komut dosyası, farklı Aboneliklerdeki depolama hesaplarına günlükleri toplamak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d46b-199">You can also use the preceding script to collect logs from storage accounts in different subscriptions.</span></span> <span data-ttu-id="0d46b-200">Komut dosyası, depolama hesabı kaynak kimliği ile ilgili erişim tuşu sağlayarak abonelikler arasında çalışmaya yapabiliyor.</span><span class="sxs-lookup"><span data-stu-id="0d46b-200">The script is able to work across subscriptions since you are providing the storage account resource id and a corresponding access key.</span></span> <span data-ttu-id="0d46b-201">Erişim anahtarı değiştirdiğinizde, yeni anahtar depolama Insight güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0d46b-201">When you change the access key, you need to update the storage insight to have the new key.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0d46b-202">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0d46b-202">Next steps</span></span>
* <span data-ttu-id="0d46b-203">[Günlük analizi PowerShell cmdlet'leri gözden](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) günlük analizi yapılandırması için PowerShell kullanma hakkında ek bilgi için.</span><span class="sxs-lookup"><span data-stu-id="0d46b-203">[Review Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for additional information on using PowerShell for configuration of Log Analytics.</span></span>

