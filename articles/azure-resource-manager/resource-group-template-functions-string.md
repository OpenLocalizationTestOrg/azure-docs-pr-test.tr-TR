---
title: "dize aaaAzure Resource Manager şablonu işlevleri - | Microsoft Docs"
description: "Bir Azure Resource Manager şablonu toowork dizeler içindeki Hello işlevleri toouse açıklar."
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
ms.openlocfilehash: 27f7f6a52cbe4e9915718184433e92ca92999346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="abfee-103">Azure Resource Manager şablonları için dize işlevleri</span><span class="sxs-lookup"><span data-stu-id="abfee-103">String functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="abfee-104">Resource Manager Dizelerle çalışmaya yönelik işlevler aşağıdaki hello sunar:</span><span class="sxs-lookup"><span data-stu-id="abfee-104">Resource Manager provides hello following functions for working with strings:</span></span>

* [<span data-ttu-id="abfee-105">Base64</span><span class="sxs-lookup"><span data-stu-id="abfee-105">base64</span></span>](#base64)
* [<span data-ttu-id="abfee-106">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="abfee-106">base64ToJson</span></span>](#base64tojson)
* [<span data-ttu-id="abfee-107">base64ToString</span><span class="sxs-lookup"><span data-stu-id="abfee-107">base64ToString</span></span>](#base64tostring)
* [<span data-ttu-id="abfee-108">concat</span><span class="sxs-lookup"><span data-stu-id="abfee-108">concat</span></span>](#concat)
* [<span data-ttu-id="abfee-109">içerir</span><span class="sxs-lookup"><span data-stu-id="abfee-109">contains</span></span>](#contains)
* [<span data-ttu-id="abfee-110">dataUri</span><span class="sxs-lookup"><span data-stu-id="abfee-110">dataUri</span></span>](#datauri)
* [<span data-ttu-id="abfee-111">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="abfee-111">dataUriToString</span></span>](#datauritostring)
* [<span data-ttu-id="abfee-112">boş</span><span class="sxs-lookup"><span data-stu-id="abfee-112">empty</span></span>](#empty)
* [<span data-ttu-id="abfee-113">endsWith</span><span class="sxs-lookup"><span data-stu-id="abfee-113">endsWith</span></span>](#endswith)
* [<span data-ttu-id="abfee-114">ilk</span><span class="sxs-lookup"><span data-stu-id="abfee-114">first</span></span>](#first)
* [<span data-ttu-id="abfee-115">IndexOf</span><span class="sxs-lookup"><span data-stu-id="abfee-115">indexOf</span></span>](#indexof)
* [<span data-ttu-id="abfee-116">Son</span><span class="sxs-lookup"><span data-stu-id="abfee-116">last</span></span>](#last)
* [<span data-ttu-id="abfee-117">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="abfee-117">lastIndexOf</span></span>](#lastindexof)
* [<span data-ttu-id="abfee-118">uzunluğu</span><span class="sxs-lookup"><span data-stu-id="abfee-118">length</span></span>](#length)
* [<span data-ttu-id="abfee-119">padLeft</span><span class="sxs-lookup"><span data-stu-id="abfee-119">padLeft</span></span>](#padleft)
* [<span data-ttu-id="abfee-120">Değiştir</span><span class="sxs-lookup"><span data-stu-id="abfee-120">replace</span></span>](#replace)
* [<span data-ttu-id="abfee-121">Atla</span><span class="sxs-lookup"><span data-stu-id="abfee-121">skip</span></span>](#skip)
* [<span data-ttu-id="abfee-122">split</span><span class="sxs-lookup"><span data-stu-id="abfee-122">split</span></span>](#split)
* [<span data-ttu-id="abfee-123">startsWith</span><span class="sxs-lookup"><span data-stu-id="abfee-123">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="abfee-124">dize</span><span class="sxs-lookup"><span data-stu-id="abfee-124">string</span></span>](#string)
* [<span data-ttu-id="abfee-125">substring</span><span class="sxs-lookup"><span data-stu-id="abfee-125">substring</span></span>](#substring)
* [<span data-ttu-id="abfee-126">Al</span><span class="sxs-lookup"><span data-stu-id="abfee-126">take</span></span>](#take)
* [<span data-ttu-id="abfee-127">toLower</span><span class="sxs-lookup"><span data-stu-id="abfee-127">toLower</span></span>](#tolower)
* [<span data-ttu-id="abfee-128">toUpper</span><span class="sxs-lookup"><span data-stu-id="abfee-128">toUpper</span></span>](#toupper)
* [<span data-ttu-id="abfee-129">Kırpma</span><span class="sxs-lookup"><span data-stu-id="abfee-129">trim</span></span>](#trim)
* [<span data-ttu-id="abfee-130">uniqueString</span><span class="sxs-lookup"><span data-stu-id="abfee-130">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="abfee-131">URI</span><span class="sxs-lookup"><span data-stu-id="abfee-131">uri</span></span>](#uri)
* [<span data-ttu-id="abfee-132">uriComponent</span><span class="sxs-lookup"><span data-stu-id="abfee-132">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="abfee-133">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="abfee-133">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a><span data-ttu-id="abfee-134">Base64</span><span class="sxs-lookup"><span data-stu-id="abfee-134">base64</span></span>
`base64(inputString)`

<span data-ttu-id="abfee-135">Base64 hello giriş dize gösterimini döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="abfee-135">Returns hello base64 representation of hello input string.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-136">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-136">Parameters</span></span>

| <span data-ttu-id="abfee-137">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-137">Parameter</span></span> | <span data-ttu-id="abfee-138">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-138">Required</span></span> | <span data-ttu-id="abfee-139">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-139">Type</span></span> | <span data-ttu-id="abfee-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-140">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-141">inputString</span><span class="sxs-lookup"><span data-stu-id="abfee-141">inputString</span></span> |<span data-ttu-id="abfee-142">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-142">Yes</span></span> |<span data-ttu-id="abfee-143">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-143">string</span></span> |<span data-ttu-id="abfee-144">değer tooreturn base64 gösterimi olarak hello.</span><span class="sxs-lookup"><span data-stu-id="abfee-144">hello value tooreturn as a base64 representation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-145">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-145">Return value</span></span>

<span data-ttu-id="abfee-146">Merhaba base64 gösterimi içeren bir dize.</span><span class="sxs-lookup"><span data-stu-id="abfee-146">A string containing hello base64 representation.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-147">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-147">Examples</span></span>

<span data-ttu-id="abfee-148">Aşağıdaki örnek hello nasıl toouse hello base64 işlevi gösterir.</span><span class="sxs-lookup"><span data-stu-id="abfee-148">hello following example shows how toouse hello base64 function.</span></span>

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

<span data-ttu-id="abfee-149">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-149">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-150">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-150">Name</span></span> | <span data-ttu-id="abfee-151">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-151">Type</span></span> | <span data-ttu-id="abfee-152">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-153">base64Output</span><span class="sxs-lookup"><span data-stu-id="abfee-153">base64Output</span></span> | <span data-ttu-id="abfee-154">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-154">String</span></span> | <span data-ttu-id="abfee-155">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="abfee-155">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="abfee-156">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-156">toStringOutput</span></span> | <span data-ttu-id="abfee-157">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-157">String</span></span> | <span data-ttu-id="abfee-158">Bir iki üç</span><span class="sxs-lookup"><span data-stu-id="abfee-158">one, two, three</span></span> |
| <span data-ttu-id="abfee-159">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-159">toJsonOutput</span></span> | <span data-ttu-id="abfee-160">Nesne</span><span class="sxs-lookup"><span data-stu-id="abfee-160">Object</span></span> | <span data-ttu-id="abfee-161">{"bir": "a", "iki": "b"}</span><span class="sxs-lookup"><span data-stu-id="abfee-161">{"one": "a", "two": "b"}</span></span> |

<a id="base64tojson" />

## <a name="base64tojson"></a><span data-ttu-id="abfee-162">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="abfee-162">base64ToJson</span></span>
`base64tojson`

<span data-ttu-id="abfee-163">Bir base64 gösterimi tooa JSON nesnesi dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="abfee-163">Converts a base64 representation tooa JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-164">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-164">Parameters</span></span>

| <span data-ttu-id="abfee-165">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-165">Parameter</span></span> | <span data-ttu-id="abfee-166">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-166">Required</span></span> | <span data-ttu-id="abfee-167">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-167">Type</span></span> | <span data-ttu-id="abfee-168">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-168">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-169">base64value değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-169">base64Value</span></span> |<span data-ttu-id="abfee-170">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-170">Yes</span></span> |<span data-ttu-id="abfee-171">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-171">string</span></span> |<span data-ttu-id="abfee-172">Merhaba base64 gösterimi tooconvert tooa JSON nesnesi.</span><span class="sxs-lookup"><span data-stu-id="abfee-172">hello base64 representation tooconvert tooa JSON object.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-173">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-173">Return value</span></span>

<span data-ttu-id="abfee-174">Bir JSON nesnesi.</span><span class="sxs-lookup"><span data-stu-id="abfee-174">A JSON object.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-175">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-175">Examples</span></span>

<span data-ttu-id="abfee-176">Merhaba aşağıdaki örnek hello base64ToJson işlevi tooconvert bir base64 değeri kullanır:</span><span class="sxs-lookup"><span data-stu-id="abfee-176">hello following example uses hello base64ToJson function tooconvert a base64 value:</span></span>

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

<span data-ttu-id="abfee-177">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-177">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-178">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-178">Name</span></span> | <span data-ttu-id="abfee-179">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-179">Type</span></span> | <span data-ttu-id="abfee-180">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-180">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-181">base64Output</span><span class="sxs-lookup"><span data-stu-id="abfee-181">base64Output</span></span> | <span data-ttu-id="abfee-182">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-182">String</span></span> | <span data-ttu-id="abfee-183">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="abfee-183">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="abfee-184">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-184">toStringOutput</span></span> | <span data-ttu-id="abfee-185">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-185">String</span></span> | <span data-ttu-id="abfee-186">Bir iki üç</span><span class="sxs-lookup"><span data-stu-id="abfee-186">one, two, three</span></span> |
| <span data-ttu-id="abfee-187">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-187">toJsonOutput</span></span> | <span data-ttu-id="abfee-188">Nesne</span><span class="sxs-lookup"><span data-stu-id="abfee-188">Object</span></span> | <span data-ttu-id="abfee-189">{"bir": "a", "iki": "b"}</span><span class="sxs-lookup"><span data-stu-id="abfee-189">{"one": "a", "two": "b"}</span></span> |

<a id="base64tostring" />

## <a name="base64tostring"></a><span data-ttu-id="abfee-190">base64ToString</span><span class="sxs-lookup"><span data-stu-id="abfee-190">base64ToString</span></span>
`base64ToString(base64Value)`

<span data-ttu-id="abfee-191">Bir base64 gösterimi tooa dizesini sayıya dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="abfee-191">Converts a base64 representation tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-192">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-192">Parameters</span></span>

| <span data-ttu-id="abfee-193">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-193">Parameter</span></span> | <span data-ttu-id="abfee-194">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-194">Required</span></span> | <span data-ttu-id="abfee-195">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-195">Type</span></span> | <span data-ttu-id="abfee-196">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-196">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-197">base64value değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-197">base64Value</span></span> |<span data-ttu-id="abfee-198">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-198">Yes</span></span> |<span data-ttu-id="abfee-199">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-199">string</span></span> |<span data-ttu-id="abfee-200">Merhaba base64 gösterimi tooconvert tooa dizesi.</span><span class="sxs-lookup"><span data-stu-id="abfee-200">hello base64 representation tooconvert tooa string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-201">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-201">Return value</span></span>

<span data-ttu-id="abfee-202">Dönüştürülen bir base64 değeri hello dizesi.</span><span class="sxs-lookup"><span data-stu-id="abfee-202">A string of hello converted base64 value.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-203">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-203">Examples</span></span>

<span data-ttu-id="abfee-204">Merhaba aşağıdaki örnek hello base64ToString işlevi tooconvert bir base64 değeri kullanır:</span><span class="sxs-lookup"><span data-stu-id="abfee-204">hello following example uses hello base64ToString function tooconvert a base64 value:</span></span>

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

<span data-ttu-id="abfee-205">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-205">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-206">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-206">Name</span></span> | <span data-ttu-id="abfee-207">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-207">Type</span></span> | <span data-ttu-id="abfee-208">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-208">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-209">base64Output</span><span class="sxs-lookup"><span data-stu-id="abfee-209">base64Output</span></span> | <span data-ttu-id="abfee-210">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-210">String</span></span> | <span data-ttu-id="abfee-211">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="abfee-211">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="abfee-212">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-212">toStringOutput</span></span> | <span data-ttu-id="abfee-213">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-213">String</span></span> | <span data-ttu-id="abfee-214">Bir iki üç</span><span class="sxs-lookup"><span data-stu-id="abfee-214">one, two, three</span></span> |
| <span data-ttu-id="abfee-215">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-215">toJsonOutput</span></span> | <span data-ttu-id="abfee-216">Nesne</span><span class="sxs-lookup"><span data-stu-id="abfee-216">Object</span></span> | <span data-ttu-id="abfee-217">{"bir": "a", "iki": "b"}</span><span class="sxs-lookup"><span data-stu-id="abfee-217">{"one": "a", "two": "b"}</span></span> |



<a id="concat" />

## <a name="concat"></a><span data-ttu-id="abfee-218">concat</span><span class="sxs-lookup"><span data-stu-id="abfee-218">concat</span></span>
`concat (arg1, arg2, arg3, ...)`

<span data-ttu-id="abfee-219">Birden çok dize değerlerini birleştirir ve hello birleştirilmiş dizeyi döndürür veya birden çok birleştirir ve birleştirilmiş hello dizisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="abfee-219">Combines multiple string values and returns hello concatenated string, or combines multiple arrays and returns hello concatenated array.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-220">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-220">Parameters</span></span>

| <span data-ttu-id="abfee-221">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-221">Parameter</span></span> | <span data-ttu-id="abfee-222">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-222">Required</span></span> | <span data-ttu-id="abfee-223">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-223">Type</span></span> | <span data-ttu-id="abfee-224">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-224">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-225">arg1</span><span class="sxs-lookup"><span data-stu-id="abfee-225">arg1</span></span> |<span data-ttu-id="abfee-226">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-226">Yes</span></span> |<span data-ttu-id="abfee-227">dize veya dizi</span><span class="sxs-lookup"><span data-stu-id="abfee-227">string or array</span></span> |<span data-ttu-id="abfee-228">Merhaba birleştirme için ilk değer.</span><span class="sxs-lookup"><span data-stu-id="abfee-228">hello first value for concatenation.</span></span> |
| <span data-ttu-id="abfee-229">Ek bağımsız değişkenler</span><span class="sxs-lookup"><span data-stu-id="abfee-229">additional arguments</span></span> |<span data-ttu-id="abfee-230">Hayır</span><span class="sxs-lookup"><span data-stu-id="abfee-230">No</span></span> |<span data-ttu-id="abfee-231">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-231">string</span></span> |<span data-ttu-id="abfee-232">Birleştirme için sıralı bir düzende ek değerler.</span><span class="sxs-lookup"><span data-stu-id="abfee-232">Additional values in sequential order for concatenation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-233">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-233">Return value</span></span>
<span data-ttu-id="abfee-234">Bir dize veya birleştirilmiş değerleri dizisi.</span><span class="sxs-lookup"><span data-stu-id="abfee-234">A string or array of concatenated values.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-235">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-235">Examples</span></span>

<span data-ttu-id="abfee-236">Aşağıdaki örnek hello nasıl toocombine iki string değerleri ve birleştirilmiş dizeyi döndürür gösterir.</span><span class="sxs-lookup"><span data-stu-id="abfee-236">hello following example shows how toocombine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="abfee-237">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-237">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-238">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-238">Name</span></span> | <span data-ttu-id="abfee-239">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-239">Type</span></span> | <span data-ttu-id="abfee-240">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-240">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-241">concatOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-241">concatOutput</span></span> | <span data-ttu-id="abfee-242">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-242">String</span></span> | <span data-ttu-id="abfee-243">önek 5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="abfee-243">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="abfee-244">Aşağıdaki örnek hello nasıl toocombine iki dizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="abfee-244">hello following example shows how toocombine two arrays.</span></span>

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

<span data-ttu-id="abfee-245">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-245">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-246">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-246">Name</span></span> | <span data-ttu-id="abfee-247">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-247">Type</span></span> | <span data-ttu-id="abfee-248">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-249">Döndür</span><span class="sxs-lookup"><span data-stu-id="abfee-249">return</span></span> | <span data-ttu-id="abfee-250">Dizi</span><span class="sxs-lookup"><span data-stu-id="abfee-250">Array</span></span> | <span data-ttu-id="abfee-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="abfee-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="abfee-252">içerir</span><span class="sxs-lookup"><span data-stu-id="abfee-252">contains</span></span>
`contains (container, itemToFind)`

<span data-ttu-id="abfee-253">Bir değer dizisini içerir, bir nesne bir anahtar veya bir dize bir alt dizeyi içeren olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="abfee-253">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-254">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-254">Parameters</span></span>

| <span data-ttu-id="abfee-255">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-255">Parameter</span></span> | <span data-ttu-id="abfee-256">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-256">Required</span></span> | <span data-ttu-id="abfee-257">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-257">Type</span></span> | <span data-ttu-id="abfee-258">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-258">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-259">kapsayıcı</span><span class="sxs-lookup"><span data-stu-id="abfee-259">container</span></span> |<span data-ttu-id="abfee-260">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-260">Yes</span></span> |<span data-ttu-id="abfee-261">dizi, nesne veya dize</span><span class="sxs-lookup"><span data-stu-id="abfee-261">array, object, or string</span></span> |<span data-ttu-id="abfee-262">Merhaba değeri toofind içeren hello değeri.</span><span class="sxs-lookup"><span data-stu-id="abfee-262">hello value that contains hello value toofind.</span></span> |
| <span data-ttu-id="abfee-263">itemToFind</span><span class="sxs-lookup"><span data-stu-id="abfee-263">itemToFind</span></span> |<span data-ttu-id="abfee-264">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-264">Yes</span></span> |<span data-ttu-id="abfee-265">dize veya int</span><span class="sxs-lookup"><span data-stu-id="abfee-265">string or int</span></span> |<span data-ttu-id="abfee-266">Merhaba değeri toofind.</span><span class="sxs-lookup"><span data-stu-id="abfee-266">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-267">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-267">Return value</span></span>

<span data-ttu-id="abfee-268">**Doğru** hello öğe bulunduysa, **False**.</span><span class="sxs-lookup"><span data-stu-id="abfee-268">**True** if hello item is found; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-269">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-269">Examples</span></span>

<span data-ttu-id="abfee-270">Merhaba aşağıdaki örnekte nasıl toouse farklı türleriyle içeren gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="abfee-270">hello following example shows how toouse contains with different types:</span></span>

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

<span data-ttu-id="abfee-271">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-271">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-272">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-272">Name</span></span> | <span data-ttu-id="abfee-273">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-273">Type</span></span> | <span data-ttu-id="abfee-274">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-274">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-275">stringTrue</span><span class="sxs-lookup"><span data-stu-id="abfee-275">stringTrue</span></span> | <span data-ttu-id="abfee-276">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-276">Bool</span></span> | <span data-ttu-id="abfee-277">True</span><span class="sxs-lookup"><span data-stu-id="abfee-277">True</span></span> |
| <span data-ttu-id="abfee-278">stringFalse</span><span class="sxs-lookup"><span data-stu-id="abfee-278">stringFalse</span></span> | <span data-ttu-id="abfee-279">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-279">Bool</span></span> | <span data-ttu-id="abfee-280">False</span><span class="sxs-lookup"><span data-stu-id="abfee-280">False</span></span> |
| <span data-ttu-id="abfee-281">objectTrue</span><span class="sxs-lookup"><span data-stu-id="abfee-281">objectTrue</span></span> | <span data-ttu-id="abfee-282">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-282">Bool</span></span> | <span data-ttu-id="abfee-283">True</span><span class="sxs-lookup"><span data-stu-id="abfee-283">True</span></span> |
| <span data-ttu-id="abfee-284">objectFalse</span><span class="sxs-lookup"><span data-stu-id="abfee-284">objectFalse</span></span> | <span data-ttu-id="abfee-285">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-285">Bool</span></span> | <span data-ttu-id="abfee-286">False</span><span class="sxs-lookup"><span data-stu-id="abfee-286">False</span></span> |
| <span data-ttu-id="abfee-287">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="abfee-287">arrayTrue</span></span> | <span data-ttu-id="abfee-288">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-288">Bool</span></span> | <span data-ttu-id="abfee-289">True</span><span class="sxs-lookup"><span data-stu-id="abfee-289">True</span></span> |
| <span data-ttu-id="abfee-290">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="abfee-290">arrayFalse</span></span> | <span data-ttu-id="abfee-291">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-291">Bool</span></span> | <span data-ttu-id="abfee-292">False</span><span class="sxs-lookup"><span data-stu-id="abfee-292">False</span></span> |

<a id="datauri" />

## <a name="datauri"></a><span data-ttu-id="abfee-293">dataUri</span><span class="sxs-lookup"><span data-stu-id="abfee-293">dataUri</span></span>
`dataUri(stringToConvert)`

<span data-ttu-id="abfee-294">Bir değer tooa verisi URI dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="abfee-294">Converts a value tooa data URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-295">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-295">Parameters</span></span>

| <span data-ttu-id="abfee-296">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-296">Parameter</span></span> | <span data-ttu-id="abfee-297">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-297">Required</span></span> | <span data-ttu-id="abfee-298">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-298">Type</span></span> | <span data-ttu-id="abfee-299">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-299">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-300">stringToConvert</span><span class="sxs-lookup"><span data-stu-id="abfee-300">stringToConvert</span></span> |<span data-ttu-id="abfee-301">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-301">Yes</span></span> |<span data-ttu-id="abfee-302">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-302">string</span></span> |<span data-ttu-id="abfee-303">Merhaba değeri tooconvert tooa veri URI'si.</span><span class="sxs-lookup"><span data-stu-id="abfee-303">hello value tooconvert tooa data URI.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-304">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-304">Return value</span></span>

<span data-ttu-id="abfee-305">Veri URI'si biçimlendirilmiş bir dize.</span><span class="sxs-lookup"><span data-stu-id="abfee-305">A string formatted as a data URI.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-306">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-306">Examples</span></span>

<span data-ttu-id="abfee-307">Aşağıdaki örneğine hello değeri tooa verileri URI dönüştürür ve verileri URI tooa dize dönüştürür:</span><span class="sxs-lookup"><span data-stu-id="abfee-307">hello following example converts a value tooa data URI, and converts a data URI tooa string:</span></span>

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

<span data-ttu-id="abfee-308">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-308">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-309">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-309">Name</span></span> | <span data-ttu-id="abfee-310">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-310">Type</span></span> | <span data-ttu-id="abfee-311">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-311">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-312">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-312">dataUriOutput</span></span> | <span data-ttu-id="abfee-313">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-313">String</span></span> | <span data-ttu-id="abfee-314">Veri: metin / düz; charset = utf8; base64, SGVsbG8 =</span><span class="sxs-lookup"><span data-stu-id="abfee-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="abfee-315">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-315">toStringOutput</span></span> | <span data-ttu-id="abfee-316">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-316">String</span></span> | <span data-ttu-id="abfee-317">Merhaba Dünya!</span><span class="sxs-lookup"><span data-stu-id="abfee-317">Hello, World!</span></span> |

<a id="datauritostring" />

## <a name="datauritostring"></a><span data-ttu-id="abfee-318">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="abfee-318">dataUriToString</span></span>
`dataUriToString(dataUriToConvert)`

<span data-ttu-id="abfee-319">Biçimlendirilmiş değer tooa dize veri URI dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="abfee-319">Converts a data URI formatted value tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-320">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-320">Parameters</span></span>

| <span data-ttu-id="abfee-321">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-321">Parameter</span></span> | <span data-ttu-id="abfee-322">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-322">Required</span></span> | <span data-ttu-id="abfee-323">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-323">Type</span></span> | <span data-ttu-id="abfee-324">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-324">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-325">dataUriToConvert</span><span class="sxs-lookup"><span data-stu-id="abfee-325">dataUriToConvert</span></span> |<span data-ttu-id="abfee-326">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-326">Yes</span></span> |<span data-ttu-id="abfee-327">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-327">string</span></span> |<span data-ttu-id="abfee-328">Merhaba veri URI tooconvert değeri.</span><span class="sxs-lookup"><span data-stu-id="abfee-328">hello data URI value tooconvert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-329">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-329">Return value</span></span>

<span data-ttu-id="abfee-330">Merhaba içeren bir dize değeri dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="abfee-330">A string containing hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-331">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-331">Examples</span></span>

<span data-ttu-id="abfee-332">Aşağıdaki örneğine hello değeri tooa verileri URI dönüştürür ve verileri URI tooa dize dönüştürür:</span><span class="sxs-lookup"><span data-stu-id="abfee-332">hello following example converts a value tooa data URI, and converts a data URI tooa string:</span></span>

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

<span data-ttu-id="abfee-333">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-333">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-334">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-334">Name</span></span> | <span data-ttu-id="abfee-335">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-335">Type</span></span> | <span data-ttu-id="abfee-336">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-336">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-337">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-337">dataUriOutput</span></span> | <span data-ttu-id="abfee-338">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-338">String</span></span> | <span data-ttu-id="abfee-339">Veri: metin / düz; charset = utf8; base64, SGVsbG8 =</span><span class="sxs-lookup"><span data-stu-id="abfee-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="abfee-340">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-340">toStringOutput</span></span> | <span data-ttu-id="abfee-341">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-341">String</span></span> | <span data-ttu-id="abfee-342">Merhaba Dünya!</span><span class="sxs-lookup"><span data-stu-id="abfee-342">Hello, World!</span></span> |

<a id="empty" /> 

## <a name="empty"></a><span data-ttu-id="abfee-343">boş</span><span class="sxs-lookup"><span data-stu-id="abfee-343">empty</span></span>
`empty(itemToTest)`

<span data-ttu-id="abfee-344">Bir dizi, nesne veya dize boş olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="abfee-344">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-345">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-345">Parameters</span></span>

| <span data-ttu-id="abfee-346">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-346">Parameter</span></span> | <span data-ttu-id="abfee-347">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-347">Required</span></span> | <span data-ttu-id="abfee-348">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-348">Type</span></span> | <span data-ttu-id="abfee-349">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-349">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-350">itemToTest</span><span class="sxs-lookup"><span data-stu-id="abfee-350">itemToTest</span></span> |<span data-ttu-id="abfee-351">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-351">Yes</span></span> |<span data-ttu-id="abfee-352">dizi, nesne veya dize</span><span class="sxs-lookup"><span data-stu-id="abfee-352">array, object, or string</span></span> |<span data-ttu-id="abfee-353">boş ise, değer toocheck hello.</span><span class="sxs-lookup"><span data-stu-id="abfee-353">hello value toocheck if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-354">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-354">Return value</span></span>

<span data-ttu-id="abfee-355">Döndürür **True** hello değeriyse, boş, aksi takdirde **False**.</span><span class="sxs-lookup"><span data-stu-id="abfee-355">Returns **True** if hello value is empty; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-356">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-356">Examples</span></span>

<span data-ttu-id="abfee-357">Aşağıdaki örneğine hello bir dizi, nesne ve dize boş olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="abfee-357">hello following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="abfee-358">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-358">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-359">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-359">Name</span></span> | <span data-ttu-id="abfee-360">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-360">Type</span></span> | <span data-ttu-id="abfee-361">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-361">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-362">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="abfee-362">arrayEmpty</span></span> | <span data-ttu-id="abfee-363">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-363">Bool</span></span> | <span data-ttu-id="abfee-364">True</span><span class="sxs-lookup"><span data-stu-id="abfee-364">True</span></span> |
| <span data-ttu-id="abfee-365">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="abfee-365">objectEmpty</span></span> | <span data-ttu-id="abfee-366">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-366">Bool</span></span> | <span data-ttu-id="abfee-367">True</span><span class="sxs-lookup"><span data-stu-id="abfee-367">True</span></span> |
| <span data-ttu-id="abfee-368">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="abfee-368">stringEmpty</span></span> | <span data-ttu-id="abfee-369">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-369">Bool</span></span> | <span data-ttu-id="abfee-370">True</span><span class="sxs-lookup"><span data-stu-id="abfee-370">True</span></span> |

<a id="endswith" />

## <a name="endswith"></a><span data-ttu-id="abfee-371">endsWith</span><span class="sxs-lookup"><span data-stu-id="abfee-371">endsWith</span></span>
`endsWith(stringToSearch, stringToFind)`

<span data-ttu-id="abfee-372">Bir dize değeri ile bitip olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="abfee-372">Determines whether a string ends with a value.</span></span> <span data-ttu-id="abfee-373">Merhaba karşılaştırma büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="abfee-373">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-374">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-374">Parameters</span></span>

| <span data-ttu-id="abfee-375">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-375">Parameter</span></span> | <span data-ttu-id="abfee-376">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-376">Required</span></span> | <span data-ttu-id="abfee-377">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-377">Type</span></span> | <span data-ttu-id="abfee-378">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-378">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-379">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="abfee-379">stringToSearch</span></span> |<span data-ttu-id="abfee-380">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-380">Yes</span></span> |<span data-ttu-id="abfee-381">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-381">string</span></span> |<span data-ttu-id="abfee-382">Merhaba öğesi toofind içeren hello değeri.</span><span class="sxs-lookup"><span data-stu-id="abfee-382">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="abfee-383">stringToFind</span><span class="sxs-lookup"><span data-stu-id="abfee-383">stringToFind</span></span> |<span data-ttu-id="abfee-384">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-384">Yes</span></span> |<span data-ttu-id="abfee-385">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-385">string</span></span> |<span data-ttu-id="abfee-386">Merhaba değeri toofind.</span><span class="sxs-lookup"><span data-stu-id="abfee-386">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-387">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-387">Return value</span></span>

<span data-ttu-id="abfee-388">**Doğru** hello son karakter veya hello dizenin karakter hello değeri; eşleşiyorsa Aksi halde, **False**.</span><span class="sxs-lookup"><span data-stu-id="abfee-388">**True** if hello last character or characters of hello string match hello value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-389">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-389">Examples</span></span>

<span data-ttu-id="abfee-390">Aşağıdaki örnek hello nasıl toouse hello startsWith ve endsWith işlevleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="abfee-390">hello following example shows how toouse hello startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="abfee-391">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-391">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-392">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-392">Name</span></span> | <span data-ttu-id="abfee-393">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-393">Type</span></span> | <span data-ttu-id="abfee-394">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-394">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-395">startsTrue</span><span class="sxs-lookup"><span data-stu-id="abfee-395">startsTrue</span></span> | <span data-ttu-id="abfee-396">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-396">Bool</span></span> | <span data-ttu-id="abfee-397">True</span><span class="sxs-lookup"><span data-stu-id="abfee-397">True</span></span> |
| <span data-ttu-id="abfee-398">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="abfee-398">startsCapTrue</span></span> | <span data-ttu-id="abfee-399">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-399">Bool</span></span> | <span data-ttu-id="abfee-400">True</span><span class="sxs-lookup"><span data-stu-id="abfee-400">True</span></span> |
| <span data-ttu-id="abfee-401">startsFalse</span><span class="sxs-lookup"><span data-stu-id="abfee-401">startsFalse</span></span> | <span data-ttu-id="abfee-402">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-402">Bool</span></span> | <span data-ttu-id="abfee-403">False</span><span class="sxs-lookup"><span data-stu-id="abfee-403">False</span></span> |
| <span data-ttu-id="abfee-404">endsTrue</span><span class="sxs-lookup"><span data-stu-id="abfee-404">endsTrue</span></span> | <span data-ttu-id="abfee-405">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-405">Bool</span></span> | <span data-ttu-id="abfee-406">True</span><span class="sxs-lookup"><span data-stu-id="abfee-406">True</span></span> |
| <span data-ttu-id="abfee-407">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="abfee-407">endsCapTrue</span></span> | <span data-ttu-id="abfee-408">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-408">Bool</span></span> | <span data-ttu-id="abfee-409">True</span><span class="sxs-lookup"><span data-stu-id="abfee-409">True</span></span> |
| <span data-ttu-id="abfee-410">endsFalse</span><span class="sxs-lookup"><span data-stu-id="abfee-410">endsFalse</span></span> | <span data-ttu-id="abfee-411">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-411">Bool</span></span> | <span data-ttu-id="abfee-412">False</span><span class="sxs-lookup"><span data-stu-id="abfee-412">False</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="abfee-413">ilk</span><span class="sxs-lookup"><span data-stu-id="abfee-413">first</span></span>
`first(arg1)`

<span data-ttu-id="abfee-414">Merhaba dizenin ilk karakter ya da hello dizisinin ilk öğesi döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="abfee-414">Returns hello first character of hello string, or first element of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-415">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-415">Parameters</span></span>

| <span data-ttu-id="abfee-416">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-416">Parameter</span></span> | <span data-ttu-id="abfee-417">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-417">Required</span></span> | <span data-ttu-id="abfee-418">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-418">Type</span></span> | <span data-ttu-id="abfee-419">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-420">arg1</span><span class="sxs-lookup"><span data-stu-id="abfee-420">arg1</span></span> |<span data-ttu-id="abfee-421">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-421">Yes</span></span> |<span data-ttu-id="abfee-422">dizi veya dize</span><span class="sxs-lookup"><span data-stu-id="abfee-422">array or string</span></span> |<span data-ttu-id="abfee-423">Merhaba değeri tooretrieve hello ilk öğe veya karakter.</span><span class="sxs-lookup"><span data-stu-id="abfee-423">hello value tooretrieve hello first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-424">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-424">Return value</span></span>

<span data-ttu-id="abfee-425">Hello ilk karakter ya da dizi hello ilk öğesinin hello türü (dize, int, dizi veya nesne) dizesi.</span><span class="sxs-lookup"><span data-stu-id="abfee-425">A string of hello first character, or hello type (string, int, array, or object) of hello first element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-426">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-426">Examples</span></span>

<span data-ttu-id="abfee-427">Merhaba aşağıdaki örnekte nasıl toouse hello ilk işlevi bir dizi ve dize ile gösterilir.</span><span class="sxs-lookup"><span data-stu-id="abfee-427">hello following example shows how toouse hello first function with an array and string.</span></span>

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

<span data-ttu-id="abfee-428">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-428">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-429">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-429">Name</span></span> | <span data-ttu-id="abfee-430">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-430">Type</span></span> | <span data-ttu-id="abfee-431">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-432">arrayOutput</span></span> | <span data-ttu-id="abfee-433">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-433">String</span></span> | <span data-ttu-id="abfee-434">bir</span><span class="sxs-lookup"><span data-stu-id="abfee-434">one</span></span> |
| <span data-ttu-id="abfee-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-435">stringOutput</span></span> | <span data-ttu-id="abfee-436">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-436">String</span></span> | <span data-ttu-id="abfee-437">O</span><span class="sxs-lookup"><span data-stu-id="abfee-437">O</span></span> |

<a id="indexof" />

## <a name="indexof"></a><span data-ttu-id="abfee-438">IndexOf</span><span class="sxs-lookup"><span data-stu-id="abfee-438">indexOf</span></span>
`indexOf(stringToSearch, stringToFind)`

<span data-ttu-id="abfee-439">Dize içinde bir değerin ilk konumunu döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="abfee-439">Returns hello first position of a value within a string.</span></span> <span data-ttu-id="abfee-440">Merhaba karşılaştırma büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="abfee-440">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-441">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-441">Parameters</span></span>

| <span data-ttu-id="abfee-442">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-442">Parameter</span></span> | <span data-ttu-id="abfee-443">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-443">Required</span></span> | <span data-ttu-id="abfee-444">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-444">Type</span></span> | <span data-ttu-id="abfee-445">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-445">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-446">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="abfee-446">stringToSearch</span></span> |<span data-ttu-id="abfee-447">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-447">Yes</span></span> |<span data-ttu-id="abfee-448">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-448">string</span></span> |<span data-ttu-id="abfee-449">Merhaba öğesi toofind içeren hello değeri.</span><span class="sxs-lookup"><span data-stu-id="abfee-449">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="abfee-450">stringToFind</span><span class="sxs-lookup"><span data-stu-id="abfee-450">stringToFind</span></span> |<span data-ttu-id="abfee-451">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-451">Yes</span></span> |<span data-ttu-id="abfee-452">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-452">string</span></span> |<span data-ttu-id="abfee-453">Merhaba değeri toofind.</span><span class="sxs-lookup"><span data-stu-id="abfee-453">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-454">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-454">Return value</span></span>

<span data-ttu-id="abfee-455">Merhaba öğesi toofind hello konumunu temsil eden bir tamsayı.</span><span class="sxs-lookup"><span data-stu-id="abfee-455">An integer that represents hello position of hello item toofind.</span></span> <span data-ttu-id="abfee-456">Merhaba sıfır tabanlı bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="abfee-456">hello value is zero-based.</span></span> <span data-ttu-id="abfee-457">Merhaba öğesi bulunmazsa -1 döndürülür.</span><span class="sxs-lookup"><span data-stu-id="abfee-457">If hello item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-458">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-458">Examples</span></span>

<span data-ttu-id="abfee-459">Aşağıdaki örnek hello nasıl toouse hello IndexOf ve lastIndexOf işlevleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="abfee-459">hello following example shows how toouse hello indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="abfee-460">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-460">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-461">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-461">Name</span></span> | <span data-ttu-id="abfee-462">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-462">Type</span></span> | <span data-ttu-id="abfee-463">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-463">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-464">firstT</span><span class="sxs-lookup"><span data-stu-id="abfee-464">firstT</span></span> | <span data-ttu-id="abfee-465">Int</span><span class="sxs-lookup"><span data-stu-id="abfee-465">Int</span></span> | <span data-ttu-id="abfee-466">0</span><span class="sxs-lookup"><span data-stu-id="abfee-466">0</span></span> |
| <span data-ttu-id="abfee-467">lastT</span><span class="sxs-lookup"><span data-stu-id="abfee-467">lastT</span></span> | <span data-ttu-id="abfee-468">Int</span><span class="sxs-lookup"><span data-stu-id="abfee-468">Int</span></span> | <span data-ttu-id="abfee-469">3</span><span class="sxs-lookup"><span data-stu-id="abfee-469">3</span></span> |
| <span data-ttu-id="abfee-470">firstString</span><span class="sxs-lookup"><span data-stu-id="abfee-470">firstString</span></span> | <span data-ttu-id="abfee-471">Int</span><span class="sxs-lookup"><span data-stu-id="abfee-471">Int</span></span> | <span data-ttu-id="abfee-472">2</span><span class="sxs-lookup"><span data-stu-id="abfee-472">2</span></span> |
| <span data-ttu-id="abfee-473">lastString</span><span class="sxs-lookup"><span data-stu-id="abfee-473">lastString</span></span> | <span data-ttu-id="abfee-474">Int</span><span class="sxs-lookup"><span data-stu-id="abfee-474">Int</span></span> | <span data-ttu-id="abfee-475">0</span><span class="sxs-lookup"><span data-stu-id="abfee-475">0</span></span> |
| <span data-ttu-id="abfee-476">notFound</span><span class="sxs-lookup"><span data-stu-id="abfee-476">notFound</span></span> | <span data-ttu-id="abfee-477">Int</span><span class="sxs-lookup"><span data-stu-id="abfee-477">Int</span></span> | <span data-ttu-id="abfee-478">-1</span><span class="sxs-lookup"><span data-stu-id="abfee-478">-1</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="abfee-479">Son</span><span class="sxs-lookup"><span data-stu-id="abfee-479">last</span></span>
`last (arg1)`

<span data-ttu-id="abfee-480">Son hello dizenin karakter ya da hello dizisinin hello son öğesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="abfee-480">Returns last character of hello string, or hello last element of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-481">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-481">Parameters</span></span>

| <span data-ttu-id="abfee-482">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-482">Parameter</span></span> | <span data-ttu-id="abfee-483">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-483">Required</span></span> | <span data-ttu-id="abfee-484">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-484">Type</span></span> | <span data-ttu-id="abfee-485">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-485">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-486">arg1</span><span class="sxs-lookup"><span data-stu-id="abfee-486">arg1</span></span> |<span data-ttu-id="abfee-487">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-487">Yes</span></span> |<span data-ttu-id="abfee-488">dizi veya dize</span><span class="sxs-lookup"><span data-stu-id="abfee-488">array or string</span></span> |<span data-ttu-id="abfee-489">Merhaba değeri tooretrieve hello son öğesi veya karakter.</span><span class="sxs-lookup"><span data-stu-id="abfee-489">hello value tooretrieve hello last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-490">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-490">Return value</span></span>

<span data-ttu-id="abfee-491">Merhaba son karakter ya da dizi hello son öğesinin hello türü (dize, int, dizi veya nesne) dizesi.</span><span class="sxs-lookup"><span data-stu-id="abfee-491">A string of hello last character, or hello type (string, int, array, or object) of hello last element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-492">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-492">Examples</span></span>

<span data-ttu-id="abfee-493">Merhaba aşağıdaki örnekte nasıl toouse hello son işlevi bir dizi ve dize ile gösterilir.</span><span class="sxs-lookup"><span data-stu-id="abfee-493">hello following example shows how toouse hello last function with an array and string.</span></span>

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

<span data-ttu-id="abfee-494">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-494">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-495">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-495">Name</span></span> | <span data-ttu-id="abfee-496">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-496">Type</span></span> | <span data-ttu-id="abfee-497">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-497">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-498">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-498">arrayOutput</span></span> | <span data-ttu-id="abfee-499">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-499">String</span></span> | <span data-ttu-id="abfee-500">üç</span><span class="sxs-lookup"><span data-stu-id="abfee-500">three</span></span> |
| <span data-ttu-id="abfee-501">stringOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-501">stringOutput</span></span> | <span data-ttu-id="abfee-502">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-502">String</span></span> | <span data-ttu-id="abfee-503">E</span><span class="sxs-lookup"><span data-stu-id="abfee-503">e</span></span> |

<a id="lastindexof" />

## <a name="lastindexof"></a><span data-ttu-id="abfee-504">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="abfee-504">lastIndexOf</span></span>
`lastIndexOf(stringToSearch, stringToFind)`

<span data-ttu-id="abfee-505">Değer bir dize içinde son konumunu döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="abfee-505">Returns hello last position of a value within a string.</span></span> <span data-ttu-id="abfee-506">Merhaba karşılaştırma büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="abfee-506">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-507">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-507">Parameters</span></span>

| <span data-ttu-id="abfee-508">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-508">Parameter</span></span> | <span data-ttu-id="abfee-509">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-509">Required</span></span> | <span data-ttu-id="abfee-510">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-510">Type</span></span> | <span data-ttu-id="abfee-511">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-511">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-512">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="abfee-512">stringToSearch</span></span> |<span data-ttu-id="abfee-513">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-513">Yes</span></span> |<span data-ttu-id="abfee-514">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-514">string</span></span> |<span data-ttu-id="abfee-515">Merhaba öğesi toofind içeren hello değeri.</span><span class="sxs-lookup"><span data-stu-id="abfee-515">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="abfee-516">stringToFind</span><span class="sxs-lookup"><span data-stu-id="abfee-516">stringToFind</span></span> |<span data-ttu-id="abfee-517">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-517">Yes</span></span> |<span data-ttu-id="abfee-518">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-518">string</span></span> |<span data-ttu-id="abfee-519">Merhaba değeri toofind.</span><span class="sxs-lookup"><span data-stu-id="abfee-519">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-520">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-520">Return value</span></span>

<span data-ttu-id="abfee-521">Merhaba son hello öğesi toofind konumunu temsil eden bir tamsayı.</span><span class="sxs-lookup"><span data-stu-id="abfee-521">An integer that represents hello last position of hello item toofind.</span></span> <span data-ttu-id="abfee-522">Merhaba sıfır tabanlı bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="abfee-522">hello value is zero-based.</span></span> <span data-ttu-id="abfee-523">Merhaba öğesi bulunmazsa -1 döndürülür.</span><span class="sxs-lookup"><span data-stu-id="abfee-523">If hello item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-524">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-524">Examples</span></span>

<span data-ttu-id="abfee-525">Aşağıdaki örnek hello nasıl toouse hello IndexOf ve lastIndexOf işlevleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="abfee-525">hello following example shows how toouse hello indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="abfee-526">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-526">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-527">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-527">Name</span></span> | <span data-ttu-id="abfee-528">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-528">Type</span></span> | <span data-ttu-id="abfee-529">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-529">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-530">firstT</span><span class="sxs-lookup"><span data-stu-id="abfee-530">firstT</span></span> | <span data-ttu-id="abfee-531">Int</span><span class="sxs-lookup"><span data-stu-id="abfee-531">Int</span></span> | <span data-ttu-id="abfee-532">0</span><span class="sxs-lookup"><span data-stu-id="abfee-532">0</span></span> |
| <span data-ttu-id="abfee-533">lastT</span><span class="sxs-lookup"><span data-stu-id="abfee-533">lastT</span></span> | <span data-ttu-id="abfee-534">Int</span><span class="sxs-lookup"><span data-stu-id="abfee-534">Int</span></span> | <span data-ttu-id="abfee-535">3</span><span class="sxs-lookup"><span data-stu-id="abfee-535">3</span></span> |
| <span data-ttu-id="abfee-536">firstString</span><span class="sxs-lookup"><span data-stu-id="abfee-536">firstString</span></span> | <span data-ttu-id="abfee-537">Int</span><span class="sxs-lookup"><span data-stu-id="abfee-537">Int</span></span> | <span data-ttu-id="abfee-538">2</span><span class="sxs-lookup"><span data-stu-id="abfee-538">2</span></span> |
| <span data-ttu-id="abfee-539">lastString</span><span class="sxs-lookup"><span data-stu-id="abfee-539">lastString</span></span> | <span data-ttu-id="abfee-540">Int</span><span class="sxs-lookup"><span data-stu-id="abfee-540">Int</span></span> | <span data-ttu-id="abfee-541">0</span><span class="sxs-lookup"><span data-stu-id="abfee-541">0</span></span> |
| <span data-ttu-id="abfee-542">notFound</span><span class="sxs-lookup"><span data-stu-id="abfee-542">notFound</span></span> | <span data-ttu-id="abfee-543">Int</span><span class="sxs-lookup"><span data-stu-id="abfee-543">Int</span></span> | <span data-ttu-id="abfee-544">-1</span><span class="sxs-lookup"><span data-stu-id="abfee-544">-1</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="abfee-545">uzunluğu</span><span class="sxs-lookup"><span data-stu-id="abfee-545">length</span></span>
`length(string)`

<span data-ttu-id="abfee-546">Bir dize veya bir dizideki öğeler Hello karakterlerin sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="abfee-546">Returns hello number of characters in a string, or elements in an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-547">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-547">Parameters</span></span>

| <span data-ttu-id="abfee-548">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-548">Parameter</span></span> | <span data-ttu-id="abfee-549">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-549">Required</span></span> | <span data-ttu-id="abfee-550">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-550">Type</span></span> | <span data-ttu-id="abfee-551">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-551">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-552">arg1</span><span class="sxs-lookup"><span data-stu-id="abfee-552">arg1</span></span> |<span data-ttu-id="abfee-553">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-553">Yes</span></span> |<span data-ttu-id="abfee-554">dizi veya dize</span><span class="sxs-lookup"><span data-stu-id="abfee-554">array or string</span></span> |<span data-ttu-id="abfee-555">öğe sayısını hello alma dizi toouse hello veya karakter sayısını hello alma dizesi toouse hello.</span><span class="sxs-lookup"><span data-stu-id="abfee-555">hello array toouse for getting hello number of elements, or hello string toouse for getting hello number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-556">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-556">Return value</span></span>

<span data-ttu-id="abfee-557">İnt</span><span class="sxs-lookup"><span data-stu-id="abfee-557">An int.</span></span> 

### <a name="examples"></a><span data-ttu-id="abfee-558">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-558">Examples</span></span>

<span data-ttu-id="abfee-559">örnekte gösterildiği nasıl aşağıdaki hello toouse uzunluğunda bir dizi ve dizesi:</span><span class="sxs-lookup"><span data-stu-id="abfee-559">hello following example shows how toouse length with an array and string:</span></span>

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

<span data-ttu-id="abfee-560">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-560">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-561">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-561">Name</span></span> | <span data-ttu-id="abfee-562">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-562">Type</span></span> | <span data-ttu-id="abfee-563">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-563">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-564">arrayLength</span><span class="sxs-lookup"><span data-stu-id="abfee-564">arrayLength</span></span> | <span data-ttu-id="abfee-565">Int</span><span class="sxs-lookup"><span data-stu-id="abfee-565">Int</span></span> | <span data-ttu-id="abfee-566">3</span><span class="sxs-lookup"><span data-stu-id="abfee-566">3</span></span> |
| <span data-ttu-id="abfee-567">stringLength</span><span class="sxs-lookup"><span data-stu-id="abfee-567">stringLength</span></span> | <span data-ttu-id="abfee-568">Int</span><span class="sxs-lookup"><span data-stu-id="abfee-568">Int</span></span> | <span data-ttu-id="abfee-569">13</span><span class="sxs-lookup"><span data-stu-id="abfee-569">13</span></span> |

<a id="padleft" />

## <a name="padleft"></a><span data-ttu-id="abfee-570">PadLeft</span><span class="sxs-lookup"><span data-stu-id="abfee-570">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="abfee-571">Merhaba toplam belirtilen uzunluk ulaşmasını kadar karakterleri toohello sol ekleyerek sağa hizalı dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="abfee-571">Returns a right-aligned string by adding characters toohello left until reaching hello total specified length.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-572">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-572">Parameters</span></span>

| <span data-ttu-id="abfee-573">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-573">Parameter</span></span> | <span data-ttu-id="abfee-574">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-574">Required</span></span> | <span data-ttu-id="abfee-575">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-575">Type</span></span> | <span data-ttu-id="abfee-576">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-576">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-577">valueToPad</span><span class="sxs-lookup"><span data-stu-id="abfee-577">valueToPad</span></span> |<span data-ttu-id="abfee-578">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-578">Yes</span></span> |<span data-ttu-id="abfee-579">dize veya int</span><span class="sxs-lookup"><span data-stu-id="abfee-579">string or int</span></span> |<span data-ttu-id="abfee-580">değer tooright hello-hizalayın.</span><span class="sxs-lookup"><span data-stu-id="abfee-580">hello value tooright-align.</span></span> |
| <span data-ttu-id="abfee-581">totalLength</span><span class="sxs-lookup"><span data-stu-id="abfee-581">totalLength</span></span> |<span data-ttu-id="abfee-582">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-582">Yes</span></span> |<span data-ttu-id="abfee-583">Int</span><span class="sxs-lookup"><span data-stu-id="abfee-583">int</span></span> |<span data-ttu-id="abfee-584">Merhaba toplam hello karakter sayısını dizesi döndürdü.</span><span class="sxs-lookup"><span data-stu-id="abfee-584">hello total number of characters in hello returned string.</span></span> |
| <span data-ttu-id="abfee-585">paddingCharacter</span><span class="sxs-lookup"><span data-stu-id="abfee-585">paddingCharacter</span></span> |<span data-ttu-id="abfee-586">Hayır</span><span class="sxs-lookup"><span data-stu-id="abfee-586">No</span></span> |<span data-ttu-id="abfee-587">tek bir karakter</span><span class="sxs-lookup"><span data-stu-id="abfee-587">single character</span></span> |<span data-ttu-id="abfee-588">Sol-Doldurma hello toplam uzunluğu ulaşılana kadar için karakter toouse hello.</span><span class="sxs-lookup"><span data-stu-id="abfee-588">hello character toouse for left-padding until hello total length is reached.</span></span> <span data-ttu-id="abfee-589">bir alanı Hello varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="abfee-589">hello default value is a space.</span></span> |

<span data-ttu-id="abfee-590">Hello özgün dizeye hello karakter toopad sayısından daha uzun olması durumunda hiçbir karakter eklenir.</span><span class="sxs-lookup"><span data-stu-id="abfee-590">If hello original string is longer than hello number of characters toopad, no characters are added.</span></span>

### <a name="return-value"></a><span data-ttu-id="abfee-591">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-591">Return value</span></span>

<span data-ttu-id="abfee-592">Belirtilen karakter sayısı en az hello bir dize.</span><span class="sxs-lookup"><span data-stu-id="abfee-592">A string with at least hello number of specified characters.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-593">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-593">Examples</span></span>

<span data-ttu-id="abfee-594">Aşağıdaki örnek hello nasıl toopad hello kullanıcı tarafından sağlanan parametre değeri hello ekleyerek sıfır karakter hello toplam karakter sayısı ulaşana kadar gösterir.</span><span class="sxs-lookup"><span data-stu-id="abfee-594">hello following example shows how toopad hello user-provided parameter value by adding hello zero character until it reaches hello total number of characters.</span></span> 

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

<span data-ttu-id="abfee-595">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-595">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-596">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-596">Name</span></span> | <span data-ttu-id="abfee-597">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-597">Type</span></span> | <span data-ttu-id="abfee-598">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-598">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-599">stringOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-599">stringOutput</span></span> | <span data-ttu-id="abfee-600">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-600">String</span></span> | <span data-ttu-id="abfee-601">0000000123</span><span class="sxs-lookup"><span data-stu-id="abfee-601">0000000123</span></span> |

<a id="replace" />

## <a name="replace"></a><span data-ttu-id="abfee-602">Değiştir</span><span class="sxs-lookup"><span data-stu-id="abfee-602">replace</span></span>
`replace(originalString, oldString, newString)`

<span data-ttu-id="abfee-603">Başka bir dizeyle yerine tek bir dize tüm örneklerini içeren yeni bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="abfee-603">Returns a new string with all instances of one string replaced by another string.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-604">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-604">Parameters</span></span>

| <span data-ttu-id="abfee-605">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-605">Parameter</span></span> | <span data-ttu-id="abfee-606">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-606">Required</span></span> | <span data-ttu-id="abfee-607">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-607">Type</span></span> | <span data-ttu-id="abfee-608">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-608">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-609">originalString</span><span class="sxs-lookup"><span data-stu-id="abfee-609">originalString</span></span> |<span data-ttu-id="abfee-610">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-610">Yes</span></span> |<span data-ttu-id="abfee-611">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-611">string</span></span> |<span data-ttu-id="abfee-612">başka bir dizeyle yerine bir dizesinin tüm örnekleri olan hello değeri.</span><span class="sxs-lookup"><span data-stu-id="abfee-612">hello value that has all instances of one string replaced by another string.</span></span> |
| <span data-ttu-id="abfee-613">oldString</span><span class="sxs-lookup"><span data-stu-id="abfee-613">oldString</span></span> |<span data-ttu-id="abfee-614">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-614">Yes</span></span> |<span data-ttu-id="abfee-615">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-615">string</span></span> |<span data-ttu-id="abfee-616">Merhaba dize toobe hello özgün dizeden kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="abfee-616">hello string toobe removed from hello original string.</span></span> |
| <span data-ttu-id="abfee-617">newString</span><span class="sxs-lookup"><span data-stu-id="abfee-617">newString</span></span> |<span data-ttu-id="abfee-618">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-618">Yes</span></span> |<span data-ttu-id="abfee-619">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-619">string</span></span> |<span data-ttu-id="abfee-620">Merhaba dize tooadd hello yerine dize kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="abfee-620">hello string tooadd in place of hello removed string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-621">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-621">Return value</span></span>

<span data-ttu-id="abfee-622">Bir dizeyle hello karakterleri değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="abfee-622">A string with hello replaced characters.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-623">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-623">Examples</span></span>

<span data-ttu-id="abfee-624">Aşağıdaki örneğine hello nasıl tooremove tüm hello kullanıcı tarafından sağlanan dizeden tireler ve nasıl hello tooreplace parçası dize başka bir dizeyle gösterir.</span><span class="sxs-lookup"><span data-stu-id="abfee-624">hello following example shows how tooremove all dashes from hello user-provided string, and how tooreplace part of hello string with another string.</span></span>

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

<span data-ttu-id="abfee-625">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-625">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-626">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-626">Name</span></span> | <span data-ttu-id="abfee-627">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-627">Type</span></span> | <span data-ttu-id="abfee-628">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-628">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-629">firstOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-629">firstOutput</span></span> | <span data-ttu-id="abfee-630">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-630">String</span></span> | <span data-ttu-id="abfee-631">1231231234</span><span class="sxs-lookup"><span data-stu-id="abfee-631">1231231234</span></span> |
| <span data-ttu-id="abfee-632">secodeOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-632">secodeOutput</span></span> | <span data-ttu-id="abfee-633">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-633">String</span></span> | <span data-ttu-id="abfee-634">123-123-xxxx</span><span class="sxs-lookup"><span data-stu-id="abfee-634">123-123-xxxx</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="abfee-635">Atla</span><span class="sxs-lookup"><span data-stu-id="abfee-635">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="abfee-636">Merhaba öğe sayısını belirtilen sonra hello sayıda karakter veya bir dizi tüm hello ile belirtilen öğelerin sonra tüm hello karakterler içeren bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="abfee-636">Returns a string with all hello characters after hello specified number of characters, or an array with all hello elements after hello specified number of elements.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-637">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-637">Parameters</span></span>

| <span data-ttu-id="abfee-638">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-638">Parameter</span></span> | <span data-ttu-id="abfee-639">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-639">Required</span></span> | <span data-ttu-id="abfee-640">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-640">Type</span></span> | <span data-ttu-id="abfee-641">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-641">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-642">originalValue</span><span class="sxs-lookup"><span data-stu-id="abfee-642">originalValue</span></span> |<span data-ttu-id="abfee-643">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-643">Yes</span></span> |<span data-ttu-id="abfee-644">dizi veya dize</span><span class="sxs-lookup"><span data-stu-id="abfee-644">array or string</span></span> |<span data-ttu-id="abfee-645">atlanıyor hello dizisi veya dize toouse.</span><span class="sxs-lookup"><span data-stu-id="abfee-645">hello array or string toouse for skipping.</span></span> |
| <span data-ttu-id="abfee-646">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="abfee-646">numberToSkip</span></span> |<span data-ttu-id="abfee-647">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-647">Yes</span></span> |<span data-ttu-id="abfee-648">Int</span><span class="sxs-lookup"><span data-stu-id="abfee-648">int</span></span> |<span data-ttu-id="abfee-649">öğeleri veya karakter tooskip Hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="abfee-649">hello number of elements or characters tooskip.</span></span> <span data-ttu-id="abfee-650">Bu değer 0 veya daha az ise, tüm öğeleri hello veya karakter hello değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="abfee-650">If this value is 0 or less, all hello elements or characters in hello value are returned.</span></span> <span data-ttu-id="abfee-651">Merhaba dizisi veya dize hello uzunluğundan büyük olursa, boş dize veya dize döndürülür.</span><span class="sxs-lookup"><span data-stu-id="abfee-651">If it is larger than hello length of hello array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-652">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-652">Return value</span></span>

<span data-ttu-id="abfee-653">Bir dizi veya dize.</span><span class="sxs-lookup"><span data-stu-id="abfee-653">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-654">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-654">Examples</span></span>

<span data-ttu-id="abfee-655">Örnek atlar hello aşağıdaki hello hello dizide öğe sayısını belirtilen ve hello bir dizedeki karakter sayısını belirtilen.</span><span class="sxs-lookup"><span data-stu-id="abfee-655">hello following example skips hello specified number of elements in hello array, and hello specified number of characters in a string.</span></span>

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

<span data-ttu-id="abfee-656">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-656">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-657">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-657">Name</span></span> | <span data-ttu-id="abfee-658">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-658">Type</span></span> | <span data-ttu-id="abfee-659">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-659">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-660">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-660">arrayOutput</span></span> | <span data-ttu-id="abfee-661">Dizi</span><span class="sxs-lookup"><span data-stu-id="abfee-661">Array</span></span> | <span data-ttu-id="abfee-662">["üç"]</span><span class="sxs-lookup"><span data-stu-id="abfee-662">["three"]</span></span> |
| <span data-ttu-id="abfee-663">stringOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-663">stringOutput</span></span> | <span data-ttu-id="abfee-664">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-664">String</span></span> | <span data-ttu-id="abfee-665">iki üç</span><span class="sxs-lookup"><span data-stu-id="abfee-665">two three</span></span> |

<a id="split" />

## <a name="split"></a><span data-ttu-id="abfee-666">split</span><span class="sxs-lookup"><span data-stu-id="abfee-666">split</span></span>
`split(inputString, delimiter)`

<span data-ttu-id="abfee-667">Sınırlayıcılar belirtilen hello tarafından ayrılmış dize hello alt dizeler hello birini içeren bir dizeler dizisi giriş döndürür.</span><span class="sxs-lookup"><span data-stu-id="abfee-667">Returns an array of strings that contains hello substrings of hello input string that are delimited by hello specified delimiters.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-668">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-668">Parameters</span></span>

| <span data-ttu-id="abfee-669">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-669">Parameter</span></span> | <span data-ttu-id="abfee-670">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-670">Required</span></span> | <span data-ttu-id="abfee-671">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-671">Type</span></span> | <span data-ttu-id="abfee-672">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-672">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-673">inputString</span><span class="sxs-lookup"><span data-stu-id="abfee-673">inputString</span></span> |<span data-ttu-id="abfee-674">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-674">Yes</span></span> |<span data-ttu-id="abfee-675">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-675">string</span></span> |<span data-ttu-id="abfee-676">Merhaba dize toosplit.</span><span class="sxs-lookup"><span data-stu-id="abfee-676">hello string toosplit.</span></span> |
| <span data-ttu-id="abfee-677">sınırlayıcı</span><span class="sxs-lookup"><span data-stu-id="abfee-677">delimiter</span></span> |<span data-ttu-id="abfee-678">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-678">Yes</span></span> |<span data-ttu-id="abfee-679">dize veya dize dizisi</span><span class="sxs-lookup"><span data-stu-id="abfee-679">string or array of strings</span></span> |<span data-ttu-id="abfee-680">Merhaba dize bölmek için sınırlayıcı toouse hello.</span><span class="sxs-lookup"><span data-stu-id="abfee-680">hello delimiter toouse for splitting hello string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-681">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-681">Return value</span></span>

<span data-ttu-id="abfee-682">Bir dizeler dizisi.</span><span class="sxs-lookup"><span data-stu-id="abfee-682">An array of strings.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-683">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-683">Examples</span></span>

<span data-ttu-id="abfee-684">Merhaba aşağıdaki örnek hello giriş dizesi virgül ile virgül veya noktalı virgül ile böler.</span><span class="sxs-lookup"><span data-stu-id="abfee-684">hello following example splits hello input string with a comma, and with either a comma or a semi-colon.</span></span>

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

<span data-ttu-id="abfee-685">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-685">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-686">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-686">Name</span></span> | <span data-ttu-id="abfee-687">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-687">Type</span></span> | <span data-ttu-id="abfee-688">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-688">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-689">firstOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-689">firstOutput</span></span> | <span data-ttu-id="abfee-690">Dizi</span><span class="sxs-lookup"><span data-stu-id="abfee-690">Array</span></span> | <span data-ttu-id="abfee-691">["bir", "iki", "üç"]</span><span class="sxs-lookup"><span data-stu-id="abfee-691">["one", "two", "three"]</span></span> |
| <span data-ttu-id="abfee-692">secondOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-692">secondOutput</span></span> | <span data-ttu-id="abfee-693">Dizi</span><span class="sxs-lookup"><span data-stu-id="abfee-693">Array</span></span> | <span data-ttu-id="abfee-694">["bir", "iki", "üç"]</span><span class="sxs-lookup"><span data-stu-id="abfee-694">["one", "two", "three"]</span></span> |

<a id="startswith" />

## <a name="startswith"></a><span data-ttu-id="abfee-695">startsWith</span><span class="sxs-lookup"><span data-stu-id="abfee-695">startsWith</span></span>
`startsWith(stringToSearch, stringToFind)`

<span data-ttu-id="abfee-696">Bir dize değeri ile başlayıp başlamadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="abfee-696">Determines whether a string starts with a value.</span></span> <span data-ttu-id="abfee-697">Merhaba karşılaştırma büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="abfee-697">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-698">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-698">Parameters</span></span>

| <span data-ttu-id="abfee-699">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-699">Parameter</span></span> | <span data-ttu-id="abfee-700">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-700">Required</span></span> | <span data-ttu-id="abfee-701">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-701">Type</span></span> | <span data-ttu-id="abfee-702">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-702">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-703">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="abfee-703">stringToSearch</span></span> |<span data-ttu-id="abfee-704">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-704">Yes</span></span> |<span data-ttu-id="abfee-705">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-705">string</span></span> |<span data-ttu-id="abfee-706">Merhaba öğesi toofind içeren hello değeri.</span><span class="sxs-lookup"><span data-stu-id="abfee-706">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="abfee-707">stringToFind</span><span class="sxs-lookup"><span data-stu-id="abfee-707">stringToFind</span></span> |<span data-ttu-id="abfee-708">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-708">Yes</span></span> |<span data-ttu-id="abfee-709">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-709">string</span></span> |<span data-ttu-id="abfee-710">Merhaba değeri toofind.</span><span class="sxs-lookup"><span data-stu-id="abfee-710">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-711">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-711">Return value</span></span>

<span data-ttu-id="abfee-712">**Doğru** hello ilk karakterin veya karakter hello dizesinin hello değeri; eşleşiyorsa Aksi halde, **False**.</span><span class="sxs-lookup"><span data-stu-id="abfee-712">**True** if hello first character or characters of hello string match hello value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-713">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-713">Examples</span></span>

<span data-ttu-id="abfee-714">Aşağıdaki örnek hello nasıl toouse hello startsWith ve endsWith işlevleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="abfee-714">hello following example shows how toouse hello startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="abfee-715">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-715">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-716">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-716">Name</span></span> | <span data-ttu-id="abfee-717">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-717">Type</span></span> | <span data-ttu-id="abfee-718">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-718">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-719">startsTrue</span><span class="sxs-lookup"><span data-stu-id="abfee-719">startsTrue</span></span> | <span data-ttu-id="abfee-720">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-720">Bool</span></span> | <span data-ttu-id="abfee-721">True</span><span class="sxs-lookup"><span data-stu-id="abfee-721">True</span></span> |
| <span data-ttu-id="abfee-722">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="abfee-722">startsCapTrue</span></span> | <span data-ttu-id="abfee-723">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-723">Bool</span></span> | <span data-ttu-id="abfee-724">True</span><span class="sxs-lookup"><span data-stu-id="abfee-724">True</span></span> |
| <span data-ttu-id="abfee-725">startsFalse</span><span class="sxs-lookup"><span data-stu-id="abfee-725">startsFalse</span></span> | <span data-ttu-id="abfee-726">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-726">Bool</span></span> | <span data-ttu-id="abfee-727">False</span><span class="sxs-lookup"><span data-stu-id="abfee-727">False</span></span> |
| <span data-ttu-id="abfee-728">endsTrue</span><span class="sxs-lookup"><span data-stu-id="abfee-728">endsTrue</span></span> | <span data-ttu-id="abfee-729">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-729">Bool</span></span> | <span data-ttu-id="abfee-730">True</span><span class="sxs-lookup"><span data-stu-id="abfee-730">True</span></span> |
| <span data-ttu-id="abfee-731">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="abfee-731">endsCapTrue</span></span> | <span data-ttu-id="abfee-732">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-732">Bool</span></span> | <span data-ttu-id="abfee-733">True</span><span class="sxs-lookup"><span data-stu-id="abfee-733">True</span></span> |
| <span data-ttu-id="abfee-734">endsFalse</span><span class="sxs-lookup"><span data-stu-id="abfee-734">endsFalse</span></span> | <span data-ttu-id="abfee-735">bool</span><span class="sxs-lookup"><span data-stu-id="abfee-735">Bool</span></span> | <span data-ttu-id="abfee-736">False</span><span class="sxs-lookup"><span data-stu-id="abfee-736">False</span></span> |

<a id="string" />

## <a name="string"></a><span data-ttu-id="abfee-737">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-737">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="abfee-738">Belirtilen değer tooa dize dönüştürür hello.</span><span class="sxs-lookup"><span data-stu-id="abfee-738">Converts hello specified value tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-739">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-739">Parameters</span></span>

| <span data-ttu-id="abfee-740">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-740">Parameter</span></span> | <span data-ttu-id="abfee-741">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-741">Required</span></span> | <span data-ttu-id="abfee-742">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-742">Type</span></span> | <span data-ttu-id="abfee-743">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-743">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-744">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="abfee-744">valueToConvert</span></span> |<span data-ttu-id="abfee-745">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-745">Yes</span></span> | <span data-ttu-id="abfee-746">Herhangi biri</span><span class="sxs-lookup"><span data-stu-id="abfee-746">Any</span></span> |<span data-ttu-id="abfee-747">Merhaba değeri tooconvert toostring.</span><span class="sxs-lookup"><span data-stu-id="abfee-747">hello value tooconvert toostring.</span></span> <span data-ttu-id="abfee-748">Nesneler ve diziler dahil olmak üzere herhangi türde bir değer dönüştürülebilir.</span><span class="sxs-lookup"><span data-stu-id="abfee-748">Any type of value can be converted, including objects and arrays.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-749">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-749">Return value</span></span>

<span data-ttu-id="abfee-750">Dönüştürülen değer hello dizesi.</span><span class="sxs-lookup"><span data-stu-id="abfee-750">A string of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-751">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-751">Examples</span></span>

<span data-ttu-id="abfee-752">Aşağıdaki örnek hello nasıl tooconvert farklı türlerde değerler toostrings gösterir:</span><span class="sxs-lookup"><span data-stu-id="abfee-752">hello following example shows how tooconvert different types of values toostrings:</span></span>

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

<span data-ttu-id="abfee-753">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-753">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-754">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-754">Name</span></span> | <span data-ttu-id="abfee-755">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-755">Type</span></span> | <span data-ttu-id="abfee-756">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-756">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-757">objectOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-757">objectOutput</span></span> | <span data-ttu-id="abfee-758">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-758">String</span></span> | <span data-ttu-id="abfee-759">{"valueA": 10, "valueB": "Örnek metin"}</span><span class="sxs-lookup"><span data-stu-id="abfee-759">{"valueA":10,"valueB":"Example Text"}</span></span> |
| <span data-ttu-id="abfee-760">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-760">arrayOutput</span></span> | <span data-ttu-id="abfee-761">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-761">String</span></span> | <span data-ttu-id="abfee-762">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="abfee-762">["a","b","c"]</span></span> |
| <span data-ttu-id="abfee-763">intOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-763">intOutput</span></span> | <span data-ttu-id="abfee-764">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-764">String</span></span> | <span data-ttu-id="abfee-765">5</span><span class="sxs-lookup"><span data-stu-id="abfee-765">5</span></span> |

<a id="substring" />

## <a name="substring"></a><span data-ttu-id="abfee-766">substring</span><span class="sxs-lookup"><span data-stu-id="abfee-766">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="abfee-767">Belirtilen hello başlar konumu karakter ve hello içeren bir alt dizenin belirtilen karakter sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="abfee-767">Returns a substring that starts at hello specified character position and contains hello specified number of characters.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-768">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-768">Parameters</span></span>

| <span data-ttu-id="abfee-769">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-769">Parameter</span></span> | <span data-ttu-id="abfee-770">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-770">Required</span></span> | <span data-ttu-id="abfee-771">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-771">Type</span></span> | <span data-ttu-id="abfee-772">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-772">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-773">stringToParse</span><span class="sxs-lookup"><span data-stu-id="abfee-773">stringToParse</span></span> |<span data-ttu-id="abfee-774">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-774">Yes</span></span> |<span data-ttu-id="abfee-775">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-775">string</span></span> |<span data-ttu-id="abfee-776">hangi hello alt dizenin ayıklanacağı hello özgün dizesi.</span><span class="sxs-lookup"><span data-stu-id="abfee-776">hello original string from which hello substring is extracted.</span></span> |
| <span data-ttu-id="abfee-777">startIndex</span><span class="sxs-lookup"><span data-stu-id="abfee-777">startIndex</span></span> |<span data-ttu-id="abfee-778">Hayır</span><span class="sxs-lookup"><span data-stu-id="abfee-778">No</span></span> |<span data-ttu-id="abfee-779">Int</span><span class="sxs-lookup"><span data-stu-id="abfee-779">int</span></span> |<span data-ttu-id="abfee-780">Merhaba sıfır tabanlı başlangıç karakteri konumu hello substring.</span><span class="sxs-lookup"><span data-stu-id="abfee-780">hello zero-based starting character position for hello substring.</span></span> |
| <span data-ttu-id="abfee-781">uzunluğu</span><span class="sxs-lookup"><span data-stu-id="abfee-781">length</span></span> |<span data-ttu-id="abfee-782">Hayır</span><span class="sxs-lookup"><span data-stu-id="abfee-782">No</span></span> |<span data-ttu-id="abfee-783">Int</span><span class="sxs-lookup"><span data-stu-id="abfee-783">int</span></span> |<span data-ttu-id="abfee-784">Merhaba hello substring karakter sayısı.</span><span class="sxs-lookup"><span data-stu-id="abfee-784">hello number of characters for hello substring.</span></span> <span data-ttu-id="abfee-785">Merhaba dize içinde tooa konuma başvurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="abfee-785">Must refer tooa location within hello string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-786">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-786">Return value</span></span>

<span data-ttu-id="abfee-787">Merhaba substring.</span><span class="sxs-lookup"><span data-stu-id="abfee-787">hello substring.</span></span>

### <a name="remarks"></a><span data-ttu-id="abfee-788">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="abfee-788">Remarks</span></span>

<span data-ttu-id="abfee-789">Merhaba substring hello dize hello sonunu aşan genişletir hello işlevi başarısız oluyor.</span><span class="sxs-lookup"><span data-stu-id="abfee-789">hello function fails when hello substring extends beyond hello end of hello string.</span></span> <span data-ttu-id="abfee-790">Merhaba hata "Merhaba dizin ve uzunluk parametreleri hello dize içinde tooa konuma başvurmalıdır ile. aşağıdaki örneğine hello başarısız</span><span class="sxs-lookup"><span data-stu-id="abfee-790">hello following example fails with hello error "hello index and length parameters must refer tooa location within hello string.</span></span> <span data-ttu-id="abfee-791">Merhaba dizin parametresi: '0' hello uzunluk parametresi: '11' hello hello dize parametresinin uzunluğu: '10'. ".</span><span class="sxs-lookup"><span data-stu-id="abfee-791">hello index parameter: '0', hello length parameter: '11', hello length of hello string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a><span data-ttu-id="abfee-792">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-792">Examples</span></span>

<span data-ttu-id="abfee-793">Aşağıdaki örneğine hello bir alt dizesi bir parametresinden ayıklar.</span><span class="sxs-lookup"><span data-stu-id="abfee-793">hello following example extracts a substring from a parameter.</span></span>

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

<span data-ttu-id="abfee-794">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-794">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-795">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-795">Name</span></span> | <span data-ttu-id="abfee-796">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-796">Type</span></span> | <span data-ttu-id="abfee-797">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-797">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-798">substringOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-798">substringOutput</span></span> | <span data-ttu-id="abfee-799">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-799">String</span></span> | <span data-ttu-id="abfee-800">iki</span><span class="sxs-lookup"><span data-stu-id="abfee-800">two</span></span> |


<a id="take" />

## <a name="take"></a><span data-ttu-id="abfee-801">Al</span><span class="sxs-lookup"><span data-stu-id="abfee-801">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="abfee-802">Dize başından hello karakter sayısını hello bir dizeyle belirtilen döndürür hello veya hello sahip bir dizi hello dizi hello başından öğelerin sayısı belirtildi.</span><span class="sxs-lookup"><span data-stu-id="abfee-802">Returns a string with hello specified number of characters from hello start of hello string, or an array with hello specified number of elements from hello start of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-803">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-803">Parameters</span></span>

| <span data-ttu-id="abfee-804">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-804">Parameter</span></span> | <span data-ttu-id="abfee-805">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-805">Required</span></span> | <span data-ttu-id="abfee-806">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-806">Type</span></span> | <span data-ttu-id="abfee-807">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-807">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-808">originalValue</span><span class="sxs-lookup"><span data-stu-id="abfee-808">originalValue</span></span> |<span data-ttu-id="abfee-809">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-809">Yes</span></span> |<span data-ttu-id="abfee-810">dizi veya dize</span><span class="sxs-lookup"><span data-stu-id="abfee-810">array or string</span></span> |<span data-ttu-id="abfee-811">dizi veya dize tootake hello öğelerinden hello.</span><span class="sxs-lookup"><span data-stu-id="abfee-811">hello array or string tootake hello elements from.</span></span> |
| <span data-ttu-id="abfee-812">numberToTake</span><span class="sxs-lookup"><span data-stu-id="abfee-812">numberToTake</span></span> |<span data-ttu-id="abfee-813">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-813">Yes</span></span> |<span data-ttu-id="abfee-814">Int</span><span class="sxs-lookup"><span data-stu-id="abfee-814">int</span></span> |<span data-ttu-id="abfee-815">öğeleri veya karakter tootake Hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="abfee-815">hello number of elements or characters tootake.</span></span> <span data-ttu-id="abfee-816">Bu değer 0 veya daha az ise, boş dize veya dize döndürülür.</span><span class="sxs-lookup"><span data-stu-id="abfee-816">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="abfee-817">Merhaba hello verilen dizi veya dize uzunluğundan büyük olursa, hello dizisi veya dize tüm hello öğeler döndürülür.</span><span class="sxs-lookup"><span data-stu-id="abfee-817">If it is larger than hello length of hello given array or string, all hello elements in hello array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-818">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-818">Return value</span></span>

<span data-ttu-id="abfee-819">Bir dizi veya dize.</span><span class="sxs-lookup"><span data-stu-id="abfee-819">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-820">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-820">Examples</span></span>

<span data-ttu-id="abfee-821">Örnek alır hello aşağıdaki hello hello dizisinden öğeleri ve bir dizeden karakterleri sayısı belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="abfee-821">hello following example takes hello specified number of elements from hello array, and characters from a string.</span></span>

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

<span data-ttu-id="abfee-822">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-822">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-823">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-823">Name</span></span> | <span data-ttu-id="abfee-824">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-824">Type</span></span> | <span data-ttu-id="abfee-825">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-825">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-826">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-826">arrayOutput</span></span> | <span data-ttu-id="abfee-827">Dizi</span><span class="sxs-lookup"><span data-stu-id="abfee-827">Array</span></span> | <span data-ttu-id="abfee-828">["", "iki"]</span><span class="sxs-lookup"><span data-stu-id="abfee-828">["one", "two"]</span></span> |
| <span data-ttu-id="abfee-829">stringOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-829">stringOutput</span></span> | <span data-ttu-id="abfee-830">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-830">String</span></span> | <span data-ttu-id="abfee-831">üzerinde</span><span class="sxs-lookup"><span data-stu-id="abfee-831">on</span></span> |

<a id="tolower" />

## <a name="tolower"></a><span data-ttu-id="abfee-832">toLower</span><span class="sxs-lookup"><span data-stu-id="abfee-832">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="abfee-833">Dönüştürür hello dize toolower durumu belirtildi.</span><span class="sxs-lookup"><span data-stu-id="abfee-833">Converts hello specified string toolower case.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-834">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-834">Parameters</span></span>

| <span data-ttu-id="abfee-835">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-835">Parameter</span></span> | <span data-ttu-id="abfee-836">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-836">Required</span></span> | <span data-ttu-id="abfee-837">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-837">Type</span></span> | <span data-ttu-id="abfee-838">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-838">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-839">stringToChange</span><span class="sxs-lookup"><span data-stu-id="abfee-839">stringToChange</span></span> |<span data-ttu-id="abfee-840">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-840">Yes</span></span> |<span data-ttu-id="abfee-841">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-841">string</span></span> |<span data-ttu-id="abfee-842">Merhaba değeri tooconvert toolower durumda.</span><span class="sxs-lookup"><span data-stu-id="abfee-842">hello value tooconvert toolower case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-843">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-843">Return value</span></span>

<span data-ttu-id="abfee-844">Merhaba dize toolower durumda dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="abfee-844">hello string converted toolower case.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-845">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-845">Examples</span></span>

<span data-ttu-id="abfee-846">Aşağıdaki örneğine hello bir parametre değeri toolower çalışması ve tooupper harfe dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="abfee-846">hello following example converts a parameter value toolower case and tooupper case.</span></span>

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

<span data-ttu-id="abfee-847">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-847">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-848">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-848">Name</span></span> | <span data-ttu-id="abfee-849">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-849">Type</span></span> | <span data-ttu-id="abfee-850">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-850">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-851">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-851">toLowerOutput</span></span> | <span data-ttu-id="abfee-852">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-852">String</span></span> | <span data-ttu-id="abfee-853">Bir iki üç</span><span class="sxs-lookup"><span data-stu-id="abfee-853">one two three</span></span> |
| <span data-ttu-id="abfee-854">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-854">toUpperOutput</span></span> | <span data-ttu-id="abfee-855">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-855">String</span></span> | <span data-ttu-id="abfee-856">BİR İKİ ÜÇ</span><span class="sxs-lookup"><span data-stu-id="abfee-856">ONE TWO THREE</span></span> |

<a id="toupper" />

## <a name="toupper"></a><span data-ttu-id="abfee-857">toUpper</span><span class="sxs-lookup"><span data-stu-id="abfee-857">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="abfee-858">Dönüştürür hello dize tooupper durumu belirtildi.</span><span class="sxs-lookup"><span data-stu-id="abfee-858">Converts hello specified string tooupper case.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-859">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-859">Parameters</span></span>

| <span data-ttu-id="abfee-860">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-860">Parameter</span></span> | <span data-ttu-id="abfee-861">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-861">Required</span></span> | <span data-ttu-id="abfee-862">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-862">Type</span></span> | <span data-ttu-id="abfee-863">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-863">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-864">stringToChange</span><span class="sxs-lookup"><span data-stu-id="abfee-864">stringToChange</span></span> |<span data-ttu-id="abfee-865">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-865">Yes</span></span> |<span data-ttu-id="abfee-866">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-866">string</span></span> |<span data-ttu-id="abfee-867">Merhaba değeri tooconvert tooupper durumda.</span><span class="sxs-lookup"><span data-stu-id="abfee-867">hello value tooconvert tooupper case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-868">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-868">Return value</span></span>

<span data-ttu-id="abfee-869">Merhaba dize tooupper durumda dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="abfee-869">hello string converted tooupper case.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-870">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-870">Examples</span></span>

<span data-ttu-id="abfee-871">Aşağıdaki örneğine hello bir parametre değeri toolower çalışması ve tooupper harfe dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="abfee-871">hello following example converts a parameter value toolower case and tooupper case.</span></span>

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

<span data-ttu-id="abfee-872">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-872">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-873">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-873">Name</span></span> | <span data-ttu-id="abfee-874">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-874">Type</span></span> | <span data-ttu-id="abfee-875">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-875">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-876">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-876">toLowerOutput</span></span> | <span data-ttu-id="abfee-877">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-877">String</span></span> | <span data-ttu-id="abfee-878">Bir iki üç</span><span class="sxs-lookup"><span data-stu-id="abfee-878">one two three</span></span> |
| <span data-ttu-id="abfee-879">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-879">toUpperOutput</span></span> | <span data-ttu-id="abfee-880">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-880">String</span></span> | <span data-ttu-id="abfee-881">BİR İKİ ÜÇ</span><span class="sxs-lookup"><span data-stu-id="abfee-881">ONE TWO THREE</span></span> |

<a id="trim" />

## <a name="trim"></a><span data-ttu-id="abfee-882">Kırpma</span><span class="sxs-lookup"><span data-stu-id="abfee-882">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="abfee-883">Belirtilen dize tüm öndeki ve sondaki boşluk karakterleri hello öğesinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="abfee-883">Removes all leading and trailing white-space characters from hello specified string.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-884">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-884">Parameters</span></span>

| <span data-ttu-id="abfee-885">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-885">Parameter</span></span> | <span data-ttu-id="abfee-886">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-886">Required</span></span> | <span data-ttu-id="abfee-887">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-887">Type</span></span> | <span data-ttu-id="abfee-888">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-888">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-889">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="abfee-889">stringToTrim</span></span> |<span data-ttu-id="abfee-890">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-890">Yes</span></span> |<span data-ttu-id="abfee-891">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-891">string</span></span> |<span data-ttu-id="abfee-892">Merhaba değeri tootrim.</span><span class="sxs-lookup"><span data-stu-id="abfee-892">hello value tootrim.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-893">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-893">Return value</span></span>

<span data-ttu-id="abfee-894">Baştaki ve sondaki boşluk karakterleri olmadan hello dizesi.</span><span class="sxs-lookup"><span data-stu-id="abfee-894">hello string without leading and trailing white-space characters.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-895">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-895">Examples</span></span>

<span data-ttu-id="abfee-896">Merhaba aşağıdaki örnek hello parametre hello boşluk karakterlerinden kırpar.</span><span class="sxs-lookup"><span data-stu-id="abfee-896">hello following example trims hello white-space characters from hello parameter.</span></span>

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

<span data-ttu-id="abfee-897">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-897">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-898">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-898">Name</span></span> | <span data-ttu-id="abfee-899">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-899">Type</span></span> | <span data-ttu-id="abfee-900">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-900">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-901">Döndür</span><span class="sxs-lookup"><span data-stu-id="abfee-901">return</span></span> | <span data-ttu-id="abfee-902">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-902">String</span></span> | <span data-ttu-id="abfee-903">Bir iki üç</span><span class="sxs-lookup"><span data-stu-id="abfee-903">one two three</span></span> |

<a id="uniquestring" />

## <a name="uniquestring"></a><span data-ttu-id="abfee-904">uniqueString</span><span class="sxs-lookup"><span data-stu-id="abfee-904">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="abfee-905">Parametre olarak sağlanan hello değerlere göre belirleyici karma dize oluşturur.</span><span class="sxs-lookup"><span data-stu-id="abfee-905">Creates a deterministic hash string based on hello values provided as parameters.</span></span> 

### <a name="parameters"></a><span data-ttu-id="abfee-906">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-906">Parameters</span></span>

| <span data-ttu-id="abfee-907">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-907">Parameter</span></span> | <span data-ttu-id="abfee-908">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-908">Required</span></span> | <span data-ttu-id="abfee-909">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-909">Type</span></span> | <span data-ttu-id="abfee-910">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-910">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-911">baseString</span><span class="sxs-lookup"><span data-stu-id="abfee-911">baseString</span></span> |<span data-ttu-id="abfee-912">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-912">Yes</span></span> |<span data-ttu-id="abfee-913">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-913">string</span></span> |<span data-ttu-id="abfee-914">Merhaba değeri benzersiz bir dize hello karma işlevi toocreate kullanılır.</span><span class="sxs-lookup"><span data-stu-id="abfee-914">hello value used in hello hash function toocreate a unique string.</span></span> |
| <span data-ttu-id="abfee-915">gerektikçe ek parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-915">additional parameters as needed</span></span> |<span data-ttu-id="abfee-916">Hayır</span><span class="sxs-lookup"><span data-stu-id="abfee-916">No</span></span> |<span data-ttu-id="abfee-917">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-917">string</span></span> |<span data-ttu-id="abfee-918">Sayıda dizeleri benzersizlik hello düzeyini belirtir gerekli toocreate hello değeri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="abfee-918">You can add as many strings as needed toocreate hello value that specifies hello level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="abfee-919">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="abfee-919">Remarks</span></span>

<span data-ttu-id="abfee-920">Bu işlev, toocreate bir kaynak için benzersiz bir ad gerektiğinde faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="abfee-920">This function is helpful when you need toocreate a unique name for a resource.</span></span> <span data-ttu-id="abfee-921">Benzersizlik hello sonucu için hello kapsamını sınırlamak parametre değerlerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="abfee-921">You provide parameter values that limit hello scope of uniqueness for hello result.</span></span> <span data-ttu-id="abfee-922">Merhaba adı toosubscription, kaynak grubu veya dağıtım aşağı benzersiz olup olmadığını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="abfee-922">You can specify whether hello name is unique down toosubscription, resource group, or deployment.</span></span> 

<span data-ttu-id="abfee-923">Merhaba, değer rastgele bir dize değil, ancak bunun yerine bir karma işlevin sonucu hello döndürdü.</span><span class="sxs-lookup"><span data-stu-id="abfee-923">hello returned value is not a random string, but rather hello result of a hash function.</span></span> <span data-ttu-id="abfee-924">Merhaba değeri 13 karakter uzunluğunda döndürülür.</span><span class="sxs-lookup"><span data-stu-id="abfee-924">hello returned value is 13 characters long.</span></span> <span data-ttu-id="abfee-925">Genel benzersiz değil.</span><span class="sxs-lookup"><span data-stu-id="abfee-925">It is not globally unique.</span></span> <span data-ttu-id="abfee-926">Bir önek ile toocombine hello değeri, adlandırma kuralını toocreate anlamlı bir ad isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="abfee-926">You may want toocombine hello value with a prefix from your naming convention toocreate a name that is meaningful.</span></span> <span data-ttu-id="abfee-927">Merhaba aşağıdaki örnek döndürülen değer hello hello biçimi gösterir.</span><span class="sxs-lookup"><span data-stu-id="abfee-927">hello following example shows hello format of hello returned value.</span></span> <span data-ttu-id="abfee-928">Merhaba gerçek değer parametreleri sağlanan hello göre değişir.</span><span class="sxs-lookup"><span data-stu-id="abfee-928">hello actual value varies by hello provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="abfee-929">Örnek hello nasıl toouse uniqueString toocreate benzersiz bir değer için yaygın olarak kullanılan düzeylerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="abfee-929">hello following examples show how toouse uniqueString toocreate a unique value for commonly used levels.</span></span>

<span data-ttu-id="abfee-930">Benzersiz kapsamlı toosubscription</span><span class="sxs-lookup"><span data-stu-id="abfee-930">Unique scoped toosubscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="abfee-931">Benzersiz kapsamlı tooresource grubu</span><span class="sxs-lookup"><span data-stu-id="abfee-931">Unique scoped tooresource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="abfee-932">Bir kaynak grubu için benzersiz kapsamlı toodeployment</span><span class="sxs-lookup"><span data-stu-id="abfee-932">Unique scoped toodeployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="abfee-933">Aşağıdaki örnek hello nasıl toocreate bir depolama hesabı için benzersiz bir ad, kaynak grubuna göre gösterir.</span><span class="sxs-lookup"><span data-stu-id="abfee-933">hello following example shows how toocreate a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="abfee-934">Merhaba kaynak grubu içinde hello adı hello oluşturulan varsa benzersiz değil aynı şekilde.</span><span class="sxs-lookup"><span data-stu-id="abfee-934">Inside hello resource group, hello name is not unique if constructed hello same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a><span data-ttu-id="abfee-935">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-935">Return value</span></span>

<span data-ttu-id="abfee-936">13 karakter içeren bir dize.</span><span class="sxs-lookup"><span data-stu-id="abfee-936">A string containing 13 characters.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-937">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-937">Examples</span></span>

<span data-ttu-id="abfee-938">Aşağıdaki örneğine hello uniquestring sonuçları döndürür:</span><span class="sxs-lookup"><span data-stu-id="abfee-938">hello following example returns results from uniquestring:</span></span>

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

## <a name="uri"></a><span data-ttu-id="abfee-939">URI</span><span class="sxs-lookup"><span data-stu-id="abfee-939">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="abfee-940">Merhaba tabanURI ve hello relativeUri dize birleştirerek bir mutlak URI oluşturur.</span><span class="sxs-lookup"><span data-stu-id="abfee-940">Creates an absolute URI by combining hello baseUri and hello relativeUri string.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-941">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-941">Parameters</span></span>

| <span data-ttu-id="abfee-942">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-942">Parameter</span></span> | <span data-ttu-id="abfee-943">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-943">Required</span></span> | <span data-ttu-id="abfee-944">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-944">Type</span></span> | <span data-ttu-id="abfee-945">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-945">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-946">tabanURI</span><span class="sxs-lookup"><span data-stu-id="abfee-946">baseUri</span></span> |<span data-ttu-id="abfee-947">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-947">Yes</span></span> |<span data-ttu-id="abfee-948">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-948">string</span></span> |<span data-ttu-id="abfee-949">Merhaba taban URI dizesi.</span><span class="sxs-lookup"><span data-stu-id="abfee-949">hello base uri string.</span></span> |
| <span data-ttu-id="abfee-950">relativeUri</span><span class="sxs-lookup"><span data-stu-id="abfee-950">relativeUri</span></span> |<span data-ttu-id="abfee-951">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-951">Yes</span></span> |<span data-ttu-id="abfee-952">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-952">string</span></span> |<span data-ttu-id="abfee-953">Merhaba göreli URI dize tooadd toohello taban URI dize.</span><span class="sxs-lookup"><span data-stu-id="abfee-953">hello relative uri string tooadd toohello base uri string.</span></span> |

<span data-ttu-id="abfee-954">Merhaba hello için değer **tabanURI** parametresi, belirli bir dosya içerebilir, ancak yalnızca hello temel yolu hello URI oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="abfee-954">hello value for hello **baseUri** parameter can include a specific file, but only hello base path is used when constructing hello URI.</span></span> <span data-ttu-id="abfee-955">Örneğin, geçirme `http://contoso.com/resources/azuredeploy.json` temel URI'sini hello tabanURI parametre sonuç olarak `http://contoso.com/resources/`.</span><span class="sxs-lookup"><span data-stu-id="abfee-955">For example, passing `http://contoso.com/resources/azuredeploy.json` as hello baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

### <a name="return-value"></a><span data-ttu-id="abfee-956">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-956">Return value</span></span>

<span data-ttu-id="abfee-957">Merhaba temel ve göreli değerleri için mutlak URI hello temsil eden dize.</span><span class="sxs-lookup"><span data-stu-id="abfee-957">A string representing hello absolute URI for hello base and relative values.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-958">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-958">Examples</span></span>

<span data-ttu-id="abfee-959">Aşağıdaki örnek hello nasıl tooconstruct bağlantı tooa iç içe geçmiş şablonu hello üst şablonunun hello değere göre gösterir.</span><span class="sxs-lookup"><span data-stu-id="abfee-959">hello following example shows how tooconstruct a link tooa nested template based on hello value of hello parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

<span data-ttu-id="abfee-960">örnekte gösterildiği nasıl aşağıdaki hello toouse URI, uriComponent ve uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="abfee-960">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="abfee-961">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-961">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-962">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-962">Name</span></span> | <span data-ttu-id="abfee-963">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-963">Type</span></span> | <span data-ttu-id="abfee-964">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-964">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-965">uriOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-965">uriOutput</span></span> | <span data-ttu-id="abfee-966">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-966">String</span></span> | <span data-ttu-id="abfee-967">http://contoso.com/resources/Nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="abfee-967">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="abfee-968">componentOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-968">componentOutput</span></span> | <span data-ttu-id="abfee-969">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-969">String</span></span> | <span data-ttu-id="abfee-970">HTTP%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="abfee-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="abfee-971">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-971">toStringOutput</span></span> | <span data-ttu-id="abfee-972">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-972">String</span></span> | <span data-ttu-id="abfee-973">http://contoso.com/resources/Nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="abfee-973">http://contoso.com/resources/nested/azuredeploy.json</span></span> |

<a id="uricomponent" />

## <a name="uricomponent"></a><span data-ttu-id="abfee-974">uriComponent</span><span class="sxs-lookup"><span data-stu-id="abfee-974">uriComponent</span></span>
`uricomponent(stringToEncode)`

<span data-ttu-id="abfee-975">Bir URI kodlar.</span><span class="sxs-lookup"><span data-stu-id="abfee-975">Encodes a URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-976">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-976">Parameters</span></span>

| <span data-ttu-id="abfee-977">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-977">Parameter</span></span> | <span data-ttu-id="abfee-978">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-978">Required</span></span> | <span data-ttu-id="abfee-979">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-979">Type</span></span> | <span data-ttu-id="abfee-980">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-980">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-981">stringToEncode</span><span class="sxs-lookup"><span data-stu-id="abfee-981">stringToEncode</span></span> |<span data-ttu-id="abfee-982">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-982">Yes</span></span> |<span data-ttu-id="abfee-983">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-983">string</span></span> |<span data-ttu-id="abfee-984">Merhaba değeri tooencode.</span><span class="sxs-lookup"><span data-stu-id="abfee-984">hello value tooencode.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-985">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-985">Return value</span></span>

<span data-ttu-id="abfee-986">Merhaba URI dizesi değeri kodlanmış.</span><span class="sxs-lookup"><span data-stu-id="abfee-986">A string of hello URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-987">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-987">Examples</span></span>

<span data-ttu-id="abfee-988">örnekte gösterildiği nasıl aşağıdaki hello toouse URI, uriComponent ve uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="abfee-988">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="abfee-989">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-989">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-990">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-990">Name</span></span> | <span data-ttu-id="abfee-991">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-991">Type</span></span> | <span data-ttu-id="abfee-992">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-992">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-993">uriOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-993">uriOutput</span></span> | <span data-ttu-id="abfee-994">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-994">String</span></span> | <span data-ttu-id="abfee-995">http://contoso.com/resources/Nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="abfee-995">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="abfee-996">componentOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-996">componentOutput</span></span> | <span data-ttu-id="abfee-997">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-997">String</span></span> | <span data-ttu-id="abfee-998">HTTP%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="abfee-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="abfee-999">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-999">toStringOutput</span></span> | <span data-ttu-id="abfee-1000">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-1000">String</span></span> | <span data-ttu-id="abfee-1001">http://contoso.com/resources/Nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="abfee-1001">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a><span data-ttu-id="abfee-1002">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="abfee-1002">uriComponentToString</span></span>
`uriComponentToString(uriEncodedString)`

<span data-ttu-id="abfee-1003">Değer bir dize bir URI kodlanmış döndürür.</span><span class="sxs-lookup"><span data-stu-id="abfee-1003">Returns a string of a URI encoded value.</span></span>

### <a name="parameters"></a><span data-ttu-id="abfee-1004">Parametreler</span><span class="sxs-lookup"><span data-stu-id="abfee-1004">Parameters</span></span>

| <span data-ttu-id="abfee-1005">Parametre</span><span class="sxs-lookup"><span data-stu-id="abfee-1005">Parameter</span></span> | <span data-ttu-id="abfee-1006">Gerekli</span><span class="sxs-lookup"><span data-stu-id="abfee-1006">Required</span></span> | <span data-ttu-id="abfee-1007">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-1007">Type</span></span> | <span data-ttu-id="abfee-1008">Açıklama</span><span class="sxs-lookup"><span data-stu-id="abfee-1008">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="abfee-1009">uriEncodedString</span><span class="sxs-lookup"><span data-stu-id="abfee-1009">uriEncodedString</span></span> |<span data-ttu-id="abfee-1010">Evet</span><span class="sxs-lookup"><span data-stu-id="abfee-1010">Yes</span></span> |<span data-ttu-id="abfee-1011">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-1011">string</span></span> |<span data-ttu-id="abfee-1012">Merhaba URI değeri tooconvert tooa dizesi kodlanmış.</span><span class="sxs-lookup"><span data-stu-id="abfee-1012">hello URI encoded value tooconvert tooa string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="abfee-1013">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="abfee-1013">Return value</span></span>

<span data-ttu-id="abfee-1014">Bir URI kodu çözülmüş bir dize değeri kodlanmış.</span><span class="sxs-lookup"><span data-stu-id="abfee-1014">A decoded string of URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="abfee-1015">Örnekler</span><span class="sxs-lookup"><span data-stu-id="abfee-1015">Examples</span></span>

<span data-ttu-id="abfee-1016">örnekte gösterildiği nasıl aşağıdaki hello toouse URI, uriComponent ve uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="abfee-1016">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="abfee-1017">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="abfee-1017">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="abfee-1018">Ad</span><span class="sxs-lookup"><span data-stu-id="abfee-1018">Name</span></span> | <span data-ttu-id="abfee-1019">Tür</span><span class="sxs-lookup"><span data-stu-id="abfee-1019">Type</span></span> | <span data-ttu-id="abfee-1020">Değer</span><span class="sxs-lookup"><span data-stu-id="abfee-1020">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="abfee-1021">uriOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-1021">uriOutput</span></span> | <span data-ttu-id="abfee-1022">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-1022">String</span></span> | <span data-ttu-id="abfee-1023">http://contoso.com/resources/Nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="abfee-1023">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="abfee-1024">componentOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-1024">componentOutput</span></span> | <span data-ttu-id="abfee-1025">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-1025">String</span></span> | <span data-ttu-id="abfee-1026">HTTP%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="abfee-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="abfee-1027">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="abfee-1027">toStringOutput</span></span> | <span data-ttu-id="abfee-1028">Dize</span><span class="sxs-lookup"><span data-stu-id="abfee-1028">String</span></span> | <span data-ttu-id="abfee-1029">http://contoso.com/resources/Nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="abfee-1029">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


## <a name="next-steps"></a><span data-ttu-id="abfee-1030">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="abfee-1030">Next steps</span></span>
* <span data-ttu-id="abfee-1031">Bir Azure Resource Manager şablonu hello bölümlerde açıklaması için bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="abfee-1031">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="abfee-1032">birden fazla şablon toomerge bkz [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="abfee-1032">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="abfee-1033">tooiterate belirtilen sayıda kaynak türünü oluştururken bkz [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="abfee-1033">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="abfee-1034">toodeploy hello şablonu oluşturduğunuz toosee bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="abfee-1034">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

