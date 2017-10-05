---
title: "Azure hizmet veri yolu SQLFilter söz dizimi başvurusu | Microsoft Docs"
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
ms.openlocfilehash: 3aaec8f9b6a3bbcf814f771405c3b589de6f7ae0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="sqlfilter-syntax"></a><span data-ttu-id="e62a3-103">SQLFilter sözdizimi</span><span class="sxs-lookup"><span data-stu-id="e62a3-103">SQLFilter syntax</span></span>

<span data-ttu-id="e62a3-104">A *SqlFilter* örneği [SqlFilter sınıfı](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)ve karşı hesaplanan bir SQL dil temelli bir filtre ifadesi temsil eden bir [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="e62a3-104">A *SqlFilter* is an instance of the [SqlFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), and represents a SQL language-based filter expression that is evaluated against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="e62a3-105">Bir SqlFilter SQL 92 standart kümesini destekler.</span><span class="sxs-lookup"><span data-stu-id="e62a3-105">A SqlFilter supports a subset of the SQL-92 standard.</span></span>  
  
 <span data-ttu-id="e62a3-106">Bu konu SqlFilter dilbilgisi ayrıntılarını listeler.</span><span class="sxs-lookup"><span data-stu-id="e62a3-106">This topic lists details about SqlFilter grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="e62a3-107">Bağımsız Değişkenler</span><span class="sxs-lookup"><span data-stu-id="e62a3-107">Arguments</span></span>  
  
-   <span data-ttu-id="e62a3-108">`<scope>`kapsamını belirten isteğe bağlı bir dize `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="e62a3-108">`<scope>` is an optional string indicating the scope of the `<property_name>`.</span></span> <span data-ttu-id="e62a3-109">Geçerli değerler `sys` veya `user`.</span><span class="sxs-lookup"><span data-stu-id="e62a3-109">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="e62a3-110">`sys` Değeri gösterir sistemi kapsamı nerede `<property_name>` bir ortak özellik adı [BrokeredMessage sınıfı](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="e62a3-110">The `sys` value indicates system scope where `<property_name>` is a public property name of the [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="e62a3-111">`user`Kullanıcı kapsam gösterir nerede `<property_name>` , bir anahtar [BrokeredMessage sınıfı](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) sözlük.</span><span class="sxs-lookup"><span data-stu-id="e62a3-111">`user` indicates user scope where `<property_name>` is a key of the [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="e62a3-112">`user`Kapsam ise varsayılan kapsamı `<scope>` belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="e62a3-112">`user` scope is the default scope if `<scope>` is not specified.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="e62a3-113">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="e62a3-113">Remarks</span></span>

<span data-ttu-id="e62a3-114">Mevcut olmayan kullanıcı özelliği erişme denemesi bir hata olduğundan mevcut olmayan sistem özelliği erişme denemesi bir hata var.</span><span class="sxs-lookup"><span data-stu-id="e62a3-114">An attempt to access a non-existent system property is an error, while an attempt to access a non-existent user property is not an error.</span></span> <span data-ttu-id="e62a3-115">Bunun yerine, mevcut olmayan kullanıcı özelliği bilinmeyen bir değere dahili olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="e62a3-115">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="e62a3-116">Bilinmeyen bir değere özel işleci değerlendirme sırasında kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="e62a3-116">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="e62a3-117">property_name</span><span class="sxs-lookup"><span data-stu-id="e62a3-117">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="e62a3-118">Bağımsız Değişkenler</span><span class="sxs-lookup"><span data-stu-id="e62a3-118">Arguments</span></span>  

 <span data-ttu-id="e62a3-119">`<regular_identifier>`bir dize aşağıdaki normal ifade tarafından temsil edilen:</span><span class="sxs-lookup"><span data-stu-id="e62a3-119">`<regular_identifier>` is a string represented by the following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
<span data-ttu-id="e62a3-120">Bu dilbilgisi bir harf ile başlayıp bir veya daha fazla alt çizgi/harf/basamaklı tarafından izlenen herhangi bir dize anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e62a3-120">This grammar means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
<span data-ttu-id="e62a3-121">`[:IsLetter:]`bir Unicode harf kategorilere herhangi bir Unicode karakter anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e62a3-121">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="e62a3-122">`System.Char.IsLetter(c)`döndürür `true` varsa `c` bir Unicode harf.</span><span class="sxs-lookup"><span data-stu-id="e62a3-122">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
<span data-ttu-id="e62a3-123">`[:IsDigit:]`ondalık bir sayı kategorilere herhangi bir Unicode karakter anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e62a3-123">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="e62a3-124">`System.Char.IsDigit(c)`döndürür `true` varsa `c` Unicode sayıdır.</span><span class="sxs-lookup"><span data-stu-id="e62a3-124">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
<span data-ttu-id="e62a3-125">A `<regular_identifier>` ayrılmış bir anahtar sözcük olamaz.</span><span class="sxs-lookup"><span data-stu-id="e62a3-125">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
<span data-ttu-id="e62a3-126">`<delimited_identifier>`sol/sağ köşeli ayraç ([]) içine herhangi bir dize değil.</span><span class="sxs-lookup"><span data-stu-id="e62a3-126">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="e62a3-127">Sağ köşeli ayraç iki sağ köşeli temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="e62a3-127">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="e62a3-128">Örnekleri aşağıda verilmiştir `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="e62a3-128">The following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
<span data-ttu-id="e62a3-129">`<quoted_identifier>`ile çift tırnak işaretleri arasına herhangi bir dize değil.</span><span class="sxs-lookup"><span data-stu-id="e62a3-129">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="e62a3-130">Çift tırnak işareti tanımlayıcıda iki çift tırnak işareti temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="e62a3-130">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="e62a3-131">Bir dize sabiti ile kolayca çakışabilir çünkü tırnak işaretli tanımlayıcılar kullanmak için önerilmez.</span><span class="sxs-lookup"><span data-stu-id="e62a3-131">It is not recommended to use quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="e62a3-132">Sınırlandırılmış bir kimlik mümkünse kullanın.</span><span class="sxs-lookup"><span data-stu-id="e62a3-132">Use a delimited identifier if possible.</span></span> <span data-ttu-id="e62a3-133">Aşağıdaki örneğidir `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="e62a3-133">The following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="e62a3-134">düzeni</span><span class="sxs-lookup"><span data-stu-id="e62a3-134">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="e62a3-135">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="e62a3-135">Remarks</span></span>
  
<span data-ttu-id="e62a3-136">`<pattern>`bir dize olarak değerlendirilen bir ifade olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e62a3-136">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="e62a3-137">LIKE işleci için bir desen olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e62a3-137">It is used as a pattern for the LIKE operator.</span></span>      <span data-ttu-id="e62a3-138">Aşağıdaki joker karakterleri içerebilir:</span><span class="sxs-lookup"><span data-stu-id="e62a3-138">It can contain the following wildcard characters:</span></span>  
  
-   <span data-ttu-id="e62a3-139">`%`: Herhangi bir dize sıfır veya daha fazla karakter.</span><span class="sxs-lookup"><span data-stu-id="e62a3-139">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="e62a3-140">`_`: Herhangi bir tek karakteri.</span><span class="sxs-lookup"><span data-stu-id="e62a3-140">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="e62a3-141">escape_char</span><span class="sxs-lookup"><span data-stu-id="e62a3-141">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="e62a3-142">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="e62a3-142">Remarks</span></span>  

<span data-ttu-id="e62a3-143">`<escape_char>`dize uzunluğu 1 olarak değerlendirilen bir ifade olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e62a3-143">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="e62a3-144">LIKE işleci için bir kaçış karakteri olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e62a3-144">It is used as an escape character for the LIKE operator.</span></span>  
  
 <span data-ttu-id="e62a3-145">Örneğin, `property LIKE 'ABC\%' ESCAPE '\'` eşleşen `ABC%` ile başlayan bir dize yerine `ABC`.</span><span class="sxs-lookup"><span data-stu-id="e62a3-145">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="e62a3-146">sabiti</span><span class="sxs-lookup"><span data-stu-id="e62a3-146">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="e62a3-147">Bağımsız Değişkenler</span><span class="sxs-lookup"><span data-stu-id="e62a3-147">Arguments</span></span>  
  
-   <span data-ttu-id="e62a3-148">`<integer_constant>`yalnızca tırnak işaretleri içine değil ve ondalık basamak içeren değil sayı dizesidir.</span><span class="sxs-lookup"><span data-stu-id="e62a3-148">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="e62a3-149">Değerleri olarak depolanan `System.Int64` dahili olarak, aynı aralık izleyin.</span><span class="sxs-lookup"><span data-stu-id="e62a3-149">The values are stored as `System.Int64` internally, and follow the same range.</span></span>  
  
     <span data-ttu-id="e62a3-150">Bu, uzun sabitleri örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e62a3-150">These are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="e62a3-151">`<decimal_constant>`yalnızca tırnak işaretleri içine değil ve ondalık içeren sayı dizesidir.</span><span class="sxs-lookup"><span data-stu-id="e62a3-151">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="e62a3-152">Değerleri olarak depolanan `System.Double` dahili olarak, aynı aralık/duyarlık izleyin.</span><span class="sxs-lookup"><span data-stu-id="e62a3-152">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span>  
  
     <span data-ttu-id="e62a3-153">Sonraki bir sürümde tam sayı semantiğini desteklemek için farklı bir veri türü bu sayı depolanabilir, arka plandaki olgu üzerinde doğrulamamalısınız veri türü olduğundan `System.Double` için `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="e62a3-153">In a future version, this number might be stored in a different data type to support exact number semantics, so you should not rely on the fact the underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="e62a3-154">Ondalık sabitleri örnekleri verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e62a3-154">The following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="e62a3-155">`<approximate_number_constant>`bir sayı yazılmış bilimsel gösterim şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="e62a3-155">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="e62a3-156">Değerleri olarak depolanan `System.Double` dahili olarak, aynı aralık/duyarlık izleyin.</span><span class="sxs-lookup"><span data-stu-id="e62a3-156">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span> <span data-ttu-id="e62a3-157">Yaklaşık sayı sabitleri örnekleri verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e62a3-157">The following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="e62a3-158">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="e62a3-158">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="e62a3-159">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="e62a3-159">Remarks</span></span>  

<span data-ttu-id="e62a3-160">Boole sabitleri anahtar sözcükleri tarafından temsil edilen **TRUE** veya **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="e62a3-160">Boolean constants are represented by the keywords **TRUE** or **FALSE**.</span></span> <span data-ttu-id="e62a3-161">Değerleri olarak depolanan `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="e62a3-161">The values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="e62a3-162">string_constant</span><span class="sxs-lookup"><span data-stu-id="e62a3-162">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="e62a3-163">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="e62a3-163">Remarks</span></span>  

<span data-ttu-id="e62a3-164">Dize sabitleri tek tırnak işaretleri içine ve geçerli Unicode karakterler içerir.</span><span class="sxs-lookup"><span data-stu-id="e62a3-164">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="e62a3-165">Bir dize sabitine katıştırılmış tek tırnak işareti, iki tırnak işaretleri tek olarak temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="e62a3-165">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="e62a3-166">İşlevi</span><span class="sxs-lookup"><span data-stu-id="e62a3-166">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="e62a3-167">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="e62a3-167">Remarks</span></span>
  
<span data-ttu-id="e62a3-168">`newid()` İşlev döndürür bir **System.Guid** tarafından oluşturulan `System.Guid.NewGuid()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e62a3-168">The `newid()` function returns a **System.Guid** generated by the `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="e62a3-169">`property(name)` İşlevi tarafından başvurulan özelliğinin değerini döndürür `name`.</span><span class="sxs-lookup"><span data-stu-id="e62a3-169">The `property(name)` function returns the value of the property referenced by `name`.</span></span> <span data-ttu-id="e62a3-170">`name` Değeri bir string değeri döndürür geçerli bir ifade olabilir.</span><span class="sxs-lookup"><span data-stu-id="e62a3-170">The `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="e62a3-171">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="e62a3-171">Considerations</span></span>
  
<span data-ttu-id="e62a3-172">Aşağıdakileri göz önünde bulundurun [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantiği:</span><span class="sxs-lookup"><span data-stu-id="e62a3-172">Consider the following [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantics:</span></span>  
  
-   <span data-ttu-id="e62a3-173">Özellik adları büyük/küçük harfe duyarsızdır.</span><span class="sxs-lookup"><span data-stu-id="e62a3-173">Property names are case-insensitive.</span></span>  
  
-   <span data-ttu-id="e62a3-174">C# örtük dönüşüm semantiği mümkün olduğunca işleçleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="e62a3-174">Operators follow C# implicit conversion semantics whenever possible.</span></span>  
  
-   <span data-ttu-id="e62a3-175">Sistem özellikleri olan ortak özellikler, gösterilen [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) örnekleri.</span><span class="sxs-lookup"><span data-stu-id="e62a3-175">System properties are public properties exposed in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) instances.</span></span>  
  
    <span data-ttu-id="e62a3-176">Aşağıdakileri göz önünde bulundurun `IS [NOT] NULL` semantiği:</span><span class="sxs-lookup"><span data-stu-id="e62a3-176">Consider the following `IS [NOT] NULL` semantics:</span></span>  
  
    -   <span data-ttu-id="e62a3-177">`property IS NULL`olarak değerlendirilir `true` özelliği yok veya özelliğin değeri, `null`.</span><span class="sxs-lookup"><span data-stu-id="e62a3-177">`property IS NULL` is evaluated as `true` if either the property doesn't exist or the property's value is `null`.</span></span>  
  
### <a name="property-evaluation-semantics"></a><span data-ttu-id="e62a3-178">Özellik değerlendirme semantiği</span><span class="sxs-lookup"><span data-stu-id="e62a3-178">Property evaluation semantics</span></span>  
  
-   <span data-ttu-id="e62a3-179">Mevcut olmayan sistem özelliği değerlendirmek için girişiminde oluşturur bir [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) özel durum.</span><span class="sxs-lookup"><span data-stu-id="e62a3-179">An attempt to evaluate a non-existent system property throws a [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span></span>  
  
-   <span data-ttu-id="e62a3-180">Var olmayan bir özellik olarak dahili olarak değerlendirilir **bilinmeyen**.</span><span class="sxs-lookup"><span data-stu-id="e62a3-180">A property that does not exist is internally evaluated as **unknown**.</span></span>  
  
 <span data-ttu-id="e62a3-181">Aritmetik işleçler bilinmeyen hesaplanmasında:</span><span class="sxs-lookup"><span data-stu-id="e62a3-181">Unknown evaluation in arithmetic operators:</span></span>  
  
-   <span data-ttu-id="e62a3-182">İkili işleçler varsa sol ve sağ tarafındaki işlenenleri olarak değerlendirildiği için **bilinmeyen**, sonuç sonra **bilinmeyen**.</span><span class="sxs-lookup"><span data-stu-id="e62a3-182">For binary operators, if either the left and/or right side of operands is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
-   <span data-ttu-id="e62a3-183">Birli işleçleri işleneni olarak değerlendirildiği taktirde **bilinmeyen**, sonuç sonra **bilinmeyen**.</span><span class="sxs-lookup"><span data-stu-id="e62a3-183">For unary operators, if an operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="e62a3-184">İkili Karşılaştırma işleçleri bilinmeyen hesaplanmasında:</span><span class="sxs-lookup"><span data-stu-id="e62a3-184">Unknown evaluation in binary comparison operators:</span></span>  
  
-   <span data-ttu-id="e62a3-185">Varsa sol ve sağ tarafındaki işlenenleri olarak değerlendirildiği **bilinmeyen**, sonuç sonra **bilinmeyen**.</span><span class="sxs-lookup"><span data-stu-id="e62a3-185">If either the left and/or right side of operands is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="e62a3-186">Bilinmeyen hesaplanmasında `[NOT] LIKE`:</span><span class="sxs-lookup"><span data-stu-id="e62a3-186">Unknown evaluation in `[NOT] LIKE`:</span></span>  
  
-   <span data-ttu-id="e62a3-187">Tüm işleneni olarak değerlendirildiği taktirde **bilinmeyen**, sonuç sonra **bilinmeyen**.</span><span class="sxs-lookup"><span data-stu-id="e62a3-187">If any operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="e62a3-188">Bilinmeyen hesaplanmasında `[NOT] IN`:</span><span class="sxs-lookup"><span data-stu-id="e62a3-188">Unknown evaluation in `[NOT] IN`:</span></span>  
  
-   <span data-ttu-id="e62a3-189">Sol işleneni olarak değerlendirildiği taktirde **bilinmeyen**, sonuç sonra **bilinmeyen**.</span><span class="sxs-lookup"><span data-stu-id="e62a3-189">If the left operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="e62a3-190">Bilinmeyen hesaplanmasında **ve** işleci:</span><span class="sxs-lookup"><span data-stu-id="e62a3-190">Unknown evaluation in **AND** operator:</span></span>  
  
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
  
 <span data-ttu-id="e62a3-191">Bilinmeyen hesaplanmasında **veya** işleci:</span><span class="sxs-lookup"><span data-stu-id="e62a3-191">Unknown evaluation in **OR** operator:</span></span>  
  
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
  
### <a name="operator-binding-semantics"></a><span data-ttu-id="e62a3-192">İşleç bağlama semantiği</span><span class="sxs-lookup"><span data-stu-id="e62a3-192">Operator binding semantics</span></span>
  
-   <span data-ttu-id="e62a3-193">Karşılaştırma işleçleri gibi `>`, `>=`, `<`, `<=`, `!=`, ve `=` veri türü promosyonlar ve örtük dönüşümler bağlama C# işleci aynı topluca izleyin.</span><span class="sxs-lookup"><span data-stu-id="e62a3-193">Comparison operators such as `>`, `>=`, `<`, `<=`, `!=`, and `=` follow the same semantics as the C# operator binding in data type promotions and implicit conversions.</span></span>  
  
-   <span data-ttu-id="e62a3-194">Aritmetik işleçler gibi `+`, `-`, `*`, `/`, ve `%` veri türü promosyonlar ve örtük dönüşümler bağlama C# işleci aynı topluca izleyin.</span><span class="sxs-lookup"><span data-stu-id="e62a3-194">Arithmetic operators such as `+`, `-`, `*`, `/`, and `%` follow the same semantics as the C# operator binding in data type promotions and implicit conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e62a3-195">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e62a3-195">Next steps</span></span>

- [<span data-ttu-id="e62a3-196">SQLFilter sınıfı</span><span class="sxs-lookup"><span data-stu-id="e62a3-196">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [<span data-ttu-id="e62a3-197">SQLRuleAction sınıfı</span><span class="sxs-lookup"><span data-stu-id="e62a3-197">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)