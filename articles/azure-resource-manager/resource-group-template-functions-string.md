---
title: "Azure Resource Manager şablonu işlevleri - dize | Microsoft Docs"
description: "Dizelerle çalışmak için bir Azure Resource Manager şablonunda kullanmak için işlevleri açıklanmaktadır."
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
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: 3e5c9ca546629f782a3d722b49f5fbaf5147e823
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="285a0-103">Azure Resource Manager şablonları için dize işlevleri</span><span class="sxs-lookup"><span data-stu-id="285a0-103">String functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="285a0-104">Resource Manager dizelerle çalışmak için aşağıdaki işlevleri sunar:</span><span class="sxs-lookup"><span data-stu-id="285a0-104">Resource Manager provides the following functions for working with strings:</span></span>

* [<span data-ttu-id="285a0-105">Base64</span><span class="sxs-lookup"><span data-stu-id="285a0-105">base64</span></span>](#base64)
* [<span data-ttu-id="285a0-106">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="285a0-106">base64ToJson</span></span>](#base64tojson)
* [<span data-ttu-id="285a0-107">base64ToString</span><span class="sxs-lookup"><span data-stu-id="285a0-107">base64ToString</span></span>](#base64tostring)
* [<span data-ttu-id="285a0-108">concat</span><span class="sxs-lookup"><span data-stu-id="285a0-108">concat</span></span>](#concat)
* [<span data-ttu-id="285a0-109">içerir</span><span class="sxs-lookup"><span data-stu-id="285a0-109">contains</span></span>](#contains)
* [<span data-ttu-id="285a0-110">dataUri</span><span class="sxs-lookup"><span data-stu-id="285a0-110">dataUri</span></span>](#datauri)
* [<span data-ttu-id="285a0-111">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="285a0-111">dataUriToString</span></span>](#datauritostring)
* [<span data-ttu-id="285a0-112">boş</span><span class="sxs-lookup"><span data-stu-id="285a0-112">empty</span></span>](#empty)
* [<span data-ttu-id="285a0-113">endsWith</span><span class="sxs-lookup"><span data-stu-id="285a0-113">endsWith</span></span>](#endswith)
* [<span data-ttu-id="285a0-114">ilk</span><span class="sxs-lookup"><span data-stu-id="285a0-114">first</span></span>](#first)
* [<span data-ttu-id="285a0-115">IndexOf</span><span class="sxs-lookup"><span data-stu-id="285a0-115">indexOf</span></span>](#indexof)
* [<span data-ttu-id="285a0-116">Son</span><span class="sxs-lookup"><span data-stu-id="285a0-116">last</span></span>](#last)
* [<span data-ttu-id="285a0-117">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="285a0-117">lastIndexOf</span></span>](#lastindexof)
* [<span data-ttu-id="285a0-118">uzunluğu</span><span class="sxs-lookup"><span data-stu-id="285a0-118">length</span></span>](#length)
* [<span data-ttu-id="285a0-119">padLeft</span><span class="sxs-lookup"><span data-stu-id="285a0-119">padLeft</span></span>](#padleft)
* [<span data-ttu-id="285a0-120">Değiştir</span><span class="sxs-lookup"><span data-stu-id="285a0-120">replace</span></span>](#replace)
* [<span data-ttu-id="285a0-121">Atla</span><span class="sxs-lookup"><span data-stu-id="285a0-121">skip</span></span>](#skip)
* [<span data-ttu-id="285a0-122">split</span><span class="sxs-lookup"><span data-stu-id="285a0-122">split</span></span>](#split)
* [<span data-ttu-id="285a0-123">startsWith</span><span class="sxs-lookup"><span data-stu-id="285a0-123">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="285a0-124">dize</span><span class="sxs-lookup"><span data-stu-id="285a0-124">string</span></span>](#string)
* [<span data-ttu-id="285a0-125">substring</span><span class="sxs-lookup"><span data-stu-id="285a0-125">substring</span></span>](#substring)
* [<span data-ttu-id="285a0-126">Al</span><span class="sxs-lookup"><span data-stu-id="285a0-126">take</span></span>](#take)
* [<span data-ttu-id="285a0-127">toLower</span><span class="sxs-lookup"><span data-stu-id="285a0-127">toLower</span></span>](#tolower)
* [<span data-ttu-id="285a0-128">toUpper</span><span class="sxs-lookup"><span data-stu-id="285a0-128">toUpper</span></span>](#toupper)
* [<span data-ttu-id="285a0-129">Kırpma</span><span class="sxs-lookup"><span data-stu-id="285a0-129">trim</span></span>](#trim)
* [<span data-ttu-id="285a0-130">uniqueString</span><span class="sxs-lookup"><span data-stu-id="285a0-130">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="285a0-131">URI</span><span class="sxs-lookup"><span data-stu-id="285a0-131">uri</span></span>](#uri)
* [<span data-ttu-id="285a0-132">uriComponent</span><span class="sxs-lookup"><span data-stu-id="285a0-132">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="285a0-133">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="285a0-133">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a><span data-ttu-id="285a0-134">Base64</span><span class="sxs-lookup"><span data-stu-id="285a0-134">base64</span></span>
`base64(inputString)`

<span data-ttu-id="285a0-135">Giriş dizesi base64 gösterimini döndürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-135">Returns the base64 representation of the input string.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-136">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-136">Parameters</span></span>

| <span data-ttu-id="285a0-137">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-137">Parameter</span></span> | <span data-ttu-id="285a0-138">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-138">Required</span></span> | <span data-ttu-id="285a0-139">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-139">Type</span></span> | <span data-ttu-id="285a0-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-140">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-141">inputString</span><span class="sxs-lookup"><span data-stu-id="285a0-141">inputString</span></span> |<span data-ttu-id="285a0-142">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-142">Yes</span></span> |<span data-ttu-id="285a0-143">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-143">string</span></span> |<span data-ttu-id="285a0-144">Bir base64 gösterimi olarak döndürülecek değer.</span><span class="sxs-lookup"><span data-stu-id="285a0-144">The value to return as a base64 representation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-145">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-145">Return value</span></span>

<span data-ttu-id="285a0-146">Base64 gösterimini içeren bir dize.</span><span class="sxs-lookup"><span data-stu-id="285a0-146">A string containing the base64 representation.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-147">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-147">Examples</span></span>

<span data-ttu-id="285a0-148">Aşağıdaki örnek, base64 işlevinin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="285a0-148">The following example shows how to use the base64 function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="285a0-149">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-149">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-150">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-150">Name</span></span> | <span data-ttu-id="285a0-151">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-151">Type</span></span> | <span data-ttu-id="285a0-152">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-153">base64Output</span><span class="sxs-lookup"><span data-stu-id="285a0-153">base64Output</span></span> | <span data-ttu-id="285a0-154">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-154">String</span></span> | <span data-ttu-id="285a0-155">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="285a0-155">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="285a0-156">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-156">toStringOutput</span></span> | <span data-ttu-id="285a0-157">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-157">String</span></span> | <span data-ttu-id="285a0-158">Bir iki üç</span><span class="sxs-lookup"><span data-stu-id="285a0-158">one, two, three</span></span> |
| <span data-ttu-id="285a0-159">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-159">toJsonOutput</span></span> | <span data-ttu-id="285a0-160">Nesne</span><span class="sxs-lookup"><span data-stu-id="285a0-160">Object</span></span> | <span data-ttu-id="285a0-161">{"bir": "a", "iki": "b"}</span><span class="sxs-lookup"><span data-stu-id="285a0-161">{"one": "a", "two": "b"}</span></span> |

<a id="base64tojson" />

## <a name="base64tojson"></a><span data-ttu-id="285a0-162">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="285a0-162">base64ToJson</span></span>
`base64tojson`

<span data-ttu-id="285a0-163">Bir base64 temsili bir JSON nesnesine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-163">Converts a base64 representation to a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-164">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-164">Parameters</span></span>

| <span data-ttu-id="285a0-165">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-165">Parameter</span></span> | <span data-ttu-id="285a0-166">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-166">Required</span></span> | <span data-ttu-id="285a0-167">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-167">Type</span></span> | <span data-ttu-id="285a0-168">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-168">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-169">base64value değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-169">base64Value</span></span> |<span data-ttu-id="285a0-170">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-170">Yes</span></span> |<span data-ttu-id="285a0-171">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-171">string</span></span> |<span data-ttu-id="285a0-172">Bir JSON nesnesine dönüştürmek için base64 gösterimi.</span><span class="sxs-lookup"><span data-stu-id="285a0-172">The base64 representation to convert to a JSON object.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-173">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-173">Return value</span></span>

<span data-ttu-id="285a0-174">Bir JSON nesnesi.</span><span class="sxs-lookup"><span data-stu-id="285a0-174">A JSON object.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-175">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-175">Examples</span></span>

<span data-ttu-id="285a0-176">Aşağıdaki örnek, bir base64 değeri dönüştürmek için base64ToJson işlevini kullanır:</span><span class="sxs-lookup"><span data-stu-id="285a0-176">The following example uses the base64ToJson function to convert a base64 value:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="285a0-177">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-177">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-178">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-178">Name</span></span> | <span data-ttu-id="285a0-179">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-179">Type</span></span> | <span data-ttu-id="285a0-180">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-180">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-181">base64Output</span><span class="sxs-lookup"><span data-stu-id="285a0-181">base64Output</span></span> | <span data-ttu-id="285a0-182">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-182">String</span></span> | <span data-ttu-id="285a0-183">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="285a0-183">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="285a0-184">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-184">toStringOutput</span></span> | <span data-ttu-id="285a0-185">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-185">String</span></span> | <span data-ttu-id="285a0-186">Bir iki üç</span><span class="sxs-lookup"><span data-stu-id="285a0-186">one, two, three</span></span> |
| <span data-ttu-id="285a0-187">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-187">toJsonOutput</span></span> | <span data-ttu-id="285a0-188">Nesne</span><span class="sxs-lookup"><span data-stu-id="285a0-188">Object</span></span> | <span data-ttu-id="285a0-189">{"bir": "a", "iki": "b"}</span><span class="sxs-lookup"><span data-stu-id="285a0-189">{"one": "a", "two": "b"}</span></span> |

<a id="base64tostring" />

## <a name="base64tostring"></a><span data-ttu-id="285a0-190">base64ToString</span><span class="sxs-lookup"><span data-stu-id="285a0-190">base64ToString</span></span>
`base64ToString(base64Value)`

<span data-ttu-id="285a0-191">Bir base64 temsili bir dizeye dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-191">Converts a base64 representation to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-192">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-192">Parameters</span></span>

| <span data-ttu-id="285a0-193">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-193">Parameter</span></span> | <span data-ttu-id="285a0-194">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-194">Required</span></span> | <span data-ttu-id="285a0-195">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-195">Type</span></span> | <span data-ttu-id="285a0-196">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-196">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-197">base64value değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-197">base64Value</span></span> |<span data-ttu-id="285a0-198">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-198">Yes</span></span> |<span data-ttu-id="285a0-199">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-199">string</span></span> |<span data-ttu-id="285a0-200">Bir dizeye dönüştürmek için base64 gösterimi.</span><span class="sxs-lookup"><span data-stu-id="285a0-200">The base64 representation to convert to a string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-201">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-201">Return value</span></span>

<span data-ttu-id="285a0-202">Dönüştürülen base64 değeri bir dize.</span><span class="sxs-lookup"><span data-stu-id="285a0-202">A string of the converted base64 value.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-203">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-203">Examples</span></span>

<span data-ttu-id="285a0-204">Aşağıdaki örnek, bir base64 değeri dönüştürmek için base64ToString işlevini kullanır:</span><span class="sxs-lookup"><span data-stu-id="285a0-204">The following example uses the base64ToString function to convert a base64 value:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="285a0-205">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-205">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-206">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-206">Name</span></span> | <span data-ttu-id="285a0-207">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-207">Type</span></span> | <span data-ttu-id="285a0-208">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-208">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-209">base64Output</span><span class="sxs-lookup"><span data-stu-id="285a0-209">base64Output</span></span> | <span data-ttu-id="285a0-210">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-210">String</span></span> | <span data-ttu-id="285a0-211">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="285a0-211">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="285a0-212">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-212">toStringOutput</span></span> | <span data-ttu-id="285a0-213">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-213">String</span></span> | <span data-ttu-id="285a0-214">Bir iki üç</span><span class="sxs-lookup"><span data-stu-id="285a0-214">one, two, three</span></span> |
| <span data-ttu-id="285a0-215">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-215">toJsonOutput</span></span> | <span data-ttu-id="285a0-216">Nesne</span><span class="sxs-lookup"><span data-stu-id="285a0-216">Object</span></span> | <span data-ttu-id="285a0-217">{"bir": "a", "iki": "b"}</span><span class="sxs-lookup"><span data-stu-id="285a0-217">{"one": "a", "two": "b"}</span></span> |



<a id="concat" />

## <a name="concat"></a><span data-ttu-id="285a0-218">concat</span><span class="sxs-lookup"><span data-stu-id="285a0-218">concat</span></span>
`concat (arg1, arg2, arg3, ...)`

<span data-ttu-id="285a0-219">Birden çok dize değerlerini birleştirir ve birleştirilmiş dizeyi döndürür veya birden çok birleştirir ve birleştirilmiş bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-219">Combines multiple string values and returns the concatenated string, or combines multiple arrays and returns the concatenated array.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-220">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-220">Parameters</span></span>

| <span data-ttu-id="285a0-221">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-221">Parameter</span></span> | <span data-ttu-id="285a0-222">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-222">Required</span></span> | <span data-ttu-id="285a0-223">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-223">Type</span></span> | <span data-ttu-id="285a0-224">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-224">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-225">arg1</span><span class="sxs-lookup"><span data-stu-id="285a0-225">arg1</span></span> |<span data-ttu-id="285a0-226">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-226">Yes</span></span> |<span data-ttu-id="285a0-227">dize veya dizi</span><span class="sxs-lookup"><span data-stu-id="285a0-227">string or array</span></span> |<span data-ttu-id="285a0-228">Birleştirme için ilk değer.</span><span class="sxs-lookup"><span data-stu-id="285a0-228">The first value for concatenation.</span></span> |
| <span data-ttu-id="285a0-229">Ek bağımsız değişkenler</span><span class="sxs-lookup"><span data-stu-id="285a0-229">additional arguments</span></span> |<span data-ttu-id="285a0-230">Hayır</span><span class="sxs-lookup"><span data-stu-id="285a0-230">No</span></span> |<span data-ttu-id="285a0-231">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-231">string</span></span> |<span data-ttu-id="285a0-232">Birleştirme için sıralı bir düzende ek değerler.</span><span class="sxs-lookup"><span data-stu-id="285a0-232">Additional values in sequential order for concatenation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-233">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-233">Return value</span></span>
<span data-ttu-id="285a0-234">Bir dize veya birleştirilmiş değerleri dizisi.</span><span class="sxs-lookup"><span data-stu-id="285a0-234">A string or array of concatenated values.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-235">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-235">Examples</span></span>

<span data-ttu-id="285a0-236">Aşağıdaki örnekte, iki dize değerleri birleştirmek ve birleştirilmiş dizeyi döndürür gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="285a0-236">The following example shows how to combine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="285a0-237">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-237">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-238">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-238">Name</span></span> | <span data-ttu-id="285a0-239">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-239">Type</span></span> | <span data-ttu-id="285a0-240">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-240">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-241">concatOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-241">concatOutput</span></span> | <span data-ttu-id="285a0-242">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-242">String</span></span> | <span data-ttu-id="285a0-243">önek 5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="285a0-243">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="285a0-244">Aşağıdaki örnekte, iki dizi birleştirmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="285a0-244">The following example shows how to combine two arrays.</span></span>

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

<span data-ttu-id="285a0-245">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-245">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-246">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-246">Name</span></span> | <span data-ttu-id="285a0-247">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-247">Type</span></span> | <span data-ttu-id="285a0-248">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-249">Döndür</span><span class="sxs-lookup"><span data-stu-id="285a0-249">return</span></span> | <span data-ttu-id="285a0-250">Dizi</span><span class="sxs-lookup"><span data-stu-id="285a0-250">Array</span></span> | <span data-ttu-id="285a0-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="285a0-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="285a0-252">içerir</span><span class="sxs-lookup"><span data-stu-id="285a0-252">contains</span></span>
`contains (container, itemToFind)`

<span data-ttu-id="285a0-253">Bir değer dizisini içerir, bir nesne bir anahtar veya bir dize bir alt dizeyi içeren olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="285a0-253">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-254">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-254">Parameters</span></span>

| <span data-ttu-id="285a0-255">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-255">Parameter</span></span> | <span data-ttu-id="285a0-256">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-256">Required</span></span> | <span data-ttu-id="285a0-257">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-257">Type</span></span> | <span data-ttu-id="285a0-258">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-258">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-259">kapsayıcı</span><span class="sxs-lookup"><span data-stu-id="285a0-259">container</span></span> |<span data-ttu-id="285a0-260">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-260">Yes</span></span> |<span data-ttu-id="285a0-261">dizi, nesne veya dize</span><span class="sxs-lookup"><span data-stu-id="285a0-261">array, object, or string</span></span> |<span data-ttu-id="285a0-262">Bulunacak değer içeren değeri.</span><span class="sxs-lookup"><span data-stu-id="285a0-262">The value that contains the value to find.</span></span> |
| <span data-ttu-id="285a0-263">itemToFind</span><span class="sxs-lookup"><span data-stu-id="285a0-263">itemToFind</span></span> |<span data-ttu-id="285a0-264">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-264">Yes</span></span> |<span data-ttu-id="285a0-265">dize veya int</span><span class="sxs-lookup"><span data-stu-id="285a0-265">string or int</span></span> |<span data-ttu-id="285a0-266">Bulunacak değer.</span><span class="sxs-lookup"><span data-stu-id="285a0-266">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-267">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-267">Return value</span></span>

<span data-ttu-id="285a0-268">**Doğru** öğe bulunduysa, **False**.</span><span class="sxs-lookup"><span data-stu-id="285a0-268">**True** if the item is found; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-269">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-269">Examples</span></span>

<span data-ttu-id="285a0-270">Aşağıdaki örnekte nasıl kullanılacağını gösterir farklı türleriyle içerir:</span><span class="sxs-lookup"><span data-stu-id="285a0-270">The following example shows how to use contains with different types:</span></span>

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

<span data-ttu-id="285a0-271">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-271">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-272">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-272">Name</span></span> | <span data-ttu-id="285a0-273">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-273">Type</span></span> | <span data-ttu-id="285a0-274">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-274">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-275">stringTrue</span><span class="sxs-lookup"><span data-stu-id="285a0-275">stringTrue</span></span> | <span data-ttu-id="285a0-276">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-276">Bool</span></span> | <span data-ttu-id="285a0-277">True</span><span class="sxs-lookup"><span data-stu-id="285a0-277">True</span></span> |
| <span data-ttu-id="285a0-278">stringFalse</span><span class="sxs-lookup"><span data-stu-id="285a0-278">stringFalse</span></span> | <span data-ttu-id="285a0-279">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-279">Bool</span></span> | <span data-ttu-id="285a0-280">False</span><span class="sxs-lookup"><span data-stu-id="285a0-280">False</span></span> |
| <span data-ttu-id="285a0-281">objectTrue</span><span class="sxs-lookup"><span data-stu-id="285a0-281">objectTrue</span></span> | <span data-ttu-id="285a0-282">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-282">Bool</span></span> | <span data-ttu-id="285a0-283">True</span><span class="sxs-lookup"><span data-stu-id="285a0-283">True</span></span> |
| <span data-ttu-id="285a0-284">objectFalse</span><span class="sxs-lookup"><span data-stu-id="285a0-284">objectFalse</span></span> | <span data-ttu-id="285a0-285">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-285">Bool</span></span> | <span data-ttu-id="285a0-286">False</span><span class="sxs-lookup"><span data-stu-id="285a0-286">False</span></span> |
| <span data-ttu-id="285a0-287">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="285a0-287">arrayTrue</span></span> | <span data-ttu-id="285a0-288">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-288">Bool</span></span> | <span data-ttu-id="285a0-289">True</span><span class="sxs-lookup"><span data-stu-id="285a0-289">True</span></span> |
| <span data-ttu-id="285a0-290">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="285a0-290">arrayFalse</span></span> | <span data-ttu-id="285a0-291">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-291">Bool</span></span> | <span data-ttu-id="285a0-292">False</span><span class="sxs-lookup"><span data-stu-id="285a0-292">False</span></span> |

<a id="datauri" />

## <a name="datauri"></a><span data-ttu-id="285a0-293">dataUri</span><span class="sxs-lookup"><span data-stu-id="285a0-293">dataUri</span></span>
`dataUri(stringToConvert)`

<span data-ttu-id="285a0-294">Bir veri URI değeri dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-294">Converts a value to a data URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-295">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-295">Parameters</span></span>

| <span data-ttu-id="285a0-296">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-296">Parameter</span></span> | <span data-ttu-id="285a0-297">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-297">Required</span></span> | <span data-ttu-id="285a0-298">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-298">Type</span></span> | <span data-ttu-id="285a0-299">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-299">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-300">stringToConvert</span><span class="sxs-lookup"><span data-stu-id="285a0-300">stringToConvert</span></span> |<span data-ttu-id="285a0-301">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-301">Yes</span></span> |<span data-ttu-id="285a0-302">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-302">string</span></span> |<span data-ttu-id="285a0-303">Bir veri URI dönüştürülecek değer.</span><span class="sxs-lookup"><span data-stu-id="285a0-303">The value to convert to a data URI.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-304">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-304">Return value</span></span>

<span data-ttu-id="285a0-305">Veri URI'si biçimlendirilmiş bir dize.</span><span class="sxs-lookup"><span data-stu-id="285a0-305">A string formatted as a data URI.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-306">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-306">Examples</span></span>

<span data-ttu-id="285a0-307">Aşağıdaki örnek, bir veri URI değeri dönüştürür ve veri URI'si bir dizeye dönüştürür:</span><span class="sxs-lookup"><span data-stu-id="285a0-307">The following example converts a value to a data URI, and converts a data URI to a string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

<span data-ttu-id="285a0-308">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-308">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-309">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-309">Name</span></span> | <span data-ttu-id="285a0-310">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-310">Type</span></span> | <span data-ttu-id="285a0-311">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-311">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-312">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-312">dataUriOutput</span></span> | <span data-ttu-id="285a0-313">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-313">String</span></span> | <span data-ttu-id="285a0-314">Veri: metin / düz; charset = utf8; base64, SGVsbG8 =</span><span class="sxs-lookup"><span data-stu-id="285a0-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="285a0-315">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-315">toStringOutput</span></span> | <span data-ttu-id="285a0-316">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-316">String</span></span> | <span data-ttu-id="285a0-317">Merhaba Dünya!</span><span class="sxs-lookup"><span data-stu-id="285a0-317">Hello, World!</span></span> |

<a id="datauritostring" />

## <a name="datauritostring"></a><span data-ttu-id="285a0-318">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="285a0-318">dataUriToString</span></span>
`dataUriToString(dataUriToConvert)`

<span data-ttu-id="285a0-319">Bir veri URI değerini bir dizeyle biçimlendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="285a0-319">Converts a data URI formatted value to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-320">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-320">Parameters</span></span>

| <span data-ttu-id="285a0-321">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-321">Parameter</span></span> | <span data-ttu-id="285a0-322">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-322">Required</span></span> | <span data-ttu-id="285a0-323">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-323">Type</span></span> | <span data-ttu-id="285a0-324">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-324">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-325">dataUriToConvert</span><span class="sxs-lookup"><span data-stu-id="285a0-325">dataUriToConvert</span></span> |<span data-ttu-id="285a0-326">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-326">Yes</span></span> |<span data-ttu-id="285a0-327">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-327">string</span></span> |<span data-ttu-id="285a0-328">Verileri dönüştürmek için URI değeri.</span><span class="sxs-lookup"><span data-stu-id="285a0-328">The data URI value to convert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-329">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-329">Return value</span></span>

<span data-ttu-id="285a0-330">Dönüştürülen değer içeren bir dize.</span><span class="sxs-lookup"><span data-stu-id="285a0-330">A string containing the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-331">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-331">Examples</span></span>

<span data-ttu-id="285a0-332">Aşağıdaki örnek, bir veri URI değeri dönüştürür ve veri URI'si bir dizeye dönüştürür:</span><span class="sxs-lookup"><span data-stu-id="285a0-332">The following example converts a value to a data URI, and converts a data URI to a string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

<span data-ttu-id="285a0-333">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-333">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-334">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-334">Name</span></span> | <span data-ttu-id="285a0-335">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-335">Type</span></span> | <span data-ttu-id="285a0-336">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-336">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-337">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-337">dataUriOutput</span></span> | <span data-ttu-id="285a0-338">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-338">String</span></span> | <span data-ttu-id="285a0-339">Veri: metin / düz; charset = utf8; base64, SGVsbG8 =</span><span class="sxs-lookup"><span data-stu-id="285a0-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="285a0-340">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-340">toStringOutput</span></span> | <span data-ttu-id="285a0-341">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-341">String</span></span> | <span data-ttu-id="285a0-342">Merhaba Dünya!</span><span class="sxs-lookup"><span data-stu-id="285a0-342">Hello, World!</span></span> |

<a id="empty" /> 

## <a name="empty"></a><span data-ttu-id="285a0-343">boş</span><span class="sxs-lookup"><span data-stu-id="285a0-343">empty</span></span>
`empty(itemToTest)`

<span data-ttu-id="285a0-344">Bir dizi, nesne veya dize boş olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="285a0-344">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-345">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-345">Parameters</span></span>

| <span data-ttu-id="285a0-346">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-346">Parameter</span></span> | <span data-ttu-id="285a0-347">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-347">Required</span></span> | <span data-ttu-id="285a0-348">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-348">Type</span></span> | <span data-ttu-id="285a0-349">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-349">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-350">itemToTest</span><span class="sxs-lookup"><span data-stu-id="285a0-350">itemToTest</span></span> |<span data-ttu-id="285a0-351">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-351">Yes</span></span> |<span data-ttu-id="285a0-352">dizi, nesne veya dize</span><span class="sxs-lookup"><span data-stu-id="285a0-352">array, object, or string</span></span> |<span data-ttu-id="285a0-353">Değerin boş olup olmadığını denetlemek için.</span><span class="sxs-lookup"><span data-stu-id="285a0-353">The value to check if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-354">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-354">Return value</span></span>

<span data-ttu-id="285a0-355">Döndürür **True** değeri geçerliyse boş, aksi takdirde **False**.</span><span class="sxs-lookup"><span data-stu-id="285a0-355">Returns **True** if the value is empty; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-356">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-356">Examples</span></span>

<span data-ttu-id="285a0-357">Aşağıdaki örnek, bir dizi, nesne ve dize boş olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="285a0-357">The following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="285a0-358">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-358">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-359">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-359">Name</span></span> | <span data-ttu-id="285a0-360">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-360">Type</span></span> | <span data-ttu-id="285a0-361">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-361">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-362">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="285a0-362">arrayEmpty</span></span> | <span data-ttu-id="285a0-363">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-363">Bool</span></span> | <span data-ttu-id="285a0-364">True</span><span class="sxs-lookup"><span data-stu-id="285a0-364">True</span></span> |
| <span data-ttu-id="285a0-365">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="285a0-365">objectEmpty</span></span> | <span data-ttu-id="285a0-366">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-366">Bool</span></span> | <span data-ttu-id="285a0-367">True</span><span class="sxs-lookup"><span data-stu-id="285a0-367">True</span></span> |
| <span data-ttu-id="285a0-368">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="285a0-368">stringEmpty</span></span> | <span data-ttu-id="285a0-369">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-369">Bool</span></span> | <span data-ttu-id="285a0-370">True</span><span class="sxs-lookup"><span data-stu-id="285a0-370">True</span></span> |

<a id="endswith" />

## <a name="endswith"></a><span data-ttu-id="285a0-371">endsWith</span><span class="sxs-lookup"><span data-stu-id="285a0-371">endsWith</span></span>
`endsWith(stringToSearch, stringToFind)`

<span data-ttu-id="285a0-372">Bir dize değeri ile bitip olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="285a0-372">Determines whether a string ends with a value.</span></span> <span data-ttu-id="285a0-373">Karşılaştırma büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="285a0-373">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-374">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-374">Parameters</span></span>

| <span data-ttu-id="285a0-375">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-375">Parameter</span></span> | <span data-ttu-id="285a0-376">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-376">Required</span></span> | <span data-ttu-id="285a0-377">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-377">Type</span></span> | <span data-ttu-id="285a0-378">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-378">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-379">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="285a0-379">stringToSearch</span></span> |<span data-ttu-id="285a0-380">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-380">Yes</span></span> |<span data-ttu-id="285a0-381">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-381">string</span></span> |<span data-ttu-id="285a0-382">Bulunacak öğe içeren değeri.</span><span class="sxs-lookup"><span data-stu-id="285a0-382">The value that contains the item to find.</span></span> |
| <span data-ttu-id="285a0-383">stringToFind</span><span class="sxs-lookup"><span data-stu-id="285a0-383">stringToFind</span></span> |<span data-ttu-id="285a0-384">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-384">Yes</span></span> |<span data-ttu-id="285a0-385">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-385">string</span></span> |<span data-ttu-id="285a0-386">Bulunacak değer.</span><span class="sxs-lookup"><span data-stu-id="285a0-386">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-387">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-387">Return value</span></span>

<span data-ttu-id="285a0-388">**Doğru** son karakterin veya karakter dizesi değeri; eşleşiyorsa Aksi halde, **False**.</span><span class="sxs-lookup"><span data-stu-id="285a0-388">**True** if the last character or characters of the string match the value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-389">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-389">Examples</span></span>

<span data-ttu-id="285a0-390">Aşağıdaki örnek startsWith ve endsWith işlevlerinin nasıl kullanılacağı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="285a0-390">The following example shows how to use the startsWith and endsWith functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="285a0-391">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-391">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-392">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-392">Name</span></span> | <span data-ttu-id="285a0-393">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-393">Type</span></span> | <span data-ttu-id="285a0-394">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-394">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-395">startsTrue</span><span class="sxs-lookup"><span data-stu-id="285a0-395">startsTrue</span></span> | <span data-ttu-id="285a0-396">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-396">Bool</span></span> | <span data-ttu-id="285a0-397">True</span><span class="sxs-lookup"><span data-stu-id="285a0-397">True</span></span> |
| <span data-ttu-id="285a0-398">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="285a0-398">startsCapTrue</span></span> | <span data-ttu-id="285a0-399">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-399">Bool</span></span> | <span data-ttu-id="285a0-400">True</span><span class="sxs-lookup"><span data-stu-id="285a0-400">True</span></span> |
| <span data-ttu-id="285a0-401">startsFalse</span><span class="sxs-lookup"><span data-stu-id="285a0-401">startsFalse</span></span> | <span data-ttu-id="285a0-402">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-402">Bool</span></span> | <span data-ttu-id="285a0-403">False</span><span class="sxs-lookup"><span data-stu-id="285a0-403">False</span></span> |
| <span data-ttu-id="285a0-404">endsTrue</span><span class="sxs-lookup"><span data-stu-id="285a0-404">endsTrue</span></span> | <span data-ttu-id="285a0-405">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-405">Bool</span></span> | <span data-ttu-id="285a0-406">True</span><span class="sxs-lookup"><span data-stu-id="285a0-406">True</span></span> |
| <span data-ttu-id="285a0-407">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="285a0-407">endsCapTrue</span></span> | <span data-ttu-id="285a0-408">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-408">Bool</span></span> | <span data-ttu-id="285a0-409">True</span><span class="sxs-lookup"><span data-stu-id="285a0-409">True</span></span> |
| <span data-ttu-id="285a0-410">endsFalse</span><span class="sxs-lookup"><span data-stu-id="285a0-410">endsFalse</span></span> | <span data-ttu-id="285a0-411">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-411">Bool</span></span> | <span data-ttu-id="285a0-412">False</span><span class="sxs-lookup"><span data-stu-id="285a0-412">False</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="285a0-413">ilk</span><span class="sxs-lookup"><span data-stu-id="285a0-413">first</span></span>
`first(arg1)`

<span data-ttu-id="285a0-414">Dize veya dizinin ilk öğesi ilk karakteri döndürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-414">Returns the first character of the string, or first element of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-415">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-415">Parameters</span></span>

| <span data-ttu-id="285a0-416">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-416">Parameter</span></span> | <span data-ttu-id="285a0-417">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-417">Required</span></span> | <span data-ttu-id="285a0-418">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-418">Type</span></span> | <span data-ttu-id="285a0-419">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-420">arg1</span><span class="sxs-lookup"><span data-stu-id="285a0-420">arg1</span></span> |<span data-ttu-id="285a0-421">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-421">Yes</span></span> |<span data-ttu-id="285a0-422">dizi veya dize</span><span class="sxs-lookup"><span data-stu-id="285a0-422">array or string</span></span> |<span data-ttu-id="285a0-423">İlk öğe veya karakter almak için değer.</span><span class="sxs-lookup"><span data-stu-id="285a0-423">The value to retrieve the first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-424">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-424">Return value</span></span>

<span data-ttu-id="285a0-425">İlk karakter veya bir dizi ilk öğe türü (dize, int, dizi veya nesne) dizesi.</span><span class="sxs-lookup"><span data-stu-id="285a0-425">A string of the first character, or the type (string, int, array, or object) of the first element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-426">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-426">Examples</span></span>

<span data-ttu-id="285a0-427">Aşağıdaki örnek ilk işlevi bir dizi ve dize ile nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="285a0-427">The following example shows how to use the first function with an array and string.</span></span>

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

<span data-ttu-id="285a0-428">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-428">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-429">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-429">Name</span></span> | <span data-ttu-id="285a0-430">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-430">Type</span></span> | <span data-ttu-id="285a0-431">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-432">arrayOutput</span></span> | <span data-ttu-id="285a0-433">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-433">String</span></span> | <span data-ttu-id="285a0-434">bir</span><span class="sxs-lookup"><span data-stu-id="285a0-434">one</span></span> |
| <span data-ttu-id="285a0-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-435">stringOutput</span></span> | <span data-ttu-id="285a0-436">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-436">String</span></span> | <span data-ttu-id="285a0-437">O</span><span class="sxs-lookup"><span data-stu-id="285a0-437">O</span></span> |

<a id="indexof" />

## <a name="indexof"></a><span data-ttu-id="285a0-438">IndexOf</span><span class="sxs-lookup"><span data-stu-id="285a0-438">indexOf</span></span>
`indexOf(stringToSearch, stringToFind)`

<span data-ttu-id="285a0-439">Dize içinde bir değerin ilk konumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-439">Returns the first position of a value within a string.</span></span> <span data-ttu-id="285a0-440">Karşılaştırma büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="285a0-440">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-441">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-441">Parameters</span></span>

| <span data-ttu-id="285a0-442">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-442">Parameter</span></span> | <span data-ttu-id="285a0-443">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-443">Required</span></span> | <span data-ttu-id="285a0-444">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-444">Type</span></span> | <span data-ttu-id="285a0-445">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-445">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-446">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="285a0-446">stringToSearch</span></span> |<span data-ttu-id="285a0-447">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-447">Yes</span></span> |<span data-ttu-id="285a0-448">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-448">string</span></span> |<span data-ttu-id="285a0-449">Bulunacak öğe içeren değeri.</span><span class="sxs-lookup"><span data-stu-id="285a0-449">The value that contains the item to find.</span></span> |
| <span data-ttu-id="285a0-450">stringToFind</span><span class="sxs-lookup"><span data-stu-id="285a0-450">stringToFind</span></span> |<span data-ttu-id="285a0-451">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-451">Yes</span></span> |<span data-ttu-id="285a0-452">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-452">string</span></span> |<span data-ttu-id="285a0-453">Bulunacak değer.</span><span class="sxs-lookup"><span data-stu-id="285a0-453">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-454">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-454">Return value</span></span>

<span data-ttu-id="285a0-455">Bulunacak öğe konumu temsil eden bir tamsayı.</span><span class="sxs-lookup"><span data-stu-id="285a0-455">An integer that represents the position of the item to find.</span></span> <span data-ttu-id="285a0-456">Sıfır tabanlı değerdir.</span><span class="sxs-lookup"><span data-stu-id="285a0-456">The value is zero-based.</span></span> <span data-ttu-id="285a0-457">Öğesi bulunmazsa -1 döndürülür.</span><span class="sxs-lookup"><span data-stu-id="285a0-457">If the item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-458">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-458">Examples</span></span>

<span data-ttu-id="285a0-459">Aşağıdaki örnek IndexOf ve lastIndexOf işlevlerinin nasıl kullanılacağı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="285a0-459">The following example shows how to use the indexOf and lastIndexOf functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

<span data-ttu-id="285a0-460">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-460">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-461">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-461">Name</span></span> | <span data-ttu-id="285a0-462">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-462">Type</span></span> | <span data-ttu-id="285a0-463">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-463">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-464">firstT</span><span class="sxs-lookup"><span data-stu-id="285a0-464">firstT</span></span> | <span data-ttu-id="285a0-465">Int</span><span class="sxs-lookup"><span data-stu-id="285a0-465">Int</span></span> | <span data-ttu-id="285a0-466">0</span><span class="sxs-lookup"><span data-stu-id="285a0-466">0</span></span> |
| <span data-ttu-id="285a0-467">lastT</span><span class="sxs-lookup"><span data-stu-id="285a0-467">lastT</span></span> | <span data-ttu-id="285a0-468">Int</span><span class="sxs-lookup"><span data-stu-id="285a0-468">Int</span></span> | <span data-ttu-id="285a0-469">3</span><span class="sxs-lookup"><span data-stu-id="285a0-469">3</span></span> |
| <span data-ttu-id="285a0-470">firstString</span><span class="sxs-lookup"><span data-stu-id="285a0-470">firstString</span></span> | <span data-ttu-id="285a0-471">Int</span><span class="sxs-lookup"><span data-stu-id="285a0-471">Int</span></span> | <span data-ttu-id="285a0-472">2</span><span class="sxs-lookup"><span data-stu-id="285a0-472">2</span></span> |
| <span data-ttu-id="285a0-473">lastString</span><span class="sxs-lookup"><span data-stu-id="285a0-473">lastString</span></span> | <span data-ttu-id="285a0-474">Int</span><span class="sxs-lookup"><span data-stu-id="285a0-474">Int</span></span> | <span data-ttu-id="285a0-475">0</span><span class="sxs-lookup"><span data-stu-id="285a0-475">0</span></span> |
| <span data-ttu-id="285a0-476">notFound</span><span class="sxs-lookup"><span data-stu-id="285a0-476">notFound</span></span> | <span data-ttu-id="285a0-477">Int</span><span class="sxs-lookup"><span data-stu-id="285a0-477">Int</span></span> | <span data-ttu-id="285a0-478">-1</span><span class="sxs-lookup"><span data-stu-id="285a0-478">-1</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="285a0-479">Son</span><span class="sxs-lookup"><span data-stu-id="285a0-479">last</span></span>
`last (arg1)`

<span data-ttu-id="285a0-480">Son karakter dizenin veya dizinin son öğesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-480">Returns last character of the string, or the last element of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-481">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-481">Parameters</span></span>

| <span data-ttu-id="285a0-482">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-482">Parameter</span></span> | <span data-ttu-id="285a0-483">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-483">Required</span></span> | <span data-ttu-id="285a0-484">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-484">Type</span></span> | <span data-ttu-id="285a0-485">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-485">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-486">arg1</span><span class="sxs-lookup"><span data-stu-id="285a0-486">arg1</span></span> |<span data-ttu-id="285a0-487">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-487">Yes</span></span> |<span data-ttu-id="285a0-488">dizi veya dize</span><span class="sxs-lookup"><span data-stu-id="285a0-488">array or string</span></span> |<span data-ttu-id="285a0-489">Son öğe veya karakter almak için değer.</span><span class="sxs-lookup"><span data-stu-id="285a0-489">The value to retrieve the last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-490">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-490">Return value</span></span>

<span data-ttu-id="285a0-491">Son karakter veya bir dizi son öğesi türü (dize, int, dizi veya nesne) dizesi.</span><span class="sxs-lookup"><span data-stu-id="285a0-491">A string of the last character, or the type (string, int, array, or object) of the last element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-492">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-492">Examples</span></span>

<span data-ttu-id="285a0-493">Aşağıdaki örnek, son işlevi bir dizi ve dize ile nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="285a0-493">The following example shows how to use the last function with an array and string.</span></span>

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

<span data-ttu-id="285a0-494">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-494">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-495">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-495">Name</span></span> | <span data-ttu-id="285a0-496">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-496">Type</span></span> | <span data-ttu-id="285a0-497">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-497">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-498">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-498">arrayOutput</span></span> | <span data-ttu-id="285a0-499">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-499">String</span></span> | <span data-ttu-id="285a0-500">üç</span><span class="sxs-lookup"><span data-stu-id="285a0-500">three</span></span> |
| <span data-ttu-id="285a0-501">stringOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-501">stringOutput</span></span> | <span data-ttu-id="285a0-502">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-502">String</span></span> | <span data-ttu-id="285a0-503">E</span><span class="sxs-lookup"><span data-stu-id="285a0-503">e</span></span> |

<a id="lastindexof" />

## <a name="lastindexof"></a><span data-ttu-id="285a0-504">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="285a0-504">lastIndexOf</span></span>
`lastIndexOf(stringToSearch, stringToFind)`

<span data-ttu-id="285a0-505">Değer bir dize içinde son konumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-505">Returns the last position of a value within a string.</span></span> <span data-ttu-id="285a0-506">Karşılaştırma büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="285a0-506">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-507">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-507">Parameters</span></span>

| <span data-ttu-id="285a0-508">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-508">Parameter</span></span> | <span data-ttu-id="285a0-509">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-509">Required</span></span> | <span data-ttu-id="285a0-510">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-510">Type</span></span> | <span data-ttu-id="285a0-511">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-511">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-512">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="285a0-512">stringToSearch</span></span> |<span data-ttu-id="285a0-513">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-513">Yes</span></span> |<span data-ttu-id="285a0-514">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-514">string</span></span> |<span data-ttu-id="285a0-515">Bulunacak öğe içeren değeri.</span><span class="sxs-lookup"><span data-stu-id="285a0-515">The value that contains the item to find.</span></span> |
| <span data-ttu-id="285a0-516">stringToFind</span><span class="sxs-lookup"><span data-stu-id="285a0-516">stringToFind</span></span> |<span data-ttu-id="285a0-517">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-517">Yes</span></span> |<span data-ttu-id="285a0-518">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-518">string</span></span> |<span data-ttu-id="285a0-519">Bulunacak değer.</span><span class="sxs-lookup"><span data-stu-id="285a0-519">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-520">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-520">Return value</span></span>

<span data-ttu-id="285a0-521">Bulunacak öğe son konumunu temsil eden bir tamsayı.</span><span class="sxs-lookup"><span data-stu-id="285a0-521">An integer that represents the last position of the item to find.</span></span> <span data-ttu-id="285a0-522">Sıfır tabanlı değerdir.</span><span class="sxs-lookup"><span data-stu-id="285a0-522">The value is zero-based.</span></span> <span data-ttu-id="285a0-523">Öğesi bulunmazsa -1 döndürülür.</span><span class="sxs-lookup"><span data-stu-id="285a0-523">If the item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-524">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-524">Examples</span></span>

<span data-ttu-id="285a0-525">Aşağıdaki örnek IndexOf ve lastIndexOf işlevlerinin nasıl kullanılacağı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="285a0-525">The following example shows how to use the indexOf and lastIndexOf functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

<span data-ttu-id="285a0-526">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-526">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-527">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-527">Name</span></span> | <span data-ttu-id="285a0-528">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-528">Type</span></span> | <span data-ttu-id="285a0-529">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-529">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-530">firstT</span><span class="sxs-lookup"><span data-stu-id="285a0-530">firstT</span></span> | <span data-ttu-id="285a0-531">Int</span><span class="sxs-lookup"><span data-stu-id="285a0-531">Int</span></span> | <span data-ttu-id="285a0-532">0</span><span class="sxs-lookup"><span data-stu-id="285a0-532">0</span></span> |
| <span data-ttu-id="285a0-533">lastT</span><span class="sxs-lookup"><span data-stu-id="285a0-533">lastT</span></span> | <span data-ttu-id="285a0-534">Int</span><span class="sxs-lookup"><span data-stu-id="285a0-534">Int</span></span> | <span data-ttu-id="285a0-535">3</span><span class="sxs-lookup"><span data-stu-id="285a0-535">3</span></span> |
| <span data-ttu-id="285a0-536">firstString</span><span class="sxs-lookup"><span data-stu-id="285a0-536">firstString</span></span> | <span data-ttu-id="285a0-537">Int</span><span class="sxs-lookup"><span data-stu-id="285a0-537">Int</span></span> | <span data-ttu-id="285a0-538">2</span><span class="sxs-lookup"><span data-stu-id="285a0-538">2</span></span> |
| <span data-ttu-id="285a0-539">lastString</span><span class="sxs-lookup"><span data-stu-id="285a0-539">lastString</span></span> | <span data-ttu-id="285a0-540">Int</span><span class="sxs-lookup"><span data-stu-id="285a0-540">Int</span></span> | <span data-ttu-id="285a0-541">0</span><span class="sxs-lookup"><span data-stu-id="285a0-541">0</span></span> |
| <span data-ttu-id="285a0-542">notFound</span><span class="sxs-lookup"><span data-stu-id="285a0-542">notFound</span></span> | <span data-ttu-id="285a0-543">Int</span><span class="sxs-lookup"><span data-stu-id="285a0-543">Int</span></span> | <span data-ttu-id="285a0-544">-1</span><span class="sxs-lookup"><span data-stu-id="285a0-544">-1</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="285a0-545">uzunluğu</span><span class="sxs-lookup"><span data-stu-id="285a0-545">length</span></span>
`length(string)`

<span data-ttu-id="285a0-546">Bir dize veya bir dizideki öğeler karakterlerin sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-546">Returns the number of characters in a string, or elements in an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-547">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-547">Parameters</span></span>

| <span data-ttu-id="285a0-548">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-548">Parameter</span></span> | <span data-ttu-id="285a0-549">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-549">Required</span></span> | <span data-ttu-id="285a0-550">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-550">Type</span></span> | <span data-ttu-id="285a0-551">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-551">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-552">arg1</span><span class="sxs-lookup"><span data-stu-id="285a0-552">arg1</span></span> |<span data-ttu-id="285a0-553">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-553">Yes</span></span> |<span data-ttu-id="285a0-554">dizi veya dize</span><span class="sxs-lookup"><span data-stu-id="285a0-554">array or string</span></span> |<span data-ttu-id="285a0-555">Karakter sayısını almak için kullanılacak öğeler veya dize sayısını almak için kullanılacak dizisi.</span><span class="sxs-lookup"><span data-stu-id="285a0-555">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-556">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-556">Return value</span></span>

<span data-ttu-id="285a0-557">İnt</span><span class="sxs-lookup"><span data-stu-id="285a0-557">An int.</span></span> 

### <a name="examples"></a><span data-ttu-id="285a0-558">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-558">Examples</span></span>

<span data-ttu-id="285a0-559">Aşağıdaki örnek, bir dizi ve dize uzunluğu kullanmayı gösterir:</span><span class="sxs-lookup"><span data-stu-id="285a0-559">The following example shows how to use length with an array and string:</span></span>

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

<span data-ttu-id="285a0-560">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-560">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-561">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-561">Name</span></span> | <span data-ttu-id="285a0-562">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-562">Type</span></span> | <span data-ttu-id="285a0-563">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-563">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-564">arrayLength</span><span class="sxs-lookup"><span data-stu-id="285a0-564">arrayLength</span></span> | <span data-ttu-id="285a0-565">Int</span><span class="sxs-lookup"><span data-stu-id="285a0-565">Int</span></span> | <span data-ttu-id="285a0-566">3</span><span class="sxs-lookup"><span data-stu-id="285a0-566">3</span></span> |
| <span data-ttu-id="285a0-567">stringLength</span><span class="sxs-lookup"><span data-stu-id="285a0-567">stringLength</span></span> | <span data-ttu-id="285a0-568">Int</span><span class="sxs-lookup"><span data-stu-id="285a0-568">Int</span></span> | <span data-ttu-id="285a0-569">13</span><span class="sxs-lookup"><span data-stu-id="285a0-569">13</span></span> |

<a id="padleft" />

## <a name="padleft"></a><span data-ttu-id="285a0-570">PadLeft</span><span class="sxs-lookup"><span data-stu-id="285a0-570">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="285a0-571">Toplam belirtilen uzunluk ulaşmasını kadar sola karakterler ekleyerek sağa hizalı dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-571">Returns a right-aligned string by adding characters to the left until reaching the total specified length.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-572">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-572">Parameters</span></span>

| <span data-ttu-id="285a0-573">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-573">Parameter</span></span> | <span data-ttu-id="285a0-574">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-574">Required</span></span> | <span data-ttu-id="285a0-575">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-575">Type</span></span> | <span data-ttu-id="285a0-576">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-576">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-577">valueToPad</span><span class="sxs-lookup"><span data-stu-id="285a0-577">valueToPad</span></span> |<span data-ttu-id="285a0-578">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-578">Yes</span></span> |<span data-ttu-id="285a0-579">dize veya int</span><span class="sxs-lookup"><span data-stu-id="285a0-579">string or int</span></span> |<span data-ttu-id="285a0-580">Sağa Hizala değeri.</span><span class="sxs-lookup"><span data-stu-id="285a0-580">The value to right-align.</span></span> |
| <span data-ttu-id="285a0-581">totalLength</span><span class="sxs-lookup"><span data-stu-id="285a0-581">totalLength</span></span> |<span data-ttu-id="285a0-582">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-582">Yes</span></span> |<span data-ttu-id="285a0-583">Int</span><span class="sxs-lookup"><span data-stu-id="285a0-583">int</span></span> |<span data-ttu-id="285a0-584">Döndürülen dize karakter toplam sayısı.</span><span class="sxs-lookup"><span data-stu-id="285a0-584">The total number of characters in the returned string.</span></span> |
| <span data-ttu-id="285a0-585">paddingCharacter</span><span class="sxs-lookup"><span data-stu-id="285a0-585">paddingCharacter</span></span> |<span data-ttu-id="285a0-586">Hayır</span><span class="sxs-lookup"><span data-stu-id="285a0-586">No</span></span> |<span data-ttu-id="285a0-587">tek bir karakter</span><span class="sxs-lookup"><span data-stu-id="285a0-587">single character</span></span> |<span data-ttu-id="285a0-588">Sol-toplam uzunluğu ulaşılana kadar doldurma için kullanılacak karakter.</span><span class="sxs-lookup"><span data-stu-id="285a0-588">The character to use for left-padding until the total length is reached.</span></span> <span data-ttu-id="285a0-589">Varsayılan değer bir alandır.</span><span class="sxs-lookup"><span data-stu-id="285a0-589">The default value is a space.</span></span> |

<span data-ttu-id="285a0-590">Özgün dizeye doldurulacak karakter sayısından daha uzun olması durumunda hiçbir karakter eklenir.</span><span class="sxs-lookup"><span data-stu-id="285a0-590">If the original string is longer than the number of characters to pad, no characters are added.</span></span>

### <a name="return-value"></a><span data-ttu-id="285a0-591">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-591">Return value</span></span>

<span data-ttu-id="285a0-592">Dizenin ile en az belirtilen karakterlerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="285a0-592">A string with at least the number of specified characters.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-593">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-593">Examples</span></span>

<span data-ttu-id="285a0-594">Aşağıdaki örnekte, kullanıcı tarafından sağlanan parametre değeri sıfır karakter toplam karakter sayısı ulaşana kadar ekleyerek paneli gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="285a0-594">The following example shows how to pad the user-provided parameter value by adding the zero character until it reaches the total number of characters.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123"
        }
    },
    "resources": [],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[padLeft(parameters('testString'),10,'0')]"
        }
    }
}
```

<span data-ttu-id="285a0-595">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-595">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-596">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-596">Name</span></span> | <span data-ttu-id="285a0-597">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-597">Type</span></span> | <span data-ttu-id="285a0-598">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-598">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-599">stringOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-599">stringOutput</span></span> | <span data-ttu-id="285a0-600">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-600">String</span></span> | <span data-ttu-id="285a0-601">0000000123</span><span class="sxs-lookup"><span data-stu-id="285a0-601">0000000123</span></span> |

<a id="replace" />

## <a name="replace"></a><span data-ttu-id="285a0-602">Değiştir</span><span class="sxs-lookup"><span data-stu-id="285a0-602">replace</span></span>
`replace(originalString, oldString, newString)`

<span data-ttu-id="285a0-603">Başka bir dizeyle yerine tek bir dize tüm örneklerini içeren yeni bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-603">Returns a new string with all instances of one string replaced by another string.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-604">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-604">Parameters</span></span>

| <span data-ttu-id="285a0-605">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-605">Parameter</span></span> | <span data-ttu-id="285a0-606">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-606">Required</span></span> | <span data-ttu-id="285a0-607">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-607">Type</span></span> | <span data-ttu-id="285a0-608">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-608">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-609">originalString</span><span class="sxs-lookup"><span data-stu-id="285a0-609">originalString</span></span> |<span data-ttu-id="285a0-610">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-610">Yes</span></span> |<span data-ttu-id="285a0-611">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-611">string</span></span> |<span data-ttu-id="285a0-612">Başka bir dizeyle yerine tek bir dize tüm örneklerini sahip değeri.</span><span class="sxs-lookup"><span data-stu-id="285a0-612">The value that has all instances of one string replaced by another string.</span></span> |
| <span data-ttu-id="285a0-613">oldString</span><span class="sxs-lookup"><span data-stu-id="285a0-613">oldString</span></span> |<span data-ttu-id="285a0-614">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-614">Yes</span></span> |<span data-ttu-id="285a0-615">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-615">string</span></span> |<span data-ttu-id="285a0-616">Özgün dizeden kaldırılacak dizesi.</span><span class="sxs-lookup"><span data-stu-id="285a0-616">The string to be removed from the original string.</span></span> |
| <span data-ttu-id="285a0-617">newString</span><span class="sxs-lookup"><span data-stu-id="285a0-617">newString</span></span> |<span data-ttu-id="285a0-618">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-618">Yes</span></span> |<span data-ttu-id="285a0-619">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-619">string</span></span> |<span data-ttu-id="285a0-620">Kaldırılan dize yerine eklenecek dize.</span><span class="sxs-lookup"><span data-stu-id="285a0-620">The string to add in place of the removed string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-621">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-621">Return value</span></span>

<span data-ttu-id="285a0-622">Değiştirilen karakterler içeren bir dize.</span><span class="sxs-lookup"><span data-stu-id="285a0-622">A string with the replaced characters.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-623">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-623">Examples</span></span>

<span data-ttu-id="285a0-624">Aşağıdaki örnek, kullanıcı tarafından sağlanan dizeden tüm çizgiler kaldırma ve dizesinin parçası başka bir dizeyle değiştirmeniz nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="285a0-624">The following example shows how to remove all dashes from the user-provided string, and how to replace part of the string with another string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123-123-1234"
        }
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'-', '')]"
        },
        "secodeOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'1234', 'xxxx')]"
        }
    }
}
```

<span data-ttu-id="285a0-625">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-625">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-626">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-626">Name</span></span> | <span data-ttu-id="285a0-627">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-627">Type</span></span> | <span data-ttu-id="285a0-628">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-628">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-629">firstOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-629">firstOutput</span></span> | <span data-ttu-id="285a0-630">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-630">String</span></span> | <span data-ttu-id="285a0-631">1231231234</span><span class="sxs-lookup"><span data-stu-id="285a0-631">1231231234</span></span> |
| <span data-ttu-id="285a0-632">secodeOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-632">secodeOutput</span></span> | <span data-ttu-id="285a0-633">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-633">String</span></span> | <span data-ttu-id="285a0-634">123-123-xxxx</span><span class="sxs-lookup"><span data-stu-id="285a0-634">123-123-xxxx</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="285a0-635">Atla</span><span class="sxs-lookup"><span data-stu-id="285a0-635">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="285a0-636">Tüm karakterleri bir dizeyle belirtilen sayıda karakter veya bir dizi tüm öğelerle sonra sonra belirtilen sayıda öğeyi döndürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-636">Returns a string with all the characters after the specified number of characters, or an array with all the elements after the specified number of elements.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-637">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-637">Parameters</span></span>

| <span data-ttu-id="285a0-638">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-638">Parameter</span></span> | <span data-ttu-id="285a0-639">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-639">Required</span></span> | <span data-ttu-id="285a0-640">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-640">Type</span></span> | <span data-ttu-id="285a0-641">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-641">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-642">originalValue</span><span class="sxs-lookup"><span data-stu-id="285a0-642">originalValue</span></span> |<span data-ttu-id="285a0-643">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-643">Yes</span></span> |<span data-ttu-id="285a0-644">dizi veya dize</span><span class="sxs-lookup"><span data-stu-id="285a0-644">array or string</span></span> |<span data-ttu-id="285a0-645">Dizi veya atlama kullanılacak dize.</span><span class="sxs-lookup"><span data-stu-id="285a0-645">The array or string to use for skipping.</span></span> |
| <span data-ttu-id="285a0-646">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="285a0-646">numberToSkip</span></span> |<span data-ttu-id="285a0-647">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-647">Yes</span></span> |<span data-ttu-id="285a0-648">Int</span><span class="sxs-lookup"><span data-stu-id="285a0-648">int</span></span> |<span data-ttu-id="285a0-649">Öğeleri veya atlamak için karakter sayısı.</span><span class="sxs-lookup"><span data-stu-id="285a0-649">The number of elements or characters to skip.</span></span> <span data-ttu-id="285a0-650">Bu değer 0 veya daha az ise, tüm öğeleri veya karakter değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="285a0-650">If this value is 0 or less, all the elements or characters in the value are returned.</span></span> <span data-ttu-id="285a0-651">Dizi veya dize uzunluğundan büyük olursa, boş dize veya dize döndürülür.</span><span class="sxs-lookup"><span data-stu-id="285a0-651">If it is larger than the length of the array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-652">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-652">Return value</span></span>

<span data-ttu-id="285a0-653">Bir dizi veya dize.</span><span class="sxs-lookup"><span data-stu-id="285a0-653">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-654">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-654">Examples</span></span>

<span data-ttu-id="285a0-655">Aşağıdaki örnek, belirtilen sayıda öğeyi dizisinde bulunan ve belirtilen bir dizedeki karakter sayısını atlar.</span><span class="sxs-lookup"><span data-stu-id="285a0-655">The following example skips the specified number of elements in the array, and the specified number of characters in a string.</span></span>

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

<span data-ttu-id="285a0-656">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-656">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-657">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-657">Name</span></span> | <span data-ttu-id="285a0-658">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-658">Type</span></span> | <span data-ttu-id="285a0-659">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-659">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-660">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-660">arrayOutput</span></span> | <span data-ttu-id="285a0-661">Dizi</span><span class="sxs-lookup"><span data-stu-id="285a0-661">Array</span></span> | <span data-ttu-id="285a0-662">["üç"]</span><span class="sxs-lookup"><span data-stu-id="285a0-662">["three"]</span></span> |
| <span data-ttu-id="285a0-663">stringOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-663">stringOutput</span></span> | <span data-ttu-id="285a0-664">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-664">String</span></span> | <span data-ttu-id="285a0-665">iki üç</span><span class="sxs-lookup"><span data-stu-id="285a0-665">two three</span></span> |

<a id="split" />

## <a name="split"></a><span data-ttu-id="285a0-666">split</span><span class="sxs-lookup"><span data-stu-id="285a0-666">split</span></span>
`split(inputString, delimiter)`

<span data-ttu-id="285a0-667">Belirtilen sınırlayıcıları tarafından ayrılmış alt dizeler giriş dizesi içeren bir dizeler dizisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-667">Returns an array of strings that contains the substrings of the input string that are delimited by the specified delimiters.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-668">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-668">Parameters</span></span>

| <span data-ttu-id="285a0-669">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-669">Parameter</span></span> | <span data-ttu-id="285a0-670">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-670">Required</span></span> | <span data-ttu-id="285a0-671">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-671">Type</span></span> | <span data-ttu-id="285a0-672">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-672">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-673">inputString</span><span class="sxs-lookup"><span data-stu-id="285a0-673">inputString</span></span> |<span data-ttu-id="285a0-674">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-674">Yes</span></span> |<span data-ttu-id="285a0-675">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-675">string</span></span> |<span data-ttu-id="285a0-676">Bölme dize.</span><span class="sxs-lookup"><span data-stu-id="285a0-676">The string to split.</span></span> |
| <span data-ttu-id="285a0-677">sınırlayıcı</span><span class="sxs-lookup"><span data-stu-id="285a0-677">delimiter</span></span> |<span data-ttu-id="285a0-678">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-678">Yes</span></span> |<span data-ttu-id="285a0-679">dize veya dize dizisi</span><span class="sxs-lookup"><span data-stu-id="285a0-679">string or array of strings</span></span> |<span data-ttu-id="285a0-680">Dize bölme için kullanılacak sınırlayıcı.</span><span class="sxs-lookup"><span data-stu-id="285a0-680">The delimiter to use for splitting the string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-681">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-681">Return value</span></span>

<span data-ttu-id="285a0-682">Bir dizeler dizisi.</span><span class="sxs-lookup"><span data-stu-id="285a0-682">An array of strings.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-683">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-683">Examples</span></span>

<span data-ttu-id="285a0-684">Aşağıdaki örnek giriş dizesi virgül ile virgül veya noktalı virgül ile böler.</span><span class="sxs-lookup"><span data-stu-id="285a0-684">The following example splits the input string with a comma, and with either a comma or a semi-colon.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstString": {
            "type": "string",
            "defaultValue": "one,two,three"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "one;two,three"
        }
    },
    "variables": {
        "delimiters": [ ",", ";" ]
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "array",
            "value": "[split(parameters('firstString'),',')]"
        },
        "secondOutput": {
            "type": "array",
            "value": "[split(parameters('secondString'),variables('delimiters'))]"
        }
    }
}
```

<span data-ttu-id="285a0-685">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-685">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-686">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-686">Name</span></span> | <span data-ttu-id="285a0-687">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-687">Type</span></span> | <span data-ttu-id="285a0-688">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-688">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-689">firstOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-689">firstOutput</span></span> | <span data-ttu-id="285a0-690">Dizi</span><span class="sxs-lookup"><span data-stu-id="285a0-690">Array</span></span> | <span data-ttu-id="285a0-691">["bir", "iki", "üç"]</span><span class="sxs-lookup"><span data-stu-id="285a0-691">["one", "two", "three"]</span></span> |
| <span data-ttu-id="285a0-692">secondOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-692">secondOutput</span></span> | <span data-ttu-id="285a0-693">Dizi</span><span class="sxs-lookup"><span data-stu-id="285a0-693">Array</span></span> | <span data-ttu-id="285a0-694">["bir", "iki", "üç"]</span><span class="sxs-lookup"><span data-stu-id="285a0-694">["one", "two", "three"]</span></span> |

<a id="startswith" />

## <a name="startswith"></a><span data-ttu-id="285a0-695">startsWith</span><span class="sxs-lookup"><span data-stu-id="285a0-695">startsWith</span></span>
`startsWith(stringToSearch, stringToFind)`

<span data-ttu-id="285a0-696">Bir dize değeri ile başlayıp başlamadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="285a0-696">Determines whether a string starts with a value.</span></span> <span data-ttu-id="285a0-697">Karşılaştırma büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="285a0-697">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-698">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-698">Parameters</span></span>

| <span data-ttu-id="285a0-699">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-699">Parameter</span></span> | <span data-ttu-id="285a0-700">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-700">Required</span></span> | <span data-ttu-id="285a0-701">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-701">Type</span></span> | <span data-ttu-id="285a0-702">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-702">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-703">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="285a0-703">stringToSearch</span></span> |<span data-ttu-id="285a0-704">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-704">Yes</span></span> |<span data-ttu-id="285a0-705">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-705">string</span></span> |<span data-ttu-id="285a0-706">Bulunacak öğe içeren değeri.</span><span class="sxs-lookup"><span data-stu-id="285a0-706">The value that contains the item to find.</span></span> |
| <span data-ttu-id="285a0-707">stringToFind</span><span class="sxs-lookup"><span data-stu-id="285a0-707">stringToFind</span></span> |<span data-ttu-id="285a0-708">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-708">Yes</span></span> |<span data-ttu-id="285a0-709">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-709">string</span></span> |<span data-ttu-id="285a0-710">Bulunacak değer.</span><span class="sxs-lookup"><span data-stu-id="285a0-710">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-711">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-711">Return value</span></span>

<span data-ttu-id="285a0-712">**Doğru** ilk karakterin veya karakter dizesi değeri; eşleşiyorsa Aksi halde, **False**.</span><span class="sxs-lookup"><span data-stu-id="285a0-712">**True** if the first character or characters of the string match the value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-713">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-713">Examples</span></span>

<span data-ttu-id="285a0-714">Aşağıdaki örnek startsWith ve endsWith işlevlerinin nasıl kullanılacağı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="285a0-714">The following example shows how to use the startsWith and endsWith functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="285a0-715">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-715">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-716">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-716">Name</span></span> | <span data-ttu-id="285a0-717">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-717">Type</span></span> | <span data-ttu-id="285a0-718">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-718">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-719">startsTrue</span><span class="sxs-lookup"><span data-stu-id="285a0-719">startsTrue</span></span> | <span data-ttu-id="285a0-720">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-720">Bool</span></span> | <span data-ttu-id="285a0-721">True</span><span class="sxs-lookup"><span data-stu-id="285a0-721">True</span></span> |
| <span data-ttu-id="285a0-722">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="285a0-722">startsCapTrue</span></span> | <span data-ttu-id="285a0-723">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-723">Bool</span></span> | <span data-ttu-id="285a0-724">True</span><span class="sxs-lookup"><span data-stu-id="285a0-724">True</span></span> |
| <span data-ttu-id="285a0-725">startsFalse</span><span class="sxs-lookup"><span data-stu-id="285a0-725">startsFalse</span></span> | <span data-ttu-id="285a0-726">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-726">Bool</span></span> | <span data-ttu-id="285a0-727">False</span><span class="sxs-lookup"><span data-stu-id="285a0-727">False</span></span> |
| <span data-ttu-id="285a0-728">endsTrue</span><span class="sxs-lookup"><span data-stu-id="285a0-728">endsTrue</span></span> | <span data-ttu-id="285a0-729">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-729">Bool</span></span> | <span data-ttu-id="285a0-730">True</span><span class="sxs-lookup"><span data-stu-id="285a0-730">True</span></span> |
| <span data-ttu-id="285a0-731">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="285a0-731">endsCapTrue</span></span> | <span data-ttu-id="285a0-732">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-732">Bool</span></span> | <span data-ttu-id="285a0-733">True</span><span class="sxs-lookup"><span data-stu-id="285a0-733">True</span></span> |
| <span data-ttu-id="285a0-734">endsFalse</span><span class="sxs-lookup"><span data-stu-id="285a0-734">endsFalse</span></span> | <span data-ttu-id="285a0-735">bool</span><span class="sxs-lookup"><span data-stu-id="285a0-735">Bool</span></span> | <span data-ttu-id="285a0-736">False</span><span class="sxs-lookup"><span data-stu-id="285a0-736">False</span></span> |

<a id="string" />

## <a name="string"></a><span data-ttu-id="285a0-737">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-737">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="285a0-738">Belirtilen değer bir dizeye dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-738">Converts the specified value to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-739">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-739">Parameters</span></span>

| <span data-ttu-id="285a0-740">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-740">Parameter</span></span> | <span data-ttu-id="285a0-741">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-741">Required</span></span> | <span data-ttu-id="285a0-742">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-742">Type</span></span> | <span data-ttu-id="285a0-743">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-743">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-744">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="285a0-744">valueToConvert</span></span> |<span data-ttu-id="285a0-745">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-745">Yes</span></span> | <span data-ttu-id="285a0-746">Herhangi biri</span><span class="sxs-lookup"><span data-stu-id="285a0-746">Any</span></span> |<span data-ttu-id="285a0-747">Metne dönüştürülecek değer.</span><span class="sxs-lookup"><span data-stu-id="285a0-747">The value to convert to string.</span></span> <span data-ttu-id="285a0-748">Nesneler ve diziler dahil olmak üzere herhangi türde bir değer dönüştürülebilir.</span><span class="sxs-lookup"><span data-stu-id="285a0-748">Any type of value can be converted, including objects and arrays.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-749">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-749">Return value</span></span>

<span data-ttu-id="285a0-750">Dönüştürülen değer dizesi.</span><span class="sxs-lookup"><span data-stu-id="285a0-750">A string of the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-751">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-751">Examples</span></span>

<span data-ttu-id="285a0-752">Aşağıdaki örnekte, farklı türlerdeki değerleri dizelere dönüştürme gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="285a0-752">The following example shows how to convert different types of values to strings:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testObject": {
            "type": "object",
            "defaultValue": {
                "valueA": 10,
                "valueB": "Example Text"
            }
        },
        "testArray": {
            "type": "array",
            "defaultValue": [
                "a",
                "b",
                "c"
            ]
        },
        "testInt": {
            "type": "int",
            "defaultValue": 5
        }
    },
    "resources": [],
    "outputs": {
        "objectOutput": {
            "type": "string",
            "value": "[string(parameters('testObject'))]"
        },
        "arrayOutput": {
            "type": "string",
            "value": "[string(parameters('testArray'))]"
        },
        "intOutput": {
            "type": "string",
            "value": "[string(parameters('testInt'))]"
        }
    }
}
```

<span data-ttu-id="285a0-753">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-753">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-754">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-754">Name</span></span> | <span data-ttu-id="285a0-755">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-755">Type</span></span> | <span data-ttu-id="285a0-756">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-756">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-757">objectOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-757">objectOutput</span></span> | <span data-ttu-id="285a0-758">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-758">String</span></span> | <span data-ttu-id="285a0-759">{"valueA": 10, "valueB": "Örnek metin"}</span><span class="sxs-lookup"><span data-stu-id="285a0-759">{"valueA":10,"valueB":"Example Text"}</span></span> |
| <span data-ttu-id="285a0-760">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-760">arrayOutput</span></span> | <span data-ttu-id="285a0-761">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-761">String</span></span> | <span data-ttu-id="285a0-762">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="285a0-762">["a","b","c"]</span></span> |
| <span data-ttu-id="285a0-763">intOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-763">intOutput</span></span> | <span data-ttu-id="285a0-764">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-764">String</span></span> | <span data-ttu-id="285a0-765">5</span><span class="sxs-lookup"><span data-stu-id="285a0-765">5</span></span> |

<a id="substring" />

## <a name="substring"></a><span data-ttu-id="285a0-766">substring</span><span class="sxs-lookup"><span data-stu-id="285a0-766">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="285a0-767">Belirtilen karakter konumunda başlayan ve belirtilen sayıda karakteri içeren bir alt dizeyi döndürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-767">Returns a substring that starts at the specified character position and contains the specified number of characters.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-768">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-768">Parameters</span></span>

| <span data-ttu-id="285a0-769">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-769">Parameter</span></span> | <span data-ttu-id="285a0-770">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-770">Required</span></span> | <span data-ttu-id="285a0-771">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-771">Type</span></span> | <span data-ttu-id="285a0-772">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-772">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-773">stringToParse</span><span class="sxs-lookup"><span data-stu-id="285a0-773">stringToParse</span></span> |<span data-ttu-id="285a0-774">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-774">Yes</span></span> |<span data-ttu-id="285a0-775">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-775">string</span></span> |<span data-ttu-id="285a0-776">Alt dizeyi ayıklandığı özgün dizesi.</span><span class="sxs-lookup"><span data-stu-id="285a0-776">The original string from which the substring is extracted.</span></span> |
| <span data-ttu-id="285a0-777">startIndex</span><span class="sxs-lookup"><span data-stu-id="285a0-777">startIndex</span></span> |<span data-ttu-id="285a0-778">Hayır</span><span class="sxs-lookup"><span data-stu-id="285a0-778">No</span></span> |<span data-ttu-id="285a0-779">Int</span><span class="sxs-lookup"><span data-stu-id="285a0-779">int</span></span> |<span data-ttu-id="285a0-780">Sıfır tabanlı başlangıç karakteri konumunu alt dizeyi.</span><span class="sxs-lookup"><span data-stu-id="285a0-780">The zero-based starting character position for the substring.</span></span> |
| <span data-ttu-id="285a0-781">uzunluğu</span><span class="sxs-lookup"><span data-stu-id="285a0-781">length</span></span> |<span data-ttu-id="285a0-782">Hayır</span><span class="sxs-lookup"><span data-stu-id="285a0-782">No</span></span> |<span data-ttu-id="285a0-783">Int</span><span class="sxs-lookup"><span data-stu-id="285a0-783">int</span></span> |<span data-ttu-id="285a0-784">Alt dizeyi karakter sayısı.</span><span class="sxs-lookup"><span data-stu-id="285a0-784">The number of characters for the substring.</span></span> <span data-ttu-id="285a0-785">Dize içinde bir konuma başvurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="285a0-785">Must refer to a location within the string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-786">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-786">Return value</span></span>

<span data-ttu-id="285a0-787">Alt dizeyi.</span><span class="sxs-lookup"><span data-stu-id="285a0-787">The substring.</span></span>

### <a name="remarks"></a><span data-ttu-id="285a0-788">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="285a0-788">Remarks</span></span>

<span data-ttu-id="285a0-789">Dize sonunu aşan alt dizeyi genişletir işlevi başarısız oluyor.</span><span class="sxs-lookup"><span data-stu-id="285a0-789">The function fails when the substring extends beyond the end of the string.</span></span> <span data-ttu-id="285a0-790">Aşağıdaki örnekte, "dizin ve uzunluk parametreleri dize içindeki bir konuma başvurmalıdır. şu hatayla başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="285a0-790">The following example fails with the error "The index and length parameters must refer to a location within the string.</span></span> <span data-ttu-id="285a0-791">Dizin parametresi: '0', uzunluk parametresi: '11', dize parametresinin uzunluğu: '10'. ".</span><span class="sxs-lookup"><span data-stu-id="285a0-791">The index parameter: '0', the length parameter: '11', the length of the string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a><span data-ttu-id="285a0-792">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-792">Examples</span></span>

<span data-ttu-id="285a0-793">Aşağıdaki örnek bir alt dizesi bir parametresinden ayıklar.</span><span class="sxs-lookup"><span data-stu-id="285a0-793">The following example extracts a substring from a parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        }
    },
    "resources": [],
    "outputs": {
        "substringOutput": {
            "value": "[substring(parameters('testString'), 4, 3)]",
            "type": "string"
        }
    }
}
```

<span data-ttu-id="285a0-794">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-794">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-795">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-795">Name</span></span> | <span data-ttu-id="285a0-796">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-796">Type</span></span> | <span data-ttu-id="285a0-797">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-797">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-798">substringOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-798">substringOutput</span></span> | <span data-ttu-id="285a0-799">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-799">String</span></span> | <span data-ttu-id="285a0-800">iki</span><span class="sxs-lookup"><span data-stu-id="285a0-800">two</span></span> |


<a id="take" />

## <a name="take"></a><span data-ttu-id="285a0-801">Al</span><span class="sxs-lookup"><span data-stu-id="285a0-801">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="285a0-802">Dize veya dizi öğeleri dizisi başından başlayarak belirtilen sayıda ile başından başlayarak belirtilen sayıda karakteri içeren bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-802">Returns a string with the specified number of characters from the start of the string, or an array with the specified number of elements from the start of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-803">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-803">Parameters</span></span>

| <span data-ttu-id="285a0-804">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-804">Parameter</span></span> | <span data-ttu-id="285a0-805">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-805">Required</span></span> | <span data-ttu-id="285a0-806">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-806">Type</span></span> | <span data-ttu-id="285a0-807">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-807">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-808">originalValue</span><span class="sxs-lookup"><span data-stu-id="285a0-808">originalValue</span></span> |<span data-ttu-id="285a0-809">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-809">Yes</span></span> |<span data-ttu-id="285a0-810">dizi veya dize</span><span class="sxs-lookup"><span data-stu-id="285a0-810">array or string</span></span> |<span data-ttu-id="285a0-811">Dizi veya dize öğeleri gerçekleştirilecek.</span><span class="sxs-lookup"><span data-stu-id="285a0-811">The array or string to take the elements from.</span></span> |
| <span data-ttu-id="285a0-812">numberToTake</span><span class="sxs-lookup"><span data-stu-id="285a0-812">numberToTake</span></span> |<span data-ttu-id="285a0-813">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-813">Yes</span></span> |<span data-ttu-id="285a0-814">Int</span><span class="sxs-lookup"><span data-stu-id="285a0-814">int</span></span> |<span data-ttu-id="285a0-815">Öğeleri veya yapılacak karakter sayısı.</span><span class="sxs-lookup"><span data-stu-id="285a0-815">The number of elements or characters to take.</span></span> <span data-ttu-id="285a0-816">Bu değer 0 veya daha az ise, boş dize veya dize döndürülür.</span><span class="sxs-lookup"><span data-stu-id="285a0-816">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="285a0-817">Verilen dizi veya dize uzunluğundan büyük olursa, dizi veya dize tüm öğeler döndürülür.</span><span class="sxs-lookup"><span data-stu-id="285a0-817">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-818">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-818">Return value</span></span>

<span data-ttu-id="285a0-819">Bir dizi veya dize.</span><span class="sxs-lookup"><span data-stu-id="285a0-819">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-820">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-820">Examples</span></span>

<span data-ttu-id="285a0-821">Aşağıdaki örnek, belirtilen sayıda dizisinden öğeleri ve bir dizeden karakterleri alır.</span><span class="sxs-lookup"><span data-stu-id="285a0-821">The following example takes the specified number of elements from the array, and characters from a string.</span></span>

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

<span data-ttu-id="285a0-822">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-822">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-823">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-823">Name</span></span> | <span data-ttu-id="285a0-824">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-824">Type</span></span> | <span data-ttu-id="285a0-825">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-825">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-826">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-826">arrayOutput</span></span> | <span data-ttu-id="285a0-827">Dizi</span><span class="sxs-lookup"><span data-stu-id="285a0-827">Array</span></span> | <span data-ttu-id="285a0-828">["", "iki"]</span><span class="sxs-lookup"><span data-stu-id="285a0-828">["one", "two"]</span></span> |
| <span data-ttu-id="285a0-829">stringOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-829">stringOutput</span></span> | <span data-ttu-id="285a0-830">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-830">String</span></span> | <span data-ttu-id="285a0-831">üzerinde</span><span class="sxs-lookup"><span data-stu-id="285a0-831">on</span></span> |

<a id="tolower" />

## <a name="tolower"></a><span data-ttu-id="285a0-832">toLower</span><span class="sxs-lookup"><span data-stu-id="285a0-832">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="285a0-833">Belirtilen dizeyi küçük harflere dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-833">Converts the specified string to lower case.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-834">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-834">Parameters</span></span>

| <span data-ttu-id="285a0-835">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-835">Parameter</span></span> | <span data-ttu-id="285a0-836">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-836">Required</span></span> | <span data-ttu-id="285a0-837">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-837">Type</span></span> | <span data-ttu-id="285a0-838">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-838">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-839">stringToChange</span><span class="sxs-lookup"><span data-stu-id="285a0-839">stringToChange</span></span> |<span data-ttu-id="285a0-840">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-840">Yes</span></span> |<span data-ttu-id="285a0-841">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-841">string</span></span> |<span data-ttu-id="285a0-842">Küçük harflere dönüştürülecek değer.</span><span class="sxs-lookup"><span data-stu-id="285a0-842">The value to convert to lower case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-843">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-843">Return value</span></span>

<span data-ttu-id="285a0-844">Dizeyi küçük harflere dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="285a0-844">The string converted to lower case.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-845">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-845">Examples</span></span>

<span data-ttu-id="285a0-846">Aşağıdaki örnekte bir parametre değeri, küçük harf ve büyük harfe dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-846">The following example converts a parameter value to lower case and to upper case.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="285a0-847">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-847">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-848">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-848">Name</span></span> | <span data-ttu-id="285a0-849">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-849">Type</span></span> | <span data-ttu-id="285a0-850">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-850">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-851">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-851">toLowerOutput</span></span> | <span data-ttu-id="285a0-852">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-852">String</span></span> | <span data-ttu-id="285a0-853">Bir iki üç</span><span class="sxs-lookup"><span data-stu-id="285a0-853">one two three</span></span> |
| <span data-ttu-id="285a0-854">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-854">toUpperOutput</span></span> | <span data-ttu-id="285a0-855">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-855">String</span></span> | <span data-ttu-id="285a0-856">BİR İKİ ÜÇ</span><span class="sxs-lookup"><span data-stu-id="285a0-856">ONE TWO THREE</span></span> |

<a id="toupper" />

## <a name="toupper"></a><span data-ttu-id="285a0-857">toUpper</span><span class="sxs-lookup"><span data-stu-id="285a0-857">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="285a0-858">Belirtilen dizenin büyük harfe dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-858">Converts the specified string to upper case.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-859">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-859">Parameters</span></span>

| <span data-ttu-id="285a0-860">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-860">Parameter</span></span> | <span data-ttu-id="285a0-861">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-861">Required</span></span> | <span data-ttu-id="285a0-862">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-862">Type</span></span> | <span data-ttu-id="285a0-863">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-863">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-864">stringToChange</span><span class="sxs-lookup"><span data-stu-id="285a0-864">stringToChange</span></span> |<span data-ttu-id="285a0-865">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-865">Yes</span></span> |<span data-ttu-id="285a0-866">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-866">string</span></span> |<span data-ttu-id="285a0-867">Büyük harfe dönüştürülecek değer.</span><span class="sxs-lookup"><span data-stu-id="285a0-867">The value to convert to upper case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-868">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-868">Return value</span></span>

<span data-ttu-id="285a0-869">Dizeyi büyük harfe dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="285a0-869">The string converted to upper case.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-870">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-870">Examples</span></span>

<span data-ttu-id="285a0-871">Aşağıdaki örnekte bir parametre değeri, küçük harf ve büyük harfe dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-871">The following example converts a parameter value to lower case and to upper case.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="285a0-872">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-872">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-873">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-873">Name</span></span> | <span data-ttu-id="285a0-874">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-874">Type</span></span> | <span data-ttu-id="285a0-875">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-875">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-876">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-876">toLowerOutput</span></span> | <span data-ttu-id="285a0-877">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-877">String</span></span> | <span data-ttu-id="285a0-878">Bir iki üç</span><span class="sxs-lookup"><span data-stu-id="285a0-878">one two three</span></span> |
| <span data-ttu-id="285a0-879">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-879">toUpperOutput</span></span> | <span data-ttu-id="285a0-880">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-880">String</span></span> | <span data-ttu-id="285a0-881">BİR İKİ ÜÇ</span><span class="sxs-lookup"><span data-stu-id="285a0-881">ONE TWO THREE</span></span> |

<a id="trim" />

## <a name="trim"></a><span data-ttu-id="285a0-882">Kırpma</span><span class="sxs-lookup"><span data-stu-id="285a0-882">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="285a0-883">Tüm öndeki ve sondaki boşluk karakterleri belirtilen dizeden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="285a0-883">Removes all leading and trailing white-space characters from the specified string.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-884">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-884">Parameters</span></span>

| <span data-ttu-id="285a0-885">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-885">Parameter</span></span> | <span data-ttu-id="285a0-886">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-886">Required</span></span> | <span data-ttu-id="285a0-887">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-887">Type</span></span> | <span data-ttu-id="285a0-888">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-888">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-889">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="285a0-889">stringToTrim</span></span> |<span data-ttu-id="285a0-890">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-890">Yes</span></span> |<span data-ttu-id="285a0-891">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-891">string</span></span> |<span data-ttu-id="285a0-892">Kesim değeri.</span><span class="sxs-lookup"><span data-stu-id="285a0-892">The value to trim.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-893">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-893">Return value</span></span>

<span data-ttu-id="285a0-894">Baştaki ve sondaki boşluk karakterleri olmadan dizesi.</span><span class="sxs-lookup"><span data-stu-id="285a0-894">The string without leading and trailing white-space characters.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-895">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-895">Examples</span></span>

<span data-ttu-id="285a0-896">Aşağıdaki örnek parametre boşluk karakterlerinden kırpar.</span><span class="sxs-lookup"><span data-stu-id="285a0-896">The following example trims the white-space characters from the parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "    one two three   "
        }
    },
    "resources": [],
    "outputs": {
        "return": {
            "type": "string",
            "value": "[trim(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="285a0-897">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-897">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-898">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-898">Name</span></span> | <span data-ttu-id="285a0-899">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-899">Type</span></span> | <span data-ttu-id="285a0-900">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-900">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-901">Döndür</span><span class="sxs-lookup"><span data-stu-id="285a0-901">return</span></span> | <span data-ttu-id="285a0-902">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-902">String</span></span> | <span data-ttu-id="285a0-903">Bir iki üç</span><span class="sxs-lookup"><span data-stu-id="285a0-903">one two three</span></span> |

<a id="uniquestring" />

## <a name="uniquestring"></a><span data-ttu-id="285a0-904">uniqueString</span><span class="sxs-lookup"><span data-stu-id="285a0-904">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="285a0-905">Parametre olarak sağlanan değerlere göre belirleyici karma dize oluşturur.</span><span class="sxs-lookup"><span data-stu-id="285a0-905">Creates a deterministic hash string based on the values provided as parameters.</span></span> 

### <a name="parameters"></a><span data-ttu-id="285a0-906">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-906">Parameters</span></span>

| <span data-ttu-id="285a0-907">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-907">Parameter</span></span> | <span data-ttu-id="285a0-908">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-908">Required</span></span> | <span data-ttu-id="285a0-909">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-909">Type</span></span> | <span data-ttu-id="285a0-910">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-910">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-911">baseString</span><span class="sxs-lookup"><span data-stu-id="285a0-911">baseString</span></span> |<span data-ttu-id="285a0-912">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-912">Yes</span></span> |<span data-ttu-id="285a0-913">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-913">string</span></span> |<span data-ttu-id="285a0-914">Karma işlevinde benzersiz bir dize oluşturmak için kullanılan değer.</span><span class="sxs-lookup"><span data-stu-id="285a0-914">The value used in the hash function to create a unique string.</span></span> |
| <span data-ttu-id="285a0-915">gerektikçe ek parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-915">additional parameters as needed</span></span> |<span data-ttu-id="285a0-916">Hayır</span><span class="sxs-lookup"><span data-stu-id="285a0-916">No</span></span> |<span data-ttu-id="285a0-917">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-917">string</span></span> |<span data-ttu-id="285a0-918">Benzersizlik düzeyini belirten değeri oluşturmak için gereken sayıda dizeleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="285a0-918">You can add as many strings as needed to create the value that specifies the level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="285a0-919">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="285a0-919">Remarks</span></span>

<span data-ttu-id="285a0-920">Bu işlev, bir kaynak için benzersiz bir ad oluşturmanız gerektiğinde faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="285a0-920">This function is helpful when you need to create a unique name for a resource.</span></span> <span data-ttu-id="285a0-921">Sonuç benzersizlik kapsamını sınırlamak parametre değerlerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="285a0-921">You provide parameter values that limit the scope of uniqueness for the result.</span></span> <span data-ttu-id="285a0-922">Adlı abonelik, kaynak grubu veya dağıtım için benzersiz olup olmadığını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="285a0-922">You can specify whether the name is unique down to subscription, resource group, or deployment.</span></span> 

<span data-ttu-id="285a0-923">Döndürülen değer rastgele bir dize, ancak bunun yerine bir karma işlevin sonucu değil.</span><span class="sxs-lookup"><span data-stu-id="285a0-923">The returned value is not a random string, but rather the result of a hash function.</span></span> <span data-ttu-id="285a0-924">Döndürülen değeri 13 karakter uzunluğunda ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="285a0-924">The returned value is 13 characters long.</span></span> <span data-ttu-id="285a0-925">Genel benzersiz değil.</span><span class="sxs-lookup"><span data-stu-id="285a0-925">It is not globally unique.</span></span> <span data-ttu-id="285a0-926">Anlamlı bir ad oluşturmak için adlandırma kuralınızın önekten değeri birleştirin isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="285a0-926">You may want to combine the value with a prefix from your naming convention to create a name that is meaningful.</span></span> <span data-ttu-id="285a0-927">Aşağıdaki örnek, döndürülen değer biçimi gösterir.</span><span class="sxs-lookup"><span data-stu-id="285a0-927">The following example shows the format of the returned value.</span></span> <span data-ttu-id="285a0-928">Gerçek değer sağlanan parametrelere göre değişir.</span><span class="sxs-lookup"><span data-stu-id="285a0-928">The actual value varies by the provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="285a0-929">Aşağıdaki örnekler uniqueString yaygın olarak kullanılan düzeyleri için benzersiz bir değer oluşturmak için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="285a0-929">The following examples show how to use uniqueString to create a unique value for commonly used levels.</span></span>

<span data-ttu-id="285a0-930">Aboneliği kapsamlıdır benzersiz</span><span class="sxs-lookup"><span data-stu-id="285a0-930">Unique scoped to subscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="285a0-931">Kaynak grubu için kapsamlı benzersiz</span><span class="sxs-lookup"><span data-stu-id="285a0-931">Unique scoped to resource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="285a0-932">Benzersiz bir kaynak grubu için dağıtım kapsamına</span><span class="sxs-lookup"><span data-stu-id="285a0-932">Unique scoped to deployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="285a0-933">Aşağıdaki örnekte, kaynak grubuna bağlı bir depolama hesabı için benzersiz bir ad oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="285a0-933">The following example shows how to create a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="285a0-934">Kaynak grubu içinde adı aynı şekilde oluşturulan varsa benzersiz değil.</span><span class="sxs-lookup"><span data-stu-id="285a0-934">Inside the resource group, the name is not unique if constructed the same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a><span data-ttu-id="285a0-935">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-935">Return value</span></span>

<span data-ttu-id="285a0-936">13 karakter içeren bir dize.</span><span class="sxs-lookup"><span data-stu-id="285a0-936">A string containing 13 characters.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-937">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-937">Examples</span></span>

<span data-ttu-id="285a0-938">Aşağıdaki örnek uniquestring sonuçları verir:</span><span class="sxs-lookup"><span data-stu-id="285a0-938">The following example returns results from uniquestring:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "uniqueRG": {
            "value": "[uniqueString(resourceGroup().id)]",
            "type" : "string"
        },
        "uniqueDeploy": {
            "value": "[uniqueString(resourceGroup().id, deployment().name)]",
            "type" : "string"
        }
    }
}
```

<a id="uri" />

## <a name="uri"></a><span data-ttu-id="285a0-939">URI</span><span class="sxs-lookup"><span data-stu-id="285a0-939">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="285a0-940">Bir mutlak URI tabanURI ve relativeUri dize birleştirerek oluşturur.</span><span class="sxs-lookup"><span data-stu-id="285a0-940">Creates an absolute URI by combining the baseUri and the relativeUri string.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-941">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-941">Parameters</span></span>

| <span data-ttu-id="285a0-942">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-942">Parameter</span></span> | <span data-ttu-id="285a0-943">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-943">Required</span></span> | <span data-ttu-id="285a0-944">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-944">Type</span></span> | <span data-ttu-id="285a0-945">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-945">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-946">tabanURI</span><span class="sxs-lookup"><span data-stu-id="285a0-946">baseUri</span></span> |<span data-ttu-id="285a0-947">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-947">Yes</span></span> |<span data-ttu-id="285a0-948">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-948">string</span></span> |<span data-ttu-id="285a0-949">Taban URI dizesi.</span><span class="sxs-lookup"><span data-stu-id="285a0-949">The base uri string.</span></span> |
| <span data-ttu-id="285a0-950">relativeUri</span><span class="sxs-lookup"><span data-stu-id="285a0-950">relativeUri</span></span> |<span data-ttu-id="285a0-951">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-951">Yes</span></span> |<span data-ttu-id="285a0-952">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-952">string</span></span> |<span data-ttu-id="285a0-953">İçin ana uri dizesi eklemek için göreli URI dizesi.</span><span class="sxs-lookup"><span data-stu-id="285a0-953">The relative uri string to add to the base uri string.</span></span> |

<span data-ttu-id="285a0-954">Değeri **tabanURI** parametresi, belirli bir dosya içerebilir, ancak yalnızca temel yolu URI oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="285a0-954">The value for the **baseUri** parameter can include a specific file, but only the base path is used when constructing the URI.</span></span> <span data-ttu-id="285a0-955">Örneğin, geçirme `http://contoso.com/resources/azuredeploy.json` temel URI'sini tabanURI parametre sonuçlarında olarak `http://contoso.com/resources/`.</span><span class="sxs-lookup"><span data-stu-id="285a0-955">For example, passing `http://contoso.com/resources/azuredeploy.json` as the baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

### <a name="return-value"></a><span data-ttu-id="285a0-956">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-956">Return value</span></span>

<span data-ttu-id="285a0-957">Temel ve göreli değerleri için mutlak URI temsil eden dize.</span><span class="sxs-lookup"><span data-stu-id="285a0-957">A string representing the absolute URI for the base and relative values.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-958">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-958">Examples</span></span>

<span data-ttu-id="285a0-959">Aşağıdaki örnek, üst şablon değere göre iç içe geçmiş bir şablon için bir bağlantı oluşturmak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="285a0-959">The following example shows how to construct a link to a nested template based on the value of the parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

<span data-ttu-id="285a0-960">Aşağıdaki örnek URI, uriComponent ve uriComponentToString nasıl kullanılacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="285a0-960">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="285a0-961">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-961">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-962">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-962">Name</span></span> | <span data-ttu-id="285a0-963">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-963">Type</span></span> | <span data-ttu-id="285a0-964">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-964">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-965">uriOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-965">uriOutput</span></span> | <span data-ttu-id="285a0-966">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-966">String</span></span> | <span data-ttu-id="285a0-967">http://contoso.com/resources/Nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="285a0-967">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="285a0-968">componentOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-968">componentOutput</span></span> | <span data-ttu-id="285a0-969">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-969">String</span></span> | <span data-ttu-id="285a0-970">HTTP%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="285a0-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="285a0-971">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-971">toStringOutput</span></span> | <span data-ttu-id="285a0-972">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-972">String</span></span> | <span data-ttu-id="285a0-973">http://contoso.com/resources/Nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="285a0-973">http://contoso.com/resources/nested/azuredeploy.json</span></span> |

<a id="uricomponent" />

## <a name="uricomponent"></a><span data-ttu-id="285a0-974">uriComponent</span><span class="sxs-lookup"><span data-stu-id="285a0-974">uriComponent</span></span>
`uricomponent(stringToEncode)`

<span data-ttu-id="285a0-975">Bir URI kodlar.</span><span class="sxs-lookup"><span data-stu-id="285a0-975">Encodes a URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-976">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-976">Parameters</span></span>

| <span data-ttu-id="285a0-977">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-977">Parameter</span></span> | <span data-ttu-id="285a0-978">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-978">Required</span></span> | <span data-ttu-id="285a0-979">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-979">Type</span></span> | <span data-ttu-id="285a0-980">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-980">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-981">stringToEncode</span><span class="sxs-lookup"><span data-stu-id="285a0-981">stringToEncode</span></span> |<span data-ttu-id="285a0-982">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-982">Yes</span></span> |<span data-ttu-id="285a0-983">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-983">string</span></span> |<span data-ttu-id="285a0-984">Kodlanacak değeri.</span><span class="sxs-lookup"><span data-stu-id="285a0-984">The value to encode.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-985">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-985">Return value</span></span>

<span data-ttu-id="285a0-986">URI'ın bir dize değeri kodlanmış.</span><span class="sxs-lookup"><span data-stu-id="285a0-986">A string of the URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-987">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-987">Examples</span></span>

<span data-ttu-id="285a0-988">Aşağıdaki örnek URI, uriComponent ve uriComponentToString nasıl kullanılacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="285a0-988">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="285a0-989">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-989">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-990">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-990">Name</span></span> | <span data-ttu-id="285a0-991">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-991">Type</span></span> | <span data-ttu-id="285a0-992">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-992">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-993">uriOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-993">uriOutput</span></span> | <span data-ttu-id="285a0-994">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-994">String</span></span> | <span data-ttu-id="285a0-995">http://contoso.com/resources/Nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="285a0-995">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="285a0-996">componentOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-996">componentOutput</span></span> | <span data-ttu-id="285a0-997">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-997">String</span></span> | <span data-ttu-id="285a0-998">HTTP%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="285a0-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="285a0-999">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-999">toStringOutput</span></span> | <span data-ttu-id="285a0-1000">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-1000">String</span></span> | <span data-ttu-id="285a0-1001">http://contoso.com/resources/Nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="285a0-1001">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a><span data-ttu-id="285a0-1002">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="285a0-1002">uriComponentToString</span></span>
`uriComponentToString(uriEncodedString)`

<span data-ttu-id="285a0-1003">Değer bir dize bir URI kodlanmış döndürür.</span><span class="sxs-lookup"><span data-stu-id="285a0-1003">Returns a string of a URI encoded value.</span></span>

### <a name="parameters"></a><span data-ttu-id="285a0-1004">Parametreler</span><span class="sxs-lookup"><span data-stu-id="285a0-1004">Parameters</span></span>

| <span data-ttu-id="285a0-1005">Parametre</span><span class="sxs-lookup"><span data-stu-id="285a0-1005">Parameter</span></span> | <span data-ttu-id="285a0-1006">Gerekli</span><span class="sxs-lookup"><span data-stu-id="285a0-1006">Required</span></span> | <span data-ttu-id="285a0-1007">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-1007">Type</span></span> | <span data-ttu-id="285a0-1008">Açıklama</span><span class="sxs-lookup"><span data-stu-id="285a0-1008">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="285a0-1009">uriEncodedString</span><span class="sxs-lookup"><span data-stu-id="285a0-1009">uriEncodedString</span></span> |<span data-ttu-id="285a0-1010">Evet</span><span class="sxs-lookup"><span data-stu-id="285a0-1010">Yes</span></span> |<span data-ttu-id="285a0-1011">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-1011">string</span></span> |<span data-ttu-id="285a0-1012">URI değeri dizeye dönüştürmek için kodlanmış.</span><span class="sxs-lookup"><span data-stu-id="285a0-1012">The URI encoded value to convert to a string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="285a0-1013">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="285a0-1013">Return value</span></span>

<span data-ttu-id="285a0-1014">Bir URI kodu çözülmüş bir dize değeri kodlanmış.</span><span class="sxs-lookup"><span data-stu-id="285a0-1014">A decoded string of URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="285a0-1015">Örnekler</span><span class="sxs-lookup"><span data-stu-id="285a0-1015">Examples</span></span>

<span data-ttu-id="285a0-1016">Aşağıdaki örnek URI, uriComponent ve uriComponentToString nasıl kullanılacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="285a0-1016">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="285a0-1017">Varsayılan değerlerle önceki örnekten çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="285a0-1017">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="285a0-1018">Ad</span><span class="sxs-lookup"><span data-stu-id="285a0-1018">Name</span></span> | <span data-ttu-id="285a0-1019">Tür</span><span class="sxs-lookup"><span data-stu-id="285a0-1019">Type</span></span> | <span data-ttu-id="285a0-1020">Değer</span><span class="sxs-lookup"><span data-stu-id="285a0-1020">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="285a0-1021">uriOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-1021">uriOutput</span></span> | <span data-ttu-id="285a0-1022">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-1022">String</span></span> | <span data-ttu-id="285a0-1023">http://contoso.com/resources/Nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="285a0-1023">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="285a0-1024">componentOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-1024">componentOutput</span></span> | <span data-ttu-id="285a0-1025">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-1025">String</span></span> | <span data-ttu-id="285a0-1026">HTTP%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="285a0-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="285a0-1027">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="285a0-1027">toStringOutput</span></span> | <span data-ttu-id="285a0-1028">Dize</span><span class="sxs-lookup"><span data-stu-id="285a0-1028">String</span></span> | <span data-ttu-id="285a0-1029">http://contoso.com/resources/Nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="285a0-1029">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


## <a name="next-steps"></a><span data-ttu-id="285a0-1030">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="285a0-1030">Next steps</span></span>
* <span data-ttu-id="285a0-1031">Bir Azure Resource Manager şablonu bölümlerde açıklaması için bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="285a0-1031">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="285a0-1032">Birden fazla şablon birleştirmek için bkz: [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="285a0-1032">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="285a0-1033">Belirtilen sayıda yinelemek için kaynak türünü oluştururken bkz [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="285a0-1033">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="285a0-1034">Oluşturduğunuz şablon dağıtma hakkında bilgi için bkz: [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="285a0-1034">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

