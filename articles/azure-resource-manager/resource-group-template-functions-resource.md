---
title: "aaaAzure Resource Manager şablonu işlevleri - kaynakları | Microsoft Docs"
description: "Bir Azure Resource Manager şablonu tooretrieve değerleri Hello işlevleri toouse kaynaklar hakkında açıklar."
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
ms.date: 08/09/2017
ms.author: tomfitz
ms.openlocfilehash: c9d524b338b8b7ea6d8c9e0135d48e4fb8f167c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a>Azure Resource Manager şablonları için kaynak işlevleri

Resource Manager kaynak değerlerini alma işlevleri aşağıdaki hello sunar:

* [listKeys ve liste {Value}](#listkeys)
* [sağlayıcıları](#providers)
* [başvuru](#reference)
* [kaynak grubu](#resourcegroup)
* [ResourceId](#resourceid)
* [aboneliği](#subscription)

Parametreler, değişkenleri ya da hello geçerli dağıtımı, tooget değerleri görmek [dağıtım değer işlevleri](resource-group-template-functions-deployment.md).

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a>listKeys ve liste {Value}
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

Hello liste işlemi destekleyen herhangi bir kaynak türü için değerleri verir hello. Merhaba en yaygın kullanımı `listKeys`. 

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| resourceName veya resourceIdentifier |Evet |Dize |Merhaba kaynak için benzersiz tanımlayıcı. |
| apiVersion |Evet |Dize |Kaynak çalışma zamanı durumunu API sürümü. Genellikle, biçiminde hello **yyyy-aa-gg**. |

### <a name="return-value"></a>Dönüş değeri

Merhaba listKeys nesnesinden biçimini izleyen hello döndürdü:

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

Diğer liste işlevler farklı dönüş biçimlerine sahip. bir işlevin toosee hello biçimi dahil hello çıkışları bölümünde hello örnek şablonda gösterildiği gibi. 

### <a name="remarks"></a>Açıklamalar

İle başlayan herhangi bir işlem **listesi** şablonunuzda bir işlevi olarak kullanılabilir. Merhaba kullanılabilir işlemleri arasında yalnızca listKeys, ancak ayrıca operations ister `list`, `listAdminKeys`, ve `listStatus`. Ancak, kullanamazsınız **listesi** hello değerleri gerektiren işlemler iste gövde. Örneğin, hello [listesi hesap SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) işlem gerektirir istek gövde parametreleri ister *signedExpiry*, dolayısıyla bir şablonda kullanamaz.

hangi kaynak türlerinin bir listesini işleme sahip toodetermine, aşağıdaki seçenekleri şu hello vardır:

* Görünüm hello [REST API işlemleri](/rest/api/) için bir kaynak sağlayıcısı ve listeleme işlemleri arayın. Örneğin, depolama hesapları hello sahip [listKeys işlemi](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).
* Kullanım hello [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet'i. Merhaba aşağıdaki örnekte tüm liste işlemler depolama hesapları için alır:

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* Azure CLI komutu toofilter listeleme işlemleri yalnızca hello aşağıdaki hello kullan:

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

Merhaba kaynak ya da hello kullanarak belirttiğiniz [ResourceId işlevi](#resourceid), veya hello biçimi `{providerNamespace}/{resourceType}/{resourceName}`.


### <a name="example"></a>Örnek

Merhaba aşağıdaki örnekte nasıl hello bir depolama hesabından tooreturn hello birincil ve ikincil anahtarları çıkarır bölümünde gösterilir.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountId": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "storageKeysOutput": {
            "value": "[listKeys(parameters('storageAccountId'), '2016-01-01')]",
            "type" : "object"
        }
    }
}
``` 

<a id="providers" />

## <a name="providers"></a>sağlayıcıları
`providers(providerNamespace, [resourceType])`

Bir kaynak sağlayıcısı ve desteklenen kaynak türleri hakkında bilgi döndürür. Bir kaynak türü belirtmezseniz, tüm desteklenen hello türleri hello kaynak sağlayıcısı için hello işlevi döndürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| providerNamespace |Evet |Dize |Namespace hello sağlayıcısı |
| Kaynak türü |Hayır |Dize |Merhaba türde bir hello içindeki kaynak ad alanı belirtildi. |

### <a name="return-value"></a>Dönüş değeri

Desteklenen her tür biçimi aşağıdaki hello verilir: 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

Merhaba dizi sıralama değerleri yıkıcıları döndürdü.

### <a name="example"></a>Örnek

Aşağıdaki örnek hello nasıl toouse hello sağlayıcısı işlevi gösterir:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers('Microsoft.Web', 'sites')]",
            "type" : "object"
        }
    }
}
```

Merhaba önceki örnekte bir nesne biçimini izleyen hello döndürür:

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<a id="reference" />

## <a name="reference"></a>Başvuru
`reference(resourceName or resourceIdentifier, [apiVersion])`

Bir kaynağın çalışma zamanı durumunu temsil eden bir nesne döndürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| resourceName veya resourceIdentifier |Evet |Dize |Adı veya bir kaynak benzersiz tanıtıcısı. |
| apiVersion |Hayır |Dize |Kaynak hello API sürümü belirtildi. Merhaba kaynak aynı şablonu içinde değil sağlandığında bu parametreyi dahil edin. Genellikle, biçiminde hello **yyyy-aa-gg**. |

### <a name="return-value"></a>Dönüş değeri

Her kaynak türü hello başvuru işlevi için farklı özellikleri döndürür. Merhaba işlevi tek, önceden tanımlanmış biçimi döndürmez. bir kaynak türü için toosee hello özellikleri döndürür hello hello nesnesinde hello örnekte gösterildiği gibi bölüm çıkarır.

### <a name="remarks"></a>Açıklamalar

Merhaba başvuru işlevi bir çalışma zamanı durumu değerinden türeten ve hello değişkenler bölümünde bu nedenle kullanılamaz. Şablon çıktıları bölümünde kullanılabilir. 

Merhaba başvuru işlevini kullanarak, dolaylı olarak başvurulan hello kaynak aynı şablonu içinde sağlandığında, bir kaynak üzerinde başka bir kaynak bağlıdır bildirin. Tooalso kullanım hello dependsOn özellik gerekli değildir. Merhaba başvurulan kaynak dağıtımı tamamlanana kadar hello işlevi değerlendirilmez.

toosee hello özellik adları ve değerleri bir kaynak türü için hello çıkışları bölümünde hello nesnesi döndüren bir şablon oluşturun. Bu tür mevcut bir kaynağı varsa, şablonunuzun herhangi yeni kaynaklar dağıtmadan hello nesnesini döndürür. 

Merhaba genellikle, kullandığınız **başvuru** tooreturn hello blob uç noktası URI gibi nesne veya tam etki alanı adı arasında belirli bir değer işlev.

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

### <a name="example"></a>Örnek

Merhaba toodeploy ve başvuru hello kaynağında aynı şablonu, kullanın:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      }
    }
}
``` 

Merhaba önceki örnekte bir nesne biçimini izleyen hello döndürür:

```json
{
   "creationTime": "2017-06-13T21:24:46.618364Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

Merhaba aşağıdaki örnekte bu şablonda dağıtılmamış bir depolama hesabı başvurur. Merhaba depolama hesabı hello içinde aynı zaten kaynak grubu.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a>kaynak grubu
`resourceGroup()`

Merhaba geçerli kaynak grubunda temsil eden bir nesne döndürür. 

### <a name="return-value"></a>Dönüş değeri

Merhaba nesne biçimini izleyen hello döndürülür:

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a>Açıklamalar

Merhaba toocreate kaynaklarında hello resourceGroup işlevinin yaygın bir kullanımdır hello kaynak grubu olarak aynı konumu. Merhaba aşağıdaki örnek hello kaynak grubu konumu tooassign hello konumu bir web sitesi için kullanır.

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a>Örnek

Merhaba aşağıdaki şablonu hello hello kaynak grubunun özelliklerini döndürür.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

Merhaba önceki örnekte bir nesne biçimini izleyen hello döndürür:

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<a id="resourceid" />

## <a name="resourceid"></a>resourceId
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

Bir kaynak benzersiz tanımlayıcısını döndürür hello. Merhaba kaynak adı belirsiz veya hello içinde sağlanan olduğunda bu işlevi kullanın aynı şablonu. 

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| subscriptionId |Hayır |dize (içinde GUID biçimi) |Merhaba geçerli abonelik varsayılan değerdir. Bir kaynağı başka bir abonelik tooretrieve gerektiğinde bu değeri belirtin. |
| resourceGroupName |Hayır |Dize |Geçerli kaynak grubunda varsayılan değerdir. Bir kaynağı başka bir kaynak grubunda tooretrieve gerektiğinde bu değeri belirtin. |
| Kaynak türü |Evet |Dize |Kaynak sağlayıcısı ad alanı dahil olmak üzere kaynak türü. |
| resourceName1 |Evet |Dize |Kaynağın adı. |
| resourceName2 |Hayır |Dize |Kaynak iç içe yerleştirilmiş ise sonraki kaynak adı kesimi. |

### <a name="return-value"></a>Dönüş değeri

Merhaba tanımlayıcı biçimini izleyen hello verilir:

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a>Açıklamalar

Merhaba, belirttiğiniz parametre değerlerini hello kaynak hello olmasına göre değişir hello geçerli dağıtım aynı abonelik ve kaynak grubu.

tooget hello kaynak kimliği hello depolama hesabı için aynı abonelik ve kaynak grubu kullanın:

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

tooget hello kaynak kimliği için bir depolama hesabı aynı abonelikte ancak farklı bir kaynak grubu, kullanımı hello:

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

tooget hello kaynak kimliği için farklı bir abonelik ve kaynak grubu, depolama hesabı kullanın:

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

tooget hello kaynak kimliği farklı bir kaynak grubu, bir veritabanı için kullanın:

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

Genellikle, toouse bu işlev bir depolama hesabı veya sanal ağ bir alternatif kaynak grubunda kullanırken gerekir. Merhaba aşağıdaki örnek bir dış kaynak grubundan bir kaynak kolayca nasıl kullanılabileceğini gösterir:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a>Örnek

Merhaba aşağıdaki örnekte bir depolama hesabı için hello kaynak kimliği hello kaynak grubunda döndürür:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| sameRGOutput | Dize | /Subscriptions/{Current-Sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentRGOutput | Dize | /Subscriptions/{Current-Sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentSubOutput | Dize | /Subscriptions/{Different-Sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| nestedResourceOutput | Dize | /Subscriptions/{Current-Sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/Servers/ServerName/Databases/databaseName |

<a id="subscription" />

## <a name="subscription"></a>aboneliği
`subscription()`

Merhaba abonelik hello geçerli dağıtım için ayrıntılarını döndürür. 

### <a name="return-value"></a>Dönüş değeri

Merhaba işlevi biçimini izleyen hello döndürür:

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a>Örnek

Merhaba aşağıdaki örnek hello çıkışları bölümünde çağrılan hello Abonelik işlevi gösterir. 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

## <a name="next-steps"></a>Sonraki adımlar
* Bir Azure Resource Manager şablonu hello bölümlerde açıklaması için bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).
* birden fazla şablon toomerge bkz [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).
* tooiterate belirtilen sayıda kaynak türünü oluştururken bkz [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).
* toodeploy hello şablonu oluşturduğunuz toosee bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).

