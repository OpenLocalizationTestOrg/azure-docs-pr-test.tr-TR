---
title: "aaaAzure Resource Manager şablonu işlevleri - dağıtım | Microsoft Docs"
description: "Bir Azure Resource Manager şablonu tooretrieve dağıtım bilgileri Hello işlevleri toouse açıklar."
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
ms.openlocfilehash: 458c3f740504fdd6799ed24cc386219726737636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="c8005-103">Azure Resource Manager şablonları için dağıtım işlevleri</span><span class="sxs-lookup"><span data-stu-id="c8005-103">Deployment functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="c8005-104">Resource Manager hello aşağıdaki değerleri hello şablon bölümlerinden alma için İşlevler ve ilgili toohello dağıtım değerleri sunar:</span><span class="sxs-lookup"><span data-stu-id="c8005-104">Resource Manager provides hello following functions for getting values from sections of hello template and values related toohello deployment:</span></span>

* [<span data-ttu-id="c8005-105">Dağıtım</span><span class="sxs-lookup"><span data-stu-id="c8005-105">deployment</span></span>](#deployment)
* [<span data-ttu-id="c8005-106">parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8005-106">parameters</span></span>](#parameters)
* [<span data-ttu-id="c8005-107">değişkenleri</span><span class="sxs-lookup"><span data-stu-id="c8005-107">variables</span></span>](#variables)

<span data-ttu-id="c8005-108">Kaynak, kaynak grupları ya da abonelikler, tooget değerleri görmek [kaynak işlevlerini](resource-group-template-functions-resource.md).</span><span class="sxs-lookup"><span data-stu-id="c8005-108">tooget values from resources, resource groups, or subscriptions, see [Resource functions](resource-group-template-functions-resource.md).</span></span>

<a id="deployment" />

## <a name="deployment"></a><span data-ttu-id="c8005-109">dağıtım</span><span class="sxs-lookup"><span data-stu-id="c8005-109">deployment</span></span>
`deployment()`

<span data-ttu-id="c8005-110">Merhaba geçerli dağıtım işlemiyle ilgili bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="c8005-110">Returns information about hello current deployment operation.</span></span>

### <a name="return-value"></a><span data-ttu-id="c8005-111">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="c8005-111">Return value</span></span>

<span data-ttu-id="c8005-112">Bu işlev, dağıtımı sırasında geçirilen hello nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="c8005-112">This function returns hello object that is passed during deployment.</span></span> <span data-ttu-id="c8005-113">Nesne döndürdü hello Hello özelliklerinde olup hello dağıtım nesnesi bir bağlantı veya bir satır içi nesnesi olarak geçirilen göre farklılık.</span><span class="sxs-lookup"><span data-stu-id="c8005-113">hello properties in hello returned object differ based on whether hello deployment object is passed as a link or as an in-line object.</span></span> <span data-ttu-id="c8005-114">Ne zaman hello dağıtım nesnesi geçirilir satır içi, gibi hello kullanırken **- TemplateFile** parametresi Azure PowerShell toopoint tooa yerel dosyasında hello nesne biçimini izleyen hello döndürdü:</span><span class="sxs-lookup"><span data-stu-id="c8005-114">When hello deployment object is passed in-line, such as when using hello **-TemplateFile** parameter in Azure PowerShell toopoint tooa local file, hello returned object has hello following format:</span></span>

```json
{
    "name": "",
    "properties": {
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [
            ],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

<span data-ttu-id="c8005-115">Ne zaman hello nesne geçirilir zaman kullanarak hello gibi bir bağlantı olarak **- TemplateUri** parametresi toopoint tooa uzaktan nesnesi, hello nesne biçimini izleyen hello döndürdü:</span><span class="sxs-lookup"><span data-stu-id="c8005-115">When hello object is passed as a link, such as when using hello **-TemplateUri** parameter toopoint tooa remote object, hello object is returned in hello following format:</span></span> 

```json
{
    "name": "",
    "properties": {
        "templateLink": {
            "uri": ""
        },
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

### <a name="remarks"></a><span data-ttu-id="c8005-116">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="c8005-116">Remarks</span></span>

<span data-ttu-id="c8005-117">Merhaba üst şablon URI'sini hello üzerinde temel deployment() toolink tooanother şablonu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8005-117">You can use deployment() toolink tooanother template based on hello URI of hello parent template.</span></span>

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a><span data-ttu-id="c8005-118">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8005-118">Example</span></span>

<span data-ttu-id="c8005-119">Merhaba aşağıdaki örnek hello dağıtım nesnesi döndürür:</span><span class="sxs-lookup"><span data-stu-id="c8005-119">hello following example returns hello deployment object:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[deployment()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="c8005-120">Merhaba önceki örnekte nesne aşağıdaki hello döndürür:</span><span class="sxs-lookup"><span data-stu-id="c8005-120">hello preceding example returns hello following object:</span></span>

```json
{
  "name": "deployment",
  "properties": {
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "resources": [],
      "outputs": {
        "subscriptionOutput": {
          "type": "Object",
          "value": "[deployment()]"
        }
      }
    },
    "parameters": {},
    "mode": "Incremental",
    "provisioningState": "Accepted"
  }
}
```

<a id="parameters" />

## <a name="parameters"></a><span data-ttu-id="c8005-121">parametreler</span><span class="sxs-lookup"><span data-stu-id="c8005-121">parameters</span></span>
`parameters(parameterName)`

<span data-ttu-id="c8005-122">Bir parametre değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="c8005-122">Returns a parameter value.</span></span> <span data-ttu-id="c8005-123">Merhaba belirtilen parametre adı hello Parametreler bölümünde hello şablonunun tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8005-123">hello specified parameter name must be defined in hello parameters section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="c8005-124">Parametreler</span><span class="sxs-lookup"><span data-stu-id="c8005-124">Parameters</span></span>

| <span data-ttu-id="c8005-125">Parametre</span><span class="sxs-lookup"><span data-stu-id="c8005-125">Parameter</span></span> | <span data-ttu-id="c8005-126">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c8005-126">Required</span></span> | <span data-ttu-id="c8005-127">Tür</span><span class="sxs-lookup"><span data-stu-id="c8005-127">Type</span></span> | <span data-ttu-id="c8005-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8005-128">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c8005-129">parameterName</span><span class="sxs-lookup"><span data-stu-id="c8005-129">parameterName</span></span> |<span data-ttu-id="c8005-130">Evet</span><span class="sxs-lookup"><span data-stu-id="c8005-130">Yes</span></span> |<span data-ttu-id="c8005-131">Dize</span><span class="sxs-lookup"><span data-stu-id="c8005-131">string</span></span> |<span data-ttu-id="c8005-132">Merhaba parametresi tooreturn Hello adı.</span><span class="sxs-lookup"><span data-stu-id="c8005-132">hello name of hello parameter tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c8005-133">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="c8005-133">Return value</span></span>

<span data-ttu-id="c8005-134">Merhaba başlangıç değeri parametresi belirtildi.</span><span class="sxs-lookup"><span data-stu-id="c8005-134">hello value of hello specified parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="c8005-135">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="c8005-135">Remarks</span></span>

<span data-ttu-id="c8005-136">Genellikle, parametreleri tooset kaynak değerlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c8005-136">Typically, you use parameters tooset resource values.</span></span> <span data-ttu-id="c8005-137">Merhaba aşağıdaki örnek dağıtımı sırasında geçirilen web sitesi toohello parametre değeri hello adını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c8005-137">hello following example sets hello name of web site toohello parameter value passed in during deployment.</span></span>

```json
"parameters": { 
  "siteName": {
      "type": "string"
  }
},
"resources": [
   {
      "apiVersion": "2016-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/Sites",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="c8005-138">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8005-138">Example</span></span>

<span data-ttu-id="c8005-139">Merhaba aşağıdaki örnek hello parametreleri işlevi Basitleştirilmiş kullanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c8005-139">hello following example shows a simplified use of hello parameters function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringParameter": {
            "type" : "string",
            "defaultValue": "option 1"
        },
        "intParameter": {
            "type": "int",
            "defaultValue": 1
        },
        "objectParameter": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b"}
        },
        "arrayParameter": {
            "type": "array",
            "defaultValue": [1, 2, 3]
        },
        "crossParameter": {
            "type": "string",
            "defaultValue": "[parameters('stringParameter')]"
        }
    },
    "variables": {},
    "resources": [],
    "outputs": {
        "stringOutput": {
            "value": "[parameters('stringParameter')]",
            "type" : "string"
        },
        "intOutput": {
            "value": "[parameters('intParameter')]",
            "type" : "int"
        },
        "objectOutput": {
            "value": "[parameters('objectParameter')]",
            "type" : "object"
        },
        "arrayOutput": {
            "value": "[parameters('arrayParameter')]",
            "type" : "array"
        },
        "crossOutput": {
            "value": "[parameters('crossParameter')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="c8005-140">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="c8005-140">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c8005-141">Ad</span><span class="sxs-lookup"><span data-stu-id="c8005-141">Name</span></span> | <span data-ttu-id="c8005-142">Tür</span><span class="sxs-lookup"><span data-stu-id="c8005-142">Type</span></span> | <span data-ttu-id="c8005-143">Değer</span><span class="sxs-lookup"><span data-stu-id="c8005-143">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c8005-144">stringOutput</span><span class="sxs-lookup"><span data-stu-id="c8005-144">stringOutput</span></span> | <span data-ttu-id="c8005-145">Dize</span><span class="sxs-lookup"><span data-stu-id="c8005-145">String</span></span> | <span data-ttu-id="c8005-146">seçenek 1</span><span class="sxs-lookup"><span data-stu-id="c8005-146">option 1</span></span> |
| <span data-ttu-id="c8005-147">intOutput</span><span class="sxs-lookup"><span data-stu-id="c8005-147">intOutput</span></span> | <span data-ttu-id="c8005-148">Int</span><span class="sxs-lookup"><span data-stu-id="c8005-148">Int</span></span> | <span data-ttu-id="c8005-149">1</span><span class="sxs-lookup"><span data-stu-id="c8005-149">1</span></span> |
| <span data-ttu-id="c8005-150">objectOutput</span><span class="sxs-lookup"><span data-stu-id="c8005-150">objectOutput</span></span> | <span data-ttu-id="c8005-151">Nesne</span><span class="sxs-lookup"><span data-stu-id="c8005-151">Object</span></span> | <span data-ttu-id="c8005-152">{"bir": "a", "iki": "b"}</span><span class="sxs-lookup"><span data-stu-id="c8005-152">{"one": "a", "two": "b"}</span></span> |
| <span data-ttu-id="c8005-153">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c8005-153">arrayOutput</span></span> | <span data-ttu-id="c8005-154">Dizi</span><span class="sxs-lookup"><span data-stu-id="c8005-154">Array</span></span> | <span data-ttu-id="c8005-155">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="c8005-155">[1, 2, 3]</span></span> |
| <span data-ttu-id="c8005-156">crossOutput</span><span class="sxs-lookup"><span data-stu-id="c8005-156">crossOutput</span></span> | <span data-ttu-id="c8005-157">Dize</span><span class="sxs-lookup"><span data-stu-id="c8005-157">String</span></span> | <span data-ttu-id="c8005-158">seçenek 1</span><span class="sxs-lookup"><span data-stu-id="c8005-158">option 1</span></span> |

<a id="variables" />

## <a name="variables"></a><span data-ttu-id="c8005-159">değişkenleri</span><span class="sxs-lookup"><span data-stu-id="c8005-159">variables</span></span>
`variables(variableName)`

<span data-ttu-id="c8005-160">Değişkenin değerini döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="c8005-160">Returns hello value of variable.</span></span> <span data-ttu-id="c8005-161">Belirtilen değişken adı Hello hello şablon değişkenleri bölümüne hello tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8005-161">hello specified variable name must be defined in hello variables section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="c8005-162">Parametreler</span><span class="sxs-lookup"><span data-stu-id="c8005-162">Parameters</span></span>

| <span data-ttu-id="c8005-163">Parametre</span><span class="sxs-lookup"><span data-stu-id="c8005-163">Parameter</span></span> | <span data-ttu-id="c8005-164">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c8005-164">Required</span></span> | <span data-ttu-id="c8005-165">Tür</span><span class="sxs-lookup"><span data-stu-id="c8005-165">Type</span></span> | <span data-ttu-id="c8005-166">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8005-166">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c8005-167">variableName</span><span class="sxs-lookup"><span data-stu-id="c8005-167">variableName</span></span> |<span data-ttu-id="c8005-168">Evet</span><span class="sxs-lookup"><span data-stu-id="c8005-168">Yes</span></span> |<span data-ttu-id="c8005-169">Dize</span><span class="sxs-lookup"><span data-stu-id="c8005-169">String</span></span> |<span data-ttu-id="c8005-170">Merhaba değişken tooreturn Hello adı.</span><span class="sxs-lookup"><span data-stu-id="c8005-170">hello name of hello variable tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c8005-171">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="c8005-171">Return value</span></span>

<span data-ttu-id="c8005-172">Merhaba belirtilen değişkenin Hello değeri.</span><span class="sxs-lookup"><span data-stu-id="c8005-172">hello value of hello specified variable.</span></span>

### <a name="remarks"></a><span data-ttu-id="c8005-173">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="c8005-173">Remarks</span></span>

<span data-ttu-id="c8005-174">Genellikle, karmaşık değerler yalnızca bir kez oluşturarak şablonunuzu değişkenleri toosimplify kullanın.</span><span class="sxs-lookup"><span data-stu-id="c8005-174">Typically, you use variables toosimplify your template by constructing complex values only once.</span></span> <span data-ttu-id="c8005-175">Merhaba aşağıdaki örnekte bir depolama hesabı için benzersiz bir ad oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c8005-175">hello following example constructs a unique name for a storage account.</span></span>

```json
"variables": {
    "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
},
"resources": [
    {
        "type": "Microsoft.Storage/storageAccounts",
        "name": "[variables('storageName')]",
        ...
    },
    {
        "type": "Microsoft.Compute/virtualMachines",
        "dependsOn": [
            "[variables('storageName')]"
        ],
        ...
    }
],
```

### <a name="example"></a><span data-ttu-id="c8005-176">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8005-176">Example</span></span>

<span data-ttu-id="c8005-177">Merhaba örnek şablonu farklı değişken değerleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="c8005-177">hello example template returns different variable values.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {
        "var1": "myVariable",
        "var2": [ 1,2,3,4 ],
        "var3": "[ variables('var1') ]",
        "var4": {
            "property1": "value1",
            "property2": "value2"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput1": {
            "value": "[variables('var1')]",
            "type" : "string"
        },
        "exampleOutput2": {
            "value": "[variables('var2')]",
            "type" : "array"
        },
        "exampleOutput3": {
            "value": "[variables('var3')]",
            "type" : "string"
        },
        "exampleOutput4": {
            "value": "[variables('var4')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="c8005-178">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="c8005-178">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c8005-179">Ad</span><span class="sxs-lookup"><span data-stu-id="c8005-179">Name</span></span> | <span data-ttu-id="c8005-180">Tür</span><span class="sxs-lookup"><span data-stu-id="c8005-180">Type</span></span> | <span data-ttu-id="c8005-181">Değer</span><span class="sxs-lookup"><span data-stu-id="c8005-181">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c8005-182">exampleOutput1</span><span class="sxs-lookup"><span data-stu-id="c8005-182">exampleOutput1</span></span> | <span data-ttu-id="c8005-183">Dize</span><span class="sxs-lookup"><span data-stu-id="c8005-183">String</span></span> | <span data-ttu-id="c8005-184">myVariable</span><span class="sxs-lookup"><span data-stu-id="c8005-184">myVariable</span></span> |
| <span data-ttu-id="c8005-185">exampleOutput2</span><span class="sxs-lookup"><span data-stu-id="c8005-185">exampleOutput2</span></span> | <span data-ttu-id="c8005-186">Dizi</span><span class="sxs-lookup"><span data-stu-id="c8005-186">Array</span></span> | <span data-ttu-id="c8005-187">[1, 2, 3, 4]</span><span class="sxs-lookup"><span data-stu-id="c8005-187">[1, 2, 3, 4]</span></span> |
| <span data-ttu-id="c8005-188">exampleOutput3</span><span class="sxs-lookup"><span data-stu-id="c8005-188">exampleOutput3</span></span> | <span data-ttu-id="c8005-189">Dize</span><span class="sxs-lookup"><span data-stu-id="c8005-189">String</span></span> | <span data-ttu-id="c8005-190">myVariable</span><span class="sxs-lookup"><span data-stu-id="c8005-190">myVariable</span></span> |
| <span data-ttu-id="c8005-191">exampleOutput4</span><span class="sxs-lookup"><span data-stu-id="c8005-191">exampleOutput4</span></span> |  <span data-ttu-id="c8005-192">Nesne</span><span class="sxs-lookup"><span data-stu-id="c8005-192">Object</span></span> | <span data-ttu-id="c8005-193">{"property1": "value1", "property2": "value2"}</span><span class="sxs-lookup"><span data-stu-id="c8005-193">{"property1": "value1", "property2": "value2"}</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c8005-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c8005-194">Next steps</span></span>
* <span data-ttu-id="c8005-195">Bir Azure Resource Manager şablonu hello bölümlerde açıklaması için bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c8005-195">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="c8005-196">birden fazla şablon toomerge bkz [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c8005-196">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="c8005-197">tooiterate belirtilen sayıda kaynak türünü oluştururken bkz [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="c8005-197">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="c8005-198">toodeploy hello şablonu oluşturduğunuz toosee bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c8005-198">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

