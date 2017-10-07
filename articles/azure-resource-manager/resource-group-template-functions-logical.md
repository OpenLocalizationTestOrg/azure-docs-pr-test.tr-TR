---
title: "aaaAzure Resource Manager şablonu işlevleri - mantıksal | Microsoft Docs"
description: "Bir Azure Resource Manager şablonu toodetermine mantıksal değerleri Hello işlevleri toouse açıklar."
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
ms.openlocfilehash: aec6341fbde00b4eba3b4539ff9a9aec774333fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a>Azure Resource Manager şablonları için mantıksal işlevleri

Resource Manager şablonlarınızı içinde karşılaştırmaları yapmak için çeşitli işlevleri sağlar.

* [ve](#and)
* [bool](#bool)
* [Eğer](#if)
* [değil](#not)
* [veya](#or)

## <a name="and"></a>ve
`and(arg1, arg2)`

Her iki parametre değeri doğru olup olmadığını denetler.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |Boole değeri |ilk değer toocheck olup hello doğrudur. |
| arg2 |Evet |Boole değeri |İkinci değer toocheck olup hello doğrudur. |

### <a name="return-value"></a>Dönüş değeri

Döndürür **True** her iki değeri varsa true, aksi takdirde **False**.

### <a name="examples"></a>Örnekler

örnekte gösterildiği nasıl aşağıdaki hello toouse mantıksal işlevleri.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

Örnek önceki hello Hello çıktısı şöyledir:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| andExampleOutput | bool | False |
| orExampleOutput | bool | True |
| notExampleOutput | bool | False |


## <a name="bool"></a>bool
`bool(arg1)`

Dönüştürür hello parametresi tooa boolean.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |dize veya int |değer tooconvert tooa hello boolean. |

### <a name="return-value"></a>Dönüş değeri
Merhaba, bir Boole değeri dönüştürülür.

### <a name="examples"></a>Örnekler

örnekte gösterildiği nasıl aşağıdaki hello toouse bool bir string veya tamsayı.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "trueString": {
            "value": "[bool('true')]",
            "type" : "bool"
        },
        "falseString": {
            "value": "[bool('false')]",
            "type" : "bool"
        },
        "trueInt": {
            "value": "[bool(1)]",
            "type" : "bool"
        },
        "falseInt": {
            "value": "[bool(0)]",
            "type" : "bool"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| trueString | bool | True |
| falseString | bool | False |
| trueInt | bool | True |
| falseInt | bool | False |

## <a name="if"></a>Eğer
`if(condition, trueValue, falseValue)`

Bir değer olup olmadığına göre göre döndürür bir koşul true veya false.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| Koşul |Evet |Boole değeri |doğru olup olmadığını değeri toocheck hello. |
| trueValue |Evet | dize, int, nesne veya dizi |Merhaba koşulun doğru olması durumunda hello değeri tooreturn. |
| false değerini |Evet | dize, int, nesne veya dizi |Merhaba koşul yanlış olduğunda hello değeri tooreturn. |

### <a name="return-value"></a>Dönüş değeri

İkinci parametre ilk parametre olduğunda döndürür **True**; Aksi halde, üçüncü parametre döndürür.

### <a name="remarks"></a>Açıklamalar

Bu işlev tooconditionally kümesi bir kaynak özelliğini kullanabilirsiniz. Merhaba aşağıdaki örnekte tam bir şablon değildir, ancak koşullu hello kullanılabilirlik kümesi ayarlamak için ilgili bölümleri hello gösterir.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "availabilitySet": {
            "type": "string",
            "allowedValues": [
                "yes",
                "no"
            ]
        }
    },
    "variables": {
        ...
        "availabilitySetName": "availabilitySet1",
        "availabilitySet": {
            "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
        }
    },
    "resources": [
        {
            "condition": "[equals(parameters('availabilitySet'),'yes')]",
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            ...
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "properties": {
                "availabilitySet": "[if(equals(parameters('availabilitySet'),'yes'), variables('availabilitySet'), json('null'))]",
                ...
            }
        },
        ...
    ],
    ...
}
```

### <a name="examples"></a>Örnekler

örnekte gösterildiği nasıl aşağıdaki hello toouse hello `if` işlevi.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "yesOutput": {
            "type": "string",
            "value": "[if(equals('a', 'a'), 'yes', 'no')]"
        },
        "noOutput": {
            "type": "string",
            "value": "[if(equals('a', 'b'), 'yes', 'no')]"
        }
    }
}
```

Örnek önceki hello Hello çıktısı şöyledir:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| yesOutput | Dize | Evet |
| noOutput | Dize | Yok |


## <a name="not"></a>değil
`not(arg1)`

Boole değeri tooits dönüştürür ters değeri.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |Boole değeri |Merhaba değeri tooconvert. |


### <a name="return-value"></a>Dönüş değeri

Döndürür **True** parametresi olduğunda **False**. Döndürür **False** parametresi olduğunda **doğru**.

### <a name="examples"></a>Örnekler

örnekte gösterildiği nasıl aşağıdaki hello toouse mantıksal işlevleri.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

Örnek önceki hello Hello çıktısı şöyledir:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| andExampleOutput | bool | False |
| orExampleOutput | bool | True |
| notExampleOutput | bool | False |

Merhaba aşağıdaki örnek kullanır **değil** ile [eşittir](resource-group-template-functions-comparison.md#equals).

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


## <a name="or"></a>or
`or(arg1, arg2)`

Her iki parametre değeri doğru olup olmadığını denetler.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |Boole değeri |ilk değer toocheck olup hello doğrudur. |
| arg2 |Evet |Boole değeri |İkinci değer toocheck olup hello doğrudur. |

### <a name="return-value"></a>Dönüş değeri

Döndürür **True** ya da değeri geçerliyse true, aksi takdirde **False**.

### <a name="examples"></a>Örnekler

örnekte gösterildiği nasıl aşağıdaki hello toouse mantıksal işlevleri.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

Örnek önceki hello Hello çıktısı şöyledir:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| andExampleOutput | bool | False |
| orExampleOutput | bool | True |
| notExampleOutput | bool | False |


## <a name="next-steps"></a>Sonraki adımlar
* Bir Azure Resource Manager şablonu hello bölümlerde açıklaması için bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).
* birden fazla şablon toomerge bkz [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).
* tooiterate belirtilen sayıda kaynak türünü oluştururken bkz [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).
* toodeploy hello şablonu oluşturduğunuz toosee bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).

