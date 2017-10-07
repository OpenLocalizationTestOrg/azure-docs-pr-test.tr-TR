---
title: "Windows için Azure sanal makine uzantısı aaaOMS | Microsoft Docs"
description: "Merhaba OMS Aracısı'nı kullanarak bir sanal makine uzantısı Windows sanal makine dağıtın."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: feae6176-2373-4034-b5d9-a32c6b4e1f10
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: nepeters
ms.openlocfilehash: 3000f66c0acdec1d1fad2125b8c6b72a92b1ec92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a><span data-ttu-id="9a708-103">Windows için OMS sanal makine uzantısı</span><span class="sxs-lookup"><span data-stu-id="9a708-103">OMS virtual machine extension for Windows</span></span>

<span data-ttu-id="9a708-104">Operations Management Suite (OMS) bulut izleme, uyarma ve uyarı düzeltme özellikleri sağlar ve şirket içi varlıklar.</span><span class="sxs-lookup"><span data-stu-id="9a708-104">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="9a708-105">Merhaba OMS Aracısı sanal makine uzantısı Windows için yayımlanan ve Microsoft tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="9a708-105">hello OMS Agent virtual machine extension for Windows is published and supported by Microsoft.</span></span> <span data-ttu-id="9a708-106">Merhaba uzantısı Azure sanal makinelerde hello OMS Aracısı'nı yükler ve sanal makineleri olan bir OMS çalışma kaydeder.</span><span class="sxs-lookup"><span data-stu-id="9a708-106">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="9a708-107">Bu belge ayrıntıları hello platformları, yapılandırmaları ve dağıtım seçenekleri için Windows hello OMS sanal makine uzantısı için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="9a708-107">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a708-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9a708-108">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="9a708-109">İşletim sistemi</span><span class="sxs-lookup"><span data-stu-id="9a708-109">Operating system</span></span>
<span data-ttu-id="9a708-110">Windows, Windows Server 2008 R2 karşı çalıştırılabilir için hello OMS Aracısı uzantısı 2012, 2012 R2 ve 2016 serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="9a708-110">hello OMS Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="9a708-111">İnternet bağlantısı</span><span class="sxs-lookup"><span data-stu-id="9a708-111">Internet connectivity</span></span>
<span data-ttu-id="9a708-112">OMS Aracısı uzantısı için Windows Hello gerektirir hello hedef sanal makinenin bağlı toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="9a708-112">hello OMS Agent extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="9a708-113">Uzantı Şeması</span><span class="sxs-lookup"><span data-stu-id="9a708-113">Extension schema</span></span>

<span data-ttu-id="9a708-114">Merhaba aşağıdaki JSON hello OMS Aracısı uzantısı için hello şema gösterir.</span><span class="sxs-lookup"><span data-stu-id="9a708-114">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="9a708-115">Merhaba uzantısı hello hedef OMS çalışma alanından hello çalışma alanı kimliği ve çalışma alanı anahtarı gerekiyor, bunlar hello OMS portalında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="9a708-115">hello extension requires hello workspace Id and workspace key from hello target OMS workspace, these can be found in hello OMS portal.</span></span> <span data-ttu-id="9a708-116">Merhaba çalışma alanı anahtarı hassas verileri olarak değerlendirilmesi için bir korumalı ayarı yapılandırmasında depolanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a708-116">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="9a708-117">Azure VM uzantısının korumalı ayarı veri şifrelenir ve yalnızca hello hedef sanal makineye şifresi.</span><span class="sxs-lookup"><span data-stu-id="9a708-117">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="9a708-118">Unutmayın **Workspaceıd** ve **workspaceKey** büyük küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="9a708-118">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```
### <a name="property-values"></a><span data-ttu-id="9a708-119">Özellik değerleri</span><span class="sxs-lookup"><span data-stu-id="9a708-119">Property values</span></span>

| <span data-ttu-id="9a708-120">Ad</span><span class="sxs-lookup"><span data-stu-id="9a708-120">Name</span></span> | <span data-ttu-id="9a708-121">Değer / örnek</span><span class="sxs-lookup"><span data-stu-id="9a708-121">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="9a708-122">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9a708-122">apiVersion</span></span> | <span data-ttu-id="9a708-123">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="9a708-123">2015-06-15</span></span> |
| <span data-ttu-id="9a708-124">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="9a708-124">publisher</span></span> | <span data-ttu-id="9a708-125">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="9a708-125">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="9a708-126">type</span><span class="sxs-lookup"><span data-stu-id="9a708-126">type</span></span> | <span data-ttu-id="9a708-127">MicrosoftMonitoringAgent</span><span class="sxs-lookup"><span data-stu-id="9a708-127">MicrosoftMonitoringAgent</span></span> |
| <span data-ttu-id="9a708-128">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="9a708-128">typeHandlerVersion</span></span> | <span data-ttu-id="9a708-129">1.0</span><span class="sxs-lookup"><span data-stu-id="9a708-129">1.0</span></span> |
| <span data-ttu-id="9a708-130">Workspaceıd (örneğin)</span><span class="sxs-lookup"><span data-stu-id="9a708-130">workspaceId (e.g)</span></span> | <span data-ttu-id="9a708-131">6f680a37-00c6-41C7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="9a708-131">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="9a708-132">workspaceKey (örneğin)</span><span class="sxs-lookup"><span data-stu-id="9a708-132">workspaceKey (e.g)</span></span> | <span data-ttu-id="9a708-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI + rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ ==</span><span class="sxs-lookup"><span data-stu-id="9a708-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="9a708-134">Şablon dağıtımı</span><span class="sxs-lookup"><span data-stu-id="9a708-134">Template deployment</span></span>

<span data-ttu-id="9a708-135">Azure VM uzantıları, Azure Resource Manager şablonları ile dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="9a708-135">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="9a708-136">Merhaba JSON şeması Hello önceki bölümde ayrıntılı bir Azure Resource Manager şablon dağıtımı sırasında bir Azure Resource Manager şablonu toorun hello OMS Aracısı uzantısı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9a708-136">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello OMS Agent extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="9a708-137">Merhaba OMS Aracısı VM uzantısı içeren bir örnek şablonu hello üzerinde bulunabilir [Azure hızlı başlangıç Galerisi](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="9a708-137">A sample template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span></span> 

<span data-ttu-id="9a708-138">Hello JSON bir sanal makine uzantısı hello sanal makine kaynağı içinde iç içe geçmiş veya hello kök veya Resource Manager JSON şablonu en üst düzeyinde yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9a708-138">hello JSON for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="9a708-139">Merhaba JSON Hello yerleşimini hello değeri hello kaynak adı ve türü etkiler.</span><span class="sxs-lookup"><span data-stu-id="9a708-139">hello placement of hello JSON affects hello value of hello resource name and type.</span></span> <span data-ttu-id="9a708-140">Daha fazla bilgi için bkz: [Ayarla alt kaynakları için ad ve tür](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="9a708-140">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="9a708-141">Merhaba aşağıdaki örneği hello OMS uzantısı hello sanal makine kaynağı içinde iç içe geçmiş varsayar.</span><span class="sxs-lookup"><span data-stu-id="9a708-141">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="9a708-142">Merhaba uzantısı kaynak iç içe geçirme sırasında hello JSON hello yerleştirilir `"resources": []` hello sanal makinenin nesnesi.</span><span class="sxs-lookup"><span data-stu-id="9a708-142">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>


```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

<span data-ttu-id="9a708-143">Merhaba uzantısı JSON hello hello şablon kökünde yerleştirirken başvuru toohello üst sanal makinesini hello kaynak adı içerir ve hello türü hello iç içe geçmiş yapılandırma yansıtır.</span><span class="sxs-lookup"><span data-stu-id="9a708-143">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span> 

```json
{
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "name": "<parentVmResource>/OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

## <a name="powershell-deployment"></a><span data-ttu-id="9a708-144">PowerShell dağıtım</span><span class="sxs-lookup"><span data-stu-id="9a708-144">PowerShell deployment</span></span>

<span data-ttu-id="9a708-145">Merhaba `Set-AzureRmVMExtension` komutu kullanılan toodeploy hello OMS Aracısı sanal makine uzantısı tooan varolan sanal makine olabilir.</span><span class="sxs-lookup"><span data-stu-id="9a708-145">hello `Set-AzureRmVMExtension` command can be used toodeploy hello OMS Agent virtual machine extension tooan existing virtual machine.</span></span> <span data-ttu-id="9a708-146">Hello komutu çalıştırmadan önce bir PowerShell karma tablosu toobe hello ortak ve özel yapılandırmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a708-146">Before running hello command, hello public and private configurations need toobe stored in a PowerShell hash table.</span></span> 

```powershell
$PublicSettings = @{"workspaceId" = "myWorkspaceId"}
$ProtectedSettings = @{"workspaceKey" = "myWorkspaceKey"}

Set-AzureRmVMExtension -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
    -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" `
    -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
    -ExtensionType "MicrosoftMonitoringAgent" `
    -TypeHandlerVersion 1.0 `
    -Settings $PublicSettings `
    -ProtectedSettings $ProtectedSettings `
    -Location WestUS ` 
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="9a708-147">Sorun giderme ve Destek</span><span class="sxs-lookup"><span data-stu-id="9a708-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="9a708-148">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="9a708-148">Troubleshoot</span></span>

<span data-ttu-id="9a708-149">Veri uzantısı dağıtımları hello durumuyla ilgili hello Azure portal ve hello Azure PowerShell modülü kullanılarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="9a708-149">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="9a708-150">Aşağıdaki komutu kullanarak çalışma hello belirli bir VM için uzantıların toosee hello dağıtım durumu hello Azure PowerShell modülü.</span><span class="sxs-lookup"><span data-stu-id="9a708-150">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="9a708-151">Uzantı yürütme hello bulunan oturum toofiles directory aşağıdaki çıktı:</span><span class="sxs-lookup"><span data-stu-id="9a708-151">Extension execution output is logged toofiles found in hello following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a><span data-ttu-id="9a708-152">Destek</span><span class="sxs-lookup"><span data-stu-id="9a708-152">Support</span></span>

<span data-ttu-id="9a708-153">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz hello Azure uzmanlarıyla hello [MSDN Azure ve yığın taşması forumları](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="9a708-153">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="9a708-154">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="9a708-154">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="9a708-155">Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/en-us/support/options/) ve Get destek seçin.</span><span class="sxs-lookup"><span data-stu-id="9a708-155">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="9a708-156">Hello Azure destek kullanma hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="9a708-156">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
