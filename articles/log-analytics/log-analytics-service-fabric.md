---
title: "PowerShell kullanarak Azure günlük analizi ile Service Fabric uygulamaları aaaAssess | Microsoft Docs"
description: "Günlük PowerShell tooassess hello risk ve sistem durumunu Service Fabric uygulamaları, mikro hizmetler, düğümleri ve kümelerini kullanarak analizleri hello Service Fabric çözüm kullanabilirsiniz."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 2047b3fa-96b1-4230-af5d-a4c331d973ce
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: nini
ms.openlocfilehash: 3f6d6c0df02d6d453b77e50b75b64bf7eb73bbbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assess-azure-service-fabric-applications-and-micro-services-with-powershell"></a><span data-ttu-id="2e1ef-103">Azure Service Fabric uygulamaları ve mikro hizmetler PowerShell ile değerlendirin</span><span class="sxs-lookup"><span data-stu-id="2e1ef-103">Assess Azure Service Fabric applications and micro-services with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2e1ef-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2e1ef-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="2e1ef-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e1ef-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>


![Service Fabric simgesi](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="2e1ef-107">Bu makalede nasıl toouse hello günlük analizi toohelp Service Fabric çözümde tanımlamak ve Service Fabric küme genelinde sorunlarını giderme açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-107">This article describes how toouse hello Service Fabric solution in Log Analytics toohelp identify and troubleshoot issues across your Service Fabric cluster.</span></span> <span data-ttu-id="2e1ef-108">Service Fabric düğümlerinizi nasıl performans gösterdiğini ve mikro hizmetler ve uygulamaları nasıl çalıştığını görmek yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-108">It helps you see how your Service Fabric nodes are performing and how your applications and micro-services are running.</span></span>

<span data-ttu-id="2e1ef-109">Merhaba Service Fabric çözümü bu verileri Azure WAD tablolardan toplayarak Service Fabric Vm'lerinizi Azure Tanılama verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-109">hello Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="2e1ef-110">Günlük analizi, daha sonra Service Fabric framework olayları aşağıdaki hello okur:</span><span class="sxs-lookup"><span data-stu-id="2e1ef-110">Log Analytics then reads hello following Service Fabric framework events:</span></span>

- <span data-ttu-id="2e1ef-111">**Güvenilir hizmeti olayları**</span><span class="sxs-lookup"><span data-stu-id="2e1ef-111">**Reliable Service Events**</span></span>
- <span data-ttu-id="2e1ef-112">**Aktör olayları**</span><span class="sxs-lookup"><span data-stu-id="2e1ef-112">**Actor Events**</span></span>
- <span data-ttu-id="2e1ef-113">**İşletimsel olayları**</span><span class="sxs-lookup"><span data-stu-id="2e1ef-113">**Operational Events**</span></span>
- <span data-ttu-id="2e1ef-114">**Özel ETW olayları**</span><span class="sxs-lookup"><span data-stu-id="2e1ef-114">**Custom ETW events**</span></span>

<span data-ttu-id="2e1ef-115">Merhaba Service Fabric çözüm Panosu, Service Fabric ortamınızda, önemli sorunları ve ilgili olayları gösterir.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-115">hello Service Fabric solution dashboard shows you notable issues and relevant events in your Service Fabric environment.</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="2e1ef-116">Yükleme ve yapılandırma hello çözümü</span><span class="sxs-lookup"><span data-stu-id="2e1ef-116">Installing and configuring hello solution</span></span>
<span data-ttu-id="2e1ef-117">Bu üç kolay adımı tooinstall izleyin ve hello çözüm yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="2e1ef-117">Follow these three easy steps tooinstall and configure hello solution:</span></span>

1. <span data-ttu-id="2e1ef-118">Merhaba çalışma alanınız ile depolama hesapları dahil olmak üzere tüm küme kaynakları toocreate kullanılan Azure aboneliği ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-118">Associate hello Azure subscription that you used toocreate all cluster resources, including storage accounts, with your workspace.</span></span> <span data-ttu-id="2e1ef-119">Bkz: [günlük Analytics ile çalışmaya başlama](log-analytics-get-started.md) günlük analizi çalışma alanı oluşturma hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-119">See [Get started with Log Analytics](log-analytics-get-started.md) for information about creating a Log Analytics workspace.</span></span>
2. <span data-ttu-id="2e1ef-120">Günlük analizi toocollect yapılandırabilir ve Service Fabric günlükleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-120">Configure Log Analytics toocollect and view Service Fabric logs.</span></span>
3. <span data-ttu-id="2e1ef-121">Merhaba Service Fabric çalışma alanınızı çözümde etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-121">Enable hello Service Fabric solution in your workspace.</span></span>

## <a name="configure-log-analytics-toocollect-and-view-service-fabric-logs"></a><span data-ttu-id="2e1ef-122">Günlük analizi toocollect yapılandırmak ve Service Fabric günlükleri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="2e1ef-122">Configure Log Analytics toocollect and view Service Fabric logs</span></span>
<span data-ttu-id="2e1ef-123">Bu bölümde, nasıl tooconfigure günlük analizi tooretrieve Service Fabric günlüklerini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-123">In this section, you learn how tooconfigure Log Analytics tooretrieve Service Fabric logs.</span></span> <span data-ttu-id="2e1ef-124">Merhaba günlükleri tooview izin, çözümlemek ve kümenizin veya hello OMS portalı kullanarak bu kümede çalışan hello uygulamaları ve Hizmetleri sorunlarını giderme.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-124">hello logs allow you tooview, analyze, and troubleshoot issues in your cluster or in hello applications and services running in that cluster, using hello OMS portal.</span></span>

> [!NOTE]
> <span data-ttu-id="2e1ef-125">Hello Azure tanılama uzantı tooupload hello günlükleri depolama tablolar için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-125">Configure hello Azure Diagnostics extension tooupload hello logs for storage tables.</span></span> <span data-ttu-id="2e1ef-126">Günlük analizi göründüğünü Hello tablolar eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-126">hello tables must match what Log Analytics looks for.</span></span> <span data-ttu-id="2e1ef-127">Daha fazla bilgi için bkz: [nasıl toocollect ile Azure tanılama günlüklerini](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span><span class="sxs-lookup"><span data-stu-id="2e1ef-127">For more information, see [How toocollect logs with Azure Diagnostics](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span></span> <span data-ttu-id="2e1ef-128">Merhaba yapılandırma ayarları örnekleri bu makaledeki tablolar olmalıdır hello depolama hangi hello adlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-128">hello configuration settings examples in this article show you what hello names of hello storage tables should be.</span></span> <span data-ttu-id="2e1ef-129">Tanılama hello kümede ayarlama ve günlükleri tooa depolama hesabı karşıya sonra hello sonraki tooconfigure günlük analizi toocollect adımdır Bu günlükler.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-129">Once Diagnostics is set up on hello cluster and is uploading logs tooa storage account, hello next step is tooconfigure Log Analytics toocollect these logs.</span></span>
>
>

<span data-ttu-id="2e1ef-130">Merhaba güncelleştirdiğinizden emin olun **EtwEventSourceProviderConfiguration** hello bölümünde **template.json** dosya hello yapılandırma uygulamadan önce yeni EventSources update tarafından hello tooadd girişleri çalışan **deploy.ps1**.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-130">Ensure that you update hello **EtwEventSourceProviderConfiguration** section in hello **template.json** file tooadd entries for hello new EventSources before you apply hello configuration update by running **deploy.ps1**.</span></span> <span data-ttu-id="2e1ef-131">Merhaba tablo karşıya yükleme için hello aynı (ETWEventTable).</span><span class="sxs-lookup"><span data-stu-id="2e1ef-131">hello table for upload is hello same as (ETWEventTable).</span></span> <span data-ttu-id="2e1ef-132">Merhaba şu anda günlük analizi yalnızca uygulama ETW olayları hello okuyabilir *WADETWEventTable* tablo.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-132">At hello moment, Log Analytics can only read application ETW events from hello *WADETWEventTable* table.</span></span>

<span data-ttu-id="2e1ef-133">Merhaba aşağıdaki araçlar olan kullanılan tooperform bu bölümdeki hello işlemleri bazıları:</span><span class="sxs-lookup"><span data-stu-id="2e1ef-133">hello following tools are used tooperform some of hello operations in this section:</span></span>

* <span data-ttu-id="2e1ef-134">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e1ef-134">Azure PowerShell</span></span>
* [<span data-ttu-id="2e1ef-135">Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="2e1ef-135">Operations Management Suite</span></span>](http://www.microsoft.com/oms)

### <a name="configure-a-log-analytics-workspace-tooshow-hello-cluster-logs"></a><span data-ttu-id="2e1ef-136">Günlük analizi çalışma alanı tooshow hello küme günlüklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2e1ef-136">Configure a Log Analytics workspace tooshow hello cluster logs</span></span>

<span data-ttu-id="2e1ef-137">Günlük analizi çalışma alanı oluşturduktan sonra hello çalışma toopull günlükleri'hello Azure depolama tablolardan yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-137">After you create a Log Analytics workspace, configure hello workspace toopull logs from hello Azure storage tables.</span></span> <span data-ttu-id="2e1ef-138">Ardından, PowerShell Betiği aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2e1ef-138">Then, run hello following PowerShell script:</span></span>

```
<#
    This script will configure an Operations Management Suite workspace (previously called an Operational Insights workspace) tooread Diagnostics from an Azure Storage account.
    It will enable all supported data types (currently Service Fabric Events, ETW Events and IIS Logs).
    It supports Resource Manager storage accounts.
    If you have more than one Azure Subscription, you will be prompted for hello subscription tooconfigure.
    If you have more than one Log Analytics workspace you will be prompted for hello workspace tooconfigure.
    It will then look through your Service Fabric clusters, and configure your Log Analytics workspace tooread Diagnostics from storage accounts that are connected toothat cluster and have diagnostics enabled.
#>

try
{
    Get-AzureRMContext
}
catch [System.Management.Automation.PSInvalidOperationException]
{
    Add-AzureRmAccount
}

$validTables = "WADServiceFabric*EventTable", "WADETWEventTable"
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter hello number corresponding toohello Azure subscription you would like toowork with.`n"

            $count = 1
            foreach ($subscription in $allSubscriptions) {
                $uiPrompt += "$count. " + $subscription.Name + " (" + $subscription.Id + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $subscription = $allSubscriptions[$answer]
             Write-Host $subscription.Id
        }  
    }
    return $subscription
}

function Select-Workspace {
    $workspace = ""
    $allWorkspaces = Get-AzureRmOperationalInsightsWorkspace  

    switch ($allWorkspaces.Count) {
        0 {Write-Error "No Operations Management Suite workspaces found. `n"}
        1 {return $allWorkspaces}
        default {
            $uiPrompt = "Enter hello number corresponding toohello workspace you want tooconfigure.`n"
            $count = 1
            foreach ($workspace in $allWorkspaces) {
                $uiPrompt += "$count. " + $workspace.Name + " (" + $workspace.CustomerId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $workspace = $allWorkspaces[$answer]
             Write-Host $workspace.WorkspaceName
        }  
    }
    return $workspace
}

function Check-ETWProviderLogging {
     param(
     [string]$id,
     [string]$provider,
     [string]$expectedTable,
     [string]$table
    )       
         Write-Debug ("ID: $id Provider: $provider ExpectedTable $expectedTable ActualTable $table")
         if ( ($table -eq $null) -or ($table -eq ""))  
         {
             Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics toowrite too$expectedTable.")
         }  
         elseif ( $table -ne $expectedTable )
         {
             Write-Warning ("$id $provider events are being written too$table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
         }  
         else
         {
             Write-Verbose "$id $provider events are being written tooWAD$expectedTable (Correct configuration.)"
         }
 }

function Check-ServiceFabricScaleSetDiagnostics {
     param(
          [psobject]$scaleSetDiagnostics
   )
     $storageAccountsFound = @()
     Write-Verbose ("Checking " + $scaleSetDiagnostics)
     $sfReliableActorTable = $null
     $sfReliableServiceTable = $null
     $sfOperationalTable = $null

     Write-Debug $scaleSetDiagnostics
     $serviceFabricProviderList = ""
     $etwManifestProviderList = ""

     if ( $scaleSetDiagnostics.xmlCfg )  
      {
             Write-Debug ("Found XMLcfg")
             $xmlCfg = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($scaleSetDiagnostics.xmlCfg))
             Write-Debug $xmlCfg
             $etwProviders = Select-Xml -Content $xmlCfg -XPath "//EtwProviders"                 
             $serviceFabricProviderList = $etwProviders.Node.EtwEventSourceProviderConfiguration
             $etwManifestProviderList = $etwProviders.Node.EtwManifestProviderConfiguration
      } elseif ($scaleSetDiagnostics.WadCfg )  
     {
         Write-Debug ("Found WADcfg")
         Write-Debug $scaleSetDiagnostics.WadCfg
         $serviceFabricProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwEventSourceProviderConfiguration
         $etwManifestProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwManifestProviderConfiguration
     } else
     {
         Write-Error "Unable tooparse Azure Diagnostics setting for $id"
             Write-Warning ("$id does not have diagnostics enabled")
     }
     foreach ($provider in $serviceFabricProviderList)  
     {
         Write-Debug ("Event Source Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
         if ($provider.Provider -eq "Microsoft-ServiceFabric-Actors")
         {
             $sfReliableActorTable = $provider.DefaultEvents.eventDestination  
         } elseif ($provider.Provider -eq "Microsoft-ServiceFabric-Services")  
         {  
             $sfReliableServiceTable = $provider.DefaultEvents.eventDestination  
         } else  
         {
             Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
         }
     }
     foreach ($provider in $etwManifestProviderList)
     {
         Write-Debug ("Manifest Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
         if ($provider.Provider -eq "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8")
         {
             $sfOperationalTable = $provider.DefaultEvents.eventDestination  
         } else  
         {
             Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
         }
     }

     Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Actors" "ServiceFabricReliableActorEventTable" $sfReliableActorTable
     Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Services" "ServiceFabricReliableServiceEventTable" $sfReliableServiceTable
     Check-ETWProviderLogging $id "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8 (System events)" "ServiceFabricSystemEventTable" $sfOperationalTable

     Write-Verbose ("StorageAccount: " + $scaleSetDiagnostics.StorageAccount)
     $storageAccountsFound += ($scaleSetDiagnostics.StorageAccount)
     return ($storageAccountsFound)
 }

function Select-StorageAccount {
    $allResources = Get-AzureRmResource #pulls in all resources
    $serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"}) #pulls in all service fabric clusters in hello resource
    $storageAccountList = @()
    foreach($cluster in $serviceFabricClusters) {
        Write-Host("Checking cluster: " + $cluster.Name)
         $scaleSet = $allResources.Where({($_.ResourceType -eq "Microsoft.Compute/virtualMachineScaleSets") -and ($_.ResourceGroupName -eq $cluster.ResourceGroupName)})

         foreach($set in $scaleSet) {
             $resource = Get-AzureRmResource -ResourceId $set.ResourceId
             $extensions = $resource.Properties.VirtualMachineProfile.ExtensionProfile.Extensions

             foreach($ext in $extensions) {
                 if ($ext.Properties.Publisher -eq "Microsoft.Azure.Diagnostics" -and $ext.Properties.Type -eq "IaaSDiagnostics") {
                     $storageAccountList += (Check-ServiceFabricScaleSetDiagnostics $ext.Properties.Settings)
                 }
             }
          }

         $storageAccountsToCheck = $allResources.Where({($_.ResourceType -eq "Microsoft.Storage/storageAccounts") -and ($_.ResourceName -in $storageAccountList)})

         if ($storageAccountsToCheck.Count -eq "0") {
                Write-Error "No storage accounts found"
           }
           else {
                    foreach ($storageAccount in $storageAccountsToCheck) {
                        Write-Host("Checking Storage Account: " + $storageAccount.Name)
                        $insightsName = $storageAccount.Name + $workspace.Name
                        $existingConfig = ""
                        try
                            {
                                $existingConfig = Get-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -ErrorAction Stop
                            }
                        catch
                            {
                                # HTTP Not Found is returned if hello storage insight doesn't exist
                            }
                        if ($existingConfig) {                         
                                  [array]$Tables = $existingConfig.Tables
                                   foreach($table in $validTables) {
                                         if($Tables -notcontains $table) {
                                               $Tables += $table
                                               $dirty = $true;
                                               Write-Host "Adding Table: $table";
                                         }
                                         else {
                                               Write-Host "$table is already configured.`n";
                                             }
                                      }
                                      # If any of hello tables from hello table list are not already monitored, then we add them
                                   if($dirty -eq $true) {
                                           Set-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -Tables $Tables
                                           Write-Host "Updating Storage Insight. `n"
                                    }
                                    else {
                                           Write-Host "Storage Insight already updated."
                                  }
                          }
                     else {
                            $key = (Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccount.ResourceGroupName -Name $storageAccount.Name)[0].Value
                           New-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -StorageAccountResourceId $storageAccount.ResourceId -StorageAccountKey $key -Tables $validTables
                            Write-Host "New Azure Storage Insight Configured. `n"
                           }
                    }
             }
      }
      return
     }

$subscription = Select-Subscription
$subscriptionId = $subscription.SubscriptionId
$subscription = Select-AzureRmSubscription -SubscriptionId $subscriptionId
$workspace = Select-Workspace
$storageAccount = Select-StorageAccount
```

<span data-ttu-id="2e1ef-139">Merhaba günlük analizi çalışma alanı tooread hello Azure'den yapılandırdıktan sonra depolama hesabınızın tablolarda toohello Azure portalında oturum.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-139">After you've configured hello Log Analytics workspace tooread from hello Azure tables in your storage account, log in toohello Azure portal.</span></span> <span data-ttu-id="2e1ef-140">Merhaba günlük analizi çalışma alanından seçin **tüm kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-140">Select hello Log Analytics workspace from **All Resources**.</span></span> <span data-ttu-id="2e1ef-141">Depolama hesabı bağlı günlükleri toohello çalışma Hello sayısı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-141">hello number of storage account logs connected toohello workspace is displayed.</span></span> <span data-ttu-id="2e1ef-142">Select hello **depolama hesabı günlüklerine** döşeme.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-142">Select hello **Storage account logs** tile.</span></span> <span data-ttu-id="2e1ef-143">Depolama hesabı günlükleri tooverify depolama hesabınıza bağlı toohello doğru çalışma olduğunu Hello listesini gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-143">Review hello list of storage account logs tooverify that your storage account is connected toohello correct workspace.</span></span>

![Depolama hesabı günlükleri](./media/log-analytics-service-fabric/sf1.png)

## <a name="enable-hello-service-fabric-solution"></a><span data-ttu-id="2e1ef-145">Merhaba Service Fabric çözüm etkinleştir</span><span class="sxs-lookup"><span data-stu-id="2e1ef-145">Enable hello Service Fabric solution</span></span>
<span data-ttu-id="2e1ef-146">Komut dosyası tooadd hello çözüm tooyour günlük analizi çalışma alanı aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-146">Use hello following script tooadd hello solution tooyour Log Analytics workspace.</span></span> <span data-ttu-id="2e1ef-147">Merhaba tooenable hello Service Fabric çözüm istediğiniz hello günlük analizi çalışma alanı ile ilişkili Azure abonelik kullanarak PowerShell'de Hello komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-147">Run hello script in PowerShell, using hello Azure subscription that is associated with hello Log Analytics workspace that you want tooenable hello Service Fabric solution in.</span></span>

```
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter hello number corresponding toohello Azure subscription you would like toowork with.`n"
            $count = 1
            foreach ($subscription in $allSubscriptions) {
                $uiPrompt += "$count. " + $subscription.SubscriptionName + " (" + $subscription.SubscriptionId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $subscription = $allSubscriptions[$answer]
             Write-Host $subscription.SubscriptionId
        }  
    }
    return $subscription
}

function Select-Workspace {
    $workspace = ""
    $allWorkspaces = Get-AzureRmOperationalInsightsWorkspace  
    switch ($allWorkspaces.Count) {
        0 {Write-Error "No Operations Management Suite workspaces found"}
        1 {return $allWorkspaces}
        default {
            $uiPrompt = "Enter hello number corresponding toohello workspace you want tooconfigure.`n"
            $count = 1
            foreach ($workspace in $allWorkspaces) {
                $uiPrompt += "$count. " + $workspace.Name + " (" + $workspace.CustomerId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $workspace = $allWorkspaces[$answer]
                           Write-Host $workspace.WorkspaceName
        }  
    }
    return $workspace
}
$subscription = Select-Subscription
$subscriptionId = $subscription.Id
$subscription = Select-AzureRmSubscription -SubscriptionId $subscriptionId
$workspace = Select-Workspace
Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -IntelligencePackName "ServiceFabric" -Enabled $true
```

<span data-ttu-id="2e1ef-148">Merhaba çözüm etkinleştirdikten sonra hello Service Fabric döşeme tooyour günlük analizi eklenir *genel bakış* sayfası.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-148">After you enable hello solution, hello Service Fabric tile is added tooyour Log Analytics *Overview* page.</span></span> <span data-ttu-id="2e1ef-149">Başlangıç sayfası runAsync hataları ve son 24 saat hello oluştu iptalleri gibi önemli sorunları görünümünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-149">hello page shows a view of notable issues such as runAsync failures and cancellations that occurred in hello last 24 hours.</span></span>

![Service Fabric döşeme](./media/log-analytics-service-fabric/sf2.png)

### <a name="view-service-fabric-events"></a><span data-ttu-id="2e1ef-151">Service Fabric olaylarını görüntüle</span><span class="sxs-lookup"><span data-stu-id="2e1ef-151">View Service Fabric events</span></span>
<span data-ttu-id="2e1ef-152">Merhaba tıklatın **Service Fabric** döşeme tooopen hello Service Fabric Pano.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-152">Click hello **Service Fabric** tile tooopen hello Service Fabric dashboard.</span></span> <span data-ttu-id="2e1ef-153">Merhaba Pano izleyen hello tabloda hello sütunları içerir.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-153">hello dashboard includes hello columns in hello table that follows.</span></span> <span data-ttu-id="2e1ef-154">Her sütun, belirtilen zaman aralığı hello sütunun ölçütlerine sayısı eşleştirerek hello üst 10 olaylarını listeler.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-154">Each column lists hello top 10 events by count matching that column's criteria for hello specified time range.</span></span> <span data-ttu-id="2e1ef-155">Merhaba tüm liste tıklayarak sağlar günlük arama çalıştırabilirsiniz **tümünü görmek** hello sağ alt her sütunun veya hello sütun başlığını tıklatarak.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-155">You can run a log search that provides hello entire list by clicking **See all** at hello right bottom of each column, or by clicking hello column header.</span></span>

| <span data-ttu-id="2e1ef-156">**Service Fabric olay**</span><span class="sxs-lookup"><span data-stu-id="2e1ef-156">**Service Fabric event**</span></span> | <span data-ttu-id="2e1ef-157">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="2e1ef-157">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="2e1ef-158">Önemli sorunlar</span><span class="sxs-lookup"><span data-stu-id="2e1ef-158">Notable Issues</span></span> | <span data-ttu-id="2e1ef-159">RunAsyncFailures, RunAsynCancellations ve düğüm listeleri gibi sorunları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-159">Displays issues including RunAsyncFailures, RunAsynCancellations, and Node Downs.</span></span> |
| <span data-ttu-id="2e1ef-160">İşletimsel olayları</span><span class="sxs-lookup"><span data-stu-id="2e1ef-160">Operational Events</span></span> | <span data-ttu-id="2e1ef-161">Uygulama yükseltme ve dağıtımlarını içeren önemli çalışma olaylarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-161">Displays notable operational events including application upgrade and deployments.</span></span> |
| <span data-ttu-id="2e1ef-162">Güvenilir hizmeti olayları</span><span class="sxs-lookup"><span data-stu-id="2e1ef-162">Reliable Service Events</span></span> | <span data-ttu-id="2e1ef-163">Runasyncinvocations dahil olmak üzere önemli güvenilir hizmet olayları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-163">Displays notable reliable service events including  Runasyncinvocations.</span></span> |
| <span data-ttu-id="2e1ef-164">Aktör olayları</span><span class="sxs-lookup"><span data-stu-id="2e1ef-164">Actor Events</span></span> | <span data-ttu-id="2e1ef-165">Mikro-Hizmetleri tarafından oluşturulan önemli aktör olayları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-165">Displays notable actor events generated by your micro-services.</span></span> <span data-ttu-id="2e1ef-166">Olayları bir aktör yöntemi, aktör etkinleştirmeleri ve deactivations ve benzeri tarafından oluşturulan özel durumları içerir.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-166">Events include exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="2e1ef-167">Uygulama olayları</span><span class="sxs-lookup"><span data-stu-id="2e1ef-167">Application Events</span></span> | <span data-ttu-id="2e1ef-168">Uygulamalarınız tarafından oluşturulan tüm özel ETW olayları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-168">Displays all custom ETW events generated by your applications.</span></span> |

![Service Fabric Panosu](./media/log-analytics-service-fabric/sf3.png)

![Service Fabric Panosu](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="2e1ef-171">Merhaba aşağıdaki tabloda veri toplama yöntemleri ve verileri için Service Fabric nasıl toplanır ilgili diğer ayrıntılar gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="2e1ef-171">hello following table shows data collection methods and other details about how data is collected for Service Fabric:</span></span>

| <span data-ttu-id="2e1ef-172">Platform</span><span class="sxs-lookup"><span data-stu-id="2e1ef-172">platform</span></span> | <span data-ttu-id="2e1ef-173">Doğrudan Aracısı</span><span class="sxs-lookup"><span data-stu-id="2e1ef-173">Direct Agent</span></span> | <span data-ttu-id="2e1ef-174">Operations Manager Aracısı</span><span class="sxs-lookup"><span data-stu-id="2e1ef-174">Operations Manager agent</span></span> | <span data-ttu-id="2e1ef-175">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="2e1ef-175">Azure Storage</span></span> | <span data-ttu-id="2e1ef-176">Operations Manager gerekli?</span><span class="sxs-lookup"><span data-stu-id="2e1ef-176">Operations Manager required?</span></span> | <span data-ttu-id="2e1ef-177">Operations Manager Aracısı verilerinin yönetim grubu gönderilen</span><span class="sxs-lookup"><span data-stu-id="2e1ef-177">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="2e1ef-178">Toplama sıklığı</span><span class="sxs-lookup"><span data-stu-id="2e1ef-178">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="2e1ef-179">Windows</span><span class="sxs-lookup"><span data-stu-id="2e1ef-179">Windows</span></span> |  |  | <span data-ttu-id="2e1ef-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="2e1ef-180">&#8226;</span></span> |  |  |<span data-ttu-id="2e1ef-181">10 dakika</span><span class="sxs-lookup"><span data-stu-id="2e1ef-181">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="2e1ef-182">Olaylarla hello kapsamını değiştirmek **verilerini alarak son yedi gün** hello Pano hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-182">Change hello scope of events with **Data based on last seven days** at hello top of hello dashboard.</span></span> <span data-ttu-id="2e1ef-183">Bir gün veya altı saat olmak üzere son yedi gün içinde hello oluşturulan olayları gösterir.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-183">You can also show events generated within hello last seven days, one day, or six hours.</span></span> <span data-ttu-id="2e1ef-184">Ya da seçebilirsiniz **özel** toospecify özel bir tarih aralığı.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-184">Or, you can select **Custom** toospecify a custom date range.</span></span>
>
>

## <a name="troubleshoot-your-service-fabric-and-log-analytics-configuration"></a><span data-ttu-id="2e1ef-185">Service Fabric ve günlük analizi yapılandırma sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="2e1ef-185">Troubleshoot your Service Fabric and Log Analytics configuration</span></span>
<span data-ttu-id="2e1ef-186">Günlük analizi oluşturulamıyor tooview olayı verilerini olduğundan, günlük analizi yapılandırması tooverify gerekiyorsa, komut dosyası izleyen hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-186">If you need tooverify your Log Analytics configuration because you are unable tooview event data in Log Analytics, use hello following script.</span></span> <span data-ttu-id="2e1ef-187">Hello aşağıdaki eylemleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="2e1ef-187">It performs hello following actions:</span></span>

1. <span data-ttu-id="2e1ef-188">Service Fabric tanılama yapılandırmanızı okur</span><span class="sxs-lookup"><span data-stu-id="2e1ef-188">Reads your Service Fabric diagnostics configuration</span></span>
2. <span data-ttu-id="2e1ef-189">Merhaba tablolara yazılan veriler denetler</span><span class="sxs-lookup"><span data-stu-id="2e1ef-189">Checks for data written into hello tables</span></span>
3. <span data-ttu-id="2e1ef-190">Günlük analizi hello tablolardan yapılandırılmış tooread olduğunu doğrular</span><span class="sxs-lookup"><span data-stu-id="2e1ef-190">Verifies that Log Analytics is configured tooread from hello tables</span></span>

```
<#
    Verify Service Fabric and Log Analytics configuration
    1. Read Service Fabric diagnostics configuration
    2. Check for data being written into hello tables
    3. Verify Log Analytics is configured tooread from hello tables

    Supported tables:
    WADServiceFabricReliableActorEventTable
    WADServiceFabricReliableServiceEventTable
    WADServiceFabricSystemEventTable
    WADETWEventTable

    Script will write a warning for every misconfiguration detected
    toosee items that are correctly configured set $VerbosePreference="Continue"
#>
Param
(
    [Parameter(Mandatory=$true,
    ValueFromPipeline=$true,
    Position=1)]
    [string]$workspaceName
)

$WADtables = @("WADServiceFabricReliableActorEventTable",
               "WADServiceFabricReliableServiceEventTable",
               "WADServiceFabricSystemEventTable",
               "WADETWEventTable"
               )

<#
    Check if OMS Log Analytics is configured tooindex service fabric events from hello specified table
#>

function Check-OMSLogAnalyticsConfiguration {
    param(
    [psobject]$workspace,
    [psobject]$storageAccount,
    [string]$id
    )

    $existingInsights = Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

    if ($existingInsights)
    {
        $currentStorageAccountInsight = $existingInsights.Where({$_.StorageAccountResourceId -eq $storageAccount.ResourceId})

        if ("WADServiceFabric*EventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured tooindex service fabric actor, service and operational events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured tooindex service fabric actor, service and operational events from " + $storageAccount.Name)
        }
        if ("WADETWEventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured tooindex service fabric application events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured tooindex service fabric application events from " + $storageAccount.Name)
        }
    } else
    {
        Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + "is not configured tooread service fabric events from " + $storageAccount.Name)
    }    
}

<#
    Check Azure table storage tooconfirm there is recent data written by Service Fabric
#>

function Check-TablesForData {
    param(
    [psobject]$storageAccount
    )

    $ctx = (Get-AzureRmStorageAccount -ResourceGroupName $storageAccount.ResourceGroupName -Name $storageAccount.ResourceName).Context

    $createdTables = Get-AzureStorageTable -Context $ctx

    $recently = Get-Date -Format s ((Get-Date).AddMinutes(-20).ToUniversalTime())
    $recently = $recently + "Z"

    foreach ($table in $WADtables)
    {
        if ($table -in $createdTables.Name)
        {
            $tbl = Get-AzureStorageTable -Name $table -Context $ctx
            $query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery
            $list = New-Object System.Collections.Generic.List[string]
            $list.Add("RowKey")
            $list.Add("ProviderName")
            $list.Add("Timestamp")
            $query.FilterString = "Timestamp gt datetime'$recently'"
            $query.SelectColumns = $list
            $query.TakeCount = 20
            $entities = $tbl.CloudTable.ExecuteQuery($query)
            Write-Debug $entities
            if ($entities.Count -gt 0)
            {
                Write-Verbose ("Data was written too$table in " + $storageAccount.ResourceName + "after $recently")
            } else
            {
                Write-Warning ("No data after $recently is in  $table in " + $storageAccount.ResourceName)
            }
        } else
        {
            Write-Warning ("$table does not exist in storage account " + $storageAccount.ResourceName)
        }
    }
}

<#
    Check if ETW provider is configured toolog events toohello expected table storage
#>
function Check-ETWProviderLogging {
    param(
    [string]$id,
    [string]$provider,
    [string]$expectedTable,
    [string]$table
    )      
        Write-Debug ("ID: $id Provider: $provider ExpectedTable $expectedTable ActualTable $table")
        if ( ($table -eq $null) -or ($table -eq ""))
        {
            Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics toowrite too$expectedTable.")
        }
        elseif ( $table -ne $expectedTable )
        {
            Write-Warning ("$id $provider events are being written too$table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
        }
        else
        {
            Write-Verbose "$id $provider events are being written tooWAD$expectedTable (Correct configuration.)"
        }
}

<#
    Check Azure Diagnostics Configuration for a Service Fabric cluster
#>
function Check-ServiceFabricScaleSetDiagnostics {
    param(
    [psobject]$scaleSetDiagnostics
    )

    $storageAccountsFound = @()
    Write-Verbose ("Checking " + $scaleSetDiagnostics)
    $sfReliableActorTable = $null
    $sfReliableServiceTable = $null
    $sfOperationalTable = $null
    Write-Debug $scaleSetDiagnostics
    $serviceFabricProviderList = ""
    $etwManifestProviderList = ""

    if ( $scaleSetDiagnostics.xmlCfg )
    {
        Write-Debug ("Found XMLcfg")
        $xmlCfg = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($scaleSetDiagnostics.xmlCfg))
        Write-Debug $xmlCfg
        $etwProviders = Select-Xml -Content $xmlCfg -XPath "//EtwProviders"                
        $serviceFabricProviderList = $etwProviders.Node.EtwEventSourceProviderConfiguration
        $etwManifestProviderList = $etwProviders.Node.EtwManifestProviderConfiguration
    } elseif ($scaleSetDiagnostics.WadCfg )
    {
        Write-Debug ("Found WADcfg")
        Write-Debug $scaleSetDiagnostics.WadCfg
        $serviceFabricProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwEventSourceProviderConfiguration
        $etwManifestProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwManifestProviderConfiguration
    } else
    {
        Write-Error "Unable tooparse Azure Diagnostics setting for $id"
        Write-Warning ("$id does not have diagnostics enabled")
    }

    foreach ($provider in $serviceFabricProviderList)
    {
        Write-Debug ("Event Source Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
        if ($provider.Provider -eq "Microsoft-ServiceFabric-Actors")
        {
            $sfReliableActorTable = $provider.DefaultEvents.eventDestination
        } elseif ($provider.Provider -eq "Microsoft-ServiceFabric-Services")
        {
            $sfReliableServiceTable = $provider.DefaultEvents.eventDestination
        } else
        {
            Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
        }
    }
    foreach ($provider in $etwManifestProviderList)
    {
        Write-Debug ("Manifest Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
        if ($provider.Provider -eq "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8")
        {
            $sfOperationalTable = $provider.DefaultEvents.eventDestination
        } else
        {
            Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
        }
    }

    Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Actors" "ServiceFabricReliableActorEventTable" $sfReliableActorTable
    Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Services" "ServiceFabricReliableServiceEventTable" $sfReliableServiceTable
    Check-ETWProviderLogging $id "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8 (System events)" "ServiceFabricSystemEventTable" $sfOperationalTable

    Write-Verbose ("StorageAccount: " + $scaleSetDiagnostics.StorageAccount)

    $storageAccountsFound += ($scaleSetDiagnostics.StorageAccount)
    return ($storageAccountsFound)
}

# This script uses Get-AzureRmVMDiagnosticsExtension and needs a version where -Name is not a required parameter
Import-Module AzureRM.Compute -MinimumVersion 1.2.2

try
{
    Get-AzureRmContext
}
catch [System.Management.Automation.PSInvalidOperationException]
{
    Login-AzureRmAccount
}

$allResources = Get-AzureRmResource

$OMSworkspace = $allResources.Where({($_.ResourceType -eq "Microsoft.OperationalInsights/workspaces") -and ($_.ResourceName -eq $workspaceName)})

if ($OMSworkspace.Name -ne $workspaceName)
{
    Write-Error ("Unable toofind Log Analytics Workspace " + $workspaceName)
}

$serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"})
$storageAccountList = @()
foreach($cluster in $serviceFabricClusters) {
    Write-Verbose ("Checking cluster: " + $cluster.Name)
    $scaleSet = ($allResources.Where({($_.ResourceType -eq "Microsoft.Compute/virtualMachineScaleSets") -and ($_.ResourceGroupName -eq $cluster.ResourceGroupName)}))

    foreach($set in $scaleSet) {
        $resource = Get-AzureRmResource -ResourceId $set.ResourceId
        $extensions = $resource.Properties.VirtualMachineProfile.ExtensionProfile.Extensions
        foreach($ext in $extensions) {
            if ($ext.Properties.Publisher -eq "Microsoft.Azure.Diagnostics" -and $ext.Properties.Type -eq "IaaSDiagnostics") {
                $storageAccountList += (Check-ServiceFabricScaleSetDiagnostics $ext.Properties.Settings)
            }
        }
    }
}

$storageAccountList = $storageAccountList | Sort-Object | Get-Unique
$storageAccountsToCheck = ($allResources.Where({($_.ResourceType -eq "Microsoft.Storage/storageAccounts") -and ($_.ResourceName -in $storageAccountList)}))

foreach($storageAccount in $storageAccountsToCheck)
{
    Check-TablesForData $storageAccount
    Check-OMSLogAnalyticsConfiguration $OMSworkspace $storageAccount
}
 ```


## <a name="next-steps"></a><span data-ttu-id="2e1ef-191">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2e1ef-191">Next steps</span></span>
* <span data-ttu-id="2e1ef-192">Kullanım [günlük analizi günlük aramalarda](log-analytics-log-searches.md) tooview ayrıntılı Service Fabric olay verileri.</span><span class="sxs-lookup"><span data-stu-id="2e1ef-192">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Service Fabric event data.</span></span>
