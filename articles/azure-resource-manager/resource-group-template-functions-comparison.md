---
title: "aaaAzure Resource Manager şablonu işlevleri - karşılaştırma | Microsoft Docs"
description: "Bir Azure Resource Manager şablonu toocompare değerleri Hello işlevleri toouse açıklar."
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
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: ebcfc9ed6c93f8b540ec4c066e9457c621800b7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a>Azure Resource Manager şablonları için karşılaştırma işlevleri

Resource Manager şablonlarınızı içinde karşılaştırmaları yapmak için çeşitli işlevleri sağlar.

* [eşittir](#equals)
* [büyük](#greater)
* [greaterOrEquals](#greaterorequals)
* [daha az](#less)
* [lessOrEquals](#lessorequals)

## <a name="equals"></a>eşittir
`equals(arg1, arg2)`

İki değerin birbirine eşit olup olmadığını denetler.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |int, string, dizi veya nesne |Merhaba ilk değer toocheck eşitlik için. |
| arg2 |Evet |int, string, dizi veya nesne |Merhaba ikinci değer toocheck eşitlik için. |

### <a name="return-value"></a>Dönüş değeri

Döndürür **True** hello değerler eşit; Aksi takdirde ise **False**.

### <a name="remarks"></a>Açıklamalar

Merhaba equals işlevi genellikle hello ile kullanılan `condition` öğesi tootest bir kaynak olup olmadığını dağıtılır.

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

### <a name="example"></a>Örnek

Merhaba örnek şablonu farklı türlerdeki eşitlik için değerleri denetler. Tüm hello varsayılan değerler True döndürür.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 1
        },
        "firstString": {
            "type": "string",
            "defaultValue": "a"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "firstObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[equals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[equals(parameters('firstString'), parameters('secondString'))]"
        },
        "checkArrays": {
            "type": "bool",
            "value": "[equals(parameters('firstArray'), parameters('secondArray'))]"
        },
        "checkObjects": {
            "type": "bool",
            "value": "[equals(parameters('firstObject'), parameters('secondObject'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| checkInts | bool | True |
| checkStrings | bool | True |
| checkArrays | bool | True |
| checkObjects | bool | True |


Merhaba aşağıdaki örnek kullanır [değil](resource-group-template-functions-logical.md#not) ile **eşittir**.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "checkNotEquals": {
            "type": "bool",
            "value": "[not(equals(1, 2))]"
        }
    }
```

Örnek önceki hello Hello çıktısı şöyledir:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| checkNotEquals | bool | True |


## <a name="greater"></a>büyük
`greater(arg1, arg2)`

Merhaba ilk değer hello ikinci değerden daha büyük olup olmadığını denetler.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |int veya dize |Merhaba hello büyük karşılaştırma için ilk değer. |
| arg2 |Evet |int veya dize |Merhaba hello büyük karşılaştırma için ikinci değer. |

### <a name="return-value"></a>Dönüş değeri

Döndürür **True** hello ilk değer, hello ikinci değerden daha büyük Aksi takdirde **False**.

### <a name="example"></a>Örnek

Merhaba örnek şablon hello bir değer hello diğer büyük olup olmadığını denetler.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greater(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greater(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| checkInts | bool | False |
| checkStrings | bool | True |


## <a name="greaterorequals"></a>greaterOrEquals
`greaterOrEquals(arg1, arg2)`

Merhaba ilk değeri sıfırdan büyük veya eşit toohello ikinci değer olup olmadığını denetler.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |int veya dize |Merhaba hello büyük veya eşit karşılaştırma için ilk değer. |
| arg2 |Evet |int veya dize |Merhaba hello büyük veya eşit karşılaştırma için ikinci değer. |

### <a name="return-value"></a>Dönüş değeri

Döndürür **True** hello ilk değer sıfırdan büyük veya eşit toohello ikinci; değeriyse, aksi takdirde, **False**.

### <a name="example"></a>Örnek

Merhaba örnek şablon hello bir değer değerinden büyük veya eşit toohello diğer denetler.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| checkInts | bool | False |
| checkStrings | bool | True |



## <a name="less"></a>daha az
`less(arg1, arg2)`

Merhaba ilk değer küçük olup olmadığını ikinci değer hello denetler.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |int veya dize |Merhaba karşılaştırma daha az hello için ilk değer. |
| arg2 |Evet |int veya dize |Merhaba hello daha az karşılaştırma için ikinci değer. |

### <a name="return-value"></a>Dönüş değeri

Döndürür **True** hello ilk değer hello küçükse ikinci değer; Aksi halde, **False**.

### <a name="example"></a>Örnek

Hello örnek şablon hello bir değer hello diğer değerinden olmadığını denetler.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[less(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[less(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| checkInts | bool | True |
| checkStrings | bool | False |


## <a name="lessorequals"></a>lessOrEquals
`lessOrEquals(arg1, arg2)`

Merhaba ilk değer küçük veya buna eşit olup olmadığını denetler toohello ikinci değer.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |int veya dize |Merhaba ilk değeri hello küçük veya eşittir karşılaştırması. |
| arg2 |Evet |int veya dize |İkinci değer hello için daha az hello veya karşılaştırma eşittir. |

### <a name="return-value"></a>Dönüş değeri

Döndürür **True** hello ilk değer küçük veya buna eşit ise toohello ikinci değeri; Aksi halde, **False**.

### <a name="example"></a>Örnek

Merhaba örnek şablon hello bir değer küçük veya buna eşit olup olmadığını denetler toohello diğer.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| checkInts | bool | True |
| checkStrings | bool | False |



## <a name="next-steps"></a>Sonraki adımlar
* Bir Azure Resource Manager şablonu hello bölümlerde açıklaması için bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).
* birden fazla şablon toomerge bkz [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).
* tooiterate belirtilen sayıda kaynak türünü oluştururken bkz [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).
* toodeploy hello şablonu oluşturduğunuz toosee bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).

