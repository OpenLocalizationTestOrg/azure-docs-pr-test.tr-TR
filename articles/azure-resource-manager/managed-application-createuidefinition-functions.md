---
title: "Azure yönetilen uygulama kullanıcı Arabirimi tanımı işlevlerin oluşturma | Microsoft Docs"
description: "Azure yönetilen uygulamaları için kullanıcı Arabirimi tanımları oluşturulurken kullanılacak işlevleri açıklanmaktadır"
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
ms.openlocfilehash: 62ee10eb8e6f33cc4d828cf01b405c846bef8aa4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="createuidefinition-functions"></a><span data-ttu-id="eb44b-103">CreateUiDefinition işlevleri</span><span class="sxs-lookup"><span data-stu-id="eb44b-103">CreateUiDefinition functions</span></span>
<span data-ttu-id="eb44b-104">Bu bölüm bir CreateUiDefinition tüm desteklenen işlevlerini imzaları içerir.</span><span class="sxs-lookup"><span data-stu-id="eb44b-104">This section contains the signatures for all supported functions of a CreateUiDefinition.</span></span>

<span data-ttu-id="eb44b-105">Bir işlevi kullanmak için köşeli bildirimiyle koyun.</span><span class="sxs-lookup"><span data-stu-id="eb44b-105">To use a function, surround the declaration with square brackets.</span></span> <span data-ttu-id="eb44b-106">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="eb44b-106">For example:</span></span>

```json
"[function()]"
```

<span data-ttu-id="eb44b-107">Dizeler ve diğer işlevleri işlevi için parametre olarak başvurulabilir, ancak dizeler tek tırnak içine alınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eb44b-107">Strings and other functions can be referenced as parameters for a function, but strings must be surrounded in single quotes.</span></span> <span data-ttu-id="eb44b-108">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="eb44b-108">For example:</span></span>

```json
"[fn1(fn2(), 'foobar')]"
```

<span data-ttu-id="eb44b-109">Uygunsa, dot işleci kullanılarak bir işlev çıktısını özelliklerini başvuruda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="eb44b-109">Where applicable, you can reference properties of the output of a function by using the dot operator.</span></span> <span data-ttu-id="eb44b-110">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="eb44b-110">For example:</span></span>

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a><span data-ttu-id="eb44b-111">İşlevler başvurma</span><span class="sxs-lookup"><span data-stu-id="eb44b-111">Referencing functions</span></span>
<span data-ttu-id="eb44b-112">Bu işlevler, özellikleri veya bir CreateUiDefinition bağlamında çıkışları başvurmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="eb44b-112">These functions can be used to reference outputs from the properties or context of a CreateUiDefinition.</span></span>

### <a name="basics"></a><span data-ttu-id="eb44b-113">temel kavramları</span><span class="sxs-lookup"><span data-stu-id="eb44b-113">basics</span></span>
<span data-ttu-id="eb44b-114">Temel kavramları adımında tanımlı bir öğenin çıktı değerleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-114">Returns the output values of an element that is defined in the Basics step.</span></span>

<span data-ttu-id="eb44b-115">Aşağıdaki örnek adlı öğe çıktısı verir `foo` temelleri adımda:</span><span class="sxs-lookup"><span data-stu-id="eb44b-115">The following example returns the output of the element named `foo` in the Basics step:</span></span>

```json
"[basics('foo')]"
```

### <a name="steps"></a><span data-ttu-id="eb44b-116">Adımları</span><span class="sxs-lookup"><span data-stu-id="eb44b-116">steps</span></span>
<span data-ttu-id="eb44b-117">Belirtilen adımında tanımlı bir öğenin çıktı değerleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-117">Returns the output values of an element that is defined in the specified step.</span></span> <span data-ttu-id="eb44b-118">Temel kavramları adımda öğelerin çıkış değerleri almak için kullanın `basics()` yerine.</span><span class="sxs-lookup"><span data-stu-id="eb44b-118">To get the output values of elements in the Basics step, use `basics()` instead.</span></span>

<span data-ttu-id="eb44b-119">Aşağıdaki örnek adlı öğe çıktısı verir `bar` adlı adımda `foo`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-119">The following example returns the output of the element named `bar` in the step named `foo`:</span></span>

```json
"[steps('foo').bar]"
```

### <a name="location"></a><span data-ttu-id="eb44b-120">location</span><span class="sxs-lookup"><span data-stu-id="eb44b-120">location</span></span>
<span data-ttu-id="eb44b-121">Temel adımı veya geçerli bağlamı içinde seçilen konumu döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-121">Returns the location selected in the Basics step or the current context.</span></span>

<span data-ttu-id="eb44b-122">Aşağıdaki örnek döndürebilir `"westus"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-122">The following example could return `"westus"`:</span></span>

```json
"[location()]"
```

## <a name="string-functions"></a><span data-ttu-id="eb44b-123">Dize işlevleri</span><span class="sxs-lookup"><span data-stu-id="eb44b-123">String functions</span></span>
<span data-ttu-id="eb44b-124">Bu işlevler yalnızca JSON dizelerle kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="eb44b-124">These functions can only be used with JSON strings.</span></span>

### <a name="concat"></a><span data-ttu-id="eb44b-125">concat</span><span class="sxs-lookup"><span data-stu-id="eb44b-125">concat</span></span>
<span data-ttu-id="eb44b-126">Bir veya daha fazla art arda ekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-126">Concatenates one or more strings.</span></span>

<span data-ttu-id="eb44b-127">Örneğin, varsa çıkış değeri `element1` varsa `"bar"`, bu örnek dizesini döndürür sonra `"foobar!"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-127">For example, if the output value of `element1` if `"bar"`, then this example returns the string `"foobar!"`:</span></span>

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a><span data-ttu-id="eb44b-128">substring</span><span class="sxs-lookup"><span data-stu-id="eb44b-128">substring</span></span>
<span data-ttu-id="eb44b-129">Belirtilen dizenin alt dizeyi döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-129">Returns the substring of the specified string.</span></span> <span data-ttu-id="eb44b-130">Alt dizeyi belirtilen dizinden başlatır ve belirtilen uzunluğa sahip.</span><span class="sxs-lookup"><span data-stu-id="eb44b-130">The substring starts at the specified index and has the specified length.</span></span>

<span data-ttu-id="eb44b-131">Aşağıdaki örnek verir `"ftw"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-131">The following example returns `"ftw"`:</span></span>

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a><span data-ttu-id="eb44b-132">Değiştir</span><span class="sxs-lookup"><span data-stu-id="eb44b-132">replace</span></span>
<span data-ttu-id="eb44b-133">Geçerli dizesinde belirtilen dizenin tüm oluşumlarını başka dize ile değiştirilir bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-133">Returns a string in which all occurrences of the specified string in the current string are replaced with another string.</span></span>

<span data-ttu-id="eb44b-134">Aşağıdaki örnek verir `"Everything is awesome!"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-134">The following example returns `"Everything is awesome!"`:</span></span>

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a><span data-ttu-id="eb44b-135">GUID</span><span class="sxs-lookup"><span data-stu-id="eb44b-135">guid</span></span>
<span data-ttu-id="eb44b-136">Genel olarak benzersiz bir dize (GUID) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eb44b-136">Generates a globally unique string (GUID).</span></span>

<span data-ttu-id="eb44b-137">Aşağıdaki örnek döndürebilir `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-137">The following example could return `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span></span>

```json
"[guid()]"
```

### <a name="tolower"></a><span data-ttu-id="eb44b-138">toLower</span><span class="sxs-lookup"><span data-stu-id="eb44b-138">toLower</span></span>
<span data-ttu-id="eb44b-139">Küçük harfe dönüştürülmüş bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-139">Returns a string converted to lowercase.</span></span>

<span data-ttu-id="eb44b-140">Aşağıdaki örnek verir `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-140">The following example returns `"foobar"`:</span></span>

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a><span data-ttu-id="eb44b-141">toUpper</span><span class="sxs-lookup"><span data-stu-id="eb44b-141">toUpper</span></span>
<span data-ttu-id="eb44b-142">Büyük harfe dönüştürülmüş bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-142">Returns a string converted to uppercase.</span></span>

<span data-ttu-id="eb44b-143">Aşağıdaki örnek verir `"FOOBAR"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-143">The following example returns `"FOOBAR"`:</span></span>

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a><span data-ttu-id="eb44b-144">Toplama işlevleri</span><span class="sxs-lookup"><span data-stu-id="eb44b-144">Collection functions</span></span>
<span data-ttu-id="eb44b-145">Bu işlevler, JSON dizeler, dizileri ve nesneleri gibi koleksiyonlar ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="eb44b-145">These functions can be used with collections, like JSON strings, arrays and objects.</span></span>

### <a name="contains"></a><span data-ttu-id="eb44b-146">içerir</span><span class="sxs-lookup"><span data-stu-id="eb44b-146">contains</span></span>
<span data-ttu-id="eb44b-147">Döndürür `true` bir dizeyi belirtilen alt dizeyi içeren belirtilen değer bir dizi içeriyor veya belirtilen anahtar bir nesne içerir.</span><span class="sxs-lookup"><span data-stu-id="eb44b-147">Returns `true` if a string contains the specified substring, an array contains the specified value, or an object contains the specified key.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="eb44b-148">Örnek 1: dize</span><span class="sxs-lookup"><span data-stu-id="eb44b-148">Example 1: string</span></span>
<span data-ttu-id="eb44b-149">Aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-149">The following example returns `true`:</span></span>

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="eb44b-150">Örnek 2: dizi</span><span class="sxs-lookup"><span data-stu-id="eb44b-150">Example 2: array</span></span>
<span data-ttu-id="eb44b-151">Varsayın `element1` döndürür `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="eb44b-151">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="eb44b-152">Aşağıdaki örnek verir `false`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-152">The following example returns `false`:</span></span>

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="eb44b-153">Örnek 3: nesnesi</span><span class="sxs-lookup"><span data-stu-id="eb44b-153">Example 3: object</span></span>
<span data-ttu-id="eb44b-154">Varsayın `element1` döndürür:</span><span class="sxs-lookup"><span data-stu-id="eb44b-154">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="eb44b-155">Aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-155">The following example returns `true`:</span></span>

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a><span data-ttu-id="eb44b-156">uzunluğu</span><span class="sxs-lookup"><span data-stu-id="eb44b-156">length</span></span>
<span data-ttu-id="eb44b-157">Bir dize, değer dizideki veya nesnedeki anahtar sayısı karakterlerin sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-157">Returns the number of characters in a string, the number of values in an array, or the number of keys in an object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="eb44b-158">Örnek 1: dize</span><span class="sxs-lookup"><span data-stu-id="eb44b-158">Example 1: string</span></span>
<span data-ttu-id="eb44b-159">Aşağıdaki örnek verir `6`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-159">The following example returns `6`:</span></span>

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="eb44b-160">Örnek 2: dizi</span><span class="sxs-lookup"><span data-stu-id="eb44b-160">Example 2: array</span></span>
<span data-ttu-id="eb44b-161">Varsayın `element1` döndürür `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="eb44b-161">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="eb44b-162">Aşağıdaki örnek verir `3`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-162">The following example returns `3`:</span></span>

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="eb44b-163">Örnek 3: nesnesi</span><span class="sxs-lookup"><span data-stu-id="eb44b-163">Example 3: object</span></span>
<span data-ttu-id="eb44b-164">Varsayın `element1` döndürür:</span><span class="sxs-lookup"><span data-stu-id="eb44b-164">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="eb44b-165">Aşağıdaki örnek verir `2`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-165">The following example returns `2`:</span></span>

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a><span data-ttu-id="eb44b-166">boş</span><span class="sxs-lookup"><span data-stu-id="eb44b-166">empty</span></span>
<span data-ttu-id="eb44b-167">Döndürür `true` dize, dizi veya nesne null veya boş ise.</span><span class="sxs-lookup"><span data-stu-id="eb44b-167">Returns `true` if the string, array, or object is null or empty.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="eb44b-168">Örnek 1: dize</span><span class="sxs-lookup"><span data-stu-id="eb44b-168">Example 1: string</span></span>
<span data-ttu-id="eb44b-169">Aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-169">The following example returns `true`:</span></span>

```json
"[empty('')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="eb44b-170">Örnek 2: dizi</span><span class="sxs-lookup"><span data-stu-id="eb44b-170">Example 2: array</span></span>
<span data-ttu-id="eb44b-171">Varsayın `element1` döndürür `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="eb44b-171">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="eb44b-172">Aşağıdaki örnek verir `false`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-172">The following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="eb44b-173">Örnek 3: nesnesi</span><span class="sxs-lookup"><span data-stu-id="eb44b-173">Example 3: object</span></span>
<span data-ttu-id="eb44b-174">Varsayın `element1` döndürür:</span><span class="sxs-lookup"><span data-stu-id="eb44b-174">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="eb44b-175">Aşağıdaki örnek verir `false`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-175">The following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a><span data-ttu-id="eb44b-176">Örnek 4: boş ve tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="eb44b-176">Example 4: null and undefined</span></span>
<span data-ttu-id="eb44b-177">Varsayın `element1` olan `null` veya tanımlanmamış.</span><span class="sxs-lookup"><span data-stu-id="eb44b-177">Assume `element1` is `null` or undefined.</span></span> <span data-ttu-id="eb44b-178">Aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-178">The following example returns `true`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a><span data-ttu-id="eb44b-179">ilk</span><span class="sxs-lookup"><span data-stu-id="eb44b-179">first</span></span>
<span data-ttu-id="eb44b-180">Belirtilen dizenin ilk karakteri döndürür; Belirtilen dizinin ilk değerini; veya ilk anahtarı ve belirtilen nesnenin değeri.</span><span class="sxs-lookup"><span data-stu-id="eb44b-180">Returns the first character of the specified string; first value of the specified array; or the first key and value of the specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="eb44b-181">Örnek 1: dize</span><span class="sxs-lookup"><span data-stu-id="eb44b-181">Example 1: string</span></span>
<span data-ttu-id="eb44b-182">Aşağıdaki örnek verir `"f"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-182">The following example returns `"f"`:</span></span>

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="eb44b-183">Örnek 2: dizi</span><span class="sxs-lookup"><span data-stu-id="eb44b-183">Example 2: array</span></span>
<span data-ttu-id="eb44b-184">Varsayın `element1` döndürür `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="eb44b-184">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="eb44b-185">Aşağıdaki örnek verir `1`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-185">The following example returns `1`:</span></span>

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="eb44b-186">Örnek 3: nesnesi</span><span class="sxs-lookup"><span data-stu-id="eb44b-186">Example 3: object</span></span>
<span data-ttu-id="eb44b-187">Varsayın `element1` döndürür:</span><span class="sxs-lookup"><span data-stu-id="eb44b-187">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="eb44b-188">Aşağıdaki örnek verir `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-188">The following example returns `{"key1": "foobar"}`:</span></span>

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a><span data-ttu-id="eb44b-189">Son</span><span class="sxs-lookup"><span data-stu-id="eb44b-189">last</span></span>
<span data-ttu-id="eb44b-190">Belirtilen dize, son değerini belirtilen dizi veya son anahtarı ve belirtilen nesne değerini son karakteri döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-190">Returns the last character of the specified string, the last value of the specified array, or the last key and value of the specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="eb44b-191">Örnek 1: dize</span><span class="sxs-lookup"><span data-stu-id="eb44b-191">Example 1: string</span></span>
<span data-ttu-id="eb44b-192">Aşağıdaki örnek verir `"r"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-192">The following example returns `"r"`:</span></span>

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="eb44b-193">Örnek 2: dizi</span><span class="sxs-lookup"><span data-stu-id="eb44b-193">Example 2: array</span></span>
<span data-ttu-id="eb44b-194">Varsayın `element1` döndürür `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="eb44b-194">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="eb44b-195">Aşağıdaki örnek verir `2`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-195">The following example returns `2`:</span></span>

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="eb44b-196">Örnek 3: nesnesi</span><span class="sxs-lookup"><span data-stu-id="eb44b-196">Example 3: object</span></span>
<span data-ttu-id="eb44b-197">Varsayın `element1` döndürür:</span><span class="sxs-lookup"><span data-stu-id="eb44b-197">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="eb44b-198">Aşağıdaki örnek verir `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-198">The following example returns `{"key2": "raboof"}`:</span></span>

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a><span data-ttu-id="eb44b-199">Al</span><span class="sxs-lookup"><span data-stu-id="eb44b-199">take</span></span>
<span data-ttu-id="eb44b-200">Belirtilen sayıda ardışık karakteri dize başından, bitişik değerleri dizisi başından itibaren belirli sayıda veya belirtilen sayıda bitişik anahtarlar ve değerler nesne başından döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-200">Returns a specified number of contiguous characters from the start of the string, a specified number of contiguous values from the start of the array, or a specified number of contiguous keys and values from the start of the object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="eb44b-201">Örnek 1: dize</span><span class="sxs-lookup"><span data-stu-id="eb44b-201">Example 1: string</span></span>
<span data-ttu-id="eb44b-202">Aşağıdaki örnek verir `"foo"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-202">The following example returns `"foo"`:</span></span>

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="eb44b-203">Örnek 2: dizi</span><span class="sxs-lookup"><span data-stu-id="eb44b-203">Example 2: array</span></span>
<span data-ttu-id="eb44b-204">Varsayın `element1` döndürür `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="eb44b-204">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="eb44b-205">Aşağıdaki örnek verir `[1, 2]`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-205">The following example returns `[1, 2]`:</span></span>

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="eb44b-206">Örnek 3: nesnesi</span><span class="sxs-lookup"><span data-stu-id="eb44b-206">Example 3: object</span></span>
<span data-ttu-id="eb44b-207">Varsayın `element1` döndürür:</span><span class="sxs-lookup"><span data-stu-id="eb44b-207">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="eb44b-208">Aşağıdaki örnek verir `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-208">The following example returns `{"key1": "foobar"}`:</span></span>

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a><span data-ttu-id="eb44b-209">Atla</span><span class="sxs-lookup"><span data-stu-id="eb44b-209">skip</span></span>
<span data-ttu-id="eb44b-210">Belirtilen bir koleksiyondaki öğelerin sayısı atlar ve kalan öğeleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-210">Bypasses a specified number of elements in a collection, and then returns the remaining elements.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="eb44b-211">Örnek 1: dize</span><span class="sxs-lookup"><span data-stu-id="eb44b-211">Example 1: string</span></span>
<span data-ttu-id="eb44b-212">Aşağıdaki örnek verir `"bar"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-212">The following example returns `"bar"`:</span></span>

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="eb44b-213">Örnek 2: dizi</span><span class="sxs-lookup"><span data-stu-id="eb44b-213">Example 2: array</span></span>
<span data-ttu-id="eb44b-214">Varsayın `element1` döndürür `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="eb44b-214">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="eb44b-215">Aşağıdaki örnek verir `[3]`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-215">The following example returns `[3]`:</span></span>

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="eb44b-216">Örnek 3: nesnesi</span><span class="sxs-lookup"><span data-stu-id="eb44b-216">Example 3: object</span></span>
<span data-ttu-id="eb44b-217">Varsayın `element1` döndürür:</span><span class="sxs-lookup"><span data-stu-id="eb44b-217">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="eb44b-218">Aşağıdaki örnek verir `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-218">The following example returns `{"key2": "raboof"}`:</span></span>

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a><span data-ttu-id="eb44b-219">Mantıksal işlevleri</span><span class="sxs-lookup"><span data-stu-id="eb44b-219">Logical functions</span></span>
<span data-ttu-id="eb44b-220">Bu işlevler koşulları içinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="eb44b-220">These functions can be used in conditionals.</span></span> <span data-ttu-id="eb44b-221">Bazı işlevler tüm JSON veri türlerini desteklemiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="eb44b-221">Some functions may not support all JSON data types.</span></span>

### <a name="equals"></a><span data-ttu-id="eb44b-222">eşittir</span><span class="sxs-lookup"><span data-stu-id="eb44b-222">equals</span></span>
<span data-ttu-id="eb44b-223">Döndürür `true` parametrelerinin her ikisini de aynı türde ve değer varsa.</span><span class="sxs-lookup"><span data-stu-id="eb44b-223">Returns `true` if both parameters have the same type and value.</span></span> <span data-ttu-id="eb44b-224">Bu işlev tüm JSON veri türlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-224">This function supports all JSON data types.</span></span>

<span data-ttu-id="eb44b-225">Aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-225">The following example returns `true`:</span></span>

```json
"[equals(0, 0)]"
```

<span data-ttu-id="eb44b-226">Aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-226">The following example returns `true`:</span></span>

```json
"[equals('foo', 'foo')]"
```

<span data-ttu-id="eb44b-227">Aşağıdaki örnek verir `false`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-227">The following example returns `false`:</span></span>

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a><span data-ttu-id="eb44b-228">daha az</span><span class="sxs-lookup"><span data-stu-id="eb44b-228">less</span></span>
<span data-ttu-id="eb44b-229">Döndürür `true` ilk parametre ikinci parametre değerinden kesinlikle küçük ise.</span><span class="sxs-lookup"><span data-stu-id="eb44b-229">Returns `true` if the first parameter is strictly less than the second parameter.</span></span> <span data-ttu-id="eb44b-230">Bu işlev parametreleri yalnızca türü numarası ve dize destekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-230">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="eb44b-231">Aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-231">The following example returns `true`:</span></span>

```json
"[less(1, 2)]"
```

<span data-ttu-id="eb44b-232">Aşağıdaki örnek verir `false`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-232">The following example returns `false`:</span></span>

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a><span data-ttu-id="eb44b-233">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="eb44b-233">lessOrEquals</span></span>
<span data-ttu-id="eb44b-234">Döndürür `true` ilk parametre ikinci parametre küçük veya buna eşit olması durumunda.</span><span class="sxs-lookup"><span data-stu-id="eb44b-234">Returns `true` if the first parameter is less than or equal to the second parameter.</span></span> <span data-ttu-id="eb44b-235">Bu işlev parametreleri yalnızca türü numarası ve dize destekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-235">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="eb44b-236">Aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-236">The following example returns `true`:</span></span>

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a><span data-ttu-id="eb44b-237">büyük</span><span class="sxs-lookup"><span data-stu-id="eb44b-237">greater</span></span>
<span data-ttu-id="eb44b-238">Döndürür `true` ilk parametre ikinci parametre kesinlikle büyük ise.</span><span class="sxs-lookup"><span data-stu-id="eb44b-238">Returns `true` if the first parameter is strictly greater than the second parameter.</span></span> <span data-ttu-id="eb44b-239">Bu işlev parametreleri yalnızca türü numarası ve dize destekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-239">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="eb44b-240">Aşağıdaki örnek verir `false`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-240">The following example returns `false`:</span></span>

```json
"[greater(1, 2)]"
```

<span data-ttu-id="eb44b-241">Aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-241">The following example returns `true`:</span></span>

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a><span data-ttu-id="eb44b-242">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="eb44b-242">greaterOrEquals</span></span>
<span data-ttu-id="eb44b-243">Döndürür `true` ilk parametre ikinci parametre eşit veya daha büyük olduğunda.</span><span class="sxs-lookup"><span data-stu-id="eb44b-243">Returns `true` if the first parameter is greater than or equal to the second parameter.</span></span> <span data-ttu-id="eb44b-244">Bu işlev parametreleri yalnızca türü numarası ve dize destekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-244">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="eb44b-245">Aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-245">The following example returns `true`:</span></span>

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a><span data-ttu-id="eb44b-246">ve</span><span class="sxs-lookup"><span data-stu-id="eb44b-246">and</span></span>
<span data-ttu-id="eb44b-247">Döndürür `true` için tüm parametreleri değerlendirin varsa `true`.</span><span class="sxs-lookup"><span data-stu-id="eb44b-247">Returns `true` if all the parameters evaluate to `true`.</span></span> <span data-ttu-id="eb44b-248">Bu işlev yalnızca Boole türünde iki veya daha fazla parametre destekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-248">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="eb44b-249">Aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-249">The following example returns `true`:</span></span>

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="eb44b-250">Aşağıdaki örnek verir `false`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-250">The following example returns `false`:</span></span>

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a><span data-ttu-id="eb44b-251">or</span><span class="sxs-lookup"><span data-stu-id="eb44b-251">or</span></span>
<span data-ttu-id="eb44b-252">Döndürür `true` parametrelerin en az biri değerlendirilirse `true`.</span><span class="sxs-lookup"><span data-stu-id="eb44b-252">Returns `true` if at least one of the parameters evaluates to `true`.</span></span> <span data-ttu-id="eb44b-253">Bu işlev yalnızca Boole türünde iki veya daha fazla parametre destekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-253">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="eb44b-254">Aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-254">The following example returns `true`:</span></span>

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="eb44b-255">Aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-255">The following example returns `true`:</span></span>

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a><span data-ttu-id="eb44b-256">değil</span><span class="sxs-lookup"><span data-stu-id="eb44b-256">not</span></span>
<span data-ttu-id="eb44b-257">Döndürür `true` parametresi değerlendirilirse `false`.</span><span class="sxs-lookup"><span data-stu-id="eb44b-257">Returns `true` if the parameter evaluates to `false`.</span></span> <span data-ttu-id="eb44b-258">Bu işlev yalnızca Boole türünde parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-258">This function supports parameters only of type Boolean.</span></span>

<span data-ttu-id="eb44b-259">Aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-259">The following example returns `true`:</span></span>

```json
"[not(false)]"
```

<span data-ttu-id="eb44b-260">Aşağıdaki örnek verir `false`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-260">The following example returns `false`:</span></span>

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a><span data-ttu-id="eb44b-261">birleşim</span><span class="sxs-lookup"><span data-stu-id="eb44b-261">coalesce</span></span>
<span data-ttu-id="eb44b-262">İlk null olmayan parametresinin değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-262">Returns the value of the first non-null parameter.</span></span> <span data-ttu-id="eb44b-263">Bu işlev tüm JSON veri türlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-263">This function supports all JSON data types.</span></span>

<span data-ttu-id="eb44b-264">Varsayın `element1` ve `element2` tanımlanmaz.</span><span class="sxs-lookup"><span data-stu-id="eb44b-264">Assume `element1` and `element2` are undefined.</span></span> <span data-ttu-id="eb44b-265">Aşağıdaki örnek verir `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-265">The following example returns `"foobar"`:</span></span>

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a><span data-ttu-id="eb44b-266">Dönüşüm işlevleri</span><span class="sxs-lookup"><span data-stu-id="eb44b-266">Conversion functions</span></span>
<span data-ttu-id="eb44b-267">Bu işlevler, JSON veri türleri ve Kodlamalar arasında değerleri dönüştürmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="eb44b-267">These functions can be used to convert values between JSON data types and encodings.</span></span>

### <a name="int"></a><span data-ttu-id="eb44b-268">Int</span><span class="sxs-lookup"><span data-stu-id="eb44b-268">int</span></span>
<span data-ttu-id="eb44b-269">Parametresi, bir tamsayıya dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-269">Converts the parameter to an integer.</span></span> <span data-ttu-id="eb44b-270">Bu işlev türü numarası ve dize parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-270">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="eb44b-271">Aşağıdaki örnek verir `1`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-271">The following example returns `1`:</span></span>

```json
"[int('1')]"
```

<span data-ttu-id="eb44b-272">Aşağıdaki örnek verir `2`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-272">The following example returns `2`:</span></span>

```json
"[int(2.9)]"
```

### <a name="float"></a><span data-ttu-id="eb44b-273">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="eb44b-273">float</span></span>
<span data-ttu-id="eb44b-274">Parametresi için bir kayan nokta dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-274">Converts the parameter to a floating-point.</span></span> <span data-ttu-id="eb44b-275">Bu işlev türü numarası ve dize parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-275">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="eb44b-276">Aşağıdaki örnek verir `1.0`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-276">The following example returns `1.0`:</span></span>

```json
"[float('1.0')]"
```

<span data-ttu-id="eb44b-277">Aşağıdaki örnek verir `2.9`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-277">The following example returns `2.9`:</span></span>

```json
"[float(2.9)]"
```

### <a name="string"></a><span data-ttu-id="eb44b-278">Dize</span><span class="sxs-lookup"><span data-stu-id="eb44b-278">string</span></span>
<span data-ttu-id="eb44b-279">Parametresi bir dizeye dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-279">Converts the parameter to a string.</span></span> <span data-ttu-id="eb44b-280">Bu işlev parametreleri tüm JSON veri türlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-280">This function supports parameters of all JSON data types.</span></span>

<span data-ttu-id="eb44b-281">Aşağıdaki örnek verir `"1"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-281">The following example returns `"1"`:</span></span>

```json
"[string(1)]"
```

<span data-ttu-id="eb44b-282">Aşağıdaki örnek verir `"2.9"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-282">The following example returns `"2.9"`:</span></span>

```json
"[string(2.9)]"
```

<span data-ttu-id="eb44b-283">Aşağıdaki örnek verir `"[1,2,3]"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-283">The following example returns `"[1,2,3]"`:</span></span>

```json
"[string([1,2,3])]"
```

<span data-ttu-id="eb44b-284">Aşağıdaki örnek verir `"{"foo":"bar"}"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-284">The following example returns `"{"foo":"bar"}"`:</span></span>

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a><span data-ttu-id="eb44b-285">bool</span><span class="sxs-lookup"><span data-stu-id="eb44b-285">bool</span></span>
<span data-ttu-id="eb44b-286">Parametresi bir Boolean değerine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-286">Converts the parameter to a Boolean.</span></span> <span data-ttu-id="eb44b-287">Bu işlev türü numarası, dize ve Boolean parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-287">This function supports parameters of type number, string, and Boolean.</span></span> <span data-ttu-id="eb44b-288">Boole değerlerini JavaScript'te benzeyen, herhangi bir değer dışında `0` veya `'false'` döndürür `true`.</span><span class="sxs-lookup"><span data-stu-id="eb44b-288">Similar to Booleans in JavaScript, any value except `0` or `'false'` returns `true`.</span></span>

<span data-ttu-id="eb44b-289">Aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-289">The following example returns `true`:</span></span>

```json
"[bool(1)]"
```

<span data-ttu-id="eb44b-290">Aşağıdaki örnek verir `false`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-290">The following example returns `false`:</span></span>

```json
"[bool(0)]"
```

<span data-ttu-id="eb44b-291">Aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-291">The following example returns `true`:</span></span>

```json
"[bool(true)]"
```

<span data-ttu-id="eb44b-292">Aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-292">The following example returns `true`:</span></span>

```json
"[bool('true')]"
```

### <a name="parse"></a><span data-ttu-id="eb44b-293">Ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="eb44b-293">parse</span></span>
<span data-ttu-id="eb44b-294">Parametresi, yerel bir türe dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-294">Converts the parameter to a native type.</span></span> <span data-ttu-id="eb44b-295">Diğer bir deyişle, bu işlev, tersidir `string()`.</span><span class="sxs-lookup"><span data-stu-id="eb44b-295">In other words, this function is the inverse of `string()`.</span></span> <span data-ttu-id="eb44b-296">Bu işlev yalnızca dize türünde parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-296">This function supports parameters only of type string.</span></span>

<span data-ttu-id="eb44b-297">Aşağıdaki örnek verir `1`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-297">The following example returns `1`:</span></span>

```json
"[parse('1')]"
```

<span data-ttu-id="eb44b-298">Aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-298">The following example returns `true`:</span></span>

```json
"[parse('true')]"
```

<span data-ttu-id="eb44b-299">Aşağıdaki örnek verir `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-299">The following example returns `[1,2,3]`:</span></span>

```json
"[parse('[1,2,3]')]"
```

<span data-ttu-id="eb44b-300">Aşağıdaki örnek verir `{"foo":"bar"}`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-300">The following example returns `{"foo":"bar"}`:</span></span>

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a><span data-ttu-id="eb44b-301">encodeBase64</span><span class="sxs-lookup"><span data-stu-id="eb44b-301">encodeBase64</span></span>
<span data-ttu-id="eb44b-302">Base-64 kodlu bir dize parametresi kodlar.</span><span class="sxs-lookup"><span data-stu-id="eb44b-302">Encodes the parameter to a base-64 encoded string.</span></span> <span data-ttu-id="eb44b-303">Bu işlev yalnızca dize türünde parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-303">This function supports parameters only of type string.</span></span>

<span data-ttu-id="eb44b-304">Aşağıdaki örnek verir `"Zm9vYmFy"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-304">The following example returns `"Zm9vYmFy"`:</span></span>

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a><span data-ttu-id="eb44b-305">decodeBase64</span><span class="sxs-lookup"><span data-stu-id="eb44b-305">decodeBase64</span></span>
<span data-ttu-id="eb44b-306">Base-64 kodlu bir dize parametresinden kodunu çözer.</span><span class="sxs-lookup"><span data-stu-id="eb44b-306">Decodes the parameter from a base-64 encoded string.</span></span> <span data-ttu-id="eb44b-307">Bu işlev yalnızca dize türünde parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-307">This function supports parameters only of type string.</span></span>

<span data-ttu-id="eb44b-308">Aşağıdaki örnek verir `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-308">The following example returns `"foobar"`:</span></span>

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a><span data-ttu-id="eb44b-309">Encodeurıcomponent</span><span class="sxs-lookup"><span data-stu-id="eb44b-309">encodeUriComponent</span></span>
<span data-ttu-id="eb44b-310">Kodlanan URL dizesi parametresi olarak kodlar.</span><span class="sxs-lookup"><span data-stu-id="eb44b-310">Encodes the parameter to a URL encoded string.</span></span> <span data-ttu-id="eb44b-311">Bu işlev yalnızca dize türünde parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-311">This function supports parameters only of type string.</span></span>

<span data-ttu-id="eb44b-312">Aşağıdaki örnek verir `"https%3A%2F%2Fportal.azure.com%2F"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-312">The following example returns `"https%3A%2F%2Fportal.azure.com%2F"`:</span></span>

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a><span data-ttu-id="eb44b-313">Decodeurıcomponent</span><span class="sxs-lookup"><span data-stu-id="eb44b-313">decodeUriComponent</span></span>
<span data-ttu-id="eb44b-314">Bir URL kodlanmış dize parametresinden kodunu çözer.</span><span class="sxs-lookup"><span data-stu-id="eb44b-314">Decodes the parameter from a URL encoded string.</span></span> <span data-ttu-id="eb44b-315">Bu işlev yalnızca dize türünde parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-315">This function supports parameters only of type string.</span></span>

<span data-ttu-id="eb44b-316">Aşağıdaki örnek verir `"https://portal.azure.com/"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-316">The following example returns `"https://portal.azure.com/"`:</span></span>

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a><span data-ttu-id="eb44b-317">Matematik işlevleri</span><span class="sxs-lookup"><span data-stu-id="eb44b-317">Math functions</span></span>
### <a name="add"></a><span data-ttu-id="eb44b-318">Ekleme</span><span class="sxs-lookup"><span data-stu-id="eb44b-318">add</span></span>
<span data-ttu-id="eb44b-319">İki sayı ekleyen ve sonuç döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-319">Adds two numbers, and returns the result.</span></span>

<span data-ttu-id="eb44b-320">Aşağıdaki örnek verir `3`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-320">The following example returns `3`:</span></span>

```json
"[add(1, 2)]"
```

### <a name="sub"></a><span data-ttu-id="eb44b-321">Sub</span><span class="sxs-lookup"><span data-stu-id="eb44b-321">sub</span></span>
<span data-ttu-id="eb44b-322">İkinci sayı ilk sayıdan çıkarır ve sonucu döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-322">Subtracts the second number from the first number, and returns the result.</span></span>

<span data-ttu-id="eb44b-323">Aşağıdaki örnek verir `1`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-323">The following example returns `1`:</span></span>

```json
"[sub(3, 2)]"
```

### <a name="mul"></a><span data-ttu-id="eb44b-324">mul</span><span class="sxs-lookup"><span data-stu-id="eb44b-324">mul</span></span>
<span data-ttu-id="eb44b-325">İki sayıyı çarpar ve sonucu döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-325">Multiplies two numbers, and returns the result.</span></span>

<span data-ttu-id="eb44b-326">Aşağıdaki örnek verir `6`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-326">The following example returns `6`:</span></span>

```json
"[mul(2, 3)]"
```

### <a name="div"></a><span data-ttu-id="eb44b-327">div</span><span class="sxs-lookup"><span data-stu-id="eb44b-327">div</span></span>
<span data-ttu-id="eb44b-328">İkinci sayı ilk sayıyı böler ve sonucu döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-328">Divides the first number by the second number, and returns the result.</span></span> <span data-ttu-id="eb44b-329">Sonuç her zaman bir tamsayıdır.</span><span class="sxs-lookup"><span data-stu-id="eb44b-329">The result is always an integer.</span></span>

<span data-ttu-id="eb44b-330">Aşağıdaki örnek verir `2`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-330">The following example returns `2`:</span></span>

```json
"[div(6, 3)]"
```

### <a name="mod"></a><span data-ttu-id="eb44b-331">mod</span><span class="sxs-lookup"><span data-stu-id="eb44b-331">mod</span></span>
<span data-ttu-id="eb44b-332">İkinci sayı ilk sayıyı böler ve kalanı döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-332">Divides the first number by the second number, and returns the remainder.</span></span>

<span data-ttu-id="eb44b-333">Aşağıdaki örnek verir `0`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-333">The following example returns `0`:</span></span>

```json
"[mod(6, 3)]"
```

<span data-ttu-id="eb44b-334">Aşağıdaki örnek verir `2`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-334">The following example returns `2`:</span></span>

```json
"[mod(6, 4)]"
```

### <a name="min"></a><span data-ttu-id="eb44b-335">dk</span><span class="sxs-lookup"><span data-stu-id="eb44b-335">min</span></span>
<span data-ttu-id="eb44b-336">İki sayının küçük döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-336">Returns the small of the two numbers.</span></span>

<span data-ttu-id="eb44b-337">Aşağıdaki örnek verir `1`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-337">The following example returns `1`:</span></span>

```json
"[min(1, 2)]"
```

### <a name="max"></a><span data-ttu-id="eb44b-338">max</span><span class="sxs-lookup"><span data-stu-id="eb44b-338">max</span></span>
<span data-ttu-id="eb44b-339">Büyük iki sayının döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-339">Returns the larger of the two numbers.</span></span>

<span data-ttu-id="eb44b-340">Aşağıdaki örnek verir `2`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-340">The following example returns `2`:</span></span>

```json
"[max(1, 2)]"
```

### <a name="range"></a><span data-ttu-id="eb44b-341">Aralık</span><span class="sxs-lookup"><span data-stu-id="eb44b-341">range</span></span>
<span data-ttu-id="eb44b-342">Belirtilen aralıkta tam sayı sayılardan oluşan bir dizi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eb44b-342">Generates a sequence of integral numbers within the specified range.</span></span>

<span data-ttu-id="eb44b-343">Aşağıdaki örnek verir `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-343">The following example returns `[1,2,3]`:</span></span>

```json
"[range(1, 3)]"
```

### <a name="rand"></a><span data-ttu-id="eb44b-344">rand</span><span class="sxs-lookup"><span data-stu-id="eb44b-344">rand</span></span>
<span data-ttu-id="eb44b-345">Belirtilen aralık içinde rastgele bir tamsayı döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-345">Returns a random integral number within the specified range.</span></span> <span data-ttu-id="eb44b-346">Bu işlev, şifreleme açısından güvenli rastgele sayılar oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="eb44b-346">This function does not generate cryptographically secure random numbers.</span></span>

<span data-ttu-id="eb44b-347">Aşağıdaki örnek döndürebilir `42`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-347">The following example could return `42`:</span></span>

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a><span data-ttu-id="eb44b-348">Kat</span><span class="sxs-lookup"><span data-stu-id="eb44b-348">floor</span></span>
<span data-ttu-id="eb44b-349">Belirtilen sayıdan küçük veya eşit en büyük tamsayıyı döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-349">Returns the largest integer less than or equal to the specified number.</span></span>

<span data-ttu-id="eb44b-350">Aşağıdaki örnek verir `3`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-350">The following example returns `3`:</span></span>

```json
"[floor(3.14)]"
```

### <a name="ceil"></a><span data-ttu-id="eb44b-351">ceil</span><span class="sxs-lookup"><span data-stu-id="eb44b-351">ceil</span></span>
<span data-ttu-id="eb44b-352">Büyük veya eşit belirtilen en büyük tamsayıyı döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-352">Returns the largest integer greater than or equal to the specified number.</span></span>

<span data-ttu-id="eb44b-353">Aşağıdaki örnek verir `4`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-353">The following example returns `4`:</span></span>

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a><span data-ttu-id="eb44b-354">Date işlevleri</span><span class="sxs-lookup"><span data-stu-id="eb44b-354">Date functions</span></span>
### <a name="utcnow"></a><span data-ttu-id="eb44b-355">utcNow</span><span class="sxs-lookup"><span data-stu-id="eb44b-355">utcNow</span></span>
<span data-ttu-id="eb44b-356">Bir dize, yerel bilgisayardaki geçerli tarih ve saati ISO 8601 biçiminde döndürür.</span><span class="sxs-lookup"><span data-stu-id="eb44b-356">Returns a string in ISO 8601 format of the current date and time on the local computer.</span></span>

<span data-ttu-id="eb44b-357">Aşağıdaki örnek döndürebilir `"1990-12-31T23:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-357">The following example could return `"1990-12-31T23:59:59.000Z"`:</span></span>

```json
"[utcNow()]"
```

### <a name="addseconds"></a><span data-ttu-id="eb44b-358">saniyeEkle</span><span class="sxs-lookup"><span data-stu-id="eb44b-358">addSeconds</span></span>
<span data-ttu-id="eb44b-359">Bir tam sayı saniye sayısı için belirtilen zaman damgası ekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-359">Adds an integral number of seconds to the specified timestamp.</span></span>

<span data-ttu-id="eb44b-360">Aşağıdaki örnek verir `"1991-01-01T00:00:00.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-360">The following example returns `"1991-01-01T00:00:00.000Z"`:</span></span>

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a><span data-ttu-id="eb44b-361">addMinutes</span><span class="sxs-lookup"><span data-stu-id="eb44b-361">addMinutes</span></span>
<span data-ttu-id="eb44b-362">Bir tam sayı dakika sayısı için belirtilen zaman damgası ekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-362">Adds an integral number of minutes to the specified timestamp.</span></span>

<span data-ttu-id="eb44b-363">Aşağıdaki örnek verir `"1991-01-01T00:00:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-363">The following example returns `"1991-01-01T00:00:59.000Z"`:</span></span>

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a><span data-ttu-id="eb44b-364">addHours</span><span class="sxs-lookup"><span data-stu-id="eb44b-364">addHours</span></span>
<span data-ttu-id="eb44b-365">Bir tamsayı saat için belirtilen zaman damgası ekler.</span><span class="sxs-lookup"><span data-stu-id="eb44b-365">Adds an integral number of hours to the specified timestamp.</span></span>

<span data-ttu-id="eb44b-366">Aşağıdaki örnek verir `"1991-01-01T00:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="eb44b-366">The following example returns `"1991-01-01T00:59:59.000Z"`:</span></span>

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a><span data-ttu-id="eb44b-367">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eb44b-367">Next steps</span></span>
* <span data-ttu-id="eb44b-368">Bir bir giriş için Azure Resource Manager'ı için bkz: [Azure Resource Manager'a genel bakış](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eb44b-368">For an introduction to Azure Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

