---
title: "aaaAzure Resource Manager şablonu yapısı ve sözdizimi | Microsoft Docs"
description: "Merhaba yapısı ve bildirim temelli JSON sözdizimini kullanarak Azure Resource Manager şablonları özelliklerini açıklar."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/14/2017
ms.author: tomfitz
ms.openlocfilehash: b0709852f8777c91cc1704d6bca16257a017d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="ca1d1-103">Merhaba yapısı ve Azure Resource Manager şablonları sözdizimi anlama</span><span class="sxs-lookup"><span data-stu-id="ca1d1-103">Understand hello structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="ca1d1-104">Bu konu, bir Azure Resource Manager şablonu hello yapısını açıklar.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-104">This topic describes hello structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="ca1d1-105">Bu bölümlerdeki kullanılabilir olan bir şablonu ve özelliklerinin hello hello farklı bölümleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-105">It presents hello different sections of a template and hello properties that are available in those sections.</span></span> <span data-ttu-id="ca1d1-106">JSON ve dağıtımınız için tooconstruct değerleri kullanabileceğiniz ifadeler Hello şablonu oluşur.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-106">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="ca1d1-107">Şablon oluşturmanın adım adım öğretici için bkz [, ilk Azure Resource Manager şablonu oluşturma](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="ca1d1-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

## <a name="template-format"></a><span data-ttu-id="ca1d1-108">Şablon biçimi</span><span class="sxs-lookup"><span data-stu-id="ca1d1-108">Template format</span></span>
<span data-ttu-id="ca1d1-109">Basit yapısını bir şablon hello aşağıdaki öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="ca1d1-109">In its simplest structure, a template contains hello following elements:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| <span data-ttu-id="ca1d1-110">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="ca1d1-110">Element name</span></span> | <span data-ttu-id="ca1d1-111">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ca1d1-111">Required</span></span> | <span data-ttu-id="ca1d1-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ca1d1-112">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ca1d1-113">$schema</span><span class="sxs-lookup"><span data-stu-id="ca1d1-113">$schema</span></span> |<span data-ttu-id="ca1d1-114">Evet</span><span class="sxs-lookup"><span data-stu-id="ca1d1-114">Yes</span></span> |<span data-ttu-id="ca1d1-115">Merhaba şablon dili hello sürümü açıklanmaktadır hello JSON Şeması dosyasının konumu.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-115">Location of hello JSON schema file that describes hello version of hello template language.</span></span> <span data-ttu-id="ca1d1-116">Örnek önceki hello gösterilen hello URL kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-116">Use hello URL shown in hello preceding example.</span></span> |
| <span data-ttu-id="ca1d1-117">contentVersion</span><span class="sxs-lookup"><span data-stu-id="ca1d1-117">contentVersion</span></span> |<span data-ttu-id="ca1d1-118">Evet</span><span class="sxs-lookup"><span data-stu-id="ca1d1-118">Yes</span></span> |<span data-ttu-id="ca1d1-119">Merhaba şablonu (örneğin, 1.0.0.0) sürümü.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-119">Version of hello template (such as 1.0.0.0).</span></span> <span data-ttu-id="ca1d1-120">Bu öğe için herhangi bir değer sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-120">You can provide any value for this element.</span></span> <span data-ttu-id="ca1d1-121">Merhaba şablonu kullanarak kaynak dağıtırken, bu değer kullanılan toomake hello sağ şablon kullanıldığından emin olabilir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-121">When deploying resources using hello template, this value can be used toomake sure that hello right template is being used.</span></span> |
| <span data-ttu-id="ca1d1-122">parametreler</span><span class="sxs-lookup"><span data-stu-id="ca1d1-122">parameters</span></span> |<span data-ttu-id="ca1d1-123">Hayır</span><span class="sxs-lookup"><span data-stu-id="ca1d1-123">No</span></span> |<span data-ttu-id="ca1d1-124">Dağıtım olduğunda, sağlanan değerler toocustomize kaynak dağıtım yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-124">Values that are provided when deployment is executed toocustomize resource deployment.</span></span> |
| <span data-ttu-id="ca1d1-125">değişkenleri</span><span class="sxs-lookup"><span data-stu-id="ca1d1-125">variables</span></span> |<span data-ttu-id="ca1d1-126">Hayır</span><span class="sxs-lookup"><span data-stu-id="ca1d1-126">No</span></span> |<span data-ttu-id="ca1d1-127">JSON parçalanma hello şablonu toosimplify şablon dili ifadeleri olarak kullanılan değerler.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-127">Values that are used as JSON fragments in hello template toosimplify template language expressions.</span></span> |
| <span data-ttu-id="ca1d1-128">Kaynakları</span><span class="sxs-lookup"><span data-stu-id="ca1d1-128">resources</span></span> |<span data-ttu-id="ca1d1-129">Evet</span><span class="sxs-lookup"><span data-stu-id="ca1d1-129">Yes</span></span> |<span data-ttu-id="ca1d1-130">Dağıtılan veya bir kaynak grubunda güncelleştirilmiş kaynak türleri.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-130">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="ca1d1-131">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="ca1d1-131">outputs</span></span> |<span data-ttu-id="ca1d1-132">Hayır</span><span class="sxs-lookup"><span data-stu-id="ca1d1-132">No</span></span> |<span data-ttu-id="ca1d1-133">Dağıtımdan sonra döndürülen değer.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-133">Values that are returned after deployment.</span></span> |

<span data-ttu-id="ca1d1-134">Her öğe ayarlayabileceğiniz özellikler içerir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-134">Each element contains properties you can set.</span></span> <span data-ttu-id="ca1d1-135">Aşağıdaki örneğine hello hello bir şablon için tam söz dizimi içeriyor:</span><span class="sxs-lookup"><span data-stu-id="ca1d1-135">hello following example contains hello full syntax for a template:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  
        "<parameter-name>" : {
            "type" : "<type-of-parameter-value>",
            "defaultValue": "<default-value-of-parameter>",
            "allowedValues": [ "<array-of-allowed-values>" ],
            "minValue": <minimum-value-for-int>,
            "maxValue": <maximum-value-for-int>,
            "minLength": <minimum-length-for-string-or-array>,
            "maxLength": <maximum-length-for-string-or-array-parameters>,
            "metadata": {
                "description": "<description-of-hello parameter>" 
            }
        }
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "condition": "<boolean-value-whether-to-deploy>",
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": {
              "<tag-name1>": "<tag-value1>",
              "<tag-name2>": "<tag-value2>"
          },
          "comments": "<your-reference-notes>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>",
              "mode": "<serial-or-parallel>",
              "batchSize": "<number-to-deploy-serially>"
          },
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": {
              "<settings-for-the-resource>",
              "copy": [
                  {
                      "name": ,
                      "count": ,
                      "input": {}
                  }
              ]
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

<span data-ttu-id="ca1d1-136">Bu konunun ilerleyen bölümlerinde daha ayrıntılı hello şablon hello bölümlerini inceleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-136">We examine hello sections of hello template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="ca1d1-137">İfadeler ve işlevleri</span><span class="sxs-lookup"><span data-stu-id="ca1d1-137">Expressions and functions</span></span>
<span data-ttu-id="ca1d1-138">Merhaba temel sözdizimi hello şablonunun JSON şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-138">hello basic syntax of hello template is JSON.</span></span> <span data-ttu-id="ca1d1-139">Ancak, ifadeler ve işlevleri hello JSON değerleri hello şablonu içinde kullanılabilir genişletir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-139">However, expressions and functions extend hello JSON values available within hello template.</span></span>  <span data-ttu-id="ca1d1-140">İfadeler, ilk JSON dize değişmez değerleri içinde yazılır ve son karakterlerdir hello köşeli: `[` ve `]`sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-140">Expressions are written within JSON string literals whose first and last characters are hello brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="ca1d1-141">Merhaba şablon dağıtıldığında hello ifade hello değeri değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-141">hello value of hello expression is evaluated when hello template is deployed.</span></span> <span data-ttu-id="ca1d1-142">Bir dize yazılmış olsa da, hello ifade değerlendirme sonucunu hello gibi bir dizi veya tamsayı hello gerçek ifade bağlı olarak farklı bir JSON türde olabilir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-142">While written as a string literal, hello result of evaluating hello expression can be of a different JSON type, such as an array or integer, depending on hello actual expression.</span></span>  <span data-ttu-id="ca1d1-143">sabit değerli bir dize Başlat köşeli ayraç ile toohave `[`, ancak değil bir ifade olarak yorumlanır olması, fazladan ayraç toostart hello dizesiyle eklemek `[[`.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-143">toohave a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket toostart hello string with `[[`.</span></span>

<span data-ttu-id="ca1d1-144">Genellikle, hello dağıtım yapılandırma işlevleri tooperform işlemleri içeren ifadeler kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-144">Typically, you use expressions with functions tooperform operations for configuring hello deployment.</span></span> <span data-ttu-id="ca1d1-145">JavaScript'te, işlev çağrıları olarak biçimlendirilmiş gibi yalnızca `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-145">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="ca1d1-146">Özellikler hello nokta ve [dizin] işleçleri kullanarak başvuru.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-146">You reference properties by using hello dot and [index] operators.</span></span>

<span data-ttu-id="ca1d1-147">örnekte gösterildiği nasıl birkaç işlevleri oluşturulurken toouse değerleri hello:</span><span class="sxs-lookup"><span data-stu-id="ca1d1-147">hello following example shows how toouse several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="ca1d1-148">Merhaba tam şablon işlevlerin listesi için bkz: [Azure Resource Manager şablonu işlevleri](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="ca1d1-148">For hello full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="ca1d1-149">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ca1d1-149">Parameters</span></span>
<span data-ttu-id="ca1d1-150">Merhaba Parametreler bölümünde hello şablonunun dağıtırken giriş hangi değerlerin kaynakları hello belirtin.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-150">In hello parameters section of hello template, you specify which values you can input when deploying hello resources.</span></span> <span data-ttu-id="ca1d1-151">Bu parametre değerleri (örneğin, geliştirme, test ve üretim) belirli bir ortam için uyarlanabilir değerleri sağlayarak toocustomize hello dağıtımını etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-151">These parameter values enable you toocustomize hello deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="ca1d1-152">Şablonunuzda tooprovide parametrelere sahip değildir, ancak parametre olmadan şablonunuzu her zaman hello dağıtmak için kullanacağınız aynı kaynaklarla hello aynı adları, konumları ve özellikler.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-152">You do not have tooprovide parameters in your template, but without parameters your template would always deploy hello same resources with hello same names, locations, and properties.</span></span>

<span data-ttu-id="ca1d1-153">Yapı izlenerek hello ile parametrelerini tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="ca1d1-153">You define parameters with hello following structure:</span></span>

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-hello parameter>" 
        }
    }
}
```

| <span data-ttu-id="ca1d1-154">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="ca1d1-154">Element name</span></span> | <span data-ttu-id="ca1d1-155">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ca1d1-155">Required</span></span> | <span data-ttu-id="ca1d1-156">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ca1d1-156">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ca1d1-157">parameterName</span><span class="sxs-lookup"><span data-stu-id="ca1d1-157">parameterName</span></span> |<span data-ttu-id="ca1d1-158">Evet</span><span class="sxs-lookup"><span data-stu-id="ca1d1-158">Yes</span></span> |<span data-ttu-id="ca1d1-159">Merhaba parametresinin adı.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-159">Name of hello parameter.</span></span> <span data-ttu-id="ca1d1-160">Geçerli bir JavaScript tanımlayıcı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-160">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="ca1d1-161">type</span><span class="sxs-lookup"><span data-stu-id="ca1d1-161">type</span></span> |<span data-ttu-id="ca1d1-162">Evet</span><span class="sxs-lookup"><span data-stu-id="ca1d1-162">Yes</span></span> |<span data-ttu-id="ca1d1-163">Merhaba parametre değeri türü.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-163">Type of hello parameter value.</span></span> <span data-ttu-id="ca1d1-164">İzin verilen türleri Hello listesi sonra bu tabloya bakın.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-164">See hello list of allowed types after this table.</span></span> |
| <span data-ttu-id="ca1d1-165">defaultValue</span><span class="sxs-lookup"><span data-stu-id="ca1d1-165">defaultValue</span></span> |<span data-ttu-id="ca1d1-166">Hayır</span><span class="sxs-lookup"><span data-stu-id="ca1d1-166">No</span></span> |<span data-ttu-id="ca1d1-167">Merhaba parametresi için hiçbir değer sağlanmazsa hello parametresinin varsayılan değeri.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-167">Default value for hello parameter, if no value is provided for hello parameter.</span></span> |
| <span data-ttu-id="ca1d1-168">allowedValues</span><span class="sxs-lookup"><span data-stu-id="ca1d1-168">allowedValues</span></span> |<span data-ttu-id="ca1d1-169">Hayır</span><span class="sxs-lookup"><span data-stu-id="ca1d1-169">No</span></span> |<span data-ttu-id="ca1d1-170">Merhaba parametresi toomake hello sağ değer sağlandığından emin izin verilen değerleri dizisi.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-170">Array of allowed values for hello parameter toomake sure that hello right value is provided.</span></span> |
| <span data-ttu-id="ca1d1-171">MinValue</span><span class="sxs-lookup"><span data-stu-id="ca1d1-171">minValue</span></span> |<span data-ttu-id="ca1d1-172">Hayır</span><span class="sxs-lookup"><span data-stu-id="ca1d1-172">No</span></span> |<span data-ttu-id="ca1d1-173">Merhaba int türü parametreler için minimum değeri, bu kapsayıcı değerdir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-173">hello minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="ca1d1-174">MaxValue</span><span class="sxs-lookup"><span data-stu-id="ca1d1-174">maxValue</span></span> |<span data-ttu-id="ca1d1-175">Hayır</span><span class="sxs-lookup"><span data-stu-id="ca1d1-175">No</span></span> |<span data-ttu-id="ca1d1-176">Merhaba int türü parametreleri için en büyük değer, bu kapsayıcı değerdir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-176">hello maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="ca1d1-177">minLength</span><span class="sxs-lookup"><span data-stu-id="ca1d1-177">minLength</span></span> |<span data-ttu-id="ca1d1-178">Hayır</span><span class="sxs-lookup"><span data-stu-id="ca1d1-178">No</span></span> |<span data-ttu-id="ca1d1-179">Merhaba dize, secureString ve dizi türü parametreler için minimum uzunluk, bu kapsayıcı değerdir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-179">hello minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="ca1d1-180">maxLength</span><span class="sxs-lookup"><span data-stu-id="ca1d1-180">maxLength</span></span> |<span data-ttu-id="ca1d1-181">Hayır</span><span class="sxs-lookup"><span data-stu-id="ca1d1-181">No</span></span> |<span data-ttu-id="ca1d1-182">Merhaba dize, secureString ve dizi türü parametreleri için en fazla uzunluk, bu kapsayıcı değerdir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-182">hello maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="ca1d1-183">açıklama</span><span class="sxs-lookup"><span data-stu-id="ca1d1-183">description</span></span> |<span data-ttu-id="ca1d1-184">Hayır</span><span class="sxs-lookup"><span data-stu-id="ca1d1-184">No</span></span> |<span data-ttu-id="ca1d1-185">Olan hello parametre açıklaması hello portal üzerinden toousers görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-185">Description of hello parameter that is displayed toousers through hello portal.</span></span> |

<span data-ttu-id="ca1d1-186">Merhaba izin verilen türleri ve değerleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ca1d1-186">hello allowed types and values are:</span></span>

* <span data-ttu-id="ca1d1-187">**dize**</span><span class="sxs-lookup"><span data-stu-id="ca1d1-187">**string**</span></span>
* <span data-ttu-id="ca1d1-188">**secureString**</span><span class="sxs-lookup"><span data-stu-id="ca1d1-188">**secureString**</span></span>
* <span data-ttu-id="ca1d1-189">**int**</span><span class="sxs-lookup"><span data-stu-id="ca1d1-189">**int**</span></span>
* <span data-ttu-id="ca1d1-190">**bool**</span><span class="sxs-lookup"><span data-stu-id="ca1d1-190">**bool**</span></span>
* <span data-ttu-id="ca1d1-191">**Nesne**</span><span class="sxs-lookup"><span data-stu-id="ca1d1-191">**object**</span></span> 
* <span data-ttu-id="ca1d1-192">**secureObject**</span><span class="sxs-lookup"><span data-stu-id="ca1d1-192">**secureObject**</span></span>
* <span data-ttu-id="ca1d1-193">**dizi**</span><span class="sxs-lookup"><span data-stu-id="ca1d1-193">**array**</span></span>

<span data-ttu-id="ca1d1-194">toospecify parametre isteğe bağlı olarak (boş bir dize olabilir) bir defaultValue sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-194">toospecify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="ca1d1-195">Şablonunuzdaki hello komutu toodeploy hello şablonu içindeki bir parametre ile eşleşen bir parametre adı belirtirseniz, olası karışıklığı sağladığınız hello değerleri hakkında yoktur.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-195">If you specify a parameter name in your template that matches a parameter in hello command toodeploy hello template, there is potential ambiguity about hello values you provide.</span></span> <span data-ttu-id="ca1d1-196">Resource Manager hello sonek ekleyerek bu karışıklığı çözümler **FromTemplate** toohello şablon parametresi.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-196">Resource Manager resolves this confusion by adding hello postfix **FromTemplate** toohello template parameter.</span></span> <span data-ttu-id="ca1d1-197">Örneğin, adlı bir parametre dahil ederseniz **ResourceGroupName** isteğe bağlı olarak, şablonunuzda hello ile çakışıyor **ResourceGroupName** hello parametresinde [ Yeni-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-197">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="ca1d1-198">Dağıtım sırasında istendiğinde tooprovide için bir değer olduğunuz **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-198">During deployment, you are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="ca1d1-199">Genel olarak, aynı dağıtım işlemleri için kullanılan parametreler olarak ad hello parametrelerle adlandırılmasıyla değil Bu Karışıklığı önlemek.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-199">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="ca1d1-200">Tüm parolalar, anahtarlar ve diğer parolaları hello kullanması gereken **secureString** türü.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-200">All passwords, keys, and other secrets should use hello **secureString** type.</span></span> <span data-ttu-id="ca1d1-201">Bir JSON nesnesinde hassas verileri geçirirseniz, hello kullan **secureObject** türü.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-201">If you pass sensitive data in a JSON object, use hello **secureObject** type.</span></span> <span data-ttu-id="ca1d1-202">Şablon parametreleri secureString veya secureObject türleriyle kaynak dağıtımdan sonra okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-202">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="ca1d1-203">Örneğin, hello hello dağıtım geçmişi dosyasında şu girişi hello değeri bir dize ve nesne için kullanılabilir ancak secureString ve secureObject gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-203">For example, hello following entry in hello deployment history shows hello value for a string and object but not for secureString and secureObject.</span></span>
>
> ![Dağıtım değerlerini göster](./media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="ca1d1-205">örnekte gösterildiği nasıl aşağıdaki hello toodefine Parametreler:</span><span class="sxs-lookup"><span data-stu-id="ca1d1-205">hello following example shows how toodefine parameters:</span></span>

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

<span data-ttu-id="ca1d1-206">Tooinput hello parametre dağıtım sırasında nasıl değerleri için bkz: [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ca1d1-206">For how tooinput hello parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="ca1d1-207">Değişkenler</span><span class="sxs-lookup"><span data-stu-id="ca1d1-207">Variables</span></span>
<span data-ttu-id="ca1d1-208">Merhaba değişkenler bölümünde şablonunuzu kullanılabilir değerleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-208">In hello variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="ca1d1-209">Toodefine değişkenleri gerekmez, ancak bunlar karmaşık ifadeler azaltarak genellikle şablonunuzu basitleştirin.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-209">You do not need toodefine variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="ca1d1-210">Yapı izlenerek hello ile değişkenleri tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="ca1d1-210">You define variables with hello following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="ca1d1-211">örnekte gösterildiği nasıl aşağıdaki hello toodefine iki parametre değerlerinin oluşturulan bir değişkeni:</span><span class="sxs-lookup"><span data-stu-id="ca1d1-211">hello following example shows how toodefine a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="ca1d1-212">Merhaba sonraki örnek karmaşık bir JSON türe sahip bir değişken ve diğer değişkenlerinden oluşturulan değişkenleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="ca1d1-212">hello next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a><span data-ttu-id="ca1d1-213">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ca1d1-213">Resources</span></span>
<span data-ttu-id="ca1d1-214">Merhaba kaynaklar bölümünde dağıtılan veya güncelleştirilen hello kaynakları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-214">In hello resources section, you define hello resources that are deployed or updated.</span></span> <span data-ttu-id="ca1d1-215">Merhaba türlerini anlamanız gerekir çünkü bu bölümde karmaşık alabilirsiniz tooprovide hello doğru değerleri dağıtma.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-215">This section can get complicated because you must understand hello types you are deploying tooprovide hello right values.</span></span> <span data-ttu-id="ca1d1-216">Tooset gereken hello kaynak özgü değerlerini (apiVersion, türü ve özellikleri), görmek [kaynakları tanımlayan Azure Resource Manager şablonları](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="ca1d1-216">For hello resource-specific values (apiVersion, type, and properties) that you need tooset, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="ca1d1-217">Yapı izlenerek hello ile kaynakları tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="ca1d1-217">You define resources with hello following structure:</span></span>

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| <span data-ttu-id="ca1d1-218">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="ca1d1-218">Element name</span></span> | <span data-ttu-id="ca1d1-219">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ca1d1-219">Required</span></span> | <span data-ttu-id="ca1d1-220">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ca1d1-220">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ca1d1-221">Koşul</span><span class="sxs-lookup"><span data-stu-id="ca1d1-221">condition</span></span> | <span data-ttu-id="ca1d1-222">Hayır</span><span class="sxs-lookup"><span data-stu-id="ca1d1-222">No</span></span> | <span data-ttu-id="ca1d1-223">Merhaba kaynak dağıtılabilir olup olmadığını gösteren Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-223">Boolean value that indicates whether hello resource is deployed.</span></span> |
| <span data-ttu-id="ca1d1-224">apiVersion</span><span class="sxs-lookup"><span data-stu-id="ca1d1-224">apiVersion</span></span> |<span data-ttu-id="ca1d1-225">Evet</span><span class="sxs-lookup"><span data-stu-id="ca1d1-225">Yes</span></span> |<span data-ttu-id="ca1d1-226">Merhaba kaynak oluşturmak için REST API toouse hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-226">Version of hello REST API toouse for creating hello resource.</span></span> |
| <span data-ttu-id="ca1d1-227">type</span><span class="sxs-lookup"><span data-stu-id="ca1d1-227">type</span></span> |<span data-ttu-id="ca1d1-228">Evet</span><span class="sxs-lookup"><span data-stu-id="ca1d1-228">Yes</span></span> |<span data-ttu-id="ca1d1-229">Merhaba kaynak türü.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-229">Type of hello resource.</span></span> <span data-ttu-id="ca1d1-230">Bu değer hello kaynak sağlayıcısı ve hello kaynak türü hello ad birleşimidir (gibi **Microsoft.Storage/storageAccounts**).</span><span class="sxs-lookup"><span data-stu-id="ca1d1-230">This value is a combination of hello namespace of hello resource provider and hello resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="ca1d1-231">ad</span><span class="sxs-lookup"><span data-stu-id="ca1d1-231">name</span></span> |<span data-ttu-id="ca1d1-232">Evet</span><span class="sxs-lookup"><span data-stu-id="ca1d1-232">Yes</span></span> |<span data-ttu-id="ca1d1-233">Merhaba kaynağın adı.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-233">Name of hello resource.</span></span> <span data-ttu-id="ca1d1-234">Merhaba adı RFC3986 içinde tanımlanan URI bileşeni kısıtlamaları izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-234">hello name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="ca1d1-235">Ayrıca, hello kaynak adı toooutside tarafların kullanıma Azure Hizmetleri hello adı toomake girişimi toospoof olmadığından emin doğrula başka bir kimlik.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-235">In addition, Azure services that expose hello resource name toooutside parties validate hello name toomake sure it is not an attempt toospoof another identity.</span></span> |
| <span data-ttu-id="ca1d1-236">location</span><span class="sxs-lookup"><span data-stu-id="ca1d1-236">location</span></span> |<span data-ttu-id="ca1d1-237">Değişir</span><span class="sxs-lookup"><span data-stu-id="ca1d1-237">Varies</span></span> |<span data-ttu-id="ca1d1-238">Merhaba, desteklenen coğrafi konumda kaynak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-238">Supported geo-locations of hello provided resource.</span></span> <span data-ttu-id="ca1d1-239">Merhaba kullanılabilir konumlardan herhangi birinden seçebilirsiniz, ancak genellikle algılama toopick Kapat tooyour kullanıcıları olan bir kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-239">You can select any of hello available locations, but typically it makes sense toopick one that is close tooyour users.</span></span> <span data-ttu-id="ca1d1-240">Genellikle, ayrıca hello aynı birbiriyle etkileşimde tooplace kaynakları mantıklıdır bölgesi.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-240">Usually, it also makes sense tooplace resources that interact with each other in hello same region.</span></span> <span data-ttu-id="ca1d1-241">Çoğu kaynak türleri bir konum gerektirir, ancak bazı türleri (örneğin, bir rol ataması) bir konum gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-241">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="ca1d1-242">Bkz: [Azure Resource Manager şablonları kaynak konumunu ayarla](resource-manager-template-location.md).</span><span class="sxs-lookup"><span data-stu-id="ca1d1-242">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="ca1d1-243">etiketler</span><span class="sxs-lookup"><span data-stu-id="ca1d1-243">tags</span></span> |<span data-ttu-id="ca1d1-244">Hayır</span><span class="sxs-lookup"><span data-stu-id="ca1d1-244">No</span></span> |<span data-ttu-id="ca1d1-245">Merhaba kaynakla ilişkilendirilmiş etiketler.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-245">Tags that are associated with hello resource.</span></span> <span data-ttu-id="ca1d1-246">Bkz: [Azure Resource Manager'da kaynakları etiketi](resource-manager-template-tags.md).</span><span class="sxs-lookup"><span data-stu-id="ca1d1-246">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="ca1d1-247">Açıklamaları</span><span class="sxs-lookup"><span data-stu-id="ca1d1-247">comments</span></span> |<span data-ttu-id="ca1d1-248">Hayır</span><span class="sxs-lookup"><span data-stu-id="ca1d1-248">No</span></span> |<span data-ttu-id="ca1d1-249">Şablonunuzda hello kaynakları belgeleme için notları</span><span class="sxs-lookup"><span data-stu-id="ca1d1-249">Your notes for documenting hello resources in your template</span></span> |
| <span data-ttu-id="ca1d1-250">Kopyalama</span><span class="sxs-lookup"><span data-stu-id="ca1d1-250">copy</span></span> |<span data-ttu-id="ca1d1-251">Hayır</span><span class="sxs-lookup"><span data-stu-id="ca1d1-251">No</span></span> |<span data-ttu-id="ca1d1-252">Birden fazla örneği gerekiyorsa, kaynakları toocreate sayısı hello.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-252">If more than one instance is needed, hello number of resources toocreate.</span></span> <span data-ttu-id="ca1d1-253">Merhaba varsayılan paralel moddur.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-253">hello default mode is parallel.</span></span> <span data-ttu-id="ca1d1-254">Değil tüm veya istediğinizde hello hello adresindeki kaynakları toodeploy seri modunu belirtin aynı anda.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-254">Specify serial mode when you do not want all or hello resources toodeploy at hello same time.</span></span> <span data-ttu-id="ca1d1-255">Daha fazla bilgi için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="ca1d1-255">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="ca1d1-256">dependsOn</span><span class="sxs-lookup"><span data-stu-id="ca1d1-256">dependsOn</span></span> |<span data-ttu-id="ca1d1-257">Hayır</span><span class="sxs-lookup"><span data-stu-id="ca1d1-257">No</span></span> |<span data-ttu-id="ca1d1-258">Bu kaynak dağıtılmadan önce dağıtılmalıdır kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-258">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="ca1d1-259">Resource Manager kaynakları arasındaki hello bağımlılıkları değerlendirir ve hello doğru sırayla dağıtır.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-259">Resource Manager evaluates hello dependencies between resources and deploys them in hello correct order.</span></span> <span data-ttu-id="ca1d1-260">Kaynakları birbirlerine bağımlı olmadıkları zaman bunların paralel olarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-260">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="ca1d1-261">Merhaba değeri olan bir kaynağın virgülle ayrılmış bir liste olabilir adları veya kaynak benzersiz tanımlayıcıları.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-261">hello value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="ca1d1-262">Yalnızca bu şablonda dağıtılan kaynakları listeler.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-262">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="ca1d1-263">Bu şablonda tanımlı değil kaynakları önceden var olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-263">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="ca1d1-264">Dağıtımınızı yavaş ve döngüsel bağımlılıklar oluşturma gibi gereksiz bağımlılıkları eklemekten kaçının.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-264">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="ca1d1-265">Bağımlılıklarını ayarlama hakkında yönergeler için bkz [Azure Resource Manager'da bağımlılıkları tanımlama](resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="ca1d1-265">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="ca1d1-266">properties</span><span class="sxs-lookup"><span data-stu-id="ca1d1-266">properties</span></span> |<span data-ttu-id="ca1d1-267">Hayır</span><span class="sxs-lookup"><span data-stu-id="ca1d1-267">No</span></span> |<span data-ttu-id="ca1d1-268">Kaynak özgü yapılandırma ayarları.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-268">Resource-specific configuration settings.</span></span> <span data-ttu-id="ca1d1-269">Merhaba özelliklerinin Hello değerlerini olduğunuz hello aynı hello istek gövdesinde hello REST API işlemi (PUT yöntemini) toocreate hello kaynağı için sağladığınız hello değerleri olarak.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-269">hello values for hello properties are hello same as hello values you provide in hello request body for hello REST API operation (PUT method) toocreate hello resource.</span></span> <span data-ttu-id="ca1d1-270">Kopya dizi toocreate bir özelliği birden çok örneğini de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-270">You can also specify a copy array toocreate multiple instances of a property.</span></span> <span data-ttu-id="ca1d1-271">Daha fazla bilgi için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="ca1d1-271">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="ca1d1-272">Kaynakları</span><span class="sxs-lookup"><span data-stu-id="ca1d1-272">resources</span></span> |<span data-ttu-id="ca1d1-273">Hayır</span><span class="sxs-lookup"><span data-stu-id="ca1d1-273">No</span></span> |<span data-ttu-id="ca1d1-274">Tanımlanan hello kaynağına bağımlı alt kaynakları.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-274">Child resources that depend on hello resource being defined.</span></span> <span data-ttu-id="ca1d1-275">Yalnızca hello üst kaynak hello şema tarafından izin verilen kaynak türleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-275">Only provide resource types that are permitted by hello schema of hello parent resource.</span></span> <span data-ttu-id="ca1d1-276">Merhaba hello alt kaynağının tam olarak nitelenmiş tür hello üst kaynak türü, gibi içerir **Microsoft.Web/sites/extensions**.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-276">hello fully qualified type of hello child resource includes hello parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="ca1d1-277">Merhaba üst Kaynak bağımlılığı kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-277">Dependency on hello parent resource is not implied.</span></span> <span data-ttu-id="ca1d1-278">Bu bağımlılık açıkça tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-278">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="ca1d1-279">Merhaba kaynaklar bölümünde hello kaynakları toodeploy dizisi içerir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-279">hello resources section contains an array of hello resources toodeploy.</span></span> <span data-ttu-id="ca1d1-280">Her kaynak içinde bir dizi alt kaynakları da tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-280">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="ca1d1-281">Bu nedenle, kaynakları bölümünüzü gibi bir yapıya sahip:</span><span class="sxs-lookup"><span data-stu-id="ca1d1-281">Therefore, your resources section could have a structure like:</span></span>

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

<span data-ttu-id="ca1d1-282">Alt kaynakları tanımlama hakkında daha fazla bilgi için bkz: [Resource Manager şablonunda alt kaynak için ad ve tür ayarlamak](resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="ca1d1-282">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

<span data-ttu-id="ca1d1-283">Merhaba **koşulu** öğesi hello kaynak dağıtılabilir olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-283">hello **condition** element specifies whether hello resource is deployed.</span></span> <span data-ttu-id="ca1d1-284">Bu öğe için başlangıç değerini tootrue ya da yanlış çözümler.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-284">hello value for this element resolves tootrue or false.</span></span> <span data-ttu-id="ca1d1-285">Örneğin, yeni bir depolama hesabı dağıtmış olup olmadığını toospecify kullanın:</span><span class="sxs-lookup"><span data-stu-id="ca1d1-285">For example, toospecify whether a new storage account is deployed, use:</span></span>

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

<span data-ttu-id="ca1d1-286">Yeni veya mevcut bir kaynağı kullanarak bir örnek için bkz: [yeni veya varolan bir koşul şablonu](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="ca1d1-286">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="ca1d1-287">toospecify bir parola veya SSH anahtarı, bir sanal makinenin dağıtıldığı olup olmadığını tanımlayın iki sürümü hello sanal makine, şablon ve kullanım **koşulu** toodifferentiate kullanımı.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-287">toospecify whether a virtual machine is deployed with a password or SSH key, define two versions of hello virtual machine in your template and use **condition** toodifferentiate usage.</span></span> <span data-ttu-id="ca1d1-288">Hangi senaryo toodeploy belirten bir parametre geçirin.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-288">Pass a parameter that specifies which scenario toodeploy.</span></span>

```json
{
    "condition": "[equals(parameters('passwordOrSshKey'),'password')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'password')]",
    "properties": {
        "osProfile": {
            "computerName": "[variables('vmName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
        },
        ...
    },
    ...
},
{
    "condition": "[equals(parameters('passwordOrSshKey'),'sshKey')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'ssh')]",
    "properties": {
        "osProfile": {
            "linuxConfiguration": {
                "disablePasswordAuthentication": "true",
                "ssh": {
                    "publicKeys": [
                        {
                            "path": "[variables('sshKeyPath')]",
                            "keyData": "[parameters('adminSshKey')]"
                        }
                    ]
                }
            }
        },
        ...
    },
    ...
}
``` 

<span data-ttu-id="ca1d1-289">Bir parola veya SSH anahtar toodeploy sanal makine kullanarak bir örnek için bkz: [kullanıcı adı veya SSH koşul şablon](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="ca1d1-289">For an example of using a password or SSH key toodeploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="outputs"></a><span data-ttu-id="ca1d1-290">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="ca1d1-290">Outputs</span></span>
<span data-ttu-id="ca1d1-291">Merhaba çıkışları bölümünde dağıtımından döndürülen değerlerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-291">In hello Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="ca1d1-292">Örneğin, dağıtılmış bir kaynak hello URI tooaccess döndürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-292">For example, you could return hello URI tooaccess a deployed resource.</span></span>

<span data-ttu-id="ca1d1-293">Merhaba aşağıdaki örnek bir çıktı tanımının hello yapısını gösterir:</span><span class="sxs-lookup"><span data-stu-id="ca1d1-293">hello following example shows hello structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="ca1d1-294">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="ca1d1-294">Element name</span></span> | <span data-ttu-id="ca1d1-295">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ca1d1-295">Required</span></span> | <span data-ttu-id="ca1d1-296">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ca1d1-296">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ca1d1-297">outputName</span><span class="sxs-lookup"><span data-stu-id="ca1d1-297">outputName</span></span> |<span data-ttu-id="ca1d1-298">Evet</span><span class="sxs-lookup"><span data-stu-id="ca1d1-298">Yes</span></span> |<span data-ttu-id="ca1d1-299">Merhaba çıkış değeri adı.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-299">Name of hello output value.</span></span> <span data-ttu-id="ca1d1-300">Geçerli bir JavaScript tanımlayıcı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-300">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="ca1d1-301">type</span><span class="sxs-lookup"><span data-stu-id="ca1d1-301">type</span></span> |<span data-ttu-id="ca1d1-302">Evet</span><span class="sxs-lookup"><span data-stu-id="ca1d1-302">Yes</span></span> |<span data-ttu-id="ca1d1-303">Merhaba çıkış değerini yazın.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-303">Type of hello output value.</span></span> <span data-ttu-id="ca1d1-304">Çıkış değerleri aynı şablon giriş parametreleri olarak türleri hello destekler.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-304">Output values support hello same types as template input parameters.</span></span> |
| <span data-ttu-id="ca1d1-305">değer</span><span class="sxs-lookup"><span data-stu-id="ca1d1-305">value</span></span> |<span data-ttu-id="ca1d1-306">Evet</span><span class="sxs-lookup"><span data-stu-id="ca1d1-306">Yes</span></span> |<span data-ttu-id="ca1d1-307">Hesaplanan ve çıktı değeri olarak döndürülen şablon dili ifadesi.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-307">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="ca1d1-308">Merhaba aşağıdaki örnek hello çıkışları bölümünde döndürülen bir değer gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-308">hello following example shows a value that is returned in hello Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="ca1d1-309">Çıktı ile çalışma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları durumda paylaşımı](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="ca1d1-309">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="template-limits"></a><span data-ttu-id="ca1d1-310">Şablon sınırları</span><span class="sxs-lookup"><span data-stu-id="ca1d1-310">Template limits</span></span>

<span data-ttu-id="ca1d1-311">Merhaba boyut sınırı, şablon too1 MB ve her bir parametreyi too64 KB dosya.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-311">Limit hello size of your template too1 MB, and each parameter file too64 KB.</span></span> <span data-ttu-id="ca1d1-312">yinelemeli Kaynak tanımları ve değişkenleri ve parametreleri için değerler ile genişletilmiştir sonra hello 1 MB sınırını toohello son durum hello şablonunun uygulanır.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-312">hello 1-MB limit applies toohello final state of hello template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

<span data-ttu-id="ca1d1-313">Ayrıca için sınırlıdır:</span><span class="sxs-lookup"><span data-stu-id="ca1d1-313">You are also limited to:</span></span>

* <span data-ttu-id="ca1d1-314">256 parametreleri</span><span class="sxs-lookup"><span data-stu-id="ca1d1-314">256 parameters</span></span>
* <span data-ttu-id="ca1d1-315">256 değişkenleri</span><span class="sxs-lookup"><span data-stu-id="ca1d1-315">256 variables</span></span>
* <span data-ttu-id="ca1d1-316">800 kaynakları (kopya sayısı dahil)</span><span class="sxs-lookup"><span data-stu-id="ca1d1-316">800 resources (including copy count)</span></span>
* <span data-ttu-id="ca1d1-317">64 çıkış değerleri</span><span class="sxs-lookup"><span data-stu-id="ca1d1-317">64 output values</span></span>
* <span data-ttu-id="ca1d1-318">bir şablon ifadesinde 24.576 karakterleri</span><span class="sxs-lookup"><span data-stu-id="ca1d1-318">24,576 characters in a template expression</span></span>

<span data-ttu-id="ca1d1-319">İç içe geçmiş bir şablon kullanarak bazı şablonu sınırı aşabilir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-319">You can exceed some template limits by using a nested template.</span></span> <span data-ttu-id="ca1d1-320">Daha fazla bilgi için bkz: [Azure kaynaklarını dağıtırken bağlı şablonları kullanma](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ca1d1-320">For more information, see [Using linked templates when deploying Azure resources](resource-group-linked-templates.md).</span></span> <span data-ttu-id="ca1d1-321">tooreduce hello numarası parametreleri, değişkenleri veya çıkışları, değerlerden bir nesnesinde birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-321">tooreduce hello number of parameters, variables, or outputs, you can combine several values into an object.</span></span> <span data-ttu-id="ca1d1-322">Daha fazla bilgi için bkz: [nesneleri parametreleri olarak](resource-manager-objects-as-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="ca1d1-322">For more information, see [Objects as parameters](resource-manager-objects-as-parameters.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca1d1-323">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ca1d1-323">Next steps</span></span>
* <span data-ttu-id="ca1d1-324">tooview tam şablonları farklı türlerde çözümler için bkz: hello [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="ca1d1-324">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="ca1d1-325">Kullanabileceğiniz gelen bir şablonda hello işlevleri hakkında daha fazla ayrıntı için bkz: [Azure Resource Manager şablonu işlevleri](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="ca1d1-325">For details about hello functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="ca1d1-326">dağıtım işlemi sırasında birden fazla şablon toocombine bkz [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ca1d1-326">toocombine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="ca1d1-327">Farklı bir kaynak grubu içinde mevcut toouse kaynakları gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-327">You may need toouse resources that exist within a different resource group.</span></span> <span data-ttu-id="ca1d1-328">Bu senaryo, depolama hesapları veya birden çok kaynak grupları arasında paylaşılan sanal ağlar ile çalışırken yaygındır.</span><span class="sxs-lookup"><span data-stu-id="ca1d1-328">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="ca1d1-329">Daha fazla bilgi için bkz: Merhaba [ResourceId işlevi](resource-group-template-functions-resource.md#resourceid).</span><span class="sxs-lookup"><span data-stu-id="ca1d1-329">For more information, see hello [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
