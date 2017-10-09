---
title: "Azure Search'te dizin oluşturucular içinde aaaField eşlemeleri"
description: "Azure Search dizin oluşturucu alan eşlemelerini tooaccount alan adları ve veri Beyanları farklılıkları için yapılandırma"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 0325a4de-0190-4dd5-a64d-4e56601d973b
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: eugenesh
ms.openlocfilehash: 009d5dbc12cb9e8d9cfd3e8042e907ca88399ad7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="field-mappings-in-azure-search-indexers"></a>Azure Search'te dizin oluşturucular üzerinde alan eşlemeleri
Azure Search'te dizin oluşturucular kullanırken, kendiniz bazen burada giriş verilerinizi hedef dizininizi hello şeması oldukça eşleşmediği durumlarda bulabilirsiniz. Bu durumda, kullandığınız **alan eşlemelerini** tootransform hello verilerinizi istenen şekli.

Alan eşlemelerini yararlı olduğu bazı durumlar:

* Bir alan veri kaynağınız sahip `_id`, ancak Azure Search, alt çizgi ile başlayan alan adları izin vermez. Alan eşleme, çok "alanı yeniden adlandırma" sağlar.
* Merhaba birkaç alanlarına dizin ile Merhaba toopopulate istediğiniz aynı veri kaynağı Örneğin veri tooapply farklı çözümleyiciler toothose alanları istemiyor. Alan eşlemelerini "veri kaynağı alanı çatallaştırma" olanak tanır.
* TooBase64 ihtiyacınız kodlamak veya kodunu çözmek verilerinizi. Alan eşlemelerini birkaç Destek **işlevleri eşleme**, kodlama ve kod çözme dahil olmak üzere işlevleri Base64 için.   

## <a name="setting-up-field-mappings"></a>Alan eşlemelerini ayarlama
Alan eşlemelerini hello kullanarak yeni bir dizin oluşturucu oluştururken ekleyebilirsiniz [oluşturma dizin oluşturucu](https://msdn.microsoft.com/library/azure/dn946899.aspx) API. Alan eşlemelerini hello kullanarak bir dizin oluşturma dizin oluşturucu üzerinde yönetebilirsiniz [güncelleştirme dizin oluşturucu](https://msdn.microsoft.com/library/azure/dn946892.aspx) API.

Alan eşlemeyi 3 bölümden oluşur:

1. A `sourceFieldName`, veri kaynağında bir alan temsil eder. Bu özellik gereklidir.
2. İsteğe bağlı bir `targetFieldName`, search dizininizi bir alanı temsil eder. Atlanırsa, hello hello veri kaynağı olduğu gibi aynı adı kullanılır.
3. İsteğe bağlı bir `mappingFunction`, önceden tanımlanmış işlevleri, çeşitli birini kullanarak verilerinizi dönüştürebilirsiniz. işlevlerin tam listesi Hello [aşağıda](#mappingFunctions).

Alan eşlemeleri toohello eklenen `fieldMappings` hello dizin oluşturucu tanımı dizi.

Örneğin, işte alan adları farklılıkları nasıl uyum sağlayabilir:

```JSON

PUT https://[service name].search.windows.net/indexers/myindexer?api-version=[api-version]
Content-Type: application/json
api-key: [admin key]
{
    "dataSourceName" : "mydatasource",
    "targetIndexName" : "myindex",
    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ]
}
```

Bir dizin oluşturucu, birden çok alan eşlemelerini olabilir. Nasıl, "bir alan çatallaştırma" Örneğin, burada'nın:

```JSON

"fieldMappings" : [
    { "sourceFieldName" : "text", "targetFieldName" : "textStandardEnglishAnalyzer" },
    { "sourceFieldName" : "text", "targetFieldName" : "textSoundexAnalyzer" },
]
```

> [!NOTE]
> Azure arama büyük küçük harf duyarsız karşılaştırma tooresolve hello alan ve işlev adları alan eşlemelerini kullanır. Bu (tüm hello büyük/küçük harf sağ tooget yok) kullanışlıdır ancak bu veri kaynağı veya dizin yalnızca örneğe göre farklı alanlara sahip olamaz anlamına gelir.  
>
>

<a name="mappingFunctions"></a>

## <a name="field-mapping-functions"></a>Alan eşleme işlevleri
Bu işlevler şu anda desteklenir:

* [base64Encode](#base64EncodeFunction)
* [base64Decode](#base64DecodeFunction)
* [extractTokenAtPosition](#extractTokenAtPositionFunction)
* [jsonArrayToStringCollection](#jsonArrayToStringCollectionFunction)

<a name="base64EncodeFunction"></a>

### <a name="base64encode"></a>base64Encode
Gerçekleştirir *URL için güvenli* Merhaba Base64 kodlaması giriş dizesi. Merhaba giriş UTF-8 ile kodlanmış olduğunu varsayar.

#### <a name="sample-use-case"></a>Örnek Kullanım örneği
Yalnızca (Müşteriler hello arama API, örneğin kullanarak mümkün tooaddress hello belge olması gerektiğinden) bir Azure Search belge anahtarında URL için güvenli karakter bulunabilir. Verilerinizi URL güvenli olmayan karakterler içeriyor ve toouse istiyorsanız bunu toopopulate bir anahtar alanı arama dizininizdeki bu işlevi kullanın.   

#### <a name="example"></a>Örnek
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Path",
    "targetFieldName" : "UrlSafePath",
    "mappingFunction" : { "name" : "base64Encode" }
  }]
```

<a name="base64DecodeFunction"></a>

### <a name="base64decode"></a>base64Decode
Base64 hello giriş dizesi çözer. Merhaba giriş tooa varsayılır *URL için güvenli* Base64 ile kodlanmış dize.

#### <a name="sample-use-case"></a>Örnek Kullanım örneği
BLOB özel meta verileri değerleri ASCII kodlanmış olmalıdır. Blob özel meta verilerde Base64 kodlama toorepresent rasgele Unicode dizelerini kullanabilirsiniz. Ancak, toomake arama anlamlı, bu işlevi tooturn hello kodlanmış verileri "Normal" dizelere geri arama dizininize doldurulurken kullanabilirsiniz.  

#### <a name="example"></a>Örnek
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Base64EncodedMetadata",
    "targetFieldName" : "SearchableMetadata",
    "mappingFunction" : { "name" : "base64Decode" }
  }]
```

<a name="extractTokenAtPositionFunction"></a>

### <a name="extracttokenatposition"></a>extractTokenAtPosition
Hello kullanarak bir dize alan sınırlayıcı ve çekmeleri hello belirteci adresindeki belirtilen bölmelerini hello elde edilen bölünmüş belirtilen konumda hello.

Örneğin, hello giriş ise `Jane Doe`, hello `delimiter` olan `" "`(boşluk) ve hello `position` 0, hello sonuç `Jane`hello if `position` 1 ' dir hello sonuç `Doe`. Başlangıç konumu yok tooa belirteci başvuruyorsa, bir hata döndürülür.

#### <a name="sample-use-case"></a>Örnek Kullanım örneği
Veri kaynağınızı içeren bir `PersonName` alan ve istediğiniz tooindex iki ayrı olarak `FirstName` ve `LastName` alanları. Bu işlev toosplit hello sınırlayıcı hello gibi hello boşluk karakteri kullanarak giriş kullanabilirsiniz.

#### <a name="parameters"></a>Parametreler
* `delimiter`: bir dizeyi toouse bölme hello olduğunda giriş dizesi hello ayırıcı olarak.
* `position`: dize hello girdikten sonra hello belirteci toopick bir tamsayı sıfır tabanlı konumu ayrılır.    

#### <a name="example"></a>Örnek
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "FirstName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 0 } }
  },
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "LastName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 1 } }
  }]
```

<a name="jsonArrayToStringCollectionFunction"></a>

### <a name="jsonarraytostringcollection"></a>jsonArrayToStringCollection
Biçimlendirilmiş dizeler JSON dizisi olarak bir dize kullanılan toopopulate olabilen bir dize dizisi dönüşümler bir `Collection(Edm.String)` hello dizinindeki alan.

Örneğin, dize hello giriş ise `["red", "white", "blue"]`, sonra da hello hedef alan türü `Collection(Edm.String)` hello üç değerlerle doldurulur `red`, `white` ve `blue`. JSON dizesi dizileri olarak ayrıştırılamıyor giriş değerleri için bir hata döndürülür.

#### <a name="sample-use-case"></a>Örnek Kullanım örneği
Azure SQL veritabanı doğal olarak çok eşleyen bir yerleşik veri türüne sahip değil`Collection(Edm.String)` Azure Search'te alanları. toopopulate koleksiyonu alanları dize, JSON dize dizisi olarak, kaynak veri biçimi ve bu işlevi kullanın.

#### <a name="example"></a>Örnek
```JSON

"fieldMappings" : [
  { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } }
]
```

## <a name="help-us-make-azure-search-better"></a>Azure Search iyileştirmemize yardımcı olun
Özellik istekleri veya fikir geliştirmeleri için varsa, lütfen üzerinde toous ulaşmak bizim [UserVoice sitesinde](https://feedback.azure.com/forums/263029-azure-search/).
