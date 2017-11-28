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
# <a name="createuidefinition-functions"></a><span data-ttu-id="f83b1-103">CreateUiDefinition işlevleri</span><span class="sxs-lookup"><span data-stu-id="f83b1-103">CreateUiDefinition functions</span></span>
<span data-ttu-id="f83b1-104">Bu bölüm bir CreateUiDefinition tüm desteklenen işlevlerini hello imzaları içerir.</span><span class="sxs-lookup"><span data-stu-id="f83b1-104">This section contains hello signatures for all supported functions of a CreateUiDefinition.</span></span>

<span data-ttu-id="f83b1-105">toouse bir işlevi köşeli surround hello bildirimiyle.</span><span class="sxs-lookup"><span data-stu-id="f83b1-105">toouse a function, surround hello declaration with square brackets.</span></span> <span data-ttu-id="f83b1-106">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f83b1-106">For example:</span></span>

```json
"[function()]"
```

<span data-ttu-id="f83b1-107">Dizeler ve diğer işlevleri işlevi için parametre olarak başvurulabilir, ancak dizeler tek tırnak içine alınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f83b1-107">Strings and other functions can be referenced as parameters for a function, but strings must be surrounded in single quotes.</span></span> <span data-ttu-id="f83b1-108">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f83b1-108">For example:</span></span>

```json
"[fn1(fn2(), 'foobar')]"
```

<span data-ttu-id="f83b1-109">Uygunsa, hello nokta işlecini kullanarak bir işlevin hello çıktı özelliklerini başvuruda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="f83b1-109">Where applicable, you can reference properties of hello output of a function by using hello dot operator.</span></span> <span data-ttu-id="f83b1-110">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f83b1-110">For example:</span></span>

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a><span data-ttu-id="f83b1-111">İşlevler başvurma</span><span class="sxs-lookup"><span data-stu-id="f83b1-111">Referencing functions</span></span>
<span data-ttu-id="f83b1-112">Bu işlevler hello özellikleri ya da bir CreateUiDefinition bağlamında kullanılan tooreference çıkışları olabilir.</span><span class="sxs-lookup"><span data-stu-id="f83b1-112">These functions can be used tooreference outputs from hello properties or context of a CreateUiDefinition.</span></span>

### <a name="basics"></a><span data-ttu-id="f83b1-113">temel kavramları</span><span class="sxs-lookup"><span data-stu-id="f83b1-113">basics</span></span>
<span data-ttu-id="f83b1-114">Hello çıktı hello temelleri adımında tanımlı bir öğe değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="f83b1-114">Returns hello output values of an element that is defined in hello Basics step.</span></span>

<span data-ttu-id="f83b1-115">Merhaba aşağıdaki örnek verir adlı hello öğe hello çıktısını `foo` hello temelleri adımda:</span><span class="sxs-lookup"><span data-stu-id="f83b1-115">hello following example returns hello output of hello element named `foo` in hello Basics step:</span></span>

```json
"[basics('foo')]"
```

### <a name="steps"></a><span data-ttu-id="f83b1-116">Adımları</span><span class="sxs-lookup"><span data-stu-id="f83b1-116">steps</span></span>
<span data-ttu-id="f83b1-117">Merhaba çıktı hello belirtilen adımında tanımlı bir öğe değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="f83b1-117">Returns hello output values of an element that is defined in hello specified step.</span></span> <span data-ttu-id="f83b1-118">Merhaba temelleri adımda öğelerin tooget hello çıkış değerleri kullanmak `basics()` yerine.</span><span class="sxs-lookup"><span data-stu-id="f83b1-118">tooget hello output values of elements in hello Basics step, use `basics()` instead.</span></span>

<span data-ttu-id="f83b1-119">Merhaba aşağıdaki örnek verir adlı hello öğe hello çıktısını `bar` adlı hello adımda `foo`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-119">hello following example returns hello output of hello element named `bar` in hello step named `foo`:</span></span>

```json
"[steps('foo').bar]"
```

### <a name="location"></a><span data-ttu-id="f83b1-120">location</span><span class="sxs-lookup"><span data-stu-id="f83b1-120">location</span></span>
<span data-ttu-id="f83b1-121">Merhaba temel adımı veya hello geçerli bağlam seçilen hello konumu döndürür.</span><span class="sxs-lookup"><span data-stu-id="f83b1-121">Returns hello location selected in hello Basics step or hello current context.</span></span>

<span data-ttu-id="f83b1-122">Merhaba aşağıdaki örnek döndürebilir `"westus"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-122">hello following example could return `"westus"`:</span></span>

```json
"[location()]"
```

## <a name="string-functions"></a><span data-ttu-id="f83b1-123">Dize işlevleri</span><span class="sxs-lookup"><span data-stu-id="f83b1-123">String functions</span></span>
<span data-ttu-id="f83b1-124">Bu işlevler yalnızca JSON dizelerle kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f83b1-124">These functions can only be used with JSON strings.</span></span>

### <a name="concat"></a><span data-ttu-id="f83b1-125">concat</span><span class="sxs-lookup"><span data-stu-id="f83b1-125">concat</span></span>
<span data-ttu-id="f83b1-126">Bir veya daha fazla art arda ekler.</span><span class="sxs-lookup"><span data-stu-id="f83b1-126">Concatenates one or more strings.</span></span>

<span data-ttu-id="f83b1-127">Örneğin değeri hello çıktı, `element1` varsa `"bar"`, bu örnek hello dizesini döndürür sonra `"foobar!"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-127">For example, if hello output value of `element1` if `"bar"`, then this example returns hello string `"foobar!"`:</span></span>

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a><span data-ttu-id="f83b1-128">substring</span><span class="sxs-lookup"><span data-stu-id="f83b1-128">substring</span></span>
<span data-ttu-id="f83b1-129">Belirtilen dize hello hello dizenin döndürür.</span><span class="sxs-lookup"><span data-stu-id="f83b1-129">Returns hello substring of hello specified string.</span></span> <span data-ttu-id="f83b1-130">Merhaba substring hello belirtilen dizinden başlatır ve hello uzunluğu belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="f83b1-130">hello substring starts at hello specified index and has hello specified length.</span></span>

<span data-ttu-id="f83b1-131">Merhaba aşağıdaki örnek verir `"ftw"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-131">hello following example returns `"ftw"`:</span></span>

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a><span data-ttu-id="f83b1-132">Değiştir</span><span class="sxs-lookup"><span data-stu-id="f83b1-132">replace</span></span>
<span data-ttu-id="f83b1-133">Merhaba hangi tüm oluşumlarını dizesinde dize hello geçerli dizesinde belirtilen döndürür başka dize ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="f83b1-133">Returns a string in which all occurrences of hello specified string in hello current string are replaced with another string.</span></span>

<span data-ttu-id="f83b1-134">Merhaba aşağıdaki örnek verir `"Everything is awesome!"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-134">hello following example returns `"Everything is awesome!"`:</span></span>

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a><span data-ttu-id="f83b1-135">GUID</span><span class="sxs-lookup"><span data-stu-id="f83b1-135">guid</span></span>
<span data-ttu-id="f83b1-136">Genel olarak benzersiz bir dize (GUID) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f83b1-136">Generates a globally unique string (GUID).</span></span>

<span data-ttu-id="f83b1-137">Merhaba aşağıdaki örnek döndürebilir `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-137">hello following example could return `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span></span>

```json
"[guid()]"
```

### <a name="tolower"></a><span data-ttu-id="f83b1-138">toLower</span><span class="sxs-lookup"><span data-stu-id="f83b1-138">toLower</span></span>
<span data-ttu-id="f83b1-139">Dönüştürülmüş dizeyi toolowercase döndürür.</span><span class="sxs-lookup"><span data-stu-id="f83b1-139">Returns a string converted toolowercase.</span></span>

<span data-ttu-id="f83b1-140">Merhaba aşağıdaki örnek verir `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-140">hello following example returns `"foobar"`:</span></span>

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a><span data-ttu-id="f83b1-141">toUpper</span><span class="sxs-lookup"><span data-stu-id="f83b1-141">toUpper</span></span>
<span data-ttu-id="f83b1-142">Dönüştürülmüş dizeyi toouppercase döndürür.</span><span class="sxs-lookup"><span data-stu-id="f83b1-142">Returns a string converted toouppercase.</span></span>

<span data-ttu-id="f83b1-143">Merhaba aşağıdaki örnek verir `"FOOBAR"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-143">hello following example returns `"FOOBAR"`:</span></span>

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a><span data-ttu-id="f83b1-144">Toplama işlevleri</span><span class="sxs-lookup"><span data-stu-id="f83b1-144">Collection functions</span></span>
<span data-ttu-id="f83b1-145">Bu işlevler, JSON dizeler, dizileri ve nesneleri gibi koleksiyonlar ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f83b1-145">These functions can be used with collections, like JSON strings, arrays and objects.</span></span>

### <a name="contains"></a><span data-ttu-id="f83b1-146">içerir</span><span class="sxs-lookup"><span data-stu-id="f83b1-146">contains</span></span>
<span data-ttu-id="f83b1-147">Döndürür `true` bir dize içeriyorsa, belirtilen alt dizeyi Merhaba, bir dizi içeriyor hello belirtilen değer ya da hello belirtilen anahtar bir nesne içerir.</span><span class="sxs-lookup"><span data-stu-id="f83b1-147">Returns `true` if a string contains hello specified substring, an array contains hello specified value, or an object contains hello specified key.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="f83b1-148">Örnek 1: dize</span><span class="sxs-lookup"><span data-stu-id="f83b1-148">Example 1: string</span></span>
<span data-ttu-id="f83b1-149">Merhaba aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-149">hello following example returns `true`:</span></span>

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="f83b1-150">Örnek 2: dizi</span><span class="sxs-lookup"><span data-stu-id="f83b1-150">Example 2: array</span></span>
<span data-ttu-id="f83b1-151">Varsayın `element1` döndürür `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="f83b1-151">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="f83b1-152">Merhaba aşağıdaki örnek verir `false`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-152">hello following example returns `false`:</span></span>

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="f83b1-153">Örnek 3: nesnesi</span><span class="sxs-lookup"><span data-stu-id="f83b1-153">Example 3: object</span></span>
<span data-ttu-id="f83b1-154">Varsayın `element1` döndürür:</span><span class="sxs-lookup"><span data-stu-id="f83b1-154">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="f83b1-155">Merhaba aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-155">hello following example returns `true`:</span></span>

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a><span data-ttu-id="f83b1-156">uzunluğu</span><span class="sxs-lookup"><span data-stu-id="f83b1-156">length</span></span>
<span data-ttu-id="f83b1-157">Dize, bir dizideki hello sayısını veya bir nesne anahtarlarında hello sayısı Hello karakterlerin sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="f83b1-157">Returns hello number of characters in a string, hello number of values in an array, or hello number of keys in an object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="f83b1-158">Örnek 1: dize</span><span class="sxs-lookup"><span data-stu-id="f83b1-158">Example 1: string</span></span>
<span data-ttu-id="f83b1-159">Merhaba aşağıdaki örnek verir `6`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-159">hello following example returns `6`:</span></span>

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="f83b1-160">Örnek 2: dizi</span><span class="sxs-lookup"><span data-stu-id="f83b1-160">Example 2: array</span></span>
<span data-ttu-id="f83b1-161">Varsayın `element1` döndürür `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="f83b1-161">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="f83b1-162">Merhaba aşağıdaki örnek verir `3`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-162">hello following example returns `3`:</span></span>

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="f83b1-163">Örnek 3: nesnesi</span><span class="sxs-lookup"><span data-stu-id="f83b1-163">Example 3: object</span></span>
<span data-ttu-id="f83b1-164">Varsayın `element1` döndürür:</span><span class="sxs-lookup"><span data-stu-id="f83b1-164">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="f83b1-165">Merhaba aşağıdaki örnek verir `2`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-165">hello following example returns `2`:</span></span>

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a><span data-ttu-id="f83b1-166">boş</span><span class="sxs-lookup"><span data-stu-id="f83b1-166">empty</span></span>
<span data-ttu-id="f83b1-167">Döndürür `true` hello dize, dizi veya nesne null veya boş ise.</span><span class="sxs-lookup"><span data-stu-id="f83b1-167">Returns `true` if hello string, array, or object is null or empty.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="f83b1-168">Örnek 1: dize</span><span class="sxs-lookup"><span data-stu-id="f83b1-168">Example 1: string</span></span>
<span data-ttu-id="f83b1-169">Merhaba aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-169">hello following example returns `true`:</span></span>

```json
"[empty('')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="f83b1-170">Örnek 2: dizi</span><span class="sxs-lookup"><span data-stu-id="f83b1-170">Example 2: array</span></span>
<span data-ttu-id="f83b1-171">Varsayın `element1` döndürür `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="f83b1-171">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="f83b1-172">Merhaba aşağıdaki örnek verir `false`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-172">hello following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="f83b1-173">Örnek 3: nesnesi</span><span class="sxs-lookup"><span data-stu-id="f83b1-173">Example 3: object</span></span>
<span data-ttu-id="f83b1-174">Varsayın `element1` döndürür:</span><span class="sxs-lookup"><span data-stu-id="f83b1-174">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="f83b1-175">Merhaba aşağıdaki örnek verir `false`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-175">hello following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a><span data-ttu-id="f83b1-176">Örnek 4: boş ve tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="f83b1-176">Example 4: null and undefined</span></span>
<span data-ttu-id="f83b1-177">Varsayın `element1` olan `null` veya tanımlanmamış.</span><span class="sxs-lookup"><span data-stu-id="f83b1-177">Assume `element1` is `null` or undefined.</span></span> <span data-ttu-id="f83b1-178">Merhaba aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-178">hello following example returns `true`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a><span data-ttu-id="f83b1-179">ilk</span><span class="sxs-lookup"><span data-stu-id="f83b1-179">first</span></span>
<span data-ttu-id="f83b1-180">Belirtilen bir dize döndürür hello ilk karakteri hello; Merhaba belirtilen dizinin ilk değerini; veya ilk anahtar ve değer hello belirtilen nesnenin hello.</span><span class="sxs-lookup"><span data-stu-id="f83b1-180">Returns hello first character of hello specified string; first value of hello specified array; or hello first key and value of hello specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="f83b1-181">Örnek 1: dize</span><span class="sxs-lookup"><span data-stu-id="f83b1-181">Example 1: string</span></span>
<span data-ttu-id="f83b1-182">Merhaba aşağıdaki örnek verir `"f"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-182">hello following example returns `"f"`:</span></span>

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="f83b1-183">Örnek 2: dizi</span><span class="sxs-lookup"><span data-stu-id="f83b1-183">Example 2: array</span></span>
<span data-ttu-id="f83b1-184">Varsayın `element1` döndürür `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="f83b1-184">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="f83b1-185">Merhaba aşağıdaki örnek verir `1`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-185">hello following example returns `1`:</span></span>

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="f83b1-186">Örnek 3: nesnesi</span><span class="sxs-lookup"><span data-stu-id="f83b1-186">Example 3: object</span></span>
<span data-ttu-id="f83b1-187">Varsayın `element1` döndürür:</span><span class="sxs-lookup"><span data-stu-id="f83b1-187">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="f83b1-188">Merhaba aşağıdaki örnek verir `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-188">hello following example returns `{"key1": "foobar"}`:</span></span>

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a><span data-ttu-id="f83b1-189">Son</span><span class="sxs-lookup"><span data-stu-id="f83b1-189">last</span></span>
<span data-ttu-id="f83b1-190">Döndürür hello son karakteri belirtilen Merhaba, dize hello son değeri hello belirtilen dizinin veya son anahtar ve değer hello belirtilen nesnenin hello.</span><span class="sxs-lookup"><span data-stu-id="f83b1-190">Returns hello last character of hello specified string, hello last value of hello specified array, or hello last key and value of hello specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="f83b1-191">Örnek 1: dize</span><span class="sxs-lookup"><span data-stu-id="f83b1-191">Example 1: string</span></span>
<span data-ttu-id="f83b1-192">Merhaba aşağıdaki örnek verir `"r"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-192">hello following example returns `"r"`:</span></span>

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="f83b1-193">Örnek 2: dizi</span><span class="sxs-lookup"><span data-stu-id="f83b1-193">Example 2: array</span></span>
<span data-ttu-id="f83b1-194">Varsayın `element1` döndürür `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="f83b1-194">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="f83b1-195">Merhaba aşağıdaki örnek verir `2`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-195">hello following example returns `2`:</span></span>

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="f83b1-196">Örnek 3: nesnesi</span><span class="sxs-lookup"><span data-stu-id="f83b1-196">Example 3: object</span></span>
<span data-ttu-id="f83b1-197">Varsayın `element1` döndürür:</span><span class="sxs-lookup"><span data-stu-id="f83b1-197">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="f83b1-198">Merhaba aşağıdaki örnek verir `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-198">hello following example returns `{"key2": "raboof"}`:</span></span>

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a><span data-ttu-id="f83b1-199">Al</span><span class="sxs-lookup"><span data-stu-id="f83b1-199">take</span></span>
<span data-ttu-id="f83b1-200">Belirtilen sayıda ardışık karakteri hello dize hello başından, bitişik değerleri hello dizi hello başından itibaren belirli sayıda veya belirtilen sayıda bitişik anahtarlara ve hello nesnesinin hello başlangıç değerleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="f83b1-200">Returns a specified number of contiguous characters from hello start of hello string, a specified number of contiguous values from hello start of hello array, or a specified number of contiguous keys and values from hello start of hello object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="f83b1-201">Örnek 1: dize</span><span class="sxs-lookup"><span data-stu-id="f83b1-201">Example 1: string</span></span>
<span data-ttu-id="f83b1-202">Merhaba aşağıdaki örnek verir `"foo"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-202">hello following example returns `"foo"`:</span></span>

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="f83b1-203">Örnek 2: dizi</span><span class="sxs-lookup"><span data-stu-id="f83b1-203">Example 2: array</span></span>
<span data-ttu-id="f83b1-204">Varsayın `element1` döndürür `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="f83b1-204">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="f83b1-205">Merhaba aşağıdaki örnek verir `[1, 2]`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-205">hello following example returns `[1, 2]`:</span></span>

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="f83b1-206">Örnek 3: nesnesi</span><span class="sxs-lookup"><span data-stu-id="f83b1-206">Example 3: object</span></span>
<span data-ttu-id="f83b1-207">Varsayın `element1` döndürür:</span><span class="sxs-lookup"><span data-stu-id="f83b1-207">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="f83b1-208">Merhaba aşağıdaki örnek verir `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-208">hello following example returns `{"key1": "foobar"}`:</span></span>

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a><span data-ttu-id="f83b1-209">Atla</span><span class="sxs-lookup"><span data-stu-id="f83b1-209">skip</span></span>
<span data-ttu-id="f83b1-210">Belirtilen bir koleksiyondaki öğelerin sayısı atlar ve öğeleri kalan hello döndürür.</span><span class="sxs-lookup"><span data-stu-id="f83b1-210">Bypasses a specified number of elements in a collection, and then returns hello remaining elements.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="f83b1-211">Örnek 1: dize</span><span class="sxs-lookup"><span data-stu-id="f83b1-211">Example 1: string</span></span>
<span data-ttu-id="f83b1-212">Merhaba aşağıdaki örnek verir `"bar"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-212">hello following example returns `"bar"`:</span></span>

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="f83b1-213">Örnek 2: dizi</span><span class="sxs-lookup"><span data-stu-id="f83b1-213">Example 2: array</span></span>
<span data-ttu-id="f83b1-214">Varsayın `element1` döndürür `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="f83b1-214">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="f83b1-215">Merhaba aşağıdaki örnek verir `[3]`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-215">hello following example returns `[3]`:</span></span>

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="f83b1-216">Örnek 3: nesnesi</span><span class="sxs-lookup"><span data-stu-id="f83b1-216">Example 3: object</span></span>
<span data-ttu-id="f83b1-217">Varsayın `element1` döndürür:</span><span class="sxs-lookup"><span data-stu-id="f83b1-217">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="f83b1-218">Merhaba aşağıdaki örnek verir `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-218">hello following example returns `{"key2": "raboof"}`:</span></span>

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a><span data-ttu-id="f83b1-219">Mantıksal işlevleri</span><span class="sxs-lookup"><span data-stu-id="f83b1-219">Logical functions</span></span>
<span data-ttu-id="f83b1-220">Bu işlevler koşulları içinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f83b1-220">These functions can be used in conditionals.</span></span> <span data-ttu-id="f83b1-221">Bazı işlevler tüm JSON veri türlerini desteklemiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="f83b1-221">Some functions may not support all JSON data types.</span></span>

### <a name="equals"></a><span data-ttu-id="f83b1-222">eşittir</span><span class="sxs-lookup"><span data-stu-id="f83b1-222">equals</span></span>
<span data-ttu-id="f83b1-223">Döndürür `true` parametrelerinin her ikisini de aynı tür ve değer hello varsa.</span><span class="sxs-lookup"><span data-stu-id="f83b1-223">Returns `true` if both parameters have hello same type and value.</span></span> <span data-ttu-id="f83b1-224">Bu işlev tüm JSON veri türlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="f83b1-224">This function supports all JSON data types.</span></span>

<span data-ttu-id="f83b1-225">Merhaba aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-225">hello following example returns `true`:</span></span>

```json
"[equals(0, 0)]"
```

<span data-ttu-id="f83b1-226">Merhaba aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-226">hello following example returns `true`:</span></span>

```json
"[equals('foo', 'foo')]"
```

<span data-ttu-id="f83b1-227">Merhaba aşağıdaki örnek verir `false`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-227">hello following example returns `false`:</span></span>

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a><span data-ttu-id="f83b1-228">daha az</span><span class="sxs-lookup"><span data-stu-id="f83b1-228">less</span></span>
<span data-ttu-id="f83b1-229">Döndürür `true` hello ilk parametre hello ikinci parametre değerinden kesinlikle küçük ise.</span><span class="sxs-lookup"><span data-stu-id="f83b1-229">Returns `true` if hello first parameter is strictly less than hello second parameter.</span></span> <span data-ttu-id="f83b1-230">Bu işlev parametreleri yalnızca türü numarası ve dize destekler.</span><span class="sxs-lookup"><span data-stu-id="f83b1-230">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="f83b1-231">Merhaba aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-231">hello following example returns `true`:</span></span>

```json
"[less(1, 2)]"
```

<span data-ttu-id="f83b1-232">Merhaba aşağıdaki örnek verir `false`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-232">hello following example returns `false`:</span></span>

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a><span data-ttu-id="f83b1-233">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="f83b1-233">lessOrEquals</span></span>
<span data-ttu-id="f83b1-234">Döndürür `true` hello ilk parametre küçük veya buna eşit ise toohello ikinci parametre.</span><span class="sxs-lookup"><span data-stu-id="f83b1-234">Returns `true` if hello first parameter is less than or equal toohello second parameter.</span></span> <span data-ttu-id="f83b1-235">Bu işlev parametreleri yalnızca türü numarası ve dize destekler.</span><span class="sxs-lookup"><span data-stu-id="f83b1-235">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="f83b1-236">Merhaba aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-236">hello following example returns `true`:</span></span>

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a><span data-ttu-id="f83b1-237">büyük</span><span class="sxs-lookup"><span data-stu-id="f83b1-237">greater</span></span>
<span data-ttu-id="f83b1-238">Döndürür `true` hello ilk parametre hello ikinci parametre kesinlikle büyük ise.</span><span class="sxs-lookup"><span data-stu-id="f83b1-238">Returns `true` if hello first parameter is strictly greater than hello second parameter.</span></span> <span data-ttu-id="f83b1-239">Bu işlev parametreleri yalnızca türü numarası ve dize destekler.</span><span class="sxs-lookup"><span data-stu-id="f83b1-239">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="f83b1-240">Merhaba aşağıdaki örnek verir `false`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-240">hello following example returns `false`:</span></span>

```json
"[greater(1, 2)]"
```

<span data-ttu-id="f83b1-241">Merhaba aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-241">hello following example returns `true`:</span></span>

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a><span data-ttu-id="f83b1-242">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="f83b1-242">greaterOrEquals</span></span>
<span data-ttu-id="f83b1-243">Döndürür `true` hello ilk parametresi sıfırdan büyük veya eşit toohello ikinci parametre ise.</span><span class="sxs-lookup"><span data-stu-id="f83b1-243">Returns `true` if hello first parameter is greater than or equal toohello second parameter.</span></span> <span data-ttu-id="f83b1-244">Bu işlev parametreleri yalnızca türü numarası ve dize destekler.</span><span class="sxs-lookup"><span data-stu-id="f83b1-244">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="f83b1-245">Merhaba aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-245">hello following example returns `true`:</span></span>

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a><span data-ttu-id="f83b1-246">ve</span><span class="sxs-lookup"><span data-stu-id="f83b1-246">and</span></span>
<span data-ttu-id="f83b1-247">Döndürür `true` tüm hello parametreler çok değerlendirmek,`true`.</span><span class="sxs-lookup"><span data-stu-id="f83b1-247">Returns `true` if all hello parameters evaluate too`true`.</span></span> <span data-ttu-id="f83b1-248">Bu işlev yalnızca Boole türünde iki veya daha fazla parametre destekler.</span><span class="sxs-lookup"><span data-stu-id="f83b1-248">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="f83b1-249">Merhaba aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-249">hello following example returns `true`:</span></span>

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="f83b1-250">Merhaba aşağıdaki örnek verir `false`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-250">hello following example returns `false`:</span></span>

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a><span data-ttu-id="f83b1-251">or</span><span class="sxs-lookup"><span data-stu-id="f83b1-251">or</span></span>
<span data-ttu-id="f83b1-252">Döndürür `true` hello parametreleri en az biri çok değerlendirilirse`true`.</span><span class="sxs-lookup"><span data-stu-id="f83b1-252">Returns `true` if at least one of hello parameters evaluates too`true`.</span></span> <span data-ttu-id="f83b1-253">Bu işlev yalnızca Boole türünde iki veya daha fazla parametre destekler.</span><span class="sxs-lookup"><span data-stu-id="f83b1-253">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="f83b1-254">Merhaba aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-254">hello following example returns `true`:</span></span>

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="f83b1-255">Merhaba aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-255">hello following example returns `true`:</span></span>

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a><span data-ttu-id="f83b1-256">değil</span><span class="sxs-lookup"><span data-stu-id="f83b1-256">not</span></span>
<span data-ttu-id="f83b1-257">Döndürür `true` hello parametre çok değerlendirilirse`false`.</span><span class="sxs-lookup"><span data-stu-id="f83b1-257">Returns `true` if hello parameter evaluates too`false`.</span></span> <span data-ttu-id="f83b1-258">Bu işlev yalnızca Boole türünde parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="f83b1-258">This function supports parameters only of type Boolean.</span></span>

<span data-ttu-id="f83b1-259">Merhaba aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-259">hello following example returns `true`:</span></span>

```json
"[not(false)]"
```

<span data-ttu-id="f83b1-260">Merhaba aşağıdaki örnek verir `false`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-260">hello following example returns `false`:</span></span>

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a><span data-ttu-id="f83b1-261">birleşim</span><span class="sxs-lookup"><span data-stu-id="f83b1-261">coalesce</span></span>
<span data-ttu-id="f83b1-262">Merhaba ilk null olmayan parametresinin değerini döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="f83b1-262">Returns hello value of hello first non-null parameter.</span></span> <span data-ttu-id="f83b1-263">Bu işlev tüm JSON veri türlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="f83b1-263">This function supports all JSON data types.</span></span>

<span data-ttu-id="f83b1-264">Varsayın `element1` ve `element2` tanımlanmaz.</span><span class="sxs-lookup"><span data-stu-id="f83b1-264">Assume `element1` and `element2` are undefined.</span></span> <span data-ttu-id="f83b1-265">Merhaba aşağıdaki örnek verir `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-265">hello following example returns `"foobar"`:</span></span>

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a><span data-ttu-id="f83b1-266">Dönüşüm işlevleri</span><span class="sxs-lookup"><span data-stu-id="f83b1-266">Conversion functions</span></span>
<span data-ttu-id="f83b1-267">Bu işlevler kullanılan tooconvert değerleri JSON veri türleri ve Kodlamalar arasında olabilir.</span><span class="sxs-lookup"><span data-stu-id="f83b1-267">These functions can be used tooconvert values between JSON data types and encodings.</span></span>

### <a name="int"></a><span data-ttu-id="f83b1-268">Int</span><span class="sxs-lookup"><span data-stu-id="f83b1-268">int</span></span>
<span data-ttu-id="f83b1-269">Merhaba parametresi tooan tamsayı dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="f83b1-269">Converts hello parameter tooan integer.</span></span> <span data-ttu-id="f83b1-270">Bu işlev türü numarası ve dize parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="f83b1-270">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="f83b1-271">Merhaba aşağıdaki örnek verir `1`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-271">hello following example returns `1`:</span></span>

```json
"[int('1')]"
```

<span data-ttu-id="f83b1-272">Merhaba aşağıdaki örnek verir `2`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-272">hello following example returns `2`:</span></span>

```json
"[int(2.9)]"
```

### <a name="float"></a><span data-ttu-id="f83b1-273">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="f83b1-273">float</span></span>
<span data-ttu-id="f83b1-274">Kayan nokta Hello parametresi tooa dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="f83b1-274">Converts hello parameter tooa floating-point.</span></span> <span data-ttu-id="f83b1-275">Bu işlev türü numarası ve dize parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="f83b1-275">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="f83b1-276">Merhaba aşağıdaki örnek verir `1.0`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-276">hello following example returns `1.0`:</span></span>

```json
"[float('1.0')]"
```

<span data-ttu-id="f83b1-277">Merhaba aşağıdaki örnek verir `2.9`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-277">hello following example returns `2.9`:</span></span>

```json
"[float(2.9)]"
```

### <a name="string"></a><span data-ttu-id="f83b1-278">Dize</span><span class="sxs-lookup"><span data-stu-id="f83b1-278">string</span></span>
<span data-ttu-id="f83b1-279">Merhaba parametre tooa dizesi dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="f83b1-279">Converts hello parameter tooa string.</span></span> <span data-ttu-id="f83b1-280">Bu işlev parametreleri tüm JSON veri türlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="f83b1-280">This function supports parameters of all JSON data types.</span></span>

<span data-ttu-id="f83b1-281">Merhaba aşağıdaki örnek verir `"1"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-281">hello following example returns `"1"`:</span></span>

```json
"[string(1)]"
```

<span data-ttu-id="f83b1-282">Merhaba aşağıdaki örnek verir `"2.9"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-282">hello following example returns `"2.9"`:</span></span>

```json
"[string(2.9)]"
```

<span data-ttu-id="f83b1-283">Merhaba aşağıdaki örnek verir `"[1,2,3]"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-283">hello following example returns `"[1,2,3]"`:</span></span>

```json
"[string([1,2,3])]"
```

<span data-ttu-id="f83b1-284">Merhaba aşağıdaki örnek verir `"{"foo":"bar"}"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-284">hello following example returns `"{"foo":"bar"}"`:</span></span>

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a><span data-ttu-id="f83b1-285">bool</span><span class="sxs-lookup"><span data-stu-id="f83b1-285">bool</span></span>
<span data-ttu-id="f83b1-286">Merhaba parametresi tooa Boolean dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="f83b1-286">Converts hello parameter tooa Boolean.</span></span> <span data-ttu-id="f83b1-287">Bu işlev türü numarası, dize ve Boolean parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="f83b1-287">This function supports parameters of type number, string, and Boolean.</span></span> <span data-ttu-id="f83b1-288">JavaScript'te dışındaki herhangi bir değer benzer tooBooleans `0` veya `'false'` döndürür `true`.</span><span class="sxs-lookup"><span data-stu-id="f83b1-288">Similar tooBooleans in JavaScript, any value except `0` or `'false'` returns `true`.</span></span>

<span data-ttu-id="f83b1-289">Merhaba aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-289">hello following example returns `true`:</span></span>

```json
"[bool(1)]"
```

<span data-ttu-id="f83b1-290">Merhaba aşağıdaki örnek verir `false`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-290">hello following example returns `false`:</span></span>

```json
"[bool(0)]"
```

<span data-ttu-id="f83b1-291">Merhaba aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-291">hello following example returns `true`:</span></span>

```json
"[bool(true)]"
```

<span data-ttu-id="f83b1-292">Merhaba aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-292">hello following example returns `true`:</span></span>

```json
"[bool('true')]"
```

### <a name="parse"></a><span data-ttu-id="f83b1-293">Ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="f83b1-293">parse</span></span>
<span data-ttu-id="f83b1-294">Merhaba parametresi tooa yerel tür dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="f83b1-294">Converts hello parameter tooa native type.</span></span> <span data-ttu-id="f83b1-295">Diğer bir deyişle, bu hello tersini işlevidir `string()`.</span><span class="sxs-lookup"><span data-stu-id="f83b1-295">In other words, this function is hello inverse of `string()`.</span></span> <span data-ttu-id="f83b1-296">Bu işlev yalnızca dize türünde parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="f83b1-296">This function supports parameters only of type string.</span></span>

<span data-ttu-id="f83b1-297">Merhaba aşağıdaki örnek verir `1`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-297">hello following example returns `1`:</span></span>

```json
"[parse('1')]"
```

<span data-ttu-id="f83b1-298">Merhaba aşağıdaki örnek verir `true`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-298">hello following example returns `true`:</span></span>

```json
"[parse('true')]"
```

<span data-ttu-id="f83b1-299">Merhaba aşağıdaki örnek verir `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-299">hello following example returns `[1,2,3]`:</span></span>

```json
"[parse('[1,2,3]')]"
```

<span data-ttu-id="f83b1-300">Merhaba aşağıdaki örnek verir `{"foo":"bar"}`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-300">hello following example returns `{"foo":"bar"}`:</span></span>

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a><span data-ttu-id="f83b1-301">encodeBase64</span><span class="sxs-lookup"><span data-stu-id="f83b1-301">encodeBase64</span></span>
<span data-ttu-id="f83b1-302">Merhaba parametresi tooa base-64 kodlanmış dize olarak kodlar.</span><span class="sxs-lookup"><span data-stu-id="f83b1-302">Encodes hello parameter tooa base-64 encoded string.</span></span> <span data-ttu-id="f83b1-303">Bu işlev yalnızca dize türünde parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="f83b1-303">This function supports parameters only of type string.</span></span>

<span data-ttu-id="f83b1-304">Merhaba aşağıdaki örnek verir `"Zm9vYmFy"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-304">hello following example returns `"Zm9vYmFy"`:</span></span>

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a><span data-ttu-id="f83b1-305">decodeBase64</span><span class="sxs-lookup"><span data-stu-id="f83b1-305">decodeBase64</span></span>
<span data-ttu-id="f83b1-306">Base-64 kodlu bir dize Hello parametresinden kodunu çözer.</span><span class="sxs-lookup"><span data-stu-id="f83b1-306">Decodes hello parameter from a base-64 encoded string.</span></span> <span data-ttu-id="f83b1-307">Bu işlev yalnızca dize türünde parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="f83b1-307">This function supports parameters only of type string.</span></span>

<span data-ttu-id="f83b1-308">Merhaba aşağıdaki örnek verir `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-308">hello following example returns `"foobar"`:</span></span>

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a><span data-ttu-id="f83b1-309">Encodeurıcomponent</span><span class="sxs-lookup"><span data-stu-id="f83b1-309">encodeUriComponent</span></span>
<span data-ttu-id="f83b1-310">Merhaba parametresi tooa URL kodlanmış dize olarak kodlar.</span><span class="sxs-lookup"><span data-stu-id="f83b1-310">Encodes hello parameter tooa URL encoded string.</span></span> <span data-ttu-id="f83b1-311">Bu işlev yalnızca dize türünde parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="f83b1-311">This function supports parameters only of type string.</span></span>

<span data-ttu-id="f83b1-312">Merhaba aşağıdaki örnek verir `"https%3A%2F%2Fportal.azure.com%2F"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-312">hello following example returns `"https%3A%2F%2Fportal.azure.com%2F"`:</span></span>

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a><span data-ttu-id="f83b1-313">Decodeurıcomponent</span><span class="sxs-lookup"><span data-stu-id="f83b1-313">decodeUriComponent</span></span>
<span data-ttu-id="f83b1-314">Bir URL kodlanmış dize Hello parametresinden kodunu çözer.</span><span class="sxs-lookup"><span data-stu-id="f83b1-314">Decodes hello parameter from a URL encoded string.</span></span> <span data-ttu-id="f83b1-315">Bu işlev yalnızca dize türünde parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="f83b1-315">This function supports parameters only of type string.</span></span>

<span data-ttu-id="f83b1-316">Merhaba aşağıdaki örnek verir `"https://portal.azure.com/"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-316">hello following example returns `"https://portal.azure.com/"`:</span></span>

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a><span data-ttu-id="f83b1-317">Matematik işlevleri</span><span class="sxs-lookup"><span data-stu-id="f83b1-317">Math functions</span></span>
### <a name="add"></a><span data-ttu-id="f83b1-318">Ekleme</span><span class="sxs-lookup"><span data-stu-id="f83b1-318">add</span></span>
<span data-ttu-id="f83b1-319">İki sayı ekleyen ve hello sonucunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="f83b1-319">Adds two numbers, and returns hello result.</span></span>

<span data-ttu-id="f83b1-320">Merhaba aşağıdaki örnek verir `3`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-320">hello following example returns `3`:</span></span>

```json
"[add(1, 2)]"
```

### <a name="sub"></a><span data-ttu-id="f83b1-321">Sub</span><span class="sxs-lookup"><span data-stu-id="f83b1-321">sub</span></span>
<span data-ttu-id="f83b1-322">Merhaba ikinci sayı hello ilk numarasından çıkarır ve hello sonucunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="f83b1-322">Subtracts hello second number from hello first number, and returns hello result.</span></span>

<span data-ttu-id="f83b1-323">Merhaba aşağıdaki örnek verir `1`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-323">hello following example returns `1`:</span></span>

```json
"[sub(3, 2)]"
```

### <a name="mul"></a><span data-ttu-id="f83b1-324">mul</span><span class="sxs-lookup"><span data-stu-id="f83b1-324">mul</span></span>
<span data-ttu-id="f83b1-325">İki sayıyı çarpar ve hello sonucunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="f83b1-325">Multiplies two numbers, and returns hello result.</span></span>

<span data-ttu-id="f83b1-326">Merhaba aşağıdaki örnek verir `6`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-326">hello following example returns `6`:</span></span>

```json
"[mul(2, 3)]"
```

### <a name="div"></a><span data-ttu-id="f83b1-327">div</span><span class="sxs-lookup"><span data-stu-id="f83b1-327">div</span></span>
<span data-ttu-id="f83b1-328">Merhaba ikinci sayı Hello ilk sayıyı böler ve hello sonucunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="f83b1-328">Divides hello first number by hello second number, and returns hello result.</span></span> <span data-ttu-id="f83b1-329">Merhaba sonucu her zaman bir tamsayıdır.</span><span class="sxs-lookup"><span data-stu-id="f83b1-329">hello result is always an integer.</span></span>

<span data-ttu-id="f83b1-330">Merhaba aşağıdaki örnek verir `2`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-330">hello following example returns `2`:</span></span>

```json
"[div(6, 3)]"
```

### <a name="mod"></a><span data-ttu-id="f83b1-331">mod</span><span class="sxs-lookup"><span data-stu-id="f83b1-331">mod</span></span>
<span data-ttu-id="f83b1-332">Merhaba ikinci sayı Hello ilk sayıyı böler ve hello kalanı döndürür.</span><span class="sxs-lookup"><span data-stu-id="f83b1-332">Divides hello first number by hello second number, and returns hello remainder.</span></span>

<span data-ttu-id="f83b1-333">Merhaba aşağıdaki örnek verir `0`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-333">hello following example returns `0`:</span></span>

```json
"[mod(6, 3)]"
```

<span data-ttu-id="f83b1-334">Merhaba aşağıdaki örnek verir `2`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-334">hello following example returns `2`:</span></span>

```json
"[mod(6, 4)]"
```

### <a name="min"></a><span data-ttu-id="f83b1-335">dk</span><span class="sxs-lookup"><span data-stu-id="f83b1-335">min</span></span>
<span data-ttu-id="f83b1-336">Küçük hello iki numaraları döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="f83b1-336">Returns hello small of hello two numbers.</span></span>

<span data-ttu-id="f83b1-337">Merhaba aşağıdaki örnek verir `1`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-337">hello following example returns `1`:</span></span>

```json
"[min(1, 2)]"
```

### <a name="max"></a><span data-ttu-id="f83b1-338">max</span><span class="sxs-lookup"><span data-stu-id="f83b1-338">max</span></span>
<span data-ttu-id="f83b1-339">Döndürür hello hello iki sayı ile daha büyük.</span><span class="sxs-lookup"><span data-stu-id="f83b1-339">Returns hello larger of hello two numbers.</span></span>

<span data-ttu-id="f83b1-340">Merhaba aşağıdaki örnek verir `2`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-340">hello following example returns `2`:</span></span>

```json
"[max(1, 2)]"
```

### <a name="range"></a><span data-ttu-id="f83b1-341">Aralık</span><span class="sxs-lookup"><span data-stu-id="f83b1-341">range</span></span>
<span data-ttu-id="f83b1-342">İntegral dizisi oluşturur numaraları hello içinde belirtilen aralık.</span><span class="sxs-lookup"><span data-stu-id="f83b1-342">Generates a sequence of integral numbers within hello specified range.</span></span>

<span data-ttu-id="f83b1-343">Merhaba aşağıdaki örnek verir `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-343">hello following example returns `[1,2,3]`:</span></span>

```json
"[range(1, 3)]"
```

### <a name="rand"></a><span data-ttu-id="f83b1-344">rand</span><span class="sxs-lookup"><span data-stu-id="f83b1-344">rand</span></span>
<span data-ttu-id="f83b1-345">Bir rastgele döndürür tamsayı hello içinde belirtilen aralık.</span><span class="sxs-lookup"><span data-stu-id="f83b1-345">Returns a random integral number within hello specified range.</span></span> <span data-ttu-id="f83b1-346">Bu işlev, şifreleme açısından güvenli rastgele sayılar oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="f83b1-346">This function does not generate cryptographically secure random numbers.</span></span>

<span data-ttu-id="f83b1-347">Merhaba aşağıdaki örnek döndürebilir `42`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-347">hello following example could return `42`:</span></span>

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a><span data-ttu-id="f83b1-348">Kat</span><span class="sxs-lookup"><span data-stu-id="f83b1-348">floor</span></span>
<span data-ttu-id="f83b1-349">Küçük veya buna eşit Hello en büyük tamsayıyı döndürür toohello belirtilen sayı.</span><span class="sxs-lookup"><span data-stu-id="f83b1-349">Returns hello largest integer less than or equal toohello specified number.</span></span>

<span data-ttu-id="f83b1-350">Merhaba aşağıdaki örnek verir `3`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-350">hello following example returns `3`:</span></span>

```json
"[floor(3.14)]"
```

### <a name="ceil"></a><span data-ttu-id="f83b1-351">ceil</span><span class="sxs-lookup"><span data-stu-id="f83b1-351">ceil</span></span>
<span data-ttu-id="f83b1-352">Değerinden büyük tamsayıyı döndürür hello veya eşit toohello numarası belirtildi.</span><span class="sxs-lookup"><span data-stu-id="f83b1-352">Returns hello largest integer greater than or equal toohello specified number.</span></span>

<span data-ttu-id="f83b1-353">Merhaba aşağıdaki örnek verir `4`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-353">hello following example returns `4`:</span></span>

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a><span data-ttu-id="f83b1-354">Date işlevleri</span><span class="sxs-lookup"><span data-stu-id="f83b1-354">Date functions</span></span>
### <a name="utcnow"></a><span data-ttu-id="f83b1-355">utcNow</span><span class="sxs-lookup"><span data-stu-id="f83b1-355">utcNow</span></span>
<span data-ttu-id="f83b1-356">ISO 8601 biçiminde hello geçerli tarih ve saat hello yerel bilgisayardaki bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="f83b1-356">Returns a string in ISO 8601 format of hello current date and time on hello local computer.</span></span>

<span data-ttu-id="f83b1-357">Merhaba aşağıdaki örnek döndürebilir `"1990-12-31T23:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-357">hello following example could return `"1990-12-31T23:59:59.000Z"`:</span></span>

```json
"[utcNow()]"
```

### <a name="addseconds"></a><span data-ttu-id="f83b1-358">saniyeEkle</span><span class="sxs-lookup"><span data-stu-id="f83b1-358">addSeconds</span></span>
<span data-ttu-id="f83b1-359">Bir tamsayı belirtilen saniye toohello ekler zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="f83b1-359">Adds an integral number of seconds toohello specified timestamp.</span></span>

<span data-ttu-id="f83b1-360">Merhaba aşağıdaki örnek verir `"1991-01-01T00:00:00.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-360">hello following example returns `"1991-01-01T00:00:00.000Z"`:</span></span>

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a><span data-ttu-id="f83b1-361">addMinutes</span><span class="sxs-lookup"><span data-stu-id="f83b1-361">addMinutes</span></span>
<span data-ttu-id="f83b1-362">Bir tamsayı belirtilen dakika toohello ekler zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="f83b1-362">Adds an integral number of minutes toohello specified timestamp.</span></span>

<span data-ttu-id="f83b1-363">Merhaba aşağıdaki örnek verir `"1991-01-01T00:00:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-363">hello following example returns `"1991-01-01T00:00:59.000Z"`:</span></span>

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a><span data-ttu-id="f83b1-364">addHours</span><span class="sxs-lookup"><span data-stu-id="f83b1-364">addHours</span></span>
<span data-ttu-id="f83b1-365">Belirtilen saat toohello bir tamsayı ekler zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="f83b1-365">Adds an integral number of hours toohello specified timestamp.</span></span>

<span data-ttu-id="f83b1-366">Merhaba aşağıdaki örnek verir `"1991-01-01T00:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="f83b1-366">hello following example returns `"1991-01-01T00:59:59.000Z"`:</span></span>

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a><span data-ttu-id="f83b1-367">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f83b1-367">Next steps</span></span>
* <span data-ttu-id="f83b1-368">Bir giriş tooAzure kaynak yöneticisi için bkz: [Azure Resource Manager'a genel bakış](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f83b1-368">For an introduction tooAzure Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

