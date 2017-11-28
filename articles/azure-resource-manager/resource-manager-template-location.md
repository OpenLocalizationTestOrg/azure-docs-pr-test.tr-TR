---
title: "Şablon aaaAzure kaynak konumda | Microsoft Docs"
description: "Gösterir nasıl tooset bir Azure Resource Manager şablonu kaynak için bir konum"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: tomfitz
ms.openlocfilehash: f2ad6ca6ac5f34484a2e5e57dd8d67c77dacc41a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a><span data-ttu-id="8f9c0-103">Azure Resource Manager şablonları kaynak konumunu ayarla</span><span class="sxs-lookup"><span data-stu-id="8f9c0-103">Set resource location in Azure Resource Manager templates</span></span>
<span data-ttu-id="8f9c0-104">Bir şablon dağıtılırken, her kaynak için bir konum sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f9c0-104">When deploying a template, you must provide a location for each resource.</span></span> <span data-ttu-id="8f9c0-105">Bu konu, her kaynak için kullanılabilir tooyour abonelik olan toodetermine hello konumlarını nasıl yazın gösterir.</span><span class="sxs-lookup"><span data-stu-id="8f9c0-105">This topic shows how toodetermine hello locations that are available tooyour subscription for each resource type.</span></span>

## <a name="determine-supported-locations"></a><span data-ttu-id="8f9c0-106">Desteklenen konumlar belirler</span><span class="sxs-lookup"><span data-stu-id="8f9c0-106">Determine supported locations</span></span>

<span data-ttu-id="8f9c0-107">Her kaynak türü için desteklenen konumlardan tam bir listesi için bkz: [bölgeye göre ürünleri](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="8f9c0-107">For a complete list of supported locations for each resource type, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="8f9c0-108">Ancak, aboneliğinizi erişim tooall hello konumları bu listedeki sahip olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="8f9c0-108">However, your subscription might not have access tooall hello locations in that list.</span></span> <span data-ttu-id="8f9c0-109">toosee özelleştirilmiş kullanılabilir tooyour abonelik olan konumların listesini Azure PowerShell veya Azure CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="8f9c0-109">toosee a customized list of locations that are available tooyour subscription, use Azure PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="8f9c0-110">Merhaba aşağıdaki örnek PowerShell tooget hello konumlarını Merhaba kullanan `Microsoft.Web\sites` kaynak türü:</span><span class="sxs-lookup"><span data-stu-id="8f9c0-110">hello following example uses PowerShell tooget hello locations for hello `Microsoft.Web\sites` resource type:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="8f9c0-111">Merhaba aşağıdaki örnek Azure CLI 2.0 tooget hello konumlarını Merhaba kullanan `Microsoft.Web\sites` kaynak türü:</span><span class="sxs-lookup"><span data-stu-id="8f9c0-111">hello following example uses Azure CLI 2.0 tooget hello locations for hello `Microsoft.Web\sites` resource type:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a><span data-ttu-id="8f9c0-112">Şablondaki konum ayarlama</span><span class="sxs-lookup"><span data-stu-id="8f9c0-112">Set location in template</span></span>

<span data-ttu-id="8f9c0-113">Kaynaklarınız için desteklenen hello konumlarını belirlendikten sonra tooset bu konuma şablonunuzda gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f9c0-113">After determining hello supported locations for your resources, you need tooset that location in your template.</span></span> <span data-ttu-id="8f9c0-114">Bu değeri olan bir kaynak grubu hello kaynak türlerini destekleyen bir konumda toocreate en kolay yolu tooset hello ve her konumun çok ayarlayın`[resourceGroup().location]`.</span><span class="sxs-lookup"><span data-stu-id="8f9c0-114">hello easiest way tooset this value is toocreate a resource group in a location that supports hello resource types, and set each location too`[resourceGroup().location]`.</span></span> <span data-ttu-id="8f9c0-115">Hello şablonu tooresource grupları farklı konumlarda dağıtmanız ve hello şablon veya parametre değerleri değiştirin değil.</span><span class="sxs-lookup"><span data-stu-id="8f9c0-115">You can redeploy hello template tooresource groups in different locations, and not change any values in hello template or parameters.</span></span> 

<span data-ttu-id="8f9c0-116">Merhaba aşağıdaki örnekte gösterilir dağıtılan toohello olan bir depolama hesabını hello kaynak grubu ile aynı konumda:</span><span class="sxs-lookup"><span data-stu-id="8f9c0-116">hello following example shows a storage account that is deployed toohello same location as hello resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
      "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

<span data-ttu-id="8f9c0-117">Şablonunuzda toohardcode hello konumu gerekiyorsa, desteklenen hello bölgelerinden hello adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="8f9c0-117">If you need toohardcode hello location in your template, provide hello name of one of hello supported regions.</span></span> <span data-ttu-id="8f9c0-118">her zaman bir depolama hesabı tooNorth Orta ABD dağıtılan hello aşağıdaki örneğine gösterir:</span><span class="sxs-lookup"><span data-stu-id="8f9c0-118">hello following example shows a storage account that is always deployed tooNorth Central US:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storageloc', uniqueString(resourceGroup().id))]",
      "location": "North Central US",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="8f9c0-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8f9c0-119">Next steps</span></span>
* <span data-ttu-id="8f9c0-120">Nasıl hakkında öneriler için bkz: toocreate şablonları [en iyi uygulamalar Azure Resource Manager şablonları oluşturmak için](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="8f9c0-120">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

