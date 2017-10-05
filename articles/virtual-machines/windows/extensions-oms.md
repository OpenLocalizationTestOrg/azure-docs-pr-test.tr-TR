---
title: "Windows için OMS Azure sanal makine uzantısı | Microsoft Docs"
description: "OMS Aracısı'nı kullanarak bir sanal makine uzantısı Windows sanal makine dağıtın."
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
ms.openlocfilehash: d933f488fdda0c1d37892be65f2712cf0eb5694e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a><span data-ttu-id="ca75c-103">Windows için OMS sanal makine uzantısı</span><span class="sxs-lookup"><span data-stu-id="ca75c-103">OMS virtual machine extension for Windows</span></span>

<span data-ttu-id="ca75c-104">Operations Management Suite (OMS) bulut izleme, uyarma ve uyarı düzeltme özellikleri sağlar ve şirket içi varlıklar.</span><span class="sxs-lookup"><span data-stu-id="ca75c-104">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="ca75c-105">Windows için OMS Aracısı sanal makine uzantısı yayımlanan ve Microsoft tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="ca75c-105">The OMS Agent virtual machine extension for Windows is published and supported by Microsoft.</span></span> <span data-ttu-id="ca75c-106">Uzantı Azure sanal makinelerde OMS Aracısı'nı yükler ve sanal makineleri olan bir OMS çalışma kaydeder.</span><span class="sxs-lookup"><span data-stu-id="ca75c-106">The extension installs the OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="ca75c-107">Bu belge, desteklenen platformlar, yapılandırmaları ve Windows için OMS sanal makine uzantısı için dağıtım seçeneklerini ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="ca75c-107">This document details the supported platforms, configurations, and deployment options for the OMS virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca75c-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ca75c-108">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="ca75c-109">İşletim sistemi</span><span class="sxs-lookup"><span data-stu-id="ca75c-109">Operating system</span></span>
<span data-ttu-id="ca75c-110">Windows, Windows Server 2008 R2 karşı çalıştırılabilir için OMS aracısının uzantısı 2012, 2012 R2 ve 2016 serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="ca75c-110">The OMS Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="ca75c-111">İnternet bağlantısı</span><span class="sxs-lookup"><span data-stu-id="ca75c-111">Internet connectivity</span></span>
<span data-ttu-id="ca75c-112">Windows için OMS aracısının uzantısı hedef sanal makine internet'e bağlı olduğunu gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ca75c-112">The OMS Agent extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="ca75c-113">Uzantı Şeması</span><span class="sxs-lookup"><span data-stu-id="ca75c-113">Extension schema</span></span>

<span data-ttu-id="ca75c-114">Aşağıdaki JSON şeması OMS Aracısı uzantısı gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca75c-114">The following JSON shows the schema for the OMS Agent extension.</span></span> <span data-ttu-id="ca75c-115">Uzantı çalışma alanı kimliği ve hedef OMS çalışma alanından bir çalışma alanı anahtarı gerektirir, bu OMS Portalı'nda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="ca75c-115">The extension requires the workspace Id and workspace key from the target OMS workspace, these can be found in the OMS portal.</span></span> <span data-ttu-id="ca75c-116">Çalışma alanı anahtarı hassas verileri olarak değerlendirilmesi için bir korumalı ayarı yapılandırmasında depolanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca75c-116">Because the workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="ca75c-117">Azure VM uzantısının korumalı ayarı veri şifrelenir ve yalnızca hedef sanal makineye şifresi.</span><span class="sxs-lookup"><span data-stu-id="ca75c-117">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span> <span data-ttu-id="ca75c-118">Unutmayın **Workspaceıd** ve **workspaceKey** büyük küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="ca75c-118">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

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
### <a name="property-values"></a><span data-ttu-id="ca75c-119">Özellik değerleri</span><span class="sxs-lookup"><span data-stu-id="ca75c-119">Property values</span></span>

| <span data-ttu-id="ca75c-120">Ad</span><span class="sxs-lookup"><span data-stu-id="ca75c-120">Name</span></span> | <span data-ttu-id="ca75c-121">Değer / örnek</span><span class="sxs-lookup"><span data-stu-id="ca75c-121">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="ca75c-122">apiVersion</span><span class="sxs-lookup"><span data-stu-id="ca75c-122">apiVersion</span></span> | <span data-ttu-id="ca75c-123">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="ca75c-123">2015-06-15</span></span> |
| <span data-ttu-id="ca75c-124">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="ca75c-124">publisher</span></span> | <span data-ttu-id="ca75c-125">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="ca75c-125">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="ca75c-126">type</span><span class="sxs-lookup"><span data-stu-id="ca75c-126">type</span></span> | <span data-ttu-id="ca75c-127">MicrosoftMonitoringAgent</span><span class="sxs-lookup"><span data-stu-id="ca75c-127">MicrosoftMonitoringAgent</span></span> |
| <span data-ttu-id="ca75c-128">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="ca75c-128">typeHandlerVersion</span></span> | <span data-ttu-id="ca75c-129">1.0</span><span class="sxs-lookup"><span data-stu-id="ca75c-129">1.0</span></span> |
| <span data-ttu-id="ca75c-130">Workspaceıd (örneğin)</span><span class="sxs-lookup"><span data-stu-id="ca75c-130">workspaceId (e.g)</span></span> | <span data-ttu-id="ca75c-131">6f680a37-00c6-41C7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="ca75c-131">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="ca75c-132">workspaceKey (örneğin)</span><span class="sxs-lookup"><span data-stu-id="ca75c-132">workspaceKey (e.g)</span></span> | <span data-ttu-id="ca75c-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI + rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ ==</span><span class="sxs-lookup"><span data-stu-id="ca75c-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="ca75c-134">Şablon dağıtımı</span><span class="sxs-lookup"><span data-stu-id="ca75c-134">Template deployment</span></span>

<span data-ttu-id="ca75c-135">Azure VM uzantıları, Azure Resource Manager şablonları ile dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="ca75c-135">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="ca75c-136">Önceki bölümde ayrıntılı JSON şeması bir Azure Resource Manager şablonu OMS Aracısı uzantısı bir Azure Resource Manager şablon dağıtımı sırasında çalıştırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ca75c-136">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the OMS Agent extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="ca75c-137">OMS Aracısı VM uzantısı içeren bir örnek şablonu bulunabilir [Azure hızlı başlangıç Galerisi](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="ca75c-137">A sample template that includes the OMS Agent VM extension can be found on the [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span></span> 

<span data-ttu-id="ca75c-138">Bir sanal makine uzantısı için JSON içinde sanal makine kaynağı iç içe geçmiş veya kök veya Resource Manager JSON şablonu en üst düzeyinde yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ca75c-138">The JSON for a virtual machine extension can be nested inside the virtual machine resource, or placed at the root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="ca75c-139">JSON yerleşimini kaynak adı ve türü değeri etkiler.</span><span class="sxs-lookup"><span data-stu-id="ca75c-139">The placement of the JSON affects the value of the resource name and type.</span></span> <span data-ttu-id="ca75c-140">Daha fazla bilgi için bkz: [Ayarla alt kaynakları için ad ve tür](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="ca75c-140">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="ca75c-141">Aşağıdaki örnek, OMS uzantısı içinde sanal makine kaynağı iç içe geçmiş varsayar.</span><span class="sxs-lookup"><span data-stu-id="ca75c-141">The following example assumes the OMS extension is nested inside the virtual machine resource.</span></span> <span data-ttu-id="ca75c-142">Uzantı kaynak iç içe geçirme sırasında JSON yerleştirilir `"resources": []` sanal makinenin nesnesi.</span><span class="sxs-lookup"><span data-stu-id="ca75c-142">When nesting the extension resource, the JSON is placed in the `"resources": []` object of the virtual machine.</span></span>


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

<span data-ttu-id="ca75c-143">JSON uzantısı şablon kökünde yerleştirirken, kaynak adı üst sanal makine için referans içeriyor ve iç içe geçmiş yapılandırma türü yansıtır.</span><span class="sxs-lookup"><span data-stu-id="ca75c-143">When placing the extension JSON at the root of the template, the resource name includes a reference to the parent virtual machine, and the type reflects the nested configuration.</span></span> 

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

## <a name="powershell-deployment"></a><span data-ttu-id="ca75c-144">PowerShell dağıtım</span><span class="sxs-lookup"><span data-stu-id="ca75c-144">PowerShell deployment</span></span>

<span data-ttu-id="ca75c-145">`Set-AzureRmVMExtension` Komutu, OMS Aracısı sanal makine uzantısı olan bir sanal makineyi dağıtmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ca75c-145">The `Set-AzureRmVMExtension` command can be used to deploy the OMS Agent virtual machine extension to an existing virtual machine.</span></span> <span data-ttu-id="ca75c-146">Komutu çalıştırmadan önce genel ve özel yapılandırmaları bir PowerShell karma tablosunda depolanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca75c-146">Before running the command, the public and private configurations need to be stored in a PowerShell hash table.</span></span> 

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

## <a name="troubleshoot-and-support"></a><span data-ttu-id="ca75c-147">Sorun giderme ve Destek</span><span class="sxs-lookup"><span data-stu-id="ca75c-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="ca75c-148">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="ca75c-148">Troubleshoot</span></span>

<span data-ttu-id="ca75c-149">Veri uzantısı dağıtımları durumuyla ilgili Azure portalından ve Azure PowerShell modülü kullanılarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="ca75c-149">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="ca75c-150">İçin belirli bir VM uzantıları dağıtım durumunu görmek için Azure PowerShell modülünü kullanarak şu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ca75c-150">To see the deployment state of extensions for a given VM, run the following command using the Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="ca75c-151">Uzantı yürütme çıktısı aşağıdaki dizinde bulunan dosyalara kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="ca75c-151">Extension execution output is logged to files found in the following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a><span data-ttu-id="ca75c-152">Destek</span><span class="sxs-lookup"><span data-stu-id="ca75c-152">Support</span></span>

<span data-ttu-id="ca75c-153">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, üzerinde Azure uzmanlar başvurabilirsiniz [MSDN Azure ve yığın taşması forumları](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="ca75c-153">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="ca75c-154">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="ca75c-154">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="ca75c-155">Git [Azure Destek sitesi](https://azure.microsoft.com/en-us/support/options/) ve Get destek seçin.</span><span class="sxs-lookup"><span data-stu-id="ca75c-155">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="ca75c-156">Azure desteği hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="ca75c-156">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
