---
title: "aaaAzure Resource Manager şablonu işlevleri - sayısal | Microsoft Docs"
description: "Bir Azure Resource Manager şablonu toowork içinde Hello işlevleri toouse numaralarıyla açıklar."
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
ms.date: 06/13/2017
ms.author: tomfitz
ms.openlocfilehash: 855d5b354d094b9815edc160e3d72efbfd36ba77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="386b5-103">Sayısal işlevler için Azure Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="386b5-103">Numeric functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="386b5-104">Resource Manager hello şu tamsayıları ile çalışmak için işlevleri sunar:</span><span class="sxs-lookup"><span data-stu-id="386b5-104">Resource Manager provides hello following functions for working with integers:</span></span>

* [<span data-ttu-id="386b5-105">ekleme</span><span class="sxs-lookup"><span data-stu-id="386b5-105">add</span></span>](#add)
* [<span data-ttu-id="386b5-106">Copyındex</span><span class="sxs-lookup"><span data-stu-id="386b5-106">copyIndex</span></span>](#copyindex)
* [<span data-ttu-id="386b5-107">div</span><span class="sxs-lookup"><span data-stu-id="386b5-107">div</span></span>](#div)
* [<span data-ttu-id="386b5-108">kayan nokta</span><span class="sxs-lookup"><span data-stu-id="386b5-108">float</span></span>](#float)
* [<span data-ttu-id="386b5-109">int</span><span class="sxs-lookup"><span data-stu-id="386b5-109">int</span></span>](#int)
* [<span data-ttu-id="386b5-110">Min</span><span class="sxs-lookup"><span data-stu-id="386b5-110">min</span></span>](#min)
* [<span data-ttu-id="386b5-111">max</span><span class="sxs-lookup"><span data-stu-id="386b5-111">max</span></span>](#max)
* [<span data-ttu-id="386b5-112">mod</span><span class="sxs-lookup"><span data-stu-id="386b5-112">mod</span></span>](#mod)
* [<span data-ttu-id="386b5-113">mul</span><span class="sxs-lookup"><span data-stu-id="386b5-113">mul</span></span>](#mul)
* [<span data-ttu-id="386b5-114">Sub</span><span class="sxs-lookup"><span data-stu-id="386b5-114">sub</span></span>](#sub)

<a id="add" />

## <a name="add"></a><span data-ttu-id="386b5-115">Ekleme</span><span class="sxs-lookup"><span data-stu-id="386b5-115">add</span></span>
`add(operand1, operand2)`

<span data-ttu-id="386b5-116">Merhaba iki sağlanan tamsayı toplamını döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="386b5-116">Returns hello sum of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="386b5-117">Parametreler</span><span class="sxs-lookup"><span data-stu-id="386b5-117">Parameters</span></span>

| <span data-ttu-id="386b5-118">Parametre</span><span class="sxs-lookup"><span data-stu-id="386b5-118">Parameter</span></span> | <span data-ttu-id="386b5-119">Gerekli</span><span class="sxs-lookup"><span data-stu-id="386b5-119">Required</span></span> | <span data-ttu-id="386b5-120">Tür</span><span class="sxs-lookup"><span data-stu-id="386b5-120">Type</span></span> | <span data-ttu-id="386b5-121">Açıklama</span><span class="sxs-lookup"><span data-stu-id="386b5-121">Description</span></span> |
|:--- |:--- |:--- |:--- | 
|<span data-ttu-id="386b5-122">operand1</span><span class="sxs-lookup"><span data-stu-id="386b5-122">operand1</span></span> |<span data-ttu-id="386b5-123">Evet</span><span class="sxs-lookup"><span data-stu-id="386b5-123">Yes</span></span> |<span data-ttu-id="386b5-124">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-124">int</span></span> |<span data-ttu-id="386b5-125">İlk sayı tooadd.</span><span class="sxs-lookup"><span data-stu-id="386b5-125">First number tooadd.</span></span> |
|<span data-ttu-id="386b5-126">operand2</span><span class="sxs-lookup"><span data-stu-id="386b5-126">operand2</span></span> |<span data-ttu-id="386b5-127">Evet</span><span class="sxs-lookup"><span data-stu-id="386b5-127">Yes</span></span> |<span data-ttu-id="386b5-128">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-128">int</span></span> |<span data-ttu-id="386b5-129">İkinci sayı tooadd.</span><span class="sxs-lookup"><span data-stu-id="386b5-129">Second number tooadd.</span></span> |

### <a name="return-value"></a><span data-ttu-id="386b5-130">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="386b5-130">Return value</span></span>

<span data-ttu-id="386b5-131">Merhaba parametreleri hello toplamını içeren bir tamsayı.</span><span class="sxs-lookup"><span data-stu-id="386b5-131">An integer that contains hello sum of hello parameters.</span></span>

### <a name="example"></a><span data-ttu-id="386b5-132">Örnek</span><span class="sxs-lookup"><span data-stu-id="386b5-132">Example</span></span>

<span data-ttu-id="386b5-133">Aşağıdaki örnek hello iki parametre ekler.</span><span class="sxs-lookup"><span data-stu-id="386b5-133">hello following example adds two parameters.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer tooadd"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer tooadd"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "addResult": {
            "type": "int",
            "value": "[add(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="386b5-134">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="386b5-134">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="386b5-135">Ad</span><span class="sxs-lookup"><span data-stu-id="386b5-135">Name</span></span> | <span data-ttu-id="386b5-136">Tür</span><span class="sxs-lookup"><span data-stu-id="386b5-136">Type</span></span> | <span data-ttu-id="386b5-137">Değer</span><span class="sxs-lookup"><span data-stu-id="386b5-137">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="386b5-138">addResult</span><span class="sxs-lookup"><span data-stu-id="386b5-138">addResult</span></span> | <span data-ttu-id="386b5-139">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-139">Int</span></span> | <span data-ttu-id="386b5-140">8</span><span class="sxs-lookup"><span data-stu-id="386b5-140">8</span></span> |

<a id="copyindex" />

## <a name="copyindex"></a><span data-ttu-id="386b5-141">Copyındex</span><span class="sxs-lookup"><span data-stu-id="386b5-141">copyIndex</span></span>
`copyIndex(loopName, offset)`

<span data-ttu-id="386b5-142">Bir yineleme döngüsü dizinini döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="386b5-142">Returns hello index of an iteration loop.</span></span> 

### <a name="parameters"></a><span data-ttu-id="386b5-143">Parametreler</span><span class="sxs-lookup"><span data-stu-id="386b5-143">Parameters</span></span>

| <span data-ttu-id="386b5-144">Parametre</span><span class="sxs-lookup"><span data-stu-id="386b5-144">Parameter</span></span> | <span data-ttu-id="386b5-145">Gerekli</span><span class="sxs-lookup"><span data-stu-id="386b5-145">Required</span></span> | <span data-ttu-id="386b5-146">Tür</span><span class="sxs-lookup"><span data-stu-id="386b5-146">Type</span></span> | <span data-ttu-id="386b5-147">Açıklama</span><span class="sxs-lookup"><span data-stu-id="386b5-147">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="386b5-148">loopName</span><span class="sxs-lookup"><span data-stu-id="386b5-148">loopName</span></span> | <span data-ttu-id="386b5-149">Hayır</span><span class="sxs-lookup"><span data-stu-id="386b5-149">No</span></span> | <span data-ttu-id="386b5-150">Dize</span><span class="sxs-lookup"><span data-stu-id="386b5-150">string</span></span> | <span data-ttu-id="386b5-151">Merhaba yineleme alma hello adı hello döngü.</span><span class="sxs-lookup"><span data-stu-id="386b5-151">hello name of hello loop for getting hello iteration.</span></span> |
| <span data-ttu-id="386b5-152">uzaklık</span><span class="sxs-lookup"><span data-stu-id="386b5-152">offset</span></span> |<span data-ttu-id="386b5-153">Hayır</span><span class="sxs-lookup"><span data-stu-id="386b5-153">No</span></span> |<span data-ttu-id="386b5-154">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-154">int</span></span> |<span data-ttu-id="386b5-155">Merhaba sayı tooadd toohello sıfır tabanlı yineleme değeri.</span><span class="sxs-lookup"><span data-stu-id="386b5-155">hello number tooadd toohello zero-based iteration value.</span></span> |

### <a name="remarks"></a><span data-ttu-id="386b5-156">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="386b5-156">Remarks</span></span>

<span data-ttu-id="386b5-157">Bu işlev her zaman ile kullanılan bir **kopyalama** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="386b5-157">This function is always used with a **copy** object.</span></span> <span data-ttu-id="386b5-158">İçin hiçbir değer sağlanmazsa **uzaklık**, hello geçerli yineleme değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="386b5-158">If no value is provided for **offset**, hello current iteration value is returned.</span></span> <span data-ttu-id="386b5-159">Merhaba yineleme değeri sıfırdan başlatır.</span><span class="sxs-lookup"><span data-stu-id="386b5-159">hello iteration value starts at zero.</span></span>

<span data-ttu-id="386b5-160">Merhaba **loopName** özelliği sağlar toospecify Copyındex tooa kaynak yineleme ya da özellik yineleme başvuran olup olmadığını.</span><span class="sxs-lookup"><span data-stu-id="386b5-160">hello **loopName** property enables you toospecify whether copyIndex is referring tooa resource iteration or property iteration.</span></span> <span data-ttu-id="386b5-161">İçin hiçbir değer sağlanmazsa **loopName**, hello geçerli kaynak türü yineleme kullanılır.</span><span class="sxs-lookup"><span data-stu-id="386b5-161">If no value is provided for **loopName**, hello current resource type iteration is used.</span></span> <span data-ttu-id="386b5-162">İçin bir değer girin **loopName** bir özellik dolaşırken.</span><span class="sxs-lookup"><span data-stu-id="386b5-162">Provide a value for **loopName** when iterating on a property.</span></span> 
 
<span data-ttu-id="386b5-163">Nasıl kullanabileceğinize tam bir açıklaması için **Copyındex**, bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="386b5-163">For a complete description of how you use **copyIndex**, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

### <a name="example"></a><span data-ttu-id="386b5-164">Örnek</span><span class="sxs-lookup"><span data-stu-id="386b5-164">Example</span></span>

<span data-ttu-id="386b5-165">Merhaba aşağıdaki örnek hello adına dahil bir kopya döngü ve hello dizin değeri gösterir.</span><span class="sxs-lookup"><span data-stu-id="386b5-165">hello following example shows a copy loop and hello index value included in hello name.</span></span> 

```json
"resources": [ 
  { 
    "name": "[concat('examplecopy-', copyIndex())]", 
    "type": "Microsoft.Web/sites", 
    "copy": { 
      "name": "websitescopy", 
      "count": "[parameters('count')]" 
    }, 
    ...
  }
]
```

### <a name="return-value"></a><span data-ttu-id="386b5-166">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="386b5-166">Return value</span></span>

<span data-ttu-id="386b5-167">Merhaba geçerli dizin hello yinelemenin temsil eden bir tamsayı.</span><span class="sxs-lookup"><span data-stu-id="386b5-167">An integer representing hello current index of hello iteration.</span></span>

<a id="div" />

## <a name="div"></a><span data-ttu-id="386b5-168">div</span><span class="sxs-lookup"><span data-stu-id="386b5-168">div</span></span>
`div(operand1, operand2)`

<span data-ttu-id="386b5-169">Tamsayı bölme hello iki sağlanan tamsayıların döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="386b5-169">Returns hello integer division of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="386b5-170">Parametreler</span><span class="sxs-lookup"><span data-stu-id="386b5-170">Parameters</span></span>

| <span data-ttu-id="386b5-171">Parametre</span><span class="sxs-lookup"><span data-stu-id="386b5-171">Parameter</span></span> | <span data-ttu-id="386b5-172">Gerekli</span><span class="sxs-lookup"><span data-stu-id="386b5-172">Required</span></span> | <span data-ttu-id="386b5-173">Tür</span><span class="sxs-lookup"><span data-stu-id="386b5-173">Type</span></span> | <span data-ttu-id="386b5-174">Açıklama</span><span class="sxs-lookup"><span data-stu-id="386b5-174">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="386b5-175">operand1</span><span class="sxs-lookup"><span data-stu-id="386b5-175">operand1</span></span> |<span data-ttu-id="386b5-176">Evet</span><span class="sxs-lookup"><span data-stu-id="386b5-176">Yes</span></span> |<span data-ttu-id="386b5-177">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-177">int</span></span> |<span data-ttu-id="386b5-178">ayrılmış hello numarası.</span><span class="sxs-lookup"><span data-stu-id="386b5-178">hello number being divided.</span></span> |
| <span data-ttu-id="386b5-179">operand2</span><span class="sxs-lookup"><span data-stu-id="386b5-179">operand2</span></span> |<span data-ttu-id="386b5-180">Evet</span><span class="sxs-lookup"><span data-stu-id="386b5-180">Yes</span></span> |<span data-ttu-id="386b5-181">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-181">int</span></span> |<span data-ttu-id="386b5-182">kullanılan toodivide hello numarası.</span><span class="sxs-lookup"><span data-stu-id="386b5-182">hello number that is used toodivide.</span></span> <span data-ttu-id="386b5-183">0 olamaz.</span><span class="sxs-lookup"><span data-stu-id="386b5-183">Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="386b5-184">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="386b5-184">Return value</span></span>

<span data-ttu-id="386b5-185">Bir tamsayı temsil eden hello bölme.</span><span class="sxs-lookup"><span data-stu-id="386b5-185">An integer representing hello division.</span></span>

### <a name="example"></a><span data-ttu-id="386b5-186">Örnek</span><span class="sxs-lookup"><span data-stu-id="386b5-186">Example</span></span>

<span data-ttu-id="386b5-187">Aşağıdaki örnek hello başka bir parametre olarak bir parametre böler.</span><span class="sxs-lookup"><span data-stu-id="386b5-187">hello following example divides one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 8,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used toodivide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "divResult": {
            "type": "int",
            "value": "[div(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="386b5-188">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="386b5-188">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="386b5-189">Ad</span><span class="sxs-lookup"><span data-stu-id="386b5-189">Name</span></span> | <span data-ttu-id="386b5-190">Tür</span><span class="sxs-lookup"><span data-stu-id="386b5-190">Type</span></span> | <span data-ttu-id="386b5-191">Değer</span><span class="sxs-lookup"><span data-stu-id="386b5-191">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="386b5-192">divResult</span><span class="sxs-lookup"><span data-stu-id="386b5-192">divResult</span></span> | <span data-ttu-id="386b5-193">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-193">Int</span></span> | <span data-ttu-id="386b5-194">2</span><span class="sxs-lookup"><span data-stu-id="386b5-194">2</span></span> |

<a id="float" />

## <a name="float"></a><span data-ttu-id="386b5-195">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="386b5-195">float</span></span>
`float(arg1)`

<span data-ttu-id="386b5-196">Kayan noktalı sayıyı hello değeri tooa dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="386b5-196">Converts hello value tooa floating point number.</span></span> <span data-ttu-id="386b5-197">Özel Parametreler tooan uygulama, bir mantıksal uygulama gibi geçirilirken yalnızca bu işlevi kullanın.</span><span class="sxs-lookup"><span data-stu-id="386b5-197">You only use this function when passing custom parameters tooan application, such as a Logic App.</span></span>

### <a name="parameters"></a><span data-ttu-id="386b5-198">Parametreler</span><span class="sxs-lookup"><span data-stu-id="386b5-198">Parameters</span></span>

| <span data-ttu-id="386b5-199">Parametre</span><span class="sxs-lookup"><span data-stu-id="386b5-199">Parameter</span></span> | <span data-ttu-id="386b5-200">Gerekli</span><span class="sxs-lookup"><span data-stu-id="386b5-200">Required</span></span> | <span data-ttu-id="386b5-201">Tür</span><span class="sxs-lookup"><span data-stu-id="386b5-201">Type</span></span> | <span data-ttu-id="386b5-202">Açıklama</span><span class="sxs-lookup"><span data-stu-id="386b5-202">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="386b5-203">arg1</span><span class="sxs-lookup"><span data-stu-id="386b5-203">arg1</span></span> |<span data-ttu-id="386b5-204">Evet</span><span class="sxs-lookup"><span data-stu-id="386b5-204">Yes</span></span> |<span data-ttu-id="386b5-205">dize veya int</span><span class="sxs-lookup"><span data-stu-id="386b5-205">string or int</span></span> |<span data-ttu-id="386b5-206">kayan noktalı sayı değeri tooconvert tooa hello.</span><span class="sxs-lookup"><span data-stu-id="386b5-206">hello value tooconvert tooa floating point number.</span></span> |

### <a name="return-value"></a><span data-ttu-id="386b5-207">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="386b5-207">Return value</span></span>
<span data-ttu-id="386b5-208">Kayan nokta sayısı.</span><span class="sxs-lookup"><span data-stu-id="386b5-208">A floating point number.</span></span>

### <a name="example"></a><span data-ttu-id="386b5-209">Örnek</span><span class="sxs-lookup"><span data-stu-id="386b5-209">Example</span></span>

<span data-ttu-id="386b5-210">Aşağıdaki örnek hello nasıl toouse float toopass parametreleri tooa mantıksal uygulama gösterir:</span><span class="sxs-lookup"><span data-stu-id="386b5-210">hello following example shows how toouse float toopass parameters tooa Logic App:</span></span>

```json
{
    "type": "Microsoft.Logic/workflows",
    "properties": {
        ...
        "parameters": {
        "custom1": {
            "value": "[float('3.0')]"
        },
        "custom2": {
            "value": "[float(3)]"
        },
```

<a id="int" />

## <a name="int"></a><span data-ttu-id="386b5-211">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-211">int</span></span>
`int(valueToConvert)`

<span data-ttu-id="386b5-212">Merhaba belirtilen değere tooan tamsayı dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="386b5-212">Converts hello specified value tooan integer.</span></span>

### <a name="parameters"></a><span data-ttu-id="386b5-213">Parametreler</span><span class="sxs-lookup"><span data-stu-id="386b5-213">Parameters</span></span>

| <span data-ttu-id="386b5-214">Parametre</span><span class="sxs-lookup"><span data-stu-id="386b5-214">Parameter</span></span> | <span data-ttu-id="386b5-215">Gerekli</span><span class="sxs-lookup"><span data-stu-id="386b5-215">Required</span></span> | <span data-ttu-id="386b5-216">Tür</span><span class="sxs-lookup"><span data-stu-id="386b5-216">Type</span></span> | <span data-ttu-id="386b5-217">Açıklama</span><span class="sxs-lookup"><span data-stu-id="386b5-217">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="386b5-218">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="386b5-218">valueToConvert</span></span> |<span data-ttu-id="386b5-219">Evet</span><span class="sxs-lookup"><span data-stu-id="386b5-219">Yes</span></span> |<span data-ttu-id="386b5-220">dize veya int</span><span class="sxs-lookup"><span data-stu-id="386b5-220">string or int</span></span> |<span data-ttu-id="386b5-221">Merhaba değeri tooconvert tooan tamsayı.</span><span class="sxs-lookup"><span data-stu-id="386b5-221">hello value tooconvert tooan integer.</span></span> |

### <a name="return-value"></a><span data-ttu-id="386b5-222">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="386b5-222">Return value</span></span>

<span data-ttu-id="386b5-223">Merhaba, bir tamsayı değeri dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="386b5-223">An integer of hello converted value.</span></span>

### <a name="example"></a><span data-ttu-id="386b5-224">Örnek</span><span class="sxs-lookup"><span data-stu-id="386b5-224">Example</span></span>

<span data-ttu-id="386b5-225">Merhaba aşağıdaki örnek hello kullanıcı tarafından sağlanan parametre değeri toointeger dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="386b5-225">hello following example converts hello user-provided parameter value toointeger.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToConvert": { 
            "type": "string",
            "defaultValue": "4"
        }
    },
    "resources": [
    ],
    "outputs": {
        "intResult": {
            "type": "int",
            "value": "[int(parameters('stringToConvert'))]"
        }
    }
}
```

<span data-ttu-id="386b5-226">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="386b5-226">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="386b5-227">Ad</span><span class="sxs-lookup"><span data-stu-id="386b5-227">Name</span></span> | <span data-ttu-id="386b5-228">Tür</span><span class="sxs-lookup"><span data-stu-id="386b5-228">Type</span></span> | <span data-ttu-id="386b5-229">Değer</span><span class="sxs-lookup"><span data-stu-id="386b5-229">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="386b5-230">intResult</span><span class="sxs-lookup"><span data-stu-id="386b5-230">intResult</span></span> | <span data-ttu-id="386b5-231">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-231">Int</span></span> | <span data-ttu-id="386b5-232">4</span><span class="sxs-lookup"><span data-stu-id="386b5-232">4</span></span> |


<a id="min" />

## <a name="min"></a><span data-ttu-id="386b5-233">dk</span><span class="sxs-lookup"><span data-stu-id="386b5-233">min</span></span>
`min (arg1)`

<span data-ttu-id="386b5-234">Döndürür dizisi veya virgülle ayrılmış tamsayı listesi en düşük değerden hello.</span><span class="sxs-lookup"><span data-stu-id="386b5-234">Returns hello minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="386b5-235">Parametreler</span><span class="sxs-lookup"><span data-stu-id="386b5-235">Parameters</span></span>

| <span data-ttu-id="386b5-236">Parametre</span><span class="sxs-lookup"><span data-stu-id="386b5-236">Parameter</span></span> | <span data-ttu-id="386b5-237">Gerekli</span><span class="sxs-lookup"><span data-stu-id="386b5-237">Required</span></span> | <span data-ttu-id="386b5-238">Tür</span><span class="sxs-lookup"><span data-stu-id="386b5-238">Type</span></span> | <span data-ttu-id="386b5-239">Açıklama</span><span class="sxs-lookup"><span data-stu-id="386b5-239">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="386b5-240">arg1</span><span class="sxs-lookup"><span data-stu-id="386b5-240">arg1</span></span> |<span data-ttu-id="386b5-241">Evet</span><span class="sxs-lookup"><span data-stu-id="386b5-241">Yes</span></span> |<span data-ttu-id="386b5-242">dizi tamsayı veya virgülle ayrılmış tamsayı listesi</span><span class="sxs-lookup"><span data-stu-id="386b5-242">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="386b5-243">Merhaba koleksiyonu tooget hello en küçük değer.</span><span class="sxs-lookup"><span data-stu-id="386b5-243">hello collection tooget hello minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="386b5-244">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="386b5-244">Return value</span></span>

<span data-ttu-id="386b5-245">En düşük değer hello koleksiyonundan temsil eden bir tamsayı.</span><span class="sxs-lookup"><span data-stu-id="386b5-245">An integer representing minimum value from hello collection.</span></span>

### <a name="example"></a><span data-ttu-id="386b5-246">Örnek</span><span class="sxs-lookup"><span data-stu-id="386b5-246">Example</span></span>

<span data-ttu-id="386b5-247">örnekte gösterildiği nasıl aşağıdaki hello toouse en az bir dizi ve tamsayı listesi:</span><span class="sxs-lookup"><span data-stu-id="386b5-247">hello following example shows how toouse min with an array and a list of integers:</span></span>

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

<span data-ttu-id="386b5-248">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="386b5-248">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="386b5-249">Ad</span><span class="sxs-lookup"><span data-stu-id="386b5-249">Name</span></span> | <span data-ttu-id="386b5-250">Tür</span><span class="sxs-lookup"><span data-stu-id="386b5-250">Type</span></span> | <span data-ttu-id="386b5-251">Değer</span><span class="sxs-lookup"><span data-stu-id="386b5-251">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="386b5-252">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="386b5-252">arrayOutput</span></span> | <span data-ttu-id="386b5-253">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-253">Int</span></span> | <span data-ttu-id="386b5-254">0</span><span class="sxs-lookup"><span data-stu-id="386b5-254">0</span></span> |
| <span data-ttu-id="386b5-255">intOutput</span><span class="sxs-lookup"><span data-stu-id="386b5-255">intOutput</span></span> | <span data-ttu-id="386b5-256">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-256">Int</span></span> | <span data-ttu-id="386b5-257">0</span><span class="sxs-lookup"><span data-stu-id="386b5-257">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="386b5-258">max</span><span class="sxs-lookup"><span data-stu-id="386b5-258">max</span></span>
`max (arg1)`

<span data-ttu-id="386b5-259">En büyük değer dizisi veya virgülle ayrılmış tamsayı listesi döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="386b5-259">Returns hello maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="386b5-260">Parametreler</span><span class="sxs-lookup"><span data-stu-id="386b5-260">Parameters</span></span>

| <span data-ttu-id="386b5-261">Parametre</span><span class="sxs-lookup"><span data-stu-id="386b5-261">Parameter</span></span> | <span data-ttu-id="386b5-262">Gerekli</span><span class="sxs-lookup"><span data-stu-id="386b5-262">Required</span></span> | <span data-ttu-id="386b5-263">Tür</span><span class="sxs-lookup"><span data-stu-id="386b5-263">Type</span></span> | <span data-ttu-id="386b5-264">Açıklama</span><span class="sxs-lookup"><span data-stu-id="386b5-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="386b5-265">arg1</span><span class="sxs-lookup"><span data-stu-id="386b5-265">arg1</span></span> |<span data-ttu-id="386b5-266">Evet</span><span class="sxs-lookup"><span data-stu-id="386b5-266">Yes</span></span> |<span data-ttu-id="386b5-267">dizi tamsayı veya virgülle ayrılmış tamsayı listesi</span><span class="sxs-lookup"><span data-stu-id="386b5-267">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="386b5-268">Merhaba koleksiyonu tooget hello en büyük değer.</span><span class="sxs-lookup"><span data-stu-id="386b5-268">hello collection tooget hello maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="386b5-269">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="386b5-269">Return value</span></span>

<span data-ttu-id="386b5-270">Merhaba en büyük değer hello koleksiyonundan temsil eden bir tamsayı.</span><span class="sxs-lookup"><span data-stu-id="386b5-270">An integer representing hello maximum value from hello collection.</span></span>

### <a name="example"></a><span data-ttu-id="386b5-271">Örnek</span><span class="sxs-lookup"><span data-stu-id="386b5-271">Example</span></span>

<span data-ttu-id="386b5-272">örnekte gösterildiği nasıl aşağıdaki hello toouse bir dizi ve tamsayı listesi ile en fazla:</span><span class="sxs-lookup"><span data-stu-id="386b5-272">hello following example shows how toouse max with an array and a list of integers:</span></span>

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

<span data-ttu-id="386b5-273">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="386b5-273">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="386b5-274">Ad</span><span class="sxs-lookup"><span data-stu-id="386b5-274">Name</span></span> | <span data-ttu-id="386b5-275">Tür</span><span class="sxs-lookup"><span data-stu-id="386b5-275">Type</span></span> | <span data-ttu-id="386b5-276">Değer</span><span class="sxs-lookup"><span data-stu-id="386b5-276">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="386b5-277">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="386b5-277">arrayOutput</span></span> | <span data-ttu-id="386b5-278">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-278">Int</span></span> | <span data-ttu-id="386b5-279">5</span><span class="sxs-lookup"><span data-stu-id="386b5-279">5</span></span> |
| <span data-ttu-id="386b5-280">intOutput</span><span class="sxs-lookup"><span data-stu-id="386b5-280">intOutput</span></span> | <span data-ttu-id="386b5-281">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-281">Int</span></span> | <span data-ttu-id="386b5-282">5</span><span class="sxs-lookup"><span data-stu-id="386b5-282">5</span></span> |

<a id="mod" />

## <a name="mod"></a><span data-ttu-id="386b5-283">mod</span><span class="sxs-lookup"><span data-stu-id="386b5-283">mod</span></span>
`mod(operand1, operand2)`

<span data-ttu-id="386b5-284">Merhaba iki sağlanan tamsayılar kullanılarak hello tamsayı bölme Hello kalanı döndürür.</span><span class="sxs-lookup"><span data-stu-id="386b5-284">Returns hello remainder of hello integer division using hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="386b5-285">Parametreler</span><span class="sxs-lookup"><span data-stu-id="386b5-285">Parameters</span></span>

| <span data-ttu-id="386b5-286">Parametre</span><span class="sxs-lookup"><span data-stu-id="386b5-286">Parameter</span></span> | <span data-ttu-id="386b5-287">Gerekli</span><span class="sxs-lookup"><span data-stu-id="386b5-287">Required</span></span> | <span data-ttu-id="386b5-288">Tür</span><span class="sxs-lookup"><span data-stu-id="386b5-288">Type</span></span> | <span data-ttu-id="386b5-289">Açıklama</span><span class="sxs-lookup"><span data-stu-id="386b5-289">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="386b5-290">operand1</span><span class="sxs-lookup"><span data-stu-id="386b5-290">operand1</span></span> |<span data-ttu-id="386b5-291">Evet</span><span class="sxs-lookup"><span data-stu-id="386b5-291">Yes</span></span> |<span data-ttu-id="386b5-292">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-292">int</span></span> |<span data-ttu-id="386b5-293">ayrılmış hello numarası.</span><span class="sxs-lookup"><span data-stu-id="386b5-293">hello number being divided.</span></span> |
| <span data-ttu-id="386b5-294">operand2</span><span class="sxs-lookup"><span data-stu-id="386b5-294">operand2</span></span> |<span data-ttu-id="386b5-295">Evet</span><span class="sxs-lookup"><span data-stu-id="386b5-295">Yes</span></span> |<span data-ttu-id="386b5-296">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-296">int</span></span> |<span data-ttu-id="386b5-297">kullanılan toodivide hello numarası 0 olamaz.</span><span class="sxs-lookup"><span data-stu-id="386b5-297">hello number that is used toodivide, Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="386b5-298">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="386b5-298">Return value</span></span>
<span data-ttu-id="386b5-299">Bir tamsayı temsil eden hello kalan.</span><span class="sxs-lookup"><span data-stu-id="386b5-299">An integer representing hello remainder.</span></span>

### <a name="example"></a><span data-ttu-id="386b5-300">Örnek</span><span class="sxs-lookup"><span data-stu-id="386b5-300">Example</span></span>

<span data-ttu-id="386b5-301">Merhaba aşağıdaki örnekte başka bir parametre olarak bir parametre ayırma hello kalanı döndürür.</span><span class="sxs-lookup"><span data-stu-id="386b5-301">hello following example returns hello remainder of dividing one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used toodivide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "modResult": {
            "type": "int",
            "value": "[mod(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="386b5-302">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="386b5-302">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="386b5-303">Ad</span><span class="sxs-lookup"><span data-stu-id="386b5-303">Name</span></span> | <span data-ttu-id="386b5-304">Tür</span><span class="sxs-lookup"><span data-stu-id="386b5-304">Type</span></span> | <span data-ttu-id="386b5-305">Değer</span><span class="sxs-lookup"><span data-stu-id="386b5-305">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="386b5-306">modResult</span><span class="sxs-lookup"><span data-stu-id="386b5-306">modResult</span></span> | <span data-ttu-id="386b5-307">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-307">Int</span></span> | <span data-ttu-id="386b5-308">1</span><span class="sxs-lookup"><span data-stu-id="386b5-308">1</span></span> |

<a id="mul" />

## <a name="mul"></a><span data-ttu-id="386b5-309">mul</span><span class="sxs-lookup"><span data-stu-id="386b5-309">mul</span></span>
`mul(operand1, operand2)`

<span data-ttu-id="386b5-310">Çarpma hello iki sağlanan tamsayıların döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="386b5-310">Returns hello multiplication of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="386b5-311">Parametreler</span><span class="sxs-lookup"><span data-stu-id="386b5-311">Parameters</span></span>

| <span data-ttu-id="386b5-312">Parametre</span><span class="sxs-lookup"><span data-stu-id="386b5-312">Parameter</span></span> | <span data-ttu-id="386b5-313">Gerekli</span><span class="sxs-lookup"><span data-stu-id="386b5-313">Required</span></span> | <span data-ttu-id="386b5-314">Tür</span><span class="sxs-lookup"><span data-stu-id="386b5-314">Type</span></span> | <span data-ttu-id="386b5-315">Açıklama</span><span class="sxs-lookup"><span data-stu-id="386b5-315">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="386b5-316">operand1</span><span class="sxs-lookup"><span data-stu-id="386b5-316">operand1</span></span> |<span data-ttu-id="386b5-317">Evet</span><span class="sxs-lookup"><span data-stu-id="386b5-317">Yes</span></span> |<span data-ttu-id="386b5-318">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-318">int</span></span> |<span data-ttu-id="386b5-319">İlk sayı toomultiply.</span><span class="sxs-lookup"><span data-stu-id="386b5-319">First number toomultiply.</span></span> |
| <span data-ttu-id="386b5-320">operand2</span><span class="sxs-lookup"><span data-stu-id="386b5-320">operand2</span></span> |<span data-ttu-id="386b5-321">Evet</span><span class="sxs-lookup"><span data-stu-id="386b5-321">Yes</span></span> |<span data-ttu-id="386b5-322">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-322">int</span></span> |<span data-ttu-id="386b5-323">İkinci sayı toomultiply.</span><span class="sxs-lookup"><span data-stu-id="386b5-323">Second number toomultiply.</span></span> |

### <a name="return-value"></a><span data-ttu-id="386b5-324">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="386b5-324">Return value</span></span>

<span data-ttu-id="386b5-325">Bir tamsayı temsil eden hello çarpma.</span><span class="sxs-lookup"><span data-stu-id="386b5-325">An integer representing hello multiplication.</span></span>

### <a name="example"></a><span data-ttu-id="386b5-326">Örnek</span><span class="sxs-lookup"><span data-stu-id="386b5-326">Example</span></span>

<span data-ttu-id="386b5-327">Aşağıdaki örnek hello başka bir parametre olarak bir parametre çarpar.</span><span class="sxs-lookup"><span data-stu-id="386b5-327">hello following example multiplies one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer toomultiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer toomultiply"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "mulResult": {
            "type": "int",
            "value": "[mul(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="386b5-328">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="386b5-328">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="386b5-329">Ad</span><span class="sxs-lookup"><span data-stu-id="386b5-329">Name</span></span> | <span data-ttu-id="386b5-330">Tür</span><span class="sxs-lookup"><span data-stu-id="386b5-330">Type</span></span> | <span data-ttu-id="386b5-331">Değer</span><span class="sxs-lookup"><span data-stu-id="386b5-331">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="386b5-332">mulResult</span><span class="sxs-lookup"><span data-stu-id="386b5-332">mulResult</span></span> | <span data-ttu-id="386b5-333">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-333">Int</span></span> | <span data-ttu-id="386b5-334">15</span><span class="sxs-lookup"><span data-stu-id="386b5-334">15</span></span> |

<a id="sub" />

## <a name="sub"></a><span data-ttu-id="386b5-335">Sub</span><span class="sxs-lookup"><span data-stu-id="386b5-335">sub</span></span>
`sub(operand1, operand2)`

<span data-ttu-id="386b5-336">Döndürür hello iki sağlanan tamsayıların çıkarma hello.</span><span class="sxs-lookup"><span data-stu-id="386b5-336">Returns hello subtraction of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="386b5-337">Parametreler</span><span class="sxs-lookup"><span data-stu-id="386b5-337">Parameters</span></span>

| <span data-ttu-id="386b5-338">Parametre</span><span class="sxs-lookup"><span data-stu-id="386b5-338">Parameter</span></span> | <span data-ttu-id="386b5-339">Gerekli</span><span class="sxs-lookup"><span data-stu-id="386b5-339">Required</span></span> | <span data-ttu-id="386b5-340">Tür</span><span class="sxs-lookup"><span data-stu-id="386b5-340">Type</span></span> | <span data-ttu-id="386b5-341">Açıklama</span><span class="sxs-lookup"><span data-stu-id="386b5-341">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="386b5-342">operand1</span><span class="sxs-lookup"><span data-stu-id="386b5-342">operand1</span></span> |<span data-ttu-id="386b5-343">Evet</span><span class="sxs-lookup"><span data-stu-id="386b5-343">Yes</span></span> |<span data-ttu-id="386b5-344">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-344">int</span></span> |<span data-ttu-id="386b5-345">gelen çıkarılır hello numarası.</span><span class="sxs-lookup"><span data-stu-id="386b5-345">hello number that is subtracted from.</span></span> |
| <span data-ttu-id="386b5-346">operand2</span><span class="sxs-lookup"><span data-stu-id="386b5-346">operand2</span></span> |<span data-ttu-id="386b5-347">Evet</span><span class="sxs-lookup"><span data-stu-id="386b5-347">Yes</span></span> |<span data-ttu-id="386b5-348">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-348">int</span></span> |<span data-ttu-id="386b5-349">çıkarılır hello numarası.</span><span class="sxs-lookup"><span data-stu-id="386b5-349">hello number that is subtracted.</span></span> |

### <a name="return-value"></a><span data-ttu-id="386b5-350">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="386b5-350">Return value</span></span>
<span data-ttu-id="386b5-351">Bir tamsayı temsil eden hello çıkarma.</span><span class="sxs-lookup"><span data-stu-id="386b5-351">An integer representing hello subtraction.</span></span>

### <a name="example"></a><span data-ttu-id="386b5-352">Örnek</span><span class="sxs-lookup"><span data-stu-id="386b5-352">Example</span></span>

<span data-ttu-id="386b5-353">Aşağıdaki örnek hello başka bir parametre bir parametresinden çıkarır.</span><span class="sxs-lookup"><span data-stu-id="386b5-353">hello following example subtracts one parameter from another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer subtracted from"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer toosubtract"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "subResult": {
            "type": "int",
            "value": "[sub(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="386b5-354">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="386b5-354">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="386b5-355">Ad</span><span class="sxs-lookup"><span data-stu-id="386b5-355">Name</span></span> | <span data-ttu-id="386b5-356">Tür</span><span class="sxs-lookup"><span data-stu-id="386b5-356">Type</span></span> | <span data-ttu-id="386b5-357">Değer</span><span class="sxs-lookup"><span data-stu-id="386b5-357">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="386b5-358">subResult</span><span class="sxs-lookup"><span data-stu-id="386b5-358">subResult</span></span> | <span data-ttu-id="386b5-359">Int</span><span class="sxs-lookup"><span data-stu-id="386b5-359">Int</span></span> | <span data-ttu-id="386b5-360">4</span><span class="sxs-lookup"><span data-stu-id="386b5-360">4</span></span> |

## <a name="next-steps"></a><span data-ttu-id="386b5-361">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="386b5-361">Next steps</span></span>
* <span data-ttu-id="386b5-362">Bir Azure Resource Manager şablonu hello bölümlerde açıklaması için bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="386b5-362">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="386b5-363">birden fazla şablon toomerge bkz [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="386b5-363">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="386b5-364">tooiterate belirtilen sayıda kaynak türünü oluştururken bkz [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="386b5-364">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="386b5-365">toodeploy hello şablonu oluşturduğunuz toosee bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="386b5-365">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

