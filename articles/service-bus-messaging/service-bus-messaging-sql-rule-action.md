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
# <a name="sqlruleaction-syntax"></a><span data-ttu-id="8ec63-103">SQLRuleAction sözdizimi</span><span class="sxs-lookup"><span data-stu-id="8ec63-103">SQLRuleAction syntax</span></span>

<span data-ttu-id="8ec63-104">A *SqlRuleAction* hello örneği [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) sınıfı ve SQL dilinde yazılmış eylemleri temsil kümesi göre karşı gerçekleştirilen sözdizimi bir [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="8ec63-104">A *SqlRuleAction* is an instance of hello [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span>   
  
<span data-ttu-id="8ec63-105">Bu konu hello SQL kural eylemi dilbilgisi ayrıntılarını listeler.</span><span class="sxs-lookup"><span data-stu-id="8ec63-105">This topic lists details about hello SQL rule action grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="8ec63-106">Bağımsız Değişkenler</span><span class="sxs-lookup"><span data-stu-id="8ec63-106">Arguments</span></span>  
  
-   <span data-ttu-id="8ec63-107">`<scope>`Merhaba hello kapsamını belirten isteğe bağlı bir dize `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="8ec63-107">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="8ec63-108">Geçerli değerler `sys` veya `user`.</span><span class="sxs-lookup"><span data-stu-id="8ec63-108">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="8ec63-109">Merhaba `sys` değeri gösterir sistemi kapsamı nerede `<property_name>` hello ortak özelliği adıdır [BrokeredMessage sınıfı](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="8ec63-109">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="8ec63-110">`user`Kullanıcı kapsam gösterir nerede `<property_name>` hello anahtarıdır [BrokeredMessage sınıfı](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) sözlük.</span><span class="sxs-lookup"><span data-stu-id="8ec63-110">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="8ec63-111">`user`Kapsam ise hello varsayılan kapsam `<scope>` belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="8ec63-111">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
### <a name="remarks"></a><span data-ttu-id="8ec63-112">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="8ec63-112">Remarks</span></span>  

<span data-ttu-id="8ec63-113">Bir girişim tooaccess mevcut olmayan kullanıcı özelliği bir hata olduğundan girişimi tooaccess mevcut olmayan sistem bir hata değildir.</span><span class="sxs-lookup"><span data-stu-id="8ec63-113">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="8ec63-114">Bunun yerine, mevcut olmayan kullanıcı özelliği bilinmeyen bir değere dahili olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="8ec63-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="8ec63-115">Bilinmeyen bir değere özel işleci değerlendirme sırasında kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="8ec63-115">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="8ec63-116">property_name</span><span class="sxs-lookup"><span data-stu-id="8ec63-116">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="8ec63-117">Bağımsız Değişkenler</span><span class="sxs-lookup"><span data-stu-id="8ec63-117">Arguments</span></span>  
 <span data-ttu-id="8ec63-118">`<regular_identifier>`Merhaba tarafından temsil edilen bir dize normal ifade takip ediyor:</span><span class="sxs-lookup"><span data-stu-id="8ec63-118">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 <span data-ttu-id="8ec63-119">Bu, bir harf ile başlayıp bir veya daha fazla alt çizgi/harf/basamaklı tarafından izlenen herhangi bir dize anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8ec63-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
 <span data-ttu-id="8ec63-120">`[:IsLetter:]`bir Unicode harf kategorilere herhangi bir Unicode karakter anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8ec63-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="8ec63-121">`System.Char.IsLetter(c)`döndürür `true` varsa `c` bir Unicode harf.</span><span class="sxs-lookup"><span data-stu-id="8ec63-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
 <span data-ttu-id="8ec63-122">`[:IsDigit:]`ondalık bir sayı kategorilere herhangi bir Unicode karakter anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8ec63-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="8ec63-123">`System.Char.IsDigit(c)`döndürür `true` varsa `c` Unicode sayıdır.</span><span class="sxs-lookup"><span data-stu-id="8ec63-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
 <span data-ttu-id="8ec63-124">A `<regular_identifier>` ayrılmış bir anahtar sözcük olamaz.</span><span class="sxs-lookup"><span data-stu-id="8ec63-124">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
 <span data-ttu-id="8ec63-125">`<delimited_identifier>`sol/sağ köşeli ayraç ([]) içine herhangi bir dize değil.</span><span class="sxs-lookup"><span data-stu-id="8ec63-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="8ec63-126">Sağ köşeli ayraç iki sağ köşeli temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="8ec63-126">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="8ec63-127">Merhaba örnekleri aşağıda verilmiştir `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="8ec63-127">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 <span data-ttu-id="8ec63-128">`<quoted_identifier>`ile çift tırnak işaretleri arasına herhangi bir dize değil.</span><span class="sxs-lookup"><span data-stu-id="8ec63-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="8ec63-129">Çift tırnak işareti tanımlayıcıda iki çift tırnak işareti temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="8ec63-129">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="8ec63-130">Bir dize sabiti ile kolayca çakışabilir çünkü toouse tanımlayıcıları tırnak içine alınmış önerilmez.</span><span class="sxs-lookup"><span data-stu-id="8ec63-130">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="8ec63-131">Sınırlandırılmış bir kimlik mümkünse kullanın.</span><span class="sxs-lookup"><span data-stu-id="8ec63-131">Use a delimited identifier if possible.</span></span> <span data-ttu-id="8ec63-132">Merhaba örneği aşağıdadır `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="8ec63-132">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="8ec63-133">düzeni</span><span class="sxs-lookup"><span data-stu-id="8ec63-133">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="8ec63-134">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="8ec63-134">Remarks</span></span>
  
 <span data-ttu-id="8ec63-135">`<pattern>`bir dize olarak değerlendirilen bir ifade olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ec63-135">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="8ec63-136">İşleç gibi hello kalıp olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8ec63-136">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="8ec63-137">Merhaba aşağıdaki joker karakterleri içerebilir:</span><span class="sxs-lookup"><span data-stu-id="8ec63-137">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="8ec63-138">`%`: Herhangi bir dize sıfır veya daha fazla karakter.</span><span class="sxs-lookup"><span data-stu-id="8ec63-138">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="8ec63-139">`_`: Herhangi bir tek karakteri.</span><span class="sxs-lookup"><span data-stu-id="8ec63-139">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="8ec63-140">escape_char</span><span class="sxs-lookup"><span data-stu-id="8ec63-140">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="8ec63-141">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="8ec63-141">Remarks</span></span>
  
 <span data-ttu-id="8ec63-142">`<escape_char>`dize uzunluğu 1 olarak değerlendirilen bir ifade olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ec63-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="8ec63-143">Merhaba işleci gibi bir kaçış karakteri olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8ec63-143">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="8ec63-144">Örneğin, `property LIKE 'ABC\%' ESCAPE '\'` eşleşen `ABC%` ile başlayan bir dize yerine `ABC`.</span><span class="sxs-lookup"><span data-stu-id="8ec63-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="8ec63-145">sabiti</span><span class="sxs-lookup"><span data-stu-id="8ec63-145">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="8ec63-146">Bağımsız Değişkenler</span><span class="sxs-lookup"><span data-stu-id="8ec63-146">Arguments</span></span>  
  
-   <span data-ttu-id="8ec63-147">`<integer_constant>`yalnızca tırnak işaretleri içine değil ve ondalık basamak içeren değil sayı dizesidir.</span><span class="sxs-lookup"><span data-stu-id="8ec63-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="8ec63-148">Merhaba depolanan değerlerin olarak `System.Int64` dahili olarak ve izleme hello aynı aralık.</span><span class="sxs-lookup"><span data-stu-id="8ec63-148">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="8ec63-149">Merhaba, uzun sabitleri örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8ec63-149">hello following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="8ec63-150">`<decimal_constant>`yalnızca tırnak işaretleri içine değil ve ondalık içeren sayı dizesidir.</span><span class="sxs-lookup"><span data-stu-id="8ec63-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="8ec63-151">Merhaba depolanan değerlerin olarak `System.Double` dahili olarak ve aynı aralığı/duyarlık hello izleyin.</span><span class="sxs-lookup"><span data-stu-id="8ec63-151">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="8ec63-152">Sonraki bir sürümde bir farklı veri türü toosupport tam sayı semantiği bu sayı depolanabilir, hello olgu hello altta yatan doğrulamamalısınız veri türü olduğundan `System.Double` için `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="8ec63-152">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="8ec63-153">Merhaba, ondalık sabitleri örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8ec63-153">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="8ec63-154">`<approximate_number_constant>`bir sayı yazılmış bilimsel gösterim şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="8ec63-154">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="8ec63-155">Merhaba depolanan değerlerin olarak `System.Double` dahili olarak ve aynı aralığı/duyarlık hello izleyin.</span><span class="sxs-lookup"><span data-stu-id="8ec63-155">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="8ec63-156">Merhaba, yaklaşık sayı sabitleri örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8ec63-156">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="8ec63-157">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="8ec63-157">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="8ec63-158">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="8ec63-158">Remarks</span></span>
  
<span data-ttu-id="8ec63-159">Boole sabitleri hello anahtar tarafından temsil edilen `TRUE` veya `FALSE`.</span><span class="sxs-lookup"><span data-stu-id="8ec63-159">Boolean constants are represented by hello keywords `TRUE` or `FALSE`.</span></span> <span data-ttu-id="8ec63-160">Merhaba depolanan değerlerin olarak `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="8ec63-160">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="8ec63-161">string_constant</span><span class="sxs-lookup"><span data-stu-id="8ec63-161">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="8ec63-162">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="8ec63-162">Remarks</span></span>
  
<span data-ttu-id="8ec63-163">Dize sabitleri tek tırnak işaretleri içine ve geçerli Unicode karakterler içerir.</span><span class="sxs-lookup"><span data-stu-id="8ec63-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="8ec63-164">Bir dize sabitine katıştırılmış tek tırnak işareti, iki tırnak işaretleri tek olarak temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="8ec63-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="8ec63-165">İşlevi</span><span class="sxs-lookup"><span data-stu-id="8ec63-165">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="8ec63-166">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="8ec63-166">Remarks</span></span>  

<span data-ttu-id="8ec63-167">Merhaba `newid()` işlev döndürür bir **System.Guid** hello tarafından oluşturulan `System.Guid.NewGuid()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="8ec63-167">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="8ec63-168">Merhaba `property(name)` işlevi tarafından başvurulan hello özelliğinin hello değeri döndürür `name`.</span><span class="sxs-lookup"><span data-stu-id="8ec63-168">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="8ec63-169">Merhaba `name` değeri bir string değeri döndürür geçerli bir ifade olabilir.</span><span class="sxs-lookup"><span data-stu-id="8ec63-169">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="8ec63-170">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="8ec63-170">Considerations</span></span>

- <span data-ttu-id="8ec63-171">Kullanılan toocreate yeni bir özellik veya güncelleştirme hello değeri mevcut bir özellik kümesidir.</span><span class="sxs-lookup"><span data-stu-id="8ec63-171">SET is used toocreate a new property or update hello value of an existing property.</span></span>
- <span data-ttu-id="8ec63-172">Kaldır kullanılan tooremove bir özellik değil.</span><span class="sxs-lookup"><span data-stu-id="8ec63-172">REMOVE is used tooremove a property.</span></span>
- <span data-ttu-id="8ec63-173">Merhaba ifade türü ve hello var olan özellik türü farklı olduğunda örtük dönüşüm mümkünse gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="8ec63-173">SET performs implicit conversion if possible when hello expression type and hello existing property type are different.</span></span>
- <span data-ttu-id="8ec63-174">Mevcut olmayan Sistem özellikleri başvurulan eylem başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="8ec63-174">Action fails if non-existent system properties were referenced.</span></span>
- <span data-ttu-id="8ec63-175">Mevcut olmayan kullanıcı özelliklerini başvurulan, eylem başarısız olmaz.</span><span class="sxs-lookup"><span data-stu-id="8ec63-175">Action does not fail if non-existent user properties were referenced.</span></span>
- <span data-ttu-id="8ec63-176">Mevcut olmayan kullanıcı özelliği dahili olarak "Bilinmiyor" olarak değerlendirilir, aşağıdaki hello aynı topluca [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) işleçleri değerlendirirken.</span><span class="sxs-lookup"><span data-stu-id="8ec63-176">A non-existent user property is evaluated as "Unknown" internally, following hello same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ec63-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8ec63-177">Next steps</span></span>

- [<span data-ttu-id="8ec63-178">SQLRuleAction sınıfı</span><span class="sxs-lookup"><span data-stu-id="8ec63-178">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [<span data-ttu-id="8ec63-179">SQLFilter sınıfı</span><span class="sxs-lookup"><span data-stu-id="8ec63-179">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
