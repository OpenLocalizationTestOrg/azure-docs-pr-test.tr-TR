---
title: "aaaAzure Resource Manager şablonu işlevleri - mantıksal | Microsoft Docs"
description: "Bir Azure Resource Manager şablonu toodetermine mantıksal değerleri Hello işlevleri toouse açıklar."
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
ms.openlocfilehash: aec6341fbde00b4eba3b4539ff9a9aec774333fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="95768-103">Azure Resource Manager şablonları için mantıksal işlevleri</span><span class="sxs-lookup"><span data-stu-id="95768-103">Logical functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="95768-104">Resource Manager şablonlarınızı içinde karşılaştırmaları yapmak için çeşitli işlevleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="95768-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="95768-105">ve</span><span class="sxs-lookup"><span data-stu-id="95768-105">and</span></span>](#and)
* [<span data-ttu-id="95768-106">bool</span><span class="sxs-lookup"><span data-stu-id="95768-106">bool</span></span>](#bool)
* [<span data-ttu-id="95768-107">Eğer</span><span class="sxs-lookup"><span data-stu-id="95768-107">if</span></span>](#if)
* [<span data-ttu-id="95768-108">değil</span><span class="sxs-lookup"><span data-stu-id="95768-108">not</span></span>](#not)
* [<span data-ttu-id="95768-109">veya</span><span class="sxs-lookup"><span data-stu-id="95768-109">or</span></span>](#or)

## <a name="and"></a><span data-ttu-id="95768-110">ve</span><span class="sxs-lookup"><span data-stu-id="95768-110">and</span></span>
`and(arg1, arg2)`

<span data-ttu-id="95768-111">Her iki parametre değeri doğru olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="95768-111">Checks whether both parameter values are true.</span></span>

### <a name="parameters"></a><span data-ttu-id="95768-112">Parametreler</span><span class="sxs-lookup"><span data-stu-id="95768-112">Parameters</span></span>

| <span data-ttu-id="95768-113">Parametre</span><span class="sxs-lookup"><span data-stu-id="95768-113">Parameter</span></span> | <span data-ttu-id="95768-114">Gerekli</span><span class="sxs-lookup"><span data-stu-id="95768-114">Required</span></span> | <span data-ttu-id="95768-115">Tür</span><span class="sxs-lookup"><span data-stu-id="95768-115">Type</span></span> | <span data-ttu-id="95768-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="95768-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="95768-117">arg1</span><span class="sxs-lookup"><span data-stu-id="95768-117">arg1</span></span> |<span data-ttu-id="95768-118">Evet</span><span class="sxs-lookup"><span data-stu-id="95768-118">Yes</span></span> |<span data-ttu-id="95768-119">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="95768-119">boolean</span></span> |<span data-ttu-id="95768-120">ilk değer toocheck olup hello doğrudur.</span><span class="sxs-lookup"><span data-stu-id="95768-120">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="95768-121">arg2</span><span class="sxs-lookup"><span data-stu-id="95768-121">arg2</span></span> |<span data-ttu-id="95768-122">Evet</span><span class="sxs-lookup"><span data-stu-id="95768-122">Yes</span></span> |<span data-ttu-id="95768-123">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="95768-123">boolean</span></span> |<span data-ttu-id="95768-124">İkinci değer toocheck olup hello doğrudur.</span><span class="sxs-lookup"><span data-stu-id="95768-124">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="95768-125">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="95768-125">Return value</span></span>

<span data-ttu-id="95768-126">Döndürür **True** her iki değeri varsa true, aksi takdirde **False**.</span><span class="sxs-lookup"><span data-stu-id="95768-126">Returns **True** if both values are true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="95768-127">Örnekler</span><span class="sxs-lookup"><span data-stu-id="95768-127">Examples</span></span>

<span data-ttu-id="95768-128">örnekte gösterildiği nasıl aşağıdaki hello toouse mantıksal işlevleri.</span><span class="sxs-lookup"><span data-stu-id="95768-128">hello following example shows how toouse logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="95768-129">Örnek önceki hello Hello çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="95768-129">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="95768-130">Ad</span><span class="sxs-lookup"><span data-stu-id="95768-130">Name</span></span> | <span data-ttu-id="95768-131">Tür</span><span class="sxs-lookup"><span data-stu-id="95768-131">Type</span></span> | <span data-ttu-id="95768-132">Değer</span><span class="sxs-lookup"><span data-stu-id="95768-132">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="95768-133">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="95768-133">andExampleOutput</span></span> | <span data-ttu-id="95768-134">bool</span><span class="sxs-lookup"><span data-stu-id="95768-134">Bool</span></span> | <span data-ttu-id="95768-135">False</span><span class="sxs-lookup"><span data-stu-id="95768-135">False</span></span> |
| <span data-ttu-id="95768-136">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="95768-136">orExampleOutput</span></span> | <span data-ttu-id="95768-137">bool</span><span class="sxs-lookup"><span data-stu-id="95768-137">Bool</span></span> | <span data-ttu-id="95768-138">True</span><span class="sxs-lookup"><span data-stu-id="95768-138">True</span></span> |
| <span data-ttu-id="95768-139">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="95768-139">notExampleOutput</span></span> | <span data-ttu-id="95768-140">bool</span><span class="sxs-lookup"><span data-stu-id="95768-140">Bool</span></span> | <span data-ttu-id="95768-141">False</span><span class="sxs-lookup"><span data-stu-id="95768-141">False</span></span> |


## <a name="bool"></a><span data-ttu-id="95768-142">bool</span><span class="sxs-lookup"><span data-stu-id="95768-142">bool</span></span>
`bool(arg1)`

<span data-ttu-id="95768-143">Dönüştürür hello parametresi tooa boolean.</span><span class="sxs-lookup"><span data-stu-id="95768-143">Converts hello parameter tooa boolean.</span></span>

### <a name="parameters"></a><span data-ttu-id="95768-144">Parametreler</span><span class="sxs-lookup"><span data-stu-id="95768-144">Parameters</span></span>

| <span data-ttu-id="95768-145">Parametre</span><span class="sxs-lookup"><span data-stu-id="95768-145">Parameter</span></span> | <span data-ttu-id="95768-146">Gerekli</span><span class="sxs-lookup"><span data-stu-id="95768-146">Required</span></span> | <span data-ttu-id="95768-147">Tür</span><span class="sxs-lookup"><span data-stu-id="95768-147">Type</span></span> | <span data-ttu-id="95768-148">Açıklama</span><span class="sxs-lookup"><span data-stu-id="95768-148">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="95768-149">arg1</span><span class="sxs-lookup"><span data-stu-id="95768-149">arg1</span></span> |<span data-ttu-id="95768-150">Evet</span><span class="sxs-lookup"><span data-stu-id="95768-150">Yes</span></span> |<span data-ttu-id="95768-151">dize veya int</span><span class="sxs-lookup"><span data-stu-id="95768-151">string or int</span></span> |<span data-ttu-id="95768-152">değer tooconvert tooa hello boolean.</span><span class="sxs-lookup"><span data-stu-id="95768-152">hello value tooconvert tooa boolean.</span></span> |

### <a name="return-value"></a><span data-ttu-id="95768-153">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="95768-153">Return value</span></span>
<span data-ttu-id="95768-154">Merhaba, bir Boole değeri dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="95768-154">A boolean of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="95768-155">Örnekler</span><span class="sxs-lookup"><span data-stu-id="95768-155">Examples</span></span>

<span data-ttu-id="95768-156">örnekte gösterildiği nasıl aşağıdaki hello toouse bool bir string veya tamsayı.</span><span class="sxs-lookup"><span data-stu-id="95768-156">hello following example shows how toouse bool with a string or integer.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "trueString": {
            "value": "[bool('true')]",
            "type" : "bool"
        },
        "falseString": {
            "value": "[bool('false')]",
            "type" : "bool"
        },
        "trueInt": {
            "value": "[bool(1)]",
            "type" : "bool"
        },
        "falseInt": {
            "value": "[bool(0)]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="95768-157">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="95768-157">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="95768-158">Ad</span><span class="sxs-lookup"><span data-stu-id="95768-158">Name</span></span> | <span data-ttu-id="95768-159">Tür</span><span class="sxs-lookup"><span data-stu-id="95768-159">Type</span></span> | <span data-ttu-id="95768-160">Değer</span><span class="sxs-lookup"><span data-stu-id="95768-160">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="95768-161">trueString</span><span class="sxs-lookup"><span data-stu-id="95768-161">trueString</span></span> | <span data-ttu-id="95768-162">bool</span><span class="sxs-lookup"><span data-stu-id="95768-162">Bool</span></span> | <span data-ttu-id="95768-163">True</span><span class="sxs-lookup"><span data-stu-id="95768-163">True</span></span> |
| <span data-ttu-id="95768-164">falseString</span><span class="sxs-lookup"><span data-stu-id="95768-164">falseString</span></span> | <span data-ttu-id="95768-165">bool</span><span class="sxs-lookup"><span data-stu-id="95768-165">Bool</span></span> | <span data-ttu-id="95768-166">False</span><span class="sxs-lookup"><span data-stu-id="95768-166">False</span></span> |
| <span data-ttu-id="95768-167">trueInt</span><span class="sxs-lookup"><span data-stu-id="95768-167">trueInt</span></span> | <span data-ttu-id="95768-168">bool</span><span class="sxs-lookup"><span data-stu-id="95768-168">Bool</span></span> | <span data-ttu-id="95768-169">True</span><span class="sxs-lookup"><span data-stu-id="95768-169">True</span></span> |
| <span data-ttu-id="95768-170">falseInt</span><span class="sxs-lookup"><span data-stu-id="95768-170">falseInt</span></span> | <span data-ttu-id="95768-171">bool</span><span class="sxs-lookup"><span data-stu-id="95768-171">Bool</span></span> | <span data-ttu-id="95768-172">False</span><span class="sxs-lookup"><span data-stu-id="95768-172">False</span></span> |

## <a name="if"></a><span data-ttu-id="95768-173">Eğer</span><span class="sxs-lookup"><span data-stu-id="95768-173">if</span></span>
`if(condition, trueValue, falseValue)`

<span data-ttu-id="95768-174">Bir değer olup olmadığına göre göre döndürür bir koşul true veya false.</span><span class="sxs-lookup"><span data-stu-id="95768-174">Returns a value based on whether a condition is true or false.</span></span>

### <a name="parameters"></a><span data-ttu-id="95768-175">Parametreler</span><span class="sxs-lookup"><span data-stu-id="95768-175">Parameters</span></span>

| <span data-ttu-id="95768-176">Parametre</span><span class="sxs-lookup"><span data-stu-id="95768-176">Parameter</span></span> | <span data-ttu-id="95768-177">Gerekli</span><span class="sxs-lookup"><span data-stu-id="95768-177">Required</span></span> | <span data-ttu-id="95768-178">Tür</span><span class="sxs-lookup"><span data-stu-id="95768-178">Type</span></span> | <span data-ttu-id="95768-179">Açıklama</span><span class="sxs-lookup"><span data-stu-id="95768-179">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="95768-180">Koşul</span><span class="sxs-lookup"><span data-stu-id="95768-180">condition</span></span> |<span data-ttu-id="95768-181">Evet</span><span class="sxs-lookup"><span data-stu-id="95768-181">Yes</span></span> |<span data-ttu-id="95768-182">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="95768-182">boolean</span></span> |<span data-ttu-id="95768-183">doğru olup olmadığını değeri toocheck hello.</span><span class="sxs-lookup"><span data-stu-id="95768-183">hello value toocheck whether it is true.</span></span> |
| <span data-ttu-id="95768-184">trueValue</span><span class="sxs-lookup"><span data-stu-id="95768-184">trueValue</span></span> |<span data-ttu-id="95768-185">Evet</span><span class="sxs-lookup"><span data-stu-id="95768-185">Yes</span></span> | <span data-ttu-id="95768-186">dize, int, nesne veya dizi</span><span class="sxs-lookup"><span data-stu-id="95768-186">string, int, object, or array</span></span> |<span data-ttu-id="95768-187">Merhaba koşulun doğru olması durumunda hello değeri tooreturn.</span><span class="sxs-lookup"><span data-stu-id="95768-187">hello value tooreturn when hello condition is true.</span></span> |
| <span data-ttu-id="95768-188">false değerini</span><span class="sxs-lookup"><span data-stu-id="95768-188">falseValue</span></span> |<span data-ttu-id="95768-189">Evet</span><span class="sxs-lookup"><span data-stu-id="95768-189">Yes</span></span> | <span data-ttu-id="95768-190">dize, int, nesne veya dizi</span><span class="sxs-lookup"><span data-stu-id="95768-190">string, int, object, or array</span></span> |<span data-ttu-id="95768-191">Merhaba koşul yanlış olduğunda hello değeri tooreturn.</span><span class="sxs-lookup"><span data-stu-id="95768-191">hello value tooreturn when hello condition is false.</span></span> |

### <a name="return-value"></a><span data-ttu-id="95768-192">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="95768-192">Return value</span></span>

<span data-ttu-id="95768-193">İkinci parametre ilk parametre olduğunda döndürür **True**; Aksi halde, üçüncü parametre döndürür.</span><span class="sxs-lookup"><span data-stu-id="95768-193">Returns second parameter when first parameter is **True**; otherwise, returns third parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="95768-194">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="95768-194">Remarks</span></span>

<span data-ttu-id="95768-195">Bu işlev tooconditionally kümesi bir kaynak özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95768-195">You can use this function tooconditionally set a resource property.</span></span> <span data-ttu-id="95768-196">Merhaba aşağıdaki örnekte tam bir şablon değildir, ancak koşullu hello kullanılabilirlik kümesi ayarlamak için ilgili bölümleri hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="95768-196">hello following example is not a full template, but it shows hello relevant portions for conditionally setting hello availability set.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "availabilitySet": {
            "type": "string",
            "allowedValues": [
                "yes",
                "no"
            ]
        }
    },
    "variables": {
        ...
        "availabilitySetName": "availabilitySet1",
        "availabilitySet": {
            "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
        }
    },
    "resources": [
        {
            "condition": "[equals(parameters('availabilitySet'),'yes')]",
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            ...
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "properties": {
                "availabilitySet": "[if(equals(parameters('availabilitySet'),'yes'), variables('availabilitySet'), json('null'))]",
                ...
            }
        },
        ...
    ],
    ...
}
```

### <a name="examples"></a><span data-ttu-id="95768-197">Örnekler</span><span class="sxs-lookup"><span data-stu-id="95768-197">Examples</span></span>

<span data-ttu-id="95768-198">örnekte gösterildiği nasıl aşağıdaki hello toouse hello `if` işlevi.</span><span class="sxs-lookup"><span data-stu-id="95768-198">hello following example shows how toouse hello `if` function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "yesOutput": {
            "type": "string",
            "value": "[if(equals('a', 'a'), 'yes', 'no')]"
        },
        "noOutput": {
            "type": "string",
            "value": "[if(equals('a', 'b'), 'yes', 'no')]"
        }
    }
}
```

<span data-ttu-id="95768-199">Örnek önceki hello Hello çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="95768-199">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="95768-200">Ad</span><span class="sxs-lookup"><span data-stu-id="95768-200">Name</span></span> | <span data-ttu-id="95768-201">Tür</span><span class="sxs-lookup"><span data-stu-id="95768-201">Type</span></span> | <span data-ttu-id="95768-202">Değer</span><span class="sxs-lookup"><span data-stu-id="95768-202">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="95768-203">yesOutput</span><span class="sxs-lookup"><span data-stu-id="95768-203">yesOutput</span></span> | <span data-ttu-id="95768-204">Dize</span><span class="sxs-lookup"><span data-stu-id="95768-204">String</span></span> | <span data-ttu-id="95768-205">Evet</span><span class="sxs-lookup"><span data-stu-id="95768-205">yes</span></span> |
| <span data-ttu-id="95768-206">noOutput</span><span class="sxs-lookup"><span data-stu-id="95768-206">noOutput</span></span> | <span data-ttu-id="95768-207">Dize</span><span class="sxs-lookup"><span data-stu-id="95768-207">String</span></span> | <span data-ttu-id="95768-208">Yok</span><span class="sxs-lookup"><span data-stu-id="95768-208">no</span></span> |


## <a name="not"></a><span data-ttu-id="95768-209">değil</span><span class="sxs-lookup"><span data-stu-id="95768-209">not</span></span>
`not(arg1)`

<span data-ttu-id="95768-210">Boole değeri tooits dönüştürür ters değeri.</span><span class="sxs-lookup"><span data-stu-id="95768-210">Converts boolean value tooits opposite value.</span></span>

### <a name="parameters"></a><span data-ttu-id="95768-211">Parametreler</span><span class="sxs-lookup"><span data-stu-id="95768-211">Parameters</span></span>

| <span data-ttu-id="95768-212">Parametre</span><span class="sxs-lookup"><span data-stu-id="95768-212">Parameter</span></span> | <span data-ttu-id="95768-213">Gerekli</span><span class="sxs-lookup"><span data-stu-id="95768-213">Required</span></span> | <span data-ttu-id="95768-214">Tür</span><span class="sxs-lookup"><span data-stu-id="95768-214">Type</span></span> | <span data-ttu-id="95768-215">Açıklama</span><span class="sxs-lookup"><span data-stu-id="95768-215">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="95768-216">arg1</span><span class="sxs-lookup"><span data-stu-id="95768-216">arg1</span></span> |<span data-ttu-id="95768-217">Evet</span><span class="sxs-lookup"><span data-stu-id="95768-217">Yes</span></span> |<span data-ttu-id="95768-218">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="95768-218">boolean</span></span> |<span data-ttu-id="95768-219">Merhaba değeri tooconvert.</span><span class="sxs-lookup"><span data-stu-id="95768-219">hello value tooconvert.</span></span> |


### <a name="return-value"></a><span data-ttu-id="95768-220">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="95768-220">Return value</span></span>

<span data-ttu-id="95768-221">Döndürür **True** parametresi olduğunda **False**.</span><span class="sxs-lookup"><span data-stu-id="95768-221">Returns **True** when parameter is **False**.</span></span> <span data-ttu-id="95768-222">Döndürür **False** parametresi olduğunda **doğru**.</span><span class="sxs-lookup"><span data-stu-id="95768-222">Returns **False** when parameter is **True**.</span></span>

### <a name="examples"></a><span data-ttu-id="95768-223">Örnekler</span><span class="sxs-lookup"><span data-stu-id="95768-223">Examples</span></span>

<span data-ttu-id="95768-224">örnekte gösterildiği nasıl aşağıdaki hello toouse mantıksal işlevleri.</span><span class="sxs-lookup"><span data-stu-id="95768-224">hello following example shows how toouse logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="95768-225">Örnek önceki hello Hello çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="95768-225">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="95768-226">Ad</span><span class="sxs-lookup"><span data-stu-id="95768-226">Name</span></span> | <span data-ttu-id="95768-227">Tür</span><span class="sxs-lookup"><span data-stu-id="95768-227">Type</span></span> | <span data-ttu-id="95768-228">Değer</span><span class="sxs-lookup"><span data-stu-id="95768-228">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="95768-229">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="95768-229">andExampleOutput</span></span> | <span data-ttu-id="95768-230">bool</span><span class="sxs-lookup"><span data-stu-id="95768-230">Bool</span></span> | <span data-ttu-id="95768-231">False</span><span class="sxs-lookup"><span data-stu-id="95768-231">False</span></span> |
| <span data-ttu-id="95768-232">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="95768-232">orExampleOutput</span></span> | <span data-ttu-id="95768-233">bool</span><span class="sxs-lookup"><span data-stu-id="95768-233">Bool</span></span> | <span data-ttu-id="95768-234">True</span><span class="sxs-lookup"><span data-stu-id="95768-234">True</span></span> |
| <span data-ttu-id="95768-235">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="95768-235">notExampleOutput</span></span> | <span data-ttu-id="95768-236">bool</span><span class="sxs-lookup"><span data-stu-id="95768-236">Bool</span></span> | <span data-ttu-id="95768-237">False</span><span class="sxs-lookup"><span data-stu-id="95768-237">False</span></span> |

<span data-ttu-id="95768-238">Merhaba aşağıdaki örnek kullanır **değil** ile [eşittir](resource-group-template-functions-comparison.md#equals).</span><span class="sxs-lookup"><span data-stu-id="95768-238">hello following example uses **not** with [equals](resource-group-template-functions-comparison.md#equals).</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "checkNotEquals": {
            "type": "bool",
            "value": "[not(equals(1, 2))]"
        }
    }
```

<span data-ttu-id="95768-239">Örnek önceki hello Hello çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="95768-239">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="95768-240">Ad</span><span class="sxs-lookup"><span data-stu-id="95768-240">Name</span></span> | <span data-ttu-id="95768-241">Tür</span><span class="sxs-lookup"><span data-stu-id="95768-241">Type</span></span> | <span data-ttu-id="95768-242">Değer</span><span class="sxs-lookup"><span data-stu-id="95768-242">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="95768-243">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="95768-243">checkNotEquals</span></span> | <span data-ttu-id="95768-244">bool</span><span class="sxs-lookup"><span data-stu-id="95768-244">Bool</span></span> | <span data-ttu-id="95768-245">True</span><span class="sxs-lookup"><span data-stu-id="95768-245">True</span></span> |


## <a name="or"></a><span data-ttu-id="95768-246">or</span><span class="sxs-lookup"><span data-stu-id="95768-246">or</span></span>
`or(arg1, arg2)`

<span data-ttu-id="95768-247">Her iki parametre değeri doğru olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="95768-247">Checks whether either parameter value is true.</span></span>

### <a name="parameters"></a><span data-ttu-id="95768-248">Parametreler</span><span class="sxs-lookup"><span data-stu-id="95768-248">Parameters</span></span>

| <span data-ttu-id="95768-249">Parametre</span><span class="sxs-lookup"><span data-stu-id="95768-249">Parameter</span></span> | <span data-ttu-id="95768-250">Gerekli</span><span class="sxs-lookup"><span data-stu-id="95768-250">Required</span></span> | <span data-ttu-id="95768-251">Tür</span><span class="sxs-lookup"><span data-stu-id="95768-251">Type</span></span> | <span data-ttu-id="95768-252">Açıklama</span><span class="sxs-lookup"><span data-stu-id="95768-252">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="95768-253">arg1</span><span class="sxs-lookup"><span data-stu-id="95768-253">arg1</span></span> |<span data-ttu-id="95768-254">Evet</span><span class="sxs-lookup"><span data-stu-id="95768-254">Yes</span></span> |<span data-ttu-id="95768-255">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="95768-255">boolean</span></span> |<span data-ttu-id="95768-256">ilk değer toocheck olup hello doğrudur.</span><span class="sxs-lookup"><span data-stu-id="95768-256">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="95768-257">arg2</span><span class="sxs-lookup"><span data-stu-id="95768-257">arg2</span></span> |<span data-ttu-id="95768-258">Evet</span><span class="sxs-lookup"><span data-stu-id="95768-258">Yes</span></span> |<span data-ttu-id="95768-259">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="95768-259">boolean</span></span> |<span data-ttu-id="95768-260">İkinci değer toocheck olup hello doğrudur.</span><span class="sxs-lookup"><span data-stu-id="95768-260">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="95768-261">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="95768-261">Return value</span></span>

<span data-ttu-id="95768-262">Döndürür **True** ya da değeri geçerliyse true, aksi takdirde **False**.</span><span class="sxs-lookup"><span data-stu-id="95768-262">Returns **True** if either value is true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="95768-263">Örnekler</span><span class="sxs-lookup"><span data-stu-id="95768-263">Examples</span></span>

<span data-ttu-id="95768-264">örnekte gösterildiği nasıl aşağıdaki hello toouse mantıksal işlevleri.</span><span class="sxs-lookup"><span data-stu-id="95768-264">hello following example shows how toouse logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="95768-265">Örnek önceki hello Hello çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="95768-265">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="95768-266">Ad</span><span class="sxs-lookup"><span data-stu-id="95768-266">Name</span></span> | <span data-ttu-id="95768-267">Tür</span><span class="sxs-lookup"><span data-stu-id="95768-267">Type</span></span> | <span data-ttu-id="95768-268">Değer</span><span class="sxs-lookup"><span data-stu-id="95768-268">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="95768-269">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="95768-269">andExampleOutput</span></span> | <span data-ttu-id="95768-270">bool</span><span class="sxs-lookup"><span data-stu-id="95768-270">Bool</span></span> | <span data-ttu-id="95768-271">False</span><span class="sxs-lookup"><span data-stu-id="95768-271">False</span></span> |
| <span data-ttu-id="95768-272">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="95768-272">orExampleOutput</span></span> | <span data-ttu-id="95768-273">bool</span><span class="sxs-lookup"><span data-stu-id="95768-273">Bool</span></span> | <span data-ttu-id="95768-274">True</span><span class="sxs-lookup"><span data-stu-id="95768-274">True</span></span> |
| <span data-ttu-id="95768-275">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="95768-275">notExampleOutput</span></span> | <span data-ttu-id="95768-276">bool</span><span class="sxs-lookup"><span data-stu-id="95768-276">Bool</span></span> | <span data-ttu-id="95768-277">False</span><span class="sxs-lookup"><span data-stu-id="95768-277">False</span></span> |


## <a name="next-steps"></a><span data-ttu-id="95768-278">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="95768-278">Next steps</span></span>
* <span data-ttu-id="95768-279">Bir Azure Resource Manager şablonu hello bölümlerde açıklaması için bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="95768-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="95768-280">birden fazla şablon toomerge bkz [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="95768-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="95768-281">tooiterate belirtilen sayıda kaynak türünü oluştururken bkz [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="95768-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="95768-282">toodeploy hello şablonu oluşturduğunuz toosee bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="95768-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

