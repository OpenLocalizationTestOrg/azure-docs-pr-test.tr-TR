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
# <a name="use-powershell-tooenable-azure-diagnostics-in-a-virtual-machine-running-windows"></a>Windows çalıştıran bir sanal makinede PowerShell tooenable Azure Tanılama'yı kullanın
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Azure Tanılama, dağıtılan bir uygulama tanılama verilerini hello koleksiyonunu sağlayan Azure içinde hello yetenektir. Merhaba tanılama uzantısını toocollect tanılama veri uygulama günlükleri veya bir Azure sanal makinesinden Windows çalıştıran (VM) performans sayaçları gibi kullanabilirsiniz. Bu makalede nasıl toouse Windows PowerShell tooenable hello tanılama uzantı için bir VM açıklanmaktadır. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) için bu makalede gerekli hello Önkoşullar için.

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-resource-manager-deployment-model"></a>Merhaba Resource Manager dağıtım modeli kullanırsanız hello tanılama uzantısını etkinleştirme
Merhaba uzantısı yapılandırma toohello Resource Manager şablonu ekleyerek hello Azure Resource Manager dağıtım modeli üzerinden Windows VM oluştururken hello tanılama uzantısını etkinleştirebilirsiniz. Bkz: [hello Azure Resource Manager şablonunu kullanarak izleme ve tanılama Windows sanal makine oluşturma](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

tooenable hello tanılama uzantısını hello Resource Manager dağıtım modeli oluşturulmuş mevcut bir VM'yi, kullanabileceğiniz hello [kümesi AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet'ini aşağıda gösterildiği gibi.

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


*$diagnosticsconfig_path* hello açıklandığı gibi XML'de hello tanılama yapılandırması içeren hello yolu toohello dosyası olduğundan [örnek](#sample-diagnostics-configuration) aşağıda.  

Merhaba tanılama yapılandırma dosyası belirtiyorsa bir **StorageAccount** bir depolama hesabı adı bir öğesiyle sonra hello *kümesi AzureRMVMDiagnosticsExtension* komut dosyası otomatik olarak hello ayarlayın Tanılama uzantısını toosend tanılama veri toothat depolama hesabı. Bu toowork için hello depolama hesabının içinde toobe gerekir VM hello gibi aynı abonelik hello.

Öyle değilse **StorageAccount** yeniden hello toopass gerekiyor hello tanılama yapılandırması, belirtilen *StorageAccountName* parametresi toohello cmdlet'i. Merhaba, *StorageAccountName* parametresi belirtilirse, ardından hello cmdlet'i her zaman hello parametresinde belirtilen hello depolama hesabı kullanıyorsanız ve hello tanılama yapılandırma dosyasında belirtilen bir hello değil.

Merhaba tanılama depolama hesabı konusu hello VM, farklı bir abonelik yeniden tooexplicitly gerekiyor hello geçirirseniz *StorageAccountName* ve *StorageAccountKey* parametreleri toohello cmdlet'i. Merhaba *StorageAccountKey* parametresi hello cmdlet, otomatik olarak sorgulamak ve hello tanılama uzantı etkinleştirilirken hello anahtar değeri ayarlamak gibi hello tanılama depolama hesabı olan aynı abonelik hello zaman gerekli değildir. Ancak, Merhaba, tanılama depolama hesabı farklı bir abonelikte sonra hello cmdlet mümkün tooget hello anahtarı otomatik olarak olmayabilir ve tooexplicitly ihtiyacınız hello hello tuşuyla belirtin *StorageAccountKey* parametre.  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

Merhaba tanılama uzantısını VM üzerinde etkinleştirildikten sonra hello kullanarak hello geçerli ayarları alabilirsiniz [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet'i.

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

Merhaba cmdlet'i döndürür *PublicSettings*, hello tanılama yapılandırması içerir. Desteklenen yapılandırma, WadCfg ve xmlCfg iki tür vardır. WadCfg JSON yapılandırması ve xmlCfg XML yapılandırması Base64 ile kodlanmış bir biçimde değil. tooread XML Merhaba, toodecode gerekir.

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

Merhaba [Kaldır AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet kullanılan tooremove hello tanılama uzantısını hello VM olabilir.  

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-classic-deployment-model"></a>Merhaba Klasik dağıtım modelini kullanırsanız hello tanılama uzantısını etkinleştirme
Merhaba kullanabilirsiniz [kümesi AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet tooenable tanılama uzantısını hello Klasik dağıtım modeli aracılığıyla oluşturduğunuz bir VM üzerinde. Merhaba aşağıdaki örnekte nasıl toocreate hello tanılama uzantısını ile Merhaba Klasik dağıtım modeli aracılığıyla yeni bir VM etkin gösterir.

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

Merhaba Klasik dağıtım modeli, ilk kullanım hello aracılığıyla oluşturulmuş mevcut bir VM'yi tooenable hello tanılama uzantısını [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet tooget hello VM yapılandırması. Ardından hello kullanarak hello VM yapılandırması tooinclude hello tanılama uzantısını güncelleştirin [kümesi AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet'i. Son olarak, güncelleştirilmiş hello yapılandırma toohello VM kullanarak uygulama [güncelleştirme-AzureVM](/powershell/module/azure/update-azurevm).

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a>Örnek tanılama yapılandırması
Merhaba aşağıdaki XML hello tanılama ortak yapılandırma komut dosyaları yukarıdaki hello için kullanılabilir. Bu örnek yapılandırmanın çeşitli performans sayaçları toohello tanılama depolama hesabı, Merhaba uygulaması, güvenlik ve sistem kanalları hello Windows olay günlüklerindeki hatalar birlikte ve hataları hello tanılama aktarır Altyapı günlükleri.

Merhaba yapılandırma toobe güncelleştirilmiş tooinclude hello aşağıdakiler gerekir:

* Merhaba *ResourceId* hello özniteliği **ölçümleri** öğesi hello kaynak kimliği hello VM için güncelleştirilmiş toobe gerekiyor.
  
  * Merhaba kaynak kimliği desen aşağıdaki hello kullanarak olacak oluşturulan: "/ subscriptions / {*hello VM ile Merhaba abonelik için abonelik Kimliğini*} /resourceGroups/ {*hello VMhellokaynakgrubuadı*} / providers/Microsoft.Compute/virtualMachines/ {*VM adı hello*} ".
  * Örneğin, hello hello VM çalıştırdığı hello abonelik için abonelik Kimliğini ise **11111111-1111-1111-1111-111111111111**, hello kaynak grubu adı hello kaynak grubu için **MyResourceGroup**, ve hello VM adı **MyWindowsVM**, değeri hello *ResourceId* olacaktır:
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * Ölçümleri oluşturulan göre hello performans sayaçları ve ölçümleri yapılandırma şeklini daha fazla bilgi için bkz: [depolama Azure tanılama ölçümleri tablosuna](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).
* Merhaba **StorageAccount** öğesi hello hello tanılama depolama hesabı adıyla güncelleştirilmiş toobe gerekiyor.
  
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

## <a name="next-steps"></a>Sonraki adımlar
* Hello Azure tanılama özelliği ve diğer teknikleri tootroubleshoot sorunları kullanma ile ilgili ek kılavuzlar için bkz: [Azure Cloud Services ve sanal makineleri etkinleştirme tanılamada](../../cloud-services/cloud-services-dotnet-diagnostics.md).
* [Tanılama yapılandırmaları şema](https://msdn.microsoft.com/library/azure/mt634524.aspx) hello çeşitli XML yapılandırmaları hello tanılama uzantısını için seçenekleri açıklar.

