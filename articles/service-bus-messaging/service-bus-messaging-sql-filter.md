---
title: "aaaAzure hizmet veri yolu SQLFilter söz dizimi başvurusu | Microsoft Docs"
description: "SQLFilter dilbilgisi hakkında ayrıntılar."
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
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: ea49d42e343a6b324eb34c7831ff6be2855346e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sqlfilter-syntax"></a><span data-ttu-id="1f5df-103">SQLFilter sözdizimi</span><span class="sxs-lookup"><span data-stu-id="1f5df-103">SQLFilter syntax</span></span>

<span data-ttu-id="1f5df-104">A *SqlFilter* hello örneği [SqlFilter sınıfı](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)ve karşı hesaplanan bir SQL dil temelli bir filtre ifadesi temsil eden bir [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="1f5df-104">A *SqlFilter* is an instance of hello [SqlFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), and represents a SQL language-based filter expression that is evaluated against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="1f5df-105">Bir SqlFilter hello SQL 92 standart kümesini destekler.</span><span class="sxs-lookup"><span data-stu-id="1f5df-105">A SqlFilter supports a subset of hello SQL-92 standard.</span></span>  
  
 <span data-ttu-id="1f5df-106">Bu konu SqlFilter dilbilgisi ayrıntılarını listeler.</span><span class="sxs-lookup"><span data-stu-id="1f5df-106">This topic lists details about SqlFilter grammar.</span></span>  
  
```  
<predicate ::=  
      { NOT <predicate> }  
      | <predicate> AND <predicate>  
      | <predicate> OR <predicate>  
      | <expression> { = | <> | != | > | >= | < | <= } <expression>  
      | <property> IS [NOT] NULL  
      | <expression> [NOT] IN ( <expression> [, ...n] )  
      | <expression> [NOT] LIKE <pattern> [ESCAPE <escape_char>]  
      | EXISTS ( <property> )  
      | ( <predicate> )  
  
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
  
## <a name="arguments"></a><span data-ttu-id="1f5df-107">Bağımsız Değişkenler</span><span class="sxs-lookup"><span data-stu-id="1f5df-107">Arguments</span></span>  
  
-   <span data-ttu-id="1f5df-108">`<scope>`Merhaba hello kapsamını belirten isteğe bağlı bir dize `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="1f5df-108">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="1f5df-109">Geçerli değerler `sys` veya `user`.</span><span class="sxs-lookup"><span data-stu-id="1f5df-109">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="1f5df-110">Merhaba `sys` değeri gösterir sistemi kapsamı nerede `<property_name>` hello ortak özelliği adıdır [BrokeredMessage sınıfı](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="1f5df-110">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="1f5df-111">`user`Kullanıcı kapsam gösterir nerede `<property_name>` hello anahtarıdır [BrokeredMessage sınıfı](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) sözlük.</span><span class="sxs-lookup"><span data-stu-id="1f5df-111">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="1f5df-112">`user`Kapsam ise hello varsayılan kapsam `<scope>` belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="1f5df-112">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="1f5df-113">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="1f5df-113">Remarks</span></span>

<span data-ttu-id="1f5df-114">Bir girişim tooaccess mevcut olmayan kullanıcı özelliği bir hata olduğundan girişimi tooaccess mevcut olmayan sistem bir hata değildir.</span><span class="sxs-lookup"><span data-stu-id="1f5df-114">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="1f5df-115">Bunun yerine, mevcut olmayan kullanıcı özelliği bilinmeyen bir değere dahili olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="1f5df-115">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="1f5df-116">Bilinmeyen bir değere özel işleci değerlendirme sırasında kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="1f5df-116">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="1f5df-117">property_name</span><span class="sxs-lookup"><span data-stu-id="1f5df-117">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="1f5df-118">Bağımsız Değişkenler</span><span class="sxs-lookup"><span data-stu-id="1f5df-118">Arguments</span></span>  

 <span data-ttu-id="1f5df-119">`<regular_identifier>`Merhaba tarafından temsil edilen bir dize normal ifade takip ediyor:</span><span class="sxs-lookup"><span data-stu-id="1f5df-119">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
<span data-ttu-id="1f5df-120">Bu dilbilgisi bir harf ile başlayıp bir veya daha fazla alt çizgi/harf/basamaklı tarafından izlenen herhangi bir dize anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1f5df-120">This grammar means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
<span data-ttu-id="1f5df-121">`[:IsLetter:]`bir Unicode harf kategorilere herhangi bir Unicode karakter anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1f5df-121">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="1f5df-122">`System.Char.IsLetter(c)`döndürür `true` varsa `c` bir Unicode harf.</span><span class="sxs-lookup"><span data-stu-id="1f5df-122">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
<span data-ttu-id="1f5df-123">`[:IsDigit:]`ondalık bir sayı kategorilere herhangi bir Unicode karakter anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1f5df-123">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="1f5df-124">`System.Char.IsDigit(c)`döndürür `true` varsa `c` Unicode sayıdır.</span><span class="sxs-lookup"><span data-stu-id="1f5df-124">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
<span data-ttu-id="1f5df-125">A `<regular_identifier>` ayrılmış bir anahtar sözcük olamaz.</span><span class="sxs-lookup"><span data-stu-id="1f5df-125">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
<span data-ttu-id="1f5df-126">`<delimited_identifier>`sol/sağ köşeli ayraç ([]) içine herhangi bir dize değil.</span><span class="sxs-lookup"><span data-stu-id="1f5df-126">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="1f5df-127">Sağ köşeli ayraç iki sağ köşeli temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="1f5df-127">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="1f5df-128">Merhaba örnekleri aşağıda verilmiştir `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="1f5df-128">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
<span data-ttu-id="1f5df-129">`<quoted_identifier>`ile çift tırnak işaretleri arasına herhangi bir dize değil.</span><span class="sxs-lookup"><span data-stu-id="1f5df-129">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="1f5df-130">Çift tırnak işareti tanımlayıcıda iki çift tırnak işareti temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="1f5df-130">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="1f5df-131">Bir dize sabiti ile kolayca çakışabilir çünkü toouse tanımlayıcıları tırnak içine alınmış önerilmez.</span><span class="sxs-lookup"><span data-stu-id="1f5df-131">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="1f5df-132">Sınırlandırılmış bir kimlik mümkünse kullanın.</span><span class="sxs-lookup"><span data-stu-id="1f5df-132">Use a delimited identifier if possible.</span></span> <span data-ttu-id="1f5df-133">Merhaba örneği aşağıdadır `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="1f5df-133">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="1f5df-134">düzeni</span><span class="sxs-lookup"><span data-stu-id="1f5df-134">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="1f5df-135">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="1f5df-135">Remarks</span></span>
  
<span data-ttu-id="1f5df-136">`<pattern>`bir dize olarak değerlendirilen bir ifade olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1f5df-136">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="1f5df-137">İşleç gibi hello kalıp olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f5df-137">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="1f5df-138">Merhaba aşağıdaki joker karakterleri içerebilir:</span><span class="sxs-lookup"><span data-stu-id="1f5df-138">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="1f5df-139">`%`: Herhangi bir dize sıfır veya daha fazla karakter.</span><span class="sxs-lookup"><span data-stu-id="1f5df-139">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="1f5df-140">`_`: Herhangi bir tek karakteri.</span><span class="sxs-lookup"><span data-stu-id="1f5df-140">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="1f5df-141">escape_char</span><span class="sxs-lookup"><span data-stu-id="1f5df-141">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="1f5df-142">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="1f5df-142">Remarks</span></span>  

<span data-ttu-id="1f5df-143">`<escape_char>`dize uzunluğu 1 olarak değerlendirilen bir ifade olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1f5df-143">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="1f5df-144">Merhaba işleci gibi bir kaçış karakteri olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f5df-144">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="1f5df-145">Örneğin, `property LIKE 'ABC\%' ESCAPE '\'` eşleşen `ABC%` ile başlayan bir dize yerine `ABC`.</span><span class="sxs-lookup"><span data-stu-id="1f5df-145">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="1f5df-146">sabiti</span><span class="sxs-lookup"><span data-stu-id="1f5df-146">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="1f5df-147">Bağımsız Değişkenler</span><span class="sxs-lookup"><span data-stu-id="1f5df-147">Arguments</span></span>  
  
-   <span data-ttu-id="1f5df-148">`<integer_constant>`yalnızca tırnak işaretleri içine değil ve ondalık basamak içeren değil sayı dizesidir.</span><span class="sxs-lookup"><span data-stu-id="1f5df-148">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="1f5df-149">Merhaba depolanan değerlerin olarak `System.Int64` dahili olarak ve izleme hello aynı aralık.</span><span class="sxs-lookup"><span data-stu-id="1f5df-149">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="1f5df-150">Bu, uzun sabitleri örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1f5df-150">These are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="1f5df-151">`<decimal_constant>`yalnızca tırnak işaretleri içine değil ve ondalık içeren sayı dizesidir.</span><span class="sxs-lookup"><span data-stu-id="1f5df-151">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="1f5df-152">Merhaba depolanan değerlerin olarak `System.Double` dahili olarak ve aynı aralığı/duyarlık hello izleyin.</span><span class="sxs-lookup"><span data-stu-id="1f5df-152">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="1f5df-153">Sonraki bir sürümde bir farklı veri türü toosupport tam sayı semantiği bu sayı depolanabilir, hello olgu hello altta yatan doğrulamamalısınız veri türü olduğundan `System.Double` için `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="1f5df-153">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="1f5df-154">Merhaba, ondalık sabitleri örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1f5df-154">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="1f5df-155">`<approximate_number_constant>`bir sayı yazılmış bilimsel gösterim şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1f5df-155">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="1f5df-156">Merhaba depolanan değerlerin olarak `System.Double` dahili olarak ve aynı aralığı/duyarlık hello izleyin.</span><span class="sxs-lookup"><span data-stu-id="1f5df-156">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="1f5df-157">Merhaba, yaklaşık sayı sabitleri örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1f5df-157">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="1f5df-158">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="1f5df-158">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="1f5df-159">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="1f5df-159">Remarks</span></span>  

<span data-ttu-id="1f5df-160">Boole sabitleri hello anahtar tarafından temsil edilen **TRUE** veya **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="1f5df-160">Boolean constants are represented by hello keywords **TRUE** or **FALSE**.</span></span> <span data-ttu-id="1f5df-161">Merhaba depolanan değerlerin olarak `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="1f5df-161">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="1f5df-162">string_constant</span><span class="sxs-lookup"><span data-stu-id="1f5df-162">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="1f5df-163">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="1f5df-163">Remarks</span></span>  

<span data-ttu-id="1f5df-164">Dize sabitleri tek tırnak işaretleri içine ve geçerli Unicode karakterler içerir.</span><span class="sxs-lookup"><span data-stu-id="1f5df-164">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="1f5df-165">Bir dize sabitine katıştırılmış tek tırnak işareti, iki tırnak işaretleri tek olarak temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="1f5df-165">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="1f5df-166">İşlevi</span><span class="sxs-lookup"><span data-stu-id="1f5df-166">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="1f5df-167">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="1f5df-167">Remarks</span></span>
  
<span data-ttu-id="1f5df-168">Merhaba `newid()` işlev döndürür bir **System.Guid** hello tarafından oluşturulan `System.Guid.NewGuid()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1f5df-168">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="1f5df-169">Merhaba `property(name)` işlevi tarafından başvurulan hello özelliğinin hello değeri döndürür `name`.</span><span class="sxs-lookup"><span data-stu-id="1f5df-169">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="1f5df-170">Merhaba `name` değeri bir string değeri döndürür geçerli bir ifade olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f5df-170">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="1f5df-171">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="1f5df-171">Considerations</span></span>
  
<span data-ttu-id="1f5df-172">Merhaba aşağıdakileri göz önünde bulundurun [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantiği:</span><span class="sxs-lookup"><span data-stu-id="1f5df-172">Consider hello following [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantics:</span></span>  
  
-   <span data-ttu-id="1f5df-173">Özellik adları büyük/küçük harfe duyarsızdır.</span><span class="sxs-lookup"><span data-stu-id="1f5df-173">Property names are case-insensitive.</span></span>  
  
-   <span data-ttu-id="1f5df-174">C# örtük dönüşüm semantiği mümkün olduğunca işleçleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="1f5df-174">Operators follow C# implicit conversion semantics whenever possible.</span></span>  
  
-   <span data-ttu-id="1f5df-175">Sistem özellikleri olan ortak özellikler, gösterilen [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) örnekleri.</span><span class="sxs-lookup"><span data-stu-id="1f5df-175">System properties are public properties exposed in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) instances.</span></span>  
  
    <span data-ttu-id="1f5df-176">Merhaba aşağıdakileri göz önünde bulundurun `IS [NOT] NULL` semantiği:</span><span class="sxs-lookup"><span data-stu-id="1f5df-176">Consider hello following `IS [NOT] NULL` semantics:</span></span>  
  
    -   <span data-ttu-id="1f5df-177">`property IS NULL`olarak değerlendirilir `true` ya da hello özelliği mevcut değil veya özelliğin değeri hello ise `null`.</span><span class="sxs-lookup"><span data-stu-id="1f5df-177">`property IS NULL` is evaluated as `true` if either hello property doesn't exist or hello property's value is `null`.</span></span>  
  
### <a name="property-evaluation-semantics"></a><span data-ttu-id="1f5df-178">Özellik değerlendirme semantiği</span><span class="sxs-lookup"><span data-stu-id="1f5df-178">Property evaluation semantics</span></span>  
  
-   <span data-ttu-id="1f5df-179">Mevcut olmayan sistem özelliği oluşturur girişimi tooevaluate bir [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) özel durum.</span><span class="sxs-lookup"><span data-stu-id="1f5df-179">An attempt tooevaluate a non-existent system property throws a [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span></span>  
  
-   <span data-ttu-id="1f5df-180">Var olmayan bir özellik olarak dahili olarak değerlendirilir **bilinmeyen**.</span><span class="sxs-lookup"><span data-stu-id="1f5df-180">A property that does not exist is internally evaluated as **unknown**.</span></span>  
  
 <span data-ttu-id="1f5df-181">Aritmetik işleçler bilinmeyen hesaplanmasında:</span><span class="sxs-lookup"><span data-stu-id="1f5df-181">Unknown evaluation in arithmetic operators:</span></span>  
  
-   <span data-ttu-id="1f5df-182">Ya da sola ve/veya işlenenler sağ tarafındaki Merhaba, ikili işleçler için olarak değerlendirilir **bilinmeyen**, hello sonuç sonra **bilinmeyen**.</span><span class="sxs-lookup"><span data-stu-id="1f5df-182">For binary operators, if either hello left and/or right side of operands is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
-   <span data-ttu-id="1f5df-183">Birli işleçleri işleneni olarak değerlendirildiği taktirde **bilinmeyen**, hello sonuç sonra **bilinmeyen**.</span><span class="sxs-lookup"><span data-stu-id="1f5df-183">For unary operators, if an operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="1f5df-184">İkili Karşılaştırma işleçleri bilinmeyen hesaplanmasında:</span><span class="sxs-lookup"><span data-stu-id="1f5df-184">Unknown evaluation in binary comparison operators:</span></span>  
  
-   <span data-ttu-id="1f5df-185">Ya da sola ve/veya işlenenler sağ tarafındaki hello varsa olarak değerlendirilir **bilinmeyen**, hello sonuç sonra **bilinmeyen**.</span><span class="sxs-lookup"><span data-stu-id="1f5df-185">If either hello left and/or right side of operands is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="1f5df-186">Bilinmeyen hesaplanmasında `[NOT] LIKE`:</span><span class="sxs-lookup"><span data-stu-id="1f5df-186">Unknown evaluation in `[NOT] LIKE`:</span></span>  
  
-   <span data-ttu-id="1f5df-187">Tüm işleneni olarak değerlendirildiği taktirde **bilinmeyen**, hello sonuç sonra **bilinmeyen**.</span><span class="sxs-lookup"><span data-stu-id="1f5df-187">If any operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="1f5df-188">Bilinmeyen hesaplanmasında `[NOT] IN`:</span><span class="sxs-lookup"><span data-stu-id="1f5df-188">Unknown evaluation in `[NOT] IN`:</span></span>  
  
-   <span data-ttu-id="1f5df-189">Sol işleneni hello olarak değerlendirildiği taktirde **bilinmeyen**, hello sonuç sonra **bilinmeyen**.</span><span class="sxs-lookup"><span data-stu-id="1f5df-189">If hello left operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="1f5df-190">Bilinmeyen hesaplanmasında **ve** işleci:</span><span class="sxs-lookup"><span data-stu-id="1f5df-190">Unknown evaluation in **AND** operator:</span></span>  
  
```  
+---+---+---+---+  
|AND| T | F | U |  
+---+---+---+---+  
| T | T | F | U |  
+---+---+---+---+  
| F | F | F | F |  
+---+---+---+---+  
| U | U | F | U |  
+---+---+---+---+  
```  
  
 <span data-ttu-id="1f5df-191">Bilinmeyen hesaplanmasında **veya** işleci:</span><span class="sxs-lookup"><span data-stu-id="1f5df-191">Unknown evaluation in **OR** operator:</span></span>  
  
```  
+---+---+---+---+  
|OR | T | F | U |  
+---+---+---+---+  
| T | T | T | T |  
+---+---+---+---+  
| F | T | F | U |  
+---+---+---+---+  
| U | T | U | U |  
+---+---+---+---+  
```  
  
### <a name="operator-binding-semantics"></a><span data-ttu-id="1f5df-192">İşleç bağlama semantiği</span><span class="sxs-lookup"><span data-stu-id="1f5df-192">Operator binding semantics</span></span>
  
-   <span data-ttu-id="1f5df-193">Karşılaştırma işleçleri gibi `>`, `>=`, `<`, `<=`, `!=`, ve `=` izleyin hello aynı veri bağlama hello C# işleci topluca promosyonlar ve örtük dönüşümler yazın.</span><span class="sxs-lookup"><span data-stu-id="1f5df-193">Comparison operators such as `>`, `>=`, `<`, `<=`, `!=`, and `=` follow hello same semantics as hello C# operator binding in data type promotions and implicit conversions.</span></span>  
  
-   <span data-ttu-id="1f5df-194">Aritmetik işleçler gibi `+`, `-`, `*`, `/`, ve `%` izleyin hello aynı veri bağlama hello C# işleci topluca promosyonlar ve örtük dönüşümler yazın.</span><span class="sxs-lookup"><span data-stu-id="1f5df-194">Arithmetic operators such as `+`, `-`, `*`, `/`, and `%` follow hello same semantics as hello C# operator binding in data type promotions and implicit conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f5df-195">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1f5df-195">Next steps</span></span>

- [<span data-ttu-id="1f5df-196">SQLFilter sınıfı</span><span class="sxs-lookup"><span data-stu-id="1f5df-196">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [<span data-ttu-id="1f5df-197">SQLRuleAction sınıfı</span><span class="sxs-lookup"><span data-stu-id="1f5df-197">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)