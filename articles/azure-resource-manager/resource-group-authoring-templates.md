---
title: "Azure Resource Manager şablonu yapısı ve sözdizimi | Microsoft Docs"
description: "Yapı ve bildirim temelli JSON sözdizimini kullanarak Azure Resource Manager şablonları özelliklerini açıklar."
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
ms.openlocfilehash: dc9b64062d7f68c83aa090eec96744819a5ca423
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-the-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="1d4b1-103">Yapı ve Azure Resource Manager şablonları sözdizimi anlama</span><span class="sxs-lookup"><span data-stu-id="1d4b1-103">Understand the structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="1d4b1-104">Bu konu, bir Azure Resource Manager şablonu yapısını açıklar.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-104">This topic describes the structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="1d4b1-105">Bir şablon ve bu bölümlerdeki özellikler farklı bölümlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-105">It presents the different sections of a template and the properties that are available in those sections.</span></span> <span data-ttu-id="1d4b1-106">JSON ve dağıtımınız için değerleri oluşturmada kullanabileceğiniz ifadeler, şablon oluşur.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="1d4b1-107">Şablon oluşturmanın adım adım öğretici için bkz [, ilk Azure Resource Manager şablonu oluşturma](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="1d4b1-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

## <a name="template-format"></a><span data-ttu-id="1d4b1-108">Şablon biçimi</span><span class="sxs-lookup"><span data-stu-id="1d4b1-108">Template format</span></span>
<span data-ttu-id="1d4b1-109">En basit yapısını şablon aşağıdaki öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="1d4b1-109">In its simplest structure, a template contains the following elements:</span></span>

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

| <span data-ttu-id="1d4b1-110">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="1d4b1-110">Element name</span></span> | <span data-ttu-id="1d4b1-111">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1d4b1-111">Required</span></span> | <span data-ttu-id="1d4b1-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1d4b1-112">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1d4b1-113">$schema</span><span class="sxs-lookup"><span data-stu-id="1d4b1-113">$schema</span></span> |<span data-ttu-id="1d4b1-114">Evet</span><span class="sxs-lookup"><span data-stu-id="1d4b1-114">Yes</span></span> |<span data-ttu-id="1d4b1-115">Şablon dili sürümü açıklanmaktadır JSON Şeması dosyasının konumu.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-115">Location of the JSON schema file that describes the version of the template language.</span></span> <span data-ttu-id="1d4b1-116">Önceki örnekte gösterilen URL'yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-116">Use the URL shown in the preceding example.</span></span> |
| <span data-ttu-id="1d4b1-117">contentVersion</span><span class="sxs-lookup"><span data-stu-id="1d4b1-117">contentVersion</span></span> |<span data-ttu-id="1d4b1-118">Evet</span><span class="sxs-lookup"><span data-stu-id="1d4b1-118">Yes</span></span> |<span data-ttu-id="1d4b1-119">Şablon (örneğin, 1.0.0.0) sürümü.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-119">Version of the template (such as 1.0.0.0).</span></span> <span data-ttu-id="1d4b1-120">Bu öğe için herhangi bir değer sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-120">You can provide any value for this element.</span></span> <span data-ttu-id="1d4b1-121">Şablonu kullanarak kaynak dağıtırken, bu değer doğru şablonu kullanılmakta olduğunu emin olmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-121">When deploying resources using the template, this value can be used to make sure that the right template is being used.</span></span> |
| <span data-ttu-id="1d4b1-122">Parametreleri</span><span class="sxs-lookup"><span data-stu-id="1d4b1-122">parameters</span></span> |<span data-ttu-id="1d4b1-123">Hayır</span><span class="sxs-lookup"><span data-stu-id="1d4b1-123">No</span></span> |<span data-ttu-id="1d4b1-124">Dağıtım kaynağı dağıtım özelleştirmek için yürütüldüğünde, sağlanan değerler.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-124">Values that are provided when deployment is executed to customize resource deployment.</span></span> |
| <span data-ttu-id="1d4b1-125">değişkenleri</span><span class="sxs-lookup"><span data-stu-id="1d4b1-125">variables</span></span> |<span data-ttu-id="1d4b1-126">Hayır</span><span class="sxs-lookup"><span data-stu-id="1d4b1-126">No</span></span> |<span data-ttu-id="1d4b1-127">Şablondaki JSON parçaları olarak şablon dili ifadeleri basitleştirmek için kullanılan değerler.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-127">Values that are used as JSON fragments in the template to simplify template language expressions.</span></span> |
| <span data-ttu-id="1d4b1-128">Kaynakları</span><span class="sxs-lookup"><span data-stu-id="1d4b1-128">resources</span></span> |<span data-ttu-id="1d4b1-129">Evet</span><span class="sxs-lookup"><span data-stu-id="1d4b1-129">Yes</span></span> |<span data-ttu-id="1d4b1-130">Dağıtılan veya bir kaynak grubunda güncelleştirilmiş kaynak türleri.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-130">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="1d4b1-131">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="1d4b1-131">outputs</span></span> |<span data-ttu-id="1d4b1-132">Hayır</span><span class="sxs-lookup"><span data-stu-id="1d4b1-132">No</span></span> |<span data-ttu-id="1d4b1-133">Dağıtımdan sonra döndürülen değer.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-133">Values that are returned after deployment.</span></span> |

<span data-ttu-id="1d4b1-134">Her öğe ayarlayabileceğiniz özellikler içerir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-134">Each element contains properties you can set.</span></span> <span data-ttu-id="1d4b1-135">Aşağıdaki örnek, bir şablon için tam söz dizimi içerir:</span><span class="sxs-lookup"><span data-stu-id="1d4b1-135">The following example contains the full syntax for a template:</span></span>

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
                "description": "<description-of-the parameter>" 
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

<span data-ttu-id="1d4b1-136">Bu konunun ilerleyen bölümlerinde daha ayrıntılı şablon bölümlerini inceleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-136">We examine the sections of the template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="1d4b1-137">İfadeler ve işlevleri</span><span class="sxs-lookup"><span data-stu-id="1d4b1-137">Expressions and functions</span></span>
<span data-ttu-id="1d4b1-138">Şablonun temel sözdizimi JSON şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-138">The basic syntax of the template is JSON.</span></span> <span data-ttu-id="1d4b1-139">Ancak, ifadeler ve işlevleri şablonu içinde kullanılabilir olan JSON değerlerin genişletir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-139">However, expressions and functions extend the JSON values available within the template.</span></span>  <span data-ttu-id="1d4b1-140">İfadeler, ilk JSON dize değişmez değerleri içinde yazılır ve son karakterler olan ayraçlar: `[` ve `]`sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-140">Expressions are written within JSON string literals whose first and last characters are the brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="1d4b1-141">Şablon dağıtıldığında ifade değeri değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-141">The value of the expression is evaluated when the template is deployed.</span></span> <span data-ttu-id="1d4b1-142">Bir dize yazılmış olsa da, ifade değerlendirme sonucu gibi bir dizi veya tamsayı, gerçek ifade bağlı olarak farklı bir JSON türde olabilir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-142">While written as a string literal, the result of evaluating the expression can be of a different JSON type, such as an array or integer, depending on the actual expression.</span></span>  <span data-ttu-id="1d4b1-143">Başlangıç noktası ile sabit değerli bir dize olması `[`, ancak olmayan bir ifade olarak yorumlanır olması, dizesiyle başlatmak için ek bir köşeli ayraç eklemek `[[`.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-143">To have a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket to start the string with `[[`.</span></span>

<span data-ttu-id="1d4b1-144">Genellikle, ifadeler işlevleriyle dağıtım yapılandırma işlemleri gerçekleştirmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-144">Typically, you use expressions with functions to perform operations for configuring the deployment.</span></span> <span data-ttu-id="1d4b1-145">JavaScript'te, işlev çağrıları olarak biçimlendirilmiş gibi yalnızca `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-145">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="1d4b1-146">Nokta ve [dizin] işleçleri kullanarak özellikleri başvuru.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-146">You reference properties by using the dot and [index] operators.</span></span>

<span data-ttu-id="1d4b1-147">Aşağıdaki örnek değerleri oluşturulurken, çeşitli işlevleri kullanmayı gösterir:</span><span class="sxs-lookup"><span data-stu-id="1d4b1-147">The following example shows how to use several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="1d4b1-148">Şablon işlevleri tam listesi için bkz: [Azure Resource Manager şablonu işlevleri](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="1d4b1-148">For the full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="1d4b1-149">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1d4b1-149">Parameters</span></span>
<span data-ttu-id="1d4b1-150">Şablon parametreleri bölümünde kaynakları dağıtırken giriş hangi değerlerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-150">In the parameters section of the template, you specify which values you can input when deploying the resources.</span></span> <span data-ttu-id="1d4b1-151">Bu parametre değerleri (örneğin, geliştirme, test ve üretim) belirli bir ortam için uyarlanabilir değerleri sağlayarak dağıtım özelleştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-151">These parameter values enable you to customize the deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="1d4b1-152">Şablonunuzdaki parametreleri sağlamak zorunda değildir, ancak parametre olmadan şablonunuzu her zaman aynı kaynakları adları, konumları ve özellikleri ile dağıtmak için kullanacağınız.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-152">You do not have to provide parameters in your template, but without parameters your template would always deploy the same resources with the same names, locations, and properties.</span></span>

<span data-ttu-id="1d4b1-153">Şu yapıda parametrelerini tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="1d4b1-153">You define parameters with the following structure:</span></span>

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
            "description": "<description-of-the parameter>" 
        }
    }
}
```

| <span data-ttu-id="1d4b1-154">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="1d4b1-154">Element name</span></span> | <span data-ttu-id="1d4b1-155">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1d4b1-155">Required</span></span> | <span data-ttu-id="1d4b1-156">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1d4b1-156">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1d4b1-157">parameterName</span><span class="sxs-lookup"><span data-stu-id="1d4b1-157">parameterName</span></span> |<span data-ttu-id="1d4b1-158">Evet</span><span class="sxs-lookup"><span data-stu-id="1d4b1-158">Yes</span></span> |<span data-ttu-id="1d4b1-159">Parametrenin adı.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-159">Name of the parameter.</span></span> <span data-ttu-id="1d4b1-160">Geçerli bir JavaScript tanımlayıcı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-160">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="1d4b1-161">type</span><span class="sxs-lookup"><span data-stu-id="1d4b1-161">type</span></span> |<span data-ttu-id="1d4b1-162">Evet</span><span class="sxs-lookup"><span data-stu-id="1d4b1-162">Yes</span></span> |<span data-ttu-id="1d4b1-163">Parametre değeri türü.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-163">Type of the parameter value.</span></span> <span data-ttu-id="1d4b1-164">İzin verilen türleri listesini sonra bu tabloya bakın.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-164">See the list of allowed types after this table.</span></span> |
| <span data-ttu-id="1d4b1-165">defaultValue</span><span class="sxs-lookup"><span data-stu-id="1d4b1-165">defaultValue</span></span> |<span data-ttu-id="1d4b1-166">Hayır</span><span class="sxs-lookup"><span data-stu-id="1d4b1-166">No</span></span> |<span data-ttu-id="1d4b1-167">Parametresi için hiçbir değer sağlanmazsa parametre için varsayılan değer.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-167">Default value for the parameter, if no value is provided for the parameter.</span></span> |
| <span data-ttu-id="1d4b1-168">allowedValues</span><span class="sxs-lookup"><span data-stu-id="1d4b1-168">allowedValues</span></span> |<span data-ttu-id="1d4b1-169">Hayır</span><span class="sxs-lookup"><span data-stu-id="1d4b1-169">No</span></span> |<span data-ttu-id="1d4b1-170">Doğru değeri sağlandığından emin olmak parametresi için izin verilen değerleri dizisi.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-170">Array of allowed values for the parameter to make sure that the right value is provided.</span></span> |
| <span data-ttu-id="1d4b1-171">MinValue</span><span class="sxs-lookup"><span data-stu-id="1d4b1-171">minValue</span></span> |<span data-ttu-id="1d4b1-172">Hayır</span><span class="sxs-lookup"><span data-stu-id="1d4b1-172">No</span></span> |<span data-ttu-id="1d4b1-173">İnt türü parametreler için minimum değeri, bu kapsayıcı değerdir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-173">The minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="1d4b1-174">MaxValue</span><span class="sxs-lookup"><span data-stu-id="1d4b1-174">maxValue</span></span> |<span data-ttu-id="1d4b1-175">Hayır</span><span class="sxs-lookup"><span data-stu-id="1d4b1-175">No</span></span> |<span data-ttu-id="1d4b1-176">İnt türü parametreleri için maksimum değeri, bu kapsayıcı değerdir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-176">The maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="1d4b1-177">minLength</span><span class="sxs-lookup"><span data-stu-id="1d4b1-177">minLength</span></span> |<span data-ttu-id="1d4b1-178">Hayır</span><span class="sxs-lookup"><span data-stu-id="1d4b1-178">No</span></span> |<span data-ttu-id="1d4b1-179">Dize, secureString ve dizi türü parametreler için minimum uzunluk, bu kapsayıcı değerdir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-179">The minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="1d4b1-180">maxLength</span><span class="sxs-lookup"><span data-stu-id="1d4b1-180">maxLength</span></span> |<span data-ttu-id="1d4b1-181">Hayır</span><span class="sxs-lookup"><span data-stu-id="1d4b1-181">No</span></span> |<span data-ttu-id="1d4b1-182">Dize, secureString ve dizi türü parametreleri için en fazla uzunluk, bu kapsayıcı değerdir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-182">The maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="1d4b1-183">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1d4b1-183">description</span></span> |<span data-ttu-id="1d4b1-184">Hayır</span><span class="sxs-lookup"><span data-stu-id="1d4b1-184">No</span></span> |<span data-ttu-id="1d4b1-185">Portal aracılığıyla kullanıcılara görüntülenen parametre açıklaması.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-185">Description of the parameter that is displayed to users through the portal.</span></span> |

<span data-ttu-id="1d4b1-186">İzin verilen türleri ve değerleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1d4b1-186">The allowed types and values are:</span></span>

* <span data-ttu-id="1d4b1-187">**dize**</span><span class="sxs-lookup"><span data-stu-id="1d4b1-187">**string**</span></span>
* <span data-ttu-id="1d4b1-188">**secureString**</span><span class="sxs-lookup"><span data-stu-id="1d4b1-188">**secureString**</span></span>
* <span data-ttu-id="1d4b1-189">**int**</span><span class="sxs-lookup"><span data-stu-id="1d4b1-189">**int**</span></span>
* <span data-ttu-id="1d4b1-190">**bool**</span><span class="sxs-lookup"><span data-stu-id="1d4b1-190">**bool**</span></span>
* <span data-ttu-id="1d4b1-191">**Nesne**</span><span class="sxs-lookup"><span data-stu-id="1d4b1-191">**object**</span></span> 
* <span data-ttu-id="1d4b1-192">**secureObject**</span><span class="sxs-lookup"><span data-stu-id="1d4b1-192">**secureObject**</span></span>
* <span data-ttu-id="1d4b1-193">**dizi**</span><span class="sxs-lookup"><span data-stu-id="1d4b1-193">**array**</span></span>

<span data-ttu-id="1d4b1-194">Parametre isteğe bağlı olarak belirtmek için (boş bir dize olabilir) bir defaultValue sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-194">To specify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="1d4b1-195">Şablonunuzdaki şablonu dağıtmak için komut bir parametre ile eşleşen bir parametre adı belirtirseniz, olası karışıklığı sağladığınız değerleri hakkında yoktur.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-195">If you specify a parameter name in your template that matches a parameter in the command to deploy the template, there is potential ambiguity about the values you provide.</span></span> <span data-ttu-id="1d4b1-196">Resource Manager sonek ekleyerek bu karışıklığı çözümler **FromTemplate** şablon parametresi için.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-196">Resource Manager resolves this confusion by adding the postfix **FromTemplate** to the template parameter.</span></span> <span data-ttu-id="1d4b1-197">Örneğin, adlı bir parametre dahil ederseniz **ResourceGroupName** ile çakıştığı şablonunuzda, **ResourceGroupName** parametresinde [New-AzureRmResourceGroupDeployment ](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-197">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="1d4b1-198">Dağıtım sırasında için bir değer sağlamanız istenir **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-198">During deployment, you are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="1d4b1-199">Genel olarak, Karışıklığı önlemek için bu parametreleri dağıtım işlemleri için kullanılan parametreleri aynı ada sahip adlandırılmasıyla değil kaçınmalısınız.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-199">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="1d4b1-200">Tüm parolalar, anahtarlar ve diğer parolaları kullanması gereken **secureString** türü.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-200">All passwords, keys, and other secrets should use the **secureString** type.</span></span> <span data-ttu-id="1d4b1-201">Bir JSON nesnesinde hassas verileri geçirdiğiniz kullanırsanız **secureObject** türü.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-201">If you pass sensitive data in a JSON object, use the **secureObject** type.</span></span> <span data-ttu-id="1d4b1-202">Şablon parametreleri secureString veya secureObject türleriyle kaynak dağıtımdan sonra okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-202">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="1d4b1-203">Örneğin, dağıtım geçmişi dosyasında şu girişi değeri bir dize ve nesne için kullanılabilir ancak secureString ve secureObject gösterir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-203">For example, the following entry in the deployment history shows the value for a string and object but not for secureString and secureObject.</span></span>
>
> ![Dağıtım değerlerini göster](./media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="1d4b1-205">Aşağıdaki örnek, parametreleri tanımlayan gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="1d4b1-205">The following example shows how to define parameters:</span></span>

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

<span data-ttu-id="1d4b1-206">Dağıtım sırasında parametre değerlerini giriş nasıl için [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="1d4b1-206">For how to input the parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="1d4b1-207">Değişkenler</span><span class="sxs-lookup"><span data-stu-id="1d4b1-207">Variables</span></span>
<span data-ttu-id="1d4b1-208">Değişkenler bölümünde şablonunuzu kullanılabilir değerleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-208">In the variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="1d4b1-209">Değişkenleri tanımlayın gerekmez, ancak bunlar karmaşık ifadeler azaltarak genellikle şablonunuzu basitleştirin.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-209">You do not need to define variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="1d4b1-210">Şu yapıda değişkenleri tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="1d4b1-210">You define variables with the following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="1d4b1-211">Aşağıdaki örnekte, iki parametre değerlerinin oluşturulan bir değişkeni tanımlamak gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="1d4b1-211">The following example shows how to define a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="1d4b1-212">Sonraki örnek karmaşık bir JSON türe sahip bir değişken ve diğer değişkenlerinden oluşturulan değişkenleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="1d4b1-212">The next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

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

## <a name="resources"></a><span data-ttu-id="1d4b1-213">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="1d4b1-213">Resources</span></span>
<span data-ttu-id="1d4b1-214">Kaynaklar bölümünde dağıtılan veya güncelleştirilen kaynakları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-214">In the resources section, you define the resources that are deployed or updated.</span></span> <span data-ttu-id="1d4b1-215">Sağ değerlerini sağlamak için dağıtıyorsanız türlerini anlamanız gerekir çünkü bu bölümde karmaşık elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-215">This section can get complicated because you must understand the types you are deploying to provide the right values.</span></span> <span data-ttu-id="1d4b1-216">Ayarlamak için gereken kaynak özgü değerleri için (apiVersion, türü ve özellikleri), bkz: [kaynakları tanımlayan Azure Resource Manager şablonları](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="1d4b1-216">For the resource-specific values (apiVersion, type, and properties) that you need to set, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="1d4b1-217">Aşağıdaki Yapı kaynaklarını tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="1d4b1-217">You define resources with the following structure:</span></span>

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

| <span data-ttu-id="1d4b1-218">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="1d4b1-218">Element name</span></span> | <span data-ttu-id="1d4b1-219">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1d4b1-219">Required</span></span> | <span data-ttu-id="1d4b1-220">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1d4b1-220">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1d4b1-221">Koşul</span><span class="sxs-lookup"><span data-stu-id="1d4b1-221">condition</span></span> | <span data-ttu-id="1d4b1-222">Hayır</span><span class="sxs-lookup"><span data-stu-id="1d4b1-222">No</span></span> | <span data-ttu-id="1d4b1-223">Kaynak dağıtılabilir olup olmadığını gösteren Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-223">Boolean value that indicates whether the resource is deployed.</span></span> |
| <span data-ttu-id="1d4b1-224">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1d4b1-224">apiVersion</span></span> |<span data-ttu-id="1d4b1-225">Evet</span><span class="sxs-lookup"><span data-stu-id="1d4b1-225">Yes</span></span> |<span data-ttu-id="1d4b1-226">Kaynak oluşturmak için kullanmak için REST API sürümü.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-226">Version of the REST API to use for creating the resource.</span></span> |
| <span data-ttu-id="1d4b1-227">type</span><span class="sxs-lookup"><span data-stu-id="1d4b1-227">type</span></span> |<span data-ttu-id="1d4b1-228">Evet</span><span class="sxs-lookup"><span data-stu-id="1d4b1-228">Yes</span></span> |<span data-ttu-id="1d4b1-229">Kaynak türü.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-229">Type of the resource.</span></span> <span data-ttu-id="1d4b1-230">Bu değer, kaynak sağlayıcısı ve kaynak türü ad birleşimidir (gibi **Microsoft.Storage/storageAccounts**).</span><span class="sxs-lookup"><span data-stu-id="1d4b1-230">This value is a combination of the namespace of the resource provider and the resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="1d4b1-231">ad</span><span class="sxs-lookup"><span data-stu-id="1d4b1-231">name</span></span> |<span data-ttu-id="1d4b1-232">Evet</span><span class="sxs-lookup"><span data-stu-id="1d4b1-232">Yes</span></span> |<span data-ttu-id="1d4b1-233">Kaynağın adı.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-233">Name of the resource.</span></span> <span data-ttu-id="1d4b1-234">Ad RFC3986 içinde tanımlanan URI bileşeni kısıtlamaları izlemelidir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-234">The name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="1d4b1-235">Ayrıca, emin olmak için adı dışında tarafların doğrulamak için kaynak adı kullanıma Azure Hizmetleri değil başka bir kimlik aldatma girişimi.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-235">In addition, Azure services that expose the resource name to outside parties validate the name to make sure it is not an attempt to spoof another identity.</span></span> |
| <span data-ttu-id="1d4b1-236">location</span><span class="sxs-lookup"><span data-stu-id="1d4b1-236">location</span></span> |<span data-ttu-id="1d4b1-237">Değişir</span><span class="sxs-lookup"><span data-stu-id="1d4b1-237">Varies</span></span> |<span data-ttu-id="1d4b1-238">Sağlanan kaynak coğrafi konumda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-238">Supported geo-locations of the provided resource.</span></span> <span data-ttu-id="1d4b1-239">Kullanılabilir konumlardan herhangi birinden seçebilirsiniz, ancak genellikle kullanıcılarınızın yakın olan bir seçmek için mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-239">You can select any of the available locations, but typically it makes sense to pick one that is close to your users.</span></span> <span data-ttu-id="1d4b1-240">Genellikle, bu da aynı bölgede birbiriyle etkileşimde kaynakları yerleştirin mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-240">Usually, it also makes sense to place resources that interact with each other in the same region.</span></span> <span data-ttu-id="1d4b1-241">Çoğu kaynak türleri bir konum gerektirir, ancak bazı türleri (örneğin, bir rol ataması) bir konum gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-241">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="1d4b1-242">Bkz: [Azure Resource Manager şablonları kaynak konumunu ayarla](resource-manager-template-location.md).</span><span class="sxs-lookup"><span data-stu-id="1d4b1-242">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="1d4b1-243">etiketler</span><span class="sxs-lookup"><span data-stu-id="1d4b1-243">tags</span></span> |<span data-ttu-id="1d4b1-244">Hayır</span><span class="sxs-lookup"><span data-stu-id="1d4b1-244">No</span></span> |<span data-ttu-id="1d4b1-245">Kaynakla ilişkilendirilmiş etiketler.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-245">Tags that are associated with the resource.</span></span> <span data-ttu-id="1d4b1-246">Bkz: [Azure Resource Manager'da kaynakları etiketi](resource-manager-template-tags.md).</span><span class="sxs-lookup"><span data-stu-id="1d4b1-246">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="1d4b1-247">Açıklamaları</span><span class="sxs-lookup"><span data-stu-id="1d4b1-247">comments</span></span> |<span data-ttu-id="1d4b1-248">Hayır</span><span class="sxs-lookup"><span data-stu-id="1d4b1-248">No</span></span> |<span data-ttu-id="1d4b1-249">Şablonunuzda kaynaklar belgeleme için notları</span><span class="sxs-lookup"><span data-stu-id="1d4b1-249">Your notes for documenting the resources in your template</span></span> |
| <span data-ttu-id="1d4b1-250">Kopyalama</span><span class="sxs-lookup"><span data-stu-id="1d4b1-250">copy</span></span> |<span data-ttu-id="1d4b1-251">Hayır</span><span class="sxs-lookup"><span data-stu-id="1d4b1-251">No</span></span> |<span data-ttu-id="1d4b1-252">Birden fazla örneği gerekirse oluşturmak için kaynak sayısı.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-252">If more than one instance is needed, the number of resources to create.</span></span> <span data-ttu-id="1d4b1-253">Paralel varsayılan moddur.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-253">The default mode is parallel.</span></span> <span data-ttu-id="1d4b1-254">Tüm kullanmak istemiyorsanız, seri modu veya aynı anda dağıtmak amacıyla kaynaklarınızı belirtin.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-254">Specify serial mode when you do not want all or the resources to deploy at the same time.</span></span> <span data-ttu-id="1d4b1-255">Daha fazla bilgi için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="1d4b1-255">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="1d4b1-256">dependsOn</span><span class="sxs-lookup"><span data-stu-id="1d4b1-256">dependsOn</span></span> |<span data-ttu-id="1d4b1-257">Hayır</span><span class="sxs-lookup"><span data-stu-id="1d4b1-257">No</span></span> |<span data-ttu-id="1d4b1-258">Bu kaynak dağıtılmadan önce dağıtılmalıdır kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-258">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="1d4b1-259">Resource Manager kaynakları arasındaki bağımlılıkları değerlendirir ve doğru sırada dağıtır.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-259">Resource Manager evaluates the dependencies between resources and deploys them in the correct order.</span></span> <span data-ttu-id="1d4b1-260">Kaynakları birbirlerine bağımlı olmadıkları zaman bunların paralel olarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-260">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="1d4b1-261">Değer bir kaynağın virgülle ayrılmış bir liste olabilir adları veya kaynak benzersiz tanımlayıcıları.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-261">The value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="1d4b1-262">Yalnızca bu şablonda dağıtılan kaynakları listeler.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-262">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="1d4b1-263">Bu şablonda tanımlı değil kaynakları önceden var olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-263">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="1d4b1-264">Dağıtımınızı yavaş ve döngüsel bağımlılıklar oluşturma gibi gereksiz bağımlılıkları eklemekten kaçının.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-264">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="1d4b1-265">Bağımlılıklarını ayarlama hakkında yönergeler için bkz [Azure Resource Manager'da bağımlılıkları tanımlama](resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="1d4b1-265">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="1d4b1-266">properties</span><span class="sxs-lookup"><span data-stu-id="1d4b1-266">properties</span></span> |<span data-ttu-id="1d4b1-267">Hayır</span><span class="sxs-lookup"><span data-stu-id="1d4b1-267">No</span></span> |<span data-ttu-id="1d4b1-268">Kaynak özgü yapılandırma ayarları.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-268">Resource-specific configuration settings.</span></span> <span data-ttu-id="1d4b1-269">Özelliklerine ilişkin değerleri kaynak oluşturmak REST API işlemi için (PUT yöntemini) istek gövdesinde sağladığınız değerleri ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-269">The values for the properties are the same as the values you provide in the request body for the REST API operation (PUT method) to create the resource.</span></span> <span data-ttu-id="1d4b1-270">Ayrıca bir özelliği birden çok örneğini oluşturmak için bir kopya dizisi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-270">You can also specify a copy array to create multiple instances of a property.</span></span> <span data-ttu-id="1d4b1-271">Daha fazla bilgi için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="1d4b1-271">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="1d4b1-272">Kaynakları</span><span class="sxs-lookup"><span data-stu-id="1d4b1-272">resources</span></span> |<span data-ttu-id="1d4b1-273">Hayır</span><span class="sxs-lookup"><span data-stu-id="1d4b1-273">No</span></span> |<span data-ttu-id="1d4b1-274">Tanımlanan kaynağına bağımlı alt kaynakları.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-274">Child resources that depend on the resource being defined.</span></span> <span data-ttu-id="1d4b1-275">Yalnızca üst kaynak şema tarafından izin verilen kaynak türleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-275">Only provide resource types that are permitted by the schema of the parent resource.</span></span> <span data-ttu-id="1d4b1-276">Tam olarak nitelenmiş tür alt kaynağının üst kaynak türü gibi içerir **Microsoft.Web/sites/extensions**.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-276">The fully qualified type of the child resource includes the parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="1d4b1-277">Üst Kaynak bağımlılığı kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-277">Dependency on the parent resource is not implied.</span></span> <span data-ttu-id="1d4b1-278">Bu bağımlılık açıkça tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-278">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="1d4b1-279">Kaynaklar bölümünde dağıtmak amacıyla kaynaklarınızı dizisi içerir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-279">The resources section contains an array of the resources to deploy.</span></span> <span data-ttu-id="1d4b1-280">Her kaynak içinde bir dizi alt kaynakları da tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-280">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="1d4b1-281">Bu nedenle, kaynakları bölümünüzü gibi bir yapıya sahip:</span><span class="sxs-lookup"><span data-stu-id="1d4b1-281">Therefore, your resources section could have a structure like:</span></span>

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

<span data-ttu-id="1d4b1-282">Alt kaynakları tanımlama hakkında daha fazla bilgi için bkz: [Resource Manager şablonunda alt kaynak için ad ve tür ayarlamak](resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="1d4b1-282">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

<span data-ttu-id="1d4b1-283">**Koşulu** öğesi kaynak dağıtılabilir olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-283">The **condition** element specifies whether the resource is deployed.</span></span> <span data-ttu-id="1d4b1-284">Bu öğe için değer true veya false değerine çözümler.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-284">The value for this element resolves to true or false.</span></span> <span data-ttu-id="1d4b1-285">Örneğin, yeni bir depolama hesabı dağıtılabilir olup olmadığını belirtmek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="1d4b1-285">For example, to specify whether a new storage account is deployed, use:</span></span>

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

<span data-ttu-id="1d4b1-286">Yeni veya mevcut bir kaynağı kullanarak bir örnek için bkz: [yeni veya varolan bir koşul şablonu](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="1d4b1-286">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="1d4b1-287">Bir sanal makine bir parola veya SSH anahtarı ile birlikte dağıtılabilir olup olmadığını belirlemek için iki sürümünü sanal makine, şablon ve kullanım tanımlama **koşulu** kullanım ayırt etmek için.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-287">To specify whether a virtual machine is deployed with a password or SSH key, define two versions of the virtual machine in your template and use **condition** to differentiate usage.</span></span> <span data-ttu-id="1d4b1-288">Dağıtmak için hangi senaryonun belirten bir parametre geçirin.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-288">Pass a parameter that specifies which scenario to deploy.</span></span>

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

<span data-ttu-id="1d4b1-289">Sanal makineyi dağıtmak için bir parola veya SSH anahtarı kullanarak bir örnek için bkz: [kullanıcı adı veya SSH koşul şablon](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="1d4b1-289">For an example of using a password or SSH key to deploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="outputs"></a><span data-ttu-id="1d4b1-290">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="1d4b1-290">Outputs</span></span>
<span data-ttu-id="1d4b1-291">Çıkış bölümünde dağıtımından döndürülen değerlerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-291">In the Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="1d4b1-292">Örneğin, dağıtılan bir kaynağa erişmek için URI döndürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-292">For example, you could return the URI to access a deployed resource.</span></span>

<span data-ttu-id="1d4b1-293">Aşağıdaki örnek bir çıktı tanımının yapısını gösterir:</span><span class="sxs-lookup"><span data-stu-id="1d4b1-293">The following example shows the structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="1d4b1-294">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="1d4b1-294">Element name</span></span> | <span data-ttu-id="1d4b1-295">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1d4b1-295">Required</span></span> | <span data-ttu-id="1d4b1-296">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1d4b1-296">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1d4b1-297">outputName</span><span class="sxs-lookup"><span data-stu-id="1d4b1-297">outputName</span></span> |<span data-ttu-id="1d4b1-298">Evet</span><span class="sxs-lookup"><span data-stu-id="1d4b1-298">Yes</span></span> |<span data-ttu-id="1d4b1-299">Çıkış değeri adı.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-299">Name of the output value.</span></span> <span data-ttu-id="1d4b1-300">Geçerli bir JavaScript tanımlayıcı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-300">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="1d4b1-301">type</span><span class="sxs-lookup"><span data-stu-id="1d4b1-301">type</span></span> |<span data-ttu-id="1d4b1-302">Evet</span><span class="sxs-lookup"><span data-stu-id="1d4b1-302">Yes</span></span> |<span data-ttu-id="1d4b1-303">Çıktı değerin türü.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-303">Type of the output value.</span></span> <span data-ttu-id="1d4b1-304">Şablon giriş parametreleri aynı türlerine çıkış değerlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-304">Output values support the same types as template input parameters.</span></span> |
| <span data-ttu-id="1d4b1-305">değer</span><span class="sxs-lookup"><span data-stu-id="1d4b1-305">value</span></span> |<span data-ttu-id="1d4b1-306">Evet</span><span class="sxs-lookup"><span data-stu-id="1d4b1-306">Yes</span></span> |<span data-ttu-id="1d4b1-307">Hesaplanan ve çıktı değeri olarak döndürülen şablon dili ifadesi.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-307">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="1d4b1-308">Aşağıdaki örnek çıkış bölümünde döndürülen bir değer gösterir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-308">The following example shows a value that is returned in the Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="1d4b1-309">Çıktı ile çalışma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları durumda paylaşımı](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="1d4b1-309">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="template-limits"></a><span data-ttu-id="1d4b1-310">Şablon sınırları</span><span class="sxs-lookup"><span data-stu-id="1d4b1-310">Template limits</span></span>

<span data-ttu-id="1d4b1-311">Şablonunuzu 1 MB ve her parametre dosyası 64 KB boyutu sınırı.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-311">Limit the size of your template to 1 MB, and each parameter file to 64 KB.</span></span> <span data-ttu-id="1d4b1-312">Yinelemeli Kaynak tanımları ve değişkenleri ve parametreleri için değerler ile genişletilmiştir sonra 1 MB sınırını şablonunun son durumuna uygulanır.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-312">The 1-MB limit applies to the final state of the template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

<span data-ttu-id="1d4b1-313">Ayrıca için sınırlıdır:</span><span class="sxs-lookup"><span data-stu-id="1d4b1-313">You are also limited to:</span></span>

* <span data-ttu-id="1d4b1-314">256 parametreleri</span><span class="sxs-lookup"><span data-stu-id="1d4b1-314">256 parameters</span></span>
* <span data-ttu-id="1d4b1-315">256 değişkenleri</span><span class="sxs-lookup"><span data-stu-id="1d4b1-315">256 variables</span></span>
* <span data-ttu-id="1d4b1-316">800 kaynakları (kopya sayısı dahil)</span><span class="sxs-lookup"><span data-stu-id="1d4b1-316">800 resources (including copy count)</span></span>
* <span data-ttu-id="1d4b1-317">64 çıkış değerleri</span><span class="sxs-lookup"><span data-stu-id="1d4b1-317">64 output values</span></span>
* <span data-ttu-id="1d4b1-318">bir şablon ifadesinde 24.576 karakterleri</span><span class="sxs-lookup"><span data-stu-id="1d4b1-318">24,576 characters in a template expression</span></span>

<span data-ttu-id="1d4b1-319">İç içe geçmiş bir şablon kullanarak bazı şablonu sınırı aşabilir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-319">You can exceed some template limits by using a nested template.</span></span> <span data-ttu-id="1d4b1-320">Daha fazla bilgi için bkz: [Azure kaynaklarını dağıtırken bağlı şablonları kullanma](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1d4b1-320">For more information, see [Using linked templates when deploying Azure resources](resource-group-linked-templates.md).</span></span> <span data-ttu-id="1d4b1-321">Parametreler, değişkenleri veya çıkışları sayısını azaltmak için değerlerden bir nesnede birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-321">To reduce the number of parameters, variables, or outputs, you can combine several values into an object.</span></span> <span data-ttu-id="1d4b1-322">Daha fazla bilgi için bkz: [nesneleri parametreleri olarak](resource-manager-objects-as-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="1d4b1-322">For more information, see [Objects as parameters](resource-manager-objects-as-parameters.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d4b1-323">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1d4b1-323">Next steps</span></span>
* <span data-ttu-id="1d4b1-324">Farklı türlerde çözümler için tam şablonları görüntülemek üzere bkz. [Azure Hızlı Başlangıç Şablonları](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="1d4b1-324">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="1d4b1-325">Kullanabileceğiniz gelen bir şablonda işlevleri hakkında daha fazla ayrıntı için bkz: [Azure Resource Manager şablonu işlevleri](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="1d4b1-325">For details about the functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="1d4b1-326">Birden fazla şablon dağıtımı sırasında birleştirmek için bkz: [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1d4b1-326">To combine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="1d4b1-327">Farklı bir kaynak grubu içinde mevcut kaynakları kullanmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-327">You may need to use resources that exist within a different resource group.</span></span> <span data-ttu-id="1d4b1-328">Bu senaryo, depolama hesapları veya birden çok kaynak grupları arasında paylaşılan sanal ağlar ile çalışırken yaygındır.</span><span class="sxs-lookup"><span data-stu-id="1d4b1-328">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="1d4b1-329">Daha fazla bilgi için bkz: [ResourceId işlevi](resource-group-template-functions-resource.md#resourceid).</span><span class="sxs-lookup"><span data-stu-id="1d4b1-329">For more information, see the [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
