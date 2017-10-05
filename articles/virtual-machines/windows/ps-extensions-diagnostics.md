---
title: "Bir Windows VM üzerinde tanılamayı etkinleştirmek için Azure PowerShell kullanın | Microsoft Docs"
services: virtual-machines-windows
documentationcenter: 
description: "Windows çalıştıran bir sanal makine Azure Tanılama'yı etkinleştirmek için PowerShell kullanma hakkında bilgi edinin"
author: sbtron
manager: timlt
editor: 
ms.assetid: 2e6d88f2-1980-4a24-827e-a81616a0d247
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: saurabh
ms.openlocfilehash: d0be4a712657edfc516c5f32e66519f5d9486728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-enable-azure-diagnostics-in-a-virtual-machine-running-windows"></a><span data-ttu-id="7a14b-103">Windows çalıştıran bir sanal makinede PowerShell kullanarak Azure Tanılama’yı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="7a14b-103">Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="7a14b-104">Azure tanılama dağıtılan bir uygulama tanılama verilerini toplama sağlar. Azure içinde bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="7a14b-104">Azure Diagnostics is the capability within Azure that enables the collection of diagnostic data on a deployed application.</span></span> <span data-ttu-id="7a14b-105">Bir Azure sanal Windows çalıştıran makineden (VM) uygulama günlüklerini veya performans sayaçları gibi tanılama verilerini toplamak için tanılama uzantısını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a14b-105">You can use the diagnostics extension to collect diagnostic data like application logs or performance counters from an Azure virtual machine (VM) that is running Windows.</span></span> <span data-ttu-id="7a14b-106">Bu makalede, bir VM için tanılama uzantısını etkinleştirmek için Windows PowerShell kullanmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="7a14b-106">This article describes how to use Windows PowerShell to enable the diagnostics extension for a VM.</span></span> <span data-ttu-id="7a14b-107">Bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview) Bu makale için gereken önkoşulları için.</span><span class="sxs-lookup"><span data-stu-id="7a14b-107">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span>

## <a name="enable-the-diagnostics-extension-if-you-use-the-resource-manager-deployment-model"></a><span data-ttu-id="7a14b-108">Resource Manager dağıtım modeli kullanırsanız tanılama uzantısını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="7a14b-108">Enable the diagnostics extension if you use the Resource Manager deployment model</span></span>
<span data-ttu-id="7a14b-109">Azure Resource Manager dağıtım modeli üzerinden Windows VM uzantısı yapılandırma Resource Manager şablonu ekleyerek oluştururken tanılama uzantısını etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a14b-109">You can enable the diagnostics extension while you create a Windows VM through the Azure Resource Manager deployment model by adding the extension configuration to the Resource Manager template.</span></span> <span data-ttu-id="7a14b-110">Bkz: [Azure Resource Manager şablonunu kullanarak izleme ve Tanılama ile Windows sanal makine oluşturma](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7a14b-110">See [Create a Windows virtual machine with monitoring and diagnostics by using the Azure Resource Manager template](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="7a14b-111">Resource Manager dağıtım modeli oluşturulmuş mevcut bir VM'yi tanılama uzantısını etkinleştirmek için kullanabileceğiniz [kümesi AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet'ini aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="7a14b-111">To enable the diagnostics extension on an existing VM that was created through the Resource Manager deployment model, you can use the [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet as shown below.</span></span>

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


<span data-ttu-id="7a14b-112">*$diagnosticsconfig_path* açıklandığı gibi XML'de tanılama yapılandırması içeren dosyanın yolu olan [örnek](#sample-diagnostics-configuration) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="7a14b-112">*$diagnosticsconfig_path* is the path to the file that contains the diagnostics configuration in XML, as described in the [sample](#sample-diagnostics-configuration) below.</span></span>  

<span data-ttu-id="7a14b-113">Tanılama yapılandırma dosyası belirtiyorsa bir **StorageAccount** bir depolama hesabı adı bir öğesiyle sonra *kümesi AzureRMVMDiagnosticsExtension* komut dosyası otomatik olarak Tanılama'yı ayarlama Bu depolama hesabına Tanılama verileri gönder uzantısı.</span><span class="sxs-lookup"><span data-stu-id="7a14b-113">If the diagnostics configuration file specifies a **StorageAccount** element with a storage account name, then the *Set-AzureRMVMDiagnosticsExtension* script will automatically set the diagnostics extension to send diagnostic data to that storage account.</span></span> <span data-ttu-id="7a14b-114">Bunun çalışması için depolama hesabı VM ile aynı abonelikte olması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="7a14b-114">For this to work, the storage account needs to be in the same subscription as the VM.</span></span>

<span data-ttu-id="7a14b-115">Öyle değilse **StorageAccount** olarak geçirmenize gerek sonra tanılama yapılandırmasında belirtilen *StorageAccountName* cmdlet parametresi.</span><span class="sxs-lookup"><span data-stu-id="7a14b-115">If no **StorageAccount** was specified in the diagnostics configuration, then you need to pass in the *StorageAccountName* parameter to the cmdlet.</span></span> <span data-ttu-id="7a14b-116">Varsa *StorageAccountName* parametresi belirtilirse, ardından cmdlet her zaman parametre ile bir tanılama yapılandırma dosyasında belirtilen belirtilen depolama hesabı kullanır.</span><span class="sxs-lookup"><span data-stu-id="7a14b-116">If the *StorageAccountName* parameter is specified, then the cmdlet will always use the storage account that is specified in the parameter and not the one that is specified in the diagnostics configuration file.</span></span>

<span data-ttu-id="7a14b-117">Sanal makineden farklı bir abonelik tanılama depolama hesabı bulunduğu sonra içinde açıkça geçirmenize gerek *StorageAccountName* ve *StorageAccountKey* cmdlet parametreleri.</span><span class="sxs-lookup"><span data-stu-id="7a14b-117">If the diagnostics storage account is in a different subscription from the VM, then you need to explicitly pass in the *StorageAccountName* and *StorageAccountKey* parameters to the cmdlet.</span></span> <span data-ttu-id="7a14b-118">*StorageAccountKey* cmdlet, otomatik olarak sorgulamak ve tanılama uzantısını etkinleştirirken anahtar değeri ayarlamak gibi tanılama depolama hesabı aynı abonelikte olduğunda parametresi gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="7a14b-118">The *StorageAccountKey* parameter is not needed when the diagnostics storage account is in the same subscription, as the cmdlet can automatically query and set the key value when enabling the diagnostics extension.</span></span> <span data-ttu-id="7a14b-119">Ancak, tanılama depolama hesabı farklı bir abonelikte cmdlet anahtarını otomatik olarak almak mümkün olmayabilir açıkça gereken ise ve tuşuyla belirtmeniz *StorageAccountKey* parametresi.</span><span class="sxs-lookup"><span data-stu-id="7a14b-119">However, if the diagnostics storage account is in a different subscription, then the cmdlet might not be able to get the key automatically and you need to explicitly specify the key through the *StorageAccountKey* parameter.</span></span>  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

<span data-ttu-id="7a14b-120">Tanılama uzantısını VM üzerinde etkinleştirildikten sonra geçerli ayarları kullanarak alabileceğiniz [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="7a14b-120">Once the diagnostics extension is enabled on a VM, you can get the current settings by using the [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span></span>

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

<span data-ttu-id="7a14b-121">Cmdlet döndürür *PublicSettings*, tanılama yapılandırması içerir.</span><span class="sxs-lookup"><span data-stu-id="7a14b-121">The cmdlet returns *PublicSettings*, which contains the diagnostics configuration.</span></span> <span data-ttu-id="7a14b-122">Desteklenen yapılandırma, WadCfg ve xmlCfg iki tür vardır.</span><span class="sxs-lookup"><span data-stu-id="7a14b-122">There are two kinds of configuration supported, WadCfg and xmlCfg.</span></span> <span data-ttu-id="7a14b-123">WadCfg JSON yapılandırması ve xmlCfg XML yapılandırması Base64 ile kodlanmış bir biçimde değil.</span><span class="sxs-lookup"><span data-stu-id="7a14b-123">WadCfg is JSON configuration, and xmlCfg is XML configuration in a Base64-encoded format.</span></span> <span data-ttu-id="7a14b-124">XML okumak için çözülmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7a14b-124">To read the XML, you need to decode it.</span></span>

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

<span data-ttu-id="7a14b-125">[Kaldır AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet, VM'den tanılama uzantısını kaldırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7a14b-125">The [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet can be used to remove the diagnostics extension from the VM.</span></span>  

## <a name="enable-the-diagnostics-extension-if-you-use-the-classic-deployment-model"></a><span data-ttu-id="7a14b-126">Klasik dağıtım modeli kullanırsanız tanılama uzantısını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="7a14b-126">Enable the diagnostics extension if you use the classic deployment model</span></span>
<span data-ttu-id="7a14b-127">Kullanabileceğiniz [kümesi AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet Klasik dağıtım modeli aracılığıyla oluşturduğunuz bir VM'de tanılama uzantısını etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="7a14b-127">You can use the [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet to enable a diagnostics extension on a VM that you create through the classic deployment model.</span></span> <span data-ttu-id="7a14b-128">Aşağıdaki örnek tanılama uzantısı ile klasik dağıtım modeli aracılığıyla yeni bir VM oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7a14b-128">The following example shows how to create a new VM through the classic deployment model with the diagnostics extension enabled.</span></span>

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

<span data-ttu-id="7a14b-129">Klasik dağıtım modeli aracılığıyla oluşturulmuş mevcut bir VM'yi tanılama uzantısını etkinleştirmek için önce kullanın [Get-AzureVM](/powershell/module/azure/get-azurevm) VM yapılandırmasını almak için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7a14b-129">To enable the diagnostics extension on an existing VM that was created through the classic deployment model, first use the [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet to get the VM configuration.</span></span> <span data-ttu-id="7a14b-130">Tanılama uzantısını kullanarak eklemek için VM yapılandırması güncelleştirme [kümesi AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="7a14b-130">Then update the VM configuration to include the diagnostics extension by using the [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span></span> <span data-ttu-id="7a14b-131">Son olarak, güncelleştirilmiş yapılandırmayı kullanarak VM uygulamak [güncelleştirme-AzureVM](/powershell/module/azure/update-azurevm).</span><span class="sxs-lookup"><span data-stu-id="7a14b-131">Finally, apply the updated configuration to the VM by using [Update-AzureVM](/powershell/module/azure/update-azurevm).</span></span>

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a><span data-ttu-id="7a14b-132">Örnek tanılama yapılandırması</span><span class="sxs-lookup"><span data-stu-id="7a14b-132">Sample diagnostics configuration</span></span>
<span data-ttu-id="7a14b-133">Aşağıdaki XML, yukarıdaki komut dosyalarıyla tanılama genel yapılandırması için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7a14b-133">The following XML can be used for the diagnostics public configuration with the above scripts.</span></span> <span data-ttu-id="7a14b-134">Bu örnek yapılandırmanın çeşitli performans sayaçları tanılama depolama hesabı, uygulama, güvenlik ve Windows olay günlüklerini kanallarında sistem hatalarını ve tanılama altyapı günlüklerinden hataları birlikte aktarın.</span><span class="sxs-lookup"><span data-stu-id="7a14b-134">This sample configuration will transfer various performance counters to the diagnostics storage account, along with errors from the application, security, and system channels in the Windows event logs and any errors from the diagnostics infrastructure logs.</span></span>

<span data-ttu-id="7a14b-135">Yapılandırma aşağıdaki içerecek şekilde güncelleştirilmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="7a14b-135">The configuration needs to be updated to include the following:</span></span>

* <span data-ttu-id="7a14b-136">*ResourceId* özniteliği **ölçümleri** öğesi kaynak Kimliğiyle VM için güncelleştirilmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="7a14b-136">The *resourceID* attribute of the **Metrics** element needs to be updated with the resource ID for the VM.</span></span>
  
  * <span data-ttu-id="7a14b-137">Kaynak Kimliği şu biçimi kullanarak oluşturulabilir: "/ subscriptions / {*VM ile abonelik kimliği için abonelik*} /resourceGroups/ {*VM için kaynak grubu adı*} / providers/Microsoft.Compute/virtualMachines/ {*VM adını*} ".</span><span class="sxs-lookup"><span data-stu-id="7a14b-137">The resource ID can be constructed by using the following pattern: "/subscriptions/{*subscription ID for the subscription with the VM*}/resourceGroups/{*The resourcegroup name for the VM*}/providers/Microsoft.Compute/virtualMachines/{*The VM Name*}".</span></span>
  * <span data-ttu-id="7a14b-138">Örneğin, VM çalıştığı abonelik için abonelik kimliği ise **11111111-1111-1111-1111-111111111111**, kaynak grubu için kaynak grubu adı **MyResourceGroup**ve VM adı **MyWindowsVM**, ardından değeri *ResourceId* olacaktır:</span><span class="sxs-lookup"><span data-stu-id="7a14b-138">For example, if the subscription ID for the subscription where the VM is running is **11111111-1111-1111-1111-111111111111**, the resource group name for the resource group is **MyResourceGroup**, and the VM Name is **MyWindowsVM**, then the value for *resourceID* would be:</span></span>
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * <span data-ttu-id="7a14b-139">Hakkında daha fazla bilgi için ölçümleri performans sayaçları ve ölçümleri yapılandırmasını temel alarak oluşturulur, bkz: [depolama Azure tanılama ölçümleri tablosuna](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span><span class="sxs-lookup"><span data-stu-id="7a14b-139">For more information on how metrics are generated based on the performance counters and metrics configuration, see [Azure Diagnostics metrics table in storage](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span></span>
* <span data-ttu-id="7a14b-140">**StorageAccount** öğesi tanılama depolama hesabı adı ile güncelleştirilmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="7a14b-140">The **StorageAccount** element needs to be updated with the name of the diagnostics storage account.</span></span>
  
    ```
    <?xml version="1.0" encoding="utf-8"?>
    <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
        <WadCfg>
          <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
            <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error"/>
            <PerformanceCounters scheduledTransferPeriod="PT1M">
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU utilization" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Privileged Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU privileged time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% User Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU user time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor Information(_Total)\Processor Frequency" sampleRate="PT15S" unit="Count">
            <annotation displayName="CPU frequency" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\System\Processes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Processes" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Thread Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Threads" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Handle Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Handles" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\% Committed Bytes In Use" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Memory usage" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory available" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory committed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Commit Limit" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory commit limit" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Paged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Nonpaged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory non-paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Read Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active read time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Write Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active write time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Transfers/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Reads/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk read operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Writes/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk write operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Read Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk read speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Write Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk write speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Read Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average read queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Write Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average write queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\% Free Space" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk free space (percentage)" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\Free Megabytes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk free space (MB)" locale="en-us"/>
          </PerformanceCounterConfiguration>
        </PerformanceCounters>
        <Metrics resourceId="(Update with resource ID for the VM)" >
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*[System[(Level = 1 or Level = 2)]]"/>
          <DataSource name="Security!*[System[(Level = 1 or Level = 2)]"/>
          <DataSource name="System!*[System[(Level = 1 or Level = 2)]]"/>
        </WindowsEventLog>
          </DiagnosticMonitorConfiguration>
        </WadCfg>
        <StorageAccount>(Update with diagnostics storage account name)</StorageAccount>
    </PublicConfig>
    ```

## <a name="next-steps"></a><span data-ttu-id="7a14b-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7a14b-141">Next steps</span></span>
* <span data-ttu-id="7a14b-142">Sorunları gidermek için Azure tanılama yetenek ve başka teknikler kullanarak ek yönergeler için bkz: [Azure Cloud Services ve sanal makineleri etkinleştirme tanılamada](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="7a14b-142">For additional guidance on using the Azure Diagnostics capability and other techniques to troubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="7a14b-143">[Tanılama yapılandırmaları şema](https://msdn.microsoft.com/library/azure/mt634524.aspx) tanılama uzantısını için çeşitli XML yapılandırma seçenekleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7a14b-143">[Diagnostics configurations schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) explains the various XML configurations options for the diagnostics extension.</span></span>

