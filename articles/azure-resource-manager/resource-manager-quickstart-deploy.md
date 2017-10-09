---
title: "aaaDeploy kaynakları tooAzure | Microsoft Docs"
description: "Azure PowerShell veya Azure CLI toodeploy kaynakları tooAzure kullanın. Merhaba kaynaklar bir Resource Manager şablonunda tanımlanır."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/16/2017
ms.author: tomfitz
ms.openlocfilehash: 0cd3f8ad45af1fb85c78899b56f6807d00b859f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-tooazure"></a>Kaynakları tooAzure dağıtma

Bu konuda gösterilmektedir nasıl toodeploy kaynakları tooyour Azure aboneliği. Azure PowerShell veya Azure CLI toodeploy Merhaba, çözümünüz için altyapıyı tanımlayan Resource Manager şablonu kullanabilirsiniz.

Bir giriş tooconcepts Kaynak Yöneticisi'nin için bkz: [Azure Resource Manager'a genel bakış](resource-group-overview.md).

## <a name="steps-for-deployment"></a>Dağıtım adımları

Bu konu hello dağıttığınız varsayar [Örnek Depolama şablondaki](#example-storage-template) bu konuda. Farklı bir şablon kullanabilirsiniz, ancak geçirdiğiniz hello parametreleri bu konuda gösterilen değerinden farklı.

Bir şablonu oluşturduktan sonra şablonunuzu dağıtmak için hello genel adımlar şunlardır:

1. Tooyour hesabında oturum
2. Merhaba abonelik toouse (yalnızca birden çok aboneliğiniz varsa ve toouse hello varsayılan abonelik olmayan bir istiyorsanız gerekli) seçin
3. Kaynak grubu oluşturma
4. Merhaba şablonu dağıtma
5. Dağıtım durumunuzu denetleme

Merhaba aşağıdaki bölümlerde tooperform olanlar nasıl adımları ile göster [PowerShell](#powershell) veya [Azure CLI](#azure-cli).

## <a name="powershell"></a>PowerShell

1. Azure PowerShell tooinstall bkz [Azure PowerShell cmdlet'leri kullanmaya başlama](/powershell/azure/overview).

2. tooquickly dağıtımına başlayın, hello aşağıdaki cmdlet'leri kullanın:

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  Merhaba `Set-AzureRmContext` cmdlet varsayılan aboneliğinizin dışında toouse bir abonelik isterseniz, yalnızca gerekli. Tüm aboneliklerinizi ve kullanıcıların kimlikleri toosee kullanın:

  ```powershell
  Get-AzureRmSubscription
  ```

3. Merhaba dağıtım birkaç dakika toocomplete alabilir. Tamamlandığında aşağıdakine benzer bir ileti görürsünüz:

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. kaynak grubu ve depolama hesabı olan toosee tooyour abonelik, kullanım dağıtılan:

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. Şablon dağıtırken, şablon parametrelerini PowerShell parametreleri olarak belirtebilirsiniz. Hello varsayılan değerleri hello şablonda kullanılan şekilde hello daha önceki örnekteki hiçbir şablon parametreleri içermiyordu. toodeploy başka bir depolama hesabı ve hello depolama adı öneki ve hello depolama hesabı SKU, kullanımı için parametre değerlerini sağlayın:

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  Artık kaynak grubunuzda iki depolama hesabı bulunmaktadır. 

## <a name="azure-cli"></a>Azure CLI

1. Azure CLI tooinstall bkz [Azure CLI 2.0 yükleme](/cli/azure/install-az-cli2).

2. tooquickly dağıtımına başlayın, hello aşağıdaki komutları kullanın:

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  Merhaba `az account set` komutu varsayılan aboneliğinizin dışında toouse bir abonelik isterseniz, yalnızca gerekli. Tüm aboneliklerinizi ve kullanıcıların kimlikleri toosee kullanın:

  ```azurecli
  az account list
  ```

3. Merhaba dağıtım birkaç dakika toocomplete alabilir. Tamamlandığında aşağıdakine benzer bir ileti görürsünüz:

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. kaynak grubu ve depolama hesabı olan toosee tooyour abonelik, kullanım dağıtılan:

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. Şablon dağıtırken, şablon parametrelerini PowerShell parametreleri olarak belirtebilirsiniz. Hello varsayılan değerleri hello şablonda kullanılan şekilde hello daha önceki örnekteki hiçbir şablon parametreleri içermiyordu. toodeploy başka bir depolama hesabı ve hello depolama adı öneki ve hello depolama hesabı SKU, kullanımı için parametre değerlerini sağlayın:

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  Artık kaynak grubunuzda iki depolama hesabı bulunmaktadır. 

## <a name="example-storage-template"></a>Örnek depolama şablonu

Örnek şablon toodeploy bir depolama hesabı tooyour aboneliği aşağıdaki hello kullan:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name."
      }
    },
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    }
  },
  "variables": {
    "storageName": "[concat(parameters('storageNamePrefix'), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-05-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {  }
}
```

## <a name="next-steps"></a>Sonraki adımlar

* PowerShell toodeploy şablonları kullanma hakkında ayrıntılı bilgi için bkz: [Resource Manager şablonları ve Azure PowerShell ile kaynakları dağıtmak](/azure/azure-resource-manager/resource-group-template-deploy).
* Azure CLI toodeploy şablonları kullanma hakkında ayrıntılı bilgi için bkz: [Resource Manager şablonları ve Azure CLI kaynaklarla dağıtmak](/azure/azure-resource-manager/resource-group-template-deploy-cli).



