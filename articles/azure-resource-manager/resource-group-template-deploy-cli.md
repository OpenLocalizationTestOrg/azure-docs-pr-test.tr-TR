---
title: "Azure CLI ve şablon aaaDeploy kaynaklarla | Microsoft Docs"
description: "Azure Resource Manager ve Azure CLI toodeploy kaynakları tooAzure kullanın. Merhaba kaynaklar bir Resource Manager şablonunda tanımlanır."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 493b7932-8d1e-4499-912c-26098282ec95
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: tomfitz
ms.openlocfilehash: 9f8bb9a8720399390a407030d2d32bcd97d32f13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a>Kaynakları Resource Manager şablonları ve Azure CLI ile dağıtma

Bu konuda açıklanmaktadır nasıl toouse Azure CLI 2.0 Resource Manager şablonları toodeploy ile kaynakları tooAzure. Dağıtma hello kavramları hakkında bilgi sahibi değilseniz ve Azure çözümlerinizi bkz [Azure Resource Manager'a genel bakış](resource-group-overview.md).  

Merhaba Resource Manager şablonu ya da makinenizde yerel bir dosya ya da GitHub gibi bir havuzda bulunan dış dosyası dağıtabilirsiniz. Bu makalede dağıttığınız hello şablon hello kullanılabilir [örnek şablonu](#sample-template) bölümünde, ya da farklı bir [depolama hesabı şablonu github](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

Azure CLI yüklenmiş yoksa hello kullanabilirsiniz [bulut Kabuk](#deploy-template-from-cloud-shell).

## <a name="deploy-local-template"></a>Yerel şablonu dağıtma

Kaynakları tooAzure dağıtırken:

1. Azure hesabı tooyour içinde oturum
2. Dağıtılan hello kaynaklar için hello kapsayıcı görevi gören bir kaynak grubu oluşturun. Hello hello kaynak grubu adı yalnızca alfasayısal karakterler, nokta, alt çizgi, kısa çizgi ve parantez içerebilir. Too90 karakter olabilir. Bir nokta ile bitemez.
3. Merhaba kaynakları toocreate tanımlar toohello kaynak grubu hello şablonu dağıtma

Bir şablon toocustomize hello dağıtımını etkinleştirmek parametreleri içerebilir. Örneğin, belirli bir ortamda (örneğin, geliştirme, test ve üretim) için uyarlanabilir değerler sağlayabilirsiniz. Merhaba örnek şablonu hello depolama hesabı SKU için bir parametre tanımlar. 

Aşağıdaki örnek hello bir kaynak grubu oluşturur ve yerel makinenize bir şablondan dağıtır:

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

Merhaba dağıtım birkaç dakika toocomplete alabilir. Tamamlandığında, hello sonuç içeren bir ileti görür:

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a>Dış şablonu dağıtma

Resource Manager şablonları yerel makinenizde depolamak yerine toostore tercih edebilirsiniz harici bir konumda bunları. Şablonları bir kaynak denetimi deponuza (örneğin, GitHub) depolayabilirsiniz. Veya, bunları paylaşılan erişim için bir Azure depolama hesabı, kuruluşunuzda depolayabilirsiniz.

toodeploy dış bir şablonu kullanmak hello **şablonu URI** parametresi. Merhaba örnek toodeploy hello örnek şablonunu github'dan Hello URI kullanın.
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

Merhaba önceki örnekte genel olarak erişilebilir bir URI şablonunuzu hassas bir veri içermemesi çünkü çoğu senaryo için çalışır hello şablonu için gerektirir. Toospecify hassas verileri (örneğin, bir yönetici parolası) gerekiyorsa, bu değeri güvenli bir parametre olarak geçirin. Ancak, şablon toobe genel olarak erişilebilir istemiyorsanız, bir özel depolama kapsayıcısı depolayarak koruyabilirsiniz. Bir paylaşılan erişim imzası (SAS) belirteci gerektiren şablonu dağıtma hakkında daha fazla bilgi için bkz: [dağıtma özel şablonu SAS belirteci ile](resource-manager-cli-sas-token.md).

## <a name="deploy-template-from-cloud-shell"></a>Cloud Shell'den şablon dağıtma

Kullanabileceğiniz [bulut Kabuk](../cloud-shell/overview.md) toorun hello Azure CLI komutları şablonunuzu dağıtmak için. Ancak, ilk şablonunuzu hello dosya paylaşım içine bulut Kabuğunuzu yüklemeniz gerekir. Daha önce Cloud Shell kullanmadıysanız, kurulumu hakkında bilgi için bkz. [Azure Cloud Shell’e Genel Bakış](../cloud-shell/overview.md).

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).   

2. Cloud Shell kaynak grubunuzu seçin. Merhaba adı deseni `cloud-shell-storage-<region>`.

   ![Kaynak grubu seçin](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. Bulut Kabuğunuzu Hello depolama hesabı seçin.

   ![Depolama hesabı seçme](./media/resource-group-template-deploy-cli/select-storage.png)

4. **Dosyalar**’ı seçin.

   ![Dosya seçme](./media/resource-group-template-deploy-cli/select-files.png)

5. Hello dosya paylaşımı için bulut Kabuğu'nu seçin. Merhaba adı deseni `cs-<user>-<domain>-com-<uniqueGuid>`.

   ![Dosya paylaşımı seçme](./media/resource-group-template-deploy-cli/select-file-share.png)

6. **Dizin ekle**’yi seçin.

   ![Dizin ekleme](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. **Şablonlar** olarak adlandırıp **Tamam**’ı seçin.

   ![Ad dizini](./media/resource-group-template-deploy-cli/name-templates.png)

8. Yeni dizininizi seçin.

   ![Dizin seçme](./media/resource-group-template-deploy-cli/select-templates.png)

9. **Karşıya Yükle**’yi seçin.

   ![Karşıya yükleme seçme](./media/resource-group-template-deploy-cli/select-upload.png)

10. Şablonunuzu bulup karşıya yükleyin.

   ![Dosya yükleme](./media/resource-group-template-deploy-cli/upload-files.png)

11. Açık hello istemi.

   ![Cloud Shell’i açma](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. Merhaba bulut Kabuk komutları aşağıdaki hello girin:

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

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

toopass yerel parametre dosyası kullanmak `@` toospecify storage.parameters.json adlı bir yerel dosya.

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a>Şablon dağıtımı test etme

herhangi bir kaynağa gerçekte dağıtımı olmadan şablonu ve parametre değerlerini tootest kullanmak [az grup dağıtımı doğrulamak](/cli/azure/group/deployment#validate). 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

Hiçbir hata algılanırsa, hello komut hello sınama dağıtımı hakkında bilgi döndürür. Özellikle, bu hello fark **hata** değeri NULL'dur.

```azurecli
{
  "error": null,
  "properties": {
      ...
```

Bir hata algılandığında, hello komutu bir hata iletisi döndürür. Örneğin, toopass hello depolama hesabının SKU, yanlış bir değere çalışırken aşağıdaki hata hello döndürür:

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'hello provided value 'badSKU' for hello template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. hello parameter value is not part of hello allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

Şablonunuzun söz dizimi hatası varsa, hello komut hello şablon ayrıştırılamadı belirten bir hata döndürür. Merhaba iletisi hello satır numarasını ve ayrıştırma hatası hello konumunu belirtir.

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template parse failed: 'After parsing a value an unexpected character was encountered:
      \". Path 'variables', line 31, position 3.'.",
    "target": null
  },
  "properties": null
}
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

toouse tam modu, kullanım hello `mode` parametre:

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
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
* Bu makaledeki örneklerde Hello varsayılan aboneliğinizin kaynakları tooa kaynak grubuna dağıtın. toouse farklı bir abonelik bkz [birden çok Azure Aboneliklerini yönetmek](/cli/azure/manage-azure-subscriptions-azure-cli).
* Bir şablon dağıtan bir tam örnek betik için bkz: [Resource Manager şablonu dağıtım betiği](resource-manager-samples-cli-deploy.md).
* şablonunuzu toodefine parametrelerinde nasıl görürüm toounderstand [anlamak hello yapısı ve Azure Resource Manager şablonları sözdizimini](resource-group-authoring-templates.md).
* Genel dağıtım hatalarını giderme ipuçları için bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).
* Bir SAS belirteci gerektiren şablonu dağıtma hakkında daha fazla bilgi için bkz: [dağıtma özel şablonu SAS belirteci ile](resource-manager-cli-sas-token.md).
* Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).
