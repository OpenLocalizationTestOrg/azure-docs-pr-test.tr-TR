---
title: "azure'da aaaSQLRuleAction söz dizimi başvurusu | Microsoft Docs"
description: "SQLRuleAction dilbilgisi hakkında ayrıntılar."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 8ef281f942847bcc535b83a5ffb30d03539734f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sqlruleaction-syntax"></a>SQLRuleAction sözdizimi

A *SqlRuleAction* hello örneği [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) sınıfı ve SQL dilinde yazılmış eylemleri temsil kümesi göre karşı gerçekleştirilen sözdizimi bir [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).   
  
Bu konu hello SQL kural eylemi dilbilgisi ayrıntılarını listeler.  
  
```  
<statements> ::=
    <statement> [, ...n]  
  
```  
  
```  
<statement> ::=
    <action> [;]
    Remarks
    -------
    Semicolon is optional.  
  
```  
  
```  
<action> ::=
    SET <property> = <expression>
    REMOVE <property>  
```

```
<expression> ::=
    <constant>
    | <function>
    | <property>
    | <expression> { + | - | * | / | % } <expression>
    | { + | - } <expression>
    | ( <expression> )
``` 

```
<property> := 
    [<scope> .] <property_name>
``` 
  
## <a name="arguments"></a>Bağımsız Değişkenler  
  
-   `<scope>`Merhaba hello kapsamını belirten isteğe bağlı bir dize `<property_name>`. Geçerli değerler `sys` veya `user`. Merhaba `sys` değeri gösterir sistemi kapsamı nerede `<property_name>` hello ortak özelliği adıdır [BrokeredMessage sınıfı](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage). `user`Kullanıcı kapsam gösterir nerede `<property_name>` hello anahtarıdır [BrokeredMessage sınıfı](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) sözlük. `user`Kapsam ise hello varsayılan kapsam `<scope>` belirtilmedi.  
  
### <a name="remarks"></a>Açıklamalar  

Bir girişim tooaccess mevcut olmayan kullanıcı özelliği bir hata olduğundan girişimi tooaccess mevcut olmayan sistem bir hata değildir. Bunun yerine, mevcut olmayan kullanıcı özelliği bilinmeyen bir değere dahili olarak değerlendirilir. Bilinmeyen bir değere özel işleci değerlendirme sırasında kabul edilir.  
  
## <a name="propertyname"></a>property_name  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a>Bağımsız Değişkenler  
 `<regular_identifier>`Merhaba tarafından temsil edilen bir dize normal ifade takip ediyor:  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 Bu, bir harf ile başlayıp bir veya daha fazla alt çizgi/harf/basamaklı tarafından izlenen herhangi bir dize anlamına gelir.  
  
 `[:IsLetter:]`bir Unicode harf kategorilere herhangi bir Unicode karakter anlamına gelir. `System.Char.IsLetter(c)`döndürür `true` varsa `c` bir Unicode harf.  
  
 `[:IsDigit:]`ondalık bir sayı kategorilere herhangi bir Unicode karakter anlamına gelir. `System.Char.IsDigit(c)`döndürür `true` varsa `c` Unicode sayıdır.  
  
 A `<regular_identifier>` ayrılmış bir anahtar sözcük olamaz.  
  
 `<delimited_identifier>`sol/sağ köşeli ayraç ([]) içine herhangi bir dize değil. Sağ köşeli ayraç iki sağ köşeli temsil edilir. Merhaba örnekleri aşağıda verilmiştir `<delimited_identifier>`:  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 `<quoted_identifier>`ile çift tırnak işaretleri arasına herhangi bir dize değil. Çift tırnak işareti tanımlayıcıda iki çift tırnak işareti temsil edilir. Bir dize sabiti ile kolayca çakışabilir çünkü toouse tanımlayıcıları tırnak içine alınmış önerilmez. Sınırlandırılmış bir kimlik mümkünse kullanın. Merhaba örneği aşağıdadır `<quoted_identifier>`:  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a>düzeni  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>Açıklamalar
  
 `<pattern>`bir dize olarak değerlendirilen bir ifade olmalıdır. İşleç gibi hello kalıp olarak kullanılır.      Merhaba aşağıdaki joker karakterleri içerebilir:  
  
-   `%`: Herhangi bir dize sıfır veya daha fazla karakter.  
  
-   `_`: Herhangi bir tek karakteri.  
  
## <a name="escapechar"></a>escape_char  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>Açıklamalar
  
 `<escape_char>`dize uzunluğu 1 olarak değerlendirilen bir ifade olmalıdır. Merhaba işleci gibi bir kaçış karakteri olarak kullanılır.  
  
 Örneğin, `property LIKE 'ABC\%' ESCAPE '\'` eşleşen `ABC%` ile başlayan bir dize yerine `ABC`.  
  
## <a name="constant"></a>sabiti  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a>Bağımsız Değişkenler  
  
-   `<integer_constant>`yalnızca tırnak işaretleri içine değil ve ondalık basamak içeren değil sayı dizesidir. Merhaba depolanan değerlerin olarak `System.Int64` dahili olarak ve izleme hello aynı aralık.  
  
     Merhaba, uzun sabitleri örnekleri şunlardır:  
  
    ```  
    1894  
    2  
    ```  
  
-   `<decimal_constant>`yalnızca tırnak işaretleri içine değil ve ondalık içeren sayı dizesidir. Merhaba depolanan değerlerin olarak `System.Double` dahili olarak ve aynı aralığı/duyarlık hello izleyin.  
  
     Sonraki bir sürümde bir farklı veri türü toosupport tam sayı semantiği bu sayı depolanabilir, hello olgu hello altta yatan doğrulamamalısınız veri türü olduğundan `System.Double` için `<decimal_constant>`.  
  
     Merhaba, ondalık sabitleri örnekleri şunlardır:  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   `<approximate_number_constant>`bir sayı yazılmış bilimsel gösterim şeklindedir. Merhaba depolanan değerlerin olarak `System.Double` dahili olarak ve aynı aralığı/duyarlık hello izleyin. Merhaba, yaklaşık sayı sabitleri örnekleri şunlardır:  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a>boolean_constant  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a>Açıklamalar
  
Boole sabitleri hello anahtar tarafından temsil edilen `TRUE` veya `FALSE`. Merhaba depolanan değerlerin olarak `System.Boolean`.  
  
## <a name="stringconstant"></a>string_constant  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a>Açıklamalar
  
Dize sabitleri tek tırnak işaretleri içine ve geçerli Unicode karakterler içerir. Bir dize sabitine katıştırılmış tek tırnak işareti, iki tırnak işaretleri tek olarak temsil edilir.  
  
## <a name="function"></a>İşlevi  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a>Açıklamalar  

Merhaba `newid()` işlev döndürür bir **System.Guid** hello tarafından oluşturulan `System.Guid.NewGuid()` yöntemi.  
  
Merhaba `property(name)` işlevi tarafından başvurulan hello özelliğinin hello değeri döndürür `name`. Merhaba `name` değeri bir string değeri döndürür geçerli bir ifade olabilir.  
  
## <a name="considerations"></a>Dikkat edilmesi gerekenler

- Kullanılan toocreate yeni bir özellik veya güncelleştirme hello değeri mevcut bir özellik kümesidir.
- Kaldır kullanılan tooremove bir özellik değil.
- Merhaba ifade türü ve hello var olan özellik türü farklı olduğunda örtük dönüşüm mümkünse gerçekleştirir.
- Mevcut olmayan Sistem özellikleri başvurulan eylem başarısız olur.
- Mevcut olmayan kullanıcı özelliklerini başvurulan, eylem başarısız olmaz.
- Mevcut olmayan kullanıcı özelliği dahili olarak "Bilinmiyor" olarak değerlendirilir, aşağıdaki hello aynı topluca [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) işleçleri değerlendirirken.

## <a name="next-steps"></a>Sonraki adımlar

- [SQLRuleAction sınıfı](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [SQLFilter sınıfı](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
