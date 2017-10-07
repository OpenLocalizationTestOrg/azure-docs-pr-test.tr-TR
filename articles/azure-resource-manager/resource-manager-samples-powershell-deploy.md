---
title: "PowerShell komut dosyası örneği - aaaAzure şablonu dağıtma | Microsoft Docs"
description: "Bir Azure Resource Manager şablonunu dağıtmak için örnek komut dosyası."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 536b8ccecad4ed8a4c4a4139c6bf4600e2eb9405
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-deployment---powershell-script"></a><span data-ttu-id="c0a63-103">Azure Resource Manager şablon dağıtımı - PowerShell Betiği</span><span class="sxs-lookup"><span data-stu-id="c0a63-103">Azure Resource Manager template deployment - PowerShell script</span></span>

<span data-ttu-id="c0a63-104">Bu komut dosyasını bir Resource Manager şablonu tooa kaynak grubu aboneliğinizde dağıtır.</span><span class="sxs-lookup"><span data-stu-id="c0a63-104">This script deploys a Resource Manager template tooa resource group in your subscription.</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c0a63-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="c0a63-105">Sample script</span></span>

```powershell
<#
 .SYNOPSIS
    Deploys a template tooAzure

 .DESCRIPTION
    Deploys an Azure Resource Manager template
#>

param (
    [Parameter(Mandatory)]
    #hello subscription id where hello template will be deployed.
    [string]$SubscriptionId,  

    [Parameter(Mandatory)]
    #hello resource group where hello template will be deployed. Can be hello name of an existing or a new resource group.
    [string]$ResourceGroupName, 

    #Optional, a resource group location. If specified, will try toocreate a new resource group in this location. If not specified, assumes resource group is existing.
    [string]$ResourceGroupLocation, 

    #hello deployment name.
    [Parameter(Mandatory)]
    [string]$DeploymentName,    

    #Path toohello template file. Defaults tootemplate.json.
    [string]$TemplateFilePath = "template.json",  

    #Path toohello parameters file. Defaults tooparameters.json. If file is not found, will prompt for parameter values based on template.
    [string]$ParametersFilePath = "parameters.json"
)

$ErrorActionPreference = "Stop"

# Login tooAzure and select subscription
Write-Output "Logging in"
Login-AzureRmAccount
Write-Output "Selecting subscription '$SubscriptionId'"
Select-AzureRmSubscription -SubscriptionID $SubscriptionId

# Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $ResourceGroupName -ErrorAction SilentlyContinue
if ( -not $ResourceGroup ) {
    Write-Output "Could not find resource group '$ResourceGroupName' - will create it"
    if ( -not $ResourceGroupLocation ) {
        $ResourceGroupLocation = Read-Host -Prompt 'Enter location for resource group'
    }
    Write-Output "Creating resource group '$ResourceGroupName' in location '$ResourceGroupLocation'"
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else {
    Write-Output "Using existing resource group '$ResourceGroupName'"
}

# Start hello deployment
Write-Output "Starting deployment"
if ( Test-Path $ParametersFilePath ) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath -TemplateParameterFile $ParametersFilePath
}
else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath
}
``` 

## <a name="clean-up-deployment"></a><span data-ttu-id="c0a63-106">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="c0a63-106">Clean up deployment</span></span> 

<span data-ttu-id="c0a63-107">Çalışma hello aşağıdaki tooremove hello kaynak grubunu ve tüm kaynaklarını komutu.</span><span class="sxs-lookup"><span data-stu-id="c0a63-107">Run hello following command tooremove hello resource group and all its resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c0a63-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="c0a63-108">Script explanation</span></span>

<span data-ttu-id="c0a63-109">Bu komut dosyası komutları toocreate hello dağıtım aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="c0a63-109">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="c0a63-110">Merhaba tablosundaki her öğesi toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="c0a63-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c0a63-111">Komut</span><span class="sxs-lookup"><span data-stu-id="c0a63-111">Command</span></span> | <span data-ttu-id="c0a63-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="c0a63-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c0a63-113">Register-AzureRmResourceProvider</span><span class="sxs-lookup"><span data-stu-id="c0a63-113">Register-AzureRmResourceProvider</span></span>](/powershell/module/azurerm.resources/register-azurermresourceprovider) | <span data-ttu-id="c0a63-114">Kaynak türleri dağıtılan tooyour abonelik olabilir bir kaynak sağlayıcısına kaydeder.</span><span class="sxs-lookup"><span data-stu-id="c0a63-114">Registers a resource provider so its resource types can be deployed tooyour subscription.</span></span>  |
| [<span data-ttu-id="c0a63-115">Get-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c0a63-115">Get-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | <span data-ttu-id="c0a63-116">Kaynak grupları alır.</span><span class="sxs-lookup"><span data-stu-id="c0a63-116">Gets resource groups.</span></span>  |
| [<span data-ttu-id="c0a63-117">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c0a63-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c0a63-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c0a63-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c0a63-119">Yeni-AzureRmResourceGroupDeployment</span><span class="sxs-lookup"><span data-stu-id="c0a63-119">New-AzureRmResourceGroupDeployment</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) | <span data-ttu-id="c0a63-120">Bir Azure dağıtım tooa kaynak grubu ekler.</span><span class="sxs-lookup"><span data-stu-id="c0a63-120">Adds an Azure deployment tooa resource group.</span></span>  |
| [<span data-ttu-id="c0a63-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c0a63-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="c0a63-122">Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır.</span><span class="sxs-lookup"><span data-stu-id="c0a63-122">Removes a resource group and all resources contained within.</span></span> |



## <a name="next-steps"></a><span data-ttu-id="c0a63-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c0a63-123">Next steps</span></span>
* <span data-ttu-id="c0a63-124">Bir giriş toodeploying şablonları için bkz: [Resource Manager şablonları ve Azure PowerShell ile kaynakları dağıtmak](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c0a63-124">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="c0a63-125">Bir SAS belirteci gerektiren şablonu dağıtma hakkında daha fazla bilgi için bkz: [dağıtma özel şablonu SAS belirteci ile](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="c0a63-125">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="c0a63-126">Şablon toodefine parametrelerinde bkz [şablonları yazma](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="c0a63-126">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="c0a63-127">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="c0a63-127">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

