---
title: "Azure'da SQLRuleAction söz dizimi başvurusu | Microsoft Docs"
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
ms.openlocfilehash: 7379b7f58563675f28d77928d933c0d9c7992e71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="sqlruleaction-syntax"></a><span data-ttu-id="5acbd-103">SQLRuleAction sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5acbd-103">SQLRuleAction syntax</span></span>

<span data-ttu-id="5acbd-104">A *SqlRuleAction* örneği [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) sınıfı ve SQL dilinde yazılmış eylemleri temsil kümesi göre karşı gerçekleştirilen sözdizimi bir [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="5acbd-104">A *SqlRuleAction* is an instance of the [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span>   
  
<span data-ttu-id="5acbd-105">Bu konu, SQL kural eylemi dilbilgisi ayrıntılarını listeler.</span><span class="sxs-lookup"><span data-stu-id="5acbd-105">This topic lists details about the SQL rule action grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="5acbd-106">Bağımsız Değişkenler</span><span class="sxs-lookup"><span data-stu-id="5acbd-106">Arguments</span></span>  
  
-   <span data-ttu-id="5acbd-107">`<scope>`kapsamını belirten isteğe bağlı bir dize `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="5acbd-107">`<scope>` is an optional string indicating the scope of the `<property_name>`.</span></span> <span data-ttu-id="5acbd-108">Geçerli değerler `sys` veya `user`.</span><span class="sxs-lookup"><span data-stu-id="5acbd-108">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="5acbd-109">`sys` Değeri gösterir sistemi kapsamı nerede `<property_name>` bir ortak özellik adı [BrokeredMessage sınıfı](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="5acbd-109">The `sys` value indicates system scope where `<property_name>` is a public property name of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="5acbd-110">`user`Kullanıcı kapsam gösterir nerede `<property_name>` , bir anahtar [BrokeredMessage sınıfı](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) sözlük.</span><span class="sxs-lookup"><span data-stu-id="5acbd-110">`user` indicates user scope where `<property_name>` is a key of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="5acbd-111">`user`Kapsam ise varsayılan kapsamı `<scope>` belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="5acbd-111">`user` scope is the default scope if `<scope>` is not specified.</span></span>  
  
### <a name="remarks"></a><span data-ttu-id="5acbd-112">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="5acbd-112">Remarks</span></span>  

<span data-ttu-id="5acbd-113">Mevcut olmayan kullanıcı özelliği erişme denemesi bir hata olduğundan mevcut olmayan sistem özelliği erişme denemesi bir hata var.</span><span class="sxs-lookup"><span data-stu-id="5acbd-113">An attempt to access a non-existent system property is an error, while an attempt to access a non-existent user property is not an error.</span></span> <span data-ttu-id="5acbd-114">Bunun yerine, mevcut olmayan kullanıcı özelliği bilinmeyen bir değere dahili olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="5acbd-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="5acbd-115">Bilinmeyen bir değere özel işleci değerlendirme sırasında kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="5acbd-115">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="5acbd-116">property_name</span><span class="sxs-lookup"><span data-stu-id="5acbd-116">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="5acbd-117">Bağımsız Değişkenler</span><span class="sxs-lookup"><span data-stu-id="5acbd-117">Arguments</span></span>  
 <span data-ttu-id="5acbd-118">`<regular_identifier>`bir dize aşağıdaki normal ifade tarafından temsil edilen:</span><span class="sxs-lookup"><span data-stu-id="5acbd-118">`<regular_identifier>` is a string represented by the following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 <span data-ttu-id="5acbd-119">Bu, bir harf ile başlayıp bir veya daha fazla alt çizgi/harf/basamaklı tarafından izlenen herhangi bir dize anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="5acbd-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
 <span data-ttu-id="5acbd-120">`[:IsLetter:]`bir Unicode harf kategorilere herhangi bir Unicode karakter anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="5acbd-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="5acbd-121">`System.Char.IsLetter(c)`döndürür `true` varsa `c` bir Unicode harf.</span><span class="sxs-lookup"><span data-stu-id="5acbd-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
 <span data-ttu-id="5acbd-122">`[:IsDigit:]`ondalık bir sayı kategorilere herhangi bir Unicode karakter anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="5acbd-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="5acbd-123">`System.Char.IsDigit(c)`döndürür `true` varsa `c` Unicode sayıdır.</span><span class="sxs-lookup"><span data-stu-id="5acbd-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
 <span data-ttu-id="5acbd-124">A `<regular_identifier>` ayrılmış bir anahtar sözcük olamaz.</span><span class="sxs-lookup"><span data-stu-id="5acbd-124">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
 <span data-ttu-id="5acbd-125">`<delimited_identifier>`sol/sağ köşeli ayraç ([]) içine herhangi bir dize değil.</span><span class="sxs-lookup"><span data-stu-id="5acbd-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="5acbd-126">Sağ köşeli ayraç iki sağ köşeli temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="5acbd-126">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="5acbd-127">Örnekleri aşağıda verilmiştir `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="5acbd-127">The following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 <span data-ttu-id="5acbd-128">`<quoted_identifier>`ile çift tırnak işaretleri arasına herhangi bir dize değil.</span><span class="sxs-lookup"><span data-stu-id="5acbd-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="5acbd-129">Çift tırnak işareti tanımlayıcıda iki çift tırnak işareti temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="5acbd-129">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="5acbd-130">Bir dize sabiti ile kolayca çakışabilir çünkü tırnak işaretli tanımlayıcılar kullanmak için önerilmez.</span><span class="sxs-lookup"><span data-stu-id="5acbd-130">It is not recommended to use quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="5acbd-131">Sınırlandırılmış bir kimlik mümkünse kullanın.</span><span class="sxs-lookup"><span data-stu-id="5acbd-131">Use a delimited identifier if possible.</span></span> <span data-ttu-id="5acbd-132">Aşağıdaki örneğidir `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="5acbd-132">The following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="5acbd-133">düzeni</span><span class="sxs-lookup"><span data-stu-id="5acbd-133">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="5acbd-134">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="5acbd-134">Remarks</span></span>
  
 <span data-ttu-id="5acbd-135">`<pattern>`bir dize olarak değerlendirilen bir ifade olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5acbd-135">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="5acbd-136">LIKE işleci için bir desen olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5acbd-136">It is used as a pattern for the LIKE operator.</span></span>      <span data-ttu-id="5acbd-137">Aşağıdaki joker karakterleri içerebilir:</span><span class="sxs-lookup"><span data-stu-id="5acbd-137">It can contain the following wildcard characters:</span></span>  
  
-   <span data-ttu-id="5acbd-138">`%`: Herhangi bir dize sıfır veya daha fazla karakter.</span><span class="sxs-lookup"><span data-stu-id="5acbd-138">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="5acbd-139">`_`: Herhangi bir tek karakteri.</span><span class="sxs-lookup"><span data-stu-id="5acbd-139">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="5acbd-140">escape_char</span><span class="sxs-lookup"><span data-stu-id="5acbd-140">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="5acbd-141">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="5acbd-141">Remarks</span></span>
  
 <span data-ttu-id="5acbd-142">`<escape_char>`dize uzunluğu 1 olarak değerlendirilen bir ifade olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5acbd-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="5acbd-143">LIKE işleci için bir kaçış karakteri olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5acbd-143">It is used as an escape character for the LIKE operator.</span></span>  
  
 <span data-ttu-id="5acbd-144">Örneğin, `property LIKE 'ABC\%' ESCAPE '\'` eşleşen `ABC%` ile başlayan bir dize yerine `ABC`.</span><span class="sxs-lookup"><span data-stu-id="5acbd-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="5acbd-145">sabiti</span><span class="sxs-lookup"><span data-stu-id="5acbd-145">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="5acbd-146">Bağımsız Değişkenler</span><span class="sxs-lookup"><span data-stu-id="5acbd-146">Arguments</span></span>  
  
-   <span data-ttu-id="5acbd-147">`<integer_constant>`yalnızca tırnak işaretleri içine değil ve ondalık basamak içeren değil sayı dizesidir.</span><span class="sxs-lookup"><span data-stu-id="5acbd-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="5acbd-148">Değerleri olarak depolanan `System.Int64` dahili olarak, aynı aralık izleyin.</span><span class="sxs-lookup"><span data-stu-id="5acbd-148">The values are stored as `System.Int64` internally, and follow the same range.</span></span>  
  
     <span data-ttu-id="5acbd-149">Uzun sabitleri örnekleri verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5acbd-149">The following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="5acbd-150">`<decimal_constant>`yalnızca tırnak işaretleri içine değil ve ondalık içeren sayı dizesidir.</span><span class="sxs-lookup"><span data-stu-id="5acbd-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="5acbd-151">Değerleri olarak depolanan `System.Double` dahili olarak, aynı aralık/duyarlık izleyin.</span><span class="sxs-lookup"><span data-stu-id="5acbd-151">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span>  
  
     <span data-ttu-id="5acbd-152">Sonraki bir sürümde tam sayı semantiğini desteklemek için farklı bir veri türü bu sayı depolanabilir, arka plandaki olgu üzerinde doğrulamamalısınız veri türü olduğundan `System.Double` için `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="5acbd-152">In a future version, this number might be stored in a different data type to support exact number semantics, so you should not rely on the fact the underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="5acbd-153">Ondalık sabitleri örnekleri verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5acbd-153">The following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="5acbd-154">`<approximate_number_constant>`bir sayı yazılmış bilimsel gösterim şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="5acbd-154">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="5acbd-155">Değerleri olarak depolanan `System.Double` dahili olarak, aynı aralık/duyarlık izleyin.</span><span class="sxs-lookup"><span data-stu-id="5acbd-155">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span> <span data-ttu-id="5acbd-156">Yaklaşık sayı sabitleri örnekleri verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5acbd-156">The following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="5acbd-157">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="5acbd-157">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="5acbd-158">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="5acbd-158">Remarks</span></span>
  
<span data-ttu-id="5acbd-159">Boole sabitleri anahtar sözcükleri tarafından temsil edilen `TRUE` veya `FALSE`.</span><span class="sxs-lookup"><span data-stu-id="5acbd-159">Boolean constants are represented by the keywords `TRUE` or `FALSE`.</span></span> <span data-ttu-id="5acbd-160">Değerleri olarak depolanan `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="5acbd-160">The values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="5acbd-161">string_constant</span><span class="sxs-lookup"><span data-stu-id="5acbd-161">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="5acbd-162">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="5acbd-162">Remarks</span></span>
  
<span data-ttu-id="5acbd-163">Dize sabitleri tek tırnak işaretleri içine ve geçerli Unicode karakterler içerir.</span><span class="sxs-lookup"><span data-stu-id="5acbd-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="5acbd-164">Bir dize sabitine katıştırılmış tek tırnak işareti, iki tırnak işaretleri tek olarak temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="5acbd-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="5acbd-165">İşlevi</span><span class="sxs-lookup"><span data-stu-id="5acbd-165">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="5acbd-166">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="5acbd-166">Remarks</span></span>  

<span data-ttu-id="5acbd-167">`newid()` İşlev döndürür bir **System.Guid** tarafından oluşturulan `System.Guid.NewGuid()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="5acbd-167">The `newid()` function returns a **System.Guid** generated by the `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="5acbd-168">`property(name)` İşlevi tarafından başvurulan özelliğinin değerini döndürür `name`.</span><span class="sxs-lookup"><span data-stu-id="5acbd-168">The `property(name)` function returns the value of the property referenced by `name`.</span></span> <span data-ttu-id="5acbd-169">`name` Değeri bir string değeri döndürür geçerli bir ifade olabilir.</span><span class="sxs-lookup"><span data-stu-id="5acbd-169">The `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="5acbd-170">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="5acbd-170">Considerations</span></span>

- <span data-ttu-id="5acbd-171">Küme, yeni bir özellik oluşturmak veya mevcut bir özellik değerini güncelleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5acbd-171">SET is used to create a new property or update the value of an existing property.</span></span>
- <span data-ttu-id="5acbd-172">Kaldır, bir özelliği kaldırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5acbd-172">REMOVE is used to remove a property.</span></span>
- <span data-ttu-id="5acbd-173">İfade türü ve var olan özellik türü farklı olduğunda örtük dönüşüm mümkünse gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="5acbd-173">SET performs implicit conversion if possible when the expression type and the existing property type are different.</span></span>
- <span data-ttu-id="5acbd-174">Mevcut olmayan Sistem özellikleri başvurulan eylem başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="5acbd-174">Action fails if non-existent system properties were referenced.</span></span>
- <span data-ttu-id="5acbd-175">Mevcut olmayan kullanıcı özelliklerini başvurulan, eylem başarısız olmaz.</span><span class="sxs-lookup"><span data-stu-id="5acbd-175">Action does not fail if non-existent user properties were referenced.</span></span>
- <span data-ttu-id="5acbd-176">Mevcut olmayan kullanıcı özelliği "Bilinmiyor" olarak dahili olarak, aynı topluca aşağıdaki değerlendirilir [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) işleçleri değerlendirirken.</span><span class="sxs-lookup"><span data-stu-id="5acbd-176">A non-existent user property is evaluated as "Unknown" internally, following the same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5acbd-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5acbd-177">Next steps</span></span>

- [<span data-ttu-id="5acbd-178">SQLRuleAction sınıfı</span><span class="sxs-lookup"><span data-stu-id="5acbd-178">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [<span data-ttu-id="5acbd-179">SQLFilter sınıfı</span><span class="sxs-lookup"><span data-stu-id="5acbd-179">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
