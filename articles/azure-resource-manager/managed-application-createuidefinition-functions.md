---
title: "aaaAzure yönetilen uygulama oluşturma UI tanımı işlevleri | Microsoft Docs"
description: "Azure yönetilen uygulamaları için kullanıcı Arabirimi tanımları oluşturulurken Hello işlevleri toouse açıklar"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 7a311a25404ccaec8c19c3ed8cd7038f6887c013
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-functions"></a>CreateUiDefinition işlevleri
Bu bölüm bir CreateUiDefinition tüm desteklenen işlevlerini hello imzaları içerir.

toouse bir işlevi köşeli surround hello bildirimiyle. Örneğin:

```json
"[function()]"
```

Dizeler ve diğer işlevleri işlevi için parametre olarak başvurulabilir, ancak dizeler tek tırnak içine alınmalıdır. Örneğin:

```json
"[fn1(fn2(), 'foobar')]"
```

Uygunsa, hello nokta işlecini kullanarak bir işlevin hello çıktı özelliklerini başvuruda bulunabilir. Örneğin:

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a>İşlevler başvurma
Bu işlevler hello özellikleri ya da bir CreateUiDefinition bağlamında kullanılan tooreference çıkışları olabilir.

### <a name="basics"></a>temel kavramları
Hello çıktı hello temelleri adımında tanımlı bir öğe değerini döndürür.

Merhaba aşağıdaki örnek verir adlı hello öğe hello çıktısını `foo` hello temelleri adımda:

```json
"[basics('foo')]"
```

### <a name="steps"></a>Adımları
Merhaba çıktı hello belirtilen adımında tanımlı bir öğe değerini döndürür. Merhaba temelleri adımda öğelerin tooget hello çıkış değerleri kullanmak `basics()` yerine.

Merhaba aşağıdaki örnek verir adlı hello öğe hello çıktısını `bar` adlı hello adımda `foo`:

```json
"[steps('foo').bar]"
```

### <a name="location"></a>location
Merhaba temel adımı veya hello geçerli bağlam seçilen hello konumu döndürür.

Merhaba aşağıdaki örnek döndürebilir `"westus"`:

```json
"[location()]"
```

## <a name="string-functions"></a>Dize işlevleri
Bu işlevler yalnızca JSON dizelerle kullanılabilir.

### <a name="concat"></a>concat
Bir veya daha fazla art arda ekler.

Örneğin değeri hello çıktı, `element1` varsa `"bar"`, bu örnek hello dizesini döndürür sonra `"foobar!"`:

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a>substring
Belirtilen dize hello hello dizenin döndürür. Merhaba substring hello belirtilen dizinden başlatır ve hello uzunluğu belirtilmiş.

Merhaba aşağıdaki örnek verir `"ftw"`:

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a>Değiştir
Merhaba hangi tüm oluşumlarını dizesinde dize hello geçerli dizesinde belirtilen döndürür başka dize ile değiştirilir.

Merhaba aşağıdaki örnek verir `"Everything is awesome!"`:

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a>GUID
Genel olarak benzersiz bir dize (GUID) oluşturur.

Merhaba aşağıdaki örnek döndürebilir `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:

```json
"[guid()]"
```

### <a name="tolower"></a>toLower
Dönüştürülmüş dizeyi toolowercase döndürür.

Merhaba aşağıdaki örnek verir `"foobar"`:

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a>toUpper
Dönüştürülmüş dizeyi toouppercase döndürür.

Merhaba aşağıdaki örnek verir `"FOOBAR"`:

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a>Toplama işlevleri
Bu işlevler, JSON dizeler, dizileri ve nesneleri gibi koleksiyonlar ile kullanılabilir.

### <a name="contains"></a>içerir
Döndürür `true` bir dize içeriyorsa, belirtilen alt dizeyi Merhaba, bir dizi içeriyor hello belirtilen değer ya da hello belirtilen anahtar bir nesne içerir.

#### <a name="example-1-string"></a>Örnek 1: dize
Merhaba aşağıdaki örnek verir `true`:

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a>Örnek 2: dizi
Varsayın `element1` döndürür `[1, 2, 3]`. Merhaba aşağıdaki örnek verir `false`:

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a>Örnek 3: nesnesi
Varsayın `element1` döndürür:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Merhaba aşağıdaki örnek verir `true`:

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a>uzunluğu
Dize, bir dizideki hello sayısını veya bir nesne anahtarlarında hello sayısı Hello karakterlerin sayısını döndürür.

#### <a name="example-1-string"></a>Örnek 1: dize
Merhaba aşağıdaki örnek verir `6`:

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a>Örnek 2: dizi
Varsayın `element1` döndürür `[1, 2, 3]`. Merhaba aşağıdaki örnek verir `3`:

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Örnek 3: nesnesi
Varsayın `element1` döndürür:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Merhaba aşağıdaki örnek verir `2`:

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a>boş
Döndürür `true` hello dize, dizi veya nesne null veya boş ise.

#### <a name="example-1-string"></a>Örnek 1: dize
Merhaba aşağıdaki örnek verir `true`:

```json
"[empty('')]"
```

#### <a name="example-2-array"></a>Örnek 2: dizi
Varsayın `element1` döndürür `[1, 2, 3]`. Merhaba aşağıdaki örnek verir `false`:

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Örnek 3: nesnesi
Varsayın `element1` döndürür:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Merhaba aşağıdaki örnek verir `false`:

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a>Örnek 4: boş ve tanımlanmamış
Varsayın `element1` olan `null` veya tanımlanmamış. Merhaba aşağıdaki örnek verir `true`:

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a>ilk
Belirtilen bir dize döndürür hello ilk karakteri hello; Merhaba belirtilen dizinin ilk değerini; veya ilk anahtar ve değer hello belirtilen nesnenin hello.

#### <a name="example-1-string"></a>Örnek 1: dize
Merhaba aşağıdaki örnek verir `"f"`:

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a>Örnek 2: dizi
Varsayın `element1` döndürür `[1, 2, 3]`. Merhaba aşağıdaki örnek verir `1`:

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Örnek 3: nesnesi
Varsayın `element1` döndürür:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
Merhaba aşağıdaki örnek verir `{"key1": "foobar"}`:

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a>Son
Döndürür hello son karakteri belirtilen Merhaba, dize hello son değeri hello belirtilen dizinin veya son anahtar ve değer hello belirtilen nesnenin hello.

#### <a name="example-1-string"></a>Örnek 1: dize
Merhaba aşağıdaki örnek verir `"r"`:

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a>Örnek 2: dizi
Varsayın `element1` döndürür `[1, 2, 3]`. Merhaba aşağıdaki örnek verir `2`:

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Örnek 3: nesnesi
Varsayın `element1` döndürür:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Merhaba aşağıdaki örnek verir `{"key2": "raboof"}`:

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a>Al
Belirtilen sayıda ardışık karakteri hello dize hello başından, bitişik değerleri hello dizi hello başından itibaren belirli sayıda veya belirtilen sayıda bitişik anahtarlara ve hello nesnesinin hello başlangıç değerleri döndürür.

#### <a name="example-1-string"></a>Örnek 1: dize
Merhaba aşağıdaki örnek verir `"foo"`:

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a>Örnek 2: dizi
Varsayın `element1` döndürür `[1, 2, 3]`. Merhaba aşağıdaki örnek verir `[1, 2]`:

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a>Örnek 3: nesnesi
Varsayın `element1` döndürür:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Merhaba aşağıdaki örnek verir `{"key1": "foobar"}`:

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a>Atla
Belirtilen bir koleksiyondaki öğelerin sayısı atlar ve öğeleri kalan hello döndürür.

#### <a name="example-1-string"></a>Örnek 1: dize
Merhaba aşağıdaki örnek verir `"bar"`:

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a>Örnek 2: dizi
Varsayın `element1` döndürür `[1, 2, 3]`. Merhaba aşağıdaki örnek verir `[3]`:

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a>Örnek 3: nesnesi
Varsayın `element1` döndürür:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
Merhaba aşağıdaki örnek verir `{"key2": "raboof"}`:

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a>Mantıksal işlevleri
Bu işlevler koşulları içinde kullanılabilir. Bazı işlevler tüm JSON veri türlerini desteklemiyor olabilir.

### <a name="equals"></a>eşittir
Döndürür `true` parametrelerinin her ikisini de aynı tür ve değer hello varsa. Bu işlev tüm JSON veri türlerini destekler.

Merhaba aşağıdaki örnek verir `true`:

```json
"[equals(0, 0)]"
```

Merhaba aşağıdaki örnek verir `true`:

```json
"[equals('foo', 'foo')]"
```

Merhaba aşağıdaki örnek verir `false`:

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a>daha az
Döndürür `true` hello ilk parametre hello ikinci parametre değerinden kesinlikle küçük ise. Bu işlev parametreleri yalnızca türü numarası ve dize destekler.

Merhaba aşağıdaki örnek verir `true`:

```json
"[less(1, 2)]"
```

Merhaba aşağıdaki örnek verir `false`:

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a>lessOrEquals
Döndürür `true` hello ilk parametre küçük veya buna eşit ise toohello ikinci parametre. Bu işlev parametreleri yalnızca türü numarası ve dize destekler.

Merhaba aşağıdaki örnek verir `true`:

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a>büyük
Döndürür `true` hello ilk parametre hello ikinci parametre kesinlikle büyük ise. Bu işlev parametreleri yalnızca türü numarası ve dize destekler.

Merhaba aşağıdaki örnek verir `false`:

```json
"[greater(1, 2)]"
```

Merhaba aşağıdaki örnek verir `true`:

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a>greaterOrEquals
Döndürür `true` hello ilk parametresi sıfırdan büyük veya eşit toohello ikinci parametre ise. Bu işlev parametreleri yalnızca türü numarası ve dize destekler.

Merhaba aşağıdaki örnek verir `true`:

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a>ve
Döndürür `true` tüm hello parametreler çok değerlendirmek,`true`. Bu işlev yalnızca Boole türünde iki veya daha fazla parametre destekler.

Merhaba aşağıdaki örnek verir `true`:

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

Merhaba aşağıdaki örnek verir `false`:

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a>or
Döndürür `true` hello parametreleri en az biri çok değerlendirilirse`true`. Bu işlev yalnızca Boole türünde iki veya daha fazla parametre destekler.

Merhaba aşağıdaki örnek verir `true`:

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

Merhaba aşağıdaki örnek verir `true`:

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a>değil
Döndürür `true` hello parametre çok değerlendirilirse`false`. Bu işlev yalnızca Boole türünde parametreleri destekler.

Merhaba aşağıdaki örnek verir `true`:

```json
"[not(false)]"
```

Merhaba aşağıdaki örnek verir `false`:

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a>birleşim
Merhaba ilk null olmayan parametresinin değerini döndürür hello. Bu işlev tüm JSON veri türlerini destekler.

Varsayın `element1` ve `element2` tanımlanmaz. Merhaba aşağıdaki örnek verir `"foobar"`:

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a>Dönüşüm işlevleri
Bu işlevler kullanılan tooconvert değerleri JSON veri türleri ve Kodlamalar arasında olabilir.

### <a name="int"></a>Int
Merhaba parametresi tooan tamsayı dönüştürür. Bu işlev türü numarası ve dize parametreleri destekler.

Merhaba aşağıdaki örnek verir `1`:

```json
"[int('1')]"
```

Merhaba aşağıdaki örnek verir `2`:

```json
"[int(2.9)]"
```

### <a name="float"></a>Kayan nokta
Kayan nokta Hello parametresi tooa dönüştürür. Bu işlev türü numarası ve dize parametreleri destekler.

Merhaba aşağıdaki örnek verir `1.0`:

```json
"[float('1.0')]"
```

Merhaba aşağıdaki örnek verir `2.9`:

```json
"[float(2.9)]"
```

### <a name="string"></a>Dize
Merhaba parametre tooa dizesi dönüştürür. Bu işlev parametreleri tüm JSON veri türlerini destekler.

Merhaba aşağıdaki örnek verir `"1"`:

```json
"[string(1)]"
```

Merhaba aşağıdaki örnek verir `"2.9"`:

```json
"[string(2.9)]"
```

Merhaba aşağıdaki örnek verir `"[1,2,3]"`:

```json
"[string([1,2,3])]"
```

Merhaba aşağıdaki örnek verir `"{"foo":"bar"}"`:

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a>bool
Merhaba parametresi tooa Boolean dönüştürür. Bu işlev türü numarası, dize ve Boolean parametreleri destekler. JavaScript'te dışındaki herhangi bir değer benzer tooBooleans `0` veya `'false'` döndürür `true`.

Merhaba aşağıdaki örnek verir `true`:

```json
"[bool(1)]"
```

Merhaba aşağıdaki örnek verir `false`:

```json
"[bool(0)]"
```

Merhaba aşağıdaki örnek verir `true`:

```json
"[bool(true)]"
```

Merhaba aşağıdaki örnek verir `true`:

```json
"[bool('true')]"
```

### <a name="parse"></a>Ayrıştırma
Merhaba parametresi tooa yerel tür dönüştürür. Diğer bir deyişle, bu hello tersini işlevidir `string()`. Bu işlev yalnızca dize türünde parametreleri destekler.

Merhaba aşağıdaki örnek verir `1`:

```json
"[parse('1')]"
```

Merhaba aşağıdaki örnek verir `true`:

```json
"[parse('true')]"
```

Merhaba aşağıdaki örnek verir `[1,2,3]`:

```json
"[parse('[1,2,3]')]"
```

Merhaba aşağıdaki örnek verir `{"foo":"bar"}`:

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a>encodeBase64
Merhaba parametresi tooa base-64 kodlanmış dize olarak kodlar. Bu işlev yalnızca dize türünde parametreleri destekler.

Merhaba aşağıdaki örnek verir `"Zm9vYmFy"`:

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a>decodeBase64
Base-64 kodlu bir dize Hello parametresinden kodunu çözer. Bu işlev yalnızca dize türünde parametreleri destekler.

Merhaba aşağıdaki örnek verir `"foobar"`:

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a>Encodeurıcomponent
Merhaba parametresi tooa URL kodlanmış dize olarak kodlar. Bu işlev yalnızca dize türünde parametreleri destekler.

Merhaba aşağıdaki örnek verir `"https%3A%2F%2Fportal.azure.com%2F"`:

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a>Decodeurıcomponent
Bir URL kodlanmış dize Hello parametresinden kodunu çözer. Bu işlev yalnızca dize türünde parametreleri destekler.

Merhaba aşağıdaki örnek verir `"https://portal.azure.com/"`:

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a>Matematik işlevleri
### <a name="add"></a>Ekleme
İki sayı ekleyen ve hello sonucunu döndürür.

Merhaba aşağıdaki örnek verir `3`:

```json
"[add(1, 2)]"
```

### <a name="sub"></a>Sub
Merhaba ikinci sayı hello ilk numarasından çıkarır ve hello sonucunu döndürür.

Merhaba aşağıdaki örnek verir `1`:

```json
"[sub(3, 2)]"
```

### <a name="mul"></a>mul
İki sayıyı çarpar ve hello sonucunu döndürür.

Merhaba aşağıdaki örnek verir `6`:

```json
"[mul(2, 3)]"
```

### <a name="div"></a>div
Merhaba ikinci sayı Hello ilk sayıyı böler ve hello sonucunu döndürür. Merhaba sonucu her zaman bir tamsayıdır.

Merhaba aşağıdaki örnek verir `2`:

```json
"[div(6, 3)]"
```

### <a name="mod"></a>mod
Merhaba ikinci sayı Hello ilk sayıyı böler ve hello kalanı döndürür.

Merhaba aşağıdaki örnek verir `0`:

```json
"[mod(6, 3)]"
```

Merhaba aşağıdaki örnek verir `2`:

```json
"[mod(6, 4)]"
```

### <a name="min"></a>dk
Küçük hello iki numaraları döndürür hello.

Merhaba aşağıdaki örnek verir `1`:

```json
"[min(1, 2)]"
```

### <a name="max"></a>max
Döndürür hello hello iki sayı ile daha büyük.

Merhaba aşağıdaki örnek verir `2`:

```json
"[max(1, 2)]"
```

### <a name="range"></a>Aralık
İntegral dizisi oluşturur numaraları hello içinde belirtilen aralık.

Merhaba aşağıdaki örnek verir `[1,2,3]`:

```json
"[range(1, 3)]"
```

### <a name="rand"></a>rand
Bir rastgele döndürür tamsayı hello içinde belirtilen aralık. Bu işlev, şifreleme açısından güvenli rastgele sayılar oluşturmaz.

Merhaba aşağıdaki örnek döndürebilir `42`:

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a>Kat
Küçük veya buna eşit Hello en büyük tamsayıyı döndürür toohello belirtilen sayı.

Merhaba aşağıdaki örnek verir `3`:

```json
"[floor(3.14)]"
```

### <a name="ceil"></a>ceil
Değerinden büyük tamsayıyı döndürür hello veya eşit toohello numarası belirtildi.

Merhaba aşağıdaki örnek verir `4`:

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a>Date işlevleri
### <a name="utcnow"></a>utcNow
ISO 8601 biçiminde hello geçerli tarih ve saat hello yerel bilgisayardaki bir dize döndürür.

Merhaba aşağıdaki örnek döndürebilir `"1990-12-31T23:59:59.000Z"`:

```json
"[utcNow()]"
```

### <a name="addseconds"></a>saniyeEkle
Bir tamsayı belirtilen saniye toohello ekler zaman damgası.

Merhaba aşağıdaki örnek verir `"1991-01-01T00:00:00.000Z"`:

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a>addMinutes
Bir tamsayı belirtilen dakika toohello ekler zaman damgası.

Merhaba aşağıdaki örnek verir `"1991-01-01T00:00:59.000Z"`:

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a>addHours
Belirtilen saat toohello bir tamsayı ekler zaman damgası.

Merhaba aşağıdaki örnek verir `"1991-01-01T00:59:59.000Z"`:

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a>Sonraki adımlar
* Bir giriş tooAzure kaynak yöneticisi için bkz: [Azure Resource Manager'a genel bakış](resource-group-overview.md).

