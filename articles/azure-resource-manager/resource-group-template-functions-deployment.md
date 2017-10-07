---
title: "aaaAzure Resource Manager şablonu işlevleri - dağıtım | Microsoft Docs"
description: "Bir Azure Resource Manager şablonu tooretrieve dağıtım bilgileri Hello işlevleri toouse açıklar."
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
ms.date: 06/13/2017
ms.author: tomfitz
ms.openlocfilehash: 458c3f740504fdd6799ed24cc386219726737636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a>Azure Resource Manager şablonları için dağıtım işlevleri 

Resource Manager hello aşağıdaki değerleri hello şablon bölümlerinden alma için İşlevler ve ilgili toohello dağıtım değerleri sunar:

* [Dağıtım](#deployment)
* [parametreleri](#parameters)
* [değişkenleri](#variables)

Kaynak, kaynak grupları ya da abonelikler, tooget değerleri görmek [kaynak işlevlerini](resource-group-template-functions-resource.md).

<a id="deployment" />

## <a name="deployment"></a>dağıtım
`deployment()`

Merhaba geçerli dağıtım işlemiyle ilgili bilgi döndürür.

### <a name="return-value"></a>Dönüş değeri

Bu işlev, dağıtımı sırasında geçirilen hello nesnesi döndürür. Nesne döndürdü hello Hello özelliklerinde olup hello dağıtım nesnesi bir bağlantı veya bir satır içi nesnesi olarak geçirilen göre farklılık. Ne zaman hello dağıtım nesnesi geçirilir satır içi, gibi hello kullanırken **- TemplateFile** parametresi Azure PowerShell toopoint tooa yerel dosyasında hello nesne biçimini izleyen hello döndürdü:

```json
{
    "name": "",
    "properties": {
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [
            ],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

Ne zaman hello nesne geçirilir zaman kullanarak hello gibi bir bağlantı olarak **- TemplateUri** parametresi toopoint tooa uzaktan nesnesi, hello nesne biçimini izleyen hello döndürdü: 

```json
{
    "name": "",
    "properties": {
        "templateLink": {
            "uri": ""
        },
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

### <a name="remarks"></a>Açıklamalar

Merhaba üst şablon URI'sini hello üzerinde temel deployment() toolink tooanother şablonu kullanabilirsiniz.

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a>Örnek

Merhaba aşağıdaki örnek hello dağıtım nesnesi döndürür:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[deployment()]",
            "type" : "object"
        }
    }
}
```

Merhaba önceki örnekte nesne aşağıdaki hello döndürür:

```json
{
  "name": "deployment",
  "properties": {
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "resources": [],
      "outputs": {
        "subscriptionOutput": {
          "type": "Object",
          "value": "[deployment()]"
        }
      }
    },
    "parameters": {},
    "mode": "Incremental",
    "provisioningState": "Accepted"
  }
}
```

<a id="parameters" />

## <a name="parameters"></a>parametreler
`parameters(parameterName)`

Bir parametre değeri döndürür. Merhaba belirtilen parametre adı hello Parametreler bölümünde hello şablonunun tanımlanması gerekir.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| parameterName |Evet |Dize |Merhaba parametresi tooreturn Hello adı. |

### <a name="return-value"></a>Dönüş değeri

Merhaba başlangıç değeri parametresi belirtildi.

### <a name="remarks"></a>Açıklamalar

Genellikle, parametreleri tooset kaynak değerlerini kullanın. Merhaba aşağıdaki örnek dağıtımı sırasında geçirilen web sitesi toohello parametre değeri hello adını ayarlar.

```json
"parameters": { 
  "siteName": {
      "type": "string"
  }
},
"resources": [
   {
      "apiVersion": "2016-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/Sites",
      ...
   }
]
```

### <a name="example"></a>Örnek

Merhaba aşağıdaki örnek hello parametreleri işlevi Basitleştirilmiş kullanımını gösterir.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringParameter": {
            "type" : "string",
            "defaultValue": "option 1"
        },
        "intParameter": {
            "type": "int",
            "defaultValue": 1
        },
        "objectParameter": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b"}
        },
        "arrayParameter": {
            "type": "array",
            "defaultValue": [1, 2, 3]
        },
        "crossParameter": {
            "type": "string",
            "defaultValue": "[parameters('stringParameter')]"
        }
    },
    "variables": {},
    "resources": [],
    "outputs": {
        "stringOutput": {
            "value": "[parameters('stringParameter')]",
            "type" : "string"
        },
        "intOutput": {
            "value": "[parameters('intParameter')]",
            "type" : "int"
        },
        "objectOutput": {
            "value": "[parameters('objectParameter')]",
            "type" : "object"
        },
        "arrayOutput": {
            "value": "[parameters('arrayParameter')]",
            "type" : "array"
        },
        "crossOutput": {
            "value": "[parameters('crossParameter')]",
            "type" : "string"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| stringOutput | Dize | seçenek 1 |
| intOutput | Int | 1 |
| objectOutput | Nesne | {"bir": "a", "iki": "b"} |
| arrayOutput | Dizi | [1, 2, 3] |
| crossOutput | Dize | seçenek 1 |

<a id="variables" />

## <a name="variables"></a>değişkenleri
`variables(variableName)`

Değişkenin değerini döndürür hello. Belirtilen değişken adı Hello hello şablon değişkenleri bölümüne hello tanımlanması gerekir.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| variableName |Evet |Dize |Merhaba değişken tooreturn Hello adı. |

### <a name="return-value"></a>Dönüş değeri

Merhaba belirtilen değişkenin Hello değeri.

### <a name="remarks"></a>Açıklamalar

Genellikle, karmaşık değerler yalnızca bir kez oluşturarak şablonunuzu değişkenleri toosimplify kullanın. Merhaba aşağıdaki örnekte bir depolama hesabı için benzersiz bir ad oluşturur.

```json
"variables": {
    "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
},
"resources": [
    {
        "type": "Microsoft.Storage/storageAccounts",
        "name": "[variables('storageName')]",
        ...
    },
    {
        "type": "Microsoft.Compute/virtualMachines",
        "dependsOn": [
            "[variables('storageName')]"
        ],
        ...
    }
],
```

### <a name="example"></a>Örnek

Merhaba örnek şablonu farklı değişken değerleri döndürür.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {
        "var1": "myVariable",
        "var2": [ 1,2,3,4 ],
        "var3": "[ variables('var1') ]",
        "var4": {
            "property1": "value1",
            "property2": "value2"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput1": {
            "value": "[variables('var1')]",
            "type" : "string"
        },
        "exampleOutput2": {
            "value": "[variables('var2')]",
            "type" : "array"
        },
        "exampleOutput3": {
            "value": "[variables('var3')]",
            "type" : "string"
        },
        "exampleOutput4": {
            "value": "[variables('var4')]",
            "type" : "object"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| exampleOutput1 | Dize | myVariable |
| exampleOutput2 | Dizi | [1, 2, 3, 4] |
| exampleOutput3 | Dize | myVariable |
| exampleOutput4 |  Nesne | {"property1": "value1", "property2": "value2"} |

## <a name="next-steps"></a>Sonraki adımlar
* Bir Azure Resource Manager şablonu hello bölümlerde açıklaması için bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).
* birden fazla şablon toomerge bkz [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).
* tooiterate belirtilen sayıda kaynak türünü oluştururken bkz [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).
* toodeploy hello şablonu oluşturduğunuz toosee bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).

