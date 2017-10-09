---
title: "PowerShell ve şablon aaaDeploy kaynaklarla | Microsoft Docs"
description: "Azure Resource Manager ve Azure PowerShell toodeploy kaynakları tooAzure kullanın. Merhaba kaynaklar bir Resource Manager şablonunda tanımlanır."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 41506811ba3c2ea5df6313db70978ade50f71161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a>Kaynakları Resource Manager şablonları ve Azure PowerShell ile dağıtma

Bu konuda açıklanmaktadır nasıl toouse Azure PowerShell'i Resource Manager şablonları toodeploy ile kaynakları tooAzure. Dağıtma hello kavramları hakkında bilgi sahibi değilseniz ve Azure çözümlerinizi bkz [Azure Resource Manager'a genel bakış](resource-group-overview.md).

Merhaba Resource Manager şablonu ya da makinenizde yerel bir dosya ya da GitHub gibi bir havuzda bulunan dış dosyası dağıtabilirsiniz. Bu makalede dağıttığınız hello şablon hello kullanılabilir [örnek şablonu](#sample-template) bölümünde veya as [depolama hesabı şablonu github](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a>Yerel makinenizde bir şablondan dağıtma

Kaynakları tooAzure dağıtırken:

1. Azure hesabı tooyour içinde oturum
2. Dağıtılan hello kaynaklar için hello kapsayıcı görevi gören bir kaynak grubu oluşturun. Hello hello kaynak grubu adı yalnızca alfasayısal karakterler, nokta, alt çizgi, kısa çizgi ve parantez içerebilir. Too90 karakter olabilir. Bir nokta ile bitemez.
3. Merhaba kaynakları toocreate tanımlar toohello kaynak grubu hello şablonu dağıtma

Bir şablon toocustomize hello dağıtımını etkinleştirmek parametreleri içerebilir. Örneğin, belirli bir ortamda (örneğin, geliştirme, test ve üretim) için uyarlanabilir değerler sağlayabilirsiniz. Merhaba örnek şablonu hello depolama hesabı SKU için bir parametre tanımlar.

Aşağıdaki örnek hello bir kaynak grubu oluşturur ve yerel makinenize bir şablondan dağıtır:

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

Merhaba dağıtım birkaç dakika toocomplete alabilir. Tamamlandığında, hello sonuç içeren bir ileti görür:

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a>Bir dış kaynaktan şablon dağıtma

Resource Manager şablonları yerel makinenizde depolamak yerine toostore tercih edebilirsiniz harici bir konumda bunları. Şablonları bir kaynak denetimi deponuza (örneğin, GitHub) depolayabilirsiniz. Veya, bunları paylaşılan erişim için bir Azure depolama hesabı, kuruluşunuzda depolayabilirsiniz.

toodeploy dış bir şablonu kullanmak hello **TemplateUri** parametresi. Merhaba örnek toodeploy hello örnek şablonunu github'dan Hello URI kullanın.

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

Merhaba önceki örnekte genel olarak erişilebilir bir URI şablonunuzu hassas bir veri içermemesi çünkü çoğu senaryo için çalışır hello şablonu için gerektirir. Toospecify hassas verileri (örneğin, bir yönetici parolası) gerekiyorsa, bu değeri güvenli bir parametre olarak geçirin. Ancak, şablon toobe genel olarak erişilebilir istemiyorsanız, bir özel depolama kapsayıcısı depolayarak koruyabilirsiniz. Bir paylaşılan erişim imzası (SAS) belirteci gerektiren şablonu dağıtma hakkında daha fazla bilgi için bkz: [dağıtma özel şablonu SAS belirteci ile](resource-manager-powershell-sas-token.md).

## <a name="parameter-files"></a>Parametre dosyaları

Satır içi değerler olarak komut parametreleri geçirme yerine daha kolay toouse hello parametre değerlerini içeren bir JSON dosyası bulabilirsiniz. Merhaba parametre dosyası biçimini izleyen hello olması gerekir:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

Merhaba Parametreler bölümünde şablonunuzda (storageAccountType) tanımlı hello parametresi ile eşleşen bir parametre adı içerdiğine dikkat edin. Merhaba parametre dosyası hello parametresi için bir değer içerir. Bu değer, dağıtım sırasında toohello şablonu otomatik olarak geçirilir. Farklı dağıtım senaryoları için birden çok parametre dosyası oluşturun ve hello uygun parametre dosyası geçirin. 

Örnek önceki hello kopyalayın ve adlı bir dosya kaydedin `storage.parameters.json`.

toopass yerel parametre dosyası kullanmak hello **TemplateParameterFile** parametre:

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

toopass bir dış parametre dosyası kullanmak hello **TemplateParameterUri** parametre:

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

Satır içi parametreleri kullanabilirsiniz ve yerel bir parametre dosyası hello aynı dağıtım işlemi. Örneğin, bazı değerler hello yerel parametre dosyasında belirtin ve dağıtım sırasında diğer değerleri satır içi ekleyin. Merhaba yerel parametre dosyası ve satır içi bir parametre için değer sağlarsanız, hello satır içi değer önceliklidir.

Bir dış parametre dosyası kullandığınızda, ancak, diğer değerler ya da satır içi geçiremezsiniz veya yerel bir dosya. Bir parametre dosyası hello belirttiğinizde **TemplateParameterUri** parametresi, tüm satır içi parametreleri yok sayılır. Merhaba dış dosyadaki tüm parametre değerlerini sağlayın. Şablonunuzu hello parametre dosyasında içeremez duyarlı bir değer içeriyorsa, bu değer tooa anahtar kasası ekleyin ya da dinamik olarak tüm parametre değerleri satır içi sağlayın.

Şablonunuzu aynı adı hello PowerShell komutunu hello parametrelerinde biri olarak hello parametresiyle içeriyorsa, PowerShell şablonunuzu hello parametresinden hello sonek ile sayısını gösterir. **FromTemplate**. Örneğin, adlı bir parametre **ResourceGroupName** hello ile şablonu çakışıyor **ResourceGroupName** hello parametresinde [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)cmdlet'i. İstendiğinde tooprovide için bir değer olan **ResourceGroupNameFromTemplate**. Genel olarak, aynı dağıtım işlemleri için kullanılan parametreler olarak ad hello parametrelerle adlandırılmasıyla değil Bu Karışıklığı önlemek.

## <a name="test-a-template-deployment"></a>Şablon dağıtımı test etme

herhangi bir kaynağa gerçekte dağıtımı olmadan şablonu ve parametre değerlerini tootest kullanmak [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment). 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

Hiçbir hata algılanırsa, bir yanıt hello komutu tamamlanır. Bir hata algılandığında, hello komutu bir hata iletisi döndürür. Örneğin, toopass hello depolama hesabının SKU, yanlış bir değere çalışırken aşağıdaki hata hello döndürür:

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

Şablonunuzun söz dizimi hatası varsa, hello komut hello şablon ayrıştırılamadı belirten bir hata döndürür. Merhaba iletisi hello satır numarasını ve ayrıştırma hatası hello konumunu belirtir.

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

toouse tam modu, kullanım hello `Mode` parametre:

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a>Örnek şablonu

Merhaba aşağıdaki şablonu bu konudaki hello örnekleri için kullanılır. Kopyalayın ve storage.json adlı bir dosya kaydedin. toounderstand nasıl toocreate bu şablonu bkz [, ilk Azure Resource Manager şablonu oluşturma](resource-manager-create-first-template.md).  

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

## <a name="next-steps"></a>Sonraki adımlar
* Bu makaledeki örneklerde Hello varsayılan aboneliğinizin kaynakları tooa kaynak grubuna dağıtın. toouse farklı bir abonelik bkz [birden çok Azure Aboneliklerini yönetmek](/powershell/azure/manage-subscriptions-azureps).
* Bir şablon dağıtan bir tam örnek betik için bkz: [Resource Manager şablonu dağıtım betiği](resource-manager-samples-powershell-deploy.md).
* şablonunuzu toodefine parametrelerinde nasıl görürüm toounderstand [anlamak hello yapısı ve Azure Resource Manager şablonları sözdizimini](resource-group-authoring-templates.md).
* Genel dağıtım hatalarını giderme ipuçları için bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).
* Bir SAS belirteci gerektiren şablonu dağıtma hakkında daha fazla bilgi için bkz: [dağıtma özel şablonu SAS belirteci ile](resource-manager-powershell-sas-token.md).
* Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).

