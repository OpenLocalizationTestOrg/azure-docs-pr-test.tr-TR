---
title: "dize aaaAzure Resource Manager şablonu işlevleri - | Microsoft Docs"
description: "Bir Azure Resource Manager şablonu toowork dizeler içindeki Hello işlevleri toouse açıklar."
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
ms.openlocfilehash: 27f7f6a52cbe4e9915718184433e92ca92999346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a>Azure Resource Manager şablonları için dize işlevleri

Resource Manager Dizelerle çalışmaya yönelik işlevler aşağıdaki hello sunar:

* [Base64](#base64)
* [base64ToJson](#base64tojson)
* [base64ToString](#base64tostring)
* [concat](#concat)
* [içerir](#contains)
* [dataUri](#datauri)
* [dataUriToString](#datauritostring)
* [boş](#empty)
* [endsWith](#endswith)
* [ilk](#first)
* [IndexOf](#indexof)
* [Son](#last)
* [lastIndexOf](#lastindexof)
* [uzunluğu](#length)
* [padLeft](#padleft)
* [Değiştir](#replace)
* [Atla](#skip)
* [split](#split)
* [startsWith](resource-group-template-functions-string.md#startswith)
* [dize](#string)
* [substring](#substring)
* [Al](#take)
* [toLower](#tolower)
* [toUpper](#toupper)
* [Kırpma](#trim)
* [uniqueString](#uniquestring)
* [URI](#uri)
* [uriComponent](resource-group-template-functions-string.md#uricomponent)
* [uriComponentToString](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a>Base64
`base64(inputString)`

Base64 hello giriş dize gösterimini döndürür hello.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| inputString |Evet |Dize |değer tooreturn base64 gösterimi olarak hello. |

### <a name="return-value"></a>Dönüş değeri

Merhaba base64 gösterimi içeren bir dize.

### <a name="examples"></a>Örnekler

Aşağıdaki örnek hello nasıl toouse hello base64 işlevi gösterir.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| base64Output | Dize | b25lLCB0d28sIHRocmVl |
| toStringOutput | Dize | Bir iki üç |
| toJsonOutput | Nesne | {"bir": "a", "iki": "b"} |

<a id="base64tojson" />

## <a name="base64tojson"></a>base64ToJson
`base64tojson`

Bir base64 gösterimi tooa JSON nesnesi dönüştürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| base64value değeri |Evet |Dize |Merhaba base64 gösterimi tooconvert tooa JSON nesnesi. |

### <a name="return-value"></a>Dönüş değeri

Bir JSON nesnesi.

### <a name="examples"></a>Örnekler

Merhaba aşağıdaki örnek hello base64ToJson işlevi tooconvert bir base64 değeri kullanır:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| base64Output | Dize | b25lLCB0d28sIHRocmVl |
| toStringOutput | Dize | Bir iki üç |
| toJsonOutput | Nesne | {"bir": "a", "iki": "b"} |

<a id="base64tostring" />

## <a name="base64tostring"></a>base64ToString
`base64ToString(base64Value)`

Bir base64 gösterimi tooa dizesini sayıya dönüştürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| base64value değeri |Evet |Dize |Merhaba base64 gösterimi tooconvert tooa dizesi. |

### <a name="return-value"></a>Dönüş değeri

Dönüştürülen bir base64 değeri hello dizesi.

### <a name="examples"></a>Örnekler

Merhaba aşağıdaki örnek hello base64ToString işlevi tooconvert bir base64 değeri kullanır:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| base64Output | Dize | b25lLCB0d28sIHRocmVl |
| toStringOutput | Dize | Bir iki üç |
| toJsonOutput | Nesne | {"bir": "a", "iki": "b"} |



<a id="concat" />

## <a name="concat"></a>concat
`concat (arg1, arg2, arg3, ...)`

Birden çok dize değerlerini birleştirir ve hello birleştirilmiş dizeyi döndürür veya birden çok birleştirir ve birleştirilmiş hello dizisi döndürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |dize veya dizi |Merhaba birleştirme için ilk değer. |
| Ek bağımsız değişkenler |Hayır |Dize |Birleştirme için sıralı bir düzende ek değerler. |

### <a name="return-value"></a>Dönüş değeri
Bir dize veya birleştirilmiş değerleri dizisi.

### <a name="examples"></a>Örnekler

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

<a id="contains" />

## <a name="contains"></a>içerir
`contains (container, itemToFind)`

Bir değer dizisini içerir, bir nesne bir anahtar veya bir dize bir alt dizeyi içeren olup olmadığını denetler.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| kapsayıcı |Evet |dizi, nesne veya dize |Merhaba değeri toofind içeren hello değeri. |
| itemToFind |Evet |dize veya int |Merhaba değeri toofind. |

### <a name="return-value"></a>Dönüş değeri

**Doğru** hello öğe bulunduysa, **False**.

### <a name="examples"></a>Örnekler

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

<a id="datauri" />

## <a name="datauri"></a>dataUri
`dataUri(stringToConvert)`

Bir değer tooa verisi URI dönüştürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| stringToConvert |Evet |Dize |Merhaba değeri tooconvert tooa veri URI'si. |

### <a name="return-value"></a>Dönüş değeri

Veri URI'si biçimlendirilmiş bir dize.

### <a name="examples"></a>Örnekler

Aşağıdaki örneğine hello değeri tooa verileri URI dönüştürür ve verileri URI tooa dize dönüştürür:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| dataUriOutput | Dize | Veri: metin / düz; charset = utf8; base64, SGVsbG8 = |
| toStringOutput | Dize | Merhaba Dünya! |

<a id="datauritostring" />

## <a name="datauritostring"></a>dataUriToString
`dataUriToString(dataUriToConvert)`

Biçimlendirilmiş değer tooa dize veri URI dönüştürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| dataUriToConvert |Evet |Dize |Merhaba veri URI tooconvert değeri. |

### <a name="return-value"></a>Dönüş değeri

Merhaba içeren bir dize değeri dönüştürülür.

### <a name="examples"></a>Örnekler

Aşağıdaki örneğine hello değeri tooa verileri URI dönüştürür ve verileri URI tooa dize dönüştürür:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| dataUriOutput | Dize | Veri: metin / düz; charset = utf8; base64, SGVsbG8 = |
| toStringOutput | Dize | Merhaba Dünya! |

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

### <a name="examples"></a>Örnekler

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

<a id="endswith" />

## <a name="endswith"></a>endsWith
`endsWith(stringToSearch, stringToFind)`

Bir dize değeri ile bitip olup olmadığını belirler. Merhaba karşılaştırma büyük/küçük harf duyarlıdır.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| stringToSearch |Evet |Dize |Merhaba öğesi toofind içeren hello değeri. |
| stringToFind |Evet |Dize |Merhaba değeri toofind. |

### <a name="return-value"></a>Dönüş değeri

**Doğru** hello son karakter veya hello dizenin karakter hello değeri; eşleşiyorsa Aksi halde, **False**.

### <a name="examples"></a>Örnekler

Aşağıdaki örnek hello nasıl toouse hello startsWith ve endsWith işlevleri gösterir:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| startsTrue | bool | True |
| startsCapTrue | bool | True |
| startsFalse | bool | False |
| endsTrue | bool | True |
| endsCapTrue | bool | True |
| endsFalse | bool | False |

<a id="first" />

## <a name="first"></a>ilk
`first(arg1)`

Merhaba dizenin ilk karakter ya da hello dizisinin ilk öğesi döndürür hello.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |dizi veya dize |Merhaba değeri tooretrieve hello ilk öğe veya karakter. |

### <a name="return-value"></a>Dönüş değeri

Hello ilk karakter ya da dizi hello ilk öğesinin hello türü (dize, int, dizi veya nesne) dizesi.

### <a name="examples"></a>Örnekler

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

<a id="indexof" />

## <a name="indexof"></a>IndexOf
`indexOf(stringToSearch, stringToFind)`

Dize içinde bir değerin ilk konumunu döndürür hello. Merhaba karşılaştırma büyük/küçük harf duyarlıdır.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| stringToSearch |Evet |Dize |Merhaba öğesi toofind içeren hello değeri. |
| stringToFind |Evet |Dize |Merhaba değeri toofind. |

### <a name="return-value"></a>Dönüş değeri

Merhaba öğesi toofind hello konumunu temsil eden bir tamsayı. Merhaba sıfır tabanlı bir değerdir. Merhaba öğesi bulunmazsa -1 döndürülür.

### <a name="examples"></a>Örnekler

Aşağıdaki örnek hello nasıl toouse hello IndexOf ve lastIndexOf işlevleri gösterir:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| firstT | Int | 0 |
| lastT | Int | 3 |
| firstString | Int | 2 |
| lastString | Int | 0 |
| notFound | Int | -1 |

<a id="last" />

## <a name="last"></a>Son
`last (arg1)`

Son hello dizenin karakter ya da hello dizisinin hello son öğesi döndürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |dizi veya dize |Merhaba değeri tooretrieve hello son öğesi veya karakter. |

### <a name="return-value"></a>Dönüş değeri

Merhaba son karakter ya da dizi hello son öğesinin hello türü (dize, int, dizi veya nesne) dizesi.

### <a name="examples"></a>Örnekler

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

<a id="lastindexof" />

## <a name="lastindexof"></a>lastIndexOf
`lastIndexOf(stringToSearch, stringToFind)`

Değer bir dize içinde son konumunu döndürür hello. Merhaba karşılaştırma büyük/küçük harf duyarlıdır.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| stringToSearch |Evet |Dize |Merhaba öğesi toofind içeren hello değeri. |
| stringToFind |Evet |Dize |Merhaba değeri toofind. |

### <a name="return-value"></a>Dönüş değeri

Merhaba son hello öğesi toofind konumunu temsil eden bir tamsayı. Merhaba sıfır tabanlı bir değerdir. Merhaba öğesi bulunmazsa -1 döndürülür.

### <a name="examples"></a>Örnekler

Aşağıdaki örnek hello nasıl toouse hello IndexOf ve lastIndexOf işlevleri gösterir:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| firstT | Int | 0 |
| lastT | Int | 3 |
| firstString | Int | 2 |
| lastString | Int | 0 |
| notFound | Int | -1 |

<a id="length" />

## <a name="length"></a>uzunluğu
`length(string)`

Bir dize veya bir dizideki öğeler Hello karakterlerin sayısını döndürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |dizi veya dize |öğe sayısını hello alma dizi toouse hello veya karakter sayısını hello alma dizesi toouse hello. |

### <a name="return-value"></a>Dönüş değeri

İnt 

### <a name="examples"></a>Örnekler

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

<a id="padleft" />

## <a name="padleft"></a>PadLeft
`padLeft(valueToPad, totalLength, paddingCharacter)`

Merhaba toplam belirtilen uzunluk ulaşmasını kadar karakterleri toohello sol ekleyerek sağa hizalı dize döndürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| valueToPad |Evet |dize veya int |değer tooright hello-hizalayın. |
| totalLength |Evet |Int |Merhaba toplam hello karakter sayısını dizesi döndürdü. |
| paddingCharacter |Hayır |tek bir karakter |Sol-Doldurma hello toplam uzunluğu ulaşılana kadar için karakter toouse hello. bir alanı Hello varsayılan değerdir. |

Hello özgün dizeye hello karakter toopad sayısından daha uzun olması durumunda hiçbir karakter eklenir.

### <a name="return-value"></a>Dönüş değeri

Belirtilen karakter sayısı en az hello bir dize.

### <a name="examples"></a>Örnekler

Aşağıdaki örnek hello nasıl toopad hello kullanıcı tarafından sağlanan parametre değeri hello ekleyerek sıfır karakter hello toplam karakter sayısı ulaşana kadar gösterir. 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123"
        }
    },
    "resources": [],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[padLeft(parameters('testString'),10,'0')]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| stringOutput | Dize | 0000000123 |

<a id="replace" />

## <a name="replace"></a>Değiştir
`replace(originalString, oldString, newString)`

Başka bir dizeyle yerine tek bir dize tüm örneklerini içeren yeni bir dize döndürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| originalString |Evet |Dize |başka bir dizeyle yerine bir dizesinin tüm örnekleri olan hello değeri. |
| oldString |Evet |Dize |Merhaba dize toobe hello özgün dizeden kaldırıldı. |
| newString |Evet |Dize |Merhaba dize tooadd hello yerine dize kaldırıldı. |

### <a name="return-value"></a>Dönüş değeri

Bir dizeyle hello karakterleri değiştirildi.

### <a name="examples"></a>Örnekler

Aşağıdaki örneğine hello nasıl tooremove tüm hello kullanıcı tarafından sağlanan dizeden tireler ve nasıl hello tooreplace parçası dize başka bir dizeyle gösterir.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123-123-1234"
        }
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'-', '')]"
        },
        "secodeOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'1234', 'xxxx')]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| firstOutput | Dize | 1231231234 |
| secodeOutput | Dize | 123-123-xxxx |

<a id="skip" />

## <a name="skip"></a>Atla
`skip(originalValue, numberToSkip)`

Merhaba öğe sayısını belirtilen sonra hello sayıda karakter veya bir dizi tüm hello ile belirtilen öğelerin sonra tüm hello karakterler içeren bir dize döndürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| originalValue |Evet |dizi veya dize |atlanıyor hello dizisi veya dize toouse. |
| numberToSkip |Evet |Int |öğeleri veya karakter tooskip Hello sayısı. Bu değer 0 veya daha az ise, tüm öğeleri hello veya karakter hello değeri döndürülür. Merhaba dizisi veya dize hello uzunluğundan büyük olursa, boş dize veya dize döndürülür. |

### <a name="return-value"></a>Dönüş değeri

Bir dizi veya dize.

### <a name="examples"></a>Örnekler

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

<a id="split" />

## <a name="split"></a>split
`split(inputString, delimiter)`

Sınırlayıcılar belirtilen hello tarafından ayrılmış dize hello alt dizeler hello birini içeren bir dizeler dizisi giriş döndürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| inputString |Evet |Dize |Merhaba dize toosplit. |
| sınırlayıcı |Evet |dize veya dize dizisi |Merhaba dize bölmek için sınırlayıcı toouse hello. |

### <a name="return-value"></a>Dönüş değeri

Bir dizeler dizisi.

### <a name="examples"></a>Örnekler

Merhaba aşağıdaki örnek hello giriş dizesi virgül ile virgül veya noktalı virgül ile böler.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstString": {
            "type": "string",
            "defaultValue": "one,two,three"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "one;two,three"
        }
    },
    "variables": {
        "delimiters": [ ",", ";" ]
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "array",
            "value": "[split(parameters('firstString'),',')]"
        },
        "secondOutput": {
            "type": "array",
            "value": "[split(parameters('secondString'),variables('delimiters'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| firstOutput | Dizi | ["bir", "iki", "üç"] |
| secondOutput | Dizi | ["bir", "iki", "üç"] |

<a id="startswith" />

## <a name="startswith"></a>startsWith
`startsWith(stringToSearch, stringToFind)`

Bir dize değeri ile başlayıp başlamadığını belirler. Merhaba karşılaştırma büyük/küçük harf duyarlıdır.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| stringToSearch |Evet |Dize |Merhaba öğesi toofind içeren hello değeri. |
| stringToFind |Evet |Dize |Merhaba değeri toofind. |

### <a name="return-value"></a>Dönüş değeri

**Doğru** hello ilk karakterin veya karakter hello dizesinin hello değeri; eşleşiyorsa Aksi halde, **False**.

### <a name="examples"></a>Örnekler

Aşağıdaki örnek hello nasıl toouse hello startsWith ve endsWith işlevleri gösterir:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| startsTrue | bool | True |
| startsCapTrue | bool | True |
| startsFalse | bool | False |
| endsTrue | bool | True |
| endsCapTrue | bool | True |
| endsFalse | bool | False |

<a id="string" />

## <a name="string"></a>Dize
`string(valueToConvert)`

Belirtilen değer tooa dize dönüştürür hello.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| valueToConvert |Evet | Herhangi biri |Merhaba değeri tooconvert toostring. Nesneler ve diziler dahil olmak üzere herhangi türde bir değer dönüştürülebilir. |

### <a name="return-value"></a>Dönüş değeri

Dönüştürülen değer hello dizesi.

### <a name="examples"></a>Örnekler

Aşağıdaki örnek hello nasıl tooconvert farklı türlerde değerler toostrings gösterir:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testObject": {
            "type": "object",
            "defaultValue": {
                "valueA": 10,
                "valueB": "Example Text"
            }
        },
        "testArray": {
            "type": "array",
            "defaultValue": [
                "a",
                "b",
                "c"
            ]
        },
        "testInt": {
            "type": "int",
            "defaultValue": 5
        }
    },
    "resources": [],
    "outputs": {
        "objectOutput": {
            "type": "string",
            "value": "[string(parameters('testObject'))]"
        },
        "arrayOutput": {
            "type": "string",
            "value": "[string(parameters('testArray'))]"
        },
        "intOutput": {
            "type": "string",
            "value": "[string(parameters('testInt'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| objectOutput | Dize | {"valueA": 10, "valueB": "Örnek metin"} |
| arrayOutput | Dize | ["a", "b", "c"] |
| intOutput | Dize | 5 |

<a id="substring" />

## <a name="substring"></a>substring
`substring(stringToParse, startIndex, length)`

Belirtilen hello başlar konumu karakter ve hello içeren bir alt dizenin belirtilen karakter sayısını döndürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| stringToParse |Evet |Dize |hangi hello alt dizenin ayıklanacağı hello özgün dizesi. |
| startIndex |Hayır |Int |Merhaba sıfır tabanlı başlangıç karakteri konumu hello substring. |
| uzunluğu |Hayır |Int |Merhaba hello substring karakter sayısı. Merhaba dize içinde tooa konuma başvurmalıdır. |

### <a name="return-value"></a>Dönüş değeri

Merhaba substring.

### <a name="remarks"></a>Açıklamalar

Merhaba substring hello dize hello sonunu aşan genişletir hello işlevi başarısız oluyor. Merhaba hata "Merhaba dizin ve uzunluk parametreleri hello dize içinde tooa konuma başvurmalıdır ile. aşağıdaki örneğine hello başarısız Merhaba dizin parametresi: '0' hello uzunluk parametresi: '11' hello hello dize parametresinin uzunluğu: '10'. ".

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a>Örnekler

Aşağıdaki örneğine hello bir alt dizesi bir parametresinden ayıklar.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        }
    },
    "resources": [],
    "outputs": {
        "substringOutput": {
            "value": "[substring(parameters('testString'), 4, 3)]",
            "type": "string"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| substringOutput | Dize | iki |


<a id="take" />

## <a name="take"></a>Al
`take(originalValue, numberToTake)`

Dize başından hello karakter sayısını hello bir dizeyle belirtilen döndürür hello veya hello sahip bir dizi hello dizi hello başından öğelerin sayısı belirtildi.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| originalValue |Evet |dizi veya dize |dizi veya dize tootake hello öğelerinden hello. |
| numberToTake |Evet |Int |öğeleri veya karakter tootake Hello sayısı. Bu değer 0 veya daha az ise, boş dize veya dize döndürülür. Merhaba hello verilen dizi veya dize uzunluğundan büyük olursa, hello dizisi veya dize tüm hello öğeler döndürülür. |

### <a name="return-value"></a>Dönüş değeri

Bir dizi veya dize.

### <a name="examples"></a>Örnekler

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

<a id="tolower" />

## <a name="tolower"></a>toLower
`toLower(stringToChange)`

Dönüştürür hello dize toolower durumu belirtildi.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| stringToChange |Evet |Dize |Merhaba değeri tooconvert toolower durumda. |

### <a name="return-value"></a>Dönüş değeri

Merhaba dize toolower durumda dönüştürülür.

### <a name="examples"></a>Örnekler

Aşağıdaki örneğine hello bir parametre değeri toolower çalışması ve tooupper harfe dönüştürür.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| toLowerOutput | Dize | Bir iki üç |
| toUpperOutput | Dize | BİR İKİ ÜÇ |

<a id="toupper" />

## <a name="toupper"></a>toUpper
`toUpper(stringToChange)`

Dönüştürür hello dize tooupper durumu belirtildi.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| stringToChange |Evet |Dize |Merhaba değeri tooconvert tooupper durumda. |

### <a name="return-value"></a>Dönüş değeri

Merhaba dize tooupper durumda dönüştürülür.

### <a name="examples"></a>Örnekler

Aşağıdaki örneğine hello bir parametre değeri toolower çalışması ve tooupper harfe dönüştürür.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| toLowerOutput | Dize | Bir iki üç |
| toUpperOutput | Dize | BİR İKİ ÜÇ |

<a id="trim" />

## <a name="trim"></a>Kırpma
`trim (stringToTrim)`

Belirtilen dize tüm öndeki ve sondaki boşluk karakterleri hello öğesinden kaldırır.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| stringToTrim |Evet |Dize |Merhaba değeri tootrim. |

### <a name="return-value"></a>Dönüş değeri

Baştaki ve sondaki boşluk karakterleri olmadan hello dizesi.

### <a name="examples"></a>Örnekler

Merhaba aşağıdaki örnek hello parametre hello boşluk karakterlerinden kırpar.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "    one two three   "
        }
    },
    "resources": [],
    "outputs": {
        "return": {
            "type": "string",
            "value": "[trim(parameters('testString'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| Döndür | Dize | Bir iki üç |

<a id="uniquestring" />

## <a name="uniquestring"></a>uniqueString
`uniqueString (baseString, ...)`

Parametre olarak sağlanan hello değerlere göre belirleyici karma dize oluşturur. 

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| baseString |Evet |Dize |Merhaba değeri benzersiz bir dize hello karma işlevi toocreate kullanılır. |
| gerektikçe ek parametreler |Hayır |Dize |Sayıda dizeleri benzersizlik hello düzeyini belirtir gerekli toocreate hello değeri ekleyebilirsiniz. |

### <a name="remarks"></a>Açıklamalar

Bu işlev, toocreate bir kaynak için benzersiz bir ad gerektiğinde faydalıdır. Benzersizlik hello sonucu için hello kapsamını sınırlamak parametre değerlerini sağlayın. Merhaba adı toosubscription, kaynak grubu veya dağıtım aşağı benzersiz olup olmadığını belirtebilirsiniz. 

Merhaba, değer rastgele bir dize değil, ancak bunun yerine bir karma işlevin sonucu hello döndürdü. Merhaba değeri 13 karakter uzunluğunda döndürülür. Genel benzersiz değil. Bir önek ile toocombine hello değeri, adlandırma kuralını toocreate anlamlı bir ad isteyebilirsiniz. Merhaba aşağıdaki örnek döndürülen değer hello hello biçimi gösterir. Merhaba gerçek değer parametreleri sağlanan hello göre değişir.

    tcvhiyu5h2o5o

Örnek hello nasıl toouse uniqueString toocreate benzersiz bir değer için yaygın olarak kullanılan düzeylerini gösterir.

Benzersiz kapsamlı toosubscription

```json
"[uniqueString(subscription().subscriptionId)]"
```

Benzersiz kapsamlı tooresource grubu

```json
"[uniqueString(resourceGroup().id)]"
```

Bir kaynak grubu için benzersiz kapsamlı toodeployment

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

Aşağıdaki örnek hello nasıl toocreate bir depolama hesabı için benzersiz bir ad, kaynak grubuna göre gösterir. Merhaba kaynak grubu içinde hello adı hello oluşturulan varsa benzersiz değil aynı şekilde.

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a>Dönüş değeri

13 karakter içeren bir dize.

### <a name="examples"></a>Örnekler

Aşağıdaki örneğine hello uniquestring sonuçları döndürür:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "uniqueRG": {
            "value": "[uniqueString(resourceGroup().id)]",
            "type" : "string"
        },
        "uniqueDeploy": {
            "value": "[uniqueString(resourceGroup().id, deployment().name)]",
            "type" : "string"
        }
    }
}
```

<a id="uri" />

## <a name="uri"></a>URI
`uri (baseUri, relativeUri)`

Merhaba tabanURI ve hello relativeUri dize birleştirerek bir mutlak URI oluşturur.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| tabanURI |Evet |Dize |Merhaba taban URI dizesi. |
| relativeUri |Evet |Dize |Merhaba göreli URI dize tooadd toohello taban URI dize. |

Merhaba hello için değer **tabanURI** parametresi, belirli bir dosya içerebilir, ancak yalnızca hello temel yolu hello URI oluşturulurken kullanılır. Örneğin, geçirme `http://contoso.com/resources/azuredeploy.json` temel URI'sini hello tabanURI parametre sonuç olarak `http://contoso.com/resources/`.

### <a name="return-value"></a>Dönüş değeri

Merhaba temel ve göreli değerleri için mutlak URI hello temsil eden dize.

### <a name="examples"></a>Örnekler

Aşağıdaki örnek hello nasıl tooconstruct bağlantı tooa iç içe geçmiş şablonu hello üst şablonunun hello değere göre gösterir.

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

örnekte gösterildiği nasıl aşağıdaki hello toouse URI, uriComponent ve uriComponentToString:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| uriOutput | Dize | http://contoso.com/resources/Nested/azuredeploy.JSON |
| componentOutput | Dize | HTTP%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON |
| toStringOutput | Dize | http://contoso.com/resources/Nested/azuredeploy.JSON |

<a id="uricomponent" />

## <a name="uricomponent"></a>uriComponent
`uricomponent(stringToEncode)`

Bir URI kodlar.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| stringToEncode |Evet |Dize |Merhaba değeri tooencode. |

### <a name="return-value"></a>Dönüş değeri

Merhaba URI dizesi değeri kodlanmış.

### <a name="examples"></a>Örnekler

örnekte gösterildiği nasıl aşağıdaki hello toouse URI, uriComponent ve uriComponentToString:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| uriOutput | Dize | http://contoso.com/resources/Nested/azuredeploy.JSON |
| componentOutput | Dize | HTTP%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON |
| toStringOutput | Dize | http://contoso.com/resources/Nested/azuredeploy.JSON |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a>uriComponentToString
`uriComponentToString(uriEncodedString)`

Değer bir dize bir URI kodlanmış döndürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| uriEncodedString |Evet |Dize |Merhaba URI değeri tooconvert tooa dizesi kodlanmış. |

### <a name="return-value"></a>Dönüş değeri

Bir URI kodu çözülmüş bir dize değeri kodlanmış.

### <a name="examples"></a>Örnekler

örnekte gösterildiği nasıl aşağıdaki hello toouse URI, uriComponent ve uriComponentToString:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| uriOutput | Dize | http://contoso.com/resources/Nested/azuredeploy.JSON |
| componentOutput | Dize | HTTP%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON |
| toStringOutput | Dize | http://contoso.com/resources/Nested/azuredeploy.JSON |


## <a name="next-steps"></a>Sonraki adımlar
* Bir Azure Resource Manager şablonu hello bölümlerde açıklaması için bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).
* birden fazla şablon toomerge bkz [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).
* tooiterate belirtilen sayıda kaynak türünü oluştururken bkz [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).
* toodeploy hello şablonu oluşturduğunuz toosee bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).

