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
# <a name="set-resource-location-in-azure-resource-manager-templates"></a>Azure Resource Manager şablonları kaynak konumunu ayarla
Bir şablon dağıtılırken, her kaynak için bir konum sağlamanız gerekir. Bu konu, her kaynak için kullanılabilir tooyour abonelik olan toodetermine hello konumlarını nasıl yazın gösterir.

## <a name="determine-supported-locations"></a>Desteklenen konumlar belirler

Her kaynak türü için desteklenen konumlardan tam bir listesi için bkz: [bölgeye göre ürünleri](https://azure.microsoft.com/regions/services/). Ancak, aboneliğinizi erişim tooall hello konumları bu listedeki sahip olmayabilir. toosee özelleştirilmiş kullanılabilir tooyour abonelik olan konumların listesini Azure PowerShell veya Azure CLI kullanın. 

Merhaba aşağıdaki örnek PowerShell tooget hello konumlarını Merhaba kullanan `Microsoft.Web\sites` kaynak türü:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

Merhaba aşağıdaki örnek Azure CLI 2.0 tooget hello konumlarını Merhaba kullanan `Microsoft.Web\sites` kaynak türü:

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a>Şablondaki konum ayarlama

Kaynaklarınız için desteklenen hello konumlarını belirlendikten sonra tooset bu konuma şablonunuzda gerekir. Bu değeri olan bir kaynak grubu hello kaynak türlerini destekleyen bir konumda toocreate en kolay yolu tooset hello ve her konumun çok ayarlayın`[resourceGroup().location]`. Hello şablonu tooresource grupları farklı konumlarda dağıtmanız ve hello şablon veya parametre değerleri değiştirin değil. 

Merhaba aşağıdaki örnekte gösterilir dağıtılan toohello olan bir depolama hesabını hello kaynak grubu ile aynı konumda:

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

Şablonunuzda toohardcode hello konumu gerekiyorsa, desteklenen hello bölgelerinden hello adını sağlayın. her zaman bir depolama hesabı tooNorth Orta ABD dağıtılan hello aşağıdaki örneğine gösterir:

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

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl hakkında öneriler için bkz: toocreate şablonları [en iyi uygulamalar Azure Resource Manager şablonları oluşturmak için](resource-manager-template-best-practices.md).

