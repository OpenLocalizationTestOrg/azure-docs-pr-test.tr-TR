---
title: "aaaDeploy Azure kaynaklarını toomultiple kaynak grupları | Microsoft Docs"
description: "Bir Azure kaynak birden çok tootarget dağıtımı sırasında grup nasıl gösterir."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: tomfitz
ms.openlocfilehash: 93a39a26e0ca18dfcb5c6e8de95c38a64186d6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-resources-toomore-than-one-resource-group"></a>Bir kaynak grubundan Azure kaynaklarını toomore dağıtma

Genellikle, şablon tooa tek kaynak grubunuzdaki tüm hello kaynakları dağıtın. Ancak, burada toodeploy bir kaynak kümesi birlikte istiyor ancak farklı kaynak gruplarına yerleştirmeyi senaryo vardır. Örneğin, Azure Site Recovery tooa ayrı kaynak grubunu ve konumu için toodeploy hello yedekleme sanal makine isteyebilirsiniz. Resource Manager iç içe geçmiş toouse şablonları tootarget farklı kaynak grupları hello üst şablonu için kullanılan hello kaynak grubundan sağlar.

Merhaba kaynak hello yaşam döngüsü kapsayıcı Merhaba uygulaması için ve kaynağı kendi koleksiyonunu grubudur. Hello şablon dışında hello kaynak grubu oluşturun ve dağıtım sırasında hello kaynak grubu tootarget belirtin. Bir giriş tooresource grupları için bkz: [Azure Resource Manager'a genel bakış](resource-group-overview.md).

## <a name="example-template"></a>Örnek şablon

farklı bir kaynak tootarget, dağıtım sırasında bir iç içe ya da bağlantılı şablonu kullanmanız gerekir. Merhaba `Microsoft.Resources/deployments` kaynak türü sağlayan bir `resourceGroup` farklı bir kaynak grubu hello için toospecify etkinleştirir parametresi, dağıtım iç içe geçmiş. Tüm hello kaynak grupları hello dağıtım çalıştırmadan önce mevcut olması gerekir. Merhaba aşağıdaki örnek dağıtır - bir dağıtım sırasında belirtilen hello kaynak grubunda iki depolama hesabı ve diğeri adlı bir kaynak grubunda `crossResourceGroupDeployment`:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "StorageAccountName1": {
            "type": "string"
        },
        "StorageAccountName2": {
            "type": "string"
        }
    },
    "variables": {},
    "resources": [
        {
            "apiVersion": "2017-05-10",
            "name": "nestedTemplate",
            "type": "Microsoft.Resources/deployments",
            "resourceGroup": "crossResourceGroupDeployment",
            "properties": {
                "mode": "Incremental",
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {},
                    "variables": {},
                    "resources": [
                        {
                            "type": "Microsoft.Storage/storageAccounts",
                            "name": "[parameters('StorageAccountName2')]",
                            "apiVersion": "2015-06-15",
                            "location": "West US",
                            "properties": {
                                "accountType": "Standard_LRS"
                            }
                        }
                    ]
                },
                "parameters": {}
            }
        },
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('StorageAccountName1')]",
            "apiVersion": "2015-06-15",
            "location": "West US",
            "properties": {
                "accountType": "Standard_LRS"
            }
        }
    ]
}
```

Ayarlarsanız `resourceGroup` var olmayan bir kaynak grubu adını toohello, hello dağıtımı başarısız olur. İçin bir değer belirtmezseniz, `resourceGroup`, Resource Manager hello üst kaynak grubu kullanır.  

## <a name="deploy-hello-template"></a>Merhaba şablonu dağıtma

toodeploy hello örnek şablon hello portalı, Azure PowerShell veya Azure CLI kullanabilirsiniz. Azure PowerShell veya Azure CLI için May 2017 veya sonraki bir sürümü kullanmanız gerekir. Merhaba örnekler varsayar, kaydettiğiniz hello şablonu yerel olarak adlı bir dosya **crossrgdeployment.json**.

PowerShell için:

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

Azure CLI için:

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

Dağıtım tamamlandıktan sonra iki kaynak grubu bakın. Her kaynak grubu bir depolama hesabını içerir.

## <a name="use-resourcegroup-function"></a>Kullanım resourceGroup() işlevi

İçin çapraz kaynak grubu dağıtımı hello [resouceGroup() işlevi](resource-group-template-functions-resource.md#resourcegroup) çözümler farklı dayalı hello iç içe geçmiş şablonu nasıl belirtin. 

Başka bir şablonu içindeki bir şablon eklemek, hello iç içe geçmiş şablonunda resouceGroup() toohello üst kaynak grubu çözümler. Katıştırılmış bir şablonu hello aşağıdaki biçimi kullanır:

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers tooparent resource group
    }
}
```

Tooa ayrı bir şablon bağlantı varsa, hello bağlantılı şablonunda resouceGroup() toohello iç içe kaynak grubu çözümler. Bağlantılı bir şablon biçimini izleyen hello kullanır:

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers toolinked resource group
    }
}
```

## <a name="next-steps"></a>Sonraki adımlar

* şablonunuzu toodefine parametrelerinde nasıl görürüm toounderstand [anlamak hello yapısı ve Azure Resource Manager şablonları sözdizimini](resource-group-authoring-templates.md).
* Genel dağıtım hatalarını giderme ipuçları için bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).
* Bir SAS belirteci gerektiren şablonu dağıtma hakkında daha fazla bilgi için bkz: [dağıtma özel şablonu SAS belirteci ile](resource-manager-powershell-sas-token.md).
