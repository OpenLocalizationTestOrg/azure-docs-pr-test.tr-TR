---
title: "aaaAzure Resource Manager şablonu işlevleri - diziler ve nesneleri | Microsoft Docs"
description: "Diziler ve nesneleri ile çalışmak için bir Azure Resource Manager şablonunda Hello işlevleri toouse açıklar."
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
ms.date: 06/12/2017
ms.author: tomfitz
ms.openlocfilehash: e5f1a9b2a71039562eae7e48c2474a1fa59a7bea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="c526f-103">Dizi ve nesne işlevleri için Azure Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="c526f-103">Array and object functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="c526f-104">Kaynak Yöneticisi, nesneler ve diziler ile çalışmak için birkaç işlevleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="c526f-104">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="c526f-105">dizi</span><span class="sxs-lookup"><span data-stu-id="c526f-105">array</span></span>](#array)
* [<span data-ttu-id="c526f-106">birleşim</span><span class="sxs-lookup"><span data-stu-id="c526f-106">coalesce</span></span>](#coalesce)
* [<span data-ttu-id="c526f-107">concat</span><span class="sxs-lookup"><span data-stu-id="c526f-107">concat</span></span>](#concat)
* [<span data-ttu-id="c526f-108">içerir</span><span class="sxs-lookup"><span data-stu-id="c526f-108">contains</span></span>](#contains)
* [<span data-ttu-id="c526f-109">createArray</span><span class="sxs-lookup"><span data-stu-id="c526f-109">createArray</span></span>](#createarray)
* [<span data-ttu-id="c526f-110">boş</span><span class="sxs-lookup"><span data-stu-id="c526f-110">empty</span></span>](#empty)
* [<span data-ttu-id="c526f-111">ilk</span><span class="sxs-lookup"><span data-stu-id="c526f-111">first</span></span>](#first)
* [<span data-ttu-id="c526f-112">kesişim</span><span class="sxs-lookup"><span data-stu-id="c526f-112">intersection</span></span>](#intersection)
* [<span data-ttu-id="c526f-113">JSON</span><span class="sxs-lookup"><span data-stu-id="c526f-113">json</span></span>](#json)
* [<span data-ttu-id="c526f-114">Son</span><span class="sxs-lookup"><span data-stu-id="c526f-114">last</span></span>](#last)
* [<span data-ttu-id="c526f-115">uzunluğu</span><span class="sxs-lookup"><span data-stu-id="c526f-115">length</span></span>](#length)
* [<span data-ttu-id="c526f-116">Min</span><span class="sxs-lookup"><span data-stu-id="c526f-116">min</span></span>](#min)
* [<span data-ttu-id="c526f-117">max</span><span class="sxs-lookup"><span data-stu-id="c526f-117">max</span></span>](#max)
* [<span data-ttu-id="c526f-118">Aralık</span><span class="sxs-lookup"><span data-stu-id="c526f-118">range</span></span>](#range)
* [<span data-ttu-id="c526f-119">Atla</span><span class="sxs-lookup"><span data-stu-id="c526f-119">skip</span></span>](#skip)
* [<span data-ttu-id="c526f-120">Al</span><span class="sxs-lookup"><span data-stu-id="c526f-120">take</span></span>](#take)
* [<span data-ttu-id="c526f-121">birleşim</span><span class="sxs-lookup"><span data-stu-id="c526f-121">union</span></span>](#union)

<span data-ttu-id="c526f-122">tooget dize değerlerini bir değer ile ayrılmış bir dizi bkz [bölme](resource-group-template-functions-string.md#split).</span><span class="sxs-lookup"><span data-stu-id="c526f-122">tooget an array of string values delimited by a value, see [split](resource-group-template-functions-string.md#split).</span></span>

<a id="array" />

## <a name="array"></a><span data-ttu-id="c526f-123">Dizi</span><span class="sxs-lookup"><span data-stu-id="c526f-123">array</span></span>
`array(convertToArray)`

<span data-ttu-id="c526f-124">Hello değeri tooan dizisine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="c526f-124">Converts hello value tooan array.</span></span>

### <a name="parameters"></a><span data-ttu-id="c526f-125">Parametreler</span><span class="sxs-lookup"><span data-stu-id="c526f-125">Parameters</span></span>

| <span data-ttu-id="c526f-126">Parametre</span><span class="sxs-lookup"><span data-stu-id="c526f-126">Parameter</span></span> | <span data-ttu-id="c526f-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c526f-127">Required</span></span> | <span data-ttu-id="c526f-128">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-128">Type</span></span> | <span data-ttu-id="c526f-129">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c526f-129">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c526f-130">convertToArray</span><span class="sxs-lookup"><span data-stu-id="c526f-130">convertToArray</span></span> |<span data-ttu-id="c526f-131">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-131">Yes</span></span> |<span data-ttu-id="c526f-132">int, string, dizi veya nesne</span><span class="sxs-lookup"><span data-stu-id="c526f-132">int, string, array, or object</span></span> |<span data-ttu-id="c526f-133">Merhaba değeri tooconvert tooan dizisi.</span><span class="sxs-lookup"><span data-stu-id="c526f-133">hello value tooconvert tooan array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c526f-134">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="c526f-134">Return value</span></span>

<span data-ttu-id="c526f-135">Bir dizi.</span><span class="sxs-lookup"><span data-stu-id="c526f-135">An array.</span></span>

### <a name="example"></a><span data-ttu-id="c526f-136">Örnek</span><span class="sxs-lookup"><span data-stu-id="c526f-136">Example</span></span>

<span data-ttu-id="c526f-137">Merhaba aşağıdaki örnekte nasıl toouse hello dizi işlevi farklı türler ile gösterilir.</span><span class="sxs-lookup"><span data-stu-id="c526f-137">hello following example shows how toouse hello array function with different types.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "intToConvert": {
            "type": "int",
            "defaultValue": 1
        },
        "stringToConvert": {
            "type": "string",
            "defaultValue": "a"
        },
        "objectToConvert": {
            "type": "object",
            "defaultValue": {"a": "b", "c": "d"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "intOutput": {
            "type": "array",
            "value": "[array(parameters('intToConvert'))]"
        },
        "stringOutput": {
            "type": "array",
            "value": "[array(parameters('stringToConvert'))]"
        },
        "objectOutput": {
            "type": "array",
            "value": "[array(parameters('objectToConvert'))]"
        }
    }
}
```

<span data-ttu-id="c526f-138">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="c526f-138">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c526f-139">Ad</span><span class="sxs-lookup"><span data-stu-id="c526f-139">Name</span></span> | <span data-ttu-id="c526f-140">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-140">Type</span></span> | <span data-ttu-id="c526f-141">Değer</span><span class="sxs-lookup"><span data-stu-id="c526f-141">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c526f-142">intOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-142">intOutput</span></span> | <span data-ttu-id="c526f-143">Dizi</span><span class="sxs-lookup"><span data-stu-id="c526f-143">Array</span></span> | <span data-ttu-id="c526f-144">[1]</span><span class="sxs-lookup"><span data-stu-id="c526f-144">[1]</span></span> |
| <span data-ttu-id="c526f-145">stringOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-145">stringOutput</span></span> | <span data-ttu-id="c526f-146">Dizi</span><span class="sxs-lookup"><span data-stu-id="c526f-146">Array</span></span> | <span data-ttu-id="c526f-147">["a"]</span><span class="sxs-lookup"><span data-stu-id="c526f-147">["a"]</span></span> |
| <span data-ttu-id="c526f-148">objectOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-148">objectOutput</span></span> | <span data-ttu-id="c526f-149">Dizi</span><span class="sxs-lookup"><span data-stu-id="c526f-149">Array</span></span> | <span data-ttu-id="c526f-150">[{"a": "b", "c": "d"}]</span><span class="sxs-lookup"><span data-stu-id="c526f-150">[{"a": "b", "c": "d"}]</span></span> |

<a id="coalesce" />

## <a name="coalesce"></a><span data-ttu-id="c526f-151">birleşim</span><span class="sxs-lookup"><span data-stu-id="c526f-151">coalesce</span></span>
`coalesce(arg1, arg2, arg3, ...)`

<span data-ttu-id="c526f-152">İlk değeri null olmayan hello parametrelerinden döndürür.</span><span class="sxs-lookup"><span data-stu-id="c526f-152">Returns first non-null value from hello parameters.</span></span> <span data-ttu-id="c526f-153">Boş dizeler, boş diziler ve boş nesneleri null değil.</span><span class="sxs-lookup"><span data-stu-id="c526f-153">Empty strings, empty arrays, and empty objects are not null.</span></span>

### <a name="parameters"></a><span data-ttu-id="c526f-154">Parametreler</span><span class="sxs-lookup"><span data-stu-id="c526f-154">Parameters</span></span>

| <span data-ttu-id="c526f-155">Parametre</span><span class="sxs-lookup"><span data-stu-id="c526f-155">Parameter</span></span> | <span data-ttu-id="c526f-156">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c526f-156">Required</span></span> | <span data-ttu-id="c526f-157">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-157">Type</span></span> | <span data-ttu-id="c526f-158">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c526f-158">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c526f-159">arg1</span><span class="sxs-lookup"><span data-stu-id="c526f-159">arg1</span></span> |<span data-ttu-id="c526f-160">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-160">Yes</span></span> |<span data-ttu-id="c526f-161">int, string, dizi veya nesne</span><span class="sxs-lookup"><span data-stu-id="c526f-161">int, string, array, or object</span></span> |<span data-ttu-id="c526f-162">Merhaba ilk değer tootest, null.</span><span class="sxs-lookup"><span data-stu-id="c526f-162">hello first value tootest for null.</span></span> |
| <span data-ttu-id="c526f-163">Ek bağımsız değişken</span><span class="sxs-lookup"><span data-stu-id="c526f-163">additional args</span></span> |<span data-ttu-id="c526f-164">Hayır</span><span class="sxs-lookup"><span data-stu-id="c526f-164">No</span></span> |<span data-ttu-id="c526f-165">int, string, dizi veya nesne</span><span class="sxs-lookup"><span data-stu-id="c526f-165">int, string, array, or object</span></span> |<span data-ttu-id="c526f-166">Ek değerler tootest, null.</span><span class="sxs-lookup"><span data-stu-id="c526f-166">Additional values tootest for null.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c526f-167">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="c526f-167">Return value</span></span>

<span data-ttu-id="c526f-168">dize, int, dizi veya nesne olabilen hello ilk null olmayan parametreleri, başlangıç değeri.</span><span class="sxs-lookup"><span data-stu-id="c526f-168">hello value of hello first non-null parameters, which can be a string, int, array, or object.</span></span> <span data-ttu-id="c526f-169">Tüm parametreleri null ise null.</span><span class="sxs-lookup"><span data-stu-id="c526f-169">Null if all parameters are null.</span></span> 

### <a name="example"></a><span data-ttu-id="c526f-170">Örnek</span><span class="sxs-lookup"><span data-stu-id="c526f-170">Example</span></span>

<span data-ttu-id="c526f-171">Merhaba aşağıdaki örnek birleşim farklı kullanımlarını hello çıktısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c526f-171">hello following example shows hello output from different uses of coalesce.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {
                "null1": null, 
                "null2": null,
                "string": "default",
                "int": 1,
                "object": {"first": "default"},
                "array": [1]
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').string)]"
        },
        "intOutput": {
            "type": "int",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').int)]"
        },
        "objectOutput": {
            "type": "object",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').object)]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').array)]"
        },
        "emptyOutput": {
            "type": "bool",
            "value": "[empty(coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2))]"
        }
    }
}
```

<span data-ttu-id="c526f-172">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="c526f-172">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c526f-173">Ad</span><span class="sxs-lookup"><span data-stu-id="c526f-173">Name</span></span> | <span data-ttu-id="c526f-174">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-174">Type</span></span> | <span data-ttu-id="c526f-175">Değer</span><span class="sxs-lookup"><span data-stu-id="c526f-175">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c526f-176">stringOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-176">stringOutput</span></span> | <span data-ttu-id="c526f-177">Dize</span><span class="sxs-lookup"><span data-stu-id="c526f-177">String</span></span> | <span data-ttu-id="c526f-178">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="c526f-178">default</span></span> |
| <span data-ttu-id="c526f-179">intOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-179">intOutput</span></span> | <span data-ttu-id="c526f-180">Int</span><span class="sxs-lookup"><span data-stu-id="c526f-180">Int</span></span> | <span data-ttu-id="c526f-181">1</span><span class="sxs-lookup"><span data-stu-id="c526f-181">1</span></span> |
| <span data-ttu-id="c526f-182">objectOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-182">objectOutput</span></span> | <span data-ttu-id="c526f-183">Nesne</span><span class="sxs-lookup"><span data-stu-id="c526f-183">Object</span></span> | <span data-ttu-id="c526f-184">{"ilk": "varsayılan"}</span><span class="sxs-lookup"><span data-stu-id="c526f-184">{"first": "default"}</span></span> |
| <span data-ttu-id="c526f-185">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-185">arrayOutput</span></span> | <span data-ttu-id="c526f-186">Dizi</span><span class="sxs-lookup"><span data-stu-id="c526f-186">Array</span></span> | <span data-ttu-id="c526f-187">[1]</span><span class="sxs-lookup"><span data-stu-id="c526f-187">[1]</span></span> |
| <span data-ttu-id="c526f-188">emptyOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-188">emptyOutput</span></span> | <span data-ttu-id="c526f-189">bool</span><span class="sxs-lookup"><span data-stu-id="c526f-189">Bool</span></span> | <span data-ttu-id="c526f-190">True</span><span class="sxs-lookup"><span data-stu-id="c526f-190">True</span></span> |

<a id="concat" />

## <a name="concat"></a><span data-ttu-id="c526f-191">concat</span><span class="sxs-lookup"><span data-stu-id="c526f-191">concat</span></span>
`concat(arg1, arg2, arg3, ...)`

<span data-ttu-id="c526f-192">Birden çok döndürür birleştirilmiş hello dizisi ve diziler birleştirir veya birden çok dize değerlerini birleştirir ve hello birleştirilmiş dizeyi döndürür.</span><span class="sxs-lookup"><span data-stu-id="c526f-192">Combines multiple arrays and returns hello concatenated array, or combines multiple string values and returns hello concatenated string.</span></span> 

### <a name="parameters"></a><span data-ttu-id="c526f-193">Parametreler</span><span class="sxs-lookup"><span data-stu-id="c526f-193">Parameters</span></span>

| <span data-ttu-id="c526f-194">Parametre</span><span class="sxs-lookup"><span data-stu-id="c526f-194">Parameter</span></span> | <span data-ttu-id="c526f-195">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c526f-195">Required</span></span> | <span data-ttu-id="c526f-196">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-196">Type</span></span> | <span data-ttu-id="c526f-197">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c526f-197">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c526f-198">arg1</span><span class="sxs-lookup"><span data-stu-id="c526f-198">arg1</span></span> |<span data-ttu-id="c526f-199">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-199">Yes</span></span> |<span data-ttu-id="c526f-200">dizi veya dize</span><span class="sxs-lookup"><span data-stu-id="c526f-200">array or string</span></span> |<span data-ttu-id="c526f-201">ilk dizi veya dize birleştirme için hello.</span><span class="sxs-lookup"><span data-stu-id="c526f-201">hello first array or string for concatenation.</span></span> |
| <span data-ttu-id="c526f-202">Ek bağımsız değişkenler</span><span class="sxs-lookup"><span data-stu-id="c526f-202">additional arguments</span></span> |<span data-ttu-id="c526f-203">Hayır</span><span class="sxs-lookup"><span data-stu-id="c526f-203">No</span></span> |<span data-ttu-id="c526f-204">dizi veya dize</span><span class="sxs-lookup"><span data-stu-id="c526f-204">array or string</span></span> |<span data-ttu-id="c526f-205">Ek diziler veya birleştirme için sıralı bir düzende dizeleri.</span><span class="sxs-lookup"><span data-stu-id="c526f-205">Additional arrays or strings in sequential order for concatenation.</span></span> |

<span data-ttu-id="c526f-206">Bu işlev bağımsız değişkenleri herhangi bir sayıda alabilir ve dizeler veya diziler için başlangıç parametreleri kabul edebilir.</span><span class="sxs-lookup"><span data-stu-id="c526f-206">This function can take any number of arguments, and can accept either strings or arrays for hello parameters.</span></span>

### <a name="return-value"></a><span data-ttu-id="c526f-207">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="c526f-207">Return value</span></span>
<span data-ttu-id="c526f-208">Bir dize veya birleştirilmiş değerleri dizisi.</span><span class="sxs-lookup"><span data-stu-id="c526f-208">A string or array of concatenated values.</span></span>

### <a name="example"></a><span data-ttu-id="c526f-209">Örnek</span><span class="sxs-lookup"><span data-stu-id="c526f-209">Example</span></span>

<span data-ttu-id="c526f-210">Aşağıdaki örnek hello nasıl toocombine iki dizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="c526f-210">hello following example shows how toocombine two arrays.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "firstArray": { 
            "type": "array", 
            "defaultValue": [ 
                "1-1", 
                "1-2", 
                "1-3" 
            ] 
        },
        "secondArray": {
            "type": "array", 
            "defaultValue": [ 
                "2-1", 
                "2-2",
                "2-3" 
            ] 
        }
    },
    "resources": [
    ],
    "outputs": {
        "return": {
            "type": "array",
            "value": "[concat(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="c526f-211">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="c526f-211">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c526f-212">Ad</span><span class="sxs-lookup"><span data-stu-id="c526f-212">Name</span></span> | <span data-ttu-id="c526f-213">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-213">Type</span></span> | <span data-ttu-id="c526f-214">Değer</span><span class="sxs-lookup"><span data-stu-id="c526f-214">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c526f-215">Döndür</span><span class="sxs-lookup"><span data-stu-id="c526f-215">return</span></span> | <span data-ttu-id="c526f-216">Dizi</span><span class="sxs-lookup"><span data-stu-id="c526f-216">Array</span></span> | <span data-ttu-id="c526f-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="c526f-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<span data-ttu-id="c526f-218">Aşağıdaki örnek hello nasıl toocombine iki string değerleri ve birleştirilmiş dizeyi döndürür gösterir.</span><span class="sxs-lookup"><span data-stu-id="c526f-218">hello following example shows how toocombine two string values and return a concatenated string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "prefix": {
            "type": "string",
            "defaultValue": "prefix"
        }
    },
    "resources": [],
    "outputs": {
        "concatOutput": {
            "value": "[concat(parameters('prefix'), '-', uniqueString(resourceGroup().id))]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="c526f-219">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="c526f-219">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c526f-220">Ad</span><span class="sxs-lookup"><span data-stu-id="c526f-220">Name</span></span> | <span data-ttu-id="c526f-221">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-221">Type</span></span> | <span data-ttu-id="c526f-222">Değer</span><span class="sxs-lookup"><span data-stu-id="c526f-222">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c526f-223">concatOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-223">concatOutput</span></span> | <span data-ttu-id="c526f-224">Dize</span><span class="sxs-lookup"><span data-stu-id="c526f-224">String</span></span> | <span data-ttu-id="c526f-225">önek 5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="c526f-225">prefix-5yj4yjf5mbg72</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="c526f-226">içerir</span><span class="sxs-lookup"><span data-stu-id="c526f-226">contains</span></span>
`contains(container, itemToFind)`

<span data-ttu-id="c526f-227">Bir değer dizisini içerir, bir nesne bir anahtar veya bir dize bir alt dizeyi içeren olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="c526f-227">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="c526f-228">Parametreler</span><span class="sxs-lookup"><span data-stu-id="c526f-228">Parameters</span></span>

| <span data-ttu-id="c526f-229">Parametre</span><span class="sxs-lookup"><span data-stu-id="c526f-229">Parameter</span></span> | <span data-ttu-id="c526f-230">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c526f-230">Required</span></span> | <span data-ttu-id="c526f-231">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-231">Type</span></span> | <span data-ttu-id="c526f-232">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c526f-232">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c526f-233">kapsayıcı</span><span class="sxs-lookup"><span data-stu-id="c526f-233">container</span></span> |<span data-ttu-id="c526f-234">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-234">Yes</span></span> |<span data-ttu-id="c526f-235">dizi, nesne veya dize</span><span class="sxs-lookup"><span data-stu-id="c526f-235">array, object, or string</span></span> |<span data-ttu-id="c526f-236">Merhaba değeri toofind içeren hello değeri.</span><span class="sxs-lookup"><span data-stu-id="c526f-236">hello value that contains hello value toofind.</span></span> |
| <span data-ttu-id="c526f-237">itemToFind</span><span class="sxs-lookup"><span data-stu-id="c526f-237">itemToFind</span></span> |<span data-ttu-id="c526f-238">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-238">Yes</span></span> |<span data-ttu-id="c526f-239">dize veya int</span><span class="sxs-lookup"><span data-stu-id="c526f-239">string or int</span></span> |<span data-ttu-id="c526f-240">Merhaba değeri toofind.</span><span class="sxs-lookup"><span data-stu-id="c526f-240">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c526f-241">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="c526f-241">Return value</span></span>

<span data-ttu-id="c526f-242">**Doğru** hello öğe bulunduysa, **False**.</span><span class="sxs-lookup"><span data-stu-id="c526f-242">**True** if hello item is found; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="c526f-243">Örnek</span><span class="sxs-lookup"><span data-stu-id="c526f-243">Example</span></span>

<span data-ttu-id="c526f-244">Merhaba aşağıdaki örnekte nasıl toouse farklı türleriyle içeren gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="c526f-244">hello following example shows how toouse contains with different types:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "OneTwoThree"
        },
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringTrue": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'e')]"
        },
        "stringFalse": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'z')]"
        },
        "objectTrue": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'one')]"
        },
        "objectFalse": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'a')]"
        },
        "arrayTrue": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'three')]"
        },
        "arrayFalse": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'four')]"
        }
    }
}
```

<span data-ttu-id="c526f-245">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="c526f-245">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c526f-246">Ad</span><span class="sxs-lookup"><span data-stu-id="c526f-246">Name</span></span> | <span data-ttu-id="c526f-247">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-247">Type</span></span> | <span data-ttu-id="c526f-248">Değer</span><span class="sxs-lookup"><span data-stu-id="c526f-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c526f-249">stringTrue</span><span class="sxs-lookup"><span data-stu-id="c526f-249">stringTrue</span></span> | <span data-ttu-id="c526f-250">bool</span><span class="sxs-lookup"><span data-stu-id="c526f-250">Bool</span></span> | <span data-ttu-id="c526f-251">True</span><span class="sxs-lookup"><span data-stu-id="c526f-251">True</span></span> |
| <span data-ttu-id="c526f-252">stringFalse</span><span class="sxs-lookup"><span data-stu-id="c526f-252">stringFalse</span></span> | <span data-ttu-id="c526f-253">bool</span><span class="sxs-lookup"><span data-stu-id="c526f-253">Bool</span></span> | <span data-ttu-id="c526f-254">False</span><span class="sxs-lookup"><span data-stu-id="c526f-254">False</span></span> |
| <span data-ttu-id="c526f-255">objectTrue</span><span class="sxs-lookup"><span data-stu-id="c526f-255">objectTrue</span></span> | <span data-ttu-id="c526f-256">bool</span><span class="sxs-lookup"><span data-stu-id="c526f-256">Bool</span></span> | <span data-ttu-id="c526f-257">True</span><span class="sxs-lookup"><span data-stu-id="c526f-257">True</span></span> |
| <span data-ttu-id="c526f-258">objectFalse</span><span class="sxs-lookup"><span data-stu-id="c526f-258">objectFalse</span></span> | <span data-ttu-id="c526f-259">bool</span><span class="sxs-lookup"><span data-stu-id="c526f-259">Bool</span></span> | <span data-ttu-id="c526f-260">False</span><span class="sxs-lookup"><span data-stu-id="c526f-260">False</span></span> |
| <span data-ttu-id="c526f-261">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="c526f-261">arrayTrue</span></span> | <span data-ttu-id="c526f-262">bool</span><span class="sxs-lookup"><span data-stu-id="c526f-262">Bool</span></span> | <span data-ttu-id="c526f-263">True</span><span class="sxs-lookup"><span data-stu-id="c526f-263">True</span></span> |
| <span data-ttu-id="c526f-264">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="c526f-264">arrayFalse</span></span> | <span data-ttu-id="c526f-265">bool</span><span class="sxs-lookup"><span data-stu-id="c526f-265">Bool</span></span> | <span data-ttu-id="c526f-266">False</span><span class="sxs-lookup"><span data-stu-id="c526f-266">False</span></span> |

<a id="createarray" />

## <a name="createarray"></a><span data-ttu-id="c526f-267">createarray</span><span class="sxs-lookup"><span data-stu-id="c526f-267">createarray</span></span>
`createArray (arg1, arg2, arg3, ...)`

<span data-ttu-id="c526f-268">Bir dizi hello parametrelerinden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c526f-268">Creates an array from hello parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="c526f-269">Parametreler</span><span class="sxs-lookup"><span data-stu-id="c526f-269">Parameters</span></span>

| <span data-ttu-id="c526f-270">Parametre</span><span class="sxs-lookup"><span data-stu-id="c526f-270">Parameter</span></span> | <span data-ttu-id="c526f-271">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c526f-271">Required</span></span> | <span data-ttu-id="c526f-272">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-272">Type</span></span> | <span data-ttu-id="c526f-273">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c526f-273">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c526f-274">arg1</span><span class="sxs-lookup"><span data-stu-id="c526f-274">arg1</span></span> |<span data-ttu-id="c526f-275">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-275">Yes</span></span> |<span data-ttu-id="c526f-276">Dize, tamsayı, dizi veya nesne</span><span class="sxs-lookup"><span data-stu-id="c526f-276">String, Integer, Array, or Object</span></span> |<span data-ttu-id="c526f-277">Merhaba hello dizinin ilk değer.</span><span class="sxs-lookup"><span data-stu-id="c526f-277">hello first value in hello array.</span></span> |
| <span data-ttu-id="c526f-278">Ek bağımsız değişkenler</span><span class="sxs-lookup"><span data-stu-id="c526f-278">additional arguments</span></span> |<span data-ttu-id="c526f-279">Hayır</span><span class="sxs-lookup"><span data-stu-id="c526f-279">No</span></span> |<span data-ttu-id="c526f-280">Dize, tamsayı, dizi veya nesne</span><span class="sxs-lookup"><span data-stu-id="c526f-280">String, Integer, Array, or Object</span></span> |<span data-ttu-id="c526f-281">Merhaba dizisinde ek değerler.</span><span class="sxs-lookup"><span data-stu-id="c526f-281">Additional values in hello array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c526f-282">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="c526f-282">Return value</span></span>

<span data-ttu-id="c526f-283">Bir dizi.</span><span class="sxs-lookup"><span data-stu-id="c526f-283">An array.</span></span>

### <a name="example"></a><span data-ttu-id="c526f-284">Örnek</span><span class="sxs-lookup"><span data-stu-id="c526f-284">Example</span></span>

<span data-ttu-id="c526f-285">örnekte gösterildiği nasıl aşağıdaki hello toouse createArray farklı türler ile:</span><span class="sxs-lookup"><span data-stu-id="c526f-285">hello following example shows how toouse createArray with different types:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringArray": {
            "type": "array",
            "value": "[createArray('a', 'b', 'c')]"
        },
        "intArray": {
            "type": "array",
            "value": "[createArray(1, 2, 3)]"
        },
        "objectArray": {
            "type": "array",
            "value": "[createArray(parameters('objectToTest'))]"
        },
        "arrayArray": {
            "type": "array",
            "value": "[createArray(parameters('arrayToTest'))]"
        }
    }
}
```

<span data-ttu-id="c526f-286">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="c526f-286">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c526f-287">Ad</span><span class="sxs-lookup"><span data-stu-id="c526f-287">Name</span></span> | <span data-ttu-id="c526f-288">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-288">Type</span></span> | <span data-ttu-id="c526f-289">Değer</span><span class="sxs-lookup"><span data-stu-id="c526f-289">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c526f-290">stringArray</span><span class="sxs-lookup"><span data-stu-id="c526f-290">stringArray</span></span> | <span data-ttu-id="c526f-291">Dizi</span><span class="sxs-lookup"><span data-stu-id="c526f-291">Array</span></span> | <span data-ttu-id="c526f-292">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="c526f-292">["a", "b", "c"]</span></span> |
| <span data-ttu-id="c526f-293">int</span><span class="sxs-lookup"><span data-stu-id="c526f-293">intArray</span></span> | <span data-ttu-id="c526f-294">Dizi</span><span class="sxs-lookup"><span data-stu-id="c526f-294">Array</span></span> | <span data-ttu-id="c526f-295">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="c526f-295">[1, 2, 3]</span></span> |
| <span data-ttu-id="c526f-296">objectArray</span><span class="sxs-lookup"><span data-stu-id="c526f-296">objectArray</span></span> | <span data-ttu-id="c526f-297">Dizi</span><span class="sxs-lookup"><span data-stu-id="c526f-297">Array</span></span> | <span data-ttu-id="c526f-298">[{"bir": "a", "iki": "b", "üç": "c"}]</span><span class="sxs-lookup"><span data-stu-id="c526f-298">[{"one": "a", "two": "b", "three": "c"}]</span></span> |
| <span data-ttu-id="c526f-299">arrayArray</span><span class="sxs-lookup"><span data-stu-id="c526f-299">arrayArray</span></span> | <span data-ttu-id="c526f-300">Dizi</span><span class="sxs-lookup"><span data-stu-id="c526f-300">Array</span></span> | <span data-ttu-id="c526f-301">[["bir", "iki", "üç"]]</span><span class="sxs-lookup"><span data-stu-id="c526f-301">[["one", "two", "three"]]</span></span> |

<a id="empty" />

## <a name="empty"></a><span data-ttu-id="c526f-302">boş</span><span class="sxs-lookup"><span data-stu-id="c526f-302">empty</span></span>

`empty(itemToTest)`

<span data-ttu-id="c526f-303">Bir dizi, nesne veya dize boş olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="c526f-303">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="c526f-304">Parametreler</span><span class="sxs-lookup"><span data-stu-id="c526f-304">Parameters</span></span>

| <span data-ttu-id="c526f-305">Parametre</span><span class="sxs-lookup"><span data-stu-id="c526f-305">Parameter</span></span> | <span data-ttu-id="c526f-306">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c526f-306">Required</span></span> | <span data-ttu-id="c526f-307">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-307">Type</span></span> | <span data-ttu-id="c526f-308">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c526f-308">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c526f-309">itemToTest</span><span class="sxs-lookup"><span data-stu-id="c526f-309">itemToTest</span></span> |<span data-ttu-id="c526f-310">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-310">Yes</span></span> |<span data-ttu-id="c526f-311">dizi, nesne veya dize</span><span class="sxs-lookup"><span data-stu-id="c526f-311">array, object, or string</span></span> |<span data-ttu-id="c526f-312">boş ise, değer toocheck hello.</span><span class="sxs-lookup"><span data-stu-id="c526f-312">hello value toocheck if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c526f-313">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="c526f-313">Return value</span></span>

<span data-ttu-id="c526f-314">Döndürür **True** hello değeriyse, boş, aksi takdirde **False**.</span><span class="sxs-lookup"><span data-stu-id="c526f-314">Returns **True** if hello value is empty; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="c526f-315">Örnek</span><span class="sxs-lookup"><span data-stu-id="c526f-315">Example</span></span>

<span data-ttu-id="c526f-316">Aşağıdaki örneğine hello bir dizi, nesne ve dize boş olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="c526f-316">hello following example checks whether an array, object, and string are empty.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": []
        },
        "testObject": {
            "type": "object",
            "defaultValue": {}
        },
        "testString": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testArray'))]"
        },
        "objectEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testObject'))]"
        },
        "stringEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="c526f-317">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="c526f-317">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c526f-318">Ad</span><span class="sxs-lookup"><span data-stu-id="c526f-318">Name</span></span> | <span data-ttu-id="c526f-319">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-319">Type</span></span> | <span data-ttu-id="c526f-320">Değer</span><span class="sxs-lookup"><span data-stu-id="c526f-320">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c526f-321">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="c526f-321">arrayEmpty</span></span> | <span data-ttu-id="c526f-322">bool</span><span class="sxs-lookup"><span data-stu-id="c526f-322">Bool</span></span> | <span data-ttu-id="c526f-323">True</span><span class="sxs-lookup"><span data-stu-id="c526f-323">True</span></span> |
| <span data-ttu-id="c526f-324">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="c526f-324">objectEmpty</span></span> | <span data-ttu-id="c526f-325">bool</span><span class="sxs-lookup"><span data-stu-id="c526f-325">Bool</span></span> | <span data-ttu-id="c526f-326">True</span><span class="sxs-lookup"><span data-stu-id="c526f-326">True</span></span> |
| <span data-ttu-id="c526f-327">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="c526f-327">stringEmpty</span></span> | <span data-ttu-id="c526f-328">bool</span><span class="sxs-lookup"><span data-stu-id="c526f-328">Bool</span></span> | <span data-ttu-id="c526f-329">True</span><span class="sxs-lookup"><span data-stu-id="c526f-329">True</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="c526f-330">ilk</span><span class="sxs-lookup"><span data-stu-id="c526f-330">first</span></span>
`first(arg1)`

<span data-ttu-id="c526f-331">Merhaba dizisinin ilk öğesi ya da hello dize ilk karakteri döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="c526f-331">Returns hello first element of hello array, or first character of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="c526f-332">Parametreler</span><span class="sxs-lookup"><span data-stu-id="c526f-332">Parameters</span></span>

| <span data-ttu-id="c526f-333">Parametre</span><span class="sxs-lookup"><span data-stu-id="c526f-333">Parameter</span></span> | <span data-ttu-id="c526f-334">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c526f-334">Required</span></span> | <span data-ttu-id="c526f-335">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-335">Type</span></span> | <span data-ttu-id="c526f-336">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c526f-336">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c526f-337">arg1</span><span class="sxs-lookup"><span data-stu-id="c526f-337">arg1</span></span> |<span data-ttu-id="c526f-338">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-338">Yes</span></span> |<span data-ttu-id="c526f-339">dizi veya dize</span><span class="sxs-lookup"><span data-stu-id="c526f-339">array or string</span></span> |<span data-ttu-id="c526f-340">Merhaba değeri tooretrieve hello ilk öğe veya karakter.</span><span class="sxs-lookup"><span data-stu-id="c526f-340">hello value tooretrieve hello first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c526f-341">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="c526f-341">Return value</span></span>

<span data-ttu-id="c526f-342">bir dizi ya da ilk karakteri bir dize hello hello ilk öğesinin Hello türü (dize, int, dizi veya nesne).</span><span class="sxs-lookup"><span data-stu-id="c526f-342">hello type (string, int, array, or object) of hello first element in an array, or hello first character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="c526f-343">Örnek</span><span class="sxs-lookup"><span data-stu-id="c526f-343">Example</span></span>

<span data-ttu-id="c526f-344">Merhaba aşağıdaki örnekte nasıl toouse hello ilk işlevi bir dizi ve dize ile gösterilir.</span><span class="sxs-lookup"><span data-stu-id="c526f-344">hello following example shows how toouse hello first function with an array and string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[first(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[first('One Two Three')]"
        }
    }
}
```

<span data-ttu-id="c526f-345">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="c526f-345">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c526f-346">Ad</span><span class="sxs-lookup"><span data-stu-id="c526f-346">Name</span></span> | <span data-ttu-id="c526f-347">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-347">Type</span></span> | <span data-ttu-id="c526f-348">Değer</span><span class="sxs-lookup"><span data-stu-id="c526f-348">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c526f-349">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-349">arrayOutput</span></span> | <span data-ttu-id="c526f-350">Dize</span><span class="sxs-lookup"><span data-stu-id="c526f-350">String</span></span> | <span data-ttu-id="c526f-351">bir</span><span class="sxs-lookup"><span data-stu-id="c526f-351">one</span></span> |
| <span data-ttu-id="c526f-352">stringOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-352">stringOutput</span></span> | <span data-ttu-id="c526f-353">Dize</span><span class="sxs-lookup"><span data-stu-id="c526f-353">String</span></span> | <span data-ttu-id="c526f-354">O</span><span class="sxs-lookup"><span data-stu-id="c526f-354">O</span></span> |

<a id="intersection" />

## <a name="intersection"></a><span data-ttu-id="c526f-355">kesişim</span><span class="sxs-lookup"><span data-stu-id="c526f-355">intersection</span></span>
`intersection(arg1, arg2, arg3, ...)`

<span data-ttu-id="c526f-356">Tek bir dizi veya nesne hello ortak öğeler ile Merhaba parametrelerinden döndürür.</span><span class="sxs-lookup"><span data-stu-id="c526f-356">Returns a single array or object with hello common elements from hello parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="c526f-357">Parametreler</span><span class="sxs-lookup"><span data-stu-id="c526f-357">Parameters</span></span>

| <span data-ttu-id="c526f-358">Parametre</span><span class="sxs-lookup"><span data-stu-id="c526f-358">Parameter</span></span> | <span data-ttu-id="c526f-359">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c526f-359">Required</span></span> | <span data-ttu-id="c526f-360">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-360">Type</span></span> | <span data-ttu-id="c526f-361">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c526f-361">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c526f-362">arg1</span><span class="sxs-lookup"><span data-stu-id="c526f-362">arg1</span></span> |<span data-ttu-id="c526f-363">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-363">Yes</span></span> |<span data-ttu-id="c526f-364">dizi veya nesne</span><span class="sxs-lookup"><span data-stu-id="c526f-364">array or object</span></span> |<span data-ttu-id="c526f-365">Ortak öğeler bulmak için ilk değer toouse hello.</span><span class="sxs-lookup"><span data-stu-id="c526f-365">hello first value toouse for finding common elements.</span></span> |
| <span data-ttu-id="c526f-366">arg2</span><span class="sxs-lookup"><span data-stu-id="c526f-366">arg2</span></span> |<span data-ttu-id="c526f-367">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-367">Yes</span></span> |<span data-ttu-id="c526f-368">dizi veya nesne</span><span class="sxs-lookup"><span data-stu-id="c526f-368">array or object</span></span> |<span data-ttu-id="c526f-369">Ortak öğeler bulmak için ikinci değer toouse hello.</span><span class="sxs-lookup"><span data-stu-id="c526f-369">hello second value toouse for finding common elements.</span></span> |
| <span data-ttu-id="c526f-370">Ek bağımsız değişkenler</span><span class="sxs-lookup"><span data-stu-id="c526f-370">additional arguments</span></span> |<span data-ttu-id="c526f-371">Hayır</span><span class="sxs-lookup"><span data-stu-id="c526f-371">No</span></span> |<span data-ttu-id="c526f-372">dizi veya nesne</span><span class="sxs-lookup"><span data-stu-id="c526f-372">array or object</span></span> |<span data-ttu-id="c526f-373">Ortak öğeler bulmak için ek değerler toouse.</span><span class="sxs-lookup"><span data-stu-id="c526f-373">Additional values toouse for finding common elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c526f-374">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="c526f-374">Return value</span></span>

<span data-ttu-id="c526f-375">Bir dizi veya nesne hello ortak öğeler ile.</span><span class="sxs-lookup"><span data-stu-id="c526f-375">An array or object with hello common elements.</span></span>

### <a name="example"></a><span data-ttu-id="c526f-376">Örnek</span><span class="sxs-lookup"><span data-stu-id="c526f-376">Example</span></span>

<span data-ttu-id="c526f-377">Aşağıdaki örnekte gösterildiği nasıl toouse kesişim diziler hello ve nesneler:</span><span class="sxs-lookup"><span data-stu-id="c526f-377">hello following example shows how toouse intersection with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "z", "three": "c"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[intersection(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[intersection(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="c526f-378">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="c526f-378">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c526f-379">Ad</span><span class="sxs-lookup"><span data-stu-id="c526f-379">Name</span></span> | <span data-ttu-id="c526f-380">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-380">Type</span></span> | <span data-ttu-id="c526f-381">Değer</span><span class="sxs-lookup"><span data-stu-id="c526f-381">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c526f-382">objectOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-382">objectOutput</span></span> | <span data-ttu-id="c526f-383">Nesne</span><span class="sxs-lookup"><span data-stu-id="c526f-383">Object</span></span> | <span data-ttu-id="c526f-384">{"bir": "a", "üç": "c"}</span><span class="sxs-lookup"><span data-stu-id="c526f-384">{"one": "a", "three": "c"}</span></span> |
| <span data-ttu-id="c526f-385">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-385">arrayOutput</span></span> | <span data-ttu-id="c526f-386">Dizi</span><span class="sxs-lookup"><span data-stu-id="c526f-386">Array</span></span> | <span data-ttu-id="c526f-387">["iki", "üç"]</span><span class="sxs-lookup"><span data-stu-id="c526f-387">["two", "three"]</span></span> |


## <a name="json"></a><span data-ttu-id="c526f-388">JSON</span><span class="sxs-lookup"><span data-stu-id="c526f-388">json</span></span>
`json(arg1)`

<span data-ttu-id="c526f-389">Bir JSON nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="c526f-389">Returns a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="c526f-390">Parametreler</span><span class="sxs-lookup"><span data-stu-id="c526f-390">Parameters</span></span>

| <span data-ttu-id="c526f-391">Parametre</span><span class="sxs-lookup"><span data-stu-id="c526f-391">Parameter</span></span> | <span data-ttu-id="c526f-392">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c526f-392">Required</span></span> | <span data-ttu-id="c526f-393">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-393">Type</span></span> | <span data-ttu-id="c526f-394">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c526f-394">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c526f-395">arg1</span><span class="sxs-lookup"><span data-stu-id="c526f-395">arg1</span></span> |<span data-ttu-id="c526f-396">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-396">Yes</span></span> |<span data-ttu-id="c526f-397">Dize</span><span class="sxs-lookup"><span data-stu-id="c526f-397">string</span></span> |<span data-ttu-id="c526f-398">Merhaba değeri tooconvert tooJSON.</span><span class="sxs-lookup"><span data-stu-id="c526f-398">hello value tooconvert tooJSON.</span></span> |


### <a name="return-value"></a><span data-ttu-id="c526f-399">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="c526f-399">Return value</span></span>

<span data-ttu-id="c526f-400">Merhaba Hello JSON nesnesinden belirtilen dize veya boş bir nesneyi zaman **null** belirtilir.</span><span class="sxs-lookup"><span data-stu-id="c526f-400">hello JSON object from hello specified string, or an empty object when **null** is specified.</span></span>

### <a name="example"></a><span data-ttu-id="c526f-401">Örnek</span><span class="sxs-lookup"><span data-stu-id="c526f-401">Example</span></span>

<span data-ttu-id="c526f-402">Aşağıdaki örnekte gösterildiği nasıl toouse kesişim diziler hello ve nesneler:</span><span class="sxs-lookup"><span data-stu-id="c526f-402">hello following example shows how toouse intersection with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "jsonOutput": {
            "type": "object",
            "value": "[json('{\"a\": \"b\"}')]"
        },
        "nullOutput": {
            "type": "bool",
            "value": "[empty(json('null'))]"
        }
    }
}
```

<span data-ttu-id="c526f-403">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="c526f-403">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c526f-404">Ad</span><span class="sxs-lookup"><span data-stu-id="c526f-404">Name</span></span> | <span data-ttu-id="c526f-405">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-405">Type</span></span> | <span data-ttu-id="c526f-406">Değer</span><span class="sxs-lookup"><span data-stu-id="c526f-406">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c526f-407">jsonOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-407">jsonOutput</span></span> | <span data-ttu-id="c526f-408">Nesne</span><span class="sxs-lookup"><span data-stu-id="c526f-408">Object</span></span> | <span data-ttu-id="c526f-409">{"a": "b"}</span><span class="sxs-lookup"><span data-stu-id="c526f-409">{"a": "b"}</span></span> |
| <span data-ttu-id="c526f-410">nullOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-410">nullOutput</span></span> | <span data-ttu-id="c526f-411">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="c526f-411">Boolean</span></span> | <span data-ttu-id="c526f-412">True</span><span class="sxs-lookup"><span data-stu-id="c526f-412">True</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="c526f-413">Son</span><span class="sxs-lookup"><span data-stu-id="c526f-413">last</span></span>
`last (arg1)`

<span data-ttu-id="c526f-414">Merhaba dizisinin son öğesi ya da hello dizenin son karakter döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="c526f-414">Returns hello last element of hello array, or last character of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="c526f-415">Parametreler</span><span class="sxs-lookup"><span data-stu-id="c526f-415">Parameters</span></span>

| <span data-ttu-id="c526f-416">Parametre</span><span class="sxs-lookup"><span data-stu-id="c526f-416">Parameter</span></span> | <span data-ttu-id="c526f-417">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c526f-417">Required</span></span> | <span data-ttu-id="c526f-418">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-418">Type</span></span> | <span data-ttu-id="c526f-419">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c526f-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c526f-420">arg1</span><span class="sxs-lookup"><span data-stu-id="c526f-420">arg1</span></span> |<span data-ttu-id="c526f-421">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-421">Yes</span></span> |<span data-ttu-id="c526f-422">dizi veya dize</span><span class="sxs-lookup"><span data-stu-id="c526f-422">array or string</span></span> |<span data-ttu-id="c526f-423">Merhaba değeri tooretrieve hello son öğesi veya karakter.</span><span class="sxs-lookup"><span data-stu-id="c526f-423">hello value tooretrieve hello last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c526f-424">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="c526f-424">Return value</span></span>

<span data-ttu-id="c526f-425">bir dizi ya da hello son karakter bir dizenin hello son öğesinin Hello türü (dize, int, dizi veya nesne).</span><span class="sxs-lookup"><span data-stu-id="c526f-425">hello type (string, int, array, or object) of hello last element in an array, or hello last character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="c526f-426">Örnek</span><span class="sxs-lookup"><span data-stu-id="c526f-426">Example</span></span>

<span data-ttu-id="c526f-427">Merhaba aşağıdaki örnekte nasıl toouse hello son işlevi bir dizi ve dize ile gösterilir.</span><span class="sxs-lookup"><span data-stu-id="c526f-427">hello following example shows how toouse hello last function with an array and string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[last(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[last('One Two Three')]"
        }
    }
}
```

<span data-ttu-id="c526f-428">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="c526f-428">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c526f-429">Ad</span><span class="sxs-lookup"><span data-stu-id="c526f-429">Name</span></span> | <span data-ttu-id="c526f-430">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-430">Type</span></span> | <span data-ttu-id="c526f-431">Değer</span><span class="sxs-lookup"><span data-stu-id="c526f-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c526f-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-432">arrayOutput</span></span> | <span data-ttu-id="c526f-433">Dize</span><span class="sxs-lookup"><span data-stu-id="c526f-433">String</span></span> | <span data-ttu-id="c526f-434">üç</span><span class="sxs-lookup"><span data-stu-id="c526f-434">three</span></span> |
| <span data-ttu-id="c526f-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-435">stringOutput</span></span> | <span data-ttu-id="c526f-436">Dize</span><span class="sxs-lookup"><span data-stu-id="c526f-436">String</span></span> | <span data-ttu-id="c526f-437">E</span><span class="sxs-lookup"><span data-stu-id="c526f-437">e</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="c526f-438">uzunluğu</span><span class="sxs-lookup"><span data-stu-id="c526f-438">length</span></span>
`length(arg1)`

<span data-ttu-id="c526f-439">Bir dizi ya da bir dizedeki karakter Hello sayıda öğeyi döndürür.</span><span class="sxs-lookup"><span data-stu-id="c526f-439">Returns hello number of elements in an array, or characters in a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="c526f-440">Parametreler</span><span class="sxs-lookup"><span data-stu-id="c526f-440">Parameters</span></span>

| <span data-ttu-id="c526f-441">Parametre</span><span class="sxs-lookup"><span data-stu-id="c526f-441">Parameter</span></span> | <span data-ttu-id="c526f-442">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c526f-442">Required</span></span> | <span data-ttu-id="c526f-443">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-443">Type</span></span> | <span data-ttu-id="c526f-444">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c526f-444">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c526f-445">arg1</span><span class="sxs-lookup"><span data-stu-id="c526f-445">arg1</span></span> |<span data-ttu-id="c526f-446">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-446">Yes</span></span> |<span data-ttu-id="c526f-447">dizi veya dize</span><span class="sxs-lookup"><span data-stu-id="c526f-447">array or string</span></span> |<span data-ttu-id="c526f-448">öğe sayısını hello alma dizi toouse hello veya karakter sayısını hello alma dizesi toouse hello.</span><span class="sxs-lookup"><span data-stu-id="c526f-448">hello array toouse for getting hello number of elements, or hello string toouse for getting hello number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c526f-449">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="c526f-449">Return value</span></span>

<span data-ttu-id="c526f-450">İnt</span><span class="sxs-lookup"><span data-stu-id="c526f-450">An int.</span></span> 

### <a name="example"></a><span data-ttu-id="c526f-451">Örnek</span><span class="sxs-lookup"><span data-stu-id="c526f-451">Example</span></span>

<span data-ttu-id="c526f-452">örnekte gösterildiği nasıl aşağıdaki hello toouse uzunluğunda bir dizi ve dizesi:</span><span class="sxs-lookup"><span data-stu-id="c526f-452">hello following example shows how toouse length with an array and string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "stringToTest": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "arrayLength": {
            "type": "int",
            "value": "[length(parameters('arrayToTest'))]"
        },
        "stringLength": {
            "type": "int",
            "value": "[length(parameters('stringToTest'))]"
        }
    }
}
```

<span data-ttu-id="c526f-453">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="c526f-453">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c526f-454">Ad</span><span class="sxs-lookup"><span data-stu-id="c526f-454">Name</span></span> | <span data-ttu-id="c526f-455">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-455">Type</span></span> | <span data-ttu-id="c526f-456">Değer</span><span class="sxs-lookup"><span data-stu-id="c526f-456">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c526f-457">arrayLength</span><span class="sxs-lookup"><span data-stu-id="c526f-457">arrayLength</span></span> | <span data-ttu-id="c526f-458">Int</span><span class="sxs-lookup"><span data-stu-id="c526f-458">Int</span></span> | <span data-ttu-id="c526f-459">3</span><span class="sxs-lookup"><span data-stu-id="c526f-459">3</span></span> |
| <span data-ttu-id="c526f-460">stringLength</span><span class="sxs-lookup"><span data-stu-id="c526f-460">stringLength</span></span> | <span data-ttu-id="c526f-461">Int</span><span class="sxs-lookup"><span data-stu-id="c526f-461">Int</span></span> | <span data-ttu-id="c526f-462">13</span><span class="sxs-lookup"><span data-stu-id="c526f-462">13</span></span> |

<span data-ttu-id="c526f-463">Kaynakları oluşturulurken bir dizi toospecify hello yineleme sayısı ile bu işlevi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c526f-463">You can use this function with an array toospecify hello number of iterations when creating resources.</span></span> <span data-ttu-id="c526f-464">Aşağıdaki örneğine hello parametre hello **siteNames** adları toouse tooan dizisi hello web siteleri oluştururken başvurur.</span><span class="sxs-lookup"><span data-stu-id="c526f-464">In hello following example, hello parameter **siteNames** would refer tooan array of names toouse when creating hello web sites.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

<span data-ttu-id="c526f-465">Bu işlev bir dizi ile kullanma hakkında daha fazla bilgi için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="c526f-465">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<a id="min" />

## <a name="min"></a><span data-ttu-id="c526f-466">dk</span><span class="sxs-lookup"><span data-stu-id="c526f-466">min</span></span>
`min(arg1)`

<span data-ttu-id="c526f-467">Döndürür dizisi veya virgülle ayrılmış tamsayı listesi en düşük değerden hello.</span><span class="sxs-lookup"><span data-stu-id="c526f-467">Returns hello minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="c526f-468">Parametreler</span><span class="sxs-lookup"><span data-stu-id="c526f-468">Parameters</span></span>

| <span data-ttu-id="c526f-469">Parametre</span><span class="sxs-lookup"><span data-stu-id="c526f-469">Parameter</span></span> | <span data-ttu-id="c526f-470">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c526f-470">Required</span></span> | <span data-ttu-id="c526f-471">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-471">Type</span></span> | <span data-ttu-id="c526f-472">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c526f-472">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c526f-473">arg1</span><span class="sxs-lookup"><span data-stu-id="c526f-473">arg1</span></span> |<span data-ttu-id="c526f-474">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-474">Yes</span></span> |<span data-ttu-id="c526f-475">dizi tamsayı veya virgülle ayrılmış tamsayı listesi</span><span class="sxs-lookup"><span data-stu-id="c526f-475">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="c526f-476">Merhaba koleksiyonu tooget hello en küçük değer.</span><span class="sxs-lookup"><span data-stu-id="c526f-476">hello collection tooget hello minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c526f-477">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="c526f-477">Return value</span></span>

<span data-ttu-id="c526f-478">Merhaba en düşük değeri temsil eden bir tamsayı.</span><span class="sxs-lookup"><span data-stu-id="c526f-478">An int representing hello minimum value.</span></span>

### <a name="example"></a><span data-ttu-id="c526f-479">Örnek</span><span class="sxs-lookup"><span data-stu-id="c526f-479">Example</span></span>

<span data-ttu-id="c526f-480">örnekte gösterildiği nasıl aşağıdaki hello toouse en az bir dizi ve tamsayı listesi:</span><span class="sxs-lookup"><span data-stu-id="c526f-480">hello following example shows how toouse min with an array and a list of integers:</span></span>

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

<span data-ttu-id="c526f-481">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="c526f-481">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c526f-482">Ad</span><span class="sxs-lookup"><span data-stu-id="c526f-482">Name</span></span> | <span data-ttu-id="c526f-483">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-483">Type</span></span> | <span data-ttu-id="c526f-484">Değer</span><span class="sxs-lookup"><span data-stu-id="c526f-484">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c526f-485">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-485">arrayOutput</span></span> | <span data-ttu-id="c526f-486">Int</span><span class="sxs-lookup"><span data-stu-id="c526f-486">Int</span></span> | <span data-ttu-id="c526f-487">0</span><span class="sxs-lookup"><span data-stu-id="c526f-487">0</span></span> |
| <span data-ttu-id="c526f-488">intOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-488">intOutput</span></span> | <span data-ttu-id="c526f-489">Int</span><span class="sxs-lookup"><span data-stu-id="c526f-489">Int</span></span> | <span data-ttu-id="c526f-490">0</span><span class="sxs-lookup"><span data-stu-id="c526f-490">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="c526f-491">max</span><span class="sxs-lookup"><span data-stu-id="c526f-491">max</span></span>
`max(arg1)`

<span data-ttu-id="c526f-492">En büyük değer dizisi veya virgülle ayrılmış tamsayı listesi döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="c526f-492">Returns hello maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="c526f-493">Parametreler</span><span class="sxs-lookup"><span data-stu-id="c526f-493">Parameters</span></span>

| <span data-ttu-id="c526f-494">Parametre</span><span class="sxs-lookup"><span data-stu-id="c526f-494">Parameter</span></span> | <span data-ttu-id="c526f-495">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c526f-495">Required</span></span> | <span data-ttu-id="c526f-496">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-496">Type</span></span> | <span data-ttu-id="c526f-497">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c526f-497">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c526f-498">arg1</span><span class="sxs-lookup"><span data-stu-id="c526f-498">arg1</span></span> |<span data-ttu-id="c526f-499">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-499">Yes</span></span> |<span data-ttu-id="c526f-500">dizi tamsayı veya virgülle ayrılmış tamsayı listesi</span><span class="sxs-lookup"><span data-stu-id="c526f-500">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="c526f-501">Merhaba koleksiyonu tooget hello en büyük değer.</span><span class="sxs-lookup"><span data-stu-id="c526f-501">hello collection tooget hello maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c526f-502">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="c526f-502">Return value</span></span>

<span data-ttu-id="c526f-503">Merhaba en yüksek değeri temsil eden bir tamsayı.</span><span class="sxs-lookup"><span data-stu-id="c526f-503">An int representing hello maximum value.</span></span>

### <a name="example"></a><span data-ttu-id="c526f-504">Örnek</span><span class="sxs-lookup"><span data-stu-id="c526f-504">Example</span></span>

<span data-ttu-id="c526f-505">örnekte gösterildiği nasıl aşağıdaki hello toouse bir dizi ve tamsayı listesi ile en fazla:</span><span class="sxs-lookup"><span data-stu-id="c526f-505">hello following example shows how toouse max with an array and a list of integers:</span></span>

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

<span data-ttu-id="c526f-506">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="c526f-506">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c526f-507">Ad</span><span class="sxs-lookup"><span data-stu-id="c526f-507">Name</span></span> | <span data-ttu-id="c526f-508">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-508">Type</span></span> | <span data-ttu-id="c526f-509">Değer</span><span class="sxs-lookup"><span data-stu-id="c526f-509">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c526f-510">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-510">arrayOutput</span></span> | <span data-ttu-id="c526f-511">Int</span><span class="sxs-lookup"><span data-stu-id="c526f-511">Int</span></span> | <span data-ttu-id="c526f-512">5</span><span class="sxs-lookup"><span data-stu-id="c526f-512">5</span></span> |
| <span data-ttu-id="c526f-513">intOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-513">intOutput</span></span> | <span data-ttu-id="c526f-514">Int</span><span class="sxs-lookup"><span data-stu-id="c526f-514">Int</span></span> | <span data-ttu-id="c526f-515">5</span><span class="sxs-lookup"><span data-stu-id="c526f-515">5</span></span> |

<a id="range" />

## <a name="range"></a><span data-ttu-id="c526f-516">Aralık</span><span class="sxs-lookup"><span data-stu-id="c526f-516">range</span></span>
`range(startingInteger, numberOfElements)`

<span data-ttu-id="c526f-517">Dizisi bir tamsayı başlatma ve bir öğe sayısı içeren oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c526f-517">Creates an array of integers from a starting integer and containing a number of items.</span></span>

### <a name="parameters"></a><span data-ttu-id="c526f-518">Parametreler</span><span class="sxs-lookup"><span data-stu-id="c526f-518">Parameters</span></span>

| <span data-ttu-id="c526f-519">Parametre</span><span class="sxs-lookup"><span data-stu-id="c526f-519">Parameter</span></span> | <span data-ttu-id="c526f-520">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c526f-520">Required</span></span> | <span data-ttu-id="c526f-521">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-521">Type</span></span> | <span data-ttu-id="c526f-522">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c526f-522">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c526f-523">startingInteger</span><span class="sxs-lookup"><span data-stu-id="c526f-523">startingInteger</span></span> |<span data-ttu-id="c526f-524">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-524">Yes</span></span> |<span data-ttu-id="c526f-525">Int</span><span class="sxs-lookup"><span data-stu-id="c526f-525">int</span></span> |<span data-ttu-id="c526f-526">Merhaba hello dizinin ilk tamsayı.</span><span class="sxs-lookup"><span data-stu-id="c526f-526">hello first integer in hello array.</span></span> |
| <span data-ttu-id="c526f-527">numberofElements</span><span class="sxs-lookup"><span data-stu-id="c526f-527">numberofElements</span></span> |<span data-ttu-id="c526f-528">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-528">Yes</span></span> |<span data-ttu-id="c526f-529">Int</span><span class="sxs-lookup"><span data-stu-id="c526f-529">int</span></span> |<span data-ttu-id="c526f-530">Merhaba tamsayılar hello dizisindeki sayısı.</span><span class="sxs-lookup"><span data-stu-id="c526f-530">hello number of integers in hello array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c526f-531">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="c526f-531">Return value</span></span>

<span data-ttu-id="c526f-532">Dizisi.</span><span class="sxs-lookup"><span data-stu-id="c526f-532">An array of integers.</span></span>

### <a name="example"></a><span data-ttu-id="c526f-533">Örnek</span><span class="sxs-lookup"><span data-stu-id="c526f-533">Example</span></span>

<span data-ttu-id="c526f-534">Aşağıdaki örnek hello nasıl toouse hello aralığı işlevi gösterir:</span><span class="sxs-lookup"><span data-stu-id="c526f-534">hello following example shows how toouse hello range function:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "startingInt": {
            "type": "int",
            "defaultValue": 5
        },
        "numberOfElements": {
            "type": "int",
            "defaultValue": 3
        }
    },
    "resources": [],
    "outputs": {
        "rangeOutput": {
            "type": "array",
            "value": "[range(parameters('startingInt'),parameters('numberOfElements'))]"
        }
    }
}
```

<span data-ttu-id="c526f-535">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="c526f-535">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c526f-536">Ad</span><span class="sxs-lookup"><span data-stu-id="c526f-536">Name</span></span> | <span data-ttu-id="c526f-537">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-537">Type</span></span> | <span data-ttu-id="c526f-538">Değer</span><span class="sxs-lookup"><span data-stu-id="c526f-538">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c526f-539">rangeOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-539">rangeOutput</span></span> | <span data-ttu-id="c526f-540">Dizi</span><span class="sxs-lookup"><span data-stu-id="c526f-540">Array</span></span> | <span data-ttu-id="c526f-541">[5, 6, 7]</span><span class="sxs-lookup"><span data-stu-id="c526f-541">[5, 6, 7]</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="c526f-542">Atla</span><span class="sxs-lookup"><span data-stu-id="c526f-542">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="c526f-543">Merhaba numarası hello dizisinde belirtilen veya hello numarası hello dizesinde belirtilen sonra tüm hello karakterler içeren bir dize döndürür sonra tüm hello öğelerine sahip bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="c526f-543">Returns an array with all hello elements after hello specified number in hello array, or returns a string with all hello characters after hello specified number in hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="c526f-544">Parametreler</span><span class="sxs-lookup"><span data-stu-id="c526f-544">Parameters</span></span>

| <span data-ttu-id="c526f-545">Parametre</span><span class="sxs-lookup"><span data-stu-id="c526f-545">Parameter</span></span> | <span data-ttu-id="c526f-546">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c526f-546">Required</span></span> | <span data-ttu-id="c526f-547">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-547">Type</span></span> | <span data-ttu-id="c526f-548">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c526f-548">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c526f-549">originalValue</span><span class="sxs-lookup"><span data-stu-id="c526f-549">originalValue</span></span> |<span data-ttu-id="c526f-550">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-550">Yes</span></span> |<span data-ttu-id="c526f-551">dizi veya dize</span><span class="sxs-lookup"><span data-stu-id="c526f-551">array or string</span></span> |<span data-ttu-id="c526f-552">atlanıyor hello dizisi veya dize toouse.</span><span class="sxs-lookup"><span data-stu-id="c526f-552">hello array or string toouse for skipping.</span></span> |
| <span data-ttu-id="c526f-553">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="c526f-553">numberToSkip</span></span> |<span data-ttu-id="c526f-554">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-554">Yes</span></span> |<span data-ttu-id="c526f-555">Int</span><span class="sxs-lookup"><span data-stu-id="c526f-555">int</span></span> |<span data-ttu-id="c526f-556">öğeleri veya karakter tooskip Hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="c526f-556">hello number of elements or characters tooskip.</span></span> <span data-ttu-id="c526f-557">Bu değer 0 veya daha az ise, tüm öğeleri hello veya karakter hello değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="c526f-557">If this value is 0 or less, all hello elements or characters in hello value are returned.</span></span> <span data-ttu-id="c526f-558">Merhaba dizisi veya dize hello uzunluğundan büyük olursa, boş dize veya dize döndürülür.</span><span class="sxs-lookup"><span data-stu-id="c526f-558">If it is larger than hello length of hello array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c526f-559">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="c526f-559">Return value</span></span>

<span data-ttu-id="c526f-560">Bir dizi veya dize.</span><span class="sxs-lookup"><span data-stu-id="c526f-560">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="c526f-561">Örnek</span><span class="sxs-lookup"><span data-stu-id="c526f-561">Example</span></span>

<span data-ttu-id="c526f-562">Örnek atlar hello aşağıdaki hello hello dizide öğe sayısını belirtilen ve hello bir dizedeki karakter sayısını belirtilen.</span><span class="sxs-lookup"><span data-stu-id="c526f-562">hello following example skips hello specified number of elements in hello array, and hello specified number of characters in a string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToSkip": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToSkip": {
            "type": "int",
            "defaultValue": 4
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[skip(parameters('testArray'),parameters('elementsToSkip'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[skip(parameters('testString'),parameters('charactersToSkip'))]"
        }
    }
}
```

<span data-ttu-id="c526f-563">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="c526f-563">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c526f-564">Ad</span><span class="sxs-lookup"><span data-stu-id="c526f-564">Name</span></span> | <span data-ttu-id="c526f-565">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-565">Type</span></span> | <span data-ttu-id="c526f-566">Değer</span><span class="sxs-lookup"><span data-stu-id="c526f-566">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c526f-567">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-567">arrayOutput</span></span> | <span data-ttu-id="c526f-568">Dizi</span><span class="sxs-lookup"><span data-stu-id="c526f-568">Array</span></span> | <span data-ttu-id="c526f-569">["üç"]</span><span class="sxs-lookup"><span data-stu-id="c526f-569">["three"]</span></span> |
| <span data-ttu-id="c526f-570">stringOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-570">stringOutput</span></span> | <span data-ttu-id="c526f-571">Dize</span><span class="sxs-lookup"><span data-stu-id="c526f-571">String</span></span> | <span data-ttu-id="c526f-572">iki üç</span><span class="sxs-lookup"><span data-stu-id="c526f-572">two three</span></span> |

<a id="take" />

## <a name="take"></a><span data-ttu-id="c526f-573">Al</span><span class="sxs-lookup"><span data-stu-id="c526f-573">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="c526f-574">Merhaba sahip bir dizi öğelerinden sayısı belirtilen döndürür hello dizi başlangıcı hello veya hello başlangıcından hello dize olan karakter sayısı hello bir dizeyle belirtilen.</span><span class="sxs-lookup"><span data-stu-id="c526f-574">Returns an array with hello specified number of elements from hello start of hello array, or a string with hello specified number of characters from hello start of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="c526f-575">Parametreler</span><span class="sxs-lookup"><span data-stu-id="c526f-575">Parameters</span></span>

| <span data-ttu-id="c526f-576">Parametre</span><span class="sxs-lookup"><span data-stu-id="c526f-576">Parameter</span></span> | <span data-ttu-id="c526f-577">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c526f-577">Required</span></span> | <span data-ttu-id="c526f-578">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-578">Type</span></span> | <span data-ttu-id="c526f-579">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c526f-579">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c526f-580">originalValue</span><span class="sxs-lookup"><span data-stu-id="c526f-580">originalValue</span></span> |<span data-ttu-id="c526f-581">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-581">Yes</span></span> |<span data-ttu-id="c526f-582">dizi veya dize</span><span class="sxs-lookup"><span data-stu-id="c526f-582">array or string</span></span> |<span data-ttu-id="c526f-583">dizi veya dize tootake hello öğelerinden hello.</span><span class="sxs-lookup"><span data-stu-id="c526f-583">hello array or string tootake hello elements from.</span></span> |
| <span data-ttu-id="c526f-584">numberToTake</span><span class="sxs-lookup"><span data-stu-id="c526f-584">numberToTake</span></span> |<span data-ttu-id="c526f-585">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-585">Yes</span></span> |<span data-ttu-id="c526f-586">Int</span><span class="sxs-lookup"><span data-stu-id="c526f-586">int</span></span> |<span data-ttu-id="c526f-587">öğeleri veya karakter tootake Hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="c526f-587">hello number of elements or characters tootake.</span></span> <span data-ttu-id="c526f-588">Bu değer 0 veya daha az ise, boş dize veya dize döndürülür.</span><span class="sxs-lookup"><span data-stu-id="c526f-588">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="c526f-589">Merhaba hello verilen dizi veya dize uzunluğundan büyük olursa, hello dizisi veya dize tüm hello öğeler döndürülür.</span><span class="sxs-lookup"><span data-stu-id="c526f-589">If it is larger than hello length of hello given array or string, all hello elements in hello array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c526f-590">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="c526f-590">Return value</span></span>

<span data-ttu-id="c526f-591">Bir dizi veya dize.</span><span class="sxs-lookup"><span data-stu-id="c526f-591">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="c526f-592">Örnek</span><span class="sxs-lookup"><span data-stu-id="c526f-592">Example</span></span>

<span data-ttu-id="c526f-593">Örnek alır hello aşağıdaki hello hello dizisinden öğeleri ve bir dizeden karakterleri sayısı belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="c526f-593">hello following example takes hello specified number of elements from hello array, and characters from a string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToTake": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToTake": {
            "type": "int",
            "defaultValue": 2
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[take(parameters('testArray'),parameters('elementsToTake'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[take(parameters('testString'),parameters('charactersToTake'))]"
        }
    }
}
```

<span data-ttu-id="c526f-594">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="c526f-594">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c526f-595">Ad</span><span class="sxs-lookup"><span data-stu-id="c526f-595">Name</span></span> | <span data-ttu-id="c526f-596">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-596">Type</span></span> | <span data-ttu-id="c526f-597">Değer</span><span class="sxs-lookup"><span data-stu-id="c526f-597">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c526f-598">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-598">arrayOutput</span></span> | <span data-ttu-id="c526f-599">Dizi</span><span class="sxs-lookup"><span data-stu-id="c526f-599">Array</span></span> | <span data-ttu-id="c526f-600">["", "iki"]</span><span class="sxs-lookup"><span data-stu-id="c526f-600">["one", "two"]</span></span> |
| <span data-ttu-id="c526f-601">stringOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-601">stringOutput</span></span> | <span data-ttu-id="c526f-602">Dize</span><span class="sxs-lookup"><span data-stu-id="c526f-602">String</span></span> | <span data-ttu-id="c526f-603">üzerinde</span><span class="sxs-lookup"><span data-stu-id="c526f-603">on</span></span> |

<a id="union" />

## <a name="union"></a><span data-ttu-id="c526f-604">birleşim</span><span class="sxs-lookup"><span data-stu-id="c526f-604">union</span></span>
`union(arg1, arg2, arg3, ...)`

<span data-ttu-id="c526f-605">Tek bir dizi veya nesne tüm öğelerle hello parametrelerinden döndürür.</span><span class="sxs-lookup"><span data-stu-id="c526f-605">Returns a single array or object with all elements from hello parameters.</span></span> <span data-ttu-id="c526f-606">Yinelenen değerler veya anahtarlar, yalnızca bir kez dahil.</span><span class="sxs-lookup"><span data-stu-id="c526f-606">Duplicate values or keys are only included once.</span></span>

### <a name="parameters"></a><span data-ttu-id="c526f-607">Parametreler</span><span class="sxs-lookup"><span data-stu-id="c526f-607">Parameters</span></span>

| <span data-ttu-id="c526f-608">Parametre</span><span class="sxs-lookup"><span data-stu-id="c526f-608">Parameter</span></span> | <span data-ttu-id="c526f-609">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c526f-609">Required</span></span> | <span data-ttu-id="c526f-610">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-610">Type</span></span> | <span data-ttu-id="c526f-611">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c526f-611">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c526f-612">arg1</span><span class="sxs-lookup"><span data-stu-id="c526f-612">arg1</span></span> |<span data-ttu-id="c526f-613">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-613">Yes</span></span> |<span data-ttu-id="c526f-614">dizi veya nesne</span><span class="sxs-lookup"><span data-stu-id="c526f-614">array or object</span></span> |<span data-ttu-id="c526f-615">öğeleri katılmak için ilk değer toouse hello.</span><span class="sxs-lookup"><span data-stu-id="c526f-615">hello first value toouse for joining elements.</span></span> |
| <span data-ttu-id="c526f-616">arg2</span><span class="sxs-lookup"><span data-stu-id="c526f-616">arg2</span></span> |<span data-ttu-id="c526f-617">Evet</span><span class="sxs-lookup"><span data-stu-id="c526f-617">Yes</span></span> |<span data-ttu-id="c526f-618">dizi veya nesne</span><span class="sxs-lookup"><span data-stu-id="c526f-618">array or object</span></span> |<span data-ttu-id="c526f-619">öğeleri katılmak için ikinci değer toouse hello.</span><span class="sxs-lookup"><span data-stu-id="c526f-619">hello second value toouse for joining elements.</span></span> |
| <span data-ttu-id="c526f-620">Ek bağımsız değişkenler</span><span class="sxs-lookup"><span data-stu-id="c526f-620">additional arguments</span></span> |<span data-ttu-id="c526f-621">Hayır</span><span class="sxs-lookup"><span data-stu-id="c526f-621">No</span></span> |<span data-ttu-id="c526f-622">dizi veya nesne</span><span class="sxs-lookup"><span data-stu-id="c526f-622">array or object</span></span> |<span data-ttu-id="c526f-623">Öğeleri katılmak için ek değerler toouse.</span><span class="sxs-lookup"><span data-stu-id="c526f-623">Additional values toouse for joining elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c526f-624">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="c526f-624">Return value</span></span>

<span data-ttu-id="c526f-625">Bir dizi veya nesne.</span><span class="sxs-lookup"><span data-stu-id="c526f-625">An array or object.</span></span>

### <a name="example"></a><span data-ttu-id="c526f-626">Örnek</span><span class="sxs-lookup"><span data-stu-id="c526f-626">Example</span></span>

<span data-ttu-id="c526f-627">Aşağıdaki örnekte gösterildiği nasıl toouse birleşim diziler hello ve nesneler:</span><span class="sxs-lookup"><span data-stu-id="c526f-627">hello following example shows how toouse union with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"three": "c", "four": "d", "five": "e"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["three", "four"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[union(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[union(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="c526f-628">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="c526f-628">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c526f-629">Ad</span><span class="sxs-lookup"><span data-stu-id="c526f-629">Name</span></span> | <span data-ttu-id="c526f-630">Tür</span><span class="sxs-lookup"><span data-stu-id="c526f-630">Type</span></span> | <span data-ttu-id="c526f-631">Değer</span><span class="sxs-lookup"><span data-stu-id="c526f-631">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c526f-632">objectOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-632">objectOutput</span></span> | <span data-ttu-id="c526f-633">Nesne</span><span class="sxs-lookup"><span data-stu-id="c526f-633">Object</span></span> | <span data-ttu-id="c526f-634">{"bir": "a", "iki": "b", "üç": "c", "dört": "d", "beş": "e"}</span><span class="sxs-lookup"><span data-stu-id="c526f-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span></span> |
| <span data-ttu-id="c526f-635">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c526f-635">arrayOutput</span></span> | <span data-ttu-id="c526f-636">Dizi</span><span class="sxs-lookup"><span data-stu-id="c526f-636">Array</span></span> | <span data-ttu-id="c526f-637">["bir", "iki", "üç", "dört"]</span><span class="sxs-lookup"><span data-stu-id="c526f-637">["one", "two", "three", "four"]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c526f-638">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c526f-638">Next steps</span></span>
* <span data-ttu-id="c526f-639">Bir Azure Resource Manager şablonu hello bölümlerde açıklaması için bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c526f-639">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="c526f-640">birden fazla şablon toomerge bkz [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c526f-640">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="c526f-641">tooiterate belirtilen sayıda kaynak türünü oluştururken bkz [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="c526f-641">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="c526f-642">toodeploy hello şablonu oluşturduğunuz toosee bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c526f-642">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

