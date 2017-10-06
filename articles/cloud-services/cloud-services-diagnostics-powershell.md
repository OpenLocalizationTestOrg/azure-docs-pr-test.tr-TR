---
title: "PowerShell kullanarak Azure Cloud Services aaaEnable tanılamada | Microsoft Docs"
description: "Bulut için tooenable tanılama PowerShell kullanarak hizmetleri nasıl öğrenin"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 66e08754-8639-4022-ae18-4237749ba17d
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/06/2016
ms.author: adegeo
ms.openlocfilehash: 7c7444df13edc8d7f5663e20ec7558d36aac45d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a>PowerShell kullanarak Azure Cloud Services tanılamada etkinleştir
Uygulama günlükleri gibi tanılama verilerini toplamak, performans sayaçlarını kullanarak bulut hizmeti vb. Azure tanılama uzantısını hello. Bu makalede nasıl tooenable hello Azure tanılama uzantısını PowerShell kullanarak bir bulut hizmeti için açıklanmaktadır.  Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) için bu makalede gerekli hello Önkoşullar için.

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>Bulut Hizmeti dağıtımının bir parçası olarak tanılama uzantısını etkinleştirme
Bu yaklaşım uygun toocontinuous tümleştirme senaryoları, burada hello tanılama uzantısını dağıtma bir parçası olarak etkinleştirilebilir bulut hizmeti hello türüdür. Yeni bir bulut hizmeti dağıtımı oluştururken hello geçirerek hello tanılama uzantısını etkinleştirebilirsiniz *ExtensionConfiguration* parametresi toohello [yeni AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet'i. Merhaba *ExtensionConfiguration* parametresi alan bir dizi hello kullanılarak oluşturulabilir tanılama Yapılandırması [yeni AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet'i.

Merhaba aşağıdaki örnekte nasıl WebRole ve her farklı tanılama yapılandırması sahip örn, bir bulut hizmeti için tanılama etkinleştirebilirsiniz gösterilmektedir.

```powershell
$service_name = "MyService"
$service_package = "CloudService.cspkg"
$service_config = "ServiceConfiguration.Cloud.cscfg"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)
```

Merhaba tanılama yapılandırma dosyası belirtiyorsa bir `StorageAccount` bir depolama hesabı adı bir öğesiyle sonra hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet'i otomatik olarak bu depolama hesabı kullanın. Bu toowork için hello depolama hesabının içinde toobe gerekir. bulut hizmeti dağıtılan hello gibi aynı abonelik hello.

MSBuild hello tarafından oluşturulan İleri hello uzantısı yapılandırma dosyalarını yayımlama Azure SDK 2.6 hedef çıktı hello hizmet yapılandırma dosyasında (.cscfg) belirtilen hello tanılama yapılandırma dizesi göre hello depolama hesabı adı içerir. Aşağıdaki Hello komut dosyası nasıl tooparse hello uzantısı yapılandırma hello dosyalarından hedef çıkış yayımlama ve hello bulut hizmeti dağıtırken tanılama uzantısını her rol için yapılandırma gösterir.

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find hello Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find hello RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
    $roleName = ""
    $roles = $extPath -split ".",0,"simplematch"
    if ($roles -is [system.array] -and $roles.Length -gt 1)
    {
        $roleName = $roles[1]
        $x = 2
        while ($x -le $roles.Length)
            {
               if ($roles[$x] -ne "PubConfig")
                {
                    $roleName = $roleName + "." + $roles[$x]
                }
                else
                {
                    break
                }
                $x++
            }
        $fullExtPath = Join-Path -path $extensionsSearchPath -ChildPath $extPath
        $diagnosticsconfig = New-AzureServiceDiagnosticsExtensionConfig -Role $roleName -DiagnosticsConfigurationPath $fullExtPath
        $diagnosticsConfigurations += $diagnosticsconfig
    }
}
New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration $diagnosticsConfigurations
```

Visual Studio Online, bulut hizmetlerinin hello tanılama uzantısını otomatik dağıtımlar için benzer bir yaklaşım kullanır. Bkz: [Yayımla AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) tam bir örnek için.

Öyle değilse `StorageAccount` yeniden hello toopass gerekiyor hello tanılama yapılandırması, belirtilen *StorageAccountName* parametresi toohello cmdlet'i. Merhaba, *StorageAccountName* parametresi belirtilirse, ardından hello cmdlet'i her zaman hello parametresinde belirtilen hello depolama hesabı kullanıyorsanız ve hello tanılama yapılandırma dosyasında belirtilen bir hello değil.

Merhaba tanılama depolama hesabı olan farklı bir abonelikte hello bulut hizmeti, gelen yeniden tooexplicitly gerekiyor hello geçirirseniz *StorageAccountName* ve *StorageAccountKey* parametreleri toohello cmdlet'ini kullanın. Merhaba *StorageAccountKey* parametresi hello cmdlet, otomatik olarak sorgulamak ve hello tanılama uzantı etkinleştirilirken hello anahtar değeri ayarlamak gibi hello tanılama depolama hesabı olan aynı abonelik hello zaman gerekli değildir. Ancak, Merhaba, tanılama depolama hesabı farklı bir abonelikte sonra hello cmdlet mümkün tooget hello anahtarı otomatik olarak olmayabilir ve tooexplicitly ihtiyacınız hello hello tuşuyla belirtin *StorageAccountKey* parametre.

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>Mevcut bir Bulut Hizmetinde tanılama uzantısını etkinleştirme
Merhaba kullanabilirsiniz [kümesi AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooenable veya güncelleştirme tanılama yapılandırması zaten çalışmakta olan bir bulut hizmeti üzerinde.

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a>Güncel tanılama uzantı yapılandırmasını alma
Kullanım hello [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget hello geçerli tanılama yapılandırması için bir bulut hizmeti.

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a>Tanılama uzantısını kaldırma
bir buluttaki tanılama kapalı tooturn hizmeti hello kullanabilirsiniz [Kaldır AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet'i.

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

Merhaba tanılama uzantısını kullanarak etkinleştirilirse *kümesi AzureServiceDiagnosticsExtension* veya hello *yeni AzureServiceDiagnosticsExtensionConfig* hello olmadan *rol* parametresi sonra kaldırabilir hello uzantısını kullanarak *Kaldır AzureServiceDiagnosticsExtension* hello olmadan *rol* parametresi. Merhaba, *rol* parametresi hello uzantısı sonra etkinleştirme ayrıca hello uzantı kaldırılırken kullanılmalıdır kullanıldı.

tek tek her rolden tooremove hello tanılama uzantısını:

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a>Sonraki Adımlar
* Azure tanılama ve diğer teknikleri tootroubleshoot sorunları kullanma ile ilgili ek kılavuzlar için bkz: [Azure Cloud Services ve sanal makineleri etkinleştirme tanılamada](cloud-services-dotnet-diagnostics.md).
* Merhaba [tanılama yapılandırma şeması](https://msdn.microsoft.com/library/azure/dn782207.aspx) hello çeşitli xml yapılandırmaları hello tanılama uzantısını için seçenekleri açıklar.
* Sanal makineler için tooenable hello tanılama uzantısını nasıl görürüm toolearn [izleme ve tanılama Azure Resource Manager şablonu kullanarak bir Windows sanal makine oluşturma](../virtual-machines/windows/extensions-diagnostics-template.md)
