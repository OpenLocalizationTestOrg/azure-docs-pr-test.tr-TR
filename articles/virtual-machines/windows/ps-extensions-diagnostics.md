---
title: "bir Windows VM üzerinde Azure PowerShell tooenable tanılamayı aaaUse | Microsoft Docs"
services: virtual-machines-windows
documentationcenter: 
description: "Bilgi nasıl Windows çalıştıran bir sanal makinede toouse PowerShell tooenable Azure tanılama"
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
ms.openlocfilehash: e945f0de154b5ba600f845f0d577b48e2254573b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooenable-azure-diagnostics-in-a-virtual-machine-running-windows"></a><span data-ttu-id="abf99-103">Windows çalıştıran bir sanal makinede PowerShell tooenable Azure Tanılama'yı kullanın</span><span class="sxs-lookup"><span data-stu-id="abf99-103">Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="abf99-104">Azure Tanılama, dağıtılan bir uygulama tanılama verilerini hello koleksiyonunu sağlayan Azure içinde hello yetenektir.</span><span class="sxs-lookup"><span data-stu-id="abf99-104">Azure Diagnostics is hello capability within Azure that enables hello collection of diagnostic data on a deployed application.</span></span> <span data-ttu-id="abf99-105">Merhaba tanılama uzantısını toocollect tanılama veri uygulama günlükleri veya bir Azure sanal makinesinden Windows çalıştıran (VM) performans sayaçları gibi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="abf99-105">You can use hello diagnostics extension toocollect diagnostic data like application logs or performance counters from an Azure virtual machine (VM) that is running Windows.</span></span> <span data-ttu-id="abf99-106">Bu makalede nasıl toouse Windows PowerShell tooenable hello tanılama uzantı için bir VM açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="abf99-106">This article describes how toouse Windows PowerShell tooenable hello diagnostics extension for a VM.</span></span> <span data-ttu-id="abf99-107">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) için bu makalede gerekli hello Önkoşullar için.</span><span class="sxs-lookup"><span data-stu-id="abf99-107">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span>

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-resource-manager-deployment-model"></a><span data-ttu-id="abf99-108">Merhaba Resource Manager dağıtım modeli kullanırsanız hello tanılama uzantısını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="abf99-108">Enable hello diagnostics extension if you use hello Resource Manager deployment model</span></span>
<span data-ttu-id="abf99-109">Merhaba uzantısı yapılandırma toohello Resource Manager şablonu ekleyerek hello Azure Resource Manager dağıtım modeli üzerinden Windows VM oluştururken hello tanılama uzantısını etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="abf99-109">You can enable hello diagnostics extension while you create a Windows VM through hello Azure Resource Manager deployment model by adding hello extension configuration toohello Resource Manager template.</span></span> <span data-ttu-id="abf99-110">Bkz: [hello Azure Resource Manager şablonunu kullanarak izleme ve tanılama Windows sanal makine oluşturma](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="abf99-110">See [Create a Windows virtual machine with monitoring and diagnostics by using hello Azure Resource Manager template](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="abf99-111">tooenable hello tanılama uzantısını hello Resource Manager dağıtım modeli oluşturulmuş mevcut bir VM'yi, kullanabileceğiniz hello [kümesi AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet'ini aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="abf99-111">tooenable hello diagnostics extension on an existing VM that was created through hello Resource Manager deployment model, you can use hello [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet as shown below.</span></span>

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


<span data-ttu-id="abf99-112">*$diagnosticsconfig_path* hello açıklandığı gibi XML'de hello tanılama yapılandırması içeren hello yolu toohello dosyası olduğundan [örnek](#sample-diagnostics-configuration) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="abf99-112">*$diagnosticsconfig_path* is hello path toohello file that contains hello diagnostics configuration in XML, as described in hello [sample](#sample-diagnostics-configuration) below.</span></span>  

<span data-ttu-id="abf99-113">Merhaba tanılama yapılandırma dosyası belirtiyorsa bir **StorageAccount** bir depolama hesabı adı bir öğesiyle sonra hello *kümesi AzureRMVMDiagnosticsExtension* komut dosyası otomatik olarak hello ayarlayın Tanılama uzantısını toosend tanılama veri toothat depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="abf99-113">If hello diagnostics configuration file specifies a **StorageAccount** element with a storage account name, then hello *Set-AzureRMVMDiagnosticsExtension* script will automatically set hello diagnostics extension toosend diagnostic data toothat storage account.</span></span> <span data-ttu-id="abf99-114">Bu toowork için hello depolama hesabının içinde toobe gerekir VM hello gibi aynı abonelik hello.</span><span class="sxs-lookup"><span data-stu-id="abf99-114">For this toowork, hello storage account needs toobe in hello same subscription as hello VM.</span></span>

<span data-ttu-id="abf99-115">Öyle değilse **StorageAccount** yeniden hello toopass gerekiyor hello tanılama yapılandırması, belirtilen *StorageAccountName* parametresi toohello cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="abf99-115">If no **StorageAccount** was specified in hello diagnostics configuration, then you need toopass in hello *StorageAccountName* parameter toohello cmdlet.</span></span> <span data-ttu-id="abf99-116">Merhaba, *StorageAccountName* parametresi belirtilirse, ardından hello cmdlet'i her zaman hello parametresinde belirtilen hello depolama hesabı kullanıyorsanız ve hello tanılama yapılandırma dosyasında belirtilen bir hello değil.</span><span class="sxs-lookup"><span data-stu-id="abf99-116">If hello *StorageAccountName* parameter is specified, then hello cmdlet will always use hello storage account that is specified in hello parameter and not hello one that is specified in hello diagnostics configuration file.</span></span>

<span data-ttu-id="abf99-117">Merhaba tanılama depolama hesabı konusu hello VM, farklı bir abonelik yeniden tooexplicitly gerekiyor hello geçirirseniz *StorageAccountName* ve *StorageAccountKey* parametreleri toohello cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="abf99-117">If hello diagnostics storage account is in a different subscription from hello VM, then you need tooexplicitly pass in hello *StorageAccountName* and *StorageAccountKey* parameters toohello cmdlet.</span></span> <span data-ttu-id="abf99-118">Merhaba *StorageAccountKey* parametresi hello cmdlet, otomatik olarak sorgulamak ve hello tanılama uzantı etkinleştirilirken hello anahtar değeri ayarlamak gibi hello tanılama depolama hesabı olan aynı abonelik hello zaman gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="abf99-118">hello *StorageAccountKey* parameter is not needed when hello diagnostics storage account is in hello same subscription, as hello cmdlet can automatically query and set hello key value when enabling hello diagnostics extension.</span></span> <span data-ttu-id="abf99-119">Ancak, Merhaba, tanılama depolama hesabı farklı bir abonelikte sonra hello cmdlet mümkün tooget hello anahtarı otomatik olarak olmayabilir ve tooexplicitly ihtiyacınız hello hello tuşuyla belirtin *StorageAccountKey* parametre.</span><span class="sxs-lookup"><span data-stu-id="abf99-119">However, if hello diagnostics storage account is in a different subscription, then hello cmdlet might not be able tooget hello key automatically and you need tooexplicitly specify hello key through hello *StorageAccountKey* parameter.</span></span>  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

<span data-ttu-id="abf99-120">Merhaba tanılama uzantısını VM üzerinde etkinleştirildikten sonra hello kullanarak hello geçerli ayarları alabilirsiniz [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="abf99-120">Once hello diagnostics extension is enabled on a VM, you can get hello current settings by using hello [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span></span>

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

<span data-ttu-id="abf99-121">Merhaba cmdlet'i döndürür *PublicSettings*, hello tanılama yapılandırması içerir.</span><span class="sxs-lookup"><span data-stu-id="abf99-121">hello cmdlet returns *PublicSettings*, which contains hello diagnostics configuration.</span></span> <span data-ttu-id="abf99-122">Desteklenen yapılandırma, WadCfg ve xmlCfg iki tür vardır.</span><span class="sxs-lookup"><span data-stu-id="abf99-122">There are two kinds of configuration supported, WadCfg and xmlCfg.</span></span> <span data-ttu-id="abf99-123">WadCfg JSON yapılandırması ve xmlCfg XML yapılandırması Base64 ile kodlanmış bir biçimde değil.</span><span class="sxs-lookup"><span data-stu-id="abf99-123">WadCfg is JSON configuration, and xmlCfg is XML configuration in a Base64-encoded format.</span></span> <span data-ttu-id="abf99-124">tooread XML Merhaba, toodecode gerekir.</span><span class="sxs-lookup"><span data-stu-id="abf99-124">tooread hello XML, you need toodecode it.</span></span>

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

<span data-ttu-id="abf99-125">Merhaba [Kaldır AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet kullanılan tooremove hello tanılama uzantısını hello VM olabilir.</span><span class="sxs-lookup"><span data-stu-id="abf99-125">hello [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet can be used tooremove hello diagnostics extension from hello VM.</span></span>  

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-classic-deployment-model"></a><span data-ttu-id="abf99-126">Merhaba Klasik dağıtım modelini kullanırsanız hello tanılama uzantısını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="abf99-126">Enable hello diagnostics extension if you use hello classic deployment model</span></span>
<span data-ttu-id="abf99-127">Merhaba kullanabilirsiniz [kümesi AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet tooenable tanılama uzantısını hello Klasik dağıtım modeli aracılığıyla oluşturduğunuz bir VM üzerinde.</span><span class="sxs-lookup"><span data-stu-id="abf99-127">You can use hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet tooenable a diagnostics extension on a VM that you create through hello classic deployment model.</span></span> <span data-ttu-id="abf99-128">Merhaba aşağıdaki örnekte nasıl toocreate hello tanılama uzantısını ile Merhaba Klasik dağıtım modeli aracılığıyla yeni bir VM etkin gösterir.</span><span class="sxs-lookup"><span data-stu-id="abf99-128">hello following example shows how toocreate a new VM through hello classic deployment model with hello diagnostics extension enabled.</span></span>

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

<span data-ttu-id="abf99-129">Merhaba Klasik dağıtım modeli, ilk kullanım hello aracılığıyla oluşturulmuş mevcut bir VM'yi tooenable hello tanılama uzantısını [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet tooget hello VM yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="abf99-129">tooenable hello diagnostics extension on an existing VM that was created through hello classic deployment model, first use hello [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet tooget hello VM configuration.</span></span> <span data-ttu-id="abf99-130">Ardından hello kullanarak hello VM yapılandırması tooinclude hello tanılama uzantısını güncelleştirin [kümesi AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="abf99-130">Then update hello VM configuration tooinclude hello diagnostics extension by using hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span></span> <span data-ttu-id="abf99-131">Son olarak, güncelleştirilmiş hello yapılandırma toohello VM kullanarak uygulama [güncelleştirme-AzureVM](/powershell/module/azure/update-azurevm).</span><span class="sxs-lookup"><span data-stu-id="abf99-131">Finally, apply hello updated configuration toohello VM by using [Update-AzureVM](/powershell/module/azure/update-azurevm).</span></span>

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a><span data-ttu-id="abf99-132">Örnek tanılama yapılandırması</span><span class="sxs-lookup"><span data-stu-id="abf99-132">Sample diagnostics configuration</span></span>
<span data-ttu-id="abf99-133">Merhaba aşağıdaki XML hello tanılama ortak yapılandırma komut dosyaları yukarıdaki hello için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="abf99-133">hello following XML can be used for hello diagnostics public configuration with hello above scripts.</span></span> <span data-ttu-id="abf99-134">Bu örnek yapılandırmanın çeşitli performans sayaçları toohello tanılama depolama hesabı, Merhaba uygulaması, güvenlik ve sistem kanalları hello Windows olay günlüklerindeki hatalar birlikte ve hataları hello tanılama aktarır Altyapı günlükleri.</span><span class="sxs-lookup"><span data-stu-id="abf99-134">This sample configuration will transfer various performance counters toohello diagnostics storage account, along with errors from hello application, security, and system channels in hello Windows event logs and any errors from hello diagnostics infrastructure logs.</span></span>

<span data-ttu-id="abf99-135">Merhaba yapılandırma toobe güncelleştirilmiş tooinclude hello aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="abf99-135">hello configuration needs toobe updated tooinclude hello following:</span></span>

* <span data-ttu-id="abf99-136">Merhaba *ResourceId* hello özniteliği **ölçümleri** öğesi hello kaynak kimliği hello VM için güncelleştirilmiş toobe gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="abf99-136">hello *resourceID* attribute of hello **Metrics** element needs toobe updated with hello resource ID for hello VM.</span></span>
  
  * <span data-ttu-id="abf99-137">Merhaba kaynak kimliği desen aşağıdaki hello kullanarak olacak oluşturulan: "/ subscriptions / {*hello VM ile Merhaba abonelik için abonelik Kimliğini*} /resourceGroups/ {*hello VMhellokaynakgrubuadı*} / providers/Microsoft.Compute/virtualMachines/ {*VM adı hello*} ".</span><span class="sxs-lookup"><span data-stu-id="abf99-137">hello resource ID can be constructed by using hello following pattern: "/subscriptions/{*subscription ID for hello subscription with hello VM*}/resourceGroups/{*hello resourcegroup name for hello VM*}/providers/Microsoft.Compute/virtualMachines/{*hello VM Name*}".</span></span>
  * <span data-ttu-id="abf99-138">Örneğin, hello hello VM çalıştırdığı hello abonelik için abonelik Kimliğini ise **11111111-1111-1111-1111-111111111111**, hello kaynak grubu adı hello kaynak grubu için **MyResourceGroup**, ve hello VM adı **MyWindowsVM**, değeri hello *ResourceId* olacaktır:</span><span class="sxs-lookup"><span data-stu-id="abf99-138">For example, if hello subscription ID for hello subscription where hello VM is running is **11111111-1111-1111-1111-111111111111**, hello resource group name for hello resource group is **MyResourceGroup**, and hello VM Name is **MyWindowsVM**, then hello value for *resourceID* would be:</span></span>
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * <span data-ttu-id="abf99-139">Ölçümleri oluşturulan göre hello performans sayaçları ve ölçümleri yapılandırma şeklini daha fazla bilgi için bkz: [depolama Azure tanılama ölçümleri tablosuna](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span><span class="sxs-lookup"><span data-stu-id="abf99-139">For more information on how metrics are generated based on hello performance counters and metrics configuration, see [Azure Diagnostics metrics table in storage](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span></span>
* <span data-ttu-id="abf99-140">Merhaba **StorageAccount** öğesi hello hello tanılama depolama hesabı adıyla güncelleştirilmiş toobe gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="abf99-140">hello **StorageAccount** element needs toobe updated with hello name of hello diagnostics storage account.</span></span>
  
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
        <Metrics resourceId="(Update with resource ID for hello VM)" >
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

## <a name="next-steps"></a><span data-ttu-id="abf99-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="abf99-141">Next steps</span></span>
* <span data-ttu-id="abf99-142">Hello Azure tanılama özelliği ve diğer teknikleri tootroubleshoot sorunları kullanma ile ilgili ek kılavuzlar için bkz: [Azure Cloud Services ve sanal makineleri etkinleştirme tanılamada](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="abf99-142">For additional guidance on using hello Azure Diagnostics capability and other techniques tootroubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="abf99-143">[Tanılama yapılandırmaları şema](https://msdn.microsoft.com/library/azure/mt634524.aspx) hello çeşitli XML yapılandırmaları hello tanılama uzantısını için seçenekleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="abf99-143">[Diagnostics configurations schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) explains hello various XML configurations options for hello diagnostics extension.</span></span>

