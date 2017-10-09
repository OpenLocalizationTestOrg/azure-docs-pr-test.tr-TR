---
title: "aaaAzure Resource Manager şablonu işlevleri - diziler ve nesneleri | Microsoft Docs"
description: "Diziler ve nesneleri ile çalışmak için bir Azure Resource Manager şablonunda Hello işlevleri toouse açıklar."
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
ms.date: 06/12/2017
ms.author: tomfitz
ms.openlocfilehash: e5f1a9b2a71039562eae7e48c2474a1fa59a7bea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a>Dizi ve nesne işlevleri için Azure Resource Manager şablonları 

Kaynak Yöneticisi, nesneler ve diziler ile çalışmak için birkaç işlevleri sağlar.

* [dizi](#array)
* [birleşim](#coalesce)
* [concat](#concat)
* [içerir](#contains)
* [createArray](#createarray)
* [boş](#empty)
* [ilk](#first)
* [kesişim](#intersection)
* [JSON](#json)
* [Son](#last)
* [uzunluğu](#length)
* [Min](#min)
* [max](#max)
* [Aralık](#range)
* [Atla](#skip)
* [Al](#take)
* [birleşim](#union)

tooget dize değerlerini bir değer ile ayrılmış bir dizi bkz [bölme](resource-group-template-functions-string.md#split).

<a id="array" />

## <a name="array"></a>Dizi
`array(convertToArray)`

Hello değeri tooan dizisine dönüştürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| convertToArray |Evet |int, string, dizi veya nesne |Merhaba değeri tooconvert tooan dizisi. |

### <a name="return-value"></a>Dönüş değeri

Bir dizi.

### <a name="example"></a>Örnek

Merhaba aşağıdaki örnekte nasıl toouse hello dizi işlevi farklı türler ile gösterilir.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "intToConvert": {
            "type": "int",
            "defaultValue": 1
        },
        "stringToConvert": {
            "type": "string",
            "defaultValue": "a"
        },
        "objectToConvert": {
            "type": "object",
            "defaultValue": {"a": "b", "c": "d"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "intOutput": {
            "type": "array",
            "value": "[array(parameters('intToConvert'))]"
        },
        "stringOutput": {
            "type": "array",
            "value": "[array(parameters('stringToConvert'))]"
        },
        "objectOutput": {
            "type": "array",
            "value": "[array(parameters('objectToConvert'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| intOutput | Dizi | [1] |
| stringOutput | Dizi | ["a"] |
| objectOutput | Dizi | [{"a": "b", "c": "d"}] |

<a id="coalesce" />

## <a name="coalesce"></a>birleşim
`coalesce(arg1, arg2, arg3, ...)`

İlk değeri null olmayan hello parametrelerinden döndürür. Boş dizeler, boş diziler ve boş nesneleri null değil.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |int, string, dizi veya nesne |Merhaba ilk değer tootest, null. |
| Ek bağımsız değişken |Hayır |int, string, dizi veya nesne |Ek değerler tootest, null. |

### <a name="return-value"></a>Dönüş değeri

dize, int, dizi veya nesne olabilen hello ilk null olmayan parametreleri, başlangıç değeri. Tüm parametreleri null ise null. 

### <a name="example"></a>Örnek

Merhaba aşağıdaki örnek birleşim farklı kullanımlarını hello çıktısını gösterir.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {
                "null1": null, 
                "null2": null,
                "string": "default",
                "int": 1,
                "object": {"first": "default"},
                "array": [1]
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').string)]"
        },
        "intOutput": {
            "type": "int",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').int)]"
        },
        "objectOutput": {
            "type": "object",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').object)]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').array)]"
        },
        "emptyOutput": {
            "type": "bool",
            "value": "[empty(coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| stringOutput | Dize | Varsayılan |
| intOutput | Int | 1 |
| objectOutput | Nesne | {"ilk": "varsayılan"} |
| arrayOutput | Dizi | [1] |
| emptyOutput | bool | True |

<a id="concat" />

## <a name="concat"></a>concat
`concat(arg1, arg2, arg3, ...)`

Birden çok döndürür birleştirilmiş hello dizisi ve diziler birleştirir veya birden çok dize değerlerini birleştirir ve hello birleştirilmiş dizeyi döndürür. 

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |dizi veya dize |ilk dizi veya dize birleştirme için hello. |
| Ek bağımsız değişkenler |Hayır |dizi veya dize |Ek diziler veya birleştirme için sıralı bir düzende dizeleri. |

Bu işlev bağımsız değişkenleri herhangi bir sayıda alabilir ve dizeler veya diziler için başlangıç parametreleri kabul edebilir.

### <a name="return-value"></a>Dönüş değeri
Bir dize veya birleştirilmiş değerleri dizisi.

### <a name="example"></a>Örnek

Aşağıdaki örnek hello nasıl toocombine iki dizi gösterir.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "firstArray": { 
            "type": "array", 
            "defaultValue": [ 
                "1-1", 
                "1-2", 
                "1-3" 
            ] 
        },
        "secondArray": {
            "type": "array", 
            "defaultValue": [ 
                "2-1", 
                "2-2",
                "2-3" 
            ] 
        }
    },
    "resources": [
    ],
    "outputs": {
        "return": {
            "type": "array",
            "value": "[concat(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| Döndür | Dizi | ["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"] |

Aşağıdaki örnek hello nasıl toocombine iki string değerleri ve birleştirilmiş dizeyi döndürür gösterir.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "prefix": {
            "type": "string",
            "defaultValue": "prefix"
        }
    },
    "resources": [],
    "outputs": {
        "concatOutput": {
            "value": "[concat(parameters('prefix'), '-', uniqueString(resourceGroup().id))]",
            "type" : "string"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| concatOutput | Dize | önek 5yj4yjf5mbg72 |

<a id="contains" />

## <a name="contains"></a>içerir
`contains(container, itemToFind)`

Bir değer dizisini içerir, bir nesne bir anahtar veya bir dize bir alt dizeyi içeren olup olmadığını denetler.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| kapsayıcı |Evet |dizi, nesne veya dize |Merhaba değeri toofind içeren hello değeri. |
| itemToFind |Evet |dize veya int |Merhaba değeri toofind. |

### <a name="return-value"></a>Dönüş değeri

**Doğru** hello öğe bulunduysa, **False**.

### <a name="example"></a>Örnek

Merhaba aşağıdaki örnekte nasıl toouse farklı türleriyle içeren gösterilmektedir:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "OneTwoThree"
        },
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringTrue": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'e')]"
        },
        "stringFalse": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'z')]"
        },
        "objectTrue": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'one')]"
        },
        "objectFalse": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'a')]"
        },
        "arrayTrue": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'three')]"
        },
        "arrayFalse": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'four')]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| stringTrue | bool | True |
| stringFalse | bool | False |
| objectTrue | bool | True |
| objectFalse | bool | False |
| arrayTrue | bool | True |
| arrayFalse | bool | False |

<a id="createarray" />

## <a name="createarray"></a>createarray
`createArray (arg1, arg2, arg3, ...)`

Bir dizi hello parametrelerinden oluşturur.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |Dize, tamsayı, dizi veya nesne |Merhaba hello dizinin ilk değer. |
| Ek bağımsız değişkenler |Hayır |Dize, tamsayı, dizi veya nesne |Merhaba dizisinde ek değerler. |

### <a name="return-value"></a>Dönüş değeri

Bir dizi.

### <a name="example"></a>Örnek

örnekte gösterildiği nasıl aşağıdaki hello toouse createArray farklı türler ile:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringArray": {
            "type": "array",
            "value": "[createArray('a', 'b', 'c')]"
        },
        "intArray": {
            "type": "array",
            "value": "[createArray(1, 2, 3)]"
        },
        "objectArray": {
            "type": "array",
            "value": "[createArray(parameters('objectToTest'))]"
        },
        "arrayArray": {
            "type": "array",
            "value": "[createArray(parameters('arrayToTest'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| stringArray | Dizi | ["a", "b", "c"] |
| int | Dizi | [1, 2, 3] |
| objectArray | Dizi | [{"bir": "a", "iki": "b", "üç": "c"}] |
| arrayArray | Dizi | [["bir", "iki", "üç"]] |

<a id="empty" />

## <a name="empty"></a>boş

`empty(itemToTest)`

Bir dizi, nesne veya dize boş olup olmadığını belirler.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| itemToTest |Evet |dizi, nesne veya dize |boş ise, değer toocheck hello. |

### <a name="return-value"></a>Dönüş değeri

Döndürür **True** hello değeriyse, boş, aksi takdirde **False**.

### <a name="example"></a>Örnek

Aşağıdaki örneğine hello bir dizi, nesne ve dize boş olup olmadığını denetler.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": []
        },
        "testObject": {
            "type": "object",
            "defaultValue": {}
        },
        "testString": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testArray'))]"
        },
        "objectEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testObject'))]"
        },
        "stringEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testString'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| arrayEmpty | bool | True |
| objectEmpty | bool | True |
| stringEmpty | bool | True |

<a id="first" />

## <a name="first"></a>ilk
`first(arg1)`

Merhaba dizisinin ilk öğesi ya da hello dize ilk karakteri döndürür hello.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |dizi veya dize |Merhaba değeri tooretrieve hello ilk öğe veya karakter. |

### <a name="return-value"></a>Dönüş değeri

bir dizi ya da ilk karakteri bir dize hello hello ilk öğesinin Hello türü (dize, int, dizi veya nesne).

### <a name="example"></a>Örnek

Merhaba aşağıdaki örnekte nasıl toouse hello ilk işlevi bir dizi ve dize ile gösterilir.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[first(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[first('One Two Three')]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| arrayOutput | Dize | bir |
| stringOutput | Dize | O |

<a id="intersection" />

## <a name="intersection"></a>kesişim
`intersection(arg1, arg2, arg3, ...)`

Tek bir dizi veya nesne hello ortak öğeler ile Merhaba parametrelerinden döndürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |dizi veya nesne |Ortak öğeler bulmak için ilk değer toouse hello. |
| arg2 |Evet |dizi veya nesne |Ortak öğeler bulmak için ikinci değer toouse hello. |
| Ek bağımsız değişkenler |Hayır |dizi veya nesne |Ortak öğeler bulmak için ek değerler toouse. |

### <a name="return-value"></a>Dönüş değeri

Bir dizi veya nesne hello ortak öğeler ile.

### <a name="example"></a>Örnek

Aşağıdaki örnekte gösterildiği nasıl toouse kesişim diziler hello ve nesneler:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "z", "three": "c"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[intersection(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[intersection(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| objectOutput | Nesne | {"bir": "a", "üç": "c"} |
| arrayOutput | Dizi | ["iki", "üç"] |


## <a name="json"></a>JSON
`json(arg1)`

Bir JSON nesnesi döndürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |Dize |Merhaba değeri tooconvert tooJSON. |


### <a name="return-value"></a>Dönüş değeri

Merhaba Hello JSON nesnesinden belirtilen dize veya boş bir nesneyi zaman **null** belirtilir.

### <a name="example"></a>Örnek

Aşağıdaki örnekte gösterildiği nasıl toouse kesişim diziler hello ve nesneler:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "jsonOutput": {
            "type": "object",
            "value": "[json('{\"a\": \"b\"}')]"
        },
        "nullOutput": {
            "type": "bool",
            "value": "[empty(json('null'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| jsonOutput | Nesne | {"a": "b"} |
| nullOutput | Boole değeri | True |

<a id="last" />

## <a name="last"></a>Son
`last (arg1)`

Merhaba dizisinin son öğesi ya da hello dizenin son karakter döndürür hello.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |dizi veya dize |Merhaba değeri tooretrieve hello son öğesi veya karakter. |

### <a name="return-value"></a>Dönüş değeri

bir dizi ya da hello son karakter bir dizenin hello son öğesinin Hello türü (dize, int, dizi veya nesne).

### <a name="example"></a>Örnek

Merhaba aşağıdaki örnekte nasıl toouse hello son işlevi bir dizi ve dize ile gösterilir.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[last(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[last('One Two Three')]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| arrayOutput | Dize | üç |
| stringOutput | Dize | E |

<a id="length" />

## <a name="length"></a>uzunluğu
`length(arg1)`

Bir dizi ya da bir dizedeki karakter Hello sayıda öğeyi döndürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |dizi veya dize |öğe sayısını hello alma dizi toouse hello veya karakter sayısını hello alma dizesi toouse hello. |

### <a name="return-value"></a>Dönüş değeri

İnt 

### <a name="example"></a>Örnek

örnekte gösterildiği nasıl aşağıdaki hello toouse uzunluğunda bir dizi ve dizesi:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "stringToTest": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "arrayLength": {
            "type": "int",
            "value": "[length(parameters('arrayToTest'))]"
        },
        "stringLength": {
            "type": "int",
            "value": "[length(parameters('stringToTest'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| arrayLength | Int | 3 |
| stringLength | Int | 13 |

Kaynakları oluşturulurken bir dizi toospecify hello yineleme sayısı ile bu işlevi kullanabilirsiniz. Aşağıdaki örneğine hello parametre hello **siteNames** adları toouse tooan dizisi hello web siteleri oluştururken başvurur.

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

Bu işlev bir dizi ile kullanma hakkında daha fazla bilgi için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).

<a id="min" />

## <a name="min"></a>dk
`min(arg1)`

Döndürür dizisi veya virgülle ayrılmış tamsayı listesi en düşük değerden hello.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |dizi tamsayı veya virgülle ayrılmış tamsayı listesi |Merhaba koleksiyonu tooget hello en küçük değer. |

### <a name="return-value"></a>Dönüş değeri

Merhaba en düşük değeri temsil eden bir tamsayı.

### <a name="example"></a>Örnek

örnekte gösterildiği nasıl aşağıdaki hello toouse en az bir dizi ve tamsayı listesi:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[min(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[min(0,3,2,5,4)]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| arrayOutput | Int | 0 |
| intOutput | Int | 0 |

<a id="max" />

## <a name="max"></a>max
`max(arg1)`

En büyük değer dizisi veya virgülle ayrılmış tamsayı listesi döndürür hello.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |dizi tamsayı veya virgülle ayrılmış tamsayı listesi |Merhaba koleksiyonu tooget hello en büyük değer. |

### <a name="return-value"></a>Dönüş değeri

Merhaba en yüksek değeri temsil eden bir tamsayı.

### <a name="example"></a>Örnek

örnekte gösterildiği nasıl aşağıdaki hello toouse bir dizi ve tamsayı listesi ile en fazla:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[max(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[max(0,3,2,5,4)]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| arrayOutput | Int | 5 |
| intOutput | Int | 5 |

<a id="range" />

## <a name="range"></a>Aralık
`range(startingInteger, numberOfElements)`

Dizisi bir tamsayı başlatma ve bir öğe sayısı içeren oluşturur.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| startingInteger |Evet |Int |Merhaba hello dizinin ilk tamsayı. |
| numberofElements |Evet |Int |Merhaba tamsayılar hello dizisindeki sayısı. |

### <a name="return-value"></a>Dönüş değeri

Dizisi.

### <a name="example"></a>Örnek

Aşağıdaki örnek hello nasıl toouse hello aralığı işlevi gösterir:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "startingInt": {
            "type": "int",
            "defaultValue": 5
        },
        "numberOfElements": {
            "type": "int",
            "defaultValue": 3
        }
    },
    "resources": [],
    "outputs": {
        "rangeOutput": {
            "type": "array",
            "value": "[range(parameters('startingInt'),parameters('numberOfElements'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| rangeOutput | Dizi | [5, 6, 7] |

<a id="skip" />

## <a name="skip"></a>Atla
`skip(originalValue, numberToSkip)`

Merhaba numarası hello dizisinde belirtilen veya hello numarası hello dizesinde belirtilen sonra tüm hello karakterler içeren bir dize döndürür sonra tüm hello öğelerine sahip bir dizi döndürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| originalValue |Evet |dizi veya dize |atlanıyor hello dizisi veya dize toouse. |
| numberToSkip |Evet |Int |öğeleri veya karakter tooskip Hello sayısı. Bu değer 0 veya daha az ise, tüm öğeleri hello veya karakter hello değeri döndürülür. Merhaba dizisi veya dize hello uzunluğundan büyük olursa, boş dize veya dize döndürülür. |

### <a name="return-value"></a>Dönüş değeri

Bir dizi veya dize.

### <a name="example"></a>Örnek

Örnek atlar hello aşağıdaki hello hello dizide öğe sayısını belirtilen ve hello bir dizedeki karakter sayısını belirtilen.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToSkip": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToSkip": {
            "type": "int",
            "defaultValue": 4
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[skip(parameters('testArray'),parameters('elementsToSkip'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[skip(parameters('testString'),parameters('charactersToSkip'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| arrayOutput | Dizi | ["üç"] |
| stringOutput | Dize | iki üç |

<a id="take" />

## <a name="take"></a>Al
`take(originalValue, numberToTake)`

Merhaba sahip bir dizi öğelerinden sayısı belirtilen döndürür hello dizi başlangıcı hello veya hello başlangıcından hello dize olan karakter sayısı hello bir dizeyle belirtilen.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| originalValue |Evet |dizi veya dize |dizi veya dize tootake hello öğelerinden hello. |
| numberToTake |Evet |Int |öğeleri veya karakter tootake Hello sayısı. Bu değer 0 veya daha az ise, boş dize veya dize döndürülür. Merhaba hello verilen dizi veya dize uzunluğundan büyük olursa, hello dizisi veya dize tüm hello öğeler döndürülür. |

### <a name="return-value"></a>Dönüş değeri

Bir dizi veya dize.

### <a name="example"></a>Örnek

Örnek alır hello aşağıdaki hello hello dizisinden öğeleri ve bir dizeden karakterleri sayısı belirtilmiş.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToTake": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToTake": {
            "type": "int",
            "defaultValue": 2
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[take(parameters('testArray'),parameters('elementsToTake'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[take(parameters('testString'),parameters('charactersToTake'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| arrayOutput | Dizi | ["", "iki"] |
| stringOutput | Dize | üzerinde |

<a id="union" />

## <a name="union"></a>birleşim
`union(arg1, arg2, arg3, ...)`

Tek bir dizi veya nesne tüm öğelerle hello parametrelerinden döndürür. Yinelenen değerler veya anahtarlar, yalnızca bir kez dahil.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |dizi veya nesne |öğeleri katılmak için ilk değer toouse hello. |
| arg2 |Evet |dizi veya nesne |öğeleri katılmak için ikinci değer toouse hello. |
| Ek bağımsız değişkenler |Hayır |dizi veya nesne |Öğeleri katılmak için ek değerler toouse. |

### <a name="return-value"></a>Dönüş değeri

Bir dizi veya nesne.

### <a name="example"></a>Örnek

Aşağıdaki örnekte gösterildiği nasıl toouse birleşim diziler hello ve nesneler:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"three": "c", "four": "d", "five": "e"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["three", "four"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[union(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[union(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| objectOutput | Nesne | {"bir": "a", "iki": "b", "üç": "c", "dört": "d", "beş": "e"} |
| arrayOutput | Dizi | ["bir", "iki", "üç", "dört"] |

## <a name="next-steps"></a>Sonraki adımlar
* Bir Azure Resource Manager şablonu hello bölümlerde açıklaması için bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).
* birden fazla şablon toomerge bkz [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).
* tooiterate belirtilen sayıda kaynak türünü oluştururken bkz [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).
* toodeploy hello şablonu oluşturduğunuz toosee bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).

