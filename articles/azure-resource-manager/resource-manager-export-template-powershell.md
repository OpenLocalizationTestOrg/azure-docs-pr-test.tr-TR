---
title: "Azure PowerShell ile aaaExport Resource Manager şablonu | Microsoft Docs"
description: "Azure Resource Manager ve Azure PowerShell tooexport bir kaynak grubundan bir şablon kullanın."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 9a239b7bce8209326c0e267a4d3d69f7014bdaed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-powershell"></a>PowerShell ile Azure Resource Manager şablonları dışarı aktarma

Resource Manager tooexport, aboneliğinizdeki mevcut kaynaklardan bir Resource Manager şablonu sağlar. Bu oluşturulan şablonu toolearn hello şablon söz dizimi veya tooautomate hello çözümünüzün yeniden dağıtımını gerektiği gibi çözümünüzü hakkında kullanabilirsiniz.

Bir şablon iki farklı şekilde tooexport olduğunu önemli toonote şöyledir:

* Bir dağıtım için kullanılan hello gerçek şablonu dışarı aktarabilirsiniz. Merhaba özgün şablonda tam olarak göründüğü gibi hello dışarı aktarılan şablonu tüm hello parametreler ve değişkenler içerir. Bu yaklaşım, tooretrieve şablon gerektiğinde faydalıdır.
* Merhaba hello kaynak grubunun geçerli durumunu temsil eden bir şablonu dışarı aktarabilirsiniz. Merhaba dışarı aktarılan şablon dağıtımı için kullanılan herhangi bir şablonu dayanmıyor. Bunun yerine, hello kaynak grubunun bir anlık görüntüdür bir şablon oluşturur. Merhaba dışarı aktarılan şablon birçok sabit kodlu değer ve normalde tanımlayacağınız kadar fazla büyük olasılıkla parametre vardır. Bu yaklaşım, hello kaynak grubu değiştirdiniz. yararlıdır. Şimdi, şablon olarak toocapture hello kaynak grubu gerekir.

Bu konuda, iki yaklaşım ortaya koyulmaktadır.

## <a name="deploy-a-solution"></a>Bir çözüm dağıtma

bir şablonu dışarı aktarmak için iki tooillustrate yaklaşıyor, bir çözüm tooyour abonelik dağıtarak başlayalım. Aboneliğinizi tooexport istediğiniz bir kaynak grubu zaten varsa, bu çözüm toodeploy sahip değil. Ancak, bu makalenin sonraki bölümlerinde hello toohello şablonu bu çözüm için ifade eder. Merhaba örnek betik, bir depolama hesabı dağıtır.

```powershell
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -DeploymentName NewStorage
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
```  

## <a name="save-template-from-deployment-history"></a>Şablonu dağıtım geçmişinden Kaydet

Hello kullanarak bir şablonu dağıtım geçmişinden alabilirsiniz [Kaydet AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) komutu. daha önce dağıttığınız örnek kaydeder hello şablonu aşağıdaki hello:

```powershell
Save-AzureRmResourceGroupDeploymentTemplate -ResourceGroupName ExampleGroup -DeploymentName NewStorage
```

Hello şablon başlangıç konumunu döndürür.

```powershell
Path
----
C:\Users\exampleuser\NewStorage.json
```

Merhaba dosyasını açın ve dağıtımı için kullanılan hello tam şablonu olduğuna dikkat edin. Merhaba parametreleri ve değişkenleri hello şablonunu github'dan eşleşir. Bu şablonu yeniden dağıtabilirsiniz.

## <a name="export-resource-group-as-template"></a>Kaynak grubunu şablon olarak dışarı aktarma

Bir şablon hello dağıtım geçmişinden almanın yerine hello kullanarak hello kaynak grubunun geçerli durumunu temsil eden bir şablonu alabilir [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) komutu. Birçok değişiklikleri tooyour kaynak grubu yaptığınız ve varolan bir şablonu tüm hello değişiklikleri temsil ettiğinde bu komutu kullanın.

```powershell
Export-AzureRmResourceGroup -ResourceGroupName ExampleGroup
```

Hello şablon başlangıç konumunu döndürür.

```powershell
Path
----
C:\Users\exampleuser\ExampleGroup.json
```

Merhaba dosyasını açın ve GitHub hello şablonunda farklı olduğuna dikkat edin. Farklı parametreler ve değişken vardır. Merhaba depolama SKU ve konumu sabit kodlanmış toovalues önemlidir. Hello aşağıdaki örnekte gösterir hello dışarı aktarılan şablonu, ancak biraz farklı parametre adı şablonunuzu vardır:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccounts_nf3mvst4nqb36standardsa_name": {
      "defaultValue": null,
      "type": "String"
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[parameters('storageAccounts_nf3mvst4nqb36standardsa_name')]",
      "apiVersion": "2016-01-01",
      "location": "southcentralus",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

Bu şablonu yeniden dağıtabilirsiniz, ancak tahmin hello depolama hesabı için benzersiz bir ad gerektirir. Merhaba, parametre adını biraz farklıdır.

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -TemplateFile C:\Users\exampleuser\ExampleGroup.json `
  -storageAccounts_nf3mvst4nqb36standardsa_name tfnewstorage0501
```

## <a name="customize-exported-template"></a>Dışarı aktarılan şablonu özelleştirme

Bu şablon toomake değiştirebilir, daha kolay toouse ve daha esnektir. Daha fazla konumları, değişiklik hello konum özelliği toouse tooallow hello kaynak grubu ile aynı konumda hello:

```json
"location": "[resourceGroup().location]",
```

tooavoid tooguess Kaldır hello parametresi hello depolama hesabı adı için depolama hesabı için bir uniques adına sahip. Bir depolama alanı adı soneki ve depolama SKU için bir parametre ekleyin:

```json
"parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
},
```

Hello depolama hesabı adı hello uniqueString işleviyle oluşturan bir değişkeni ekleyin:

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

Merhaba hello depolama hesabı toohello değişkeninin adını ayarlayın:

```json
"name": "[variables('storageAccountName')]",
```

Merhaba SKU toohello parametresini ayarlayın:

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

Şablonunuz şimdi şuna benzer görünmelidir:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), parameters('storageSuffix'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "[parameters('storageAccountType')]",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

Merhaba değiştirilmiş şablonunu yeniden dağıtın.

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba portal tooexport bir şablon kullanma hakkında daha fazla bilgi için bkz: [mevcut kaynaklardan Azure Resource Manager şablonunu dışarı aktarma](resource-manager-export-template.md).
* Şablon toodefine parametrelerinde bkz [şablonları yazma](resource-group-authoring-templates.md#parameters).
* Genel dağıtım hatalarını giderme ipuçları için bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).
