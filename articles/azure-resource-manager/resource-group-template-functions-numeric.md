---
title: "aaaAzure Resource Manager şablonu işlevleri - sayısal | Microsoft Docs"
description: "Bir Azure Resource Manager şablonu toowork içinde Hello işlevleri toouse numaralarıyla açıklar."
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
ms.openlocfilehash: 855d5b354d094b9815edc160e3d72efbfd36ba77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a>Sayısal işlevler için Azure Resource Manager şablonları

Resource Manager hello şu tamsayıları ile çalışmak için işlevleri sunar:

* [ekleme](#add)
* [Copyındex](#copyindex)
* [div](#div)
* [kayan nokta](#float)
* [int](#int)
* [Min](#min)
* [max](#max)
* [mod](#mod)
* [mul](#mul)
* [Sub](#sub)

<a id="add" />

## <a name="add"></a>Ekleme
`add(operand1, operand2)`

Merhaba iki sağlanan tamsayı toplamını döndürür hello.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- | 
|operand1 |Evet |Int |İlk sayı tooadd. |
|operand2 |Evet |Int |İkinci sayı tooadd. |

### <a name="return-value"></a>Dönüş değeri

Merhaba parametreleri hello toplamını içeren bir tamsayı.

### <a name="example"></a>Örnek

Aşağıdaki örnek hello iki parametre ekler.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer tooadd"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer tooadd"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "addResult": {
            "type": "int",
            "value": "[add(parameters('first'), parameters('second'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| addResult | Int | 8 |

<a id="copyindex" />

## <a name="copyindex"></a>Copyındex
`copyIndex(loopName, offset)`

Bir yineleme döngüsü dizinini döndürür hello. 

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| loopName | Hayır | Dize | Merhaba yineleme alma hello adı hello döngü. |
| uzaklık |Hayır |Int |Merhaba sayı tooadd toohello sıfır tabanlı yineleme değeri. |

### <a name="remarks"></a>Açıklamalar

Bu işlev her zaman ile kullanılan bir **kopyalama** nesnesi. İçin hiçbir değer sağlanmazsa **uzaklık**, hello geçerli yineleme değeri döndürülür. Merhaba yineleme değeri sıfırdan başlatır.

Merhaba **loopName** özelliği sağlar toospecify Copyındex tooa kaynak yineleme ya da özellik yineleme başvuran olup olmadığını. İçin hiçbir değer sağlanmazsa **loopName**, hello geçerli kaynak türü yineleme kullanılır. İçin bir değer girin **loopName** bir özellik dolaşırken. 
 
Nasıl kullanabileceğinize tam bir açıklaması için **Copyındex**, bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).

### <a name="example"></a>Örnek

Merhaba aşağıdaki örnek hello adına dahil bir kopya döngü ve hello dizin değeri gösterir. 

```json
"resources": [ 
  { 
    "name": "[concat('examplecopy-', copyIndex())]", 
    "type": "Microsoft.Web/sites", 
    "copy": { 
      "name": "websitescopy", 
      "count": "[parameters('count')]" 
    }, 
    ...
  }
]
```

### <a name="return-value"></a>Dönüş değeri

Merhaba geçerli dizin hello yinelemenin temsil eden bir tamsayı.

<a id="div" />

## <a name="div"></a>div
`div(operand1, operand2)`

Tamsayı bölme hello iki sağlanan tamsayıların döndürür hello.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| operand1 |Evet |Int |ayrılmış hello numarası. |
| operand2 |Evet |Int |kullanılan toodivide hello numarası. 0 olamaz. |

### <a name="return-value"></a>Dönüş değeri

Bir tamsayı temsil eden hello bölme.

### <a name="example"></a>Örnek

Aşağıdaki örnek hello başka bir parametre olarak bir parametre böler.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 8,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used toodivide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "divResult": {
            "type": "int",
            "value": "[div(parameters('first'), parameters('second'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| divResult | Int | 2 |

<a id="float" />

## <a name="float"></a>Kayan nokta
`float(arg1)`

Kayan noktalı sayıyı hello değeri tooa dönüştürür. Özel Parametreler tooan uygulama, bir mantıksal uygulama gibi geçirilirken yalnızca bu işlevi kullanın.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |dize veya int |kayan noktalı sayı değeri tooconvert tooa hello. |

### <a name="return-value"></a>Dönüş değeri
Kayan nokta sayısı.

### <a name="example"></a>Örnek

Aşağıdaki örnek hello nasıl toouse float toopass parametreleri tooa mantıksal uygulama gösterir:

```json
{
    "type": "Microsoft.Logic/workflows",
    "properties": {
        ...
        "parameters": {
        "custom1": {
            "value": "[float('3.0')]"
        },
        "custom2": {
            "value": "[float(3)]"
        },
```

<a id="int" />

## <a name="int"></a>Int
`int(valueToConvert)`

Merhaba belirtilen değere tooan tamsayı dönüştürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| valueToConvert |Evet |dize veya int |Merhaba değeri tooconvert tooan tamsayı. |

### <a name="return-value"></a>Dönüş değeri

Merhaba, bir tamsayı değeri dönüştürülür.

### <a name="example"></a>Örnek

Merhaba aşağıdaki örnek hello kullanıcı tarafından sağlanan parametre değeri toointeger dönüştürür.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToConvert": { 
            "type": "string",
            "defaultValue": "4"
        }
    },
    "resources": [
    ],
    "outputs": {
        "intResult": {
            "type": "int",
            "value": "[int(parameters('stringToConvert'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| intResult | Int | 4 |


<a id="min" />

## <a name="min"></a>dk
`min (arg1)`

Döndürür dizisi veya virgülle ayrılmış tamsayı listesi en düşük değerden hello.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |dizi tamsayı veya virgülle ayrılmış tamsayı listesi |Merhaba koleksiyonu tooget hello en küçük değer. |

### <a name="return-value"></a>Dönüş değeri

En düşük değer hello koleksiyonundan temsil eden bir tamsayı.

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
`max (arg1)`

En büyük değer dizisi veya virgülle ayrılmış tamsayı listesi döndürür hello.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| arg1 |Evet |dizi tamsayı veya virgülle ayrılmış tamsayı listesi |Merhaba koleksiyonu tooget hello en büyük değer. |

### <a name="return-value"></a>Dönüş değeri

Merhaba en büyük değer hello koleksiyonundan temsil eden bir tamsayı.

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

<a id="mod" />

## <a name="mod"></a>mod
`mod(operand1, operand2)`

Merhaba iki sağlanan tamsayılar kullanılarak hello tamsayı bölme Hello kalanı döndürür.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| operand1 |Evet |Int |ayrılmış hello numarası. |
| operand2 |Evet |Int |kullanılan toodivide hello numarası 0 olamaz. |

### <a name="return-value"></a>Dönüş değeri
Bir tamsayı temsil eden hello kalan.

### <a name="example"></a>Örnek

Merhaba aşağıdaki örnekte başka bir parametre olarak bir parametre ayırma hello kalanı döndürür.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used toodivide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "modResult": {
            "type": "int",
            "value": "[mod(parameters('first'), parameters('second'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| modResult | Int | 1 |

<a id="mul" />

## <a name="mul"></a>mul
`mul(operand1, operand2)`

Çarpma hello iki sağlanan tamsayıların döndürür hello.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| operand1 |Evet |Int |İlk sayı toomultiply. |
| operand2 |Evet |Int |İkinci sayı toomultiply. |

### <a name="return-value"></a>Dönüş değeri

Bir tamsayı temsil eden hello çarpma.

### <a name="example"></a>Örnek

Aşağıdaki örnek hello başka bir parametre olarak bir parametre çarpar.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer toomultiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer toomultiply"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "mulResult": {
            "type": "int",
            "value": "[mul(parameters('first'), parameters('second'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| mulResult | Int | 15 |

<a id="sub" />

## <a name="sub"></a>Sub
`sub(operand1, operand2)`

Döndürür hello iki sağlanan tamsayıların çıkarma hello.

### <a name="parameters"></a>Parametreler

| Parametre | Gerekli | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| operand1 |Evet |Int |gelen çıkarılır hello numarası. |
| operand2 |Evet |Int |çıkarılır hello numarası. |

### <a name="return-value"></a>Dönüş değeri
Bir tamsayı temsil eden hello çıkarma.

### <a name="example"></a>Örnek

Aşağıdaki örnek hello başka bir parametre bir parametresinden çıkarır.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer subtracted from"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer toosubtract"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "subResult": {
            "type": "int",
            "value": "[sub(parameters('first'), parameters('second'))]"
        }
    }
}
```

Hello hello önceki hello varsayılan değerlerle örnek çıktı:

| Ad | Tür | Değer |
| ---- | ---- | ----- |
| subResult | Int | 4 |

## <a name="next-steps"></a>Sonraki adımlar
* Bir Azure Resource Manager şablonu hello bölümlerde açıklaması için bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).
* birden fazla şablon toomerge bkz [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).
* tooiterate belirtilen sayıda kaynak türünü oluştururken bkz [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).
* toodeploy hello şablonu oluşturduğunuz toosee bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).

