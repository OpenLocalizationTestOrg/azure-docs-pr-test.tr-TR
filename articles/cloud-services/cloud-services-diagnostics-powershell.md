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
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="9c4a9-103">PowerShell kullanarak Azure Cloud Services tanılamada etkinleştir</span><span class="sxs-lookup"><span data-stu-id="9c4a9-103">Enable diagnostics in Azure Cloud Services using PowerShell</span></span>
<span data-ttu-id="9c4a9-104">Uygulama günlükleri gibi tanılama verilerini toplamak, performans sayaçlarını kullanarak bulut hizmeti vb. Azure tanılama uzantısını hello.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-104">You can collect diagnostic data like application logs, performance counters etc. from a Cloud Service using hello Azure Diagnostics extension.</span></span> <span data-ttu-id="9c4a9-105">Bu makalede nasıl tooenable hello Azure tanılama uzantısını PowerShell kullanarak bir bulut hizmeti için açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-105">This article describes how tooenable hello Azure Diagnostics extension for a Cloud Service using PowerShell.</span></span>  <span data-ttu-id="9c4a9-106">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) için bu makalede gerekli hello Önkoşullar için.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-106">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="9c4a9-107">Bulut Hizmeti dağıtımının bir parçası olarak tanılama uzantısını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="9c4a9-107">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="9c4a9-108">Bu yaklaşım uygun toocontinuous tümleştirme senaryoları, burada hello tanılama uzantısını dağıtma bir parçası olarak etkinleştirilebilir bulut hizmeti hello türüdür.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-108">This approach is applicable toocontinuous integration type of scenarios, where hello diagnostics extension can be enabled as part of deploying hello cloud service.</span></span> <span data-ttu-id="9c4a9-109">Yeni bir bulut hizmeti dağıtımı oluştururken hello geçirerek hello tanılama uzantısını etkinleştirebilirsiniz *ExtensionConfiguration* parametresi toohello [yeni AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-109">When creating a new Cloud Service deployment you can enable hello diagnostics extension by passing in hello *ExtensionConfiguration* parameter toohello [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="9c4a9-110">Merhaba *ExtensionConfiguration* parametresi alan bir dizi hello kullanılarak oluşturulabilir tanılama Yapılandırması [yeni AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-110">hello *ExtensionConfiguration* parameter takes an array of diagnostics configurations that can be created using hello [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span></span>

<span data-ttu-id="9c4a9-111">Merhaba aşağıdaki örnekte nasıl WebRole ve her farklı tanılama yapılandırması sahip örn, bir bulut hizmeti için tanılama etkinleştirebilirsiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-111">hello following example shows how you can enable diagnostics for a cloud service with a WebRole and WorkerRole, each having a different diagnostics configuration.</span></span>

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

<span data-ttu-id="9c4a9-112">Merhaba tanılama yapılandırma dosyası belirtiyorsa bir `StorageAccount` bir depolama hesabı adı bir öğesiyle sonra hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet'i otomatik olarak bu depolama hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-112">If hello diagnostics configuration file specifies a `StorageAccount` element with a storage account name, then hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet will automatically use that storage account.</span></span> <span data-ttu-id="9c4a9-113">Bu toowork için hello depolama hesabının içinde toobe gerekir. bulut hizmeti dağıtılan hello gibi aynı abonelik hello.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-113">For this toowork, hello storage account needs toobe in hello same subscription as hello Cloud Service being deployed.</span></span>

<span data-ttu-id="9c4a9-114">MSBuild hello tarafından oluşturulan İleri hello uzantısı yapılandırma dosyalarını yayımlama Azure SDK 2.6 hedef çıktı hello hizmet yapılandırma dosyasında (.cscfg) belirtilen hello tanılama yapılandırma dizesi göre hello depolama hesabı adı içerir.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-114">From Azure SDK 2.6 onward hello extension configuration files generated by hello MSBuild publish target output will include hello storage account name based on hello diagnostics configuration string specified in hello service configuration file (.cscfg).</span></span> <span data-ttu-id="9c4a9-115">Aşağıdaki Hello komut dosyası nasıl tooparse hello uzantısı yapılandırma hello dosyalarından hedef çıkış yayımlama ve hello bulut hizmeti dağıtırken tanılama uzantısını her rol için yapılandırma gösterir.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-115">hello script below shows you how tooparse hello Extension configuration files from hello publish target output and configure diagnostics extension for each role when deploying hello cloud service.</span></span>

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

<span data-ttu-id="9c4a9-116">Visual Studio Online, bulut hizmetlerinin hello tanılama uzantısını otomatik dağıtımlar için benzer bir yaklaşım kullanır.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-116">Visual Studio Online uses a similar approach for automated deployments of Cloud Services with hello diagnostics extension.</span></span> <span data-ttu-id="9c4a9-117">Bkz: [Yayımla AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) tam bir örnek için.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-117">See [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) for a complete example.</span></span>

<span data-ttu-id="9c4a9-118">Öyle değilse `StorageAccount` yeniden hello toopass gerekiyor hello tanılama yapılandırması, belirtilen *StorageAccountName* parametresi toohello cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-118">If no `StorageAccount` was specified in hello diagnostics configuration, then you need toopass in hello *StorageAccountName* parameter toohello cmdlet.</span></span> <span data-ttu-id="9c4a9-119">Merhaba, *StorageAccountName* parametresi belirtilirse, ardından hello cmdlet'i her zaman hello parametresinde belirtilen hello depolama hesabı kullanıyorsanız ve hello tanılama yapılandırma dosyasında belirtilen bir hello değil.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-119">If hello *StorageAccountName* parameter is specified, then hello cmdlet will always use hello storage account that is specified in hello parameter and not hello one that is specified in hello diagnostics configuration file.</span></span>

<span data-ttu-id="9c4a9-120">Merhaba tanılama depolama hesabı olan farklı bir abonelikte hello bulut hizmeti, gelen yeniden tooexplicitly gerekiyor hello geçirirseniz *StorageAccountName* ve *StorageAccountKey* parametreleri toohello cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-120">If hello diagnostics storage account is in a different subscription from hello Cloud Service, then you need tooexplicitly pass in hello *StorageAccountName* and *StorageAccountKey* parameters toohello cmdlet.</span></span> <span data-ttu-id="9c4a9-121">Merhaba *StorageAccountKey* parametresi hello cmdlet, otomatik olarak sorgulamak ve hello tanılama uzantı etkinleştirilirken hello anahtar değeri ayarlamak gibi hello tanılama depolama hesabı olan aynı abonelik hello zaman gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-121">hello *StorageAccountKey* parameter is not needed when hello diagnostics storage account is in hello same subscription, as hello cmdlet can automatically query and set hello key value when enabling hello diagnostics extension.</span></span> <span data-ttu-id="9c4a9-122">Ancak, Merhaba, tanılama depolama hesabı farklı bir abonelikte sonra hello cmdlet mümkün tooget hello anahtarı otomatik olarak olmayabilir ve tooexplicitly ihtiyacınız hello hello tuşuyla belirtin *StorageAccountKey* parametre.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-122">However, if hello diagnostics storage account is in a different subscription, then hello cmdlet might not be able tooget hello key automatically and you need tooexplicitly specify hello key through hello *StorageAccountKey* parameter.</span></span>

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="9c4a9-123">Mevcut bir Bulut Hizmetinde tanılama uzantısını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="9c4a9-123">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="9c4a9-124">Merhaba kullanabilirsiniz [kümesi AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooenable veya güncelleştirme tanılama yapılandırması zaten çalışmakta olan bir bulut hizmeti üzerinde.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-124">You can use hello [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooenable or update diagnostics configuration on a Cloud Service that is already running.</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="9c4a9-125">Güncel tanılama uzantı yapılandırmasını alma</span><span class="sxs-lookup"><span data-stu-id="9c4a9-125">Get current diagnostics extension configuration</span></span>
<span data-ttu-id="9c4a9-126">Kullanım hello [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget hello geçerli tanılama yapılandırması için bir bulut hizmeti.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-126">Use hello [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget hello current diagnostics configuration for a cloud service.</span></span>

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a><span data-ttu-id="9c4a9-127">Tanılama uzantısını kaldırma</span><span class="sxs-lookup"><span data-stu-id="9c4a9-127">Remove diagnostics extension</span></span>
<span data-ttu-id="9c4a9-128">bir buluttaki tanılama kapalı tooturn hizmeti hello kullanabilirsiniz [Kaldır AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-128">tooturn off diagnostics on a cloud service you can use hello [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="9c4a9-129">Merhaba tanılama uzantısını kullanarak etkinleştirilirse *kümesi AzureServiceDiagnosticsExtension* veya hello *yeni AzureServiceDiagnosticsExtensionConfig* hello olmadan *rol* parametresi sonra kaldırabilir hello uzantısını kullanarak *Kaldır AzureServiceDiagnosticsExtension* hello olmadan *rol* parametresi.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-129">If you enabled hello diagnostics extension using either *Set-AzureServiceDiagnosticsExtension* or hello *New-AzureServiceDiagnosticsExtensionConfig* without hello *Role* parameter then you can remove hello extension using *Remove-AzureServiceDiagnosticsExtension* without hello *Role* parameter.</span></span> <span data-ttu-id="9c4a9-130">Merhaba, *rol* parametresi hello uzantısı sonra etkinleştirme ayrıca hello uzantı kaldırılırken kullanılmalıdır kullanıldı.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-130">If hello *Role* parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="9c4a9-131">tek tek her rolden tooremove hello tanılama uzantısını:</span><span class="sxs-lookup"><span data-stu-id="9c4a9-131">tooremove hello diagnostics extension from each individual role:</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a><span data-ttu-id="9c4a9-132">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="9c4a9-132">Next Steps</span></span>
* <span data-ttu-id="9c4a9-133">Azure tanılama ve diğer teknikleri tootroubleshoot sorunları kullanma ile ilgili ek kılavuzlar için bkz: [Azure Cloud Services ve sanal makineleri etkinleştirme tanılamada](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="9c4a9-133">For additional guidance on using Azure diagnostics and other techniques tootroubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="9c4a9-134">Merhaba [tanılama yapılandırma şeması](https://msdn.microsoft.com/library/azure/dn782207.aspx) hello çeşitli xml yapılandırmaları hello tanılama uzantısını için seçenekleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="9c4a9-134">hello [Diagnostics Configuration Schema](https://msdn.microsoft.com/library/azure/dn782207.aspx) explains hello various xml configurations options for hello diagnostics extension.</span></span>
* <span data-ttu-id="9c4a9-135">Sanal makineler için tooenable hello tanılama uzantısını nasıl görürüm toolearn [izleme ve tanılama Azure Resource Manager şablonu kullanarak bir Windows sanal makine oluşturma](../virtual-machines/windows/extensions-diagnostics-template.md)</span><span class="sxs-lookup"><span data-stu-id="9c4a9-135">toolearn how tooenable hello diagnostics extension for Virtual Machines, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md)</span></span>
