---
title: "Azure dağıtımının aaaLink şablonları | Microsoft Docs"
description: "Toouse bir Azure Resource Manager şablonu toocreate şablonlarında modüler şablonu çözümü nasıl bağlı açıklar. Nasıl toopass parametre değerleri, bir parametre dosyası belirtin ve dinamik olarak URL'leri oluşturulan gösterir."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 27d8c4b2-1e24-45fe-88fd-8cf98a6bb2d2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: b935b1810db5ce894d009403cd4bb945cab34ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a>Azure kaynaklarını dağıtırken bağlı şablonları kullanma
Gelen bir Azure Resource Manager şablonu içinde toodecompose sağlayan tooanother şablonu dağıtımınızı hedeflenen, amaca şablonları kümesine bağlayabilirsiniz. Birkaç kod sınıfı bir uygulamaya gibi ayırma, ayrıştırma sınama, yeniden kullanılmasını ve okunabilirliği açısından faydaları sunar.  

Bir ana şablon tooa bağlantılı şablondan parametreleri geçirebilirsiniz ve bu parametrelerin doğrudan tooparameters veya şablon çağırma hello tarafından kullanıma sunulan değişkenleri eşleyebilirsiniz. Merhaba bağlantılı şablonu da şablonlar arasında iki yönlü veri değişimi etkinleştirme bir çıktı değişken geri toohello kaynak şablonu geçirebilirsiniz.

## <a name="linking-tooa-template"></a>Tooa şablon bağlama
Dağıtım kaynağı hello ana şablonu içindeki noktaları toohello bağlantılı şablon ekleyerek iki şablonları arasında bir bağlantı oluşturun. Merhaba ayarladığınız **templateLink** özelliği toohello hello bağlantılı şablon URI'si. Şablonunuzdaki doğrudan veya bir parametre dosyası hello bağlantılı şablonu için parametre değerlerini sağlayabilir. Merhaba aşağıdaki örnek kullanır hello **parametreleri** özelliği toospecify doğrudan bir parametre değeri.

```json
"resources": [ 
  { 
      "apiVersion": "2017-05-10", 
      "name": "linkedTemplate", 
      "type": "Microsoft.Resources/deployments", 
      "properties": { 
        "mode": "incremental", 
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion": "1.0.0.0"
        }, 
        "parameters": { 
          "StorageAccountName":{"value": "[parameters('StorageAccountName')]"} 
        } 
      } 
  } 
] 
```

Diğer kaynak türleri gibi hello bağlantılı şablonu ve kaynaklar arasındaki bağımlılıkları ayarlayabilirsiniz. Bu nedenle, diğer kaynakları bir çıkış değeri hello bağlantılı şablondan gerektirdiğinde hello bağlantılı şablonu daha önce dağıtılan emin olabilirsiniz. Veya diğer kaynaklara hello bağlantılı şablonunu kullanır, diğer kaynakları hello bağlantılı şablonu önce dağıtılan emin olabilirsiniz. Bir değer sözdizimi aşağıdaki hello ile bağlantılı bir şablondan alabilirsiniz:

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

Merhaba Kaynak Yöneticisi hizmeti mümkün tooaccess hello bağlantılı şablonu olmalıdır. Yerel bir dosya veya yalnızca yerel ağınızdaki hello bağlantılı şablonu için kullanılabilir bir dosya belirtemezsiniz. İçerir ya da bir URI değeri yalnızca sağlayabilir **http** veya **https**. Bir depolama hesabı ve kullanım bağlantılı şablonunuzda gibi aşağıdaki örneğine hello gösterilen bu öğe için URI hello tooplace bir seçenektir:

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

Merhaba bağlantılı şablon dışarıdan kullanılabilir olması gerekse de toobe genel olarak kullanılabilir toohello ortak gerekmez. Erişilebilir tooonly hello depolama hesabı sahibi olan şablon tooa özel depolama hesabınız ekleyebilirsiniz. Ardından, bir paylaşılan erişim imzası (SAS) belirteci tooenable erişim dağıtımı sırasında oluşturun. Merhaba bağlantılı şablon için bu SAS belirteci toohello URI ekleyin. Bir şablonda bir depolama hesabı ayarlama ve bir SAS belirteci oluşturma adımları için bkz [Resource Manager şablonları ve Azure PowerShell ile kaynakları dağıtmak](resource-group-template-deploy.md) veya [Resource Manager şablonları ve Azure CLI kaynaklarla dağıtmak](resource-group-template-deploy-cli.md). 

Aşağıdaki örneğine hello üst şablon bu bağlantılar tooanother şablonu gösterir. Merhaba bağlantılı şablon parametre olarak geçirilen bir SAS belirteci ile erişilir.

```json
"parameters": {
    "sasToken": { "type": "securestring" }
},
"resources": [
    {
        "apiVersion": "2017-05-10",
        "name": "linkedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
          "mode": "incremental",
          "templateLink": {
            "uri": "[concat('https://storagecontosotemplates.blob.core.windows.net/templates/helloworld.json', parameters('sasToken'))]",
            "contentVersion": "1.0.0.0"
          }
        }
    }
],
```

Merhaba belirteci güvenli bir dize geçirilen olsa bile, hello hello SAS belirteci dahil olmak üzere hello bağlantılı şablon URI'sini hello dağıtım işlemlerine günlüğe kaydedilir. toolimit Etkilenme hello belirteci için bir sona erme ayarlayın.

Resource Manager her bağlantılı bir şablon ayrı bir dağıtım işler. Hello dağıtım geçmişini hello kaynak grubu için ayrı dağıtımları hello üst ve iç içe geçmiş şablonları için bkz.

![dağıtım geçmişi](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-tooa-parameter-file"></a>Tooa parametre dosyası bağlama
Merhaba sonraki örnek kullanır hello **parametersLink** özelliği toolink tooa parametre dosyası.

```json
"resources": [ 
  { 
     "apiVersion": "2017-05-10", 
     "name": "linkedTemplate", 
     "type": "Microsoft.Resources/deployments", 
     "properties": { 
       "mode": "incremental", 
       "templateLink": {
          "uri":"https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion":"1.0.0.0"
       }, 
       "parametersLink": { 
          "uri":"https://www.contoso.com/AzureTemplates/parameters.json",
          "contentVersion":"1.0.0.0"
       } 
     } 
  } 
] 
```

Merhaba URI değeri hello bağlantılı parametre dosyası yerel bir dosya olamaz ve ya da içermelidir **http** veya **https**. Merhaba parametre dosyası da bir SAS belirteci üzerinden sınırlı tooaccess olabilir.

## <a name="using-variables-toolink-templates"></a>Değişkenleri toolink şablonlarını kullanma
Merhaba önceki örneklerde hello şablon bağlantılar için sabit kodlanmış URL değerleri gösterilmiştir. Bu yaklaşım basit bir şablon için çalışabilir, ancak iyi çok sayıda modüler şablonları çalışırken çalışmaz. Bunun yerine, hello ana şablon için bir temel URL depolar statik bir değişkeni oluşturun ve ardından dinamik olarak URL'leri için temel bu URL'den bağlı hello şablonları oluşturun. Bu yaklaşımın avantajı Hello toochange hello statik değişkende hello ana şablon yalnızca gerektiğinden, taşıma veya çatalı hello şablonu kolayca ' dir. Merhaba ana şablon hello hello boyunca URI şablonunu ayrılmış doğru geçirir.

Merhaba aşağıdaki örnekte nasıl toouse temel URL toocreate iki URL'ler için bağlantılı gösterir şablonları (**sharedTemplateUrl** ve **vmTemplate**). 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

Aynı zamanda [deployment()](resource-group-template-functions-deployment.md#deployment) tooget hello geçerli şablon için temel URL hello ve hello diğer şablonlar için bu tooget hello URL kullanmak aynı konumu. Bu yaklaşım şablon konumunuza değişirse yararlı olur (belki de son tooversioning) veya tooavoid sabit hello şablon dosyası URL'lerinde kodlama istiyor. 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a>Tam örnek
Örnek şablonları aşağıdaki hello bağlı şablonları tooillustrate Basitleştirilmiş düzenlenmesi bu makalede birkaç hello kavramları göstermektedir. Bu genel erişimi bir depolama hesabıyla aynı kapsayıcıda kapalı toohello hello şablonları eklenmiş varsayar. Merhaba bağlantılı şablon geçirmeden bir değeri geri toohello ana şablon hello **çıkarır** bölümü.

Merhaba **parent.json** dosya oluşur:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "containerSasToken": { "type": "string" }
  },
  "resources": [
    {
      "apiVersion": "2017-05-10",
      "name": "linkedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "[concat(uri(deployment().properties.templateLink.uri, 'helloworld.json'), parameters('containerSasToken'))]",
          "contentVersion": "1.0.0.0"
        }
      }
    }
  ],
  "outputs": {
    "result": {
      "type": "string",
      "value": "[reference('linkedTemplate').outputs.result.value]"
    }
  }
}
```

Merhaba **helloworld.json** dosya oluşur:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "variables": {},
  "resources": [],
  "outputs": {
    "result": {
        "value": "Hello World",
        "type" : "string"
    }
  }
}
```

PowerShell'de, hello kapsayıcı için bir belirteç almak ve hello şablonlarıyla dağıtabilirsiniz:

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

Azure CLI 2. 0'da, hello kapsayıcı için bir belirteç almak ve başlangıç şablonları koddan hello ile dağıtabilirsiniz:

```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name storagecontosotemplates \
    --query connectionString)
token=$(az storage container generate-sas \
    --name templates \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name parent.json \
    --output tsv \
    --connection-string $connection)
parameter='{"containerSasToken":{"value":"?'$token'"}}'
az group deployment create --resource-group ExampleGroup --template-uri $url?$token --parameters $parameter
```

## <a name="next-steps"></a>Sonraki adımlar
* toolearn hello hello dağıtım sırası, kaynaklar için tanımlama hakkında bkz [Azure Resource Manager'da bağımlılıkları tanımlama](resource-group-define-dependencies.md)
* toolearn toodefine bir kaynak ancak oluşturmak nasıl, birçok örneklerini görmek [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md)

