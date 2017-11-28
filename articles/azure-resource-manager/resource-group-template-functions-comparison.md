---
title: "aaaAzure Resource Manager şablonu işlevleri - karşılaştırma | Microsoft Docs"
description: "Bir Azure Resource Manager şablonu toocompare değerleri Hello işlevleri toouse açıklar."
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
ms.openlocfilehash: ebcfc9ed6c93f8b540ec4c066e9457c621800b7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="67720-103">Azure Resource Manager şablonları için karşılaştırma işlevleri</span><span class="sxs-lookup"><span data-stu-id="67720-103">Comparison functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="67720-104">Resource Manager şablonlarınızı içinde karşılaştırmaları yapmak için çeşitli işlevleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="67720-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="67720-105">eşittir</span><span class="sxs-lookup"><span data-stu-id="67720-105">equals</span></span>](#equals)
* [<span data-ttu-id="67720-106">büyük</span><span class="sxs-lookup"><span data-stu-id="67720-106">greater</span></span>](#greater)
* [<span data-ttu-id="67720-107">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="67720-107">greaterOrEquals</span></span>](#greaterorequals)
* [<span data-ttu-id="67720-108">daha az</span><span class="sxs-lookup"><span data-stu-id="67720-108">less</span></span>](#less)
* [<span data-ttu-id="67720-109">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="67720-109">lessOrEquals</span></span>](#lessorequals)

## <a name="equals"></a><span data-ttu-id="67720-110">eşittir</span><span class="sxs-lookup"><span data-stu-id="67720-110">equals</span></span>
`equals(arg1, arg2)`

<span data-ttu-id="67720-111">İki değerin birbirine eşit olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="67720-111">Checks whether two values equal each other.</span></span>

### <a name="parameters"></a><span data-ttu-id="67720-112">Parametreler</span><span class="sxs-lookup"><span data-stu-id="67720-112">Parameters</span></span>

| <span data-ttu-id="67720-113">Parametre</span><span class="sxs-lookup"><span data-stu-id="67720-113">Parameter</span></span> | <span data-ttu-id="67720-114">Gerekli</span><span class="sxs-lookup"><span data-stu-id="67720-114">Required</span></span> | <span data-ttu-id="67720-115">Tür</span><span class="sxs-lookup"><span data-stu-id="67720-115">Type</span></span> | <span data-ttu-id="67720-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="67720-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67720-117">arg1</span><span class="sxs-lookup"><span data-stu-id="67720-117">arg1</span></span> |<span data-ttu-id="67720-118">Evet</span><span class="sxs-lookup"><span data-stu-id="67720-118">Yes</span></span> |<span data-ttu-id="67720-119">int, string, dizi veya nesne</span><span class="sxs-lookup"><span data-stu-id="67720-119">int, string, array, or object</span></span> |<span data-ttu-id="67720-120">Merhaba ilk değer toocheck eşitlik için.</span><span class="sxs-lookup"><span data-stu-id="67720-120">hello first value toocheck for equality.</span></span> |
| <span data-ttu-id="67720-121">arg2</span><span class="sxs-lookup"><span data-stu-id="67720-121">arg2</span></span> |<span data-ttu-id="67720-122">Evet</span><span class="sxs-lookup"><span data-stu-id="67720-122">Yes</span></span> |<span data-ttu-id="67720-123">int, string, dizi veya nesne</span><span class="sxs-lookup"><span data-stu-id="67720-123">int, string, array, or object</span></span> |<span data-ttu-id="67720-124">Merhaba ikinci değer toocheck eşitlik için.</span><span class="sxs-lookup"><span data-stu-id="67720-124">hello second value toocheck for equality.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67720-125">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="67720-125">Return value</span></span>

<span data-ttu-id="67720-126">Döndürür **True** hello değerler eşit; Aksi takdirde ise **False**.</span><span class="sxs-lookup"><span data-stu-id="67720-126">Returns **True** if hello values are equal; otherwise, **False**.</span></span>

### <a name="remarks"></a><span data-ttu-id="67720-127">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="67720-127">Remarks</span></span>

<span data-ttu-id="67720-128">Merhaba equals işlevi genellikle hello ile kullanılan `condition` öğesi tootest bir kaynak olup olmadığını dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="67720-128">hello equals function is often used with hello `condition` element tootest whether a resource is deployed.</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

### <a name="example"></a><span data-ttu-id="67720-129">Örnek</span><span class="sxs-lookup"><span data-stu-id="67720-129">Example</span></span>

<span data-ttu-id="67720-130">Merhaba örnek şablonu farklı türlerdeki eşitlik için değerleri denetler.</span><span class="sxs-lookup"><span data-stu-id="67720-130">hello example template checks different types of values for equality.</span></span> <span data-ttu-id="67720-131">Tüm hello varsayılan değerler True döndürür.</span><span class="sxs-lookup"><span data-stu-id="67720-131">All hello default values return True.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 1
        },
        "firstString": {
            "type": "string",
            "defaultValue": "a"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "firstObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[equals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[equals(parameters('firstString'), parameters('secondString'))]"
        },
        "checkArrays": {
            "type": "bool",
            "value": "[equals(parameters('firstArray'), parameters('secondArray'))]"
        },
        "checkObjects": {
            "type": "bool",
            "value": "[equals(parameters('firstObject'), parameters('secondObject'))]"
        }
    }
}
```

<span data-ttu-id="67720-132">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="67720-132">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="67720-133">Ad</span><span class="sxs-lookup"><span data-stu-id="67720-133">Name</span></span> | <span data-ttu-id="67720-134">Tür</span><span class="sxs-lookup"><span data-stu-id="67720-134">Type</span></span> | <span data-ttu-id="67720-135">Değer</span><span class="sxs-lookup"><span data-stu-id="67720-135">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67720-136">checkInts</span><span class="sxs-lookup"><span data-stu-id="67720-136">checkInts</span></span> | <span data-ttu-id="67720-137">bool</span><span class="sxs-lookup"><span data-stu-id="67720-137">Bool</span></span> | <span data-ttu-id="67720-138">True</span><span class="sxs-lookup"><span data-stu-id="67720-138">True</span></span> |
| <span data-ttu-id="67720-139">checkStrings</span><span class="sxs-lookup"><span data-stu-id="67720-139">checkStrings</span></span> | <span data-ttu-id="67720-140">bool</span><span class="sxs-lookup"><span data-stu-id="67720-140">Bool</span></span> | <span data-ttu-id="67720-141">True</span><span class="sxs-lookup"><span data-stu-id="67720-141">True</span></span> |
| <span data-ttu-id="67720-142">checkArrays</span><span class="sxs-lookup"><span data-stu-id="67720-142">checkArrays</span></span> | <span data-ttu-id="67720-143">bool</span><span class="sxs-lookup"><span data-stu-id="67720-143">Bool</span></span> | <span data-ttu-id="67720-144">True</span><span class="sxs-lookup"><span data-stu-id="67720-144">True</span></span> |
| <span data-ttu-id="67720-145">checkObjects</span><span class="sxs-lookup"><span data-stu-id="67720-145">checkObjects</span></span> | <span data-ttu-id="67720-146">bool</span><span class="sxs-lookup"><span data-stu-id="67720-146">Bool</span></span> | <span data-ttu-id="67720-147">True</span><span class="sxs-lookup"><span data-stu-id="67720-147">True</span></span> |


<span data-ttu-id="67720-148">Merhaba aşağıdaki örnek kullanır [değil](resource-group-template-functions-logical.md#not) ile **eşittir**.</span><span class="sxs-lookup"><span data-stu-id="67720-148">hello following example uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span></span>

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

<span data-ttu-id="67720-149">Örnek önceki hello Hello çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="67720-149">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="67720-150">Ad</span><span class="sxs-lookup"><span data-stu-id="67720-150">Name</span></span> | <span data-ttu-id="67720-151">Tür</span><span class="sxs-lookup"><span data-stu-id="67720-151">Type</span></span> | <span data-ttu-id="67720-152">Değer</span><span class="sxs-lookup"><span data-stu-id="67720-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67720-153">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="67720-153">checkNotEquals</span></span> | <span data-ttu-id="67720-154">bool</span><span class="sxs-lookup"><span data-stu-id="67720-154">Bool</span></span> | <span data-ttu-id="67720-155">True</span><span class="sxs-lookup"><span data-stu-id="67720-155">True</span></span> |


## <a name="greater"></a><span data-ttu-id="67720-156">büyük</span><span class="sxs-lookup"><span data-stu-id="67720-156">greater</span></span>
`greater(arg1, arg2)`

<span data-ttu-id="67720-157">Merhaba ilk değer hello ikinci değerden daha büyük olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="67720-157">Checks whether hello first value is greater than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="67720-158">Parametreler</span><span class="sxs-lookup"><span data-stu-id="67720-158">Parameters</span></span>

| <span data-ttu-id="67720-159">Parametre</span><span class="sxs-lookup"><span data-stu-id="67720-159">Parameter</span></span> | <span data-ttu-id="67720-160">Gerekli</span><span class="sxs-lookup"><span data-stu-id="67720-160">Required</span></span> | <span data-ttu-id="67720-161">Tür</span><span class="sxs-lookup"><span data-stu-id="67720-161">Type</span></span> | <span data-ttu-id="67720-162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="67720-162">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67720-163">arg1</span><span class="sxs-lookup"><span data-stu-id="67720-163">arg1</span></span> |<span data-ttu-id="67720-164">Evet</span><span class="sxs-lookup"><span data-stu-id="67720-164">Yes</span></span> |<span data-ttu-id="67720-165">int veya dize</span><span class="sxs-lookup"><span data-stu-id="67720-165">int or string</span></span> |<span data-ttu-id="67720-166">Merhaba hello büyük karşılaştırma için ilk değer.</span><span class="sxs-lookup"><span data-stu-id="67720-166">hello first value for hello greater comparison.</span></span> |
| <span data-ttu-id="67720-167">arg2</span><span class="sxs-lookup"><span data-stu-id="67720-167">arg2</span></span> |<span data-ttu-id="67720-168">Evet</span><span class="sxs-lookup"><span data-stu-id="67720-168">Yes</span></span> |<span data-ttu-id="67720-169">int veya dize</span><span class="sxs-lookup"><span data-stu-id="67720-169">int or string</span></span> |<span data-ttu-id="67720-170">Merhaba hello büyük karşılaştırma için ikinci değer.</span><span class="sxs-lookup"><span data-stu-id="67720-170">hello second value for hello greater comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67720-171">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="67720-171">Return value</span></span>

<span data-ttu-id="67720-172">Döndürür **True** hello ilk değer, hello ikinci değerden daha büyük Aksi takdirde **False**.</span><span class="sxs-lookup"><span data-stu-id="67720-172">Returns **True** if hello first value is greater than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="67720-173">Örnek</span><span class="sxs-lookup"><span data-stu-id="67720-173">Example</span></span>

<span data-ttu-id="67720-174">Merhaba örnek şablon hello bir değer hello diğer büyük olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="67720-174">hello example template checks whether hello one value is greater than hello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greater(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greater(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="67720-175">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="67720-175">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="67720-176">Ad</span><span class="sxs-lookup"><span data-stu-id="67720-176">Name</span></span> | <span data-ttu-id="67720-177">Tür</span><span class="sxs-lookup"><span data-stu-id="67720-177">Type</span></span> | <span data-ttu-id="67720-178">Değer</span><span class="sxs-lookup"><span data-stu-id="67720-178">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67720-179">checkInts</span><span class="sxs-lookup"><span data-stu-id="67720-179">checkInts</span></span> | <span data-ttu-id="67720-180">bool</span><span class="sxs-lookup"><span data-stu-id="67720-180">Bool</span></span> | <span data-ttu-id="67720-181">False</span><span class="sxs-lookup"><span data-stu-id="67720-181">False</span></span> |
| <span data-ttu-id="67720-182">checkStrings</span><span class="sxs-lookup"><span data-stu-id="67720-182">checkStrings</span></span> | <span data-ttu-id="67720-183">bool</span><span class="sxs-lookup"><span data-stu-id="67720-183">Bool</span></span> | <span data-ttu-id="67720-184">True</span><span class="sxs-lookup"><span data-stu-id="67720-184">True</span></span> |


## <a name="greaterorequals"></a><span data-ttu-id="67720-185">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="67720-185">greaterOrEquals</span></span>
`greaterOrEquals(arg1, arg2)`

<span data-ttu-id="67720-186">Merhaba ilk değeri sıfırdan büyük veya eşit toohello ikinci değer olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="67720-186">Checks whether hello first value is greater than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="67720-187">Parametreler</span><span class="sxs-lookup"><span data-stu-id="67720-187">Parameters</span></span>

| <span data-ttu-id="67720-188">Parametre</span><span class="sxs-lookup"><span data-stu-id="67720-188">Parameter</span></span> | <span data-ttu-id="67720-189">Gerekli</span><span class="sxs-lookup"><span data-stu-id="67720-189">Required</span></span> | <span data-ttu-id="67720-190">Tür</span><span class="sxs-lookup"><span data-stu-id="67720-190">Type</span></span> | <span data-ttu-id="67720-191">Açıklama</span><span class="sxs-lookup"><span data-stu-id="67720-191">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67720-192">arg1</span><span class="sxs-lookup"><span data-stu-id="67720-192">arg1</span></span> |<span data-ttu-id="67720-193">Evet</span><span class="sxs-lookup"><span data-stu-id="67720-193">Yes</span></span> |<span data-ttu-id="67720-194">int veya dize</span><span class="sxs-lookup"><span data-stu-id="67720-194">int or string</span></span> |<span data-ttu-id="67720-195">Merhaba hello büyük veya eşit karşılaştırma için ilk değer.</span><span class="sxs-lookup"><span data-stu-id="67720-195">hello first value for hello greater or equal comparison.</span></span> |
| <span data-ttu-id="67720-196">arg2</span><span class="sxs-lookup"><span data-stu-id="67720-196">arg2</span></span> |<span data-ttu-id="67720-197">Evet</span><span class="sxs-lookup"><span data-stu-id="67720-197">Yes</span></span> |<span data-ttu-id="67720-198">int veya dize</span><span class="sxs-lookup"><span data-stu-id="67720-198">int or string</span></span> |<span data-ttu-id="67720-199">Merhaba hello büyük veya eşit karşılaştırma için ikinci değer.</span><span class="sxs-lookup"><span data-stu-id="67720-199">hello second value for hello greater or equal comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67720-200">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="67720-200">Return value</span></span>

<span data-ttu-id="67720-201">Döndürür **True** hello ilk değer sıfırdan büyük veya eşit toohello ikinci; değeriyse, aksi takdirde, **False**.</span><span class="sxs-lookup"><span data-stu-id="67720-201">Returns **True** if hello first value is greater than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="67720-202">Örnek</span><span class="sxs-lookup"><span data-stu-id="67720-202">Example</span></span>

<span data-ttu-id="67720-203">Merhaba örnek şablon hello bir değer değerinden büyük veya eşit toohello diğer denetler.</span><span class="sxs-lookup"><span data-stu-id="67720-203">hello example template checks whether hello one value is greater than or equal toohello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="67720-204">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="67720-204">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="67720-205">Ad</span><span class="sxs-lookup"><span data-stu-id="67720-205">Name</span></span> | <span data-ttu-id="67720-206">Tür</span><span class="sxs-lookup"><span data-stu-id="67720-206">Type</span></span> | <span data-ttu-id="67720-207">Değer</span><span class="sxs-lookup"><span data-stu-id="67720-207">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67720-208">checkInts</span><span class="sxs-lookup"><span data-stu-id="67720-208">checkInts</span></span> | <span data-ttu-id="67720-209">bool</span><span class="sxs-lookup"><span data-stu-id="67720-209">Bool</span></span> | <span data-ttu-id="67720-210">False</span><span class="sxs-lookup"><span data-stu-id="67720-210">False</span></span> |
| <span data-ttu-id="67720-211">checkStrings</span><span class="sxs-lookup"><span data-stu-id="67720-211">checkStrings</span></span> | <span data-ttu-id="67720-212">bool</span><span class="sxs-lookup"><span data-stu-id="67720-212">Bool</span></span> | <span data-ttu-id="67720-213">True</span><span class="sxs-lookup"><span data-stu-id="67720-213">True</span></span> |



## <a name="less"></a><span data-ttu-id="67720-214">daha az</span><span class="sxs-lookup"><span data-stu-id="67720-214">less</span></span>
`less(arg1, arg2)`

<span data-ttu-id="67720-215">Merhaba ilk değer küçük olup olmadığını ikinci değer hello denetler.</span><span class="sxs-lookup"><span data-stu-id="67720-215">Checks whether hello first value is less than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="67720-216">Parametreler</span><span class="sxs-lookup"><span data-stu-id="67720-216">Parameters</span></span>

| <span data-ttu-id="67720-217">Parametre</span><span class="sxs-lookup"><span data-stu-id="67720-217">Parameter</span></span> | <span data-ttu-id="67720-218">Gerekli</span><span class="sxs-lookup"><span data-stu-id="67720-218">Required</span></span> | <span data-ttu-id="67720-219">Tür</span><span class="sxs-lookup"><span data-stu-id="67720-219">Type</span></span> | <span data-ttu-id="67720-220">Açıklama</span><span class="sxs-lookup"><span data-stu-id="67720-220">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67720-221">arg1</span><span class="sxs-lookup"><span data-stu-id="67720-221">arg1</span></span> |<span data-ttu-id="67720-222">Evet</span><span class="sxs-lookup"><span data-stu-id="67720-222">Yes</span></span> |<span data-ttu-id="67720-223">int veya dize</span><span class="sxs-lookup"><span data-stu-id="67720-223">int or string</span></span> |<span data-ttu-id="67720-224">Merhaba karşılaştırma daha az hello için ilk değer.</span><span class="sxs-lookup"><span data-stu-id="67720-224">hello first value for hello less comparison.</span></span> |
| <span data-ttu-id="67720-225">arg2</span><span class="sxs-lookup"><span data-stu-id="67720-225">arg2</span></span> |<span data-ttu-id="67720-226">Evet</span><span class="sxs-lookup"><span data-stu-id="67720-226">Yes</span></span> |<span data-ttu-id="67720-227">int veya dize</span><span class="sxs-lookup"><span data-stu-id="67720-227">int or string</span></span> |<span data-ttu-id="67720-228">Merhaba hello daha az karşılaştırma için ikinci değer.</span><span class="sxs-lookup"><span data-stu-id="67720-228">hello second value for hello less comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67720-229">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="67720-229">Return value</span></span>

<span data-ttu-id="67720-230">Döndürür **True** hello ilk değer hello küçükse ikinci değer; Aksi halde, **False**.</span><span class="sxs-lookup"><span data-stu-id="67720-230">Returns **True** if hello first value is less than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="67720-231">Örnek</span><span class="sxs-lookup"><span data-stu-id="67720-231">Example</span></span>

<span data-ttu-id="67720-232">Hello örnek şablon hello bir değer hello diğer değerinden olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="67720-232">hello example template checks whether hello one value is less than hello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[less(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[less(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="67720-233">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="67720-233">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="67720-234">Ad</span><span class="sxs-lookup"><span data-stu-id="67720-234">Name</span></span> | <span data-ttu-id="67720-235">Tür</span><span class="sxs-lookup"><span data-stu-id="67720-235">Type</span></span> | <span data-ttu-id="67720-236">Değer</span><span class="sxs-lookup"><span data-stu-id="67720-236">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67720-237">checkInts</span><span class="sxs-lookup"><span data-stu-id="67720-237">checkInts</span></span> | <span data-ttu-id="67720-238">bool</span><span class="sxs-lookup"><span data-stu-id="67720-238">Bool</span></span> | <span data-ttu-id="67720-239">True</span><span class="sxs-lookup"><span data-stu-id="67720-239">True</span></span> |
| <span data-ttu-id="67720-240">checkStrings</span><span class="sxs-lookup"><span data-stu-id="67720-240">checkStrings</span></span> | <span data-ttu-id="67720-241">bool</span><span class="sxs-lookup"><span data-stu-id="67720-241">Bool</span></span> | <span data-ttu-id="67720-242">False</span><span class="sxs-lookup"><span data-stu-id="67720-242">False</span></span> |


## <a name="lessorequals"></a><span data-ttu-id="67720-243">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="67720-243">lessOrEquals</span></span>
`lessOrEquals(arg1, arg2)`

<span data-ttu-id="67720-244">Merhaba ilk değer küçük veya buna eşit olup olmadığını denetler toohello ikinci değer.</span><span class="sxs-lookup"><span data-stu-id="67720-244">Checks whether hello first value is less than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="67720-245">Parametreler</span><span class="sxs-lookup"><span data-stu-id="67720-245">Parameters</span></span>

| <span data-ttu-id="67720-246">Parametre</span><span class="sxs-lookup"><span data-stu-id="67720-246">Parameter</span></span> | <span data-ttu-id="67720-247">Gerekli</span><span class="sxs-lookup"><span data-stu-id="67720-247">Required</span></span> | <span data-ttu-id="67720-248">Tür</span><span class="sxs-lookup"><span data-stu-id="67720-248">Type</span></span> | <span data-ttu-id="67720-249">Açıklama</span><span class="sxs-lookup"><span data-stu-id="67720-249">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67720-250">arg1</span><span class="sxs-lookup"><span data-stu-id="67720-250">arg1</span></span> |<span data-ttu-id="67720-251">Evet</span><span class="sxs-lookup"><span data-stu-id="67720-251">Yes</span></span> |<span data-ttu-id="67720-252">int veya dize</span><span class="sxs-lookup"><span data-stu-id="67720-252">int or string</span></span> |<span data-ttu-id="67720-253">Merhaba ilk değeri hello küçük veya eşittir karşılaştırması.</span><span class="sxs-lookup"><span data-stu-id="67720-253">hello first value for hello less or equals comparison.</span></span> |
| <span data-ttu-id="67720-254">arg2</span><span class="sxs-lookup"><span data-stu-id="67720-254">arg2</span></span> |<span data-ttu-id="67720-255">Evet</span><span class="sxs-lookup"><span data-stu-id="67720-255">Yes</span></span> |<span data-ttu-id="67720-256">int veya dize</span><span class="sxs-lookup"><span data-stu-id="67720-256">int or string</span></span> |<span data-ttu-id="67720-257">İkinci değer hello için daha az hello veya karşılaştırma eşittir.</span><span class="sxs-lookup"><span data-stu-id="67720-257">hello second value for hello less or equals comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67720-258">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="67720-258">Return value</span></span>

<span data-ttu-id="67720-259">Döndürür **True** hello ilk değer küçük veya buna eşit ise toohello ikinci değeri; Aksi halde, **False**.</span><span class="sxs-lookup"><span data-stu-id="67720-259">Returns **True** if hello first value is less than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="67720-260">Örnek</span><span class="sxs-lookup"><span data-stu-id="67720-260">Example</span></span>

<span data-ttu-id="67720-261">Merhaba örnek şablon hello bir değer küçük veya buna eşit olup olmadığını denetler toohello diğer.</span><span class="sxs-lookup"><span data-stu-id="67720-261">hello example template checks whether hello one value is less than or equal toohello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="67720-262">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="67720-262">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="67720-263">Ad</span><span class="sxs-lookup"><span data-stu-id="67720-263">Name</span></span> | <span data-ttu-id="67720-264">Tür</span><span class="sxs-lookup"><span data-stu-id="67720-264">Type</span></span> | <span data-ttu-id="67720-265">Değer</span><span class="sxs-lookup"><span data-stu-id="67720-265">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67720-266">checkInts</span><span class="sxs-lookup"><span data-stu-id="67720-266">checkInts</span></span> | <span data-ttu-id="67720-267">bool</span><span class="sxs-lookup"><span data-stu-id="67720-267">Bool</span></span> | <span data-ttu-id="67720-268">True</span><span class="sxs-lookup"><span data-stu-id="67720-268">True</span></span> |
| <span data-ttu-id="67720-269">checkStrings</span><span class="sxs-lookup"><span data-stu-id="67720-269">checkStrings</span></span> | <span data-ttu-id="67720-270">bool</span><span class="sxs-lookup"><span data-stu-id="67720-270">Bool</span></span> | <span data-ttu-id="67720-271">False</span><span class="sxs-lookup"><span data-stu-id="67720-271">False</span></span> |



## <a name="next-steps"></a><span data-ttu-id="67720-272">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="67720-272">Next steps</span></span>
* <span data-ttu-id="67720-273">Bir Azure Resource Manager şablonu hello bölümlerde açıklaması için bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="67720-273">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="67720-274">birden fazla şablon toomerge bkz [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="67720-274">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="67720-275">tooiterate belirtilen sayıda kaynak türünü oluştururken bkz [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="67720-275">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="67720-276">toodeploy hello şablonu oluşturduğunuz toosee bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="67720-276">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

